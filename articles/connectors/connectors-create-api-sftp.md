---
title: "aaaLearn como toouse Olá conector SFTP em seus aplicativos lógicos | Microsoft Docs"
description: "Crie aplicativos lógicos com o serviço de Aplicativo do Azure. Conecte-se toosend tooSFTP API e receber arquivos. Você pode executar várias operações, como criar, atualizar, obter ou excluir arquivos."
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
ms.openlocfilehash: 3f50570191c9b9339fe6584b9056b2549512b789
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sftp-connector"></a><span data-ttu-id="17934-105">Introdução ao conector SFTP Olá</span><span class="sxs-lookup"><span data-stu-id="17934-105">Get started with hello SFTP connector</span></span>
<span data-ttu-id="17934-106">Use Olá SFTP conector tooaccess um toosend de conta SFTP e receber arquivos.</span><span class="sxs-lookup"><span data-stu-id="17934-106">Use hello SFTP connector tooaccess an SFTP account toosend and receive files.</span></span> <span data-ttu-id="17934-107">Você pode executar várias operações, como criar, atualizar, obter ou excluir arquivos.</span><span class="sxs-lookup"><span data-stu-id="17934-107">You can perform various operations such as create, update, get or delete files.</span></span>  

<span data-ttu-id="17934-108">toouse [qualquer conector](apis-list.md), primeiro é necessário toocreate um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="17934-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="17934-109">Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="17934-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosftp"></a><span data-ttu-id="17934-110">Conecte-se tooSFTP</span><span class="sxs-lookup"><span data-stu-id="17934-110">Connect tooSFTP</span></span>
<span data-ttu-id="17934-111">Antes de sua lógica de aplicativo pode acessar qualquer serviço, primeiro é necessário toocreate um *conexão* toohello service.</span><span class="sxs-lookup"><span data-stu-id="17934-111">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="17934-112">Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="17934-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosftp"></a><span data-ttu-id="17934-113">Criar uma conexão tooSFTP</span><span class="sxs-lookup"><span data-stu-id="17934-113">Create a connection tooSFTP</span></span>
> [!INCLUDE [Steps toocreate a connection tooSFTP](../../includes/connectors-create-api-sftp.md)]
> 
> 

## <a name="use-an-sftp-trigger"></a><span data-ttu-id="17934-114">Usar um gatilho de SFTP</span><span class="sxs-lookup"><span data-stu-id="17934-114">Use an SFTP trigger</span></span>
<span data-ttu-id="17934-115">Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="17934-115">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="17934-116">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="17934-116">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

<span data-ttu-id="17934-117">Neste exemplo, Olá **SFTP - quando um arquivo é adicionado ou modificado** gatilho é um fluxo de trabalho do aplicativo de lógica de tooinitiate usado quando um arquivo é adicionado ao ou modificado em um servidor SFTP.</span><span class="sxs-lookup"><span data-stu-id="17934-117">In this example, hello **SFTP - When a file is added or modified** trigger is used tooinitiate a logic app workflow when a file is added to, or modified on, an SFTP server.</span></span> <span data-ttu-id="17934-118">Você também pode adicionar uma condição que verifica o conteúdo de saudação do arquivo de novos ou modificados da saudação e faz com que um arquivo de saudação tooextract decisão se seu conteúdo indicar que deve ser extraído antes de usar o conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="17934-118">You also add a condition that checks hello contents of hello new or modified file, and makes a decision tooextract hello file if its contents indicate that it should be extracted before using hello contents.</span></span> <span data-ttu-id="17934-119">Finalmente, adicione um conteúdo de saudação do tooextract de ação de um arquivo e colocar o conteúdo de saudação extraído em uma pasta no servidor SFTP Olá.</span><span class="sxs-lookup"><span data-stu-id="17934-119">Finally, add an action tooextract hello contents of a file, and place hello extracted contents in a folder on hello SFTP server.</span></span> 

<span data-ttu-id="17934-120">Um exemplo de empresa, você pode usar toomonitor esse gatilho uma pasta SFTP para novos arquivos que representam os pedidos de clientes.</span><span class="sxs-lookup"><span data-stu-id="17934-120">In an enterprise example, you could use this trigger toomonitor an SFTP folder for new files that represent customer orders.</span></span>  <span data-ttu-id="17934-121">Você pode usar uma ação de conector SFTP, tais como **obter conteúdo do arquivo**, conteúdo de saudação tooget de ordem de saudação para processamento e armazenamento em um banco de dados de pedidos.</span><span class="sxs-lookup"><span data-stu-id="17934-121">You could then use an SFTP connector action, such as **Get file content**, tooget hello contents of hello order for further processing and storage in an orders database.</span></span>

> [!INCLUDE [Steps toocreate an SFTP trigger](../../includes/connectors-create-api-sftp-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="17934-122">Adicionar uma condição</span><span class="sxs-lookup"><span data-stu-id="17934-122">Add a condition</span></span>
> [!INCLUDE [Steps tooadd a condition](../../includes/connectors-create-api-sftp-condition.md)]
> 
> 

## <a name="use-an-sftp-action"></a><span data-ttu-id="17934-123">Usar uma ação de SFTP</span><span class="sxs-lookup"><span data-stu-id="17934-123">Use an SFTP action</span></span>
<span data-ttu-id="17934-124">Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="17934-124">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="17934-125">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="17934-125">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate an SFTP action](../../includes/connectors-create-api-sftp-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="17934-126">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="17934-126">Connector-specific details</span></span>

<span data-ttu-id="17934-127">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/sftpconnector/).</span><span class="sxs-lookup"><span data-stu-id="17934-127">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/sftpconnector/).</span></span>

## <a name="more-connectors"></a><span data-ttu-id="17934-128">Mais conectores</span><span class="sxs-lookup"><span data-stu-id="17934-128">More connectors</span></span>
<span data-ttu-id="17934-129">Voltar toohello [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="17934-129">Go back toohello [APIs list](apis-list.md).</span></span>
