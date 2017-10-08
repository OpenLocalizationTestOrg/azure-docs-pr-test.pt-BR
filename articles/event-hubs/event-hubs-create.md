---
title: aaaCreate um hub de eventos do Azure | Microsoft Docs
description: "Criar um namespace de Hubs de eventos do Azure e um hub de eventos usando Olá portal do Azure"
services: event-hubs
documentationcenter: na
author: sethmanheim
manager: timlt
editor: 
ms.assetid: ff99e327-c8db-4354-9040-9c60c51a2191
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/01/2017
ms.author: sethm
ms.openlocfilehash: 9a8b7711e2ca7d112e24be19353d43c365ff6935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-and-an-event-hub-using-hello-azure-portal"></a>Criar um namespace de Hubs de eventos e um hub de eventos usando Olá portal do Azure

## <a name="create-an-event-hubs-namespace"></a>Criar um namespace de Hubs de Eventos
1. Faça logon no toohello [portal do Azure][Azure portal]e clique em **novo** em Olá superior esquerda da tela hello.
1. Clique em **Internet das Coisas** e, em seguida, clique em **Hubs de Eventos**.
   
    ![](./media/event-hubs-create/create-event-hub9.png)
1. Em Olá **criar namespace** folha, insira um nome de namespace. sistema de saudação imediatamente verifica toosee se Olá nome está disponível.
   
    ![](./media/event-hubs-create/create-event-hub1.png)
1. Depois de fazer o nome do namespace Olá-se de que está disponível, escolha Olá preço (básico ou padrão). Além disso, escolha uma assinatura do Azure, o grupo de recursos e o local no qual recurso de saudação toocreate. 
1. Clique em **criar** toocreate Olá namespace. Você pode ter toowait alguns minutos Olá toofully provisionar Olá para recursos do sistema.
2. Na lista de portal de saudação de namespaces, clique Olá recém-criado namespace.
2. Clique em **Políticas de acesso compartilhado** e, em seguida, clique em **RootManageSharedAccessKey**.
    
    ![](./media/event-hubs-create/create-event-hub7.png)

3. Clique em Olá Olá de toocopy do botão de cópia **RootManageSharedAccessKey** transferência de toohello de cadeia de caracteres de conexão. Salve esta cadeia de caracteres de conexão em um local temporário, como o bloco de notas, toouse mais tarde.
    
    ![](./media/event-hubs-create/create-event-hub8.png)

## <a name="create-an-event-hub"></a>Criar um Hub de Evento

1. Na lista de namespace de Hubs de eventos Olá, clique em namespace Olá recém-criado.      
   
    ![](./media/event-hubs-create/create-event-hub2.png) 

2. Na folha de namespace hello, clique em **Hubs de eventos**.
   
    ![](./media/event-hubs-create/create-event-hub3.png)

1. Na parte superior de saudação da folha de saudação, clique em **adicionar Hub de eventos**.
   
    ![](./media/event-hubs-create/create-event-hub4.png)
1. Digite um nome para seu hub de eventos e clique em **Criar**.
   
    ![](./media/event-hubs-create/create-event-hub5.png)

O hub de eventos é criado, e você tem Olá cadeias de conexão necessárias toosend e receber eventos.

## <a name="next-steps"></a>Próximas etapas
toolearn mais sobre Hubs de eventos, consulte estes links:

* [Visão Geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Visão geral de API de Hubs de Eventos](event-hubs-api-overview.md)

[Azure portal]: https://portal.azure.com/