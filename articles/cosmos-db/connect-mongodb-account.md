---
title: "aaaMongoDB cadeia de caracteres de conexão para uma conta de banco de dados do Azure Cosmos | Microsoft Docs"
description: "Saiba como tooconnect tooan de aplicativo o MongoDB Azure Cosmos DB conta usando uma cadeia de caracteres de conexão do MongoDB."
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
ms.openlocfilehash: c0b81cb49a10e09e3f02411b91731c7f980ec47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-mongodb-application-tooazure-cosmos-db"></a><span data-ttu-id="f9961-104">Conecte-se um aplicativo de MongoDB tooAzure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="f9961-104">Connect a MongoDB application tooAzure Cosmos DB</span></span>
<span data-ttu-id="f9961-105">Saiba como tooconnect tooan de aplicativo o MongoDB Azure Cosmos DB conta usando uma cadeia de caracteres de conexão do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f9961-105">Learn how tooconnect your MongoDB app tooan Azure Cosmos DB account by using a MongoDB connection string.</span></span> <span data-ttu-id="f9961-106">Você pode usar um banco de dados do banco de dados do Azure Cosmos como dados saudação armazenar para seu aplicativo do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f9961-106">You can then use an Azure Cosmos DB database as hello data store for your MongoDB app.</span></span> 

<span data-ttu-id="f9961-107">Este tutorial fornece informações de cadeia de caracteres de conexão tooretrieve de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="f9961-107">This tutorial provides two ways tooretrieve connection string information:</span></span>

- <span data-ttu-id="f9961-108">[Olá rápida iniciar método](#QuickstartConnection), para uso com drivers .NET, Node.js, MongoDB Shell, Java e Python</span><span class="sxs-lookup"><span data-stu-id="f9961-108">[hello quick start method](#QuickstartConnection), for use with .NET, Node.js, MongoDB Shell, Java, and Python drivers</span></span>
- <span data-ttu-id="f9961-109">[Olá método de cadeia de caracteres de conexão personalizada](#GetCustomConnection), para uso com outros drivers</span><span class="sxs-lookup"><span data-stu-id="f9961-109">[hello custom connection string method](#GetCustomConnection), for use with other drivers</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9961-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f9961-110">Prerequisites</span></span>

- <span data-ttu-id="f9961-111">Uma conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="f9961-111">An Azure account.</span></span> <span data-ttu-id="f9961-112">Se você ainda não tiver uma, crie agora mesmo uma [conta gratuita do Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="f9961-112">If you don't have an Azure account, create a [free Azure account](https://azure.microsoft.com/free/) now.</span></span> 
- <span data-ttu-id="f9961-113">Uma conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f9961-113">An Azure Cosmos DB account.</span></span> <span data-ttu-id="f9961-114">Para obter instruções, consulte [compilar um aplicativo de web do MongoDB API com .NET e Olá portal do Azure](create-mongodb-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="f9961-114">For instructions, see [Build a MongoDB API web app with .NET and hello Azure portal](create-mongodb-dotnet.md).</span></span>

## <span data-ttu-id="f9961-115"><a id="QuickstartConnection"></a>Obter cadeia de caracteres de conexão do hello MongoDB usando o início rápido Olá</span><span class="sxs-lookup"><span data-stu-id="f9961-115"><a id="QuickstartConnection"></a>Get hello MongoDB connection string by using hello quick start</span></span>
1. <span data-ttu-id="f9961-116">Em um navegador da Internet, entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f9961-116">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f9961-117">Em Olá **o banco de dados do Azure Cosmos** folha, selecione Olá API para a conta do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f9961-117">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="f9961-118">No painel esquerdo de saudação da folha de conta hello, clique em **início rápido**.</span><span class="sxs-lookup"><span data-stu-id="f9961-118">In hello left pane of hello account blade, click **Quick start**.</span></span> 
4. <span data-ttu-id="f9961-119">Escolha sua plataforma (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span><span class="sxs-lookup"><span data-stu-id="f9961-119">Choose your platform (**.NET**, **Node.js**, **MongoDB Shell**, **Java**, **Python**).</span></span> <span data-ttu-id="f9961-120">Caso não veja seu driver ou ferramenta na lista, não se preocupe, pois documentamos continuamente mais trechos de código de conexão.</span><span class="sxs-lookup"><span data-stu-id="f9961-120">If you don't see your driver or tool listed, don't worry--we continuously document more connection code snippets.</span></span> <span data-ttu-id="f9961-121">Comente abaixo sobre o que você gostaria que toosee.</span><span class="sxs-lookup"><span data-stu-id="f9961-121">Please comment below on what you'd like toosee.</span></span> <span data-ttu-id="f9961-122">toolearn como toocraft sua conexão, leitura [obter informações de cadeia de caracteres de conexão da conta Olá](#GetCustomConnection).</span><span class="sxs-lookup"><span data-stu-id="f9961-122">toolearn how toocraft your own connection, read [Get hello account's connection string information](#GetCustomConnection).</span></span>
5. <span data-ttu-id="f9961-123">Copie e cole o trecho de código Olá em seu aplicativo do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f9961-123">Copy and paste hello code snippet into your MongoDB app.</span></span>

    ![Folha início rápido](./media/connect-mongodb-account/QuickStartBlade.png)

## <span data-ttu-id="f9961-125"><a id="GetCustomConnection"></a>Obter toocustomize de cadeia de caracteres de conexão do hello MongoDB</span><span class="sxs-lookup"><span data-stu-id="f9961-125"><a id="GetCustomConnection"></a> Get hello MongoDB connection string toocustomize</span></span>
1. <span data-ttu-id="f9961-126">Em um navegador da Internet, entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f9961-126">In an Internet browser, sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f9961-127">Em Olá **o banco de dados do Azure Cosmos** folha, selecione Olá API para a conta do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f9961-127">In hello **Azure Cosmos DB** blade, select hello API for MongoDB account.</span></span> 
3. <span data-ttu-id="f9961-128">No painel esquerdo de saudação da folha de conta hello, clique em **cadeia de caracteres de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="f9961-128">In hello left pane of hello account blade, click **Connection String**.</span></span> 
4. <span data-ttu-id="f9961-129">Olá **cadeia de caracteres de Conexão** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="f9961-129">hello **Connection String** blade opens.</span></span> <span data-ttu-id="f9961-130">Ele tem todas as contas de toohello Olá informações tooconnect necessário, usando um driver para o MongoDB, incluindo uma cadeia de caracteres de conexão pré-construído.</span><span class="sxs-lookup"><span data-stu-id="f9961-130">It has all hello information necessary tooconnect toohello account by using a driver for MongoDB, including a preconstructed connection string.</span></span>

    ![Folha Cadeia de conexão](./media/connect-mongodb-account/ConnectionStringBlade.png)

## <a name="connection-string-requirements"></a><span data-ttu-id="f9961-132">Requisitos da cadeia de conexão</span><span class="sxs-lookup"><span data-stu-id="f9961-132">Connection string requirements</span></span>
> [!Important]
> <span data-ttu-id="f9961-133">O Azure Cosmos DB tem padrões e requisitos de segurança rígidos.</span><span class="sxs-lookup"><span data-stu-id="f9961-133">Azure Cosmos DB has strict security requirements and standards.</span></span> <span data-ttu-id="f9961-134">As contas do Azure Cosmos DB exigem autenticação e comunicação segura por *SSL*.</span><span class="sxs-lookup"><span data-stu-id="f9961-134">Azure Cosmos DB accounts require authentication and secure communication via *SSL*.</span></span> 
>
>

<span data-ttu-id="f9961-135">Banco de dados do Azure Cosmos dá suporte a saudação MongoDB conexão string URI formato padrão, com alguns requisitos específicos: contas do Azure Cosmos DB exigem autenticação e comunicação segura via SSL.</span><span class="sxs-lookup"><span data-stu-id="f9961-135">Azure Cosmos DB supports hello standard MongoDB connection string URI format, with a couple of specific requirements: Azure Cosmos DB accounts require authentication and secure communication via SSL.</span></span> <span data-ttu-id="f9961-136">Portanto, o formato de cadeia de caracteres de conexão de saudação é:</span><span class="sxs-lookup"><span data-stu-id="f9961-136">So, hello connection string format is:</span></span>

    mongodb://username:password@host:port/[database]?ssl=true

<span data-ttu-id="f9961-137">os valores da cadeia de caracteres Hello estão disponíveis no hello **cadeia de caracteres de Conexão** folha mostrada anteriormente:</span><span class="sxs-lookup"><span data-stu-id="f9961-137">hello values of this string are available in hello **Connection String** blade shown earlier:</span></span>

* <span data-ttu-id="f9961-138">Nome de usuário (obrigatória): nome da conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f9961-138">Username (required): Azure Cosmos DB account name.</span></span>
* <span data-ttu-id="f9961-139">Senha (obrigatória): senha da conta do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="f9961-139">Password (required): Azure Cosmos DB account password.</span></span>
* <span data-ttu-id="f9961-140">Host (obrigatório): FQDN do hello Azure Cosmos DB conta.</span><span class="sxs-lookup"><span data-stu-id="f9961-140">Host (required): FQDN of hello Azure Cosmos DB account.</span></span>
* <span data-ttu-id="f9961-141">Porta (obrigatória): 10255.</span><span class="sxs-lookup"><span data-stu-id="f9961-141">Port (required): 10255.</span></span>
* <span data-ttu-id="f9961-142">Banco de dados (opcional): banco de dados Olá Olá conexão usa.</span><span class="sxs-lookup"><span data-stu-id="f9961-142">Database (optional): hello database that hello connection uses.</span></span> <span data-ttu-id="f9961-143">Se nenhum banco de dados for fornecido, o banco de dados do saudação padrão é "teste".</span><span class="sxs-lookup"><span data-stu-id="f9961-143">If no database is provided, hello default database is "test."</span></span>
* <span data-ttu-id="f9961-144">ssl=true (obrigatório)</span><span class="sxs-lookup"><span data-stu-id="f9961-144">ssl=true (required)</span></span>

<span data-ttu-id="f9961-145">Por exemplo, considere conta Olá mostrada no hello **cadeia de caracteres de Conexão** folha.</span><span class="sxs-lookup"><span data-stu-id="f9961-145">For example, consider hello account shown in hello **Connection String** blade.</span></span> <span data-ttu-id="f9961-146">Uma cadeia de conexão válida é:</span><span class="sxs-lookup"><span data-stu-id="f9961-146">A valid connection string is:</span></span>

    mongodb://contoso123:0Fc3IolnL12312asdfawejunASDF@asdfYXX2t8a97kghVcUzcDv98hawelufhawefafnoQRGwNj2nMPL1Y9qsIr9Srdw==@anhohmongo.documents.azure.com:10255/mydatabase?ssl=true

## <a name="next-steps"></a><span data-ttu-id="f9961-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f9961-147">Next steps</span></span>
* <span data-ttu-id="f9961-148">Saiba como muito[usar MongoChef](mongodb-mongochef.md) com uma API de banco de dados do Azure Cosmos para a conta do MongoDB.</span><span class="sxs-lookup"><span data-stu-id="f9961-148">Learn how too[use MongoChef](mongodb-mongochef.md) with an Azure Cosmos DB API for MongoDB account.</span></span>
* <span data-ttu-id="f9961-149">Explorar hello Azure Cosmos DB API para o MongoDB exibindo [exemplos](mongodb-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f9961-149">Explore hello Azure Cosmos DB API for MongoDB by viewing [samples](mongodb-samples.md).</span></span>
