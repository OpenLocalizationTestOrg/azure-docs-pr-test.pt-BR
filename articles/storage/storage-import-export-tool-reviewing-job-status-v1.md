---
title: "aaaReviewing status do trabalho de importação/exportação do Azure - v1 | Microsoft Docs"
description: "Saiba como arquivos de log de Olá de toouse criados quando Olá importar ou exportar trabalho foi executado toosee status de saudação do trabalho de importação/exportação de saudação."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 378bc9a7ef6bfe65209413c8c4134f313a2c0d79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="c0217-103">Examinando o Status do trabalho de Importação/Exportação do Azure com cópias de arquivos de log</span><span class="sxs-lookup"><span data-stu-id="c0217-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="c0217-104">Quando Olá serviço de importação/exportação do Microsoft Azure processa unidades associadas a um trabalho de importação ou exportação, ele grava cópia log arquivos toohello armazenamento conta tooor do qual você estiver importando ou exportando blobs.</span><span class="sxs-lookup"><span data-stu-id="c0217-104">When hello Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files toohello storage account tooor from which you are importing or exporting blobs.</span></span> <span data-ttu-id="c0217-105">o arquivo de log Olá contém o status detalhado sobre cada arquivo que foi importado ou exportado.</span><span class="sxs-lookup"><span data-stu-id="c0217-105">hello log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="c0217-106">o arquivo de log de cópia do Hello URL tooeach é retornado quando você consulta o status de saudação de um trabalho concluído; consulte [obter trabalho](/rest/api/storageservices/Get-Job3) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="c0217-106">hello URL tooeach copy log file is returned when you query hello status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="c0217-107">URLs de exemplo</span><span class="sxs-lookup"><span data-stu-id="c0217-107">Example URLs</span></span>

<span data-ttu-id="c0217-108">Olá seguem URLs de exemplo para copiar arquivos de log para um trabalho de importação com duas unidades:</span><span class="sxs-lookup"><span data-stu-id="c0217-108">hello following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="c0217-109">Consulte [formato de arquivo de Log do serviço de importação/exportação](storage-import-export-file-format-log.md) para formato de saudação dos logs de cópia e a lista completa de saudação dos códigos de status.</span><span class="sxs-lookup"><span data-stu-id="c0217-109">See [Import/Export service Log File Format](storage-import-export-file-format-log.md) for hello format of copy logs and hello full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="c0217-110">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c0217-110">Next steps</span></span>
 
 * [<span data-ttu-id="c0217-111">Configurando Olá ferramenta de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="c0217-111">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="c0217-112">Preparação de discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="c0217-112">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="c0217-113">Reparação de um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="c0217-113">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="c0217-114">Reparação de um trabalho de exportação</span><span class="sxs-lookup"><span data-stu-id="c0217-114">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="c0217-115">Olá, ferramenta de importação/exportação do Azure de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="c0217-115">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
