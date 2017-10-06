---
title: "AAA \"evento de início do lote do Azure pool delete | Microsoft Docs\""
description: "Referência para excluir um pool de lote evento inicial."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 79bb28bffc760a49cc0a95062f5086dc96c6a795
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-delete-start-event"></a>Evento inicial de exclusão de pool

 Esse evento é emitido quando uma operação de exclusão de pool é iniciada. Desde que a exclusão do pool de saudação é um evento assíncrono, você pode esperar um toobe de evento de conclusão de excluir pool emitido depois que a operação de exclusão de saudação for concluída.

 Olá, exemplo a seguir mostra Olá corpo de um evento de início de exclusão do pool.

```
{
    "id": "myPool1"
}
```

|Elemento|Tipo|Observações|
|-------------|----------|-----------|
|ID|Cadeia de caracteres|id de saudação do pool de saudação.|
