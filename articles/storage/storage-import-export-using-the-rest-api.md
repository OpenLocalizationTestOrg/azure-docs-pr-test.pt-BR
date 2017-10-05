---
title: "Usando a API REST do serviço de Importação/Exportação do Azure | Microsoft Docs"
description: "Saiba ais sobre como encontrar recursos para usar a API REST do serviço de Importação/Exportação do Azure, incluindo instruções e material de referência."
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
ms.openlocfilehash: e4f5ca289f4bd87574e448d37a1154b222f221f5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-importexport-service-rest-api"></a><span data-ttu-id="9d640-103">Usando a API REST do serviço de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="9d640-103">Using the Azure Import/Export service REST API</span></span>

<span data-ttu-id="9d640-104">O serviço de Importação/Exportação do Microsoft Azure expõe uma API REST para habilitar o controle programático de trabalhos de importação/exportação.</span><span class="sxs-lookup"><span data-stu-id="9d640-104">The Microsoft Azure Import/Export service exposes a REST API to enable programmatic control of import/export jobs.</span></span> <span data-ttu-id="9d640-105">É possível usar a API REST para executar todas as operações de importação/exportação que podem ser executadas com o [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="9d640-105">You can use the REST API to perform all of the import/export operations that you can perform with the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="9d640-106">Além disso, é possível usar a API REST para executar determinadas operações granulares, como consulta do percentual de conclusão de um trabalho, que não estão disponíveis atualmente no portal clássico.</span><span class="sxs-lookup"><span data-stu-id="9d640-106">Additionally, you can use the REST API to perform certain granular operations, such as querying the percentage completion of a job, which are not currently available in the classic portal.</span></span>

<span data-ttu-id="9d640-107">Consulte [Usar o serviço de Importação/Exportação do Microsoft Azure para transferir dados para o Armazenamento de Blobs](storage-import-export-service.md) para obter uma visão geral do serviço de Importação/Exportação e um tutorial que demonstra como usar o portal clássico para criar e gerenciar trabalhos de importação e exportação.</span><span class="sxs-lookup"><span data-stu-id="9d640-107">See [Using the Microsoft Azure Import/Export service to Transfer Data to Blob Storage](storage-import-export-service.md) for an overview of the Import/Export service and a tutorial that demonstrates how to use the classic portal to create and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="9d640-108">Pontos de extremidade de serviço</span><span class="sxs-lookup"><span data-stu-id="9d640-108">Service endpoints</span></span>

<span data-ttu-id="9d640-109">O serviço de Importação/Exportação do Azure é um provedor de recursos para o Azure Resource Manager e fornece um conjunto de APIs REST no seguinte ponto de extremidade HTTPS para o gerenciamento de trabalhos de importação/exportação:</span><span class="sxs-lookup"><span data-stu-id="9d640-109">The Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at the following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="9d640-110">Controle de versão</span><span class="sxs-lookup"><span data-stu-id="9d640-110">Versioning</span></span>

<span data-ttu-id="9d640-111">As solicitações para o serviço de Importação/Exportação devem especificar o parâmetro `api-version` e definir seu valor como `2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="9d640-111">Requests to the Import/Export service must specify the `api-version` parameter and set its value to `2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="9d640-112">Operações do serviço de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="9d640-112">Import/Export service operations</span></span>

[<span data-ttu-id="9d640-113">Criação de um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="9d640-113">Creating an import job</span></span>](storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="9d640-114">Criação de um trabalho de exportação</span><span class="sxs-lookup"><span data-stu-id="9d640-114">Creating an export job</span></span>](storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="9d640-115">Recuperação de informações de estado para um trabalho</span><span class="sxs-lookup"><span data-stu-id="9d640-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="9d640-116">Enumeração de trabalhos</span><span class="sxs-lookup"><span data-stu-id="9d640-116">Enumerating jobs</span></span>](storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="9d640-117">Cancelamento e exclusão de trabalhos</span><span class="sxs-lookup"><span data-stu-id="9d640-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="9d640-118">Backup de manifestos da unidade</span><span class="sxs-lookup"><span data-stu-id="9d640-118">Backing Up drive manifests</span></span>](storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="9d640-119">Diagnóstico e recuperação de erro para trabalhos de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="9d640-119">Diagnostics and error recovery for Import/Export jobs</span></span>](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="9d640-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9d640-120">Next steps</span></span>

* [<span data-ttu-id="9d640-121">Referência de REST de Importação/Exportação do Armazenamento</span><span class="sxs-lookup"><span data-stu-id="9d640-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
