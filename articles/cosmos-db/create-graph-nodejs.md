---
title: aaaBuild um aplicativo de Node.js do Azure Cosmos banco de dados usando a API do Graph | Microsoft Docs
description: "Apresenta um exemplo de código de Node. js que você pode usar tooconnect tooand consultar o banco de dados do Azure Cosmos"
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: daacbabf-1bb5-497f-92db-079910703046
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 07/14/2017
ms.author: denlee
ms.openlocfilehash: 1445755842bc4e4a84ca2b2f789aadde8467e190
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-nodejs-application-by-using-graph-api"></a>Azure Cosmos DB: Compilar um aplicativo Node.js usando a API do Graph

Banco de dados do Azure Cosmos é serviço de banco de dados de vários modelos de Olá globalmente distribuída da Microsoft. Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente. 

Este artigo de início rápido demonstra como toocreate um banco de dados do Azure Cosmos a conta para a API do Graph (visualização), o banco de dados e o gráfico usando Olá portal do Azure. Em seguida, compilar e executar um aplicativo de console usando Olá código-fonte aberto [Gremlin Node.js](https://www.npmjs.com/package/gremlin-secure) driver.  

> [!NOTE]
> módulo de npm Olá `gremlin-secure` é uma versão modificada do `gremlin` módulo, com suporte para SSL e SASL necessárias para conectar-se com o banco de dados do Azure Cosmos. O código-fonte está disponível no [GitHub](https://github.com/CosmosDB/gremlin-javascript).
>

## <a name="prerequisites"></a>Pré-requisitos

Antes de executar este exemplo, você deve ter Olá pré-requisitos a seguir:
* [Node.js](https://nodejs.org/en/) versão v0.10.29 ou posterior
* [Git](http://git-scm.com/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Crie uma conta de banco de dados

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <a name="add-a-graph"></a>Adicionar um gráfico

[!INCLUDE [cosmos-db-create-graph](../../includes/cosmos-db-create-graph.md)]

## <a name="clone-hello-sample-application"></a>Clonar um aplicativo de exemplo hello

Agora vamos aplicativo clone uma API do Graph do GitHub, defina a cadeia de caracteres de conexão hello e executá-lo. Você verá como é fácil toowork com dados programaticamente. 

1. Abra uma janela de terminal de Git, como o Git Bash e altere (via `cd` comando) tooa diretório de trabalho.  

2. Execute Olá repositório de exemplo do comando tooclone Olá a seguir. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-graph-nodejs-getting-started.git
    ```

3. Abra o arquivo de solução de saudação no Visual Studio. 

## <a name="review-hello-code"></a>Examine o código de saudação

Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello. Olá abrir `app.js` arquivo e você encontrará Olá linhas de código a seguir. 

* cliente de Gremlin Olá é criado.

    ```nodejs
    const client = Gremlin.createClient(
        443, 
        config.endpoint, 
        { 
            "session": false, 
            "ssl": true, 
            "user": `/dbs/${config.database}/colls/${config.collection}`,
            "password": config.primaryKey
        });
    ```

  Olá configurações estão todos em `config.js`, que podemos Editar Olá seção a seguir.

* Uma série de etapas de Gremlin são executados com hello `client.execute` método.

    ```nodejs
    console.log('Running Count'); 
    client.execute("g.V().count()", { }, (err, results) => {
        if (err) return console.error(err);
        console.log(JSON.stringify(results));
        console.log();
    });
    ```

## <a name="update-your-connection-string"></a>Atualizar sua cadeia de conexão

1. Arquivo de config.js Olá aberto. 

2. Na config.js, preencha chave config.endpoint Olá Olá **Gremlin URI** valor da saudação **visão geral** página de saudação portal do Azure. 

    `config.endpoint = "GRAPHENDPOINT";`

    ![Exibir e copiar uma folha de chaves, a chave de acesso no portal do Azure de saudação](./media/create-graph-nodejs/gremlin-uri.png)

   Se hello **Gremlin URI** valor estiver em branco, você pode gerar o valor de saudação do hello **chaves** página no portal de hello, usando Olá **URI** https:// de remoção e alteração de valor toographs de documentos.

   o ponto de extremidade do Hello Gremlin deve ser somente nome de host de saudação sem número de porta do protocolo de saudação, como `mygraphdb.graphs.azure.com` (não `https://mygraphdb.graphs.azure.com` ou `mygraphdb.graphs.azure.com:433`).

3. Na config.js, preencha o valor de config.primaryKey Olá com hello **chave primária** valor da saudação **chaves** página de saudação portal do Azure. 

    `config.primaryKey = "PRIMARYKEY";`

   ![Olá folha de chaves de portal do Azure](./media/create-graph-nodejs/keys.png)

4. Insira o nome do banco de dados de saudação e nome do gráfico (contêiner) para valor de saudação do config.database e config.collection. 

Aqui está um exemplo da aparência seu arquivo config.js concluído:

```nodejs
var config = {}

// Note that this must not have HTTPS or hello port number
config.endpoint = "testgraphacct.graphs.azure.com";
config.primaryKey = "Pams6e7LEUS7LJ2Qk0fjZf3eGo65JdMWHmyn65i52w8ozPX2oxY3iP0yu05t9v1WymAHNcMwPIqNAEv3XDFsEg==";
config.database = "graphdb"
config.collection = "Persons"

module.exports = config;
```

## <a name="run-hello-console-app"></a>Execute o aplicativo de console Olá

1. Abra uma janela do terminal e alterar (por meio de `cd` comando) toohello o diretório de instalação para o arquivo Package. JSON de Olá que está incluído no projeto de saudação.  

2. Executar `npm install` tooinstall Olá necessário npm módulos, incluindo `gremlin-secure`.

3. Executar `node app.js` em um terminal toostart seu aplicativo de nó.

## <a name="browse-with-data-explorer"></a>Procurar com o Data Explorer

Agora você pode voltar tooData Explorer no hello tooview portal do Azure, consultar, modificar e trabalhar com os novos dados de gráfico.

No Explorador de dados, o novo banco de dados de saudação aparece no hello **gráficos** painel. Expanda o banco de dados do hello, seguido por coleção Olá, e clique em **gráfico**.

dados Olá gerados pelo aplicativo de exemplo hello são exibidos no painel de Avançar hello dentro Olá **gráfico** guia quando você clica em **Aplicar filtro**.

Tente concluir `g.V()` com `.has('firstName', 'Thomas')` tootest filtro de saudação. Observe que o valor de saudação diferencia maiusculas de minúsculas.

## <a name="review-slas-in-hello-azure-portal"></a>Examine os SLAs em Olá portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-your-resources"></a>Limpar seus recursos

Se você não planeja toocontinue usando este aplicativo, exclua todos os recursos que você criou neste artigo, Olá seguinte: 

1. No hello portal do Azure, no menu de navegação à esquerda do hello, clique em **grupos de recursos**e clique em nome de saudação do recurso de saudação que você criou. 
2. Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toobe excluído e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Neste artigo, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, crie um gráfico usando o Explorador de dados e executar o aplicativo. Agora, você pode criar consultas mais complexas e implementar uma lógica de passagem de gráfico avançada usando o Gremlin. 

> [!div class="nextstepaction"]
> [Consultar usando o Gremlin](tutorial-query-graph.md)
