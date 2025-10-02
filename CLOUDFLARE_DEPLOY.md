# Deploy no Cloudflare Pages

Este projeto está configurado para deploy no Cloudflare Pages.

## Configurações de Build no Painel do Cloudflare

### Framework preset
Selecione: **Nenhum** (None)

### Build command
```
npm ci && npm run build
```

### Build output directory
```
dist
```

### Root directory
```
/
```

### Environment Variables
Configure as seguintes variáveis de ambiente no painel do Cloudflare Pages:

**IMPORTANTE:** Vá em Settings > Environment Variables e adicione:

- `NODE_VERSION`: `20.18.0`
- `VITE_SUPABASE_URL`: [sua URL do Supabase]
- `VITE_SUPABASE_ANON_KEY`: [sua chave anônima do Supabase]
- `VITE_CLOUDINARY_CLOUD_NAME`: [seu cloud name do Cloudinary]
- `VITE_CLOUDINARY_UPLOAD_PRESET`: [seu upload preset do Cloudinary]
- `VITE_STRIPE_PUBLISHABLE_KEY`: [sua chave pública do Stripe]

## Arquivos Importantes

- `.nvmrc` e `.node-version`: Força o uso do Node.js 20.18.0
- `.npmrc`: Configurações do npm
- `package-lock.json`: Lock file do npm (NUNCA remova este arquivo)
- `wrangler.toml`: Configuração do Cloudflare Pages

## Importante

- O projeto usa **npm** como gerenciador de pacotes
- **NÃO use bun** - o Cloudflare pode tentar detectá-lo automaticamente
- Se houver qualquer arquivo `bun.lockb` no repositório, remova-o
- Use apenas `package-lock.json` para gerenciar dependências
- As rotas SPA estão configuradas via `public/_redirects`

## Troubleshooting

### Erro: "lockfile had changes, but lockfile is frozen"

Este erro aparece quando o Cloudflare tenta usar `bun` em vez de `npm`. Solução:

1. Certifique-se de que NÃO existe arquivo `bun.lockb` no repositório
2. Verifique se existe o arquivo `.nvmrc` com o conteúdo `20.18.0`
3. No painel do Cloudflare, vá em Settings > Builds & deployments
4. Limpe o cache de build (Clear build cache)
5. Force um novo deploy

### Forçar o uso do npm

Se o Cloudflare continuar usando bun:

1. Vá em Settings > Environment Variables
2. Adicione: `SKIP_DEPENDENCY_INSTALL` = `true`
3. Modifique o Build command para:
```
npm ci && npm run build
```

## Redeploy

Se o deploy falhar:

1. Limpe o cache de build no painel do Cloudflare
2. Certifique-se de que todas as variáveis de ambiente estão configuradas
3. Verifique se não existe `bun.lockb` no repositório
4. Tente novamente o deploy
