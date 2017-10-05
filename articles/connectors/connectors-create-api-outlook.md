---
title: "Conector do Outlook.com no Aplicativo Lógico do Azure | Microsoft Docs"
description: "Crie Aplicativos Lógicos com o serviço de Aplicativo do Azure. O conector do Outlook.com permite que você gerencie seus emails, calendários e contatos. É possível executar várias ações, como enviar emails, agendar reuniões, adicionar contatos, etc."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 87113c85-d158-4dd5-9ed5-5748130003d6
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: bde1629504c97cf6706b42219570ffa6243073dd
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-outlookcom-connector"></a><span data-ttu-id="99360-105">Introdução ao conector do Outlook.com</span><span class="sxs-lookup"><span data-stu-id="99360-105">Get started with the Outlook.com connector</span></span>
<span data-ttu-id="99360-106">O conector do Outlook.com permite que você gerencie seus emails, calendários e contatos.</span><span class="sxs-lookup"><span data-stu-id="99360-106">Outlook.com connector allows you to manage your mail, calendars, and contacts.</span></span> <span data-ttu-id="99360-107">É possível executar várias ações, como enviar emails, agendar reuniões, adicionar contatos, etc.</span><span class="sxs-lookup"><span data-stu-id="99360-107">You can perform various actions such as send mail, schedule meetings, add contacts, etc.</span></span>

<span data-ttu-id="99360-108">É possível começar criando um aplicativo lógico agora; consulte [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="99360-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-outlookcom"></a><span data-ttu-id="99360-109">Criar uma conexão com o Outlook.com</span><span class="sxs-lookup"><span data-stu-id="99360-109">Create a connection to Outlook.com</span></span>
<span data-ttu-id="99360-110">Para criar Aplicativos Lógicos com o Outlook.com, primeiro, você deve criar uma **conexão** e, em seguida, fornecer os detalhes das seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="99360-110">To create Logic apps with Outlook.com, you must first create a **connection** then provide the details for the following properties:</span></span>

| <span data-ttu-id="99360-111">Propriedade</span><span class="sxs-lookup"><span data-stu-id="99360-111">Property</span></span> | <span data-ttu-id="99360-112">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="99360-112">Required</span></span> | <span data-ttu-id="99360-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="99360-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="99360-114">A criptografia do token</span><span class="sxs-lookup"><span data-stu-id="99360-114">Token</span></span> |<span data-ttu-id="99360-115">Sim</span><span class="sxs-lookup"><span data-stu-id="99360-115">Yes</span></span> |<span data-ttu-id="99360-116">Fornecer as credenciais do Outlook.com</span><span class="sxs-lookup"><span data-stu-id="99360-116">Provide Outlook.com Credentials</span></span> |

<span data-ttu-id="99360-117">Depois de criar a conexão, é possível usá-la para executar as ações e ouvir os gatilhos descritos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="99360-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span>

> [!INCLUDE [Steps to create a connection to Outlook.com](../../includes/connectors-create-api-outlook.md)]
>

## <a name="connector-specific-details"></a><span data-ttu-id="99360-118">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="99360-118">Connector-specific details</span></span>

<span data-ttu-id="99360-119">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/outlook/).</span><span class="sxs-lookup"><span data-stu-id="99360-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/outlook/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="99360-120">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="99360-120">More connectors</span></span>
<span data-ttu-id="99360-121">Volte para a [Lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="99360-121">Go back to the [APIs list](apis-list.md).</span></span>