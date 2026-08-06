# Workflow detalhado — git-commits-to-cv

Expandir estes passos quando o `SKILL.md` não bastar. Fonte de decisões: [agentic-career/context/cv-from-commits/CONTEXT.md](../../agentic-career/context/cv-from-commits/CONTEXT.md).

## 1. Coletar inputs

Perguntar o que faltar:

1. Caminho absoluto do **Scanned repository** (um repo git).
2. `company-slug` e `project-slug`.
3. **Commit Window**: período de emprego do projeto/empresa, **ou** `--since` / intervalo de datas fornecido pelo usuário.
4. Override opcional de **Target Role Bias** (default: Fullstack Engineer Pleno).
5. Override opcional de emails (include/exclude).

Validar que o path é um git repo:

```bash
git -C "<repo-path>" rev-parse --is-inside-work-tree
```

Definir path de saída:

```
c:\_git\projects\agentic-ai\.agents\skills\portfolio\agentic-career\output\experience\<company-slug>\<project-slug>.md
```

Se o arquivo já existir → planejar **Smart Merge** (seção 6). Caso contrário → criação limpa a partir do template.

## 2. Allowlist + discovery

Começar com defaults:

- `gabrielramador2014@gmail.com`
- `gabriel.amador@spott.eco`
- `amadorgabriel.dev@gmail.com`
- `gabriel.amador@etiquetacerta.com`

Aplicar overrides do usuário (include/exclude) **depois** da discovery.

Descobrir emails distintos:

```bash
git -C "<repo-path>" shortlog -se --all
git -C "<repo-path>" log --all --format='%ae' | sort -u
```

PowerShell (se `sort -u` não for GNU):

```powershell
git -C "<repo-path>" log --all --format='%ae' | Sort-Object -Unique
```

Para cada email **não** presente na allowlist efetiva (defaults + config de runs anteriores mencionadas no artefacto, se houver):

- Listar como **Discovered Collaborator Email**
- Perguntar: incluir nesta run? (sim/não)
- Não incluir automaticamente

Registrar a allowlist final nos metadados do artefacto.

## 3. Coletar commits no Commit Window

Montar `git log` com:

- `--since` / `--until` a partir do Commit Window
- um `--author=<email>` por email da allowlist final
- formato estável para clustering

```bash
git -C "<repo-path>" log \
  --since='YYYY-MM-DD' \
  --until='YYYY-MM-DD' \
  --author='email1@example.com' \
  --author='email2@example.com' \
  --pretty=format:'%h|%ad|%ae|%s' \
  --date=short
```

Sinais extras (opcional, por tema):

```bash
git -C "<repo-path>" log --since='YYYY-MM-DD' --author='...' --oneline --grep='migrate\|auth\|perf'
git -C "<repo-path>" log --since='YYYY-MM-DD' --author='...' --numstat --pretty=format:'COMMIT %h %s'
```

Se o volume for enorme: amostrar por mês ou por diretório (`-- path/`) após alinhar com o usuário — ainda um único scanned repo.

## 4. Agrupar em temas (não 1:1 com commits)

Ignorar ruído: typos, merge commits vazios, “fix lint”, bumps isolados de lockfile (salvo se forem o cerne de uma migração).

Preferir clusters:

| Tema | Sinais típicos |
| --- | --- |
| Features de produto | `feat`, novos módulos, rotas, telas |
| Migrações | framework upgrades, redesign de schema, monorepo splits |
| Performance | cache, lazy load, índices, profiling |
| Infra / CI/CD | Docker, pipelines, IaC, deploys |
| APIs / contratos | endpoints, OpenAPI, eventos, integrações |
| Auth / segurança | OAuth, JWT, RBAC, secrets |
| Dados | queries, EF migrations, Redis, analytics |

Mapear cada cluster → candidato a **uma** conquista (XYZ + STAR). Selecionar os **5–8** de maior impacto alinhados ao Target Role Bias.

Guardar amostra de hashes por tema para a seção de evidência.

## 5. Redigir Hybrid Artefact

1. Ler [methods.md](methods.md) e aplicar XYZ + STAR em PT-BR.
2. Preencher [artefact-template.md](artefact-template.md).
3. Toda métrica sem evidência → `[MÉTRICA A CONFIRMAR]` + item no Validation Checklist.
4. Perguntar Y interativamente **só** para bullets de topo sem medida.
5. Criar diretórios sob `agentic-career/output/experience/<company-slug>/` se necessário.
6. Escrever o arquivo `.md`.

**Não** editar `current_cv.md`. **Não** criar skill de Consolidation nesta run.

## 6. Smart Merge (re-run)

Quando o artefacto já existe:

1. Ler o arquivo atual por completo.
2. Identificar:
   - Métricas **confirmadas** (checklist marcado / notas explícitas / valores sem placeholder que o usuário validou)
   - Blocos **STAR** existentes
   - Bullets XYZ atuais
3. Diff implícito: nova evidência de commits vs bullets existentes.
4. **Atualizar** bullets quando houver evidência nova/mais forte.
5. **Preservar** métricas confirmadas e texto STAR salvo se a evidência não contradisser.
6. **Perguntar** só se ambíguo, por exemplo:
   - Dois bullets colidem e não dá para fundir sem perder claim confirmado
   - Nova evidência contradiz um Resultado STAR confirmado
   - Não está claro se um bullet antigo deve ser removido ou mantido no limite de 5–8
7. Atualizar metadados (`Última atualização`, emails, Commit Window, notas de merge).
8. Manter Validation Checklist sincronizado (remover itens confirmados; adicionar novos placeholders).

### Anti-padrões de merge

| Evitar | Fazer |
| --- | --- |
| Sobrescrever o arquivo inteiro | Mesclar seção a seção |
| Apagar STAR sem perguntar | Preservar; reescrever só com motivo |
| Trocar número confirmado por placeholder | Manter número; anotar evidência |
| Perguntar cada bullet | Perguntar só ambiguidades |

## 7. Encerrar a run

Resumir ao usuário:

- Path do artefacto escrito/atualizado
- Quantidade de XYZ bullets
- Emails incluídos / excluídos
- Itens abertos no Validation Checklist
- Lembrete: Consolidation em `current_cv.md` é passo futuro opcional (fora desta skill)
