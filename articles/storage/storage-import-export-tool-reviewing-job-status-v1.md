---
title: "Examinando o status do trabalho de Importação/Exportação do Azure — v1 | Microsoft Docs"
description: "Saiba como usar os arquivos de log criados durante a execução do trabalho de importação ou exportação para ver o status do trabalho de Importação/Exportação."
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
ms.openlocfilehash: 621e41df127fded6ec6fe1f71e86cb8630965a70
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="00d09-103">Examinando o Status do trabalho de Importação/Exportação do Azure com cópias de arquivos de log</span><span class="sxs-lookup"><span data-stu-id="00d09-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="00d09-104">Quando o serviço de Importação/Exportação do Microsoft Azure processa unidades associadas a um trabalho de importação ou exportação, ele grava arquivos de log de cópia na conta de armazenamento para a qual ou da qual os blobs estão sendo importados ou exportados.</span><span class="sxs-lookup"><span data-stu-id="00d09-104">When the Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files to the storage account to or from which you are importing or exporting blobs.</span></span> <span data-ttu-id="00d09-105">O arquivo de log contém o status detalhado sobre cada arquivo importado ou exportado.</span><span class="sxs-lookup"><span data-stu-id="00d09-105">The log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="00d09-106">A URL para cada arquivo de log de cópia é retornada ao consultar o status de um trabalho concluído; consulte [Get Job](/rest/api/storageservices/Get-Job3) (Obter Trabalho) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="00d09-106">The URL to each copy log file is returned when you query the status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="00d09-107">URLs de exemplo</span><span class="sxs-lookup"><span data-stu-id="00d09-107">Example URLs</span></span>

<span data-ttu-id="00d09-108">Estas são URLs de exemplo para arquivos de log de cópia de um trabalho de importação com duas unidades:</span><span class="sxs-lookup"><span data-stu-id="00d09-108">The following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="00d09-109">Confira [Formato de arquivo de log de serviço de Importação/Exportação](storage-import-export-file-format-log.md) para obter o formato dos logs de cópia e a lista completa de códigos de status.</span><span class="sxs-lookup"><span data-stu-id="00d09-109">See [Import/Export service Log File Format](storage-import-export-file-format-log.md) for the format of copy logs and the full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="00d09-110">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="00d09-110">Next steps</span></span>
 
 * [<span data-ttu-id="00d09-111">Configurando a Ferramenta de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="00d09-111">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="00d09-112">Preparação de discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="00d09-112">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="00d09-113">Reparação de um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="00d09-113">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="00d09-114">Reparação de um trabalho de exportação</span><span class="sxs-lookup"><span data-stu-id="00d09-114">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="00d09-115">Solucionando problemas da Ferramenta de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="00d09-115">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
