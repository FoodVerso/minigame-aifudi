# Mini Game do Aifudi — Site (Vercel)

## Deploy rápido
1. Crie um projeto no Vercel e **ative o KV** (Add → Storage → KV).
2. No projeto, adicione as variáveis de ambiente:
   - `KV_REST_API_URL` (automático ao conectar o KV)
   - `KV_REST_API_TOKEN` (automático ao conectar o KV)
   - `KV_REST_API_READ_ONLY_TOKEN` (opcional)
   - `LEADERBOARD_SECRET` (string que você inventa para assinar envios)

3. Faça deploy:
```bash
npm i
vercel deploy --prod
```

## Como o ranking global funciona
- O cliente envia `POST /api/score` com `{ ig, wa, score, ts, sig }`.
- O servidor valida a assinatura HMAC (`sig = HMAC_SHA256(LEADERBOARD_SECRET, ig:score:ts)`).
- A pontuação é gravada num **Sorted Set** (`aifudi:lb`) no Vercel KV.
- O endpoint `GET /api/leaderboard` retorna o **Top 50** com `{ ig, score }` (WhatsApp nunca é exposto).

> Dica: se você não quiser usar assinatura por enquanto, deixe `LEADERBOARD_SECRET` **vazio** durante os testes.

## Editar a logo
Substitua `public/assets/logo.webp` pela imagem que preferir.

