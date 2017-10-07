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
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="033f2-104">Usar o MongoChef com uma conta do Azure Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="033f2-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="033f2-105">tooconnect tooan o banco de dados do Azure Cosmos: API de conta do MongoDB, você deve:</span><span class="sxs-lookup"><span data-stu-id="033f2-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="033f2-106">Baixar e instalar o [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="033f2-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="033f2-107">Ter as informações de [cadeia de conexão](connect-mongodb-account.md) de sua conta do Azure Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="033f2-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-hello-connection-in-mongochef"></a><span data-ttu-id="033f2-108">Criar conexão Olá no MongoChef</span><span class="sxs-lookup"><span data-stu-id="033f2-108">Create hello connection in MongoChef</span></span>
<span data-ttu-id="033f2-109">tooadd seu banco de dados do Azure Cosmos: API para o MongoDB conta toohello MongoChef Gerenciador de conexão, execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="033f2-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello MongoChef connection manager, perform hello following steps.</span></span>

1. <span data-ttu-id="033f2-110">Recuperar o banco de dados do Azure Cosmos: API para obter informações de conexão MongoDB usando instruções Olá [aqui](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="033f2-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Captura de tela da folha de cadeia de caracteres de conexão Olá](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="033f2-112">Clique em **conectar** tooopen Olá Gerenciador de Conexão, clique em **nova Conexão**</span><span class="sxs-lookup"><span data-stu-id="033f2-112">Click **Connect** tooopen hello Connection Manager, then click **New Connection**</span></span>

    ![Captura de tela do Gerenciador de conexão de MongoChef Olá](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="033f2-114">Em Olá **nova Conexão** janela Olá **Server** , insira Olá HOST (FQDN) do hello Azure Cosmos DB: API para a porta de conta e hello MongoDB.</span><span class="sxs-lookup"><span data-stu-id="033f2-114">In hello **New Connection** window, on hello **Server** tab, enter hello HOST (FQDN) of hello Azure Cosmos DB: API for MongoDB account and hello PORT.</span></span>

    ![Captura de tela da guia servidor de Gerenciador de conexão do hello MongoChef](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="033f2-116">Em Olá **nova Conexão** janela Olá **autenticação** guia, escolha o modo de autenticação **Standard (MONGODB CR ou SCARM-SHA-1)** e digite Olá nome de usuário e SENHA.</span><span class="sxs-lookup"><span data-stu-id="033f2-116">In hello **New Connection** window, on hello **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter hello USERNAME and PASSWORD.</span></span>  <span data-ttu-id="033f2-117">Aceite o saudação padrão autenticação db (admin) ou fornecer seu próprio valor.</span><span class="sxs-lookup"><span data-stu-id="033f2-117">Accept hello default authentication db (admin) or provide your own value.</span></span>

    ![Captura de tela da guia de autenticação de Gerenciador de conexão do hello MongoChef](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="033f2-119">Em Olá **nova Conexão** janela Olá **SSL** guia, verifique Olá **usar SSL protocolo tooconnect** caixa de seleção e hello **SSL autoassinado do servidor de aceitar certificados** botão de opção.</span><span class="sxs-lookup"><span data-stu-id="033f2-119">In hello **New Connection** window, on hello **SSL** tab, check hello **Use SSL protocol tooconnect** check box and hello **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Captura de tela da guia SSL de Gerenciador de conexão do hello MongoChef](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="033f2-121">Clique em Olá **Conexão de teste** toovalidate informações de conexão de saudação, clique em **Okey** tooreturn janela de Conexão nova toohello e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="033f2-121">Click hello **Test Connection** button toovalidate hello connection information, click **OK** tooreturn toohello New Connection window, and then click **Save**.</span></span>

    ![Captura de tela da janela de conexão de teste Olá MongoChef](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-toocreate-a-database-collection-and-documents"></a><span data-ttu-id="033f2-123">Use MongoChef toocreate um banco de dados, coleção e documentos</span><span class="sxs-lookup"><span data-stu-id="033f2-123">Use MongoChef toocreate a database, collection, and documents</span></span>
<span data-ttu-id="033f2-124">toocreate um banco de dados, coleção e documentos usando MongoChef, executam Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="033f2-124">toocreate a database, collection, and documents using MongoChef, perform hello following steps.</span></span>

1. <span data-ttu-id="033f2-125">Em **Gerenciador de Conexão**, realce conexão hello e clique em **conectar**.</span><span class="sxs-lookup"><span data-stu-id="033f2-125">In **Connection Manager**, highlight hello connection and click **Connect**.</span></span>

    ![Captura de tela do Gerenciador de conexão de MongoChef Olá](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="033f2-127">Clique com botão direito host hello e escolha **Adicionar banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="033f2-127">Right click hello host and choose **Add Database**.</span></span>  <span data-ttu-id="033f2-128">Forneça um nome de banco de dados e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="033f2-128">Provide a database name and click **OK**.</span></span>

    ![Captura de tela de saudação opção MongoChef Adicionar banco de dados](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="033f2-130">Banco de dados de saudação clique com botão direito e escolha **adicionar coleção**.</span><span class="sxs-lookup"><span data-stu-id="033f2-130">Right click hello database and choose **Add Collection**.</span></span>  <span data-ttu-id="033f2-131">Forneça um nome de coleção e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="033f2-131">Provide a collection name and click **Create**.</span></span>

    ![Captura de tela de saudação opção MongoChef adicionar coleção](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="033f2-133">Clique em Olá **coleção** menu item, em seguida, clique em **Adicionar documento**.</span><span class="sxs-lookup"><span data-stu-id="033f2-133">Click hello **Collection** menu item, then click **Add Document**.</span></span>

    ![Captura de tela hello MongoChef Adicionar documento do item de menu](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="033f2-135">Na caixa de diálogo de Adicionar documento hello, cole o seguinte hello e, em seguida, clique em **Adicionar documento**.</span><span class="sxs-lookup"><span data-stu-id="033f2-135">In hello Add Document dialog, paste hello following and then click **Add Document**.</span></span>

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
6. <span data-ttu-id="033f2-136">Adicione outro documento, dessa vez com hello conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="033f2-136">Add another document, this time with hello following content.</span></span>

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
7. <span data-ttu-id="033f2-137">Execute uma consulta de exemplo.</span><span class="sxs-lookup"><span data-stu-id="033f2-137">Execute a sample query.</span></span> <span data-ttu-id="033f2-138">Por exemplo, procure famílias com Olá Sobrenome 'Andersen' e os pais de retorno hello e campos de estado.</span><span class="sxs-lookup"><span data-stu-id="033f2-138">For example, search for families with hello last name 'Andersen' and return hello parents and state fields.</span></span>

    ![Captura de tela dos resultados de consulta do MongoChef](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="033f2-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="033f2-140">Next steps</span></span>
* <span data-ttu-id="033f2-141">Conheça as [amostras](mongodb-samples.md) do Azure Cosmos DB: API para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="033f2-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
