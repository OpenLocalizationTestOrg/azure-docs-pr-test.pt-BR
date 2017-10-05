---
title: "Conector do GitHub no Aplicativo Lógico do Azure | Microsoft Docs"
description: "Crie Aplicativos Lógicos com o serviço de Aplicativo do Azure. O GitHub é um serviço de hospedagem do repositório Git baseado na Web. Ele oferece toda a funcionalidade de controle de revisão distribuída e de SCM (gerenciamento do código-fonte) do Git, além de adicionar seus próprios recursos."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 8f873e6c-f4c0-4c2e-a5bd-2e953efe5e2b
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: d4614b0ceff0ec0d36dbb1a136551f985f2fc1a1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-github-connector"></a><span data-ttu-id="4baef-105">Introdução ao conector do GitHub</span><span class="sxs-lookup"><span data-stu-id="4baef-105">Get started with the GitHub connector</span></span>
<span data-ttu-id="4baef-106">O GitHub é um serviço de hospedagem do repositório Git baseado na Web.</span><span class="sxs-lookup"><span data-stu-id="4baef-106">GitHub is a web-based Git repository hosting service.</span></span> <span data-ttu-id="4baef-107">Ele oferece toda a funcionalidade de controle de revisão distribuída e de SCM (gerenciamento do código-fonte) do Git, além de adicionar seus próprios recursos.</span><span class="sxs-lookup"><span data-stu-id="4baef-107">It offers all of the distributed revision control and source code management (SCM) functionality of Git as well as adding its own features.</span></span>

<span data-ttu-id="4baef-108">É possível começar criando um aplicativo lógico agora; consulte [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="4baef-108">You can get started by creating a Logic app now, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="create-a-connection-to-github"></a><span data-ttu-id="4baef-109">Criar uma conexão com o GitHub</span><span class="sxs-lookup"><span data-stu-id="4baef-109">Create a connection to GitHub</span></span>
<span data-ttu-id="4baef-110">Para criar Aplicativos lógicos com o GitHub, você deve primeiro criar uma **conexão**, em seguida, fornecer os detalhes para as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="4baef-110">To create Logic apps with GitHub, you must first create a **connection** then provide the details for the following properties:</span></span> 

| <span data-ttu-id="4baef-111">Propriedade</span><span class="sxs-lookup"><span data-stu-id="4baef-111">Property</span></span> | <span data-ttu-id="4baef-112">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="4baef-112">Required</span></span> | <span data-ttu-id="4baef-113">Descrição</span><span class="sxs-lookup"><span data-stu-id="4baef-113">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4baef-114">A criptografia do token</span><span class="sxs-lookup"><span data-stu-id="4baef-114">Token</span></span> |<span data-ttu-id="4baef-115">Sim</span><span class="sxs-lookup"><span data-stu-id="4baef-115">Yes</span></span> |<span data-ttu-id="4baef-116">Fornecer as credenciais do GitHub</span><span class="sxs-lookup"><span data-stu-id="4baef-116">Provide GitHub Credentials</span></span> |

<span data-ttu-id="4baef-117">Depois de criar a conexão, é possível usá-la para executar as ações e ouvir os gatilhos descritos neste artigo.</span><span class="sxs-lookup"><span data-stu-id="4baef-117">After you create the connection, you can use it to execute the actions and listen for the triggers described in this article.</span></span> 

> [!INCLUDE [Steps to create a connection to GitHub](../../includes/connectors-create-api-github.md)]
> 

## <a name="connector-specific-details"></a><span data-ttu-id="4baef-118">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="4baef-118">Connector-specific details</span></span>

<span data-ttu-id="4baef-119">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/github/).</span><span class="sxs-lookup"><span data-stu-id="4baef-119">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/github/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="4baef-120">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="4baef-120">More connectors</span></span>
<span data-ttu-id="4baef-121">Volte para a [Lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="4baef-121">Go back to the [APIs list](apis-list.md).</span></span>