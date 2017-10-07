---
title: "dados de aaaImport na pesquisa do Azure no portal de saudação | Microsoft Docs"
description: "Use Olá Assistente de importação de dados do Azure pesquisa em hello Azure Portal toocrawl dados do Azure do banco de dados do SQL Azure Cosmos, armazenamento de Blob, o armazenamento de tabela, banco de dados SQL e SQL Server em VMs do Azure."
services: search
documentationcenter: 
author: HeidiSteen
manager: jhubbard
editor: 
tags: Azure Portal
ms.assetid: f40fe07a-0536-485d-8dfa-8226eb72e2cd
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: heidist
ms.openlocfilehash: 00b0e59594560c0cdaea748df196518e9fba3834
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="import-data-tooazure-search-using-hello-portal"></a>Importar dados tooAzure pesquisa usando o portal de saudação
Olá portal do Azure fornece um **importar dados** assistente no painel de pesquisa do Azure Olá para carregar dados em um índice. 

  ![Importar dados na barra de comandos Olá][1]

Internamente, o Assistente de saudação configura e invoca uma *indexador*, automatizando várias etapas do processo de indexação de saudação: 

* Conecte-se a fonte de dados externa tooan Olá mesma assinatura do Azure
* Gerar um esquema de índice pode ser modificado com base na estrutura de dados de origem de saudação
* Carregar documentos JSON em um índice usando um conjunto de linhas recuperado da fonte de dados de saudação

Você pode experimentar este fluxo de trabalho usando dados de exemplo no Azure Cosmos DB. Visite [Introdução à pesquisa do Azure no hello Azure Portal](search-get-started-portal.md) para obter instruções.

> [!NOTE]
> Você pode iniciar Olá **importar dados** Assistente do hello Azure Cosmos DB painel toosimplify indexação da fonte de dados. Esquerda de navegação, vá muito**coleções** > **Adicionar pesquisa do Azure** tooget iniciado.

## <a name="data-sources-supported-by-hello-import-data-wizard"></a>Fontes de dados suportadas pelo Olá Assistente de importação de dados
Assistente de importação de dados Olá dá suporte a saudação fontes de dados a seguir: 

* Banco de Dados SQL do Azure
* Dados relacionais do SQL Server em uma VM do Azure
* Azure Cosmos DB
* Armazenamento do Blob do Azure
* Armazenamento da tabela do Azure

Um conjunto de dados bidimensional é uma entrada exigida. Você só pode importar de uma única tabela, exibição do banco de dados ou estrutura de dados equivalente. Você deve criar essa estrutura de dados antes de executar o Assistente de saudação.

## <a name="connect-tooyour-data"></a>Conecte-se a dados tooyour
1. Entrar toohello [portal do Azure](https://portal.azure.com) e painel de serviço Olá aberto. Você pode clicar em **mais serviços** em Olá salto barra toosearch existente "serviços de pesquisa" na assinatura atual hello. 
2. Clique em **importar dados** na folha de dados de importação Olá abrir tooslide da barra de comandos de saudação.  
3. Clique em **conectar dados tooyour** toospecify uma definição de fonte de dados usada por um indexador. Para fontes de dados de assinatura de dentro do próprio assistente Olá geralmente pode detectar e ler as informações de conexão, minimizando os requisitos gerais de configuração.

|  |  |
| --- | --- |
| **Fonte de dados existente** |Se já houver indexadores definidos em seu serviço de pesquisa, selecione uma definição de fonte de dados existente para outra importação. |
| **Banco de Dados SQL do Azure** |Nome do serviço, as credenciais para um usuário de banco de dados com permissões de leitura e um nome de banco de dados podem ser especificado na página de saudação ou por meio de uma cadeia de caracteres de conexão ADO.NET. Escolha Olá tooview de opção de cadeia de caracteres de conexão ou personalizar as propriedades. <br/><br/>Olá tabela ou exibição fornece um conjunto de linhas de saudação deve ser especificada na página de saudação. Essa opção é exibida depois conexão Olá for bem-sucedida, fornecendo uma lista suspensa para que você possa fazer uma seleção. |
| **SQL Server em VM do Azure** |Especifique um nome de serviço totalmente qualificado, a ID e a senha de usuário e um banco de dados como uma cadeia de conexão. toouse esta fonte de dados, você deve ter instalado um certificado no repositório local de saudação que criptografa conexão hello. Para obter instruções, consulte [tooAzure de conexão SQL VM pesquisa](search-howto-connecting-azure-sql-iaas-to-azure-search-using-indexers.md). <br/><br/>Olá tabela ou exibição fornece um conjunto de linhas de saudação deve ser especificada na página de saudação. Essa opção é exibida depois conexão Olá for bem-sucedida, fornecendo uma lista suspensa para que você possa fazer uma seleção. |
| **Banco de dados do Azure Cosmos** |Requisitos incluem conta hello, banco de dados e coleção. Todos os documentos na coleção hello serão incluídos no índice de saudação. Você pode definir uma consulta tooflatten ou filtrar o conjunto de linhas de saudação ou toodetect alterado documentos para operações de atualização de dados subsequentes. |
| **Armazenamento de Blobs do Azure** |Requisitos incluem hello conta de armazenamento e um contêiner. Opcionalmente, se os nomes de blob seguem uma convenção de nomenclatura virtual para fins de agrupamento, você pode especificar parte do diretório virtual de saudação do nome de saudação como uma pasta no contêiner. Confira [Indexação do Armazenamento de Blobs](search-howto-indexing-azure-blob-storage.md) para saber mais. |
| **Armazenamento de Tabelas do Azure** |Os requisitos incluem conta de armazenamento hello e um nome de tabela. Opcionalmente, você pode especificar uma consulta tooretrieve um subconjunto das tabelas de saudação. Confira [Indexação do Armazenamento de Tabelas](search-howto-indexing-azure-tables.md) para saber mais. |

## <a name="customize-target-index"></a>Personalizar o índice de destino
Um índice preliminar normalmente é inferido do conjunto de dados de saudação. Adicionar, editar ou excluir campos toocomplete Olá esquema. Além disso, definir atributos em toodetermine de nível de campo Olá seus comportamentos de busca subsequentes.

1. Em **índice de destino de personalizar**, especifique o nome da saudação e um **chave** toouniquely usada identificar cada documento. Olá chave deve ser uma cadeia de caracteres. Se os valores de campo incluem espaços ou traços ser se tooset opções avançadas no **importar seus dados** toosuppress Olá verificação de validação para esses caracteres.
2. Analise e revise Olá restante. O nome e o tipo do campo geralmente são preenchidos para você. Você pode alterar o tipo de dados de saudação até Olá índice é criado. Alterá-la posteriormente exigirá uma recompilação.
3. Defina os atributos de índice de cada campo:
   
   * Recuperáveis retorna campo Olá nos resultados da pesquisa.
   * Podem ser filtrados permite Olá campo toobe referenciada em expressões de filtro.
   * Classificável permite Olá toobe de campo usada em uma classificação.
   * Facetable permite que o campo de saudação para navegação facetada.
   * Pesquisável habilita a pesquisa de texto completo.
4. Clique em Olá **analisador** guia se você quiser toospecify um analisador de idioma no nível de campo hello. Somente os analisadores de idioma podem ser especificados no momento. O uso de um analisador personalizado ou de um analisador que não é de linguagem, como o Keyword, o Pattern etc., exige código.
   
   * Clique em **pesquisável** toodesignate texto completo de pesquisa no campo hello e habilitar lista de saudação suspensa do analisador.
   * Escolha o analisador de saudação desejado. Confira [Criar um índice para documentos em vários idiomas](search-language-support.md) para obter detalhes.
5. Clique em Olá **sugestão** tooenable sugestões de preenchimento automático de consulta nos campos selecionados.

## <a name="import-your-data"></a>Importar seus dados
1. Em **importar seus dados**, forneça um nome para o indexador hello. Lembre-se de que o produto saudação do hello importar dados Assistente é um indexador. Posteriormente, se você quiser tooview ou editá-lo, você selecionará do portal de saudação em vez de executar novamente o Assistente de saudação. 
2. Especifique o agendamento de saudação, que se baseia em Olá fuso horário em que o serviço de saudação é provisionado.
3. Definir limites de toospecify de opções avançadas em se a indexação pode continuar se um documento é descartado. Além disso, você pode especificar se **chave** campos são permitidos espaços toocontain e barras.  
4. Clique em **Okey** toocreate Olá índice e importar dados de saudação.

Você pode monitorar a indexação no portal de saudação. Como documentos são carregados, contagem de documentos Olá aumentará para índice Olá que você definiu. Às vezes, leva alguns minutos para toopick de página do portal Olá as atualizações mais recentes de saudação.

índice de saudação é tooquery pronto assim que todos os documentos de saudação são carregados.

## <a name="query-an-index-using-search-explorer"></a>Consultar um índice usando o Search Explorer

Olá portal inclui **Search Explorer** para que você pode consultar um índice sem ter que toowrite qualquer código. Você pode usar o [Search Explorer](search-explorer.md) em qualquer índice.

Olá experiência de pesquisa é com base nas configurações padrão, como Olá [sintaxe simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) e padrão [parâmetro de consulta searchMode (https://docs.microsoft.com/rest/api/searchservice/search-documents). 

Resultados são retornados em JSON, em um formato detalhado, para que você pode inspecionar o documento inteiro hello.

## <a name="edit-an-existing-indexer"></a>Editar um indexador existente
Conforme observado, o Assistente de importação de dados de saudação cria um **indexador**, que você pode modificar como uma construção autônomo no portal de saudação.

No painel de serviço hello, clique duas vezes em Olá indexador bloco tooslide uma lista de todos os indexadores criado para sua assinatura. Clique duas vezes em uma saudação indexadores toorun, editar ou excluí-lo. Substituir o índice de saudação com outro existente, alterar a fonte de dados hello e definir opções para os limites de erro durante a indexação.

## <a name="edit-an-existing-index"></a>Editar um indexador existente
Assistente Olá também criado um **índice**. Na pesquisa do Azure, índice de tooan atualizações estrutural exigirá uma recriação de índice. Uma recompilação envolve Excluir índice hello, recriando o índice hello usando um esquema revisado que tem alterações de saudação desejado e recarregar os dados. As atualizações estruturais incluem alterar um tipo de dados e renomear ou excluir um campo.

As edições que não exigem a recriação incluem adicionar um novo campo, alterar os perfis de pontuação, mudar as sugestões ou alterar os analistas de linguagem. Consulte [Atualizar Índice](https://msdn.microsoft.com/library/azure/dn800964.aspx) para obter mais informações.


## <a name="next-steps"></a>Próximas etapas
Revise esses toolearn links mais sobre indexadores:

* [Indexação do Banco de Dados SQL](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md)
* [Indexação do Azure Cosmos DB](search-howto-index-documentdb.md)
* [Indexação do Armazenamento de Blobs](search-howto-indexing-azure-blob-storage.md)
* [Indexação do Armazenamento de Tabelas](search-howto-indexing-azure-tables.md)

<!--Image references-->
[1]: ./media/search-import-data-portal/search-import-data-command.png

