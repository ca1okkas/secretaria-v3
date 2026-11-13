# Secretária v3

Secretária virtual para atendimento via WhatsApp, construída com **n8n**. O agente atende pacientes, agenda e desmarca consultas no Google Calendar, gera cobranças, envia lembretes, faz follow-up de leads e também atende por telefone.

## O que tem aqui

```
WORKFLOWS/               Workflows do n8n (importar um a um)
Prompts/                 Prompts dos agentes (Secretária e Follow-up)
CONFIGURAÇÃO COOLIFY/    docker-compose do n8n e do Chatwoot + SQL do Postgres
```

### Workflows

| Nº | Workflow | Função |
|----|----------|--------|
| 00 | Configurações | Parâmetros gerais (Chatwoot, Postgres, Twilio, Z-API) |
| 01 | Secretária v3 | Agente principal de atendimento |
| 02 | Baixar e enviar arquivo do Google Drive | Envio de arquivos ao paciente |
| 03 | Buscar janelas disponíveis Google Calendar | Horários livres |
| 04 / 4.1 | Criar / Atualizar evento Google Calendar | Agendamento |
| 05 | Escalar humano | Transfere o atendimento para uma pessoa |
| 06 | Integração Asaas | Cobranças e confirmação de pagamento |
| 07 | Quebrar e enviar mensagens | Divide e envia respostas simulando digitação |
| 08 | Agente Assistente Interno | Assistente para a equipe |
| 09 | Desmarcar agendamento e enviar alerta | Cancelamentos |
| 10 | Buscar ou criar contato + conversa | Chatwoot |
| 11 | Agente de Lembretes de Agendamento | Lembretes de consulta |
| 12 | Gestão de ligações | Resumo de ligações (Retell) |
| 13 | Agente de Recuperação de Leads | Follow-up |
| — | Retell - Secretária v3 | Agente de voz |

## Requisitos

- n8n e Chatwoot (há `docker-compose` prontos para Coolify)
- PostgreSQL (script em `CONFIGURAÇÃO COOLIFY`)
- OpenAI, Google (Calendar e Drive), ElevenLabs, Asaas, Retell, Twilio e Z-API, conforme os módulos que você usar

## Como usar

1. Suba n8n, Chatwoot e Postgres com os arquivos de `CONFIGURAÇÃO COOLIFY` e rode o SQL.
2. No n8n, importe cada JSON de `WORKFLOWS` (menu **Import from file**), começando pelo `00`.
3. Abra os nodes e selecione/crie suas credenciais. Os JSON não trazem nenhuma.
4. Preencha os nodes **Info** de cada workflow e os subworkflows indicados nas notas.
5. Ajuste os prompts em `Prompts/` ao seu negócio. Nome da clínica, telefones e e-mails dos exemplos são fictícios.

> Nunca publique chaves de API, tokens ou credenciais. O `.gitignore` já ignora `.env` e arquivos de chave.
