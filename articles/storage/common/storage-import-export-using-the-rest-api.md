---
title: "Olá aaaUsing API REST do serviço de importação/exportação do Azure | Microsoft Docs"
description: "Saiba onde toofind recursos para usar o hello importação/exportação do Azure serviço API de REST, incluindo ambos os materiais de referência como tooand."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: fc7e1007ad632cf6f771c2545644f8de43c8f181
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a>Usando a API REST do serviço de importação/exportação do Azure Olá

Olá serviço de importação/exportação do Microsoft Azure expõe um controle programático de tooenable API REST de trabalhos de importação/exportação. Você pode usar a API REST de saudação tooperform todos Olá operações que podem ser executadas com hello importação/exportação [portal do Azure](https://portal.azure.com/). Além disso, você pode usar Olá API REST tooperform determinadas operações granulares, como consultar a porcentagem de conclusão de saudação de um trabalho, que não está disponível atualmente no hello portal clássico do Azure.

Consulte [usando Olá importação/exportação do Microsoft Azure serviço tooTransfer dados tooBlob armazenamento](../storage-import-export-service.md) para obter uma visão geral do serviço de importação/exportação do hello e um tutorial que demonstra como toouse Olá toocreate portal clássico e gerenciar a importação e trabalhos de exportação.

## <a name="service-endpoints"></a>Pontos de extremidade de serviço

Olá serviço de importação/exportação do Azure é um provedor de recursos para o Gerenciador de recursos do Azure e fornece um conjunto de APIs REST em Olá ponto de extremidade HTTPS para gerenciar trabalhos de importação/exportação a seguir:

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a>Controle de versão

Solicitações toohello serviço de importação/exportação deve especificar Olá `api-version` parâmetro e defina seu valor muito`2016-11-01`.

## <a name="importexport-service-operations"></a>Operações do serviço de Importação/Exportação

[Criação de um trabalho de importação](../storage-import-export-creating-an-import-job.md)

[Criação de um trabalho de exportação](../storage-import-export-creating-an-export-job.md)

[Recuperação de informações de estado para um trabalho](storage-import-export-retrieving-state-info-for-a-job.md)

[Enumeração de trabalhos](../storage-import-export-enumerating-jobs.md)

[Cancelamento e exclusão de trabalhos](storage-import-export-cancelling-and-deleting-jobs.md)

[Backup de manifestos da unidade](../storage-import-export-backing-up-drive-manifests.md)

[Diagnóstico e recuperação de erro para trabalhos de Importação/Exportação](../storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a>Próximas etapas

* [Referência de REST de Importação/Exportação do Armazenamento](/rest/api/storageimportexport)
