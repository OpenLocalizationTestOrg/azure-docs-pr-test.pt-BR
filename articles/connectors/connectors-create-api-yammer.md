---
title: "Adicionar o Conector do Yammer ao seu Aplicativo Lógico do Azure | Microsoft Docs"
description: "Visão geral do Conector do Yammer com os parâmetros da API REST"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: b5ae0827-fbb3-45ec-8f45-ad1cc2e7eccc
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: c7a213343b4fb2b5a89a5052a459061b404a431c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-yammer-connector"></a><span data-ttu-id="8fcbb-103">Introdução ao conector do Yammer</span><span class="sxs-lookup"><span data-stu-id="8fcbb-103">Get started with the Yammer connector</span></span>
<span data-ttu-id="8fcbb-104">Conecte-se ao Yammer para acessar conversas em sua rede corporativa.</span><span class="sxs-lookup"><span data-stu-id="8fcbb-104">Connect to Yammer to access conversations in your enterprise network.</span></span> <span data-ttu-id="8fcbb-105">Com o Yammer, você pode:</span><span class="sxs-lookup"><span data-stu-id="8fcbb-105">With Yammer, you can:</span></span>

* <span data-ttu-id="8fcbb-106">Crie seu fluxo de negócios baseado nos dados obtidos do Yammer.</span><span class="sxs-lookup"><span data-stu-id="8fcbb-106">Build your business flow based on the data you get from Yammer.</span></span> 
* <span data-ttu-id="8fcbb-107">Use gatilhos para quando há uma nova mensagem em um grupo ou um feed a seguir.</span><span class="sxs-lookup"><span data-stu-id="8fcbb-107">Use triggers for when there is a new message in a group, or a feed your following.</span></span>
* <span data-ttu-id="8fcbb-108">Use as ações para postar uma mensagem, obter todas as mensagens e muito mais.</span><span class="sxs-lookup"><span data-stu-id="8fcbb-108">Use actions to post a message, get all messages, and more.</span></span> <span data-ttu-id="8fcbb-109">Essas ações obtêm uma resposta e disponibilizam a saída para outras ações.</span><span class="sxs-lookup"><span data-stu-id="8fcbb-109">These actions get a response, and then make the output available for other actions.</span></span> <span data-ttu-id="8fcbb-110">Por exemplo, quando uma nova mensagem for exibida, você poderá enviar um email usando o Office 365.</span><span class="sxs-lookup"><span data-stu-id="8fcbb-110">For example, when a new message appears, you can send an email using Office 365.</span></span>

<span data-ttu-id="8fcbb-111">Comece pela criação de um aplicativo lógico; veja [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="8fcbb-111">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-yammer"></a><span data-ttu-id="8fcbb-112">Criar uma conexão com o Yammer</span><span class="sxs-lookup"><span data-stu-id="8fcbb-112">Create a connection to Yammer</span></span>
<span data-ttu-id="8fcbb-113">Para usar o conector do Yammer, você primeiro cria uma **conexão**, em seguida, fornece os detalhes dessas propriedades:</span><span class="sxs-lookup"><span data-stu-id="8fcbb-113">To use the Yammer connector, you first create a **connection** then provide the details for these properties:</span></span> 

| <span data-ttu-id="8fcbb-114">Propriedade</span><span class="sxs-lookup"><span data-stu-id="8fcbb-114">Property</span></span> | <span data-ttu-id="8fcbb-115">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="8fcbb-115">Required</span></span> | <span data-ttu-id="8fcbb-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="8fcbb-116">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8fcbb-117">A criptografia do token</span><span class="sxs-lookup"><span data-stu-id="8fcbb-117">Token</span></span> |<span data-ttu-id="8fcbb-118">Sim</span><span class="sxs-lookup"><span data-stu-id="8fcbb-118">Yes</span></span> |<span data-ttu-id="8fcbb-119">Fornecer suas credenciais do Yammer</span><span class="sxs-lookup"><span data-stu-id="8fcbb-119">Provide Yammer Credentials</span></span> |

> [!INCLUDE [Steps to create a connection to Yammer](../../includes/connectors-create-api-yammer.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="8fcbb-120">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="8fcbb-120">Connector-specific details</span></span>

<span data-ttu-id="8fcbb-121">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/yammer/).</span><span class="sxs-lookup"><span data-stu-id="8fcbb-121">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/yammer/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="8fcbb-122">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="8fcbb-122">More connectors</span></span>
<span data-ttu-id="8fcbb-123">Volte para a [Lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="8fcbb-123">Go back to the [APIs list](apis-list.md).</span></span>