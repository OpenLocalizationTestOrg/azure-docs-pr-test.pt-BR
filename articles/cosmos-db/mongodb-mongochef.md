---
title: Usar o MongoChef no Azure Cosmos DB | Microsoft Docs
description: 'Saiba como usar o MongoChef com uma conta do Azure Cosmos DB: API para MongoDB'
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
ms.openlocfilehash: 54c9799bd646b827f602e2ea2f9a15a4fc853f00
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-mongochef-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="56190-104">Usar o MongoChef com uma conta do Azure Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="56190-104">Use MongoChef with an Azure Cosmos DB: API for MongoDB account</span></span>

<span data-ttu-id="56190-105">Para se conectar a uma conta do Azure Cosmos DB: API para MongoDB, é necessário:</span><span class="sxs-lookup"><span data-stu-id="56190-105">To connect to an Azure Cosmos DB: API for MongoDB account, you must:</span></span>

* <span data-ttu-id="56190-106">Baixar e instalar o [MongoChef](http://3t.io/mongochef)</span><span class="sxs-lookup"><span data-stu-id="56190-106">Download and install [MongoChef](http://3t.io/mongochef)</span></span>
* <span data-ttu-id="56190-107">Ter as informações de [cadeia de conexão](connect-mongodb-account.md) de sua conta do Azure Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="56190-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="create-the-connection-in-mongochef"></a><span data-ttu-id="56190-108">Criar a conexão no MongoChef</span><span class="sxs-lookup"><span data-stu-id="56190-108">Create the connection in MongoChef</span></span>
<span data-ttu-id="56190-109">Para adicionar sua conta do Azure Cosmos DB: API para MongoDB ao gerenciador de conexões do MongoChef, realize as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="56190-109">To add your Azure Cosmos DB: API for MongoDB account to the MongoChef connection manager, perform the following steps.</span></span>

1. <span data-ttu-id="56190-110">Recupere as informações de conexão do Azure Cosmos DB: API para MongoDB usando as instruções descritas [aqui](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="56190-110">Retrieve your Azure Cosmos DB: API for MongoDB connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Captura de tela da folha de cadeia de conexão](./media/mongodb-mongochef/ConnectionStringBlade.png)
2. <span data-ttu-id="56190-112">Clique em **Conectar** para abrir o Gerenciador de Conexões e clique em **Nova Conexão**</span><span class="sxs-lookup"><span data-stu-id="56190-112">Click **Connect** to open the Connection Manager, then click **New Connection**</span></span>

    ![Captura de tela do gerenciador de conexões do MongoChef](./media/mongodb-mongochef/ConnectionManager.png)
3. <span data-ttu-id="56190-114">Na janela **Nova Conexão**, na guia **Servidor**, insira o HOST (FQDN) da conta do Azure Cosmos DB: API para MongoDB e a PORTA.</span><span class="sxs-lookup"><span data-stu-id="56190-114">In the **New Connection** window, on the **Server** tab, enter the HOST (FQDN) of the Azure Cosmos DB: API for MongoDB account and the PORT.</span></span>

    ![Captura de tela da guia servidor do gerenciador de conexões do MongoChef](./media/mongodb-mongochef/ConnectionManagerServerTab.png)
4. <span data-ttu-id="56190-116">Na janela **Nova Conexão**, na guia **Autenticação**, escolha o Padrão do Modo de Autenticação **(MONGODB-CR ou SCARM-SHA-1)** e insira USERNAME e PASSWORD.</span><span class="sxs-lookup"><span data-stu-id="56190-116">In the **New Connection** window, on the **Authentication** tab, choose Authentication Mode **Standard (MONGODB-CR or SCARM-SHA-1)** and enter the USERNAME and PASSWORD.</span></span>  <span data-ttu-id="56190-117">Aceite o banco de dados de autenticação padrão (admin) ou forneça seu próprio valor.</span><span class="sxs-lookup"><span data-stu-id="56190-117">Accept the default authentication db (admin) or provide your own value.</span></span>

    ![Captura de tela da guia autenticação do gerenciador de conexões do MongoChef](./media/mongodb-mongochef/ConnectionManagerAuthenticationTab.png)
5. <span data-ttu-id="56190-119">Na janela **Nova Conexão**, na guia **SSL**, marque a caixa de seleção **Usar protocolo SSL para se conectar** e o botão de opção **Aceitar certificados SSL de servidor autoassinados**.</span><span class="sxs-lookup"><span data-stu-id="56190-119">In the **New Connection** window, on the **SSL** tab, check the **Use SSL protocol to connect** check box and the **Accept server self-signed SSL certificates** radio button.</span></span>

    ![Captura de tela da guia SSL do gerenciador de conexões do MongoChef](./media/mongodb-mongochef/ConnectionManagerSSLTab.png)
6. <span data-ttu-id="56190-121">Clique no botão **Testar Conectividade** para validar as informações de conexão, clique em **OK** para retornar à janela Nova Conexão e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="56190-121">Click the **Test Connection** button to validate the connection information, click **OK** to return to the New Connection window, and then click **Save**.</span></span>

    ![Captura de tela da janela testar conectividade do MongoChef](./media/mongodb-mongochef/TestConnectionResults.png)

## <a name="use-mongochef-to-create-a-database-collection-and-documents"></a><span data-ttu-id="56190-123">Usar o MongoChef para criar um banco de dados, uma coleção e documentos</span><span class="sxs-lookup"><span data-stu-id="56190-123">Use MongoChef to create a database, collection, and documents</span></span>
<span data-ttu-id="56190-124">Para criar um banco de dados, uma coleção e documentos usando o MongoChef, execute as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="56190-124">To create a database, collection, and documents using MongoChef, perform the following steps.</span></span>

1. <span data-ttu-id="56190-125">No **Gerenciador de Conexões**, realce a conexão e clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="56190-125">In **Connection Manager**, highlight the connection and click **Connect**.</span></span>

    ![Captura de tela do gerenciador de conexões do MongoChef](./media/mongodb-mongochef/ConnectToAccount.png)
2. <span data-ttu-id="56190-127">Clique com o botão direito do mouse e escolha **Adicionar Banco de Dados**.</span><span class="sxs-lookup"><span data-stu-id="56190-127">Right click the host and choose **Add Database**.</span></span>  <span data-ttu-id="56190-128">Forneça um nome de banco de dados e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="56190-128">Provide a database name and click **OK**.</span></span>

    ![Captura de tela da opção Adicionar Banco de Dados do MongoChef](./media/mongodb-mongochef/AddDatabase1.png)
3. <span data-ttu-id="56190-130">Clique com o botão direito do mouse no banco de dados e escolha **Adicionar Coleção**.</span><span class="sxs-lookup"><span data-stu-id="56190-130">Right click the database and choose **Add Collection**.</span></span>  <span data-ttu-id="56190-131">Forneça um nome de coleção e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="56190-131">Provide a collection name and click **Create**.</span></span>

    ![Captura de tela da opção Adicionar Coleção do MongoChef](./media/mongodb-mongochef/AddCollection.png)
4. <span data-ttu-id="56190-133">Clique no item de menu **Coleção** e clique em **Adicionar Documento**.</span><span class="sxs-lookup"><span data-stu-id="56190-133">Click the **Collection** menu item, then click **Add Document**.</span></span>

    ![Captura de tela do item menu Adicionar Documento do MongoChef](./media/mongodb-mongochef/AddDocument1.png)
5. <span data-ttu-id="56190-135">Na caixa de diálogo Adicionar Documento, cole o conteúdo a seguir e clique em **Adicionar Documento**.</span><span class="sxs-lookup"><span data-stu-id="56190-135">In the Add Document dialog, paste the following and then click **Add Document**.</span></span>

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
6. <span data-ttu-id="56190-136">Adicione outro documento, dessa vez com o conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="56190-136">Add another document, this time with the following content.</span></span>

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
7. <span data-ttu-id="56190-137">Execute uma consulta de exemplo.</span><span class="sxs-lookup"><span data-stu-id="56190-137">Execute a sample query.</span></span> <span data-ttu-id="56190-138">Por exemplo, procure famílias com o sobrenome 'Andersen' e retorne os campos de estado e pais.</span><span class="sxs-lookup"><span data-stu-id="56190-138">For example, search for families with the last name 'Andersen' and return the parents and state fields.</span></span>

    ![Captura de tela dos resultados de consulta do MongoChef](./media/mongodb-mongochef/QueryDocument1.png)

## <a name="next-steps"></a><span data-ttu-id="56190-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="56190-140">Next steps</span></span>
* <span data-ttu-id="56190-141">Conheça as [amostras](mongodb-samples.md) do Azure Cosmos DB: API para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="56190-141">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
