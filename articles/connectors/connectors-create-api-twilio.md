---
title: "aaaAdd Olá Twilio Connector em seus aplicativos do Azure lógica | Microsoft Docs"
description: "Visão geral da saudação Twilio conector com parâmetros de API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 43116187-4a2f-42e5-9852-a0d62f08c5fc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/19/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b2b487f34bc76bee24b4237a71ee767d0d22ff7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-twilio-connector"></a><span data-ttu-id="c6a35-103">Introdução ao conector do Twilio Olá</span><span class="sxs-lookup"><span data-stu-id="c6a35-103">Get started with hello Twilio connector</span></span>
<span data-ttu-id="c6a35-104">Conecte-se tooTwilio toosend e receber mensagens SMS e MMS IP global.</span><span class="sxs-lookup"><span data-stu-id="c6a35-104">Connect tooTwilio toosend and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="c6a35-105">Com o Twilio, você pode:</span><span class="sxs-lookup"><span data-stu-id="c6a35-105">With Twilio, you can:</span></span>

* <span data-ttu-id="c6a35-106">Crie o fluxo de negócios com base nos dados Olá que obter do Twilio.</span><span class="sxs-lookup"><span data-stu-id="c6a35-106">Build your business flow based on hello data you get from Twilio.</span></span> 
* <span data-ttu-id="c6a35-107">Use ações para obter uma mensagem, listar mensagens e muito mais.</span><span class="sxs-lookup"><span data-stu-id="c6a35-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="c6a35-108">Essas ações obtém uma resposta e saída de hello tornar disponível para outras ações.</span><span class="sxs-lookup"><span data-stu-id="c6a35-108">These actions get a response, and then make hello output available for other actions.</span></span> <span data-ttu-id="c6a35-109">Por exemplo, quando você recebe uma nova mensagem do Twilio, você pode obtê-la e usá-la como um fluxo de trabalho do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="c6a35-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="c6a35-110">Comece pela criação de um aplicativo lógico; veja [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c6a35-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-tootwilio"></a><span data-ttu-id="c6a35-111">Criar uma conexão tooTwilio</span><span class="sxs-lookup"><span data-stu-id="c6a35-111">Create a connection tooTwilio</span></span>
<span data-ttu-id="c6a35-112">Quando você adiciona esse conector tooyour os aplicativos lógicos, digite Olá Twilio valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="c6a35-112">When you add this Connector tooyour logic apps, enter hello following Twilio values:</span></span>

| <span data-ttu-id="c6a35-113">Propriedade</span><span class="sxs-lookup"><span data-stu-id="c6a35-113">Property</span></span> | <span data-ttu-id="c6a35-114">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="c6a35-114">Required</span></span> | <span data-ttu-id="c6a35-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="c6a35-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="c6a35-116">ID da Conta</span><span class="sxs-lookup"><span data-stu-id="c6a35-116">Account ID</span></span> |<span data-ttu-id="c6a35-117">Sim</span><span class="sxs-lookup"><span data-stu-id="c6a35-117">Yes</span></span> |<span data-ttu-id="c6a35-118">Insira seu ID de conta do Twilio</span><span class="sxs-lookup"><span data-stu-id="c6a35-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="c6a35-119">Token de Acesso</span><span class="sxs-lookup"><span data-stu-id="c6a35-119">Access Token</span></span> |<span data-ttu-id="c6a35-120">Sim</span><span class="sxs-lookup"><span data-stu-id="c6a35-120">Yes</span></span> |<span data-ttu-id="c6a35-121">Insira seu token de acesso do Twilio</span><span class="sxs-lookup"><span data-stu-id="c6a35-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps toocreate a connection tooTwilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="c6a35-122">Se você não tiver um token de acesso do Twilio, veja [Identidade de usuário e Tokens de acesso](https://www.twilio.com/docs/api/chat/guides/identity).</span><span class="sxs-lookup"><span data-stu-id="c6a35-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="c6a35-123">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="c6a35-123">Connector-specific details</span></span>

<span data-ttu-id="c6a35-124">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="c6a35-124">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="c6a35-125">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="c6a35-125">More connectors</span></span>
<span data-ttu-id="c6a35-126">Voltar toohello [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="c6a35-126">Go back toohello [APIs list](apis-list.md).</span></span>
