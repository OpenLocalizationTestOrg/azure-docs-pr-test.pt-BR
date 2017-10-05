---
title: "Usar o Conector do SharePoint Server em seus Aplicativos Lógicos | Microsoft Docs"
description: "Introdução ao uso do Conector do SharePoint Server em seus Aplicativos lógicos"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 0f3274816e279a1aa57febaa2f8294914900799a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sharepoint-connector"></a><span data-ttu-id="9dd55-103">Introdução ao conector do SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dd55-103">Get started with the SharePoint connector</span></span>
<span data-ttu-id="9dd55-104">O Conector do SharePoint fornece uma maneira de trabalhar com listas do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9dd55-104">The SharePoint Connector provides an way to work with Lists on SharePoint.</span></span>

<span data-ttu-id="9dd55-105">Comece pela criação de um aplicativo lógico; veja [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="9dd55-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-sharepoint"></a><span data-ttu-id="9dd55-106">Criar uma conexão com o SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dd55-106">Create a connection to SharePoint</span></span>
<span data-ttu-id="9dd55-107">Para usar o Conector do SharePoint, crie primeiro uma **conexão** e, então, forneça os detalhes dessas propriedades:</span><span class="sxs-lookup"><span data-stu-id="9dd55-107">To use the SharePoint Connector , you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="9dd55-108">Propriedade</span><span class="sxs-lookup"><span data-stu-id="9dd55-108">Property</span></span> | <span data-ttu-id="9dd55-109">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="9dd55-109">Required</span></span> | <span data-ttu-id="9dd55-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="9dd55-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9dd55-111">A criptografia do token</span><span class="sxs-lookup"><span data-stu-id="9dd55-111">Token</span></span> |<span data-ttu-id="9dd55-112">Sim</span><span class="sxs-lookup"><span data-stu-id="9dd55-112">Yes</span></span> |<span data-ttu-id="9dd55-113">Fornecer credenciais do SharePoint</span><span class="sxs-lookup"><span data-stu-id="9dd55-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="9dd55-114">Para se conectar ao **SharePoint**, insira sua identidade (nome de usuário e senha, credenciais do cartão inteligente etc.) no SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9dd55-114">To connect to **SharePoint**, enter your identity (username and password, smart card credentials, etc.) to SharePoint.</span></span> <span data-ttu-id="9dd55-115">Depois de se autenticar, você poderá continuar e usar o Conector do SharePoint em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="9dd55-115">Once you've been authenticated, you can proceed to use the SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="9dd55-116">No designer do aplicativo lógico, siga estas etapas para entrar no SharePoint e criar a conexão **conexão** para uso em seu aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="9dd55-116">While on the designer of your logic app, follow these steps to sign into SharePoint to create the connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="9dd55-117">Insira SharePoint na caixa de pesquisa e aguarde até que a pesquisa retorne todas as entradas com SharePoint no nome: </span><span class="sxs-lookup"><span data-stu-id="9dd55-117">Enter SharePoint in the search box and wait for the search to return all entries with SharePoint in the name:</span></span>   
   ![Configurar o SharePoint][1]  
2. <span data-ttu-id="9dd55-119">Selecione **SharePoint – Quando um arquivo é criado**</span><span class="sxs-lookup"><span data-stu-id="9dd55-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="9dd55-120">Selecione **Entrar no SharePoint**:</span><span class="sxs-lookup"><span data-stu-id="9dd55-120">Select **Sign in to SharePoint**:</span></span>   
   <span data-ttu-id="9dd55-121">![Configurar o SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="9dd55-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="9dd55-122">Forneça suas credenciais do SharePoint para entrar e se autenticar com o SharePoint </span><span class="sxs-lookup"><span data-stu-id="9dd55-122">Provide your SharePoint credentials to sign in to authenticate with SharePoint</span></span>   
   ![Configurar o SharePoint][3]     
5. <span data-ttu-id="9dd55-124">Após a conclusão da autenticação, você será redirecionado ao seu aplicativo lógico para concluí-lo por meio da configuração da caixa de diálogo **Quando um arquivo é criado** do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="9dd55-124">After the authentication completes you'll be redirected to your logic app to complete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="9dd55-125">![Configurar o SharePoint][4]</span><span class="sxs-lookup"><span data-stu-id="9dd55-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="9dd55-126">Em seguida, é possível adicionar outros gatilhos e outras ações necessárias para concluir seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="9dd55-126">You can then add other triggers and actions that you need to complete your logic app.</span></span>   
7. <span data-ttu-id="9dd55-127">Salve seu trabalho selecionando **Salvar** na barra de menus acima.</span><span class="sxs-lookup"><span data-stu-id="9dd55-127">Save your work by selecting **Save** on the menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="9dd55-128">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="9dd55-128">Connector-specific details</span></span>

<span data-ttu-id="9dd55-129">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="9dd55-129">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="9dd55-130">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="9dd55-130">More connectors</span></span>
<span data-ttu-id="9dd55-131">Volte para a [Lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="9dd55-131">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
