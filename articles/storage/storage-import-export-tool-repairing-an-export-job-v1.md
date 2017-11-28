---
title: "aaaRepairing um trabalho de exportação de importação/exportação do Azure - v1 | Microsoft Docs"
description: "Saiba como toorepair um trabalho de exportação foi criado e executado usando Olá importação/exportação do Azure service."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 728e2a42-04ce-4be8-9375-e9e2bc6827a5
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 96c674fc7c697c37882fb2980c340303896ac6c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="f44b4-103">Reparação de um trabalho de exportação</span><span class="sxs-lookup"><span data-stu-id="f44b4-103">Repairing an export job</span></span>
<span data-ttu-id="f44b4-104">Depois que um trabalho de exportação for concluída, você pode executar Olá, ferramenta de importação/exportação do Microsoft Azure local para:</span><span class="sxs-lookup"><span data-stu-id="f44b4-104">After an export job has completed, you can run hello Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="f44b4-105">Baixe os arquivos que o serviço de importação/exportação do Azure Olá foi tooexport não é possível.</span><span class="sxs-lookup"><span data-stu-id="f44b4-105">Download any files that hello Azure Import/Export service was unable tooexport.</span></span>  
  
2.  <span data-ttu-id="f44b4-106">Valide arquivos Olá na unidade Olá foram exportados corretamente.</span><span class="sxs-lookup"><span data-stu-id="f44b4-106">Validate that hello files on hello drive were correctly exported.</span></span>  
  
<span data-ttu-id="f44b4-107">Você deve ter conectividade tooAzure armazenamento toouse essa funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="f44b4-107">You must have connectivity tooAzure Storage toouse this functionality.</span></span>  
  
<span data-ttu-id="f44b4-108">saudação de comando para reparar um trabalho de importação é **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="f44b4-108">hello command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="f44b4-109">Parâmetros de RepairExport</span><span class="sxs-lookup"><span data-stu-id="f44b4-109">RepairExport parameters</span></span>

<span data-ttu-id="f44b4-110">Olá parâmetros a seguir podem ser especificados com **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="f44b4-110">hello following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="f44b4-111">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="f44b4-111">Parameter</span></span>|<span data-ttu-id="f44b4-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="f44b4-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="f44b4-113">**/r:<RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="f44b4-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="f44b4-114">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="f44b4-114">Required.</span></span> <span data-ttu-id="f44b4-115">Arquivo de reparo do toohello de caminho, que controla o progresso de saudação de reparo do hello e permite que você tooresume um reparo interrompido.</span><span class="sxs-lookup"><span data-stu-id="f44b4-115">Path toohello repair file, which tracks hello progress of hello repair, and allows you tooresume an interrupted repair.</span></span> <span data-ttu-id="f44b4-116">Cada unidade deve ter um, e somente um, arquivo de reparo.</span><span class="sxs-lookup"><span data-stu-id="f44b4-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="f44b4-117">Quando você inicia um reparo para uma determinada unidade, passará no hello caminho tooa arquivo de reparo que ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="f44b4-117">When you start a repair for a given drive, you will pass in hello path tooa repair file which does not yet exist.</span></span> <span data-ttu-id="f44b4-118">tooresume um reparo interrompido, você deve passar no nome de saudação de um arquivo de reparo existente.</span><span class="sxs-lookup"><span data-stu-id="f44b4-118">tooresume an interrupted repair, you should pass in hello name of an existing repair file.</span></span> <span data-ttu-id="f44b4-119">unidade de destino do Hello reparo arquivo correspondente toohello sempre deve ser especificada.</span><span class="sxs-lookup"><span data-stu-id="f44b4-119">hello repair file corresponding toohello target drive must always be specified.</span></span>|  
|<span data-ttu-id="f44b4-120">**/logdir:<LogDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="f44b4-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="f44b4-121">Opcional.</span><span class="sxs-lookup"><span data-stu-id="f44b4-121">Optional.</span></span> <span data-ttu-id="f44b4-122">diretório de log Hello.</span><span class="sxs-lookup"><span data-stu-id="f44b4-122">hello log directory.</span></span> <span data-ttu-id="f44b4-123">Arquivos de log detalhados serão gravados toothis directory.</span><span class="sxs-lookup"><span data-stu-id="f44b4-123">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="f44b4-124">Se nenhum diretório de log for especificado, diretório atual Olá será usado como diretório de log hello.</span><span class="sxs-lookup"><span data-stu-id="f44b4-124">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="f44b4-125">**/d:<TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="f44b4-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="f44b4-126">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="f44b4-126">Required.</span></span> <span data-ttu-id="f44b4-127">Olá diretório toovalidate e reparo.</span><span class="sxs-lookup"><span data-stu-id="f44b4-127">hello directory toovalidate and repair.</span></span> <span data-ttu-id="f44b4-128">Isso geralmente é o diretório raiz de saudação da unidade de exportação hello, mas pode também ser um compartilhamento de arquivos de rede que contém uma cópia dos arquivos hello exportada.</span><span class="sxs-lookup"><span data-stu-id="f44b4-128">This is usually hello root directory of hello export drive, but could also be a network file share containing a copy of hello exported files.</span></span>|  
|<span data-ttu-id="f44b4-129">**/bk:<BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="f44b4-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="f44b4-130">Opcional.</span><span class="sxs-lookup"><span data-stu-id="f44b4-130">Optional.</span></span> <span data-ttu-id="f44b4-131">Você deve especificar a chave do BitLocker Olá se você quiser Olá ferramenta toounlock uma unidade criptografada onde hello exportada arquivos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="f44b4-131">You should specify hello BitLocker key if you want hello tool toounlock an encrypted where hello exported files are stored.</span></span>|  
|<span data-ttu-id="f44b4-132">**/sn:<StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="f44b4-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="f44b4-133">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="f44b4-133">Required.</span></span> <span data-ttu-id="f44b4-134">trabalho de exportação de nome de Olá Olá da conta de armazenamento para hello.</span><span class="sxs-lookup"><span data-stu-id="f44b4-134">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="f44b4-135">**/sk:<StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="f44b4-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="f44b4-136">**Necessário** somente se uma SAS do contêiner não for especificada.</span><span class="sxs-lookup"><span data-stu-id="f44b4-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="f44b4-137">trabalho de exportação da chave da conta Olá para conta de armazenamento Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="f44b4-137">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="f44b4-138">**/csas:<ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="f44b4-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="f44b4-139">**Necessário** se e somente se Olá chave de conta de armazenamento não for especificada.</span><span class="sxs-lookup"><span data-stu-id="f44b4-139">**Required** if and only if hello storage account key is not specified.</span></span> <span data-ttu-id="f44b4-140">Olá SAS do contêiner para acessar blobs Olá associados ao trabalho de exportação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f44b4-140">hello container SAS for accessing hello blobs associated with hello export job.</span></span>|  
|<span data-ttu-id="f44b4-141">**/CopyLogFile:<DriveCopyLogFile\>**</span><span class="sxs-lookup"><span data-stu-id="f44b4-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="f44b4-142">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="f44b4-142">Required.</span></span> <span data-ttu-id="f44b4-143">Olá caminho toohello unidade copiar arquivo do log.</span><span class="sxs-lookup"><span data-stu-id="f44b4-143">hello path toohello drive copy log file.</span></span> <span data-ttu-id="f44b4-144">arquivo Hello é gerado pelo Olá serviço de importação/exportação do Windows Azure e pode ser baixado do armazenamento de blob Olá associado ao trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="f44b4-144">hello file is generated by hello Windows Azure Import/Export service and can be downloaded from hello blob storage associated with hello job.</span></span> <span data-ttu-id="f44b4-145">arquivo de log de cópia Olá contém informações sobre blobs com falha ou arquivos que são toobe reparado.</span><span class="sxs-lookup"><span data-stu-id="f44b4-145">hello copy log file contains information about failed blobs or files which are toobe repaired.</span></span>|  
|<span data-ttu-id="f44b4-146">**/ManifestFile:<DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="f44b4-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="f44b4-147">Opcional.</span><span class="sxs-lookup"><span data-stu-id="f44b4-147">Optional.</span></span> <span data-ttu-id="f44b4-148">arquivo de manifesto da unidade de exportação toohello caminho Hello.</span><span class="sxs-lookup"><span data-stu-id="f44b4-148">hello path toohello export drive's manifest file.</span></span> <span data-ttu-id="f44b4-149">Esse arquivo é gerado pelo serviço de importação/exportação do Windows Azure hello e armazenado na unidade de exportação hello e, opcionalmente em um blob na conta de armazenamento Olá associado ao trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="f44b4-149">This file is generated by hello Windows Azure Import/Export service and stored on hello export drive, and optionally in a blob in hello storage account associated with hello job.</span></span><br /><br /> <span data-ttu-id="f44b4-150">Olá conteúdo Olá arquivos na unidade de exportação Olá será verificado com hello os hashes MD5 contidos nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="f44b4-150">hello content of hello files on hello export drive will be verified with hello MD5 hashes contained in this file.</span></span> <span data-ttu-id="f44b4-151">Todos os arquivos que são determinado toobe corrompido será baixado e reescrito toohello diretórios de destino.</span><span class="sxs-lookup"><span data-stu-id="f44b4-151">Any files that are determined toobe corrupted will be downloaded and rewritten toohello target directories.</span></span>|  
  
## <a name="using-repairexport-mode-toocorrect-failed-exports"></a><span data-ttu-id="f44b4-152">Usando RepairExport modo toocorrect falha exportações</span><span class="sxs-lookup"><span data-stu-id="f44b4-152">Using RepairExport mode toocorrect failed exports</span></span>  
<span data-ttu-id="f44b4-153">Você pode usar arquivos toodownload do hello ferramenta de importação/exportação do Azure que falha tooexport.</span><span class="sxs-lookup"><span data-stu-id="f44b4-153">You can use hello Azure Import/Export Tool toodownload files that failed tooexport.</span></span> <span data-ttu-id="f44b4-154">arquivo de log de cópia Olá conterá uma lista dos arquivos que não tooexport.</span><span class="sxs-lookup"><span data-stu-id="f44b4-154">hello copy log file will contain a list of files that failed tooexport.</span></span>  
  
<span data-ttu-id="f44b4-155">as causas das falhas de exportação Olá incluem hello seguintes possibilidades:</span><span class="sxs-lookup"><span data-stu-id="f44b4-155">hello causes of export failures include hello following possibilities:</span></span>  
  
-   <span data-ttu-id="f44b4-156">Unidades danificadas</span><span class="sxs-lookup"><span data-stu-id="f44b4-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="f44b4-157">chave de conta de armazenamento Olá alterado durante o processo de transferência Olá</span><span class="sxs-lookup"><span data-stu-id="f44b4-157">hello storage account key changed during hello transfer process</span></span>  
  
<span data-ttu-id="f44b4-158">ferramenta de saudação toorun **RepairExport** modo, você primeiro precisa de unidade de saudação tooconnect contendo Olá arquivos exportados tooyour computador.</span><span class="sxs-lookup"><span data-stu-id="f44b4-158">toorun hello tool in **RepairExport** mode, you first need tooconnect hello drive containing hello exported files tooyour computer.</span></span> <span data-ttu-id="f44b4-159">Em seguida, execute Olá, ferramenta de importação/exportação do Azure, especificando Olá caminho toothat unidade com hello `/d` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="f44b4-159">Next, run hello Azure Import/Export Tool, specifying hello path toothat drive with hello `/d` parameter.</span></span> <span data-ttu-id="f44b4-160">Também é necessário o arquivo de log de cópia da unidade do toohello caminho Olá toospecify que você baixou.</span><span class="sxs-lookup"><span data-stu-id="f44b4-160">You also need toospecify hello path toohello drive's copy log file that you downloaded.</span></span> <span data-ttu-id="f44b4-161">Hello seguinte exemplo de linha de comando abaixo executa Olá ferramenta toorepair todos os arquivos que falharam tooexport:</span><span class="sxs-lookup"><span data-stu-id="f44b4-161">hello following command line example below runs hello tool toorepair any files that failed tooexport:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="f44b4-162">a seguir Olá é um exemplo de um arquivo de log de cópia que mostra um bloco em Olá blob falhado tooexport:</span><span class="sxs-lookup"><span data-stu-id="f44b4-162">hello following is an example of a copy log file that shows that one block in hello blob failed tooexport:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog>  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/desert.jpg</BlobPath>  
    <FilePath>\pictures\wild\desert.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList>  
      <Block Offset="65536" Length="65536" Id="AQAAAA==" Status="Failed" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="f44b4-163">arquivo de log de cópia Olá indica que ocorreu uma falha enquanto Olá serviço de importação/exportação do Windows Azure baixava um dos arquivos de toohello blocos do blob Olá na unidade de exportação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f44b4-163">hello copy log file indicates that a failure occurred while hello Windows Azure Import/Export service was downloading one of hello blob's blocks toohello file on hello export drive.</span></span> <span data-ttu-id="f44b4-164">Olá outros componentes do arquivo hello baixado com êxito e tamanho do arquivo hello foi definido corretamente.</span><span class="sxs-lookup"><span data-stu-id="f44b4-164">hello other components of hello file downloaded successfully, and hello file length was correctly set.</span></span> <span data-ttu-id="f44b4-165">Nesse caso, ferramenta Olá abrir arquivo hello na unidade hello, baixar bloco Olá Olá da conta de armazenamento e grave-o intervalo de arquivo toohello partir do deslocamento 65536 com comprimento 65536.</span><span class="sxs-lookup"><span data-stu-id="f44b4-165">In this case, hello tool will open hello file on hello drive, download hello block from hello storage account, and write it toohello file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-toovalidate-drive-contents"></a><span data-ttu-id="f44b4-166">Usando RepairExport toovalidate conteúdo da unidade</span><span class="sxs-lookup"><span data-stu-id="f44b4-166">Using RepairExport toovalidate drive contents</span></span>  
<span data-ttu-id="f44b4-167">Você também pode usar a importação/exportação do Azure com hello **RepairExport** opção toovalidate Olá conteúdo na unidade hello está correto.</span><span class="sxs-lookup"><span data-stu-id="f44b4-167">You can also use Azure Import/Export with hello **RepairExport** option toovalidate hello contents on hello drive are correct.</span></span> <span data-ttu-id="f44b4-168">arquivo de manifesto de saudação em cada unidade de exportação contém MD5s para conteúdo de saudação da unidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="f44b4-168">hello manifest file on each export drive contains MD5s for hello contents of hello drive.</span></span>  
  
<span data-ttu-id="f44b4-169">Olá serviço de importação/exportação do Azure também pode salvar os arquivos de manifesto Olá tooa conta de armazenamento durante o processo de exportação hello.</span><span class="sxs-lookup"><span data-stu-id="f44b4-169">hello Azure Import/Export service can also save hello manifest files tooa storage account during hello export process.</span></span> <span data-ttu-id="f44b4-170">Hello local dos arquivos de manifesto hello está disponível por meio de saudação [obter trabalho](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação quando o trabalho Olá tiver sido concluído.</span><span class="sxs-lookup"><span data-stu-id="f44b4-170">hello location of hello manifest files is available via hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when hello job has completed.</span></span> <span data-ttu-id="f44b4-171">Consulte [formato do arquivo de manifesto do serviço de importação/exportação](storage-import-export-file-format-metadata-and-properties.md) para obter mais informações sobre o formato de saudação de um arquivo de manifesto da unidade.</span><span class="sxs-lookup"><span data-stu-id="f44b4-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about hello format of a drive manifest file.</span></span>  
  
<span data-ttu-id="f44b4-172">Olá exemplo a seguir mostra como toorun Olá ferramenta de importação/exportação do Azure com hello **/ManifestFile** e **/CopyLogFile** parâmetros:</span><span class="sxs-lookup"><span data-stu-id="f44b4-172">hello following example shows how toorun hello Azure Import/Export Tool with hello **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="f44b4-173">Olá seguinte é um exemplo de um arquivo de manifesto:</span><span class="sxs-lookup"><span data-stu-id="f44b4-173">hello following is an example of a manifest file:</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveManifest Version="2011-10-01">  
  <Drive>  
    <DriveId>9WM35C3U</DriveId>  
    <ClientCreator>Windows Azure Import/Export service</ClientCreator>  
    <BlobList>
      <Blob>  
        <BlobPath>pictures/city/redmond.jpg</BlobPath>  
        <FilePath>\pictures\city\redmond.jpg</FilePath>  
        <Length>15360</Length>  
        <PageRangeList>  
          <PageRange Offset="0" Length="3584" Hash="72FC55ED9AFDD40A0C8D5C4193208416" />  
          <PageRange Offset="3584" Length="3584" Hash="68B28A561B73D1DA769D4C24AA427DB8" />  
          <PageRange Offset="7168" Length="512" Hash="F521DF2F50C46BC5F9EA9FB787A23EED" />  
        </PageRangeList>  
        <PropertiesPath Hash="E72A22EA959566066AD89E3B49020C0A">\pictures\city\redmond.jpg.properties</PropertiesPath>  
      </Blob>  
      <Blob>  
        <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
        <FilePath>\pictures\wild\canyon.jpg</FilePath>  
        <Length>10884</Length>  
        <BlockList>  
          <Block Offset="0" Length="2721" Id="AAAAAA==" Hash="263DC9C4B99C2177769C5EBE04787037" />  
          <Block Offset="2721" Length="2721" Id="AQAAAA==" Hash="0C52BAE2CC20EFEC15CC1E3045517AA6" />  
          <Block Offset="5442" Length="2721" Id="AgAAAA==" Hash="73D1CB62CB426230C34C9F57B7148F10" />  
          <Block Offset="8163" Length="2721" Id="AwAAAA==" Hash="11210E665C5F8E7E4F136D053B243E6A" />  
        </BlockList>  
        <PropertiesPath Hash="81D7F81B2C29F10D6E123D386C3A4D5A">\pictures\wild\canyon.jpg.properties</PropertiesPath>  
      </Blob> 
    </BlobList>  
 </Drive>  
</DriveManifest>  
``` 
  
<span data-ttu-id="f44b4-174">Depois de terminar processo de reparo Olá, ferramenta Olá lerá cada arquivo referenciado no arquivo de manifesto hello e verificar a integridade do arquivo hello com hashes MD5 de saudação.</span><span class="sxs-lookup"><span data-stu-id="f44b4-174">After finishing hello repair process, hello tool will read through each file referenced in hello manifest file and verify hello file's integrity with hello MD5 hashes.</span></span> <span data-ttu-id="f44b4-175">Para o manifesto Olá acima, ele percorrerá Olá componentes a seguir.</span><span class="sxs-lookup"><span data-stu-id="f44b4-175">For hello manifest above, it will go through hello following components.</span></span>  

```  
G:\pictures\city\redmond.jpg, offset 0, length 3584  
  
G:\pictures\city\redmond.jpg, offset 3584, length 3584  
  
G:\pictures\city\redmond.jpg, offset 7168, length 3584  
  
G:\pictures\city\redmond.jpg.properties  
  
G:\pictures\wild\canyon.jpg, offset 0, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 2721, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 5442, length 2721  
  
G:\pictures\wild\canyon.jpg, offset 8163, length 2721  
  
G:\pictures\wild\canyon.jpg.properties  
```

<span data-ttu-id="f44b4-176">Qualquer componente com falha de verificação de saudação será baixado pela ferramenta hello e reescrito toohello mesmo arquivo na unidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="f44b4-176">Any component failing hello verification will be downloaded by hello tool and rewritten toohello same file on hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="f44b4-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f44b4-177">Next steps</span></span>
 
* [<span data-ttu-id="f44b4-178">Configurando Olá ferramenta de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="f44b4-178">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="f44b4-179">Preparação de discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="f44b4-179">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="f44b4-180">Revisão do status do trabalho com arquivos de log de cópia</span><span class="sxs-lookup"><span data-stu-id="f44b4-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="f44b4-181">Reparação de um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="f44b4-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="f44b4-182">Olá, ferramenta de importação/exportação do Azure de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="f44b4-182">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
