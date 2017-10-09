---
title: "aaaBacking backup de manifestos da unidade de importação/exportação do Azure | Microsoft Docs"
description: "Saiba como toohave sua unidade manifestos para serviço de importação/exportação do Microsoft Azure Olá passam por backup automaticamente."
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
ms.openlocfilehash: f48b97a2cce62714aace2b30a393305202c7ecd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="e5772-103">Fazendo backup de manifestos de unidade de trabalhos de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="e5772-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="e5772-104">Manifestos de unidade podem ser feitos backup tooblobs por configuração Olá `BackupDriveManifest` propriedade muito`true` em Olá [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operações da API REST.</span><span class="sxs-lookup"><span data-stu-id="e5772-104">Drive manifests can be automatically backed up tooblobs by setting hello `BackupDriveManifest` property too`true` in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="e5772-105">Por padrão, Olá manifestos de unidade sem backup.</span><span class="sxs-lookup"><span data-stu-id="e5772-105">By default, hello drive manifests are not backed up.</span></span> <span data-ttu-id="e5772-106">backups de manifesto da unidade Olá são armazenados como blobs de bloco em um contêiner na conta de armazenamento Olá associado ao trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="e5772-106">hello drive manifest backups are stored as block blobs in a container within hello storage account associated with hello job.</span></span> <span data-ttu-id="e5772-107">Por padrão, o nome do contêiner de saudação é `waimportexport`, mas você pode especificar um nome diferente na Olá `DiagnosticsPath` propriedade ao chamar hello `Put Job` ou `Update Job Properties` operações.</span><span class="sxs-lookup"><span data-stu-id="e5772-107">By default, hello container name is `waimportexport`, but you can specify a different name in hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="e5772-108">Olá blob do manifesto de backup são nomeados em Olá formato a seguir: `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="e5772-108">hello backup manifest blob are named in hello following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="e5772-109">Você pode recuperar Olá URI da unidade de backup Olá manifestos de um trabalho por chamada hello [obter trabalho](/rest/api/storageimportexport/jobs#Jobs_Get) operação.</span><span class="sxs-lookup"><span data-stu-id="e5772-109">You can retrieve hello URI of hello backup drive manifests for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="e5772-110">blob Olá URI é retornado no hello `ManifestUri` propriedade para cada unidade.</span><span class="sxs-lookup"><span data-stu-id="e5772-110">hello blob URI is returned in hello `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e5772-111">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e5772-111">Next steps</span></span>

* [<span data-ttu-id="e5772-112">Usando a API REST do serviço de importação/exportação Olá</span><span class="sxs-lookup"><span data-stu-id="e5772-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
