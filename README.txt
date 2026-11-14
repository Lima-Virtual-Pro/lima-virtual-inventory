INVENTÁRIO DIGITAL LIMA VIRTUAL — V3.0 (PACOTE DE IMPLEMENTAÇÃO)

Conteúdo:
- index.html: interface web com identificação de licença, exclusão de software e área de Lixeira.
- manifest.webmanifest: metadados PWA.
- supabase/migrations/20261114_inventory_v3_trash.sql: migração aditiva de campos para retenção de 30 dias.

BACKEND
A Edge Function inventory-api foi publicada no projeto Supabase piagfpnjiwpngbikkkfp como versão 6 nesta sessão.
A função valida a licença individual por conta usando plv_get_app_access, mantém leitura/download após vencimento e exige licença ativa para cadastro, edição, novas versões e uploads. O inventário é compartilhado entre membros ativos do schema inventory.

IMPORTANTE — VALIDAÇÃO PENDENTE
Este pacote não deve ser tratado como release final de produção até concluir testes autenticados com as duas contas, testar upload/download real, restauração de software e arquivo, retenção de 30 dias e exclusão permanente. A interface ainda precisa ser publicada no GitHub Pages e integrada ao menu do Painel Lima Virtual.
Nenhum registro existente foi excluído ou transferido nesta implementação.
