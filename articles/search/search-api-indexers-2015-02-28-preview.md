---
title: "Operações de indexador (API REST do Serviço da Pesquisa do Azure: 2015-02-28-Preview) | Microsoft Docs"
description: "Operações de indexador (API REST do serviço Azure Search: 2015-02-28-Preview)"
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 42b5f85c-8304-4bc7-8e1e-a9c76b8ca25a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: eugenesh
ms.openlocfilehash: 4dd9591072b44eeabae6eac1182b4eea10fd4a22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="indexer-operations-azure-search-service-rest-api-2015-02-28-preview"></a>Operações de indexador (API REST do serviço Azure Search: 2015-02-28-Preview)
> [!NOTE]
> Este artigo descreve indexadores em Olá [2015-02-28-visualização REST API](search-api-2015-02-28-preview.md). Esta versão de API adiciona versões de visualização do indexador do Armazenamento de Blobs do Azure com a extração de documentos, o indexador do Armazenamento de Tabelas do Azure e outros aprimoramentos. Olá API também suporta disponíveis indexadores (GA), incluindo indexadores para o banco de dados do SQL Azure, SQL Server em máquinas virtuais do Azure e o banco de dados do Azure Cosmos.
> 
> 

## <a name="overview"></a>Visão geral
A pesquisa do Azure pode integrar diretamente com algumas fontes de dados comuns, removendo Olá necessidade toowrite código tooindex seus dados. tooset backup esse backup, você pode chamar hello toocreate de API de pesquisa do Azure e gerenciar **indexadores** e **fontes de dados**. 

Um **indexador** é um recurso que conecta fontes de dados a índices de pesquisa de destino. Um indexador é usado em Olá maneiras a seguir: 

* Execute uma cópia única de dados de saudação toopopulate um índice.
* Um índice com as alterações na fonte de dados de saudação em uma agenda de sincronização. agendamento de saudação faz parte da definição do indexador hello.
* Invocar sob demanda tooupdate um índice, conforme necessário. 

Um **indexador** é útil quando você deseja que o índice de tooan atualizações regulares. Você pode configurar uma agenda interna como parte de uma definição de indexador ou executá-lo em demanda usando [Executar indexador](#RunIndexer). 

Um **fonte de dados** Especifica quais dados precisam toobe indexado, credenciais tooaccess Olá dados e políticas tooenable pesquisa do Azure tooefficiently identificar alterações nos dados de saudação (como modificadas ou excluídas linhas em uma tabela de banco de dados). Ela é definida como um recurso independente para que possa ser usada por vários indexadores.

Olá, fontes de dados a seguir é atualmente suportado:

* **Banco de Dados SQL do Azure** e **SQL Server em VMs do Azure**. Para obter um passo a passo direcionado, confira [este artigo](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 
* **Azure Cosmos DB**. Para obter um passo a passo direcionado, confira [este artigo](search-howto-index-documentdb.md). 
* **Armazenamento de BLOBs do Azure**, incluindo a seguir Olá formatos de documentos: PDF, Microsoft Office (DOCX/documentos, XLS/XSLX, PPTX/PPT, MSG), HTML, XML, ZIP e texto sem formatação arquivos (inclusive JSON). Para obter um passo a passo direcionado, confira [este artigo](search-howto-indexing-azure-blob-storage.md).
* **Armazenamento de Tabelas do Azure**. Para obter um passo a passo direcionado, confira [este artigo](search-howto-indexing-azure-tables.md).

Estamos considerando adicionando suporte para fontes de dados adicionais no hello futuras. toohelp nos priorizar essas decisões, forneça seus comentários sobre Olá [Fórum de comentários da pesquisa do Azure](http://feedback.azure.com/forums/263029-azure-search).

Consulte [limites de serviço](search-limits-quotas-capacity.md) para máximo limita os recursos relacionados tooindexer e dados de origem.

## <a name="typical-usage-flow"></a>Fluxo de uso típico
Você pode criar e gerenciar índices e fontes de dados por meio de solicitações HTTP simples (POST, GET, PUT, DELETE) em relação a um recurso `data source` ou `indexer` específico.

A configuração indexação automática normalmente é um processo em quatro etapas:

1. Identifique a fonte de dados de saudação que contém dados Olá precisa toobe indexado. Tenha em mente que a pesquisa do Azure podem não suportar todos os tipos de dados de saudação presentes na fonte de dados. Consulte [suporte para tipos de dados](https://msdn.microsoft.com/library/azure/dn798938.aspx) para lista de saudação.
2. Crie um índice do Azure Search cujo esquema seja compatível com a fonte de dados
3. Crie uma fonte de dados do Azure Search conforme descrito na seção [Criar fonte de dados](#CreateDataSource).
4. Crie um indexador de pesquisa do Azure conforme descrito em [Criar indexador](#CreateIndexer).

Você deve planejar a criação de um indexador para cada combinação de índice de destino e fonte de dados. Você pode ter vários indexadores gravando no hello mesmo índice e você pode reutilizar Olá mesma fonte de dados para vários indexadores. No entanto, um indexador só pode consumir uma fonte de dados por vez e pode gravar apenas tooa único índice. 

Depois de criar um indexador, você pode recuperar seu status de execução usando Olá [obter Status do indexador](#GetIndexerStatus) operação. Você também pode executar um indexador a qualquer momento (em vez de ou em adição toorunning-lo periodicamente em um agendamento) usando Olá [executar indexador](#RunIndexer) operação.

<!-- MSDN has 2 art files plus a API topic link list -->


## <a name="create-data-source"></a>Criar fonte de dados
Na pesquisa do Azure, uma fonte de dados é usada com indexadores, fornecendo informações de conexão Olá para atualização de dados agendado ou ad hoc de um índice de destino. Você pode criar uma nova fonte de dados  em um serviço Azure Search usando uma solicitação HTTP POST.

    POST https://[service name].search.windows.net/datasources?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Como alternativa, você pode usar PUT e especificar o nome de fonte de dados de saudação em Olá URI. Se a fonte de dados de saudação não existir, ele será criado.

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]

> [!NOTE]
> número máximo de saudação de fontes de dados permitido varia de acordo com o tipo de preço. serviço gratuito Olá permite too3 fontes de dados. O serviço padrão permite 50 fontes de dados. Veja [Limites de Serviço](search-limits-quotas-capacity.md) para obter detalhes.
> 
> 

**Solicitação**

HTTPS é necessário para todas as solicitações de serviço. Olá **criar fonte de dados** solicitação pode ser criada usando um método POST ou PUT. Ao usar POST, você deve fornecer um nome de fonte de dados no corpo da solicitação de saudação junto com a definição de fonte de dados de saudação. Com PUT, o nome de saudação faz parte da URL de saudação. Se a fonte de dados de saudação não existir, ele será criado. Se já existir, é atualizado toohello nova definição. 

nome de fonte de dados Olá deve estar em letras minúsculas, começar com uma letra ou número, não ter barras ou pontos e ter menos de 128 caracteres. Depois de iniciar o nome de fonte de dados de saudação com uma letra ou número, restante de saudação do nome hello pode incluir qualquer letra, número e traços, como Olá traços não sejam consecutivos. Consulte [Regras de nomenclatura](https://msdn.microsoft.com/library/azure/dn857353.aspx) para obter detalhes.

Olá `api-version` é necessária. versão atual do Hello é `2015-02-28`.

**Cabeçalhos da solicitação**

Olá lista a seguir descreve hello necessárias e cabeçalhos opcionais da solicitação. 

* `Content-Type`: obrigatório. Defina esta opção muito`application/json`
* `api-key`: obrigatório. Olá `api-key` é usado tooauthenticate Olá solicitação tooyour serviço de pesquisa. É um valor de cadeia de caracteres, o serviço de tooyour exclusivo. Olá **criar fonte de dados** solicitação deve incluir um `api-key` cabeçalho definido tooyour a chave de administração (como a chave de consulta tooa contrário). 

Você também precisará Olá serviço nome tooconstruct Olá solicitação URL. Você pode obter o nome do serviço hello e `api-key` do seu painel de serviço no hello [Portal do Azure](https://portal.azure.com/). Consulte [criar um serviço de pesquisa no portal de saudação](search-create-service-portal.md) para obter ajuda de navegação de página.

<a name="CreateDataSourceRequestSyntax"></a>
**Sintaxe do Corpo da Solicitação**

corpo de saudação da solicitação Olá contém uma definição de fonte de dados, que inclui o tipo de fonte de dados hello, dados de saudação tooread credenciais, bem como uma detecção de alteração de dados opcionais e identificam as políticas que são usada tooefficiently de detecção de exclusão de dados alterado ou os dados excluídos na fonte de dados hello quando usado com um indexador periodicamente agendado. 

sintaxe de saudação para estruturar a carga de solicitação de saudação é da seguinte maneira. Uma solicitação de exemplo é fornecida mais adiante neste tópico.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello data source",
        "description" : "Optional. Anything you want, or nothing at all",
        "type" : "Required. Must be one of 'azuresql', 'documentdb', 'azureblob', or 'azuretable'",
        "credentials" : { "connectionString" : "Required. Connection string for your data source" },
        "container" : { "name" : "Required. hello name of hello table, collection, or blob container you wish tooindex" },
        "dataChangeDetectionPolicy" : { Optional. See below for details }, 
        "dataDeletionDetectionPolicy" : { Optional. See below for details }
    }

A solicitação contém Olá propriedades a seguir: 

* `name`: obrigatório. nome de Olá Olá da fonte de dados. Um nome de fonte de dados deve apenas conter letras minúsculas, dígitos ou traços, não podem começar ou terminar com traços e está limitado too128 caracteres.
* `description`: uma descrição opcional. 
* `type`: obrigatório. Deve ser um dos tipos de fonte de dados Olá com suporte:
  * `azuresql` ‒ banco de dados do Azure SQL ou SQL Server em máquinas virtuais do Azure
  * `documentdb` – Azure Cosmos DB
  * `azureblob` – Armazenamento de Blobs do Azure
  * `azuretable` - Armazenamento de Tabelas do Azure
* `credentials`:
  * Olá necessário `connectionString` propriedade especifica a cadeia de caracteres de conexão de Olá Olá fonte de dados. formato de saudação de cadeia de caracteres de conexão Olá depende Olá tipo de fonte de dados: 
    * Para o SQL Azure, isso é normal cadeia de conexão do SQL Server hello. Se você estiver usando a cadeia de caracteres da conexão Olá Olá tooretrieve portal do Azure, use Olá `ADO.NET connection string` opção.
    * Para o banco de dados do Azure Cosmos, cadeia de caracteres de conexão Olá deve estar no hello formato a seguir: `"AccountEndpoint=https://[your account name].documents.azure.com;AccountKey=[your account key];Database=[your database id]"`. Todos os valores hello são necessários. Você pode encontrá-los no hello [portal do Azure](https://portal.azure.com/).  
    * Para o armazenamento de tabela e de BLOBs do Azure, isso é cadeia de conexão da conta de armazenamento hello. o formato de saudação é descrito [aqui](https://azure.microsoft.com/documentation/articles/storage-configure-connection-string/). É necessário ter um protocolo de ponto de extremidade HTTPS.  
* `container`, necessária: especifica Olá dados tooindex usando Olá `name` e `query` propriedades: 
  * `name`, obrigatório:
    * SQL Azure: especifica Olá tabela ou exibição. Você pode usar nomes qualificados pelo esquema, como `[dbo].[mytable]`.
    * Documentos: Especifica a coleção de saudação. 
    * Armazenamento de BLOBs do Azure: Especifica o contêiner de armazenamento de saudação.
    * Armazenamento de tabela do Azure: Especifica o nome de saudação da tabela de saudação. 
  * `query`, opcional:
    * Documentos: permite que você toospecify uma consulta que nivele um layout de documento JSON arbitrário em um esquema simples que pesquisa do Azure pode indexar.  
    * Armazenamento de BLOBs do Azure: permite que você toospecify uma pasta virtual dentro do contêiner de blob hello. Por exemplo, para o caminho de blob `mycontainer/documents/blob.pdf`, `documents` pode ser usado como pasta virtual hello.
    * Armazenamento de tabela do Azure: permite que você toospecify uma consulta de filtros Olá conjunto de linhas toobe importado.
    * SQL Azure: não há suporte para consulta. Se você precisar dessa funcionalidade, vote [nesta sugestão](https://feedback.azure.com/forums/263029-azure-search/suggestions/9893490-support-user-provided-query-in-sql-indexer)
* Olá opcional `dataChangeDetectionPolicy` e `dataDeletionDetectionPolicy` propriedades são descritas abaixo.

<a name="DataChangeDetectionPolicies"></a>
**Políticas de Detecção de Alteração de Dados**

finalidade de saudação de dados de alterar a política de detecção é tooefficiently identificar itens de dados alterados. As políticas com suporte variam com base no tipo de fonte de dados de saudação. As seções a seguir descrevem cada política. 

***Política de Detecção de Alteração de Marca d’água Alta*** 

Use essa política quando sua fonte de dados contiver uma coluna ou propriedade que atenda Olá critérios a seguir:

* Todas as inserções especificam um valor para a coluna de saudação. 
* Item de tooan todas as atualizações também alterar o valor de saudação da coluna hello. 
* valor de saudação dessa coluna aumenta com cada alteração.
* Consultas que usam uma filtro cláusula semelhante toohello a seguir `WHERE [High Water Mark Column] > [Current High Water Mark Value]` podem ser executadas com eficiência.

Por exemplo, ao usar fontes de dados SQL do Azure, um repositório `rowversion` coluna será Olá o candidato ideal para uso com política de marca d'água alta de saudação. 

Essa política pode ser especificada da seguinte maneira:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "[a row version or last_updated column name]" 
    } 

Ao usar fontes de dados do banco de dados do Azure Cosmos, você deve usar o hello `_ts` propriedade fornecida pelo Azure Cosmos DB. 

Ao usar fontes de dados de Blob do Azure, pesquisa do Azure automaticamente usa uma marca d'água alta alterar política de detecção com base no carimbo da última modificação do blob; Você não precisa toospecify essa política.   

***Política de Detecção de Alteração de Dados Integrada do SQL***

Se o banco de dados SQL oferece suporte ao [controle de alterações](https://msdn.microsoft.com/library/bb933875.aspx), recomendamos o uso da Política de controle integrado de alterações do SQL. Essa política permite que o controle de alterações mais eficiente hello e permite que linhas de tooidentify excluído da pesquisa do Azure sem a necessidade de toohave uma coluna explícita "exclusão reversível" em seu esquema.

Controle de alterações integrado é suportada começando com hello versões de banco de dados do SQL Server a seguir: 

* SQL Server 2008 R2, se você estiver usando o SQL Server em VMs do Azure.
* Banco de Dados SQL do Azure V12, se você estiver usando o Banco de Dados SQL do Azure.  

Ao usar a política de Controle Integrado de Alterações do SQL, não especifique uma política separada de detecção de exclusão de dados, pois essa política tem suporte interno para identificação de linhas excluídas. 

Essa política só pode ser usada com tabelas; ela não pode ser usada com exibições. É necessário tooenable controle de alterações para tabela Olá que você está usando para poder usar esta diretiva. Confira [Habilitar e desabilitar o controle de alterações](https://msdn.microsoft.com/library/bb964713.aspx) para obter instruções.    

Ao estruturar Olá **criar fonte de dados** solicitação SQL política de controle de alterações integrado podem ser especificada da seguinte maneira:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy" 
    }

<a name="DataDeletionDetectionPolicies"></a>
**Políticas de Detecção de Exclusão de Dados**

finalidade de saudação de uma política de detecção de exclusão de dados é tooefficiently identificar itens de dados excluídos. Atualmente, a política Olá só tem suportada é Olá `Soft Delete` diretiva, que permite identificar excluiu os itens com base no valor de saudação de um `soft delete` coluna ou propriedade na fonte de dados de saudação. Essa política pode ser especificada da seguinte maneira:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello column that specifies whether a row was deleted", 
        "softDeleteMarkerValue" : "hello value that identifies a row as deleted" 
    }

> [!NOTE]
> Somente colunas com valores de cadeia de caracteres, inteiros ou Boolianos têm suporte. Olá valor usado como `softDeleteMarkerValue` deve ser uma cadeia de caracteres, mesmo que a coluna correspondente da saudação contém números inteiros ou boolianos. Por exemplo, se o valor de saudação que aparece em sua fonte de dados é 1, use `"1"` como Olá `softDeleteMarkerValue`.    
> 
> 

<a name="CreateDataSourceRequestExamples"></a>
**Exemplos de corpo da solicitação**

Se você pretende fonte de dados de saudação toouse com um indexador que é executado em um agendamento, este exemplo mostra como alterar toospecify e exclusão de políticas de detecção de: 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy", "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }

Se você pretende somente fonte de dados toouse Olá para uma cópia única de dados hello, políticas de saudação podem ser omitidas:

    { 
        "name" : "asqldatasource",
        "description" : "anything you want, or nothing at all",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" }
    } 

**Resposta**

Para uma solicitação bem-sucedida: "201 Criado". 

<a name="UpdateDataSource"></a>

## <a name="update-data-source"></a>Atualizar Fonte de Dados
Você pode atualizar uma fonte de dados usando uma solicitação HTTP PUT. Especifique o nome de saudação de saudação tooupdate de fonte de dados no URI de solicitação de saudação:

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Olá `api-version` é necessária. versão atual do Hello é `2015-02-28`. [Versões da API do Azure Search](https://msdn.microsoft.com/library/azure/dn864560.aspx) tem detalhes e mais informações sobre versões alternativas.

Olá `api-key` deve ser uma chave de administração (como a chave de consulta tooa contrário). Consulte a seção autenticação toohello [API REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais sobre as chaves. [Criar um serviço de pesquisa no portal de saudação](search-create-service-portal.md) explica como a URL do serviço tooget hello e propriedades de chave usado na solicitação de saudação.

**Solicitação**

Olá sintaxe do corpo de solicitação é Olá mesmos para [criar fonte de dados solicita](#CreateDataSourceRequestSyntax).

Algumas propriedades não podem ser atualizadas em uma fonte de dados existente. Por exemplo, você não pode alterar o tipo de saudação de uma fonte de dados existente.  

Se você não quiser cadeia de caracteres de conexão de saudação toochange para uma fonte de dados, você pode especificar Olá literal `<unchanged>` para cadeia de caracteres de conexão de saudação. Isso é útil em situações em que você precisa de uma fonte de dados de tooupdate, mas não tem a cadeia de caracteres de conexão do acesso conveniente toohello pois ela é sensível à segurança de dados.

**Resposta**

Para uma solicitação bem-sucedida: 201 Criado se uma nova fonte de dados for criada e 204 Sem Conteúdo se uma fonte de dados for atualizada.

<a name="ListDataSource"></a>

## <a name="list-data-sources"></a>Listar Fontes de Dados
Olá **fontes de dados de lista** operação retorna uma lista de fontes de dados de saudação em seu serviço de pesquisa do Azure. 

    GET https://[service name].search.windows.net/datasources?api-version=[api-version]
    api-key: [admin key]

Olá `api-version` é necessária. versão atual do Hello é `2015-02-28`. 

Olá `api-key` deve ser uma chave de administração (como a chave de consulta tooa contrário). Consulte a seção autenticação toohello [API REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais sobre as chaves. [Criar um serviço de pesquisa no portal de saudação](search-create-service-portal.md) explica como a URL do serviço tooget hello e propriedades de chave usado na solicitação de saudação.

**Resposta**

Para uma solicitação bem-sucedida: 200 OK.

Aqui está um exemplo de corpo de resposta:

    {
      "value" : [
        {
          "name": "datasource1",
          "type": "azuresql",
          ... other data source properties
        }]
    }

Observe que você pode filtrar a resposta Olá para propriedades de saudação toojust em que você estiver interessado. Por exemplo, se você quiser apenas uma lista de nomes de fonte de dados, use Olá OData `$select` opção de consulta:

    GET /datasources?api-version=205-02-28&$select=name

Nesse caso, resposta Olá Olá acima exemplo seria exibida da seguinte maneira: 

    {
      "value" : [ { "name": "datasource1" }, ... ]
    }

Isso é uma largura de banda de toosave técnica útil se você tiver muitas fontes de dados em seu serviço de pesquisa.

<a name="GetDataSource"></a>

## <a name="get-data-source"></a>Obter Fonte de Dados
Olá **obter fonte de dados** operação obtém a definição de fonte de dados de saudação da pesquisa do Azure.

    GET https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

Olá `api-version` é necessária. versão atual do Hello é `2015-02-28`. 

Olá `api-key` deve ser uma chave de administração (como a chave de consulta tooa contrário). Consulte a seção autenticação toohello [API REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais sobre as chaves. [Criar um serviço de pesquisa no portal de saudação](search-create-service-portal.md) explica como a URL do serviço tooget hello e propriedades de chave usado na solicitação de saudação.

**Resposta**

Código de status: 200 OK é retornado para uma resposta bem-sucedida.

resposta de saudação é semelhante tooexamples no [criar fonte de dados exemplo solicitações](#CreateDataSourceRequestExamples): 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName" : "IsDeleted", 
            "softDeleteMarkerValue" : "true" }
    }

> [!NOTE]
> Não defina Olá `Accept` cabeçalho de solicitação muito`application/json;odata.metadata=none` quando chamar esta API porque isso fará com que `@odata.type` toobe atributo omitida da resposta hello e você não será capaz de toodifferentiate entre a alteração de dados e detecção de exclusão de dados políticas de tipos diferentes. 
> 
> 

<a name="DeleteDataSource"></a>

## <a name="delete-data-source"></a>Excluir Fonte de Dados
Olá **excluir a fonte de dados** operação remove uma fonte de dados do seu serviço de pesquisa do Azure.

    DELETE https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Se qualquer indexador fizer referência a fonte de dados de saudação que você está excluindo, a operação de exclusão de saudação ainda continuará. No entanto, esses indexadores farão a transição para um estado de erro em sua próxima execução.  
> 
> 

Olá `api-version` é necessária. versão atual do Hello é `2015-02-28`. 

Olá `api-key` deve ser uma chave de administração (como a chave de consulta tooa contrário). Consulte a seção autenticação toohello [API REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais sobre as chaves. [Criar um serviço de pesquisa no portal de saudação](search-create-service-portal.md) explica como a URL do serviço tooget hello e propriedades de chave usado na solicitação de saudação.

**Resposta**

Código de status: 204 Sem Conteúdo é retornado para uma resposta bem-sucedida.

<a name="CreateIndexer"></a>

## <a name="create-indexer"></a>Criar indexador
Você pode criar um novo indexador em um serviço Azure Search usando uma solicitação HTTP POST.

    POST https://[service name].search.windows.net/indexers?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Como alternativa, você pode usar PUT e especificar o nome de fonte de dados de saudação em Olá URI. Se a fonte de dados de saudação não existir, ele será criado.

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]

> [!NOTE]
> número máximo de saudação de indexadores permitido varia de acordo com a camada de preços. serviço gratuito Olá permite que até too3 indexadores. O serviço padrão permite 50 indexadores. Veja [Limites de Serviço](search-limits-quotas-capacity.md) para obter detalhes.
> 
> 

Olá `api-version` é necessária. versão atual do Hello é `2015-02-28`. 

Olá `api-key` deve ser uma chave de administração (como a chave de consulta tooa contrário). Consulte a seção autenticação toohello [API REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais sobre as chaves. [Criar um serviço de pesquisa no portal de saudação](search-create-service-portal.md) explica como a URL do serviço tooget hello e propriedades de chave usado na solicitação de saudação.

<a name="CreateIndexerRequestSyntax"></a>
**Sintaxe do Corpo da Solicitação**

corpo de saudação da solicitação Olá contém uma definição do indexador, que especifica a fonte de dados de saudação e o índice de destino de saudação da indexação, bem como a agenda de indexação opcional e parâmetros. 

sintaxe de saudação para estruturar a carga de solicitação de saudação é da seguinte maneira. Uma solicitação de exemplo é fornecida mais adiante neste tópico.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello indexer",
        "description" : "Optional. Anything you want, or null",
        "dataSourceName" : "Required. hello name of an existing data source",
        "targetIndexName" : "Required. hello name of an existing index",
        "schedule" : { Optional. See Indexing Schedule below. },
        "parameters" : { Optional. See Indexing Parameters below. },
        "fieldMappings" : { Optional. See Field Mappings below. },
        "disabled" : Optional boolean value indicating whether hello indexer is disabled. False by default.  
    }

**Agenda do indexador**

Um indexador pode, também, especificar uma agenda. Se uma agenda estiver presente, indexador Olá será executado periodicamente de acordo com a agenda. Agenda tem Olá seguintes atributos:

* `interval`: obrigatório. Um valor de duração que especifica o intervalo ou período de execução do indexador. Olá menor permitido intervalo é de 5 minutos; Olá mais longo é um dia. Ele deve ser formatado como um valor XSD de "dayTimeDuration" (um subconjunto restrito de um [valor de duração ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) ). saudação padrão para isso é: `"P[nD][T[nH][nM]]"`. Exemplos: `PT15M` para cada 15 minutos, `PT2H` para cada 2 horas. 
* `startTime`: obrigatório. Uma data e hora UTC quando o indexador Olá deve iniciar a execução. 

**Parâmetros do indexador**

Um indexador pode, opcionalmente, especificar vários parâmetros que afetam seu comportamento. Todos os parâmetros de saudação são opcionais.  

* `maxFailedItems`: número de saudação de itens que podem falhar toobe indexados antes da execução de um indexador é considerado uma falha. O padrão é 0. Informações sobre itens com falha são retornadas pela Olá [obter Status do indexador](#GetIndexerStatus) operação. 
* `maxFailedItemsPerBatch`: número de saudação de itens que podem falhar toobe indexados em cada lote antes da execução de um indexador é considerado uma falha. O padrão é 0.
* `base64EncodeKeys`: especifica se as chaves de documento serão ou não codificadas em base 64. O Azure Search impõe restrições em relação aos caracteres que podem estar presentes em uma chave de documento. No entanto, os valores de saudação da fonte de dados podem conter caracteres inválidos. Se for necessário tooindex como valores como chaves de documento, este sinalizador pode ser definido tootrue. O padrão é `false`.
* `batchSize`: Especifica o número de saudação de itens que são lidos da fonte de dados hello e indexados como um único lote no desempenho de tooimprove de ordem. padrão de saudação depende de tipo de fonte de dados de saudação: é 1000 para o SQL Azure e o banco de dados do Azure Cosmos e 10 para o armazenamento de BLOBs do Azure.

**Mapeamentos de campo**

Você pode usar mapeamentos de campo toomap um nome de campo no hello dados fonte tooa outro nome de campo no índice de destino de saudação. Por exemplo, considere uma tabela de origem com um campo `_id`. A pesquisa do Azure não permite que um nome de campo iniciados com um sublinhado, portanto Olá campo deve ser renomeado. Isso pode ser feito usando Olá `fieldMappings` propriedade do indexador de saudação da seguinte maneira: 

    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ] 

Você pode especificar vários mapeamentos de campo: 

    "fieldMappings" : [ 
        { "sourceFieldName" : "_id", "targetFieldName" : "id" },
        { "sourceFieldName" : "_timestamp", "targetFieldName" : "timestamp" },
     ]

Nomes de campos de origem e destino diferenciam maiúsculas de minúsculas.

<a name="FieldMappingFunctions"></a>
***Funções de mapeamento de campo***

Mapeamentos de campo também podem ser usado tootransform valores de campo de origem usando *mapeando funções*.

Apenas uma dessas funções tem suporte: `jsonArrayToStringCollection`. Ele analisa um campo que contém uma cadeia de caracteres formatada como uma matriz JSON em um campo Collection no índice de destino hello. Ele se destina ao uso com o indexador do Azure SQL em particular, pois o SQL não tem um tipo de dados nativo de coleção. Ele pode ser usado da seguinte maneira: 

    "fieldMappings" : [ { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } } ] 

Por exemplo, se hello o campo de origem contém cadeia de caracteres hello `["red", "white", "blue"]`, e o campo de destino de saudação do tipo `Collection(Edm.String)` será preenchida com valores hello três `"red"`, `"white"` e `"blue"`.

Observe que Olá `targetFieldName` propriedade é opcional; se for deixado, Olá `sourceFieldName` valor é usado. 

<a name="CreateIndexerRequestExamples"></a>
**Exemplos de corpo da solicitação**

Olá, exemplo a seguir cria um indexador que copia dados da tabela Olá referenciada por Olá `ordersds` toohello da fonte de dados `orders` índice em uma agenda que inicia em 1 de janeiro de 2015 UTC e é executado por hora. Cada invocação de indexador será bem-sucedida se não mais do que 5 itens falharem toobe indexado em lote e não mais do que 10 itens falharem toobe indexado no total. 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }

**Resposta**

201 Criado para uma solicitação bem-sucedida.

<a name="UpdateIndexer"></a>

## <a name="update-indexer"></a>Atualizar Indexador
Você pode atualizar um indexador usando uma solicitação HTTP PUT. Especifique o nome de saudação de saudação indexador tooupdate no URI de solicitação de saudação:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Olá `api-version` é necessária. versão atual do Hello é `2015-02-28`. 

Olá `api-key` deve ser uma chave de administração (como a chave de consulta tooa contrário). Consulte a seção autenticação toohello [API REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais sobre as chaves. [Criar um serviço de pesquisa no portal de saudação](search-create-service-portal.md) explica como a URL do serviço tooget hello e propriedades de chave usado na solicitação de saudação.

**Solicitação**

Olá sintaxe do corpo de solicitação é Olá mesmos para [criar indexador solicitações](#CreateIndexerRequestSyntax).

**Resposta**

Para uma solicitação bem-sucedida: 201 Criado se um novo indexador for criado e 204 sem Conteúdo se um indexador existente for atualizado.

<a name="ListIndexers"></a>

## <a name="list-indexers"></a>Listar Indexadores
Olá **listar indexadores** operação retorna a lista de saudação de indexadores em seu serviço de pesquisa do Azure. 

    GET https://[service name].search.windows.net/indexers?api-version=[api-version]
    api-key: [admin key]


Olá `api-version` é necessária. versão de visualização de saudação é `2015-02-28-Preview`. [Controle de versão do Azure Search](https://msdn.microsoft.com/library/azure/dn864560.aspx) tem detalhes e mais informações sobre versões alternativas.

Olá `api-key` deve ser uma chave de administração (como a chave de consulta tooa contrário). Consulte a seção autenticação toohello [API REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais sobre as chaves. [Criar um serviço de pesquisa no portal de saudação](search-create-service-portal.md) explica como a URL do serviço tooget hello e propriedades de chave usado na solicitação de saudação.

**Resposta**

Para uma solicitação bem-sucedida: 200 OK.

Aqui está um exemplo de corpo de resposta:

    {
      "value" : [
      {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        ... other indexer properties
      }]
    }

Observe que você pode filtrar a resposta Olá para propriedades de saudação toojust em que você estiver interessado. Por exemplo, se você quiser apenas uma lista de nomes de indexadores, use Olá OData `$select` opção de consulta:

    GET /indexers?api-version=2014-10-20-Preview&$select=name

Nesse caso, resposta Olá Olá acima exemplo seria exibida da seguinte maneira: 

    {
      "value" : [ { "name": "myindexer" } ]
    }

Isso é uma largura de banda de toosave técnica útil se você tiver muitos indexadores em seu serviço de pesquisa.

<a name="GetIndexer"></a>

## <a name="get-indexer"></a>Obter Indexador
Olá **obter indexador** operação obtém a definição do indexador Olá da pesquisa do Azure.

    GET https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Olá `api-version` é necessária. versão de visualização de saudação é `2015-02-28-Preview`. 

Olá `api-key` deve ser uma chave de administração (como a chave de consulta tooa contrário). Consulte a seção autenticação toohello [API REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais sobre as chaves. [Criar um serviço de pesquisa no portal de saudação](search-create-service-portal.md) explica como a URL do serviço tooget hello e propriedades de chave usado na solicitação de saudação.

**Resposta**

Código de status: 200 OK é retornado para uma resposta bem-sucedida.

resposta de saudação é semelhante tooexamples no [indexador criar solicitações de exemplo](#CreateIndexerRequestExamples): 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }


<a name="DeleteIndexer"></a>

## <a name="delete-indexer"></a>Excluir Indexador
Olá **excluir indexador** operação remove um indexador do seu serviço de pesquisa do Azure.

    DELETE https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Quando um indexador é excluído, execuções do indexador Olá em andamento no momento serão executado toocompletion, mas nenhuma outra execução será agendada. Tentativas toouse que um indexador inexistente resultará no código de status HTTP 404 não encontrado. 

Olá `api-version` é necessária. versão de visualização de saudação é `2015-02-28-Preview`. 

Olá `api-key` deve ser uma chave de administração (como a chave de consulta tooa contrário). Consulte a seção autenticação toohello [API REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais sobre as chaves. [Criar um serviço de pesquisa no portal de saudação](search-create-service-portal.md) explica como a URL do serviço tooget hello e propriedades de chave usado na solicitação de saudação.

**Resposta**

Código de status: 204 Sem Conteúdo é retornado para uma resposta bem-sucedida.

<a name="RunIndexer"></a>

## <a name="run-indexer"></a>Executar indexador
Adição toorunning periodicamente em um agendamento, um indexador também pode ser invocado sob demanda por meio de saudação **executar indexador** operação: 

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=[api-version]
    api-key: [admin key]

Olá `api-version` é necessária. versão de visualização de saudação é `2015-02-28-Preview`. 

Olá `api-key` deve ser uma chave de administração (como a chave de consulta tooa contrário). Consulte a seção autenticação toohello [API REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais sobre as chaves. [Criar um serviço de pesquisa no portal de saudação](search-create-service-portal.md) explica como a URL do serviço tooget hello e propriedades de chave usado na solicitação de saudação.

**Resposta**

Código de status: 202 Aceito é retornado para uma resposta bem-sucedida.

<a name="GetIndexerStatus"></a>

## <a name="get-indexer-status"></a>Obter Status do Indexador
Olá **obter Status do indexador** operação recupera Olá atual status de histórico de execução e de um indexador: 

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=[api-version]
    api-key: [admin key]


Olá `api-version` é necessária. versão de visualização de saudação é `2015-02-28-Preview`. 

Olá `api-key` deve ser uma chave de administração (como a chave de consulta tooa contrário). Consulte a seção autenticação toohello [API REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais sobre as chaves. [Criar um serviço de pesquisa no portal de saudação](search-create-service-portal.md) explica como a URL do serviço tooget hello e propriedades de chave usado na solicitação de saudação.

**Resposta**

Código de status: 200 OK para uma resposta bem-sucedida.

corpo da resposta Olá contém informações sobre o status de integridade geral do indexador, última chamada do indexador hello, bem como o histórico de saudação do recente invocações do indexador (se houver). 

Um exemplo de corpo de resposta tem esta aparência: 

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

**Status do Indexador**

Status do indexador pode ser um dos Olá valores a seguir:

* `running`indica que Olá indexador está funcionando normalmente. Observe que algumas das execuções do indexador Olá podem ainda estar falhando, portanto, é uma saudação de toocheck boa ideia `lastResult` propriedade também. 
* `error`indica que indexador Olá encontrou um erro que não pode ser corrigido sem intervenção humana. Por exemplo, credenciais de fonte de dados Olá podem ter expirado ou esquema Olá Olá da fonte de dados ou de índice de destino Olá foi alterado em uma quebra maneira. 

**Resultado da Execução do Indexador**

Um resultado de execução do indexador contém informações sobre a execução de um único indexador. resultado mais recente Olá é exposto como Olá `lastResult` propriedade de status do indexador hello. Outros resultados recentes, se presente, serão retornados como Olá `executionHistory` propriedade de status do indexador hello. 

Resultado da execução do indexador contém Olá propriedades a seguir: 

* `status`: Olá status de uma execução. Consulte [Status de Execução do Indexador](#IndexerExecutionStatus) a seguir para obter detalhes. 
* `errorMessage`: mensagem de erro para uma execução com falha. 
* `startTime`: tempo de saudação em UTC quando essa execução foi iniciada.
* `endTime`: tempo de saudação em UTC quando essa execução finalizada. Esse valor não é definido se a execução de saudação ainda está em andamento.
* `errors`: uma matriz de erros de nível de item, se houver. Cada entrada contém uma chave de documento (`key` propriedade) e uma mensagem de erro (`errorMessage` propriedade). 
* `itemsProcessed`: Olá o número de itens de fonte de dados (por exemplo, linhas de tabela) que Olá indexador tentada tooindex durante essa execução. 
* `itemsFailed`: Olá o número de itens que falharam durante essa execução.  
* `initialTrackingState`: sempre `null` para a primeira execução do indexador hello, ou se a política de controle de alteração dados saudação não está habilitada na fonte de dados de saudação usada. Se essa política estiver habilitada, em execuções subsequentes esse valor indica Olá primeiro (menor) do controle de alterações valor processado por essa execução. 
* `finalTrackingState`: sempre `null` se a política de controle de alteração de dados de saudação não está habilitado na fonte de dados de saudação usada. Caso contrário, indica hello mais recente (maior) de controle de alterações com êxito é processado por essa execução de valor. 

<a name="IndexerExecutionStatus"></a>
**Status de Execução do Indexador**

Status de execução do indexador captura o status de saudação de uma execução de indexador único. Ele pode ter Olá valores a seguir:

* `success`indica que a execução do indexador Olá foi concluída com êxito.
* `inProgress`indica que a execução do indexador hello está em andamento. 
* `transientFailure` indica que a execução de um indexador falhou. Consulte a propriedade `errorMessage` para obter detalhes. Falha de saudação pode ou não exigir intervenção humana toofix - por exemplo, corrigir uma incompatibilidade de esquema entre a fonte de dados de saudação e o índice de destino Olá exige ação do usuário, enquanto um tempo de inatividade de fonte de dados temporários, não. As invocações do indexador continuarão de acordo com a agenda, se houver. 
* `persistentFailure`indica que indexador Olá falhou em uma forma que requer intervenção humana. As execuções agendadas do indexador param. Depois de abordar o problema hello, use redefinir indexador API toorestart Olá agendado de execuções. 
* `reset`indica que indexador Olá foi redefinido por tooReset uma chamada de API do indexador (veja abaixo). 

<a name="ResetIndexer"></a>

## <a name="reset-indexer"></a>Redefinir Indexador
Olá **redefinir indexador** operação redefine o estado associado indexador de saudação do controle de alterações de saudação. Isso permite que você tootrigger a reindexação (por exemplo, se o esquema de fonte de dados foi alterado) do zero ou política de detecção de alteração toochange Olá dados para uma fonte de dados associada Olá indexador.   

    POST https://[service name].search.windows.net/indexers/[indexer name]/reset?api-version=[api-version]
    api-key: [admin key]

Olá `api-version` é necessária. versão de visualização de saudação é `2015-02-28-Preview`. 

Olá `api-key` deve ser uma chave de administração (como a chave de consulta tooa contrário). Consulte a seção autenticação toohello [API REST do serviço de pesquisa](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn mais sobre as chaves. [Criar um serviço de pesquisa no portal de saudação](search-create-service-portal.md) explica como a URL do serviço tooget hello e propriedades de chave usado na solicitação de saudação.

**Resposta**

Código de status: 204 sem Conteúdo para uma resposta bem-sucedida.

## <a name="mapping-between-sql-data-types-and-azure-search-data-types"></a>Mapeamento entre tipos de dados SQL e tipos de dados do Azure Search
<table style="font-size:12">
<tr>
<td>Tipo de dados SQL</td>    
<td>Tipos de campos de índice de destino permitidos</td>
<td>Observações</td>
</tr>
<tr>
<td>bit</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>int, smallint, tinyint</td>
<td>Edm.Int32, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>bigint</td>
<td>Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>real, float</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>smallmoney, dinheiro<br>decimal<br>numérico
</td>
<td>Edm.String</td>
<td>O Azure Search não dá suporte à conversão de tipos decimais em Edm.Double porque isso causaria a perda de precisão
</td>
</tr>
<tr>
<td>char, nchar, varchar, nvarchar</td>
<td>Edm.String<br/>Collection(Edm.String)</td>
<td>Consulte [funções de mapeamento de campos](#FieldMappingFunctions) neste documento para obter detalhes sobre como tootransform uma coluna de cadeia de caracteres em um Collection</td>
</tr>
<tr>
<td>smalldatetime, datetime, datetime2, date, datetimeoffset</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>uniqueidentifer</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>geografia</td>
<td>Edm.GeographyPoint</td>
<td>Somente instâncias de Geografia do tipo POINT com SRID 4326 (que é o padrão de saudação) têm suporte</td>
</tr>
<tr>
<td>rowversion</td>
<td>N/D</td>
<td>Colunas de versão de linha não podem ser armazenadas no índice de pesquisa hello, mas eles podem ser usados para controle de alterações</td>
</tr>
<tr>
<td>tempo, período de tempo<br>binário, varbinary, imagem<br>XML, geometria, tipos CLR</td>
<td>N/D</td>
<td>Sem suporte</td>
</tr>
</table>

## <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Mapeamento entre tipos de dados JSON e tipos de dados da Pesquisa do Azure
<table style="font-size:12">
<tr>
<td>Tipo de dados JSON</td>    
<td>Tipos de campos de índice de destino permitidos</td>
<td>Observações</td>
</tr>
<tr>
<td>bool</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Números integrais</td>
<td>Edm.Int32, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Números de ponto flutuante</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>string</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>Matrizes de tipos primitivos, como [ "a", "b", "c" ]</td>
<td>Collection(Edm.String)</td>
<td></td>
</tr>
<tr>
<td>Cadeias de caracteres que se parecem com datas</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Objetos de ponto GeoJSON</td>
<td>Edm.GeographyPoint</td>
<td>Os pontos GeoJSON são objetos JSON em Olá formato a seguir: {"type": "Point", "coordinates": [longo, lat]} </td>
</tr>
<tr>
<td>Outros objetos JSON</td>
<td>N/D</td>
<td>Sem suporte; no momento, o Azure Search dá suporte apenas a tipos primitivos e coleções de cadeias de caracteres</td>
</tr>
</table>
