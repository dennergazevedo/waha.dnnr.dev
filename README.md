# Agente de IA para WhatsApp — N8N + WAHA

Gerador visual de `docker-compose.yml` para subir o **WAHA** (WhatsApp HTTP API) integrado ao **n8n** em segundos, sem editar arquivos manualmente.

## 📺 Tutorial em vídeo

Aprenda a configurar e usar tudo do zero no canal:

**[@devdenegociosmg](https://www.youtube.com/@devdenegociosmg)**

---

## O que é isso?

Uma página HTML estática que gera um arquivo `docker-compose.yml` pronto para uso com:

- **WAHA** — gateway WhatsApp via HTTP (sem Selenium, sem navegador)
- **n8n** — plataforma de automação low-code / no-code

Basta preencher username e senha, escolher o sistema operacional do servidor e baixar o arquivo gerado.

---

## Funcionalidades

- API Key e Encryption Key geradas automaticamente no carregamento da página
- URL de webhook ajustada automaticamente conforme o SO (`host.docker.internal` vs `172.17.0.1`)
- Layout lado a lado no desktop — configuração à esquerda, YAML à direita
- Syntax highlight no YAML gerado
- Copiar para área de transferência ou baixar o `.yml` diretamente

---

## Como usar

### 1. Abrir a página

Abra o `index.html` diretamente no navegador ou sirva com qualquer servidor estático.

### 2. Configurar

| Campo | Descrição |
|---|---|
| **Username** | Usuário do Dashboard WAHA (padrão: `admin`) |
| **Password** | Senha de acesso ao Dashboard e Swagger |
| **API Key** | Gerada automaticamente — use nas credenciais do n8n |

### 3. Escolher o SO do servidor

| SO | Endereço usado |
|---|---|
| macOS / Windows | `host.docker.internal` |
| Linux | `172.17.0.1` |

### 4. Gerar e baixar

Clique em **Gerar docker-compose.yml** e depois em **Baixar .yml**.

### 5. Subir os containers

```bash
docker compose up -d
```

---

## Serviços gerados

| Serviço | Porta | URL |
|---|---|---|
| WAHA Dashboard | 3000 | http://localhost:3000/dashboard |
| WAHA Swagger | 3000 | http://localhost:3000/docs |
| n8n | 5678 | http://localhost:5678 |

---

## Volumes criados

```
./waha/sessions   # sessões WhatsApp (mantém login)
./waha/media      # mídias recebidas e enviadas
./n8n/data        # banco SQLite, credenciais e workflows
./n8n/files       # arquivos acessíveis dentro dos workflows
```

---

## Avisos importantes

- **Não altere a `N8N_ENCRYPTION_KEY`** após criar os workflows — você perderá acesso às credenciais salvas.
- Em produção, configure `WEBHOOK_URL` com seu domínio HTTPS.
- A `WAHA_API_KEY` gerada deve ser usada na configuração da credencial WAHA dentro do n8n.

---

## Stack

- HTML + CSS + JavaScript puro — zero dependências, zero build
- Tema dark com highlight amber
- Syntax highlight YAML manual via regex
