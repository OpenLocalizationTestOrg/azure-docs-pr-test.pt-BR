---
title: "Usar o Conector do Slack em seus Aplicativos Lógicos do Azure | Microsoft Docs"
description: "Conectar-se ao Slack em seus aplicativos lógicos"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 234cad64-b13d-4494-ae78-18b17119ba24
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: fc5fc128efe01bd0727e3ff30d8938918e89ac3a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-slack-connector"></a><span data-ttu-id="e9411-103">Introdução ao conector do Slack</span><span class="sxs-lookup"><span data-stu-id="e9411-103">Get started with the Slack connector</span></span>
<span data-ttu-id="e9411-104">O Slack é uma ferramenta de comunicação da equipe que reúne todas as comunicações de equipe em um só lugar, que pode ser pesquisado instantaneamente e está disponível onde você estiver.</span><span class="sxs-lookup"><span data-stu-id="e9411-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="e9411-105">Comece pela criação de um aplicativo lógico; veja [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e9411-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-slack"></a><span data-ttu-id="e9411-106">Criar uma conexão com o Slack</span><span class="sxs-lookup"><span data-stu-id="e9411-106">Create a connection to Slack</span></span>
<span data-ttu-id="e9411-107">Para usar o conector do Slack, crie primeiro uma **conexão** e forneça os detalhes dessas propriedades:</span><span class="sxs-lookup"><span data-stu-id="e9411-107">To use the Slack connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="e9411-108">Propriedade</span><span class="sxs-lookup"><span data-stu-id="e9411-108">Property</span></span> | <span data-ttu-id="e9411-109">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e9411-109">Required</span></span> | <span data-ttu-id="e9411-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="e9411-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e9411-111">A criptografia do token</span><span class="sxs-lookup"><span data-stu-id="e9411-111">Token</span></span> |<span data-ttu-id="e9411-112">Sim</span><span class="sxs-lookup"><span data-stu-id="e9411-112">Yes</span></span> |<span data-ttu-id="e9411-113">Fornecer credenciais do Slack</span><span class="sxs-lookup"><span data-stu-id="e9411-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="e9411-114">Execute estas etapas para entrar no Slack e concluir a configuração da **conexão** do Slack em seu aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="e9411-114">Follow these steps to sign into Slack, and complete the configuration of the Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="e9411-115">Selecione **Recorrência**</span><span class="sxs-lookup"><span data-stu-id="e9411-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="e9411-116">Selecione uma **Frequência** e insira um **Intervalo**</span><span class="sxs-lookup"><span data-stu-id="e9411-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="e9411-117">Selecione **Adicionar uma ação**</span><span class="sxs-lookup"><span data-stu-id="e9411-117">Select **Add an action**</span></span>  
   <span data-ttu-id="e9411-118">![Configurar a Margem de atraso][1]</span><span class="sxs-lookup"><span data-stu-id="e9411-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="e9411-119">Insira Margem de atraso na caixa de pesquisa e aguarde até que a pesquisa retorne todas as entradas com Margem de atraso no nome</span><span class="sxs-lookup"><span data-stu-id="e9411-119">Enter Slack in the search box and wait for the search to return all entries with Slack in the name</span></span>
5. <span data-ttu-id="e9411-120">Selecione **Margem de atraso – Postar mensagem**</span><span class="sxs-lookup"><span data-stu-id="e9411-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="e9411-121">Selecione **Entrar no Slack**:</span><span class="sxs-lookup"><span data-stu-id="e9411-121">Select **Sign in to Slack**:</span></span>  
   <span data-ttu-id="e9411-122">![Configurar a Margem de atraso][2]</span><span class="sxs-lookup"><span data-stu-id="e9411-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="e9411-123">Fornecer suas credenciais do Slack para entrar e autorizar o aplicativo</span><span class="sxs-lookup"><span data-stu-id="e9411-123">Provide your Slack credentials to sign in to authorize the  application</span></span>    
   ![Configurar a Margem de atraso][3]  
8. <span data-ttu-id="e9411-125">Você será redirecionado à página de logon de sua organização.</span><span class="sxs-lookup"><span data-stu-id="e9411-125">You'll be redirected to your organization's Log in page.</span></span> <span data-ttu-id="e9411-126">**Autorize** o Slack a interagir com seu aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="e9411-126">**Authorize** Slack to interact with your logic app:</span></span>      
   <span data-ttu-id="e9411-127">![Configurar a Margem de atraso][5]</span><span class="sxs-lookup"><span data-stu-id="e9411-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="e9411-128">Após o término da autorização, você será redirecionado para seu aplicativo lógico para concluí-lo configurando a seção **Slack - Obter todas as mensagens**.</span><span class="sxs-lookup"><span data-stu-id="e9411-128">After the authorization completes you'll be redirected to your logic app to complete it by configuring the **Slack - Get all messages** section.</span></span> <span data-ttu-id="e9411-129">Adicione outros gatilhos e outras ações necessárias.</span><span class="sxs-lookup"><span data-stu-id="e9411-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="e9411-130">![Configurar a Margem de atraso][6]</span><span class="sxs-lookup"><span data-stu-id="e9411-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="e9411-131">Salve seu trabalho selecionando **Salvar** na barra de menus acima.</span><span class="sxs-lookup"><span data-stu-id="e9411-131">Save your work by selecting **Save** on the menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="e9411-132">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="e9411-132">Connector-specific details</span></span>

<span data-ttu-id="e9411-133">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="e9411-133">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="e9411-134">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="e9411-134">More connectors</span></span>
<span data-ttu-id="e9411-135">Volte para a [Lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e9411-135">Go back to the [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
