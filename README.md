# ORBIX · DTEL Telecom — Monitoramento Proativo

Painel de custos e eficiência do setor ORBIX. Publicado no GitHub Pages a partir da pasta `docs/`.

O conteúdo de `docs/index.html` é **criptografado** (AES-256-GCM, chave derivada do usuário e da senha com
PBKDF2-SHA256, 310 mil iterações). Sem as credenciais o arquivo não revela dados — nem no código-fonte.

## Publicar no GitHub Pages

1. Crie um repositório no GitHub e envie esta pasta (o `.gitignore` já deixa de fora planilhas, dados brutos e a senha):
   ```bash
   git init
   git add .
   git commit -m "Painel ORBIX"
   git branch -M main
   git remote add origin https://github.com/<seu-usuario>/<repositorio>.git
   git push -u origin main
   ```
2. No GitHub: **Settings → Pages → Build and deployment → Deploy from a branch → `main` / `/docs` → Save**.
3. Em 1–2 minutos o painel fica em `https://<seu-usuario>.github.io/<repositorio>/`.

## Atualizar os dados

```bash
python -X utf8 build/extrair_rfo.py build/atividades.json . build/dados.json
python -X utf8 build/gerar_dashboard.py
node build/publicar.js
git add docs && git commit -m "Atualiza dados" && git push
```

## Trocar usuário e senha

```bash
node build/publicar.js --usuario novo_usuario --senha "nova senha forte"
```
Depois faça commit/push de `docs/`. A senha antiga deixa de funcionar na hora.
