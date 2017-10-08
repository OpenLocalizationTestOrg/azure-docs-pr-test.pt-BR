---
title: "Olá aaaUse do SharePoint Server Connector em seus aplicativos lógicos | Microsoft Docs"
description: "Começar a usar Olá Olá do SharePoint Server Connector em seus aplicativos lógicos"
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
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a><span data-ttu-id="c95c0-103">Introdução ao conector do SharePoint Olá</span><span class="sxs-lookup"><span data-stu-id="c95c0-103">Get started with hello SharePoint connector</span></span>
<span data-ttu-id="c95c0-104">Olá conector do SharePoint fornece um toowork de maneira com listas no SharePoint.</span><span class="sxs-lookup"><span data-stu-id="c95c0-104">hello SharePoint Connector provides an way toowork with Lists on SharePoint.</span></span>

<span data-ttu-id="c95c0-105">Comece pela criação de um aplicativo lógico; veja [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c95c0-105">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-toosharepoint"></a><span data-ttu-id="c95c0-106">Criar uma conexão tooSharePoint</span><span class="sxs-lookup"><span data-stu-id="c95c0-106">Create a connection tooSharePoint</span></span>
<span data-ttu-id="c95c0-107">toouse Olá conector do SharePoint, você primeiro crie um **conexão** Forneça detalhes de saudação para essas propriedades:</span><span class="sxs-lookup"><span data-stu-id="c95c0-107">toouse hello SharePoint Connector , you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="c95c0-108">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c95c0-108">Property</span></span> | <span data-ttu-id="c95c0-109">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="c95c0-109">Required</span></span> | <span data-ttu-id="c95c0-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="c95c0-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c95c0-111">A criptografia do token</span><span class="sxs-lookup"><span data-stu-id="c95c0-111">Token</span></span> |<span data-ttu-id="c95c0-112">Sim</span><span class="sxs-lookup"><span data-stu-id="c95c0-112">Yes</span></span> |<span data-ttu-id="c95c0-113">Fornecer credenciais do SharePoint</span><span class="sxs-lookup"><span data-stu-id="c95c0-113">Provide SharePoint Credentials</span></span> |

<span data-ttu-id="c95c0-114">tooconnect muito**SharePoint**, digite tooSharePoint sua identidade (nome de usuário e senha, as credenciais de cartão inteligente, etc.).</span><span class="sxs-lookup"><span data-stu-id="c95c0-114">tooconnect too**SharePoint**, enter your identity (username and password, smart card credentials, etc.) tooSharePoint.</span></span> <span data-ttu-id="c95c0-115">Depois que você tenha sido autenticado, você poderá continuar conector do toouse saudação do SharePoint em seu aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="c95c0-115">Once you've been authenticated, you can proceed toouse hello SharePoint connector  in your logic app.</span></span> 

<span data-ttu-id="c95c0-116">Enquanto no designer de saudação do seu aplicativo lógico, siga toosign essas etapas na conexão de saudação do SharePoint toocreate **conexão** para uso em seu aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="c95c0-116">While on hello designer of your logic app, follow these steps toosign into SharePoint toocreate hello connection **connection** for use in your logic app:</span></span>

1. <span data-ttu-id="c95c0-117">Insira do SharePoint na caixa de pesquisa hello e aguarde Olá pesquisa tooreturn todas as entradas com o SharePoint em nome de saudação:</span><span class="sxs-lookup"><span data-stu-id="c95c0-117">Enter SharePoint in hello search box and wait for hello search tooreturn all entries with SharePoint in hello name:</span></span>   
   ![Configurar o SharePoint][1]  
2. <span data-ttu-id="c95c0-119">Selecione **SharePoint – Quando um arquivo é criado**</span><span class="sxs-lookup"><span data-stu-id="c95c0-119">Select **SharePoint - When a file is created**</span></span>   
3. <span data-ttu-id="c95c0-120">Selecione **entrar tooSharePoint**:</span><span class="sxs-lookup"><span data-stu-id="c95c0-120">Select **Sign in tooSharePoint**:</span></span>   
   <span data-ttu-id="c95c0-121">![Configurar o SharePoint][2]</span><span class="sxs-lookup"><span data-stu-id="c95c0-121">![Configure SharePoint][2]</span></span>    
4. <span data-ttu-id="c95c0-122">Forneça seu toosign de credenciais do SharePoint no tooauthenticate com o SharePoint</span><span class="sxs-lookup"><span data-stu-id="c95c0-122">Provide your SharePoint credentials toosign in tooauthenticate with SharePoint</span></span>   
   ![Configurar o SharePoint][3]     
5. <span data-ttu-id="c95c0-124">Após a conclusão da autenticação Olá você será redirecionado tooyour lógica aplicativo toocomplete-lo por meio da configuração do SharePoint **quando um arquivo é criado** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="c95c0-124">After hello authentication completes you'll be redirected tooyour logic app toocomplete it by configuring SharePoint's **When a file is created** dialog.</span></span>          
   <span data-ttu-id="c95c0-125">![Configurar o SharePoint][4]</span><span class="sxs-lookup"><span data-stu-id="c95c0-125">![Configure SharePoint][4]</span></span>  
6. <span data-ttu-id="c95c0-126">Em seguida, você pode adicionar outros gatilhos e ações que você precisa toocomplete seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="c95c0-126">You can then add other triggers and actions that you need toocomplete your logic app.</span></span>   
7. <span data-ttu-id="c95c0-127">Salve seu trabalho selecionando **salvar** na barra de menus do hello acima.</span><span class="sxs-lookup"><span data-stu-id="c95c0-127">Save your work by selecting **Save** on hello menu bar above.</span></span>  

## <a name="connector-specific-details"></a><span data-ttu-id="c95c0-128">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="c95c0-128">Connector-specific details</span></span>

<span data-ttu-id="c95c0-129">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/sharepoint/).</span><span class="sxs-lookup"><span data-stu-id="c95c0-129">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sharepoint/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="c95c0-130">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="c95c0-130">More connectors</span></span>
<span data-ttu-id="c95c0-131">Voltar toohello [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="c95c0-131">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
