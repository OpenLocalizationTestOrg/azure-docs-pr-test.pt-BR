---
title: "Cosmos do Azure DB: Criar um aplicativo com Python e Olá API DocumentDB | Microsoft Docs"
description: "Apresenta um exemplo de código do Python pode usar tooconnect tooand consulta Olá API DocumentDB do Azure Cosmos DB"
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 51c11be2-af6d-425f-a86a-39cbfe61da29
ms.service: cosmos-db
ms.custom: quick start connect, mvc
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: hero-article
ms.date: 05/13/2017
ms.author: mimig
ms.openlocfilehash: e66965ab493c6ef693e88a3767a401d39e1bde2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-build-a-documentdb-api-app-with-python-and-hello-azure-portal"></a>Banco de dados do Azure do Cosmos: Criar um aplicativo de API de documentos com Python e Olá portal do Azure

O BD Cosmos do Azure é o serviço multimodelo de banco de dados distribuído globalmente da Microsoft. Você pode criar e consultar documentos, chave/valor e bancos de dados do gráfico, que se beneficiar de distribuição global hello e recursos de escala horizontal no núcleo de saudação do banco de dados do Azure Cosmos rapidamente. 

Este guia rápido demonstra como toocreate uma conta de banco de dados do Azure Cosmos, o banco de dados de documento e a coleção usando Olá portal do Azure. Você, em seguida, compilar e executar um aplicativo de console criado em Olá [API de Python do DocumentDB](documentdb-sdk-python.md).

## <a name="prerequisites"></a>Pré-requisitos

* Antes de executar este exemplo, você deve ter Olá pré-requisitos a seguir:
    * [Visual Studio 2015](http://www.visualstudio.com/) ou superior.
    * Ferramentas Python para o Visual Studio do [GitHub](http://microsoft.github.io/PTVS/). Este tutorial usa as Ferramentas Python para o VS 2015.
    * Python 2.7 de [python.org](https://www.python.org/downloads/release/python-2712/)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a>Crie uma conta de banco de dados

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a name="add-a-collection"></a>Adicionar uma coleção

[!INCLUDE [cosmos-db-create-collection](../../includes/cosmos-db-create-collection.md)]

## <a name="clone-hello-sample-application"></a>Clonar um aplicativo de exemplo hello

Agora vamos clone uma API de documentos de aplicativo do github, defina a cadeia de caracteres de conexão hello e executá-lo. Você verá como é fácil toowork com dados programaticamente. 

1. Abra uma janela de terminal de git, como git bash, e `cd` tooa diretório de trabalho.  

2. Execute Olá repositório de exemplo do comando tooclone Olá a seguir. 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-documentdb-python-getting-started.git
    ```  
## <a name="review-hello-code"></a>Examine o código de saudação

Vamos fazer uma rápida revisão do que está acontecendo no aplicativo hello. Olá abrir DocumentDBGetStarted.py de arquivo e você encontrará que essas linhas de código criam Olá recursos de banco de dados do Azure Cosmos. 


* Olá DocumentClient é inicializado.

    ```python
    # Initialize hello Python DocumentDB client
    client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
    ```

* Um novo banco de dados é criado.

    ```python
    # Create a database
    db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })
    ```

* Uma nova coleção é criada.

    ```python
    # Create collection options
    options = {
        'offerEnableRUPerMinuteThroughput': True,
        'offerVersion': "V2",
        'offerThroughput': 400
    }

    # Create a collection
    collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)
    ```

* Alguns documentos são criados.

    ```python
    # Create some documents
    document1 = client.CreateDocument(collection['_self'],
        { 
            'id': 'server1',
            'Web Site': 0,
            'Cloud Service': 0,
            'Virtual Machine': 0,
            'name': 'some' 
        })
    ```

* Uma consulta é executada usando SQL

    ```python
    # Query them in SQL
    query = { 'query': 'SELECT * FROM server s' }    
            
    options = {} 
    options['enableCrossPartitionQuery'] = True
    options['maxItemCount'] = 2

    result_iterable = client.QueryDocuments(collection['_self'], query, options)
    results = list(result_iterable);

    print(results)
    ```

## <a name="update-your-connection-string"></a>Atualizar sua cadeia de conexão

Agora volte toohello tooget portal do Azure suas informações de cadeia de caracteres de conexão e copie-o em um aplicativo hello.

1. Em Olá [portal do Azure](http://portal.azure.com/), em seu banco de dados do Cosmos do Azure da conta, na barra de navegação esquerda de saudação, clique em **chaves**e, em seguida, clique em **chaves de leitura-gravação**. Você usará botões de cópia de saudação na direita de saudação do hello toocopy da tela hello URI e a chave primária em Olá `DocumentDBGetStarted.py` arquivo na próxima etapa do hello.

    ![Exibir e copiar uma folha de chaves, a chave de acesso no portal do Azure de saudação](./media/create-documentdb-dotnet/keys.png)

2. Em aberto Olá `DocumentDBGetStarted.py` arquivo. 

3. Copie o valor URI do portal de saudação (usando o botão de cópia de saudação) e torná-lo Olá o valor da chave do ponto de extremidade Olá no `DocumentDBGetStarted.py`. 

    `config.ENDPOINT : "https://FILLME.documents.azure.com"`

4. Em seguida, copie o valor de chave primária do portal de saudação e torná-lo Olá valor Olá `config.MASTERKEY` em `DocumentDBGetStarted.py`. Agora que você atualizou seu aplicativo com todas as informações de saudação precisa toocommunicate com o banco de dados do Azure Cosmos. 

    `config.MASTERKEY : "FILLME"`
    
## <a name="run-hello-app"></a>Executar o aplicativo hello
1. No Visual Studio, clique com botão direito no projeto Olá no **Solution Explorer**, selecione o ambiente atual de Python hello e clique com botão direito.

2. Selecione Instalar Pacote do Python e digite **pydocumentdb**

3. Execute o aplicativo de hello toorun F5. Seu aplicativo é exibido no navegador. 

Agora você pode voltar tooData Explorer e consulte a consulta, modificar e trabalhar com esses novos dados. 

## <a name="review-slas-in-hello-azure-portal"></a>Examine os SLAs em Olá portal do Azure

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a>Limpar recursos

Se você não vai toocontinue toouse este aplicativo, exclua todos os recursos criados por este guia de início rápido Olá portal do Azure com hello etapas a seguir:

1. No menu esquerdo de saudação do hello portal do Azure, clique em **grupos de recursos** e clique em nome de saudação do recurso de saudação criado por você. 
2. Na sua página de grupo de recursos, clique em **excluir**, digite o nome de saudação do hello recurso toodelete na caixa de texto de saudação e, em seguida, clique em **excluir**.

## <a name="next-steps"></a>Próximas etapas

Este guia de início rápido, você aprendeu como toocreate uma conta de banco de dados do Azure Cosmos, crie uma coleção usando Olá Explorador de dados e executar o aplicativo. Agora você pode importar a conta de banco de dados do Cosmos tooyour dados adicionais. 

> [!div class="nextstepaction"]
> [Importe dados para o banco de dados do Azure Cosmos para Olá API DocumentDB](import-data.md)


