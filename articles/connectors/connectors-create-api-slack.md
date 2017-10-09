---
title: "Olá aaaUse conector de margem de atraso em seus aplicativos lógicos do Azure | Microsoft Docs"
description: "Conecte-se tooSlack em seus aplicativos lógicos"
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
ms.openlocfilehash: 6599d7b69d2147425c9fab978c5d0f93e5605f19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-slack-connector"></a><span data-ttu-id="cbba8-103">Introdução ao conector de margem de atraso de saudação</span><span class="sxs-lookup"><span data-stu-id="cbba8-103">Get started with hello Slack connector</span></span>
<span data-ttu-id="cbba8-104">O Slack é uma ferramenta de comunicação da equipe que reúne todas as comunicações de equipe em um só lugar, que pode ser pesquisado instantaneamente e está disponível onde você estiver.</span><span class="sxs-lookup"><span data-stu-id="cbba8-104">Slack is a team communication tool, that brings together all of your team communications in one place, instantly searchable and available wherever you go.</span></span> 

<span data-ttu-id="cbba8-105">Comece pela criação de um aplicativo lógico; veja [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="cbba8-105">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tooslack"></a><span data-ttu-id="cbba8-106">Criar uma conexão tooSlack</span><span class="sxs-lookup"><span data-stu-id="cbba8-106">Create a connection tooSlack</span></span>
<span data-ttu-id="cbba8-107">conector de margem de atraso de saudação toouse, primeiro você cria um **conexão** Forneça detalhes de saudação para essas propriedades:</span><span class="sxs-lookup"><span data-stu-id="cbba8-107">toouse hello Slack connector, you first create a **connection** then provide hello details for these properties:</span></span> 

| <span data-ttu-id="cbba8-108">Propriedade</span><span class="sxs-lookup"><span data-stu-id="cbba8-108">Property</span></span> | <span data-ttu-id="cbba8-109">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="cbba8-109">Required</span></span> | <span data-ttu-id="cbba8-110">Descrição</span><span class="sxs-lookup"><span data-stu-id="cbba8-110">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cbba8-111">A criptografia do token</span><span class="sxs-lookup"><span data-stu-id="cbba8-111">Token</span></span> |<span data-ttu-id="cbba8-112">Sim</span><span class="sxs-lookup"><span data-stu-id="cbba8-112">Yes</span></span> |<span data-ttu-id="cbba8-113">Fornecer credenciais do Slack</span><span class="sxs-lookup"><span data-stu-id="cbba8-113">Provide Slack Credentials</span></span> |

<span data-ttu-id="cbba8-114">Siga essas etapas toosign em atraso e configuração Olá completa de saudação atraso **conexão** em seu aplicativo lógica:</span><span class="sxs-lookup"><span data-stu-id="cbba8-114">Follow these steps toosign into Slack, and complete hello configuration of hello Slack **connection** in your logic app:</span></span>

1. <span data-ttu-id="cbba8-115">Selecione **Recorrência**</span><span class="sxs-lookup"><span data-stu-id="cbba8-115">Select **Recurrence**</span></span>
2. <span data-ttu-id="cbba8-116">Selecione uma **Frequência** e insira um **Intervalo**</span><span class="sxs-lookup"><span data-stu-id="cbba8-116">Select a **Frequency** and enter an **Interval**</span></span>
3. <span data-ttu-id="cbba8-117">Selecione **Adicionar uma ação**</span><span class="sxs-lookup"><span data-stu-id="cbba8-117">Select **Add an action**</span></span>  
   <span data-ttu-id="cbba8-118">![Configurar a Margem de atraso][1]</span><span class="sxs-lookup"><span data-stu-id="cbba8-118">![Configure Slack][1]</span></span>  
4. <span data-ttu-id="cbba8-119">Insira o atraso na caixa de pesquisa hello e aguarde Olá pesquisa tooreturn todas as entradas com atraso no nome da saudação</span><span class="sxs-lookup"><span data-stu-id="cbba8-119">Enter Slack in hello search box and wait for hello search tooreturn all entries with Slack in hello name</span></span>
5. <span data-ttu-id="cbba8-120">Selecione **Margem de atraso – Postar mensagem**</span><span class="sxs-lookup"><span data-stu-id="cbba8-120">Select **Slack - Post message**</span></span>
6. <span data-ttu-id="cbba8-121">Selecione **entrar tooSlack**:</span><span class="sxs-lookup"><span data-stu-id="cbba8-121">Select **Sign in tooSlack**:</span></span>  
   <span data-ttu-id="cbba8-122">![Configurar a Margem de atraso][2]</span><span class="sxs-lookup"><span data-stu-id="cbba8-122">![Configure Slack][2]</span></span>
7. <span data-ttu-id="cbba8-123">Forneça seu toosign margem de atraso de credenciais no aplicativo de hello tooauthorize</span><span class="sxs-lookup"><span data-stu-id="cbba8-123">Provide your Slack credentials toosign in tooauthorize hello  application</span></span>    
   ![Configurar a Margem de atraso][3]  
8. <span data-ttu-id="cbba8-125">Você será Log redirecionado tooyour organização na página.</span><span class="sxs-lookup"><span data-stu-id="cbba8-125">You'll be redirected tooyour organization's Log in page.</span></span> <span data-ttu-id="cbba8-126">**Autorizar** toointeract Slack com seu aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="cbba8-126">**Authorize** Slack toointeract with your logic app:</span></span>      
   <span data-ttu-id="cbba8-127">![Configurar a Margem de atraso][5]</span><span class="sxs-lookup"><span data-stu-id="cbba8-127">![Configure Slack][5]</span></span> 
9. <span data-ttu-id="cbba8-128">Após a conclusão da autorização Olá você será redirecionado tooyour lógica aplicativo toocomplete-Configurando Olá **atraso - obter todas as mensagens** seção.</span><span class="sxs-lookup"><span data-stu-id="cbba8-128">After hello authorization completes you'll be redirected tooyour logic app toocomplete it by configuring hello **Slack - Get all messages** section.</span></span> <span data-ttu-id="cbba8-129">Adicione outros gatilhos e outras ações necessárias.</span><span class="sxs-lookup"><span data-stu-id="cbba8-129">Add other triggers and actions that you need.</span></span>  
   <span data-ttu-id="cbba8-130">![Configurar a Margem de atraso][6]</span><span class="sxs-lookup"><span data-stu-id="cbba8-130">![Configure Slack][6]</span></span>
10. <span data-ttu-id="cbba8-131">Salve seu trabalho selecionando **salvar** na barra de menus do hello acima.</span><span class="sxs-lookup"><span data-stu-id="cbba8-131">Save your work by selecting **Save** on hello menu bar above.</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="cbba8-132">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="cbba8-132">Connector-specific details</span></span>

<span data-ttu-id="cbba8-133">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/slack/).</span><span class="sxs-lookup"><span data-stu-id="cbba8-133">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/slack/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="cbba8-134">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="cbba8-134">More connectors</span></span>
<span data-ttu-id="cbba8-135">Voltar toohello [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="cbba8-135">Go back toohello [APIs list](apis-list.md).</span></span>

[1]: ./media/connectors-create-api-slack/connectionconfig1.png
[2]: ./media/connectors-create-api-slack/connectionconfig2.png 
[3]: ./media/connectors-create-api-slack/connectionconfig3.png
[4]: ./media/connectors-create-api-slack/connectionconfig4.png
[5]: ./media/connectors-create-api-slack/connectionconfig5.png
[6]: ./media/connectors-create-api-slack/connectionconfig6.png
