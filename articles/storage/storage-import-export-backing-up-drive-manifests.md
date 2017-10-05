---
title: "Fazendo backup de manifestos de unidade de Importação/Exportação do Azure | Microsoft Docs"
description: "Saiba como fazer backup automático dos manifestos da unidade do serviço de Importação/Exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 33eb8e1eea8f8aa7b79ef3e54f2b1ed88dc794ae
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="65123-103">Fazendo backup de manifestos de unidade de trabalhos de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="65123-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="65123-104">É possível fazer backup automático dos manifestos da unidade em blobs definindo a propriedade `BackupDriveManifest` como `true` nas operações de API REST [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update).</span><span class="sxs-lookup"><span data-stu-id="65123-104">Drive manifests can be automatically backed up to blobs by setting the `BackupDriveManifest` property to `true` in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="65123-105">Por padrão, não é feito o backup dos manifestos da unidade.</span><span class="sxs-lookup"><span data-stu-id="65123-105">By default, the drive manifests are not backed up.</span></span> <span data-ttu-id="65123-106">Os backups dos manifestos da unidade são armazenados como blobs de blocos em um contêiner na conta de armazenamento associada ao trabalho.</span><span class="sxs-lookup"><span data-stu-id="65123-106">The drive manifest backups are stored as block blobs in a container within the storage account associated with the job.</span></span> <span data-ttu-id="65123-107">Por padrão, o nome do contêiner é `waimportexport`, mas é possível especificar outro nome na propriedade `DiagnosticsPath` ao chamar as operações `Put Job` ou `Update Job Properties`.</span><span class="sxs-lookup"><span data-stu-id="65123-107">By default, the container name is `waimportexport`, but you can specify a different name in the `DiagnosticsPath` property when calling the `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="65123-108">O blob do manifesto do backup é nomeado no seguinte formato: `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="65123-108">The backup manifest blob are named in the following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="65123-109">É possível recuperar o URI dos manifestos da unidade de backup de um trabalho chamando a operação [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get).</span><span class="sxs-lookup"><span data-stu-id="65123-109">You can retrieve the URI of the backup drive manifests for a job by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="65123-110">O URI do blob é retornado na propriedade `ManifestUri` de cada unidade.</span><span class="sxs-lookup"><span data-stu-id="65123-110">The blob URI is returned in the `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="65123-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="65123-111">Next steps</span></span>

* [<span data-ttu-id="65123-112">Usando a API REST do serviço de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="65123-112">Using the Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
