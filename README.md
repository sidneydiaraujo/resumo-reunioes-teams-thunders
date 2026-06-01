# resumo-reunioes-teams — Configuração Thunders

Configuração customizada da skill [resumo-reunioes-teams](https://github.com/sidneydiaraujo/resumo-reunioes-teams) para o contexto de um Scrum Master em uma empresa com múltiplos times de desenvolvimento.

## Contexto

O usuário participa de reuniões de vários times (B2B, Projetos, B2B2C, Evolução e Regulatório), mas só quer resumir as reuniões que ele mesmo organiza ou nas quais tem participação ativa e relevante. Times de rotina dos quais ele apenas participa (dailys, reviews, plannings) são ignorados.

## Filtros configurados

### Ignorar por título
- `[Refinamento]` — reuniões de refinamento de backlog (cerimônia recorrente, não gera resumo útil)
- `Diálogo de Inovação` — série de reuniões de inovação recorrentes sem necessidade de acompanhamento

### Ignorar recorrentes de outros organizadores
Reuniões recorrentes onde o usuário **não é o organizador** são ignoradas automaticamente. Isso cobre dailys, standups e outras cerimônias de times que ele acompanha mas não facilita.

### Ignorar por time e tipo de reunião
| Time | Tipos ignorados |
|---|---|
| B2B2C | Daily, Review, Refinamento, Alinhamento Técnico, Planning |
| Evolução e Regulatório | Daily, Review, Refinamento, Alinhamento Técnico, Planning |

Esses times têm Scrum Masters próprios. As reuniões de rotina deles não precisam de resumo separado.

### O que é processado
- Qualquer reunião organizada pelo usuário
- Reuniões não recorrentes com participação ativa (workshops, bate-papos de gestão, alinhamentos pontuais, demos)

## Como usar

1. Clone a skill base:
   ```
   git clone https://github.com/sidneydiaraujo/resumo-reunioes-teams
   ```
2. Copie o `skill_config.json` deste repositório para a raiz da skill
3. Preencha os campos `work_email`, `personal_draft_email`, `teams_team` e `teams_channel` com seus dados
4. A skill já estará configurada com os filtros acima

## Ajustando para seu contexto

Se você trabalha em uma estrutura similar mas com outros nomes de times, edite `skill_config.json`:

```json
"ignore_team_patterns": [
  {
    "team_keywords": ["Nome do Seu Time"],
    "meeting_types": ["DAILY", "Review", "Planning"]
  }
]
```

Adicione quantos padrões precisar.
