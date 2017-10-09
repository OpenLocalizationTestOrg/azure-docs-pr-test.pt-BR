---
title: "aaaGet de Introdução ao Azure retransmissão híbrida conexões no nó | Microsoft Docs"
description: "Escreva um aplicativo de console Node.js para as Conexões Híbridas de Retransmissão do Azure."
services: service-bus-relay
documentationcenter: node
author: sethmanheim
manager: timlt
editor: 
ms.assetid: e44e4867-3cf3-46be-8f8a-7671e2013bc4
ms.service: service-bus-relay
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: node
ms.workload: na
ms.date: 07/07/2017
ms.author: sethm
ms.openlocfilehash: 235548399570074f7fd160fec28de8d3633625c5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="effe0-103">Introdução às Conexões Híbridas de Retransmissão</span><span class="sxs-lookup"><span data-stu-id="effe0-103">Get started with Relay Hybrid Connections</span></span>

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="effe0-104">Este tutorial fornece uma introdução muito[Azure retransmissão híbrida conexões](relay-what-is-it.md#hybrid-connections)e mostra como toouse Node. js toocreate um aplicativo cliente que envia mensagens de aplicativo de escuta tooa correspondente.</span><span class="sxs-lookup"><span data-stu-id="effe0-104">This tutorial provides an introduction too[Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how toouse Node.js toocreate a client application that sends messages tooa corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="effe0-105">O que será realizado</span><span class="sxs-lookup"><span data-stu-id="effe0-105">What will be accomplished</span></span>

<span data-ttu-id="effe0-106">Como as Conexões Híbridas exigem um componente de cliente e de servidor, criaremos dois aplicativos de console neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="effe0-106">Because Hybrid Connections requires both a client and a server component, we will create two console applications in this tutorial.</span></span> <span data-ttu-id="effe0-107">Aqui estão as etapas de saudação:</span><span class="sxs-lookup"><span data-stu-id="effe0-107">Here are hello steps:</span></span>

1. <span data-ttu-id="effe0-108">Crie um namespace de retransmissão, usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="effe0-108">Create a Relay namespace, using hello Azure portal.</span></span>
2. <span data-ttu-id="effe0-109">Crie uma conexão híbrida, usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="effe0-109">Create a hybrid connection, using hello Azure portal.</span></span>
3. <span data-ttu-id="effe0-110">Grave um servidor de mensagens de tooreceive do aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="effe0-110">Write a server console application tooreceive messages.</span></span>
4. <span data-ttu-id="effe0-111">Grave um cliente de mensagens de toosend do aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="effe0-111">Write a client console application toosend messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="effe0-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="effe0-112">Prerequisites</span></span>

1. <span data-ttu-id="effe0-113">[Node.js](https://nodejs.org/en/).</span><span class="sxs-lookup"><span data-stu-id="effe0-113">[Node.js](https://nodejs.org/en/).</span></span>
2. <span data-ttu-id="effe0-114">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="effe0-114">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a><span data-ttu-id="effe0-115">1. Criar um namespace usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="effe0-115">1. Create a namespace using hello Azure portal</span></span>

<span data-ttu-id="effe0-116">Se você já tiver criado um namespace de retransmissão, ir toohello [criar uma conexão híbrida usando Olá portal do Azure](#2-create-a-hybrid-connection-using-the-azure-portal) seção.</span><span class="sxs-lookup"><span data-stu-id="effe0-116">If you already have a Relay namespace created, jump toohello [Create a hybrid connection using hello Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a><span data-ttu-id="effe0-117">2. Criar uma conexão híbrida usando Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="effe0-117">2. Create a hybrid connection using hello Azure portal</span></span>

<span data-ttu-id="effe0-118">Se você já tiver uma conexão híbrida criada, ir toohello [criar um aplicativo de servidor](#3-create-a-server-application-listener) seção.</span><span class="sxs-lookup"><span data-stu-id="effe0-118">If you already have a hybrid connection created, jump toohello [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="effe0-119">3. Criar um aplicativo de servidor (escuta)</span><span class="sxs-lookup"><span data-stu-id="effe0-119">3. Create a server application (listener)</span></span>

<span data-ttu-id="effe0-120">toolisten e receber mensagens de saudação retransmissão, irá escrever um aplicativo de console Node. js.</span><span class="sxs-lookup"><span data-stu-id="effe0-120">toolisten and receive messages from hello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="effe0-121">4. Criar um aplicativo de cliente (remetente)</span><span class="sxs-lookup"><span data-stu-id="effe0-121">4. Create a client application (sender)</span></span>

<span data-ttu-id="effe0-122">toosend mensagens toohello retransmissão, irá escrever um aplicativo de console Node. js.</span><span class="sxs-lookup"><span data-stu-id="effe0-122">toosend messages toohello Relay, we will write a Node.js console application.</span></span>

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a><span data-ttu-id="effe0-123">5. Executar aplicativos Olá</span><span class="sxs-lookup"><span data-stu-id="effe0-123">5. Run hello applications</span></span>

1. <span data-ttu-id="effe0-124">Execute o aplicativo de servidor hello: de um tipo de prompt de comando de Node. js `node listener.js`.</span><span class="sxs-lookup"><span data-stu-id="effe0-124">Run hello server application: from a Node.js command prompt type `node listener.js`.</span></span>
2. <span data-ttu-id="effe0-125">Execute o aplicativo de cliente hello: de um tipo de prompt de comando de Node. js `node sender.js`e digite algum texto.</span><span class="sxs-lookup"><span data-stu-id="effe0-125">Run hello client application: from a Node.js command prompt type `node sender.js`, and enter some text.</span></span>
3. <span data-ttu-id="effe0-126">Verifique se o servidor Olá aplicativo console saídas Olá texto inserido no aplicativo de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="effe0-126">Ensure that hello server application console outputs hello text that was entered in hello client application.</span></span>

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

<span data-ttu-id="effe0-128">Parabéns, você criou um aplicativo de Conexões Híbridas de ponta a ponta usando o Node.js!</span><span class="sxs-lookup"><span data-stu-id="effe0-128">Congratulations, you have created an end-to-end Hybrid Connections application using Node.js!</span></span>

## <a name="next-steps"></a><span data-ttu-id="effe0-129">Próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="effe0-129">Next steps:</span></span>

* [<span data-ttu-id="effe0-130">Perguntas frequentes sobre retransmissão</span><span class="sxs-lookup"><span data-stu-id="effe0-130">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="effe0-131">Criar um namespace</span><span class="sxs-lookup"><span data-stu-id="effe0-131">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="effe0-132">Introdução ao .NET</span><span class="sxs-lookup"><span data-stu-id="effe0-132">Get started with .NET</span></span>](relay-hybrid-connections-dotnet-get-started.md)
* [<span data-ttu-id="effe0-133">Introdução ao Node</span><span class="sxs-lookup"><span data-stu-id="effe0-133">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

