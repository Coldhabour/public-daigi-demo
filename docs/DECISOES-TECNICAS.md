# Decisões técnicas

[Voltar à apresentação](../README.md)

## Um editor compartilhado entre empresas

**Necessidade:** atender empresas com identidade visual e modelos diferentes, mantendo uma base de aplicação comum.

**Solução:** separar os dados por empresa, associar usuários por vínculos e carregar a configuração correspondente sobre o mesmo editor. As políticas no banco fazem parte do controle de acesso.

**Limite atual:** algumas identidades e configurações documentais ainda dependem de registros mantidos no código. O provisionamento completo pelo painel permanece como evolução.

## Preços unitários em centavos

**Necessidade:** manter uma representação consistente dos valores monetários durante edição, salvamento e geração de documentos.

**Solução:** representar preços unitários em centavos e aplicar formatação monetária na apresentação. O subtotal é calculado a partir do preço e da quantidade.

**Ponto de atenção:** quantidades fracionárias exigem regras explícitas de arredondamento. A representação em centavos não substitui a validação dessas regras.

## Geração de Word baseada em modelos

**Necessidade:** aproveitar documentos com identidade visual e composição já definidas para cada empresa.

**Solução:** abrir o arquivo DOCX como um pacote, modificar seu conteúdo XML e preservar os demais recursos. A configuração da tabela permite diferenças de colunas entre empresas.

**Compromisso:** o gerador depende da estrutura dos modelos suportados. Alterações nesses modelos devem ser verificadas com documentos gerados e com a impressão.

## Confirmação financeira no backend

**Necessidade:** conceder acesso somente após a confirmação do pagamento, inclusive quando o provedor repete notificações.

**Solução:** validar a assinatura do webhook, consultar o pagamento na API do provedor, conferir seus dados e aplicar uma operação idempotente no banco.

**Compromisso:** a confirmação depende dos serviços externos. O estado pendente faz parte do fluxo, e a interface consulta a situação até que o acesso seja atualizado.

## Importação orientada a formatos conhecidos

**Necessidade:** reaproveitar os itens de documentos usados no fluxo de orçamento.

**Solução:** extrair e interpretar o texto de formatos PDF específicos, incluindo relatórios do Cronos e orçamentos da aplicação.

**Compromisso:** mudanças na estrutura desses documentos podem exigir ajustes nos interpretadores. PDFs digitalizados como imagem não devem ser tratados como equivalentes a PDFs com texto extraível.

## Verificações existentes

A base privada contém testes de geração e leitura de documentos, pesquisa no catálogo e resposta HTML da aplicação. Também inclui verificações de estrutura de código e estilos, além de testes SQL voltados às regras de acesso e ao isolamento entre empresas.

Essas verificações têm alcances diferentes: conferir a presença de uma regra no código não equivale a executar o fluxo completo no navegador ou contra os serviços de produção. Por isso, este portfólio não apresenta uma porcentagem de cobertura nem afirma que os testes foram executados durante sua preparação.

## Próximas evoluções

- Cadastro de empresas e gerenciamento de seus recursos pelo painel.
- Upload e versionamento de modelos e identidades visuais.
- Alertas de vencimento e acompanhamento de falhas de notificações de pagamento.
