---
name: improve-front-arch
description: Adapta e refatora módulos frontend para seguir o padrão arquitetural do Spott CMS baseado no módulo coupons. Use quando precisa reestruturar um módulo existente, criar novo módulo seguindo padrões estabelecidos, ou melhorar organização de código frontend.
---

# Improve Frontend Architecture

Adapta módulos frontend para seguir o padrão arquitetural estabelecido no Spott CMS (baseado no módulo coupons).

## Propósito

Padroniza a estrutura de módulos Next.js 14 do Spott CMS seguindo:
- Separação de concerns com hooks especializados
- Arquitetura de controllers e mutations
- Componentização reutilizável
- Tipagem TypeScript forte
- Organização previsível de arquivos

## Padrão de Referência: Coupons

O módulo `src/app/[lang]/(cms)/coupons` serve como blueprint.

### Estrutura de Diretórios

```
[src/app/[lang]/(cms)/{module}/]
├── page.tsx                    # Entry point mínimo
├── content.tsx                 # Lógica principal da página
├── layout.tsx                  # Layout específico (opcional)
├── types/
│   └── index.ts                # Types, interfaces, enums, keys
├── hooks/
│   ├── controllers/              # Hooks de leitura (React Query)
│   │   ├── useGet{Entity}Controller.tsx
│   │   └── useGet{Entity}DetailsController.tsx
│   ├── mutations/                # Hooks de escrita (React Query)
│   │   ├── useUpsert{Entity}Mutation.tsx
│   │   ├── useDelete{Entity}Mutation.tsx
│   │   └── useToggle{Entity}StatusMutation.tsx
│   └── options/                  # Configurações de UI
│       ├── get{Entity}Columns.tsx
│       └── get{Entity}CardTypeItems.tsx
├── form/
│   └── UpsertForm/
│       ├── index.tsx             # Form principal com react-hook-form
│       ├── index.const.ts        # Schemas Zod
│       └── {Field}Fieldset.tsx   # Fieldsets reutilizáveis
└── components/
    ├── Drawer/
    │   ├── Upsert{Entity}Drawer.tsx
    │   ├── Delete{Entity}Drawer.tsx
    │   └── {Entity}DetailsDrawer.tsx
    └── Chart/
        └── {Entity}Chart.tsx
```

### Convenções de Nomenclatura

| Tipo | Padrão | Exemplo |
|------|--------|---------|
| Controller | `useGet{Entity}Controller` | `useGetCouponsController` |
| Mutation | `use{Action}{Entity}Mutation` | `useUpsertCouponMutation` |
| Query Key | `{Action}_{ENTITY}` | `GET_COUPONS` |
| Type | `{Entity}Type` | `DiscountCouponType` |
| Fieldset | `{Field}Fieldset` | `DiscountNameFieldset` |

## Workflow de Adaptação

### 1. Análise do Módulo Atual

Antes de refatorar, entenda o estado atual:

- [ ] Onde está o módulo? (`src/app/[lang]/(cms)/{nome}`)
- [ ] Qual a funcionalidade principal?
- [ ] Quais entidades manipula?
- [ ] Que endpoints de API consome?
- [ ] Tem formulários? Quais campos?
- [ ] Precisa de drawers/modais?
- [ ] Exibe dados em tabela, cards ou ambos?

**Verifique padrões existentes:**
```bash
# Analisar módulo coupons como referência
cat src/app/[lang]/(cms)/coupons/content.tsx

# Ver estrutura de hooks
tree src/app/[lang]/(cms)/coupons/hooks

# Ver tipos
cat src/app/[lang]/(cms)/coupons/types/index.ts
```

### 2. Criar Estrutura Base

Crie a estrutura de diretórios:

```bash
mkdir -p src/app/[lang]/(cms)/{module}/{hooks/{controllers,mutations,options},form/UpsertForm,components/{Drawer,Chart},types}
touch src/app/[lang]/(cms)/{module}/page.tsx
touch src/app/[lang]/(cms)/{module}/content.tsx
touch src/app/[lang]/(cms)/{module}/types/index.ts
```

### 3. Definir Types (types/index.ts)

Baseado no padrão coupons, crie:

```typescript
// Query Keys
export enum {Entity}QueryKeys {
  GET_{ENTITIES} = 'GET_{ENTITIES}',
  GET_{ENTITY}_DETAILS = 'GET_{ENTITY}_DETAILS',
}

// Models
export interface {Entity} {
  id: string;
  // ... campos específicos
  status: {Entity}Status;
}

// Enums
export type {Entity}Status = 'active' | 'inactive' | 'pending';

// Requests
export type Upsert{Entity}Request = {
  // ... campos para POST/PUT
};

// Responses
export type Get{Entity}Response = {Entity};
export type GetAll{Entities}Response = PagedResult<{Entity}>;
```

### 4. Criar Controllers (hooks/controllers/)

Controller padrão para listagem:

```typescript
import { useQuery } from '@tanstack/react-query';
import api from '@/src/services/api';
import { {Entity}QueryKeys, GetAll{Entities}Response } from '../../types';

export interface Get{Entities}Params {
  page: number;
  pageSize: number;
  search?: string | null;
  // ... filtros específicos
}

const get{Entities} = async (params: Get{Entities}Params): Promise<GetAll{Entities}Response> => {
  const response = await api.get<GetAll{Entities}Response>('/{Endpoint}', {
    params,
  });
  return response.data ?? { items: [], totalCount: 0 };
};

export const useGet{Entities}Controller = (params: Get{Entities}Params) => {
  const query = useQuery<GetAll{Entities}Response>({
    queryKey: [{Entity}QueryKeys.GET_{ENTITIES}, params],
    queryFn: () => get{Entities}(params),
    keepPreviousData: true,
  });

  return {
    {entities}: query.data,
    isLoading{Entities}: query.isLoading,
    isFetching{Entities}: query.isFetching,
  };
};
```

### 5. Criar Mutations (hooks/mutations/)

Mutation padrão para upsert:

```typescript
import { useMutation, useQueryClient } from '@tanstack/react-query';
import { useTranslations } from 'next-intl';
import api from '@/src/services/api';
import { useToast } from '@/src/providers/toast';
import { {Entity}QueryKeys, Upsert{Entity}Request } from '../../types';

interface Upsert{Entity}Payload {
  id?: string;
  body: Upsert{Entity}Request;
}

const upsert{Entity} = async ({ id, body }: Upsert{Entity}Payload) => {
  if (id) {
    return await api.put(`/{Endpoint}/${id}`, body);
  }
  return await api.post('/{Endpoint}', body);
};

export const useUpsert{Entity}Mutation = () => {
  const t = useTranslations();
  const { addToast } = useToast();
  const queryClient = useQueryClient();

  const { mutateAsync: upsert{Entity}Async, isPending: isSaving } = useMutation({
    mutationFn: upsert{Entity},
    onSuccess: (response) => {
      const hasBusinessErrors = Array.isArray(response?.data?.errors);
      const isHttpSuccess = response?.status != null && response.status >= 200 && response.status < 300;

      if (isHttpSuccess && !hasBusinessErrors) {
        addToast({ success: true, title: t('page.{module}.success') });
      }

      queryClient.invalidateQueries({
        queryKey: [{Entity}QueryKeys.GET_{ENTITIES}],
      });
    },
    onError: () => {
      addToast({ success: false, title: t('page.{module}.error') });
    },
  });

  return { upsert{Entity}Async, isSaving };
};
```

### 6. Criar Options (hooks/options/)

Columns para DataTable:

```typescript
export const get{Entities}Columns = (
  t: ReturnType<typeof useTranslations>,
  lang: string,
  onEdit: (item: {Entity}) => void,
  onDelete: (item: {Entity}) => void,
) => [
  {
    accessorKey: 'name',
    header: t('page.{module}.columns.name'),
    cell: ({ row }) => row.original.name,
  },
  // ... outras colunas
  {
    id: 'actions',
    cell: ({ row }) => (
      <ActionsMenu
        onEdit={() => onEdit(row.original)}
        onDelete={() => onDelete(row.original)}
      />
    ),
  },
];
```

### 7. Criar Formulário (form/UpsertForm/)

Estrutura base do formulário:

```typescript
// index.const.ts
import { z } from 'zod';

export const upsert{Entity}FormSchema = (t: ReturnType<typeof useTranslations>) =>
  z.object({
    name: z.string().min(1, t('validation.required')),
    // ... outros campos
  });

// index.tsx
export const UpsertForm = ({ data, onCancel, onSave }: UpsertFormProps) => {
  const form = useForm<FormData>({
    resolver: zodResolver(upsert{Entity}FormSchema(t)),
    defaultValues: {
      // ... defaults
    },
  });

  // ... lógica do form com fieldsets
};
```

Fieldset reutilizável:

```typescript
// form/UpsertForm/NameFieldset.tsx
interface NameFieldsetProps {
  disabled?: boolean;
}

export const NameFieldset = ({ disabled }: NameFieldsetProps) => {
  const { register, formState: { errors } } = useFormContext();
  const t = useTranslations();

  return (
    <fieldset disabled={disabled}>
      <label>{t('page.{module}.form.name')}</label>
      <input {...register('name')} />
      {errors.name && <span>{errors.name.message}</span>}
    </fieldset>
  );
};
```

### 8. Criar Content Principal (content.tsx)

```typescript
'use client';

import { useState, useCallback, useMemo } from 'react';
import { useParams } from 'next/navigation';
import { useTranslations } from 'next-intl';
import { DataTable } from '@/src/components/DataTable/data-table';
import { Button } from '@/src/components/Button';

import { useGet{Entities}Controller } from './hooks/controllers/useGet{Entities}Controller';
import { get{Entities}Columns } from './hooks/options/get{Entities}Columns';
import { Upsert{Entity}Drawer } from './components/Drawer/Upsert{Entity}Drawer';

export const {Module}Content = () => {
  const t = useTranslations();
  const params = useParams();
  
  const [isUpsertDrawerOpen, setIsUpsertDrawerOpen] = useState(false);
  const [selectedItem, setSelectedItem] = useState<{Entity} | null>(null);
  const [currentPage, setCurrentPage] = useState(1);
  const [pageSize, setPageSize] = useState(10);

  const { {entities}, isLoading{Entities} } = useGet{Entities}Controller({
    page: currentPage,
    pageSize,
  });

  const handleEdit = useCallback((item: {Entity}) => {
    setSelectedItem(item);
    setIsUpsertDrawerOpen(true);
  }, []);

  const columns = useMemo(
    () => get{Entities}Columns(t, String(params.lang), handleEdit, handleDelete),
    [t, params.lang, handleEdit]
  );

  return (
    <div className="w-full">
      <Button onClick={() => setIsUpsertDrawerOpen(true)}>
        {t('page.{module}.new')}
      </Button>
      
      <DataTable
        columns={columns}
        data={filteredData}
        isLoading={isLoading{Entities}}
        serverSidePagination={{
          currentPage,
          totalPages,
          onPageChange: setCurrentPage,
        }}
      />
      
      <Upsert{Entity}Drawer
        isOpen={isUpsertDrawerOpen}
        onClose={() => setIsUpsertDrawerOpen(false)}
        data={selectedItem}
      />
    </div>
  );
};
```

### 9. Criar Page Entry (page.tsx)

```typescript
'use client';

import { {Module}Content } from './content';

export default function {Module}Page() {
  return <{Module}Content />;
}
```

## Checklist de Validação

Após refatoração, verifique:

- [ ] Estrutura de diretórios segue o padrão coupons
- [ ] Types centralizados em `types/index.ts`
- [ ] Controllers usam React Query com query keys
- [ ] Mutations invalidam queries após sucesso
- [ ] Forms usam react-hook-form + Zod
- [ ] Fieldsets são componentes reutilizáveis
- [ ] Content.tsx tem lógica de página, não de componentes
- [ ] Page.tsx é apenas entry point
- [ ] Nomenclatura segue convenções estabelecidas
- [ ] Imports absolutos usam `@/src/`
- [ ] Traduções em `useTranslations()`

## Anti-Patterns a Evitar

- ❌ Lógica de dados em componentes de UI
- ❌ Mutations sem invalidação de cache
- ❌ Types espalhados em múltiplos arquivos
- ❌ Hooks fazendo múltiplas responsabilidades
- ❌ Forms sem validação Zod
- ❌ Diretórios sem organização padrão
- ❌ Nomenclatura inconsistente
