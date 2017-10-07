---
title: aaaUse MongoChef para o banco de dados do Azure Cosmos | Microsoft Docs
description: 'Saiba como toouse MongoChef com um banco de dados do Azure Cosmos: API de conta do MongoDB'
keywords: MongoChef
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 352c5fb9-8772-4c5f-87ac-74885e63ecac
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: anhoh
ms.openlocfilehash: 4b047797b231c34ccc6f2ed02416525c6228d596
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a>Usar o MongoChef com uma conta do Azure Cosmos DB: API para MongoDB

tooconnect tooan o banco de dados do Azure Cosmos: API de conta do MongoDB, você deve:

* Baixar e instalar o [MongoChef](http://3t.io/mongochef)
* Ter as informações de [cadeia de conexão](connect-mongodb-account.md) de sua conta do Azure Cosmos DB: API para MongoDB

## <a name="create-hello-connection-in-mongochef"></a>Criar conexão Olá no MongoChef
tooadd seu banco de dados do Azure Cosmos: API para o MongoDB conta toohello MongoChef Gerenciador de conexão, execute Olá etapas a seguir.

1. Recuperar o banco de dados do Azure Cosmos: API para obter informações de conexão MongoDB usando instruções Olá [aqui](connect-mongodb-account.md).

    ![Captura de tela da folha de cadeia de caracteres de conexão Olá](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. Clique em **conectar** tooopen Olá Gerenciador de Conexão, clique em **nova Conexão**

    ![Captura de tela do Gerenciador de conexão de MongoChef Olá](./media/mongodb-mongochef/ConnectionManager.png)
3. Em Olá **nova Conexão** janela Olá **Server** , insira Olá HOST (FQDN) do hello Azure Cosmos DB: API para a porta de conta e hello MongoDB.

    ![Captura de tela da guia servidor de Gerenciador de conexão do hello MongoChef](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. Em Olá **nova Conexão** janela Olá **autenticação** guia, escolha o modo de autenticação **Standard (MONGODB CR ou SCARM-SHA-1)** e digite Olá nome de usuário e SENHA.  Aceite o saudação padrão autenticação db (admin) ou fornecer seu próprio valor.

    ![Captura de tela da guia de autenticação de Gerenciador de conexão do hello MongoChef](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. Em Olá **nova Conexão** janela Olá **SSL** guia, verifique Olá **usar SSL protocolo tooconnect** caixa de seleção e hello **SSL autoassinado do servidor de aceitar certificados** botão de opção.

    ![Captura de tela da guia SSL de Gerenciador de conexão do hello MongoChef](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. Clique em Olá **Conexão de teste** toovalidate informações de conexão de saudação, clique em **Okey** tooreturn janela de Conexão nova toohello e, em seguida, clique em **salvar**.

    ![Captura de tela da janela de conexão de teste Olá MongoChef](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a>Use MongoChef toocreate um banco de dados, coleção e documentos
toocreate um banco de dados, coleção e documentos usando MongoChef, executam Olá etapas a seguir.

1. Em **Gerenciador de Conexão**, realce conexão hello e clique em **conectar**.

    ![Captura de tela do Gerenciador de conexão de MongoChef Olá](./media/mongodb-mongochef/ConnectToAccount.png)
2. Clique com botão direito host hello e escolha **Adicionar banco de dados**.  Forneça um nome de banco de dados e clique em **OK**.

    ![Captura de tela de saudação opção MongoChef Adicionar banco de dados](./media/mongodb-mongochef/AddDatabase1.png)
3. Banco de dados de saudação clique com botão direito e escolha **adicionar coleção**.  Forneça um nome de coleção e clique em **Criar**.

    ![Captura de tela de saudação opção MongoChef adicionar coleção](./media/mongodb-mongochef/AddCollection.png)
4. Clique em Olá **coleção** menu item, em seguida, clique em **Adicionar documento**.

    ![Captura de tela hello MongoChef Adicionar documento do item de menu](./media/mongodb-mongochef/AddDocument1.png)
5. Na caixa de diálogo de Adicionar documento hello, cole o seguinte hello e, em seguida, clique em **Adicionar documento**.

        {
        "_id": "AndersenFamily",
        "lastName": "Andersen",
        "parents": [
               { "firstName": "Thomas" },
               { "firstName": "Mary Kay"}
        ],
        "children": [
           {
               "firstName": "Henriette Thaulow", "gender": "female", "grade": 5,
               "pets": [{ "givenName": "Fluffy" }]
           }
        ],
        "address": { "state": "WA", "county": "King", "city": "seattle" },
        "isRegistered": true
        }
6. Adicione outro documento, dessa vez com hello conteúdo a seguir.

        {
        "_id": "WakefieldFamily",
        "parents": [
            { "familyName": "Wakefield", "givenName": "Robin" },
            { "familyName": "Miller", "givenName": "Ben" }
        ],
        "children": [
            {
                "familyName": "Merriam",
                 "givenName": "Jesse",
                "gender": "female", "grade": 1,
                "pets": [
                    { "givenName": "Goofy" },
                    { "givenName": "Shadow" }
                ]
            },
            {
                "familyName": "Miller",
                 "givenName": "Lisa",
                 "gender": "female",
                 "grade": 8 }
        ],
        "address": { "state": "NY", "county": "Manhattan", "city": "NY" },
        "isRegistered": false
        }
7. Execute uma consulta de exemplo. Por exemplo, procure famílias com Olá Sobrenome 'Andersen' e os pais de retorno hello e campos de estado.

    ![Captura de tela dos resultados de consulta do MongoChef](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a>Próximas etapas
* Conheça as [amostras](mongodb-samples.md) do Azure Cosmos DB: API para MongoDB.
