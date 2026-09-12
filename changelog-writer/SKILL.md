---
name: changelog-writer
description: Write clear, concise, user friendly changelog entries for software updates, based on openspec change details and implementation progress, having the proposal, design and taks as context.
license: MIT
compatibility: No specific requirements.
metadata:
  author: Thiago Giovanella
  version: "2.0"
  generatedBy: "2.0"
---

## Implement changelog file for an OpenSpec change

**Input**: An OpenSpec change name or context indicating wich change must be documented. If vague or ambiguous you must prompt user asking for the specific change name.

**Restrictions**: The code change must be implemented before writing the changelog entry. If the code change is on git branch, the branch must be merged to main before writing the changelog entry.

The spec also needs to be archived and synced before writing the changelog entry, so the changelog can link to the archived spec.

**Steps**

1. Check if there is code change associated with the OpenSpec change. If there is no code change, inform the user that the changelog entry cannot be written until the code change is implemented.
2. Check if the spec is archived and synced. If not, inform the user that the changelog entry cannot be written until the spec is archived and synced.
3. If there are multiple changes, ask the user to specify which change they want to write the changelog entry for.
4. Once the specific change is identified, gather the necessary context from the proposal, design and tasks associated with the change to write a clear, concise and user friendly changelog entry.
5. Write the changelog entry, ensuring it is informative and easy to understand for users who may not be familiar with the technical details of the change. Include links to the archived spec and any relevant documentation or resources.
6. Give the user the steps to reproduce the change pointing the changed effects, actions or instructions the user may interact with, if applicable.
7. Write the changelog in Brazilian Portuguese for a better understanding of the users.
8. Save the changelog with a name formatted as `<change-name>.md` in the appropriate directory for changelogs in the project (the `<change-name>` slug must NOT include the `changelog-` prefix anymore).
9. The file MUST start with a YAML frontmatter block followed by markdown content. Do NOT include the title or the date in the body — both belong in frontmatter.
10. Use markdown formatting in the body (headings `###`, lists with `-` or `1.`, **bold**, paragraphs).

**Required frontmatter fields:**

- `slug`: kebab-case identifier matching the file name (without `.md`).
- `title`: human-readable release title in pt-BR.
- `date`: ISO date `YYYY-MM-DD` of the release.
- `archivedSpec` (optional): path to the archived spec folder, e.g. `openspec/changes/archive/2026-05-07-<change-name>`.

**Example of a changelog entry (`changelogs/multiplos-terapeutas.md`):**

```markdown
---
slug: multiplos-terapeutas
title: Múltiplos terapeutas
date: 2026-05-01
archivedSpec: openspec/changes/archive/2026-05-01-multiplos-terapeutas
---

Após revisão do processo de agendamento de consultas, é possível adicionar mais de um terapeuta para um mesmo agendamento. No formulário de cadastro do agendamento, use o campo "Adicionar terapeuta" para incluir os profissionais que participarão da consulta. Essa melhoria visa facilitar o agendamento de consultas em grupo e garantir que todos os terapeutas envolvidos sejam devidamente registrados.

### Como testar

1. Abra a tela de agendamento.
2. Use o campo "Adicionar terapeuta" para incluir um segundo profissional.
3. Salve e confirme que ambos aparecem no card do agendamento.
```

**Where to save the changelog file:**

The changelog file should be saved in the `changelogs` directory at the root of the project. If the directory does not exist, it should be created. The file name should follow the format `<change-name>.md`, where `<change-name>` is the OpenSpec change slug. This is the format consumed at build time by the in-app "Notas de versão" page (`/ajuda/notas-de-versao`), which renders each entry as a searchable accordion.
