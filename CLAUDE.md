# IAraFarma — Landing Page

Projeto de landing page para captação de leads da IAra Farma, ferramenta de inteligência comercial com IA para farmácias.

## Estrutura de Arquivos

```
LP-IAraFarma/
├── index.html       # Landing page principal (HTML/CSS/JS inline, ~2344 linhas)
├── obrigado.html    # Página de confirmação após envio do formulário
└── CLAUDE.md        # Este arquivo
```

## Fluxo do Formulário

1. Usuário preenche 3 campos na seção `#cta` do `index.html`:
   - `#campo-farmacia` — Nome da farmácia (text)
   - `#campo-whatsapp` — WhatsApp (tel)
   - `#campo-entregas` — Volume de entregas/dia (select: "30-50" | "50+")
2. Clique no `#btn-submit` dispara handler JS (ao final do `<script>` inline)
3. Handler valida campos → faz `fetch` POST para o webhook do n8n
4. Independente da resposta do webhook → redireciona para `obrigado.html`

## Integrações

### n8n
- **Instância:** https://automacaobluelinedigital-n8n.cloudfy.live
- **Workflow:** "IAraFarma - Leads do Site" (ID: `80YqDTAvcSyF9omU`)
- **Webhook URL:** `https://automacaobluelinedigital-n8n.cloudfy.live/webhook/iara-farma-leads`
- **Método:** POST — recebe JSON `{ farmacia, whatsapp, entregas }`
- **Ação:** Envia os dados para o WeSales CRM via HTTP Request

### WeSales CRM
- **App:** https://app.wesalescrm.com
- **Endpoint usado no n8n:** `POST https://app.wesalescrm.com/api/v1/contacts`
- **Autenticação:** Bearer Token (PIT — Personal Integration Token)
- **Campos enviados:** `name`, `phone`, `source` ("Landing Page"), `notes` (entregas/dia)

## Histórico de Alterações

### 2026-04-22
- Adicionados `id` nos campos do formulário (`campo-farmacia`, `campo-whatsapp`, `campo-entregas`, `btn-submit`)
- Adicionado handler JavaScript de submissão no `<script>` inline do `index.html`
- Criada página `obrigado.html` com identidade visual consistente
- Criado workflow n8n "IAraFarma - Leads do Site" via API e ativado
- Workflow integra webhook → WeSales CRM automaticamente
