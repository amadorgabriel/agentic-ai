# Session Workflow

**Trigger:** início de sessão de estudo, "próximo tópico", "continuar estudos"

## 1. Load context

1. Ler `output/progress.md` — criar a partir de [templates/progress.template.md](../templates/progress.template.md) se ausente
2. Se usuário mencionar vaga/JD: ler Tailored CV em `summarize-cv/output/cv/` ou seguir [jd-gap-analysis.md](jd-gap-analysis.md)
3. Se existir `summarize-cv/output/goals.md`, alinhar meta de carreira

## 2. Pick next topic

Regras:

- Preferir item `in_progress` antes de abrir novo
- Senão, primeiro `not_started` na fase atual (campo **Fase atual** em progress.md)
- Fases 0–2 são flexíveis — pular se progress mostrar `solid` nos pré-requisitos
- **Um** tópico por sessão
- Ignorar [DEFERRED.md](../DEFERRED.md) salvo pedido explícito

Anunciar: fase, tópico, por que agora, tempo estimado da sessão.

## 3. Conduct session

Estrutura sugerida (adaptar ao modo):

| Bloco | Duração | Conteúdo |
| --- | --- | --- |
| Recap | 5 min | O que é, por que importa para senior |
| Core | 20–40 min | Conceitos-chave, armadilhas comuns |
| Practice | 15–30 min | Exercício, snippet, ou pergunta de entrevista |
| Checkpoint | 5 min | 2–3 perguntas ou mini-desafio |

Carregar só a reference da fase atual (`phase-N-*.md`).

Para tópicos arquiteturais (System Design, DDD): oferecer a skill pessoal `grilling` antes de marcar `solid`.

Para prática extensa: sugerir a skill pessoal `tlc-spec-driven` com feature scoped ao tópico.

## 4. Update progress

Ao encerrar:

1. Atualizar status do tópico em `output/progress.md`
2. Se JD-driven: atualizar `output/study/plan.md`
3. Opcional: nota em `output/session-log/YYYY-MM-DD-<topico>.md`
4. Sugerir **um** tópico para a próxima sessão

## 5. CV bridge

Se tópico virou `solid` e houve projeto prático:

- Sugerir invocar `git-commits-to-cv` + `summarize-cv` para registrar experiência
- Não executar pipeline CV aqui

## Status transitions

```
not_started → in_progress → practice → solid
                ↓
            deferred (só itens de DEFERRED.md ou decisão explícita)
```

Não pular `practice` para tópicos hands-on (frameworks, ferramentas, IA).
