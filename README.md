# resumo-reunioes-teams — Configuração Thunders

Configuração customizada da skill [resumo-reunioes-teams](https://github.com/sidneydiaraujo/resumo-reunioes-teams) para o contexto de um Scrum Master em uma empresa com múltiplos times de desenvolvimento.

## Contexto

O usuário participa de reuniões de vários times (B2B, Projetos, B2B2C, Evolução e Regulatório). Apenas reuniões organizadas por anfitriões específicos são resumidas — os demais organizadores geralmente conduzem cerimônias de rotina de times que têm seus próprios Scrum Masters.

## Filtros configurados

### Anfitriões autorizados

Somente reuniões criadas por um desses organizadores são processadas:

- **Sidney de Araujo Silva** — Scrum Master principal
- **Giovana Rodrigues**
- **Eduardo Sozim**

Qualquer reunião de outro anfitrião é ignorada automaticamente.

### Ignorar por título

Mesmo que criadas por um anfitrião autorizado, reuniões com os seguintes termos no título são sempre ignoradas:

| Termo | Motivo |
|---|---|
| `[Refinamento]` | Cerimônia recorrente de backlog, não gera resumo útil |
| `Diálogo de Inovação` | Série recorrente de inovação sem necessidade de acompanhamento |
| `Release` | Evento de entrega — acompanhado por outros meios |
| `Fim de garantia` | Evento pontual sem dinâmica de reunião relevante |

### Ignorar por time e tipo de reunião

Times com Scrum Masters próprios têm suas cerimônias de rotina ignoradas:

| Time | Tipos ignorados |
|---|---|
| B2B2C | Daily, Review, Refinamento, Alinhamento Técnico, Planning |
| Evolução e Regulatório | Daily, Review, Refinamento, Alinhamento Técnico, Planning |

### O que é processado

- Reuniões de qualquer tipo organizadas por Sidney, Giovana ou Eduardo
- Dailys e alinhamentos dos times B2B e Projetos
- Workshops, bate-papos de gestão, demos, alinhamentos pontuais

## Como usar

1. Clone a skill base:
   ```
   git clone https://github.com/sidneydiaraujo/resumo-reunioes-teams
   ```
2. Clone este repositório e copie o `skill_config.json` para a raiz da skill:
   ```
   git clone https://github.com/sidneydiaraujo/resumo-reunioes-teams-thunders
   copy resumo-reunioes-teams-thunders\skill_config.json resumo-reunioes-teams\
   ```
3. Preencha os campos `work_email`, `personal_draft_email`, `teams_team` e `teams_channel` no `skill_config.json` com seus dados
4. A skill já estará configurada com os filtros acima

## Ajustando para seu contexto

### Trocar ou adicionar anfitriões

Edite `allowed_organizers` em `skill_config.json`:

```json
"allowed_organizers": [
  "Seu Nome Completo",
  "Nome de Outro Colega"
]
```

A correspondência é parcial e sem distinção de maiúsculas — "Giovana Rodrigues" bate em "Giovana Rodrigues (Thunders)" automaticamente.

### Adicionar times com rotina própria

```json
"ignore_team_patterns": [
  {
    "team_keywords": ["Nome do Time"],
    "meeting_types": ["DAILY", "Review", "Planning"]
  }
]
```
