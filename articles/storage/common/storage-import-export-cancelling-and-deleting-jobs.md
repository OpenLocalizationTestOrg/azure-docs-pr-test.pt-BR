---
title: "aaaCancel e excluir um trabalho de importação/exportação do Azure | Microsoft Docs"
description: "Saiba como toocancel e excluir trabalhos para Olá serviço de importação/exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 13456a8e7652850baacb53730cc7bb1520b0a4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a>Cancelando e excluindo trabalhos de Importação/Exportação do Azure

 toorequest que um trabalho cancelado antes que ele está em Olá `Packaging` estado, chamada hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operação e conjunto Olá `CancelRequested` elemento muito`true`. Olá trabalho for cancelado em uma base de melhor esforço. Se as unidades estiverem no processo de saudação de transferência de dados, dados podem continuar toobe transferido mesmo depois que o cancelamento foi solicitado.

 Um trabalho cancelado é movido toohello `Completed` de estado e são mantidas por 90 dias, no ponto em que ele é excluído.

 toodelete um trabalho, chamada hello [excluir trabalho](/rest/api/storageimportexport/jobs#Jobs_Delete) operação antes que o trabalho Olá tiver sido enviado (ou seja, enquanto o trabalho de saudação estiver no hello `Creating` estado). Você também pode excluir um trabalho quando ele estiver em Olá `Completed` estado. Depois que um trabalho é excluído, suas informações e status não são mais acessíveis por meio da API REST de saudação ou Olá portal do Azure.

## <a name="next-steps"></a>Próximas etapas

* [Usando a API REST do serviço de importação/exportação Olá](storage-import-export-using-the-rest-api.md)
