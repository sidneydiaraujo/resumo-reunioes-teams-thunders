# resumo-reunioes-teams — Configuração Thunders

Configuração customizada da skill [resumo-reunioes-teams](https://github.com/sidneydiaraujo/resumo-reunioes-teams) para o contexto de um Scrum Master em uma empresa com múltiplos times de desenvolvimento.

---

## Contexto

O usuário participa de reuniões de vários times (B2B, Projetos, B2B2C, Evolução e Regulatório). Apenas reuniões organizadas por anfitriões específicos são resumidas — os demais organizadores geralmente conduzem cerimônias de rotina de times que têm seus próprios Scrum Masters.

---

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

---

## Instalação

### 1. Pré-requisitos

- [Claude Code](https://claude.ai/code) instalado
- Python 3.8 ou superior
- Integração **Microsoft 365** habilitada no Claude Code

> As dependências Python são instaladas automaticamente na primeira execução.

### 2. Clone a skill base e este repositório

**Windows (PowerShell):**
```powershell
Set-Location "$env:USERPROFILE\.claude\skills"
git clone https://github.com/sidneydiaraujo/resumo-reunioes-teams
git clone https://github.com/sidneydiaraujo/resumo-reunioes-teams-thunders
```

**macOS / Linux:**
```bash
cd ~/.claude/skills
git clone https://github.com/sidneydiaraujo/resumo-reunioes-teams
git clone https://github.com/sidneydiaraujo/resumo-reunioes-teams-thunders
```

### 3. Copie o arquivo de configuração para a skill base

**Windows (PowerShell):**
```powershell
Copy-Item "resumo-reunioes-teams-thunders\skill_config.json" "resumo-reunioes-teams\"
```

**macOS / Linux:**
```bash
cp resumo-reunioes-teams-thunders/skill_config.json resumo-reunioes-teams/
```

### 4. Preencha seus dados no skill_config.json

Abra `resumo-reunioes-teams/skill_config.json` e substitua os campos com seus dados:

```json
{
  "work_email": "seu.email@empresa.com.br",
  "personal_draft_email": "seu.email.pessoal@gmail.com",
  "teams_team": "Nome do Time no Teams",
  "teams_channel": "Nome do Canal"
}
```

> Os filtros (`allowed_organizers`, `ignore_title_contains`, etc.) já estão configurados para o contexto Thunders — só os campos de email e Teams precisam ser preenchidos.

### 5. Habilite a integração Microsoft 365 no Claude Code

No Claude Code, acesse as configurações de integrações e habilite **Microsoft 365**. Na primeira vez, o Claude solicitará autenticação com sua conta corporativa.

### 6. Reinicie o Claude Code

Feche e reabra o Claude Code para carregar a skill.

---

## Como usar

```
"Resume as reuniões de hoje"
"Faz o resumo da reunião de B2B de ontem"
"Resume as reuniões desta semana"
```

---

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

---

## Integração com reunioes-consulta

Após salvar resumos, você pode consultar o conteúdo das reuniões em linguagem natural. Instale também a skill **[reunioes-consulta](https://github.com/sidneydiaraujo/reunioes-consulta)** para ter o fluxo completo.
