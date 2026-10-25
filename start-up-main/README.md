# START_UP

Aplicação web para conectar founders, designers e desenvolvedores em um ambiente de descoberta e colaboração de startups.

## Como rodar

1. Instale as dependências:
   npm install
2. Inicie o projeto:
   npm run dev

## Autenticação

Por padrão, a aplicação entra em modo demo quando as variáveis de ambiente do Supabase não estão configuradas. Isso permite testar o fluxo de login e cadastro localmente sem uma conta real.

Credenciais de demonstração:
- E-mail: joao@startup.com
- Senha: 123456

## Variáveis de ambiente

Se quiser conectar com Supabase real, crie um arquivo .env e configure:

VITE_SUPABASE_URL=
VITE_SUPABASE_ANON_KEY=

Se as variáveis forem omitidas, o app continua funcionando em modo mock local.

### Publicar com Supabase no GitHub Pages

O build publicado precisa receber estas variáveis durante a execução do GitHub
Actions:

- `SUPABASE_URL`: Project URL em **Supabase > Project Settings > API**.
- `SUPABASE_ANON_KEY`: chave publicável (`anon`/`publishable`) do mesmo projeto.

No GitHub, abra **Settings > Secrets and variables > Actions > New repository
secret** e cadastre cada valor com o nome exato acima. Nunca use a chave
`service_role` no site: variáveis `VITE_*` são incluídas no JavaScript público.
As tabelas devem estar protegidas por Row Level Security.

Depois, em **Settings > Pages**, selecione **GitHub Actions** como fonte de
deploy. Faça um push para `main` ou `master` (ou execute manualmente
**Actions > Deploy to GitHub Pages > Run workflow**). O workflow valida os
secrets, faz lint, compila o site com as credenciais do Supabase e publica o
artefato. A configuração da URL base também é ajustada para o nome do
repositório.

## Conversas em tempo real

O chat em tempo real exige um projeto Supabase configurado. Aplique o arquivo
`supabase/migrations/20261023000000_realtime_direct_messages.sql` no SQL Editor
do projeto Supabase antes de usar a página de Mensagens. A migration cria os
perfis públicos básicos, conversas diretas e mensagens, configura políticas
de acesso por participante e habilita a publicação Realtime para mensagens.
Para aplicar, abra o painel do Supabase, selecione o projeto, entre em
**SQL Editor**, crie uma consulta, cole o conteúdo completo do arquivo e
execute. A migration pode ser executada novamente sem duplicar suas políticas.

## Scripts

- npm run dev
- npm run build
- npm run lint
