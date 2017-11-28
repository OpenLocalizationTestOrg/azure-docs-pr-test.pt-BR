---
title: aaaUse Robomongo para o banco de dados do Azure Cosmos | Microsoft Docs
description: 'Saiba como toouse Robomongo com um banco de dados do Azure Cosmos: API de conta do MongoDB'
keywords: robomongo
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
ms.openlocfilehash: 3018243e904015426dc69a69b26fb53421e1fe4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="81e9b-104">Usar o Robomongo com uma conta do Azure Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="81e9b-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="81e9b-105">tooconnect tooan o banco de dados do Azure Cosmos: API de conta do MongoDB usando Robomongo, você deve:</span><span class="sxs-lookup"><span data-stu-id="81e9b-105">tooconnect tooan Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="81e9b-106">Baixar e instalar o [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="81e9b-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="81e9b-107">Ter as informações de [cadeia de conexão](connect-mongodb-account.md) de sua conta do Azure Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="81e9b-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="81e9b-108">Conectar usando o Robomongo</span><span class="sxs-lookup"><span data-stu-id="81e9b-108">Connect using Robomongo</span></span>
<span data-ttu-id="81e9b-109">tooadd seu banco de dados do Azure Cosmos: API para o MongoDB conta toohello Robomongo MongoDB conexões, executar Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="81e9b-109">tooadd your Azure Cosmos DB: API for MongoDB account toohello Robomongo MongoDB Connections, perform hello following steps.</span></span>

1. <span data-ttu-id="81e9b-110">Recuperar o banco de dados do Azure Cosmos: API de informações de conexão da conta de MongoDB usando instruções Olá [aqui](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="81e9b-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using hello instructions [here](connect-mongodb-account.md).</span></span>

    ![Captura de tela da folha de cadeia de caracteres de conexão Olá](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="81e9b-112">Execute *Robomongo.exe*</span><span class="sxs-lookup"><span data-stu-id="81e9b-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="81e9b-113">Botão de conexão Olá em **arquivo** toomanage suas conexões.</span><span class="sxs-lookup"><span data-stu-id="81e9b-113">Click hello connection button under **File** toomanage your connections.</span></span> <span data-ttu-id="81e9b-114">Em seguida, clique em **criar** em Olá **MongoDB conexões** janela, que será aberta, Olá **configurações de Conexão** janela.</span><span class="sxs-lookup"><span data-stu-id="81e9b-114">Then, click **Create** in hello **MongoDB Connections** window, which will open up hello **Connection Settings** window.</span></span>

4. <span data-ttu-id="81e9b-115">Em Olá **configurações de Conexão** janela, escolha um nome.</span><span class="sxs-lookup"><span data-stu-id="81e9b-115">In hello **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="81e9b-116">Em seguida, localize Olá **Host** e **porta** de suas informações de conexão na etapa 1 e inseri-las em **endereço** e **porta**, respectivamente .</span><span class="sxs-lookup"><span data-stu-id="81e9b-116">Then, find hello **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Captura de tela de saudação Robomongo gerenciar conexões](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="81e9b-118">Em Olá **autenticação** , clique em **executar autenticação**.</span><span class="sxs-lookup"><span data-stu-id="81e9b-118">On hello **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="81e9b-119">Em seguida, insira seu Banco de dados (o padrão é *Admin*), **Nome de Usuário** e **Senha**.</span><span class="sxs-lookup"><span data-stu-id="81e9b-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="81e9b-120">Tanto o **Nome de Usuário** quanto a **Senha** podem ser encontrados em suas informações de conexão na Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="81e9b-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Captura de tela de saudação Robomongo guia de autenticação](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="81e9b-122">Em Olá **SSL** guia, verifique **protocolo usar SSL**, em seguida, altere a saudação **método de autenticação** muito**certificado autoassinado**.</span><span class="sxs-lookup"><span data-stu-id="81e9b-122">On hello **SSL** tab, check **Use SSL protocol**, then change hello **Authentication Method** too**Self-signed Certificate**.</span></span>

    ![Captura de tela de saudação Robomongo SSL guia](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="81e9b-124">Por fim, clique em **teste** tooverify que você está tooconnect pode, em seguida, **salvar**.</span><span class="sxs-lookup"><span data-stu-id="81e9b-124">Finally, click **Test** tooverify that you are able tooconnect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81e9b-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="81e9b-125">Next steps</span></span>
* <span data-ttu-id="81e9b-126">Conheça as [amostras](mongodb-samples.md) do Azure Cosmos DB: API para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="81e9b-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
