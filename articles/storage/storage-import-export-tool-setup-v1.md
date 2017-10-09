---
title: "aaaSetting backup Olá v1 da ferramenta de importação/exportação do Azure | Microsoft Docs"
description: "Saiba como tooset backup Olá conduzem a preparação e a ferramenta de reparo para o serviço de importação/exportação do Azure hello. Isso se refere a toov1 de Olá, ferramenta de importação/exportação."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c312b1ab-5b9e-4d24-becd-790a88b3ba8d
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 4a737f2d2d0b1d00057e7fed6f9cf7b58e555b23
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-up-hello-azure-importexport-tool"></a><span data-ttu-id="a0a58-104">Configurando Olá, ferramenta de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="a0a58-104">Setting up hello Azure Import/Export Tool</span></span>
<span data-ttu-id="a0a58-105">Olá, ferramenta de importação/exportação do Microsoft Azure é a ferramenta de reparo que você pode usar com hello serviço de importação/exportação do Microsoft Azure e preparação da unidade Olá.</span><span class="sxs-lookup"><span data-stu-id="a0a58-105">hello Microsoft Azure Import/Export Tool is hello drive preparation and repair tool that you can use with hello Microsoft Azure Import/Export service.</span></span> <span data-ttu-id="a0a58-106">Você pode usar a ferramenta de saudação para Olá funções a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0a58-106">You can use hello tool for hello following functions:</span></span>  
  
-   <span data-ttu-id="a0a58-107">Antes de criar um trabalho de importação, você pode usar essa ferramenta toocopy dados toohello unidades de disco rígido for Centro de dados tooship tooa do Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="a0a58-107">Before creating an import job, you can use this tool toocopy data toohello hard drives you are going tooship tooa Windows Azure data center.</span></span>  
  
-   <span data-ttu-id="a0a58-108">Depois que um trabalho de importação for concluída, você pode usar essa ferramenta toorepair todos os blobs que foram corrompidos, estavam ausentes ou está em conflito com outros blobs.</span><span class="sxs-lookup"><span data-stu-id="a0a58-108">After an import job has completed, you can use this tool toorepair any blobs that were corrupted, were missing, or conflicted with other blobs.</span></span>  
  
-   <span data-ttu-id="a0a58-109">Depois de receber Olá unidades de um trabalho de exportação concluído, você pode usar essa ferramenta toorepair todos os arquivos que foram corrompidos ou ausentes em unidades de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0a58-109">After you receive hello drives from a completed export job, you can use this tool toorepair any files that were corrupted or missing on hello drives.</span></span>  
  
## <a name="prerequisites"></a><span data-ttu-id="a0a58-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a0a58-110">Prerequisites</span></span>  
<span data-ttu-id="a0a58-111">Se você estiver preparando unidades para um trabalho de importação, você precisará Olá toomeet pré-requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a0a58-111">If you are preparing drives for an import job, you will need toomeet hello following prerequisites:</span></span>  
  
-   <span data-ttu-id="a0a58-112">É necessário ter uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="a0a58-112">You must have an active Azure subscription.</span></span>  
  
-   <span data-ttu-id="a0a58-113">Sua assinatura deve incluir uma conta de armazenamento com suficiente espaço disponível toostore Olá de arquivos que serão tooimport.</span><span class="sxs-lookup"><span data-stu-id="a0a58-113">Your subscription must include a storage account with enough available space toostore hello files you are going tooimport.</span></span>  
  
-   <span data-ttu-id="a0a58-114">É necessário pelo menos uma das chaves de conta Olá Olá conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a0a58-114">You need at least one of hello account keys for hello storage account.</span></span>  
  
-   <span data-ttu-id="a0a58-115">Você precisa de um computador (hello "computador de cópia") com o Windows 7, Windows Server 2008 R2 ou um sistema de operacional mais recente do Windows instalado.</span><span class="sxs-lookup"><span data-stu-id="a0a58-115">You need a computer (hello "copy machine") with Windows 7, Windows Server 2008 R2, or a newer Windows operating system installed.</span></span>  
  
-   <span data-ttu-id="a0a58-116">saudação do .NET Framework 4 deve ser instalada no computador de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0a58-116">hello .NET Framework 4 must be installed on hello copy machine.</span></span>  
  
-   <span data-ttu-id="a0a58-117">O BitLocker deve ser habilitado no computador de cópia de saudação.</span><span class="sxs-lookup"><span data-stu-id="a0a58-117">BitLocker must be enabled on hello copy machine.</span></span>  
  
-   <span data-ttu-id="a0a58-118">Você precisará de um ou mais discos que contém dados toobe importado ou vazios discos rígidos SATA de 3,5 polegadas conectados toohello computador de cópia.</span><span class="sxs-lookup"><span data-stu-id="a0a58-118">You will need one or more drives that contains data toobe imported or empty 3.5-inch SATA hard drives connected toohello copy machine.</span></span>  
  
-   <span data-ttu-id="a0a58-119">arquivos Olá planejar tooimport devem estar acessíveis do computador de cópia hello, independentemente de estarem em um compartilhamento de rede ou um disco rígido local.</span><span class="sxs-lookup"><span data-stu-id="a0a58-119">hello files you plan tooimport must be accessible from hello copy machine, whether they are on a network share or a local hard drive.</span></span> 
  
<span data-ttu-id="a0a58-120">Se você estiver tentando toorepair uma importação que falhou parcialmente, será necessário:</span><span class="sxs-lookup"><span data-stu-id="a0a58-120">If you are attempting toorepair an import that has partially failed, you will need:</span></span>  
  
-   <span data-ttu-id="a0a58-121">arquivos de log de cópia Olá</span><span class="sxs-lookup"><span data-stu-id="a0a58-121">hello copy log files</span></span>  
  
-   <span data-ttu-id="a0a58-122">chave de conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="a0a58-122">hello storage account key</span></span>  
  
  <span data-ttu-id="a0a58-123">Se você estiver tentando toorepair uma exportação que falhou parcialmente, será necessário:</span><span class="sxs-lookup"><span data-stu-id="a0a58-123">If you are attempting toorepair an export that has partially failed, you will need:</span></span>  
  
-   <span data-ttu-id="a0a58-124">arquivos de log de cópia Olá</span><span class="sxs-lookup"><span data-stu-id="a0a58-124">hello copy log files</span></span>  
  
-   <span data-ttu-id="a0a58-125">arquivos de manifesto de saudação (opcionais)</span><span class="sxs-lookup"><span data-stu-id="a0a58-125">hello manifest files (optional)</span></span>  
  
-   <span data-ttu-id="a0a58-126">chave de conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="a0a58-126">hello storage account key</span></span>  
  
## <a name="installing-hello-azure-importexport-tool"></a><span data-ttu-id="a0a58-127">Olá instalar ferramenta de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="a0a58-127">Installing hello Azure Import/Export Tool</span></span>  
 <span data-ttu-id="a0a58-128">Olá, ferramenta de importação/exportação do Azure consiste em Olá seguintes arquivos:</span><span class="sxs-lookup"><span data-stu-id="a0a58-128">hello Azure Import/Export Tool consists of hello following files:</span></span>  
  
-   <span data-ttu-id="a0a58-129">WAImportExport.exe</span><span class="sxs-lookup"><span data-stu-id="a0a58-129">WAImportExport.exe</span></span>  
  
-   <span data-ttu-id="a0a58-130">WAImportExport.exe.config</span><span class="sxs-lookup"><span data-stu-id="a0a58-130">WAImportExport.exe.config</span></span>  
  
-   <span data-ttu-id="a0a58-131">WAImportExportCore.dll</span><span class="sxs-lookup"><span data-stu-id="a0a58-131">WAImportExportCore.dll</span></span>  
  
-   <span data-ttu-id="a0a58-132">WAImportExportRepair.dll</span><span class="sxs-lookup"><span data-stu-id="a0a58-132">WAImportExportRepair.dll</span></span>  
  
-   <span data-ttu-id="a0a58-133">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="a0a58-133">Microsoft.WindowsAzure.Storage.dll</span></span>  
  
-   <span data-ttu-id="a0a58-134">Hddid.dll</span><span class="sxs-lookup"><span data-stu-id="a0a58-134">Hddid.dll</span></span>  
  
 <span data-ttu-id="a0a58-135">Copie o diretório de trabalho do tooa esses arquivos, por exemplo, `c:\WAImportExport`.</span><span class="sxs-lookup"><span data-stu-id="a0a58-135">Copy these files tooa working directory, for example, `c:\WAImportExport`.</span></span> <span data-ttu-id="a0a58-136">Em seguida, abra uma janela de linha de comando no modo de administrador e defina Olá acima diretório como o diretório atual.</span><span class="sxs-lookup"><span data-stu-id="a0a58-136">Next, open a command line window in Administrator mode, and set hello above directory as current directory.</span></span>  
  
 <span data-ttu-id="a0a58-137">toooutput ajuda para o comando hello, execute a ferramenta Olá sem parâmetros:</span><span class="sxs-lookup"><span data-stu-id="a0a58-137">toooutput help for hello command, run hello tool without parameters:</span></span>  
  
```  
WAImportExport, a client tool for Microsoft Azure Import/Export service. Microsoft (c) 2013, 2014  
  
Copy a Directory:  
    WAImportExport.exe PrepImport  
        /j:<JournalFile> [/logdir:<LogDirectory>] [/id:<SessionId>] [/resumesession]  
        [/abortsession] [/sk:<StorageAccountKey>] [/csas:<ContainerSas>]  
        [/t:<TargetDriveLetter>] [/format] [/silentmode] [/encrypt]  
        [/bk:<BitLockerKey>] [/Disposition:<Disposition>] [/BlobType:<BlobType>]  
        [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]  
        /srcdir:<SourceDirectory> /dstdir:<DestinationBlobVirtualDirectory>  
  
Copy a File:  
    WAImportExport.exe PrepImport  
        /j:<JournalFile> [/logdir:<LogDirectory>] [/id:<SessionId>] [/resumesession]  
        [/abortsession] [/sk:<StorageAccountKey>] [/csas:<ContainerSas>]  
        [/t:<TargetDriveLetter>] [/format] [/silentmode] [/encrypt]  
        [/bk:<BitLockerKey>] [/Disposition:<Disposition>] [/BlobType:<BlobType>]  
        [/PropertyFile:<PropertyFile>] [/MetadataFile:<MetadataFile>]  
        /srcfile:<SourceFilePath> /dstblob:<DestinationBlobPath>  
  
Repair a Drive:  
    WAImportExport.exe RepairImport | RepairExport  
        /r:<RepairFile> [/logdir:<LogDirectory>]  
        [/d:<TargetDirectories>] [/bk:<BitLockerKey>]  
        /sn:<StorageAccountName> [/sk:<StorageAccountKey> | /csas:<ContainerSas>]  
        [/CopyLogFile:<DriveCopyLogFile>] [/ManifestFile:<DriveManifestFile>]  
        [/PathMapFile:<DrivePathMapFile>]  
  
Preview an Export Job:  
    WAImportExport.exe PreviewExport  
        [/logdir:<LogDirectory>]  
        /sn:<StorageAccountName> [/sk:<StorageAccountKey> | /csas:<ContainerSas>]  
        /ExportBlobListFile:<ExportBlobListFile> /DriveSize:<DriveSize>  
  
Parameters:  
  
    /j:<JournalFile>  
        - Required. Path toohello journal file. Each drive must have one and only one  
          journal file. hello journal file corresponding toohello target drive must always  
          be specified.  
    /logdir:<LogDirectory>  
        - Optional. hello log directory. Verbose log files as well as some temporary  
          files will be written toothis directory. If not specified, current directory  
          will be used as hello log directory.  
    /id:<SessionId>  
        - Required. hello session Id is used tooidentify a copy session. It is used too 
          ensure accurate recovery of an interrupted copy session. In addition, files  
          that are copied in a copy session are stored in a directory named after hello  
          session Id on hello target drive.  
    /resumesession  
        - Optional. If hello last copy session was terminated abnormally, this parameter  
          can be specified tooresume hello session.  
    /abortsession  
        - Optional. If hello last copy session was terminated abnormally, this parameter  
          can be specified tooabort hello session.  
    /sn:<StorageAccountName>  
        - Required. Only applicable for RepairImport and RepairExport. hello name of  
          hello storage account.  
    /sk:<StorageAccountKey>  
        - Optional. hello key of hello storage account. One of /sk: and /csas: must be  
          specified.  
    /csas:<ContainerSas>  
        - Optional. A container SAS, in format of <ContainerName>?<SasString>, toobe  
          used for import hello data. One of /sk: and /csas: must be specified.  
    /t:<TargetDriveLetter>  
        - Required. Drive letter of hello target drive.  
    /r:<RepairFile>  
        - Required. Only applicable for RepairImport and RepairExport.  
          Path toohello file for tracking repair progress. Each drive must have one  
          and only one repair file.  
    /d:<TargetDirectories>  
        - Required. Only applicable for RepairImport and RepairExport.  
          For RepairImport, one or more semicolon-separated directories toorepair;  
          For RepairExport, one directory toorepair, e.g. root directory of hello drive.  
    /format  
        - Optional. If specified, hello target drive will be formatted. DO NOT specify  
          this parameter if you do not want tooformat hello drive.  
    /silentmode  
        - Optional. If not specified, hello /format parameter will require a confirmation  
          from console before hello tool formats hello drive. If this parameter is specified,  
          not confirmation will be given for formatting hello drive.  
    /encrypt  
        - Optional. If specified, hello target drive will be encrypted with BitLocker.  
          If hello drive has already been encrypted with BitLocker, do not specify this  
          parameter and instead specify hello BitLocker key using hello "/k" parameter.  
    /bk:<BitLockerKey>  
        - Optional. hello current BitLocker key if hello drive has already been encrypted  
          with BitLocker.  
    /Disposition:<Disposition>  
        - Optional. Specifies hello behavior when a blob with hello same path as hello one  
          being imported already exists. Valid values are: rename, no-overwrite and  
          overwrite (case-sensitive). If not specified, "rename" will be used as hello  
          default value.  
    /BlobType:<BlobType>  
        - Optional. hello blob type for hello imported blob(s). Valid values are BlockBlob  
          and PageBlob. If not specified, BlockBlob will be used as hello default value.  
    /PropertyFile:<PropertyFile>  
        - Optional. Path toohello property file for hello file(s) toobe imported.  
    /MetadataFile:<MetadataFile>  
        - Optional. Path toohello metadata file for hello file(s) toobe imported.  
    /CopyLogFile:<DriveCopyLogFile>  
        - Required. Only applicable for RepairImport and RepairExport. Path toohello  
          drive copy log file (verbose or error).  
    /ManifestFile:<DriveManifestFile>  
        - Required. Only applicable for RepairExport. Path toohello drive manifest file.  
    /PathMapFile:<DrivePathMapFile>  
        - Optional. Only applicable for RepairImport. Path toohello file containing  
          mappings of file paths relative toohello drive root toolocations of actual files  
          (tab-delimited). When first specified, it will be populated with file paths  
          with empty targets, which means either they are not found in TargetDirectories,  
          access denied, with invalid name, or they exist in multiple directories. hello  
          path map file can be manually edited tooinclude hello correct target paths and  
          specified again for hello tool tooresolve hello file paths correctly.  
    /ExportBlobListFile:<ExportBlobListFile>  
        - Required. Path toohello XML file containing list of blob paths or blob path  
          prefixes for hello blobs toobe exported. hello file format is hello same as hello  
          blob list blob format in hello Put Job operation of hello Import/Export service  
          REST API.  
    /DriveSize:<DriveSize>  
        - Required. Size of drives toobe used for export. For example, 500GB, 1.5TB.  
          Note: 1 GB = 1,000,000,000 bytes  
                1 TB = 1,000,000,000,000 bytes  
    /srcdir:<SourceDirectory>  
        - Required. Source directory that contains files toobe copied toohello  
          target drives.  
    /dstdir:<DestinationBlobVirtualDirectory>  
        - Required. Destination blob virtual directory toowhich hello files will  
          be imported.  
    /srcfile:<SourceFilePath>  
        - Required. Path toohello source file toobe imported.  
    /dstblob:<DestinationBlobPath>  
        - Required. Destination blob path for hello file toobe imported.  
    /skipwrite
        - Optional. tooskip write process. Used for inplace data drive preparation.
          Be sure tooreserve enough space (3 GB per 7TB) for drive manifest file!
Examples:  
  
    Copy a source directory tooa drive:  
    WAImportExport.exe PrepImport  
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL  
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:x /format /encrypt /srcdir:d:\movi  
        es\drama /dstdir:movies/drama/  
  
    Copy another directory toohello same drive following hello above command:  
    WAImportExport.exe PrepImport  
        /j:9WM35C2V.jrn /id:session#2 /srcdir:d:\movies\action /dstdir:movies/action/  
  
    Copy another file toohello same drive following hello above commands:  
    WAImportExport.exe PrepImport  
        /j:9WM35C2V.jrn /id:session#3 /srcfile:d:\movies\dvd.vhd /dstblob:movies/dvd.vhd /BlobType:PageBlob  
  
    Preview how many 1.5 TB drives are needed for an export job:  
    WAImportExport.exe PreviewExport  
        /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7K  
        ysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\temp\myexportbloblist.xml  
        /DriveSize:1.5TB  
  
    Repair an finished import job:  
    WAImportExport.exe RepairImport  
        /r:9WM35C2V.rep /d:X:\ /bk:442926-020713-108086-436744-137335-435358-242242-2795  
        98 /sn:mytestaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94  
        f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\temp\9WM35C2V_error.log 

    Skip write process, inplace data drive preparation:
    WAImportExport.exe PrepImport
        /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GEL
        xmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movi
        es\drama /dstdir:movies/drama/ /skipwrite
```  
  
## <a name="next-steps"></a><span data-ttu-id="a0a58-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a0a58-138">Next steps</span></span>

* [<span data-ttu-id="a0a58-139">Preparação de discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="a0a58-139">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="a0a58-140">Visualização do uso da unidade para um trabalho de exportação</span><span class="sxs-lookup"><span data-stu-id="a0a58-140">Previewing Drive usage for an export job</span></span>](storage-import-export-tool-previewing-drive-usage-export-v1.md)   
* [<span data-ttu-id="a0a58-141">Revisão do status do trabalho com arquivos de log de cópia</span><span class="sxs-lookup"><span data-stu-id="a0a58-141">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="a0a58-142">Reparação de um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="a0a58-142">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="a0a58-143">Reparação de um trabalho de exportação</span><span class="sxs-lookup"><span data-stu-id="a0a58-143">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
* [<span data-ttu-id="a0a58-144">Olá, ferramenta de importação/exportação do Azure de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="a0a58-144">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
