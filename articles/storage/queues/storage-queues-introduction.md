---
title: aaaIntroduction tooAzure armazenamento de fila | Microsoft Docs
description: "Introdução tooAzure armazenamento de fila"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: robinsh
ms.openlocfilehash: 669effedff7beedde8a119c350a2a70edafedcf0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooqueues"></a>Introdução tooQueues

Armazenamento de fila do Azure é um serviço para armazenar grandes quantidades de mensagens que podem ser acessadas de qualquer lugar Olá, mundo por meio de chamadas autenticadas usando HTTP ou HTTPS. Uma mensagem da fila única pode ser o too64 KB de tamanho e uma fila pode conter milhões de mensagens, o limite de capacidade total de toohello de uma conta de armazenamento.

## <a name="common-uses"></a>Usos comuns

Usos comuns de Armazenamento de filas incluem:

* Criando uma lista de pendências de trabalho tooprocess assincronamente
* Transmissão de mensagens de uma função de trabalho do Azure de tooan de função web do Azure

## <a name="queue-service-concepts"></a>Conceitos do serviço Fila

Olá serviço fila contém Olá componentes a seguir:

![Conceitos de fila](./media/storage-queues-introduction/queue1.png)

* **Formato de URL:** filas são acessadas usando Olá formato de URL a seguir:   
    http://`<storage account>`.queue.core.windows.net/`<queue>` 
  
    Olá URL a seguir aborda uma fila no diagrama de saudação:  
  
    `http://myaccount.queue.core.windows.net/images-to-download`

* **Conta de armazenamento:** todos os acessos tooAzure armazenamento é feito por meio de uma conta de armazenamento. Consulte [Escalabilidade e Metas de Desempenho do Armazenamento do Azure](../common/storage-scalability-targets.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json) para obter detalhes sobre a capacidade da conta de armazenamento.

* **Fila:** uma fila contém um conjunto de mensagens. Todas as mensagens devem estar em uma fila. Observe que nome de fila Olá deve ser todas minúscula. Para saber mais sobre filas de nomenclatura, confira [Nomenclatura de filas e metadados](https://msdn.microsoft.com/library/azure/dd179349.aspx).

* **Mensagem:** A mensagem, em qualquer formato de backup too64 KB. tempo máximo de saudação que uma mensagem pode permanecer na fila de saudação é de sete dias.

## <a name="next-steps"></a>Próximas etapas

* [Criar uma conta de armazenamento](../storage-create-storage-account.md?toc=%2fazure%2fstorage%2fqueues%2ftoc.json)
* [Introdução às filas usando .NET](storage-dotnet-how-to-use-queues.md)
