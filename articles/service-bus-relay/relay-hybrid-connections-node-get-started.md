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
# <a name="get-started-with-relay-hybrid-connections"></a>Introdução às Conexões Híbridas de Retransmissão

[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Este tutorial fornece uma introdução muito[Azure retransmissão híbrida conexões](relay-what-is-it.md#hybrid-connections)e mostra como toouse Node. js toocreate um aplicativo cliente que envia mensagens de aplicativo de escuta tooa correspondente. 

## <a name="what-will-be-accomplished"></a>O que será realizado

Como as Conexões Híbridas exigem um componente de cliente e de servidor, criaremos dois aplicativos de console neste tutorial. Aqui estão as etapas de saudação:

1. Crie um namespace de retransmissão, usando Olá portal do Azure.
2. Crie uma conexão híbrida, usando Olá portal do Azure.
3. Grave um servidor de mensagens de tooreceive do aplicativo de console.
4. Grave um cliente de mensagens de toosend do aplicativo de console.

## <a name="prerequisites"></a>Pré-requisitos

1. [Node.js](https://nodejs.org/en/).
2. Uma assinatura do Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Criar um namespace usando Olá portal do Azure

Se você já tiver criado um namespace de retransmissão, ir toohello [criar uma conexão híbrida usando Olá portal do Azure](#2-create-a-hybrid-connection-using-the-azure-portal) seção.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Criar uma conexão híbrida usando Olá portal do Azure

Se você já tiver uma conexão híbrida criada, ir toohello [criar um aplicativo de servidor](#3-create-a-server-application-listener) seção.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Criar um aplicativo de servidor (escuta)

toolisten e receber mensagens de saudação retransmissão, irá escrever um aplicativo de console Node. js.

[!INCLUDE [relay-hybrid-connections-node-get-started-server](../../includes/relay-hybrid-connections-node-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Criar um aplicativo de cliente (remetente)

toosend mensagens toohello retransmissão, irá escrever um aplicativo de console Node. js.

[!INCLUDE [relay-hybrid-connections-node-get-started-client](../../includes/relay-hybrid-connections-node-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Executar aplicativos Olá

1. Execute o aplicativo de servidor hello: de um tipo de prompt de comando de Node. js `node listener.js`.
2. Execute o aplicativo de cliente hello: de um tipo de prompt de comando de Node. js `node sender.js`e digite algum texto.
3. Verifique se o servidor Olá aplicativo console saídas Olá texto inserido no aplicativo de cliente hello.

![running-applications](./media/relay-hybrid-connections-node-get-started/running-applications.png)

Parabéns, você criou um aplicativo de Conexões Híbridas de ponta a ponta usando o Node.js!

## <a name="next-steps"></a>Próximas etapas:

* [Perguntas frequentes sobre retransmissão](relay-faq.md)
* [Criar um namespace](relay-create-namespace-portal.md)
* [Introdução ao .NET](relay-hybrid-connections-dotnet-get-started.md)
* [Introdução ao Node](relay-hybrid-connections-node-get-started.md)

