---
title: "referência de aaaQuick para comandos de trabalho de importação da ferramenta de importação/exportação do Azure - v1 | Microsoft Docs"
description: "Referência de comandos da Ferramenta de Importação/Exportação do Azure para comandos de trabalho de importação usados com frequência. Isso se refere a toov1 de Olá, ferramenta de importação/exportação."
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
ms.openlocfilehash: 945eb4f9eff28c92ec963585d27cba73a7eb59bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="bf3f9-104">Referência rápida de comandos usados com frequência para trabalhos de importação</span><span class="sxs-lookup"><span data-stu-id="bf3f9-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="bf3f9-105">Esta seção fornece uma referência rápida de alguns comandos usados com frequência.</span><span class="sxs-lookup"><span data-stu-id="bf3f9-105">This section provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="bf3f9-106">Para obter o uso detalhado, consulte [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparando os discos rígidos para um trabalho de importação).</span><span class="sxs-lookup"><span data-stu-id="bf3f9-106">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-a-hard-drive-when-data-has-already-been-copied-toohello-hard-drive"></a><span data-ttu-id="bf3f9-107">Preparar um disco rígido, quando os dados já foram copiados toohello disco rígido</span><span class="sxs-lookup"><span data-stu-id="bf3f9-107">Prepare a hard drive when data has already been copied toohello hard drive</span></span>
 <span data-ttu-id="bf3f9-108">Olá comando a seguir prepara um disco rígido, quando os dados já foi copiado tooit, mas ainda não tem sido criptografados com o BitLocker:</span><span class="sxs-lookup"><span data-stu-id="bf3f9-108">hello following command prepares a hard drive when data has already been copied tooit, but has not yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="bf3f9-109">Copiar um único diretório tooa disco rígido</span><span class="sxs-lookup"><span data-stu-id="bf3f9-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="bf3f9-110">saudação de comando a seguir copia um único diretório tooa disco rígido de origem que ainda não tiver sido criptografado com o BitLocker:</span><span class="sxs-lookup"><span data-stu-id="bf3f9-110">hello following command copies a single source directory tooa hard drive that has not yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-two-directories-tooa-hard-drive"></a><span data-ttu-id="bf3f9-111">Copiar dois diretórios tooa disco rígido</span><span class="sxs-lookup"><span data-stu-id="bf3f9-111">Copy two directories tooa hard drive</span></span>  
 <span data-ttu-id="bf3f9-112">unidade de tooa de diretórios de origem toocopy dois, Olá use comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="bf3f9-112">toocopy two source directories tooa drive, use hello following commands:</span></span>  
  
 <span data-ttu-id="bf3f9-113">Olá primeiro comando Especifica o diretório de log hello, chave de conta de armazenamento, letra de unidade de destino, `format/encrypt` requisitos e parâmetros comuns:</span><span class="sxs-lookup"><span data-stu-id="bf3f9-113">hello first command specifies hello log directory, storage account key, target drive letter, `format/encrypt` requirements, and common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="bf3f9-114">Olá segundo comando Especifica o arquivo de diário hello, uma nova ID de sessão e locais de origem e destino hello:</span><span class="sxs-lookup"><span data-stu-id="bf3f9-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="bf3f9-115">Copiar um arquivo grande tooa disco rígido em uma segunda sessão de cópia</span><span class="sxs-lookup"><span data-stu-id="bf3f9-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="bf3f9-116">saudação de comando a seguir copia um único arquivo grande tooa disco rígido que foi preparado em uma sessão de cópia anterior:</span><span class="sxs-lookup"><span data-stu-id="bf3f9-116">hello following command copies a single large file tooa hard drive that was prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="bf3f9-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bf3f9-117">Next steps</span></span>

* [<span data-ttu-id="bf3f9-118">Discos rígidos de tooprepare do fluxo de trabalho de exemplo para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="bf3f9-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
