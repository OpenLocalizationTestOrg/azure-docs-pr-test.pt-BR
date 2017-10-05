---
title: "Adicionar o Conector do Twilio aos seus Aplicativos Lógicos do Azure | Microsoft Docs"
description: "Visão geral do Conector do Twilio com os parâmetros da API REST"
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
ms.openlocfilehash: a790ac51b0fea7e3fa379d20e0e094e7ce0d7696
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-twilio-connector"></a><span data-ttu-id="22962-103">Introdução ao conector do Twilio</span><span class="sxs-lookup"><span data-stu-id="22962-103">Get started with the Twilio connector</span></span>
<span data-ttu-id="22962-104">Conecte-se a Twilio para enviar e receber mensagens SMS, MMS e de IP globais.</span><span class="sxs-lookup"><span data-stu-id="22962-104">Connect to Twilio to send and receive global SMS, MMS, and IP messages.</span></span> <span data-ttu-id="22962-105">Com o Twilio, você pode:</span><span class="sxs-lookup"><span data-stu-id="22962-105">With Twilio, you can:</span></span>

* <span data-ttu-id="22962-106">Compile seu fluxo de negócios baseado nos dados obtidos do Twilio.</span><span class="sxs-lookup"><span data-stu-id="22962-106">Build your business flow based on the data you get from Twilio.</span></span> 
* <span data-ttu-id="22962-107">Use ações para obter uma mensagem, listar mensagens e muito mais.</span><span class="sxs-lookup"><span data-stu-id="22962-107">Use actions that get a message, list messages, and more.</span></span> <span data-ttu-id="22962-108">Essas ações obtêm uma resposta e disponibilizam a saída para outras ações.</span><span class="sxs-lookup"><span data-stu-id="22962-108">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="22962-109">Por exemplo, quando você recebe uma nova mensagem do Twilio, você pode obtê-la e usá-la como um fluxo de trabalho do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="22962-109">For example, when  you get a new Twilio message, you can take this message and use it a Service Bus workflow.</span></span> 

<span data-ttu-id="22962-110">Comece pela criação de um aplicativo lógico; veja [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="22962-110">Get started by creating a logic app; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-twilio"></a><span data-ttu-id="22962-111">Criar uma conexão com o Twilio</span><span class="sxs-lookup"><span data-stu-id="22962-111">Create a connection to Twilio</span></span>
<span data-ttu-id="22962-112">Ao adicionar esse Conector aos seus aplicativos lógicos, insira os seguintes valores do Twilio:</span><span class="sxs-lookup"><span data-stu-id="22962-112">When you add this Connector to your logic apps, enter the following Twilio values:</span></span>

| <span data-ttu-id="22962-113">Propriedade</span><span class="sxs-lookup"><span data-stu-id="22962-113">Property</span></span> | <span data-ttu-id="22962-114">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="22962-114">Required</span></span> | <span data-ttu-id="22962-115">Descrição</span><span class="sxs-lookup"><span data-stu-id="22962-115">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22962-116">ID da Conta</span><span class="sxs-lookup"><span data-stu-id="22962-116">Account ID</span></span> |<span data-ttu-id="22962-117">Sim</span><span class="sxs-lookup"><span data-stu-id="22962-117">Yes</span></span> |<span data-ttu-id="22962-118">Insira seu ID de conta do Twilio</span><span class="sxs-lookup"><span data-stu-id="22962-118">Enter your Twilio account ID</span></span> |
| <span data-ttu-id="22962-119">Token de Acesso</span><span class="sxs-lookup"><span data-stu-id="22962-119">Access Token</span></span> |<span data-ttu-id="22962-120">Sim</span><span class="sxs-lookup"><span data-stu-id="22962-120">Yes</span></span> |<span data-ttu-id="22962-121">Insira seu token de acesso do Twilio</span><span class="sxs-lookup"><span data-stu-id="22962-121">Enter your Twilio access token</span></span> |

> [!INCLUDE [Steps to create a connection to Twilio](../../includes/connectors-create-api-twilio.md)]
> 
> 

<span data-ttu-id="22962-122">Se você não tiver um token de acesso do Twilio, veja [Identidade de usuário e Tokens de acesso](https://www.twilio.com/docs/api/chat/guides/identity).</span><span class="sxs-lookup"><span data-stu-id="22962-122">If you don't have a Twilio access token, see [User Identity & Access Tokens](https://www.twilio.com/docs/api/chat/guides/identity).</span></span>

## <a name="connector-specific-details"></a><span data-ttu-id="22962-123">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="22962-123">Connector-specific details</span></span>

<span data-ttu-id="22962-124">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/twilio/).</span><span class="sxs-lookup"><span data-stu-id="22962-124">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/twilio/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="22962-125">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="22962-125">More connectors</span></span>
<span data-ttu-id="22962-126">Volte para a [Lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="22962-126">Go back to the [APIs list](apis-list.md).</span></span>