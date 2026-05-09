# BI Fogaça — Antônio Fogaça

Dashboard de acompanhamento de campanhas Meta Ads do cliente Antônio Fogaça.

## Estrutura

- `index.html` — dashboard (servido pela Cloudflare Pages)
- `atualizar_bi.py` — script que busca dados da Meta API e injeta no HTML
- `.github/workflows/update-bi.yml` — Action que roda a cada 2h (horário comercial Brasília)
- `.env.example` — template de variáveis (copie para `.env` localmente)

## Acesso do cliente

URL: https://bi-fogaca.pages.dev (ajustar após deploy)

---

## Setup local

```bash
cp .env.example .env
# edite .env e cole seu META_ACCESS_TOKEN
pip install -r requirements.txt
python atualizar_bi.py
```

Abra o `index.html` no navegador.

## Deploy (uma vez)

### 1. Criar repo privado no GitHub
1. github.com/new → nome `bi-fogaca` → **Private**
2. Inicializar e dar push:
   ```bash
   git init
   git add .
   git commit -m "BI Fogaca inicial"
   git branch -M main
   git remote add origin https://github.com/<seu-usuario>/bi-fogaca.git
   git push -u origin main
   ```

### 2. Configurar secrets no GitHub
Repo → Settings → Secrets and variables → Actions → **New repository secret**
- `META_ACCESS_TOKEN` = token de longa duração
- `META_AD_ACCOUNT_ID` = `act_950037393138268`

### 3. Conectar ao Cloudflare Pages
1. dash.cloudflare.com → **Workers & Pages** → **Create** → **Pages** → **Connect to Git**
2. Selecionar repo `bi-fogaca` → branch `main`
3. Build command: (vazio) · Output directory: `/`
4. Save and Deploy → URL `https://bi-fogaca.pages.dev`

### 4. (Opcional) Cloudflare Access para login
Pages → Custom Domain → Access Policy → Email OTP
