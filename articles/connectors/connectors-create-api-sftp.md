---
title: "Saiba como usar o conector SFTP em seus aplicativos lógicos | Microsoft Docs"
description: "Crie aplicativos lógicos com o serviço de Aplicativo do Azure. Conecte-se à API do SFTP para enviar e receber arquivos. Você pode executar várias operações, como criar, atualizar, obter ou excluir arquivos."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 697eb8b0-4a66-40c7-be7b-6aa6b131c7ad
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/20/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 31253d8daee1581167a96a20ba8ad529a04b3e92
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-sftp-connector"></a><span data-ttu-id="c2f2b-105">Introdução ao conector de SFTP</span><span class="sxs-lookup"><span data-stu-id="c2f2b-105">Get started with the SFTP connector</span></span>
<span data-ttu-id="c2f2b-106">Use o conector de SFTP de modo a acessar uma conta SFTP para enviar e receber arquivos.</span><span class="sxs-lookup"><span data-stu-id="c2f2b-106">Use the SFTP connector to access an SFTP account to send and receive files.</span></span> <span data-ttu-id="c2f2b-107">Você pode executar várias operações, como criar, atualizar, obter ou excluir arquivos.</span><span class="sxs-lookup"><span data-stu-id="c2f2b-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="c2f2b-108">Para usar [qualquer conector](apis-list.md), primeiro é preciso criar um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="c2f2b-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="c2f2b-109">Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c2f2b-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-sftp"></a><span data-ttu-id="c2f2b-110">Conectar-se ao SFTP</span><span class="sxs-lookup"><span data-stu-id="c2f2b-110">Connect to SFTP</span></span>
<span data-ttu-id="c2f2b-111">Para que o aplicativo lógico possa acessar qualquer serviço, crie primeiro uma *conexão* com o serviço.</span><span class="sxs-lookup"><span data-stu-id="c2f2b-111">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="c2f2b-112">Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="c2f2b-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-sftp"></a><span data-ttu-id="c2f2b-113">Criar uma conexão com o SFTP</span><span class="sxs-lookup"><span data-stu-id="c2f2b-113">Create a connection to SFTP</span></span>
> [!INCLUDE [Steps to create a connection to SFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="c2f2b-114">Usar um gatilho de SFTP</span><span class="sxs-lookup"><span data-stu-id="c2f2b-114">Use an SFTP trigger</span></span>
<span data-ttu-id="c2f2b-115">Um gatilho é um evento que pode ser usado para iniciar o fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="c2f2b-115">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="c2f2b-116">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c2f2b-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="c2f2b-117">Neste exemplo, o gatilho **SFTP – quando um arquivo é adicionado ou modificado** é usado para iniciar um fluxo de trabalho do aplicativo lógico quando um arquivo é adicionado ou modificado em um servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="c2f2b-117">In this example, the **SFTP - When a file is added or modified** trigger is used to initiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="c2f2b-118">Você também adiciona uma condição que verifica o conteúdo do arquivo novo ou modificado e toma uma decisão para extrair o arquivo se seu conteúdo indicar que ele deve ser extraído antes do uso.</span><span class="sxs-lookup"><span data-stu-id="c2f2b-118">You also add a condition that checks the contents of the new or modified file, and makes a decision to extract the file if its contents indicate that it should be extracted before using the contents.</span></span> <span data-ttu-id="c2f2b-119">Por fim, adicione uma ação para extrair o conteúdo de um arquivo e colocar o conteúdo extraído em uma pasta no servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="c2f2b-119">Finally, add an action to extract the contents of a file, and place the extracted contents in a folder on the SFTP server.</span></span> 

<span data-ttu-id="c2f2b-120">Em um exemplo corporativo, você pode usar esse gatilho para monitorar uma pasta SFTP para novos arquivos que representam pedidos de clientes.</span><span class="sxs-lookup"><span data-stu-id="c2f2b-120">In an enterprise example, you could use this trigger to monitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="c2f2b-121">Você pode usar uma ação do conector SFTP, como **Obter conteúdo do arquivo**, para obter o conteúdo do pedido para ter mais processamento e armazenamento em um banco de dados de pedidos.</span><span class="sxs-lookup"><span data-stu-id="c2f2b-121">You could then use an SFTP connector action, such as **Get file content**, to get the contents of the order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps to create an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="c2f2b-122">Adicionar uma condição</span><span class="sxs-lookup"><span data-stu-id="c2f2b-122">Add a condition</span></span>
> [!INCLUDE [Steps to add a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="c2f2b-123">Usar uma ação de SFTP</span><span class="sxs-lookup"><span data-stu-id="c2f2b-123">Use an SFTP action</span></span>
<span data-ttu-id="c2f2b-124">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="c2f2b-124">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="c2f2b-125">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c2f2b-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="c2f2b-126">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="c2f2b-126">Connector-specific details</span></span>

<span data-ttu-id="c2f2b-127">Veja os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="c2f2b-127">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="c2f2b-128">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="c2f2b-128">More connectors</span></span>
<span data-ttu-id="c2f2b-129">Volte para a [Lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="c2f2b-129">Go back to the [APIs list](apis-list.md).</span></span>