---
title: "Conector do Wunderlist no Aplicativo Lógico do Azure | Microsoft Docs"
description: "Criar uma conexão com o Wunderlist e usar essa conexão para compilar seu fluxo de trabalho nos aplicativos lógicos."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: e4773ecf-3ad3-44b4-a1b5-ee5f58baeadd
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 899110992cc52ca5edf1706320fd5570473de784
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-wunderlist-connector"></a><span data-ttu-id="61eb6-103">Introdução ao conector do Wunderlist</span><span class="sxs-lookup"><span data-stu-id="61eb6-103">Get started with the Wunderlist connector</span></span>
<span data-ttu-id="61eb6-104">O Wunderlist fornece um gerenciador de tarefas e de lista de tarefas pendentes para ajudar as pessoas a realizar seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="61eb6-104">Wunderlist provide a todo list and task manager to help people get their stuff done.</span></span>  <span data-ttu-id="61eb6-105">Se você estiver compartilhando uma lista de compras com alguém da família, trabalhando em um projeto ou planejando suas férias, o Wunderlist facilitará a captura, o compartilhamento e a realização de suas listas de tarefas pendentes.</span><span class="sxs-lookup"><span data-stu-id="61eb6-105">Whether you’re sharing a grocery list with a loved one, working on a project, or planning a vacation, Wunderlist makes it easy to capture, share, and complete your to¬dos.</span></span> <span data-ttu-id="61eb6-106">O Wunderlist é sincronizado instantaneamente com seu telefone, tablet e computador, para que você possa acessar todas as tarefas de qualquer lugar.</span><span class="sxs-lookup"><span data-stu-id="61eb6-106">Wunderlist instantly syncs between your phone, tablet and computer, so you can access all your tasks from anywhere.</span></span>

<span data-ttu-id="61eb6-107">Comece pela criação de um aplicativo lógico; veja [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="61eb6-107">Get started by creating a logic app now; see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-wunderlist"></a><span data-ttu-id="61eb6-108">Criar uma conexão com o Wunderlist</span><span class="sxs-lookup"><span data-stu-id="61eb6-108">Create a connection to Wunderlist</span></span>
<span data-ttu-id="61eb6-109">Para criar Aplicativos lógicos com o Wunderlist, primeiro você deve criar uma **conexão**, em seguida, forneça os detalhes para as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="61eb6-109">To create Logic apps with Wunderlist, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="61eb6-110">Propriedade</span><span class="sxs-lookup"><span data-stu-id="61eb6-110">Property</span></span> | <span data-ttu-id="61eb6-111">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="61eb6-111">Required</span></span> | <span data-ttu-id="61eb6-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="61eb6-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="61eb6-113">A criptografia do token</span><span class="sxs-lookup"><span data-stu-id="61eb6-113">Token</span></span> |<span data-ttu-id="61eb6-114">Sim</span><span class="sxs-lookup"><span data-stu-id="61eb6-114">Yes</span></span> |<span data-ttu-id="61eb6-115">Fornecer credenciais do Wunderlist</span><span class="sxs-lookup"><span data-stu-id="61eb6-115">Provide Wunderlist Credentials</span></span> |

<span data-ttu-id="61eb6-116">Depois de criar a conexão, é possível usá-la para executar as ações e ouvir os gatilhos.</span><span class="sxs-lookup"><span data-stu-id="61eb6-116">After you create the connection, you can use it to execute the actions and listen for the triggers.</span></span>

> [!INCLUDE [Steps to create a connection to Wunderlist](../../includes/connectors-create-api-wunderlist.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="61eb6-117">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="61eb6-117">Connector-specific details</span></span>

<span data-ttu-id="61eb6-118">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/wunderlist/).</span><span class="sxs-lookup"><span data-stu-id="61eb6-118">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/wunderlist/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="61eb6-119">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="61eb6-119">More connectors</span></span>
<span data-ttu-id="61eb6-120">Volte para a [Lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="61eb6-120">Go back to the [APIs list](apis-list.md).</span></span>