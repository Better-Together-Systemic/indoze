# INDOZE — Better Together Systemic
## Deploy na Vercel

### Estrutura
```
indoze-vercel/
├── index.html      ← aplicação completa
└── vercel.json     ← configuração da Vercel
```

---

### Passo 1 — Configurar a chave da Anthropic no Supabase

Antes de publicar, a chave da API da Anthropic precisa estar salva com segurança no Supabase:

1. Acesse [supabase.com](https://supabase.com) → seu projeto **indoze-better-together**
2. Vá em **Settings → Edge Functions → Secrets**
3. Clique em **Add new secret**
4. Nome: `ANTHROPIC_API_KEY`
5. Valor: sua chave `sk-ant-...`
6. Salve

A Edge Function `anthropic-proxy` já está publicada e pronta para usar esse secret.

---

### Passo 2 — Configurar URL no Supabase Auth

Para que o login funcione no domínio da Vercel:

1. No Supabase, vá em **Authentication → URL Configuration**
2. **Site URL**: coloque o domínio da Vercel (ex: `https://indoze.vercel.app`)
3. **Redirect URLs**: adicione o mesmo domínio + `/*`
4. Salve

---

### Passo 3 — Publicar na Vercel

#### Opção A — Via interface (mais simples)

1. Acesse [vercel.com](https://vercel.com) e faça login
2. Clique em **Add New → Project**
3. Escolha **Import Git Repository** — ou use **Deploy from template**
4. Se preferir sem Git: use o **Vercel CLI** (opção B abaixo)

#### Opção B — Via Vercel CLI (recomendado)

```bash
# Instalar o CLI (uma vez só)
npm install -g vercel

# Entrar na pasta do projeto
cd indoze-vercel

# Fazer o deploy
vercel

# Seguir as perguntas:
# - Set up and deploy? → Y
# - Which scope? → sua conta
# - Link to existing project? → N
# - Project name? → indoze-better-together
# - In which directory is your code? → ./
# - Override settings? → N

# Para produção (domínio fixo):
vercel --prod
```

#### Opção C — Arrastar e soltar

1. Acesse [vercel.com/new](https://vercel.com/new)
2. Role até o final da página
3. Arraste a pasta `indoze-vercel` inteira para a área indicada
4. Clique em **Deploy**

---

### Passo 4 — Domínio personalizado (opcional)

1. Na Vercel, vá em **Settings → Domains**
2. Adicione seu domínio (ex: `indoze.bettertogethersystemic.com.br`)
3. Atualize o DNS onde seu domínio está registrado com os valores que a Vercel indicar
4. Volte ao Supabase e adicione o novo domínio nas **Redirect URLs**

---

### Checklist final antes de ir ao ar

- [ ] Secret `ANTHROPIC_API_KEY` salvo no Supabase Edge Functions
- [ ] Site URL configurado no Supabase Auth
- [ ] Domínio da Vercel adicionado nas Redirect URLs do Supabase
- [ ] Testou cadastro de um usuário real
- [ ] Testou login e persistência (fechar e reabrir o browser)
- [ ] Testou o Escrivão (resposta da IA)
- [ ] Testou salvar reflexão em um dia

---

### Suporte técnico

**Projeto Supabase:** `indoze-better-together` (região São Paulo)  
**Edge Function:** `anthropic-proxy` (autenticada por JWT)  
**Banco:** PostgreSQL com RLS ativo em todas as tabelas
