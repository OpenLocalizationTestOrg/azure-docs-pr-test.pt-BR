---
title: Usar o Robomongo no Azure Cosmos DB | Microsoft Docs
description: 'Saiba como usar o Robomongo com uma conta do Azure Cosmos DB: API para MongoDB'
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
ms.openlocfilehash: 8983594776a1bbe413a6d7cf2cd518f0e327648a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-robomongo-with-an-azure-cosmos-db-api-for-mongodb-account"></a><span data-ttu-id="9cc42-104">Usar o Robomongo com uma conta do Azure Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="9cc42-104">Use Robomongo with an Azure Cosmos DB: API for MongoDB account</span></span>
<span data-ttu-id="9cc42-105">Para se conectar a uma conta do Azure Cosmos DB: API para MongoDB usando o Robomongo, é necessário:</span><span class="sxs-lookup"><span data-stu-id="9cc42-105">To connect to an Azure Cosmos DB: API for MongoDB account using Robomongo, you must:</span></span>

* <span data-ttu-id="9cc42-106">Baixar e instalar o [Robomongo](https://robomongo.org/)</span><span class="sxs-lookup"><span data-stu-id="9cc42-106">Download and install [Robomongo](https://robomongo.org/)</span></span>
* <span data-ttu-id="9cc42-107">Ter as informações de [cadeia de conexão](connect-mongodb-account.md) de sua conta do Azure Cosmos DB: API para MongoDB</span><span class="sxs-lookup"><span data-stu-id="9cc42-107">Have your Azure Cosmos DB: API for MongoDB account [connection string](connect-mongodb-account.md) information</span></span>

## <a name="connect-using-robomongo"></a><span data-ttu-id="9cc42-108">Conectar usando o Robomongo</span><span class="sxs-lookup"><span data-stu-id="9cc42-108">Connect using Robomongo</span></span>
<span data-ttu-id="9cc42-109">Para adicionar sua conta do Azure Cosmos DB: API para MongoDB às Conexões entre o Robomongo e o MongoDB, realize as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="9cc42-109">To add your Azure Cosmos DB: API for MongoDB account to the Robomongo MongoDB Connections, perform the following steps.</span></span>

1. <span data-ttu-id="9cc42-110">Recupere as informações de conexão de sua conta do Azure Cosmos DB: API para MongoDB usando as instruções descritas [aqui](connect-mongodb-account.md).</span><span class="sxs-lookup"><span data-stu-id="9cc42-110">Retrieve your Azure Cosmos DB: API for MongoDB account connection information using the instructions [here](connect-mongodb-account.md).</span></span>

    ![Captura de tela da folha de cadeia de conexão](./media/mongodb-robomongo/connectionstringblade.png)
2. <span data-ttu-id="9cc42-112">Execute *Robomongo.exe*</span><span class="sxs-lookup"><span data-stu-id="9cc42-112">Run *Robomongo.exe*</span></span>

3. <span data-ttu-id="9cc42-113">Clique no botão de conexão em **Arquivo** para gerenciar suas conexões.</span><span class="sxs-lookup"><span data-stu-id="9cc42-113">Click the connection button under **File** to manage your connections.</span></span> <span data-ttu-id="9cc42-114">Em seguida, clique em **Criar** na janela **Conexões do MongoDB**, o que abrirá a janela **Configurações de Conexão**.</span><span class="sxs-lookup"><span data-stu-id="9cc42-114">Then, click **Create** in the **MongoDB Connections** window, which will open up the **Connection Settings** window.</span></span>

4. <span data-ttu-id="9cc42-115">No janela **Configurações de Conexão**, escolha um nome.</span><span class="sxs-lookup"><span data-stu-id="9cc42-115">In the **Connection Settings** window, choose a name.</span></span> <span data-ttu-id="9cc42-116">Em seguida, localize o **Host** e **Porta** de suas informações de conexão na Etapa 1 e insira-os em **Endereço** e **Porta**, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="9cc42-116">Then, find the **Host** and **Port** from your connection information in Step 1 and enter them into **Address** and **Port**, respectively.</span></span>

    ![Captura de tela do Robomongo Manage Connections](./media/mongodb-robomongo/manageconnections.png)
5. <span data-ttu-id="9cc42-118">Na guia **Autenticação**, clique em **Executar autenticação**.</span><span class="sxs-lookup"><span data-stu-id="9cc42-118">On the **Authentication** tab, click **Perform authentication**.</span></span> <span data-ttu-id="9cc42-119">Em seguida, insira seu Banco de dados (o padrão é *Admin*), **Nome de Usuário** e **Senha**.</span><span class="sxs-lookup"><span data-stu-id="9cc42-119">Then, enter your Database (default is *Admin*), **User Name** and **Password**.</span></span>
<span data-ttu-id="9cc42-120">Tanto o **Nome de Usuário** quanto a **Senha** podem ser encontrados em suas informações de conexão na Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="9cc42-120">Both **User Name** and **Password** can be found in your connection information in Step 1.</span></span>

    ![Captura de tela da guia de Autenticação do Robomongo](./media/mongodb-robomongo/authentication.png)
6. <span data-ttu-id="9cc42-122">Na guia **SSL**, marque **Usar protocolo SSL** e altere o **Método de Autenticação** para **Certificado Autoassinado**.</span><span class="sxs-lookup"><span data-stu-id="9cc42-122">On the **SSL** tab, check **Use SSL protocol**, then change the **Authentication Method** to **Self-signed Certificate**.</span></span>

    ![Captura de tela da guia Robomongo SSL](./media/mongodb-robomongo/SSL.png)
7. <span data-ttu-id="9cc42-124">Por fim, clique em **Teste** para verificar se você é capaz de se conectar e, em seguida, **Salve**.</span><span class="sxs-lookup"><span data-stu-id="9cc42-124">Finally, click **Test** to verify that you are able to connect, then **Save**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9cc42-125">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9cc42-125">Next steps</span></span>
* <span data-ttu-id="9cc42-126">Conheça as [amostras](mongodb-samples.md) do Azure Cosmos DB: API para MongoDB.</span><span class="sxs-lookup"><span data-stu-id="9cc42-126">Explore Azure Cosmos DB: API for MongoDB [samples](mongodb-samples.md).</span></span>
