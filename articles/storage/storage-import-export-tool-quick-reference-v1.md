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
ms.openlocfilehash: e36f065e5d23268758cf6b6db9428fe8a8e1056d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="53460-104">Referência rápida de comandos usados com frequência para trabalhos de importação</span><span class="sxs-lookup"><span data-stu-id="53460-104">Quick reference for frequently used commands for import jobs</span></span>
<span data-ttu-id="53460-105">Esta seção fornece uma referência rápida de alguns comandos usados com frequência.</span><span class="sxs-lookup"><span data-stu-id="53460-105">This section provides a quick references for some frequently used commands.</span></span> <span data-ttu-id="53460-106">Para obter o uso detalhado, consulte [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) (Preparando os discos rígidos para um trabalho de importação).</span><span class="sxs-lookup"><span data-stu-id="53460-106">For detailed usage, see [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md).</span></span>  

## <a name="prepare-hello-disks-when-data-already-copied-toohello-disks"></a><span data-ttu-id="53460-107">Preparar discos hello quando os dados copiados já toohello discos</span><span class="sxs-lookup"><span data-stu-id="53460-107">Prepare hello disks when data already copied toohello disks</span></span>
 <span data-ttu-id="53460-108">Aqui está um tooprepare do comando de exemplo um discos quando os dados copiados já toohello disco rígido que não tenha sido criptografado com o BitLocker:</span><span class="sxs-lookup"><span data-stu-id="53460-108">Here is a sample command tooprepare a disks when data already copied toohello hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a><span data-ttu-id="53460-109">Copiar um único diretório tooa disco rígido</span><span class="sxs-lookup"><span data-stu-id="53460-109">Copy a single directory tooa hard drive</span></span>  
 <span data-ttu-id="53460-110">Aqui está um toocopy do comando de exemplo da fonte de um único diretório tooa disco rígido que não tenha sido criptografado com o BitLocker:</span><span class="sxs-lookup"><span data-stu-id="53460-110">Here is a sample command toocopy a single source directory tooa hard drive that hasn't been yet been encrypted with BitLocker:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-tooa-hard-drive"></a><span data-ttu-id="53460-111">Copie a unidade de disco rígido wwo diretórios tooa</span><span class="sxs-lookup"><span data-stu-id="53460-111">Copy wwo directories tooa hard drive</span></span>  
 <span data-ttu-id="53460-112">toocopy dois diretórios tooa unidade de origem, você precisará de dois comandos.</span><span class="sxs-lookup"><span data-stu-id="53460-112">toocopy two source directories tooa drive, you will need two commands.</span></span>  
  
 <span data-ttu-id="53460-113">Olá primeiro comando Especifica o diretório de log hello, chave de conta de armazenamento, letra de unidade de destino e `format/encrypt` requisitos de parâmetros comuns de toohello de adição:</span><span class="sxs-lookup"><span data-stu-id="53460-113">hello first command specifies hello log directory, storage account key, target drive letter and `format/encrypt` requirements, in addition toohello common parameters:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 <span data-ttu-id="53460-114">Olá segundo comando Especifica o arquivo de diário hello, uma nova ID de sessão e locais de origem e destino hello:</span><span class="sxs-lookup"><span data-stu-id="53460-114">hello second command specifies hello journal file, a new session ID, and hello source and destination locations:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a><span data-ttu-id="53460-115">Copiar um arquivo grande tooa disco rígido em uma segunda sessão de cópia</span><span class="sxs-lookup"><span data-stu-id="53460-115">Copy a large file tooa hard drive in a second copy session</span></span>  
 <span data-ttu-id="53460-116">Aqui está um exemplo de comando que copia uma unidade de tooa único arquivo grande que tenha sido preparada em uma sessão de cópia anterior:</span><span class="sxs-lookup"><span data-stu-id="53460-116">Here is a sample command that copies a single large file tooa drive that has been prepared in a previous copy session:</span></span>  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a><span data-ttu-id="53460-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="53460-117">Next steps</span></span>

* [<span data-ttu-id="53460-118">Discos rígidos de tooprepare do fluxo de trabalho de exemplo para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="53460-118">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
