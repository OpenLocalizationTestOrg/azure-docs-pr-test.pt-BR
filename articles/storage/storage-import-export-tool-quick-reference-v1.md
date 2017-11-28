---
title: "Referência rápida de comandos para trabalhos de importação da Ferramenta de Importação/Exportação do Azure — v1 | Microsoft Docs"
description: "Referência de comandos da Ferramenta de Importação/Exportação do Azure para comandos de trabalho de importação usados com frequência. Este documento refere-se à v1 da Ferramenta de Importação/Exportação."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 47f450ee87dac3db2ccf7659928d52a6330a5697
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="219d2-104">Referência rápida de comandos usados com frequência para trabalhos de importação</span><span class="sxs-lookup"><span data-stu-id="219d2-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="219d2-105">Esta seção fornece uma referência rápida de alguns comandos usados com frequência.</span><span class="sxs-lookup"><span data-stu-id="219d2-105">This section provides a quick references for some frequently used commands.</span></span> <span data-ttu-id="219d2-106">Para obter o uso detalhado, consulte [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparando os discos rígidos para um trabalho de importação).</span><span class="sxs-lookup"><span data-stu-id="219d2-106">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-the-disks-when-data-already-copied-to-the-disks"></a><span data-ttu-id="219d2-107">Preparar os discos quando os dados já foram copiados para os discos</span><span class="sxs-lookup"><span data-stu-id="219d2-107">Prepare the disks when data already copied to the disks</span></span>
 <span data-ttu-id="219d2-108">Este é um comando de exemplo para preparar um disco quando os dados já foram copiados para o disco rígido que ainda não foi criptografado com o BitLocker:</span><span class="sxs-lookup"><span data-stu-id="219d2-108">Here is a sample command to prepare a disks when data already copied to the hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-to-a-hard-drive"></a><span data-ttu-id="219d2-109">Copiar um único diretório para um disco rígido</span><span class="sxs-lookup"><span data-stu-id="219d2-109">Copy a single directory to a hard drive</span></span>  
 <span data-ttu-id="219d2-110">Este é um comando de exemplo para copiar um único diretório de origem para um disco rígido que ainda não foi criptografado com o BitLocker:</span><span class="sxs-lookup"><span data-stu-id="219d2-110">Here is a sample command to copy a single source directory to a hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-to-a-hard-drive"></a><span data-ttu-id="219d2-111">Copiar dois diretórios para um disco rígido</span><span class="sxs-lookup"><span data-stu-id="219d2-111">Copy wwo directories to a hard drive</span></span>  
 <span data-ttu-id="219d2-112">Para copiar dois diretórios de origem para uma unidade, você precisará de dois comandos.</span><span class="sxs-lookup"><span data-stu-id="219d2-112">To copy two source directories to a drive, you will need two commands.</span></span>  
  
 <span data-ttu-id="219d2-113">O primeiro comando especifica o diretório de log, a chave de conta de armazenamento, a letra da unidade de destino e os requisitos de `format/encrypt`, além dos parâmetros comuns:</span><span class="sxs-lookup"><span data-stu-id="219d2-113">The first command specifies the log directory, storage account key, target drive letter and `format/encrypt` requirements, in addition to the common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="219d2-114">O segundo comando especifica o arquivo de diário, uma nova ID de sessão e as localizações de origem e de destino:</span><span class="sxs-lookup"><span data-stu-id="219d2-114">The second command specifies the journal file, a new session ID, and the source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-to-a-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="219d2-115">Copiar um arquivo grande para um disco rígido em uma segunda sessão de cópia</span><span class="sxs-lookup"><span data-stu-id="219d2-115">Copy a large file to a hard drive in a second copy session</span></span>  
 <span data-ttu-id="219d2-116">Este é um comando de exemplo que copia um único arquivo grande para uma unidade que foi preparada em uma sessão de cópia anterior:</span><span class="sxs-lookup"><span data-stu-id="219d2-116">Here is a sample command that copies a single large file to a drive that has been prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="219d2-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="219d2-117">Next steps</span></span>

* [<span data-ttu-id="219d2-118">Fluxo de trabalho de exemplo para preparar discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="219d2-118">Sample workflow to prepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
