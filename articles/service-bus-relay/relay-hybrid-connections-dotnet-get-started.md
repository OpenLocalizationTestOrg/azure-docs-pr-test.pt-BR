---
title: "aaaGet iniciado com conexões de híbrida de retransmissão do Azure no .NET | Microsoft Docs"
description: "Escreva um aplicativo de console C# para Conexões Híbridas da Transmissão do Azure."
services: service-bus-relay
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d1386900-b942-4abf-acfc-38d2ef826253
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 1e4af28e7cd4393c8ca965a149a0b83ebcc44f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="847bd-103">Introdução às Conexões Híbridas de Retransmissão</span><span class="sxs-lookup"><span data-stu-id="847bd-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="847bd-104">Este tutorial fornece uma introdução muito[Azure retransmissão híbrida conexões](relay-what-is-it.md#hybrid-connections)e mostra como toouse .NET toocreate um aplicativo cliente que envia mensagens de aplicativo de escuta tooa correspondente.</span><span class="sxs-lookup"><span data-stu-id="847bd-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse .NET toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="847bd-105">O que será realizado</span><span class="sxs-lookup"><span data-stu-id="847bd-105">What will be accomplished</span></span>
<span data-ttu-id="847bd-106">Como as conexões híbridas requer um cliente e um componente de servidor, o tutorial de saudação cria dois aplicativos de console.</span><span class="sxs-lookup"><span data-stu-id="847bd-106">Because Hybrid Connections requires both a client and a server component, hello tutorial creates two console applications.</span></span> <span data-ttu-id="847bd-107">Aqui estão as etapas de saudação:</span><span class="sxs-lookup"><span data-stu-id="847bd-107">Here are hello steps:</span></span>

1. <span data-ttu-id="847bd-108">Crie um namespace de retransmissão, usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="847bd-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="847bd-109">Crie uma conexão híbrida no namespace, usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="847bd-109">Create a hybrid connection in that namespace, using hello Azure portal.</span></span>
3. <span data-ttu-id="847bd-110">Grave mensagens de tooreceive de aplicativo de um console do servidor (ouvinte).</span><span class="sxs-lookup"><span data-stu-id="847bd-110">Write a server (listener) console application tooreceive messages.</span></span>
4. <span data-ttu-id="847bd-111">Grave mensagens de toosend de aplicativo de um console de cliente (remetente).</span><span class="sxs-lookup"><span data-stu-id="847bd-111">Write a client (sender) console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="847bd-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="847bd-112">Prerequisites</span></span>

<span data-ttu-id="847bd-113">toocomplete neste tutorial, você precisará Olá pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="847bd-113">toocomplete this tutorial, you'll need hello following prerequisites:</span></span>

1. <span data-ttu-id="847bd-114">[Visual Studio 2015 ou superior](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="847bd-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="847bd-115">exemplos de saudação neste tutorial usam 2017 do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="847bd-115">hello examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="847bd-116">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="847bd-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="847bd-117">1. Criar um namespace usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="847bd-117">1. Create a namespace using hello Azure portal</span></span>
<span data-ttu-id="847bd-118">Se você já tiver criado um namespace de retransmissão, ir toohello [criar uma conexão híbrida usando Olá portal do Azure](#2-create-a-hybrid-connection-using-the-azure-portal) seção.</span><span class="sxs-lookup"><span data-stu-id="847bd-118">If you have already created a Relay namespace, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="847bd-119">2. Criar uma conexão híbrida usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="847bd-119">2. Create a hybrid connection using hello Azure portal</span></span>
<span data-ttu-id="847bd-120">Se você já tiver criado uma conexão híbrida, ir toohello [criar um aplicativo de servidor](#3-create-a-server-application-listener) seção.</span><span class="sxs-lookup"><span data-stu-id="847bd-120">If you have already created a hybrid connection, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="847bd-121">3. Criar um aplicativo de servidor (escuta)</span><span class="sxs-lookup"><span data-stu-id="847bd-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="847bd-122">toolisten e receber mensagens de saudação retransmissão, podemos irá escrever um aplicativo de console c# usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="847bd-122">toolisten and receive messages from hello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="847bd-123">4. Criar um aplicativo de cliente (remetente)</span><span class="sxs-lookup"><span data-stu-id="847bd-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="847bd-124">toosend toohello de mensagens de retransmissão, que irá escrever um aplicativo de console c# usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="847bd-124">toosend messages toohello Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="847bd-125">5. Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="847bd-125">5. Run hello applications</span></span>
1. <span data-ttu-id="847bd-126">Execute o aplicativo de servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="847bd-126">Run hello server application.</span></span>
2. <span data-ttu-id="847bd-127">Execute o aplicativo de cliente hello e digite algum texto.</span><span class="sxs-lookup"><span data-stu-id="847bd-127">Run hello client application and enter some text.</span></span>
3. <span data-ttu-id="847bd-128">Verifique se o servidor Olá aplicativo console saídas Olá texto inserido no aplicativo de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="847bd-128">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="847bd-130">Parabéns, você criou um aplicativo de Conexões Híbridas completo.</span><span class="sxs-lookup"><span data-stu-id="847bd-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="847bd-131">Próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="847bd-131">Next steps:</span></span>
* [<span data-ttu-id="847bd-132">Perguntas frequentes sobre retransmissão</span><span class="sxs-lookup"><span data-stu-id="847bd-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="847bd-133">Criar um namespace</span><span class="sxs-lookup"><span data-stu-id="847bd-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="847bd-134">Introdução ao Node</span><span class="sxs-lookup"><span data-stu-id="847bd-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

