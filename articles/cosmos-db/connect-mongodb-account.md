---
title: "Cadeia de conexão do MongoDB para a conta do Azure Cosmos DB | Microsoft Docs"
description: "Saiba como conectar seu aplicativo do MongoDB a uma conta do Azure Cosmos DB usando uma cadeia de conexão do MongoDB."
keywords: "cadeia de conexão do mongodb"
services: cosmos-db
author: AndrewHoh
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: e36f7375-9329-403b-afd1-4ab49894f75e
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/12/2017
ms.author: anhoh
ms.openlocfilehash: 5a47001705531d971d3181df9c0aa8f957168845
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="connect-a-mongodb-application-to-azure-cosmos-db"></a><span data-ttu-id="1c98f-104">Conectar um aplicativo do MongoDB ao Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="1c98f-104">Connect a MongoDB application to Azure Cosmos DB</span></span>
<span data-ttu-id="1c98f-105">Saiba como conectar seu aplicativo do MongoDB a uma conta do Azure Cosmos DB usando uma cadeia de conexão do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1c98f-105">Learn how to connect your MongoDB app to an Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="1c98f-106">Você pode usar um banco de dados do Azure Cosmos DB como o armazenamento de dados para seu aplicativo MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1c98f-106">You can then use an Azure Cosmos DB database as the data store for your MongoDB app.</span></span> 

<span data-ttu-id="1c98f-107">Este tutorial fornece duas maneiras de recuperar informações da cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="1c98f-107">This tutorial provides two ways to retrieve connection string information:</span></span>

- <span data-ttu-id="1c98f-108">[O método de início rápido](#QuickstartConnection), para uso com drivers do .NET, Node.js, Shell do MongoDB, Java e Python</span><span class="sxs-lookup"><span data-stu-id="1c98f-108">[The quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="1c98f-109">[O método de cadeia de conexão personalizada](#GetCustomConnection), para uso com outros drivers</span><span class="sxs-lookup"><span data-stu-id="1c98f-109">[The custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c98f-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1c98f-110">Prerequisites</span></span>

- <span data-ttu-id="1c98f-111">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="1c98f-111">An Azure account.</span></span> <span data-ttu-id="1c98f-112">Se você ainda não tiver uma, crie agora mesmo uma [conta gratuita do Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="1c98f-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="1c98f-113">Uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1c98f-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="1c98f-114">Para instruções, consulte [Compilar um aplicativo Web da API MongoDB com o .NET e o Portal do Azure](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="1c98f-114">For instructions, see [Build a MongoDB API web app with .NET and the Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="1c98f-115"><a id="QuickstartConnection"></a>Obter a cadeia de conexão do MongoDB usando o início rápido</span><span class="sxs-lookup"><span data-stu-id="1c98f-115"><a id="QuickstartConnection"></a>Get the MongoDB connection string by using the quick start</span></span>
1. <span data-ttu-id="1c98f-116">Em um navegador da Internet, entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c98f-116">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1c98f-117">Na folha **Azure Cosmos DB**, selecione a API da conta MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1c98f-117">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="1c98f-118">No painel esquerdo da folha da conta, clique em **Início rápido**.</span><span class="sxs-lookup"><span data-stu-id="1c98f-118">In the left pane of the account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="1c98f-119">Escolha sua plataforma (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="1c98f-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="1c98f-120">Caso não veja seu driver ou ferramenta na lista, não se preocupe, pois documentamos continuamente mais trechos de código de conexão.</span><span class="sxs-lookup"><span data-stu-id="1c98f-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="1c98f-121">Comente abaixo sobre o que você gostaria de ver.</span><span class="sxs-lookup"><span data-stu-id="1c98f-121">Please comment below on what you'd like to see.</span></span> <span data-ttu-id="1c98f-122">Para saber como gostaria de ver sua conexão e leia [Obter informações da cadeia de conexão da conta](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="1c98f-122">To learn how to craft your own connection, read [Get the account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="1c98f-123">Copie e cole o trecho de código no seu aplicativo MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1c98f-123">Copy and paste the code snippet into your MongoDB app.</span></span>

    ![Folha início rápido](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="1c98f-125"><a id="GetCustomConnection"></a> Obter a cadeia de conexão do MongoDB para personalização</span><span class="sxs-lookup"><span data-stu-id="1c98f-125"><a id="GetCustomConnection"></a> Get the MongoDB connection string to customize</span></span>
1. <span data-ttu-id="1c98f-126">Em um navegador da Internet, entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1c98f-126">In an Internet browser, sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1c98f-127">Na folha **Azure Cosmos DB**, selecione a API da conta MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1c98f-127">In the **Azure Cosmos DB** blade, select the API for MongoDB account.</span></span> 
3. <span data-ttu-id="1c98f-128">No painel esquerdo do folha de conta, clique em **Cadeia de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="1c98f-128">In the left pane of the account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="1c98f-129">A folha de **Cadeia de Conexão** é aberta.</span><span class="sxs-lookup"><span data-stu-id="1c98f-129">The **Connection String** blade opens.</span></span> <span data-ttu-id="1c98f-130">Ela tem todas as informações necessárias para se conectar à conta usando um driver para MongoDB, incluindo uma cadeia de conexão pré-construída.</span><span class="sxs-lookup"><span data-stu-id="1c98f-130">It has all the information necessary to connect to the account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Folha Cadeia de conexão](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="1c98f-132">Requisitos da cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="1c98f-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="1c98f-133">O Azure Cosmos DB tem padrões e requisitos de segurança rígidos.</span><span class="sxs-lookup"><span data-stu-id="1c98f-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="1c98f-134">As contas do Azure Cosmos DB exigem autenticação e comunicação segura por *SSL*.</span><span class="sxs-lookup"><span data-stu-id="1c98f-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="1c98f-135">O Azure Cosmos DB dá suporte ao formato de URI da cadeia de conexão padrão do MongoDB padrão, com alguns requisitos específicos: as contas do Azure Cosmos DB exigem autenticação e comunicação segura por SSL.</span><span class="sxs-lookup"><span data-stu-id="1c98f-135">Azure Cosmos DB supports the standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="1c98f-136">Sendo assim, o formato da cadeia de conexão é:</span><span class="sxs-lookup"><span data-stu-id="1c98f-136">So, the connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="1c98f-137">Os valores dessa cadeia de caracteres estão disponíveis na folha **Cadeia de conexão** mostrada acima:</span><span class="sxs-lookup"><span data-stu-id="1c98f-137">The values of this string are available in the **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="1c98f-138">Nome de usuário (obrigatória): nome da conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1c98f-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="1c98f-139">Senha (obrigatória): senha da conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1c98f-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="1c98f-140">Host (obrigatório): o FQDN da conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1c98f-140">Host (required): FQDN of the Azure Cosmos DB account.</span></span>
* <span data-ttu-id="1c98f-141">Porta (obrigatória): 10255.</span><span class="sxs-lookup"><span data-stu-id="1c98f-141">Port (required): 10255.</span></span>
* <span data-ttu-id="1c98f-142">Banco de dados (opcional): o banco de dados que a conexão usa.</span><span class="sxs-lookup"><span data-stu-id="1c98f-142">Database (optional): The database that the connection uses.</span></span> <span data-ttu-id="1c98f-143">Se nenhum banco de dados for fornecido, o banco de dados padrão é "teste".</span><span class="sxs-lookup"><span data-stu-id="1c98f-143">If no database is provided, the default database is "test."</span></span>
* <span data-ttu-id="1c98f-144">ssl=true (obrigatório)</span><span class="sxs-lookup"><span data-stu-id="1c98f-144">ssl=true (required)</span></span>

<span data-ttu-id="1c98f-145">Por exemplo, considere a conta mostrada na folha **Cadeia de conexão**.</span><span class="sxs-lookup"><span data-stu-id="1c98f-145">For example, consider the account shown in the **Connection String** blade.</span></span> <span data-ttu-id="1c98f-146">Uma cadeia de conexão válida é:</span><span class="sxs-lookup"><span data-stu-id="1c98f-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="1c98f-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1c98f-147">Next steps</span></span>
* <span data-ttu-id="1c98f-148">Saiba como usar o [MongoChef](mongodb-mongochef.md) com uma conta do Azure Cosmos DB: API para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="1c98f-148">Learn how to [use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="1c98f-149">Conheça a API do Azure Cosmos DB para o MongoDB ao ver [amostras](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1c98f-149">Explore the Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
