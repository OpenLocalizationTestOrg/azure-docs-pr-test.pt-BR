---
title: "Introdução às conexões híbridas de retransmissão do Azure no .NET | Microsoft Docs"
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
ms.openlocfilehash: 1af23bfd46dd7d3781505473f7c1d86e65ea9bc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="get-started-with-relay-hybrid-connections"></a><span data-ttu-id="d9e0d-103">Introdução às Conexões Híbridas de Retransmissão</span><span class="sxs-lookup"><span data-stu-id="d9e0d-103">Get started with Relay Hybrid Connections</span></span>
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

<span data-ttu-id="d9e0d-104">Este tutorial fornece uma introdução às [Conexões Híbridas da Transmissão do Azure](relay-what-is-it.md#hybrid-connections) e mostra como usar o .NET para criar um aplicativo cliente que envia mensagens para um aplicativo ouvinte correspondente.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-104">This tutorial provides an introduction to [Azure Relay Hybrid Connections](relay-what-is-it.md#hybrid-connections), and shows how to use .NET to create a client application that sends messages to a corresponding listener application.</span></span> 

## <a name="what-will-be-accomplished"></a><span data-ttu-id="d9e0d-105">O que será realizado</span><span class="sxs-lookup"><span data-stu-id="d9e0d-105">What will be accomplished</span></span>
<span data-ttu-id="d9e0d-106">Como as Conexões Híbridas exigem um componente de cliente e de servidor, o tutorial cria dois aplicativos de console.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-106">Because Hybrid Connections requires both a client and a server component, the tutorial creates two console applications.</span></span> <span data-ttu-id="d9e0d-107">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="d9e0d-107">Here are the steps:</span></span>

1. <span data-ttu-id="d9e0d-108">Criar um namespace de retransmissão usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-108">Create a Relay namespace, using the Azure portal.</span></span>
2. <span data-ttu-id="d9e0d-109">Crie uma conexão híbrida no namespace usando o portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-109">Create a hybrid connection in that namespace, using the Azure portal.</span></span>
3. <span data-ttu-id="d9e0d-110">Escreva um aplicativo de console do servidor (ouvinte) para receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-110">Write a server (listener) console application to receive messages.</span></span>
4. <span data-ttu-id="d9e0d-111">Escreva um aplicativo de console de cliente (remetente) para enviar mensagens.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-111">Write a client (sender) console application to send messages.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9e0d-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d9e0d-112">Prerequisites</span></span>

<span data-ttu-id="d9e0d-113">Para concluir este tutorial, você precisará dos seguintes pré-requisitos:</span><span class="sxs-lookup"><span data-stu-id="d9e0d-113">To complete this tutorial, you'll need the following prerequisites:</span></span>

1. <span data-ttu-id="d9e0d-114">[Visual Studio 2015 ou superior](http://www.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="d9e0d-114">[Visual Studio 2015 or higher](http://www.visualstudio.com).</span></span> <span data-ttu-id="d9e0d-115">Os exemplos neste tutorial usam o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-115">The examples in this tutorial use Visual Studio 2017.</span></span>
2. <span data-ttu-id="d9e0d-116">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-116">An Azure subscription.</span></span>

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-the-azure-portal"></a><span data-ttu-id="d9e0d-117">1. Criar um namespace usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d9e0d-117">1. Create a namespace using the Azure portal</span></span>
<span data-ttu-id="d9e0d-118">Se você já tiver um namespace de Retransmissão criado, vá até a seção [Criar uma Conexão Híbrida usando o portal do Azure](#2-create-a-hybrid-connection-using-the-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="d9e0d-118">If you have already created a Relay namespace, jump to the [Create a hybrid connection using the Azure portal](#2-create-a-hybrid-connection-using-the-azure-portal) section.</span></span>

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-the-azure-portal"></a><span data-ttu-id="d9e0d-119">2. Criar uma conexão híbrida usando o portal do Azure</span><span class="sxs-lookup"><span data-stu-id="d9e0d-119">2. Create a hybrid connection using the Azure portal</span></span>
<span data-ttu-id="d9e0d-120">Se você já tiver criado uma conexão híbrida, vá até a seção [Criar um aplicativo de servidor](#3-create-a-server-application-listener).</span><span class="sxs-lookup"><span data-stu-id="d9e0d-120">If you have already created a hybrid connection, jump to the [Create a server application](#3-create-a-server-application-listener) section.</span></span>

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a><span data-ttu-id="d9e0d-121">3. Criar um aplicativo de servidor (escuta)</span><span class="sxs-lookup"><span data-stu-id="d9e0d-121">3. Create a server application (listener)</span></span>
<span data-ttu-id="d9e0d-122">Para escutar e receber mensagens da retransmissão, escreveremos um aplicativo de console em C# usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-122">To listen and receive messages from the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a><span data-ttu-id="d9e0d-123">4. Criar um aplicativo de cliente (remetente)</span><span class="sxs-lookup"><span data-stu-id="d9e0d-123">4. Create a client application (sender)</span></span>
<span data-ttu-id="d9e0d-124">Para enviar mensagens para a retransmissão, escreveremos um aplicativo de console em C# usando o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-124">To send messages to the Relay, we will write a C# console application using Visual Studio.</span></span>

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-the-applications"></a><span data-ttu-id="d9e0d-125">5. Executar os aplicativos</span><span class="sxs-lookup"><span data-stu-id="d9e0d-125">5. Run the applications</span></span>
1. <span data-ttu-id="d9e0d-126">Execute o aplicativo de servidor.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-126">Run the server application.</span></span>
2. <span data-ttu-id="d9e0d-127">Execute o aplicativo de cliente e insira algum texto.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-127">Run the client application and enter some text.</span></span>
3. <span data-ttu-id="d9e0d-128">Certifique-se de que o console do aplicativo de servidor exiba o texto inserido no aplicativo de cliente.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-128">Ensure that the server application console outputs the text that was entered in the client application.</span></span>

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

<span data-ttu-id="d9e0d-130">Parabéns, você criou um aplicativo de Conexões Híbridas completo.</span><span class="sxs-lookup"><span data-stu-id="d9e0d-130">Congratulations, you have created an end-to-end Hybrid Connections application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9e0d-131">Próximas etapas:</span><span class="sxs-lookup"><span data-stu-id="d9e0d-131">Next steps:</span></span>
* [<span data-ttu-id="d9e0d-132">Perguntas frequentes sobre retransmissão</span><span class="sxs-lookup"><span data-stu-id="d9e0d-132">Relay FAQ</span></span>](relay-faq.md)
* [<span data-ttu-id="d9e0d-133">Criar um namespace</span><span class="sxs-lookup"><span data-stu-id="d9e0d-133">Create a namespace</span></span>](relay-create-namespace-portal.md)
* [<span data-ttu-id="d9e0d-134">Introdução ao Node</span><span class="sxs-lookup"><span data-stu-id="d9e0d-134">Get started with Node</span></span>](relay-hybrid-connections-node-get-started.md)

