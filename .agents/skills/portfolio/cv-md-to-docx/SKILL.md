---
name: cv-md-to-docx
description: >-
  Converte CVs markdown do summarize-cv (master_cv.md, master_cv.en.md ou
  master_cv.<job-slug>.md) em Word .docx pronto para envio, preenchendo o
  template DOCX versionado. Use when the user asks to gerar Word/DOCX do CV,
  exportar currículo para Word, MD → DOCX, preencher template do CV, or
  explicitly invokes cv-md-to-docx.
disable-model-invocation: true
---

# CV MD → DOCX

Copia o **template DOCX** canônico e preenche com o conteúdo de um CV markdown do `summarize-cv`, preservando layout/estilos do modelo (Times New Roman, seções em caixa alta, bullets).

Categoria: **portfolio** — ver [README da categoria](../README.md). Sibling de **`summarize-cv`** (mesmo critério de packaging que `git-commits-to-cv`: script + contrato I/O reutilizável).

## Formato: `.docx` (não `.docm`)

O pedido pode falar em “docm”; o artefacto do usuário é **`.docx`**. Esta skill gera **`.docx`** (sem macros). Só use `.docm` se um template macro-enabled for explicitamente necessário — o template atual não exige.

## When to run

Only on **explicit** invoke (`disable-model-invocation: true`).

Rodar **depois** de:

- **Consolidation** (`summarize-into-doc`) → `master_cv.md` / `master_cv.en.md`
- **adapt-cv-to-job** → `master_cv.<job-slug>.md`

Não faz parte do Pipeline A automático — passo de exportação sob demanda.

## Soft / Hard gates

Nenhum gate de goals. Confirmar apenas que o **arquivo markdown fonte** existe e é o desejado (master PT, EN ou tailored).

## Quick checklist

```
Skill run progress:
- [ ] 1. Confirmar input MD (path)
- [ ] 2. Garantir python-docx (`pip install -r scripts/requirements.txt`)
- [ ] 3. Rodar scripts/md_to_docx.py
- [ ] 4. Abrir o .docx gerado e spot-check seções
```

## Paths

| Artefacto | Path |
| --- | --- |
| Template PT (local, gitignored) | `assets/master_cv_pt_template.docx` |
| Template EN / en-US (local, gitignored) | `assets/master_cv_en_template.docx` |
| Script | `scripts/md_to_docx.py` |
| Regenerar template EN | `scripts/make_en_template.py` |
| Deps | `scripts/requirements.txt` (`python-docx`) |
| CVs MD (gitignored) | `../summarize-cv/output/cv/master_cv*.md` |
| DOCX gerados (gitignored) | `../summarize-cv/output/cv/master_cv*.docx` |

Cópia pessoal legada do template pode existir em `summarize-cv/output/cv/master_cv_pt_docx.docx` — **não** é a fonte canônica; use `assets/master_cv_pt_template.docx`.

### Naming de saída

| Input | Output (default, mesma pasta) |
| --- | --- |
| `master_cv.md` | `master_cv.docx` |
| `master_cv.en.md` | `master_cv.en.docx` |
| `master_cv.<job-slug>.md` | `master_cv.<job-slug>.docx` |

## Invoke

A partir da raiz desta skill (ou com paths absolutos):

```bash
pip install -r scripts/requirements.txt

python scripts/md_to_docx.py --input ../summarize-cv/output/cv/master_cv.md
python scripts/md_to_docx.py --input ../summarize-cv/output/cv/master_cv.en.md
```

O script infere o locale pelo filename (`master_cv.en.md` → EN) ou pelos headings (`## Contact`). Template e rótulos (SUMMARY / PROFESSIONAL EXPERIENCE, etc.) seguem o locale. Override:

```bash
python scripts/md_to_docx.py \
  --input ../summarize-cv/output/cv/master_cv.<job-slug>.md \
  --locale en \
  --template assets/master_cv_en_template.docx \
  --output ../summarize-cv/output/cv/master_cv.<job-slug>.docx
```

## O que o script faz

1. Lê o MD (ignora YAML frontmatter; ignora seções `JD Summary` / `Notas de consolidação`)
2. Abre o template, limpa o corpo, **mantém** styles/numbering/sectPr do modelo
3. Reescreve: nome, contato (2 linhas no padrão do template), RESUMO/SUMMARY, STACK, EXPERIÊNCIA, FORMAÇÃO, IDIOMAS (rótulos PT ou EN conforme locale)
4. Grava o `.docx` de saída

## Limitações

- Templates: **PT** (`master_cv_pt_template.docx`) e **EN / en-US** (`master_cv_en_template.docx`). O script escolhe o par template+rótulos pelo locale do MD.
- Bold pontual dentro de frases do template original não é recriado run-a-run; seções e cargos usam o padrão tipográfico do modelo.
- Github no contato só aparece se existir no MD.
- Não sincroniza Portfolio CV nem altera os masters markdown.

## Packaging note

Heavy reusable tooling + invocação independente para qualquer `master_cv*.md` → **sibling skill** (não reference module sob `summarize-cv/references/`).

## Cross-links

- [`summarize-cv`](../summarize-cv/SKILL.md) — pipeline que gera os MDs
- [summarize-into-doc](../summarize-cv/references/summarize-into-doc.md) — Consolidation
- [adapt-cv-to-job](../summarize-cv/references/adapt-cv-to-job.md) — Tailored CV
