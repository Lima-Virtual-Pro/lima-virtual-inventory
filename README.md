# Inventário Digital — Lima Virtual

Aplicação web responsiva para inventariar softwares, aplicações, arquivos e versões. A interface usa o schema privado `inventory` e a Edge Function `inventory-api` já existentes no projeto Supabase Painel-Lima-Virtual.

## O que está incluído
- `index.html`: aplicação web pronta para hospedagem estática.
- `supabase/INTEGRACAO.md`: resumo da infraestrutura Supabase já existente e utilizada.
- `manifest.webmanifest`: metadados para instalação como PWA.
- `assets/`: pasta reservada para ícones adicionais.

## Projeto Supabase já indicado no modelo
A aplicação mantém a URL e a chave pública (publishable/anon) que já constavam no HTML fornecido:
- URL: `https://piagfpnjiwpngbikkkfp.supabase.co`
- Chave: publishable key, destinada ao cliente web. Nunca coloque `service_role` ou segredo administrativo no HTML.

## Configuração necessária no Supabase
1. Abra o projeto `piagfpnjiwpngbikkkfp`.
2. A aplicação usa a Edge Function `inventory-api`, atualizada para edição, versões, exclusão de arquivos e arquivamento.
3. Em **Authentication → Providers → Google**, habilite Google e informe Client ID e Client Secret obtidos no Google Cloud Console.
4. Em **Authentication → URL Configuration**, configure:
   - Site URL: URL final de publicação (por exemplo, o domínio GitHub Pages ou domínio próprio).
   - Redirect URLs: inclua a URL exata de publicação e a URL local usada nos testes.
5. No Google Cloud Console, configure o OAuth Client do tipo Web. Adicione como origem autorizada o domínio publicado e como URI de redirecionamento autorizado o callback do Supabase:
   `https://piagfpnjiwpngbikkkfp.supabase.co/auth/v1/callback`
6. Publique `index.html` e `manifest.webmanifest` juntos no mesmo diretório/branch do site.

## Teste local
Como o login OAuth e os módulos ES funcionam melhor em origem HTTP(S), use um servidor local, por exemplo:
`python -m http.server 8080`
Acesse `http://localhost:8080`. Inclua `http://localhost:8080` nas URLs de redirecionamento permitidas do Supabase.

## Segurança e limites
- A Edge Function valida o token do usuário e exige cadastro ativo em `inventory.members`; operações de escrita exigem perfil administrador.
- O bucket `software-inventory` é privado; downloads usam URL assinada com validade de 5 minutos.
- A chave publishable no front-end não é segredo. A proteção depende de RLS e das políticas do Storage.
- Não publique `service_role`, tokens privados ou segredos OAuth no repositório.
- Limite de upload configurado em 250 MB por arquivo.
- Para excluir um software, o sistema tenta remover seus arquivos do Storage antes de remover o registro. Se a exclusão do Storage falhar, a operação é interrompida para evitar deixar registros órfãos.

## Recursos implementados
Cadastro, edição, pesquisa, filtros, indicadores, upload de múltiplos arquivos, download privado, novas versões com notas, histórico de operações, exclusão de arquivos, arquivamento sem apagar registros e exportação CSV.
