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
ms.openlocfilehash: a01c170b1bc9c2b2ce9086d39de78a39fafb2c8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a><span data-ttu-id="931a9-103">Usando a API REST do serviço de importação/exportação do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="931a9-103">Using hello Azure Import/Export service REST API</span></span>

<span data-ttu-id="931a9-104">Olá serviço de importação/exportação do Microsoft Azure expõe um controle programático de tooenable API REST de trabalhos de importação/exportação.</span><span class="sxs-lookup"><span data-stu-id="931a9-104">hello Microsoft Azure Import/Export service exposes a REST API tooenable programmatic control of import/export jobs.</span></span> <span data-ttu-id="931a9-105">Você pode usar a API REST de saudação tooperform todos Olá operações que podem ser executadas com hello importação/exportação [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="931a9-105">You can use hello REST API tooperform all of hello import/export operations that you can perform with hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="931a9-106">Além disso, você pode usar Olá API REST tooperform determinadas operações granulares, como consultar a porcentagem de conclusão de saudação de um trabalho, que não estão disponíveis no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="931a9-106">Additionally, you can use hello REST API tooperform certain granular operations, such as querying hello percentage completion of a job, which are not currently available in hello classic portal.</span></span>

<span data-ttu-id="931a9-107">Consulte [usando Olá importação/exportação do Microsoft Azure serviço tooTransfer dados tooBlob armazenamento](storage-import-export-service.md) para obter uma visão geral do serviço de importação/exportação do hello e um tutorial que demonstra como toouse Olá toocreate portal clássico e gerenciar a importação e trabalhos de exportação.</span><span class="sxs-lookup"><span data-stu-id="931a9-107">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello classic portal toocreate and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="931a9-108">Pontos de extremidade de serviço</span><span class="sxs-lookup"><span data-stu-id="931a9-108">Service endpoints</span></span>

<span data-ttu-id="931a9-109">Olá serviço de importação/exportação do Azure é um provedor de recursos para o Gerenciador de recursos do Azure e fornece um conjunto de APIs REST em Olá ponto de extremidade HTTPS para gerenciar trabalhos de importação/exportação a seguir:</span><span class="sxs-lookup"><span data-stu-id="931a9-109">hello Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at hello following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="931a9-110">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="931a9-110">Versioning</span></span>

<span data-ttu-id="931a9-111">Solicitações toohello serviço de importação/exportação deve especificar Olá `api-version` parâmetro e defina seu valor muito`2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="931a9-111">Requests toohello Import/Export service must specify hello `api-version` parameter and set its value too`2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="931a9-112">Operações do serviço de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="931a9-112">Import/Export service operations</span></span>

[<span data-ttu-id="931a9-113">Criação de um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="931a9-113">Creating an import job</span></span>](storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="931a9-114">Criação de um trabalho de exportação</span><span class="sxs-lookup"><span data-stu-id="931a9-114">Creating an export job</span></span>](storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="931a9-115">Recuperação de informações de estado para um trabalho</span><span class="sxs-lookup"><span data-stu-id="931a9-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="931a9-116">Enumeração de trabalhos</span><span class="sxs-lookup"><span data-stu-id="931a9-116">Enumerating jobs</span></span>](storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="931a9-117">Cancelamento e exclusão de trabalhos</span><span class="sxs-lookup"><span data-stu-id="931a9-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="931a9-118">Backup de manifestos da unidade</span><span class="sxs-lookup"><span data-stu-id="931a9-118">Backing Up drive manifests</span></span>](storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="931a9-119">Diagnóstico e recuperação de erro para trabalhos de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="931a9-119">Diagnostics and error recovery for Import/Export jobs</span></span>](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="931a9-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="931a9-120">Next steps</span></span>

* [<span data-ttu-id="931a9-121">Referência de REST de Importação/Exportação do Armazenamento</span><span class="sxs-lookup"><span data-stu-id="931a9-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
