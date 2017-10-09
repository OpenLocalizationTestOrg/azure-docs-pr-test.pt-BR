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
# <a name="get-started-with-relay-hybrid-connections"></a>Introdução às Conexões Híbridas de Retransmissão
[!INCLUDE [relay-selector-hybrid-connections](../../includes/relay-selector-hybrid-connections.md)]

Este tutorial fornece uma introdução muito[Azure retransmissão híbrida conexões](relay-what-is-it.md#hybrid-connections)e mostra como toouse .NET toocreate um aplicativo cliente que envia mensagens de aplicativo de escuta tooa correspondente. 

## <a name="what-will-be-accomplished"></a>O que será realizado
Como as conexões híbridas requer um cliente e um componente de servidor, o tutorial de saudação cria dois aplicativos de console. Aqui estão as etapas de saudação:

1. Crie um namespace de retransmissão, usando Olá portal do Azure.
2. Crie uma conexão híbrida no namespace, usando Olá portal do Azure.
3. Grave mensagens de tooreceive de aplicativo de um console do servidor (ouvinte).
4. Grave mensagens de toosend de aplicativo de um console de cliente (remetente).

## <a name="prerequisites"></a>Pré-requisitos

toocomplete neste tutorial, você precisará Olá pré-requisitos a seguir:

1. [Visual Studio 2015 ou superior](http://www.visualstudio.com). exemplos de saudação neste tutorial usam 2017 do Visual Studio.
2. Uma assinatura do Azure.

[!INCLUDE [create-account-note](../../includes/create-account-note.md)]

## <a name="1-create-a-namespace-using-hello-azure-portal"></a>1. Criar um namespace usando Olá portal do Azure
Se você já tiver criado um namespace de retransmissão, ir toohello [criar uma conexão híbrida usando Olá portal do Azure](#2-create-a-hybrid-connection-using-the-azure-portal) seção.

[!INCLUDE [relay-create-namespace-portal](../../includes/relay-create-namespace-portal.md)]

## <a name="2-create-a-hybrid-connection-using-hello-azure-portal"></a>2. Criar uma conexão híbrida usando Olá portal do Azure
Se você já tiver criado uma conexão híbrida, ir toohello [criar um aplicativo de servidor](#3-create-a-server-application-listener) seção.

[!INCLUDE [relay-create-hybrid-connection-portal](../../includes/relay-create-hybrid-connection-portal.md)]

## <a name="3-create-a-server-application-listener"></a>3. Criar um aplicativo de servidor (escuta)
toolisten e receber mensagens de saudação retransmissão, podemos irá escrever um aplicativo de console c# usando o Visual Studio.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-server](../../includes/relay-hybrid-connections-dotnet-get-started-server.md)]

## <a name="4-create-a-client-application-sender"></a>4. Criar um aplicativo de cliente (remetente)
toosend toohello de mensagens de retransmissão, que irá escrever um aplicativo de console c# usando o Visual Studio.

[!INCLUDE [relay-hybrid-connections-dotnet-get-started-client](../../includes/relay-hybrid-connections-dotnet-get-started-client.md)]

## <a name="5-run-hello-applications"></a>5. Executar aplicativos Olá
1. Execute o aplicativo de servidor de saudação.
2. Execute o aplicativo de cliente hello e digite algum texto.
3. Verifique se o servidor Olá aplicativo console saídas Olá texto inserido no aplicativo de cliente hello.

![running-applications](./media/relay-hybrid-connections-dotnet-get-started/running-applications.png)

Parabéns, você criou um aplicativo de Conexões Híbridas completo.

## <a name="next-steps"></a>Próximas etapas:
* [Perguntas frequentes sobre retransmissão](relay-faq.md)
* [Criar um namespace](relay-create-namespace-portal.md)
* [Introdução ao Node](relay-hybrid-connections-node-get-started.md)

