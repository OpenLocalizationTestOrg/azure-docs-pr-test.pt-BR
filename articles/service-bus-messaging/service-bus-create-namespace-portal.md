---
title: "aaaHow toocreate um namespace de barramento de serviço no portal do Azure de saudação | Microsoft Docs"
description: "Crie um namespace de barramento de serviço usando Olá portal do Azure."
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: fbb10e62-b133-4851-9d27-40bd844db3ba
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: get-started-article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/27/2017
ms.author: sethm
ms.openlocfilehash: d8907e7e4a804056f6d66d5a177d9ace967ed2ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-hello-azure-portal"></a>Criar um namespace de barramento de serviço usando Olá portal do Azure

Um namespace é um contêiner de escopo para todos os componentes de mensagem. Várias filas e tópicos podem residir em um único namespace e os namespaces geralmente servem como contêineres de aplicativos. Há duas maneiras diferentes toocreate um namespace de barramento de serviço:

1. Portal do Azure (este artigo)
2. [Modelos do Gerenciador de Recursos][create-namespace-using-arm]

## <a name="create-a-namespace-in-hello-azure-portal"></a>Criar um namespace no hello portal do Azure

[!INCLUDE [service-bus-create-namespace-portal](../../includes/service-bus-create-namespace-portal.md)]

Parabéns! Agora você criou um namespace Mensagens do Barramento de Serviço.

## <a name="next-steps"></a>Próximas etapas

Confira nosso [GitHub exemplos][github-samples], que mostram algumas das hello mais avançados recursos de mensagens do barramento de serviço do Azure.

[create-namespace-using-arm]: service-bus-resource-manager-overview.md
[github-samples]: https://github.com/Azure/azure-service-bus/tree/master/samples
