---
title: "Reparando um trabalho de exportação do serviço de Importação/Exportação do Azure — v1 | Microsoft Docs"
description: "Saiba como reparar um trabalho de exportação criado e executado usando o serviço de Importação/Exportação do Azure."
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
ms.openlocfilehash: 30ca0f8d06cb1927c19e66035ff485db0fc09e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="repairing-an-export-job"></a><span data-ttu-id="8ab08-103">Reparação de um trabalho de exportação</span><span class="sxs-lookup"><span data-stu-id="8ab08-103">Repairing an export job</span></span>
<span data-ttu-id="8ab08-104">Após a conclusão de um trabalho de exportação, você poderá executar a Ferramenta de Importação/Exportação do Microsoft Azure local para:</span><span class="sxs-lookup"><span data-stu-id="8ab08-104">After an export job has completed, you can run the Microsoft Azure Import/Export Tool on-premises to:</span></span>  
  
1.  <span data-ttu-id="8ab08-105">Baixar todos os arquivos que o serviço de Importação/Exportação do Azure não conseguiu exportar.</span><span class="sxs-lookup"><span data-stu-id="8ab08-105">Download any files that the Azure Import/Export service was unable to export.</span></span>  
  
2.  <span data-ttu-id="8ab08-106">Validar se os arquivos na unidade foram exportados corretamente.</span><span class="sxs-lookup"><span data-stu-id="8ab08-106">Validate that the files on the drive were correctly exported.</span></span>  
  
<span data-ttu-id="8ab08-107">Você deve ter conectividade com o Armazenamento do Azure para usar essa funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="8ab08-107">You must have connectivity to Azure Storage to use this functionality.</span></span>  
  
<span data-ttu-id="8ab08-108">O comando para reparar um trabalho de importação é **RepairExport**.</span><span class="sxs-lookup"><span data-stu-id="8ab08-108">The command for repairing an import job is **RepairExport**.</span></span>

## <a name="repairexport-parameters"></a><span data-ttu-id="8ab08-109">Parâmetros de RepairExport</span><span class="sxs-lookup"><span data-stu-id="8ab08-109">RepairExport parameters</span></span>

<span data-ttu-id="8ab08-110">Os seguintes parâmetros podem ser especificados com **RepairExport**:</span><span class="sxs-lookup"><span data-stu-id="8ab08-110">The following parameters can be specified with **RepairExport**:</span></span>  
  
|<span data-ttu-id="8ab08-111">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="8ab08-111">Parameter</span></span>|<span data-ttu-id="8ab08-112">Descrição</span><span class="sxs-lookup"><span data-stu-id="8ab08-112">Description</span></span>|  
|---------------|-----------------|  
|<span data-ttu-id="8ab08-113">**/r:<RepairFile\>**</span><span class="sxs-lookup"><span data-stu-id="8ab08-113">**/r:<RepairFile\>**</span></span>|<span data-ttu-id="8ab08-114">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="8ab08-114">Required.</span></span> <span data-ttu-id="8ab08-115">Caminho até o arquivo de reparo, que controla o progresso do reparo e permite que você retome um reparo interrompido.</span><span class="sxs-lookup"><span data-stu-id="8ab08-115">Path to the repair file, which tracks the progress of the repair, and allows you to resume an interrupted repair.</span></span> <span data-ttu-id="8ab08-116">Cada unidade deve ter um, e somente um, arquivo de reparo.</span><span class="sxs-lookup"><span data-stu-id="8ab08-116">Each drive must have one and only one repair file.</span></span> <span data-ttu-id="8ab08-117">Ao iniciar o reparo de uma determinada unidade, você passará no caminho até um arquivo de reparo que ainda não existe.</span><span class="sxs-lookup"><span data-stu-id="8ab08-117">When you start a repair for a given drive, you will pass in the path to a repair file which does not yet exist.</span></span> <span data-ttu-id="8ab08-118">Para retomar um reparo interrompido, você deve passar no nome de um arquivo de reparo existente.</span><span class="sxs-lookup"><span data-stu-id="8ab08-118">To resume an interrupted repair, you should pass in the name of an existing repair file.</span></span> <span data-ttu-id="8ab08-119">O arquivo de reparo que corresponde à unidade de destino deve sempre ser especificado.</span><span class="sxs-lookup"><span data-stu-id="8ab08-119">The repair file corresponding to the target drive must always be specified.</span></span>|  
|<span data-ttu-id="8ab08-120">**/logdir:<LogDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="8ab08-120">**/logdir:<LogDirectory\>**</span></span>|<span data-ttu-id="8ab08-121">Opcional.</span><span class="sxs-lookup"><span data-stu-id="8ab08-121">Optional.</span></span> <span data-ttu-id="8ab08-122">O diretório de log.</span><span class="sxs-lookup"><span data-stu-id="8ab08-122">The log directory.</span></span> <span data-ttu-id="8ab08-123">Os arquivos de log detalhados serão gravados nesse diretório.</span><span class="sxs-lookup"><span data-stu-id="8ab08-123">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="8ab08-124">Se nenhum diretório de log for especificado, o diretório atual será usado como o diretório de log.</span><span class="sxs-lookup"><span data-stu-id="8ab08-124">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="8ab08-125">**/d:<TargetDirectory\>**</span><span class="sxs-lookup"><span data-stu-id="8ab08-125">**/d:<TargetDirectory\>**</span></span>|<span data-ttu-id="8ab08-126">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="8ab08-126">Required.</span></span> <span data-ttu-id="8ab08-127">O diretório a ser validado e reparado.</span><span class="sxs-lookup"><span data-stu-id="8ab08-127">The directory to validate and repair.</span></span> <span data-ttu-id="8ab08-128">Normalmente é o diretório raiz da unidade de exportação, mas também pode ser um compartilhamento de arquivos de rede que contém uma cópia dos arquivos exportados.</span><span class="sxs-lookup"><span data-stu-id="8ab08-128">This is usually the root directory of the export drive, but could also be a network file share containing a copy of the exported files.</span></span>|  
|<span data-ttu-id="8ab08-129">**/bk:<BitLockerKey\>**</span><span class="sxs-lookup"><span data-stu-id="8ab08-129">**/bk:<BitLockerKey\>**</span></span>|<span data-ttu-id="8ab08-130">Opcional.</span><span class="sxs-lookup"><span data-stu-id="8ab08-130">Optional.</span></span> <span data-ttu-id="8ab08-131">Você deve especificar a chave do BitLocker se quiser que a ferramenta desbloqueie uma unidade criptografada na qual os arquivos exportados foram armazenados.</span><span class="sxs-lookup"><span data-stu-id="8ab08-131">You should specify the BitLocker key if you want the tool to unlock an encrypted where the exported files are stored.</span></span>|  
|<span data-ttu-id="8ab08-132">**/sn:<StorageAccountName\>**</span><span class="sxs-lookup"><span data-stu-id="8ab08-132">**/sn:<StorageAccountName\>**</span></span>|<span data-ttu-id="8ab08-133">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="8ab08-133">Required.</span></span> <span data-ttu-id="8ab08-134">O nome da conta de armazenamento do trabalho de exportação.</span><span class="sxs-lookup"><span data-stu-id="8ab08-134">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="8ab08-135">**/sk:<StorageAccountKey\>**</span><span class="sxs-lookup"><span data-stu-id="8ab08-135">**/sk:<StorageAccountKey\>**</span></span>|<span data-ttu-id="8ab08-136">**Necessário** somente se uma SAS do contêiner não for especificada.</span><span class="sxs-lookup"><span data-stu-id="8ab08-136">**Required** if and only if a container SAS is not specified.</span></span> <span data-ttu-id="8ab08-137">A chave de conta da conta de armazenamento do trabalho de exportação.</span><span class="sxs-lookup"><span data-stu-id="8ab08-137">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="8ab08-138">**/csas:<ContainerSas\>**</span><span class="sxs-lookup"><span data-stu-id="8ab08-138">**/csas:<ContainerSas\>**</span></span>|<span data-ttu-id="8ab08-139">**Necessário** somente se a chave da conta de armazenamento não for especificada.</span><span class="sxs-lookup"><span data-stu-id="8ab08-139">**Required** if and only if the storage account key is not specified.</span></span> <span data-ttu-id="8ab08-140">O SAS do contêiner para acessar os blobs associados ao trabalho de exportação.</span><span class="sxs-lookup"><span data-stu-id="8ab08-140">The container SAS for accessing the blobs associated with the export job.</span></span>|  
|<span data-ttu-id="8ab08-141">**/CopyLogFile:<DriveCopyLogFile\>**</span><span class="sxs-lookup"><span data-stu-id="8ab08-141">**/CopyLogFile:<DriveCopyLogFile\>**</span></span>|<span data-ttu-id="8ab08-142">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="8ab08-142">Required.</span></span> <span data-ttu-id="8ab08-143">O caminho até o arquivo de log de cópia da unidade.</span><span class="sxs-lookup"><span data-stu-id="8ab08-143">The path to the drive copy log file.</span></span> <span data-ttu-id="8ab08-144">O arquivo é gerado pelo serviço de Importação/Exportação do Windows Azure e pode ser baixado do armazenamento de blobs associado ao trabalho.</span><span class="sxs-lookup"><span data-stu-id="8ab08-144">The file is generated by the Windows Azure Import/Export service and can be downloaded from the blob storage associated with the job.</span></span> <span data-ttu-id="8ab08-145">O arquivo de log de cópia contém informações sobre blobs com falha ou arquivos que devem ser reparados.</span><span class="sxs-lookup"><span data-stu-id="8ab08-145">The copy log file contains information about failed blobs or files which are to be repaired.</span></span>|  
|<span data-ttu-id="8ab08-146">**/ManifestFile:<DriveManifestFile\>**</span><span class="sxs-lookup"><span data-stu-id="8ab08-146">**/ManifestFile:<DriveManifestFile\>**</span></span>|<span data-ttu-id="8ab08-147">Opcional.</span><span class="sxs-lookup"><span data-stu-id="8ab08-147">Optional.</span></span> <span data-ttu-id="8ab08-148">O caminho até o arquivo de manifesto da unidade de exportação.</span><span class="sxs-lookup"><span data-stu-id="8ab08-148">The path to the export drive's manifest file.</span></span> <span data-ttu-id="8ab08-149">Esse arquivo é gerado pelo serviço de Importação/Exportação do Windows Azure e armazenado na unidade de exportação e, opcionalmente, em um blob na conta de armazenamento associada ao trabalho.</span><span class="sxs-lookup"><span data-stu-id="8ab08-149">This file is generated by the Windows Azure Import/Export service and stored on the export drive, and optionally in a blob in the storage account associated with the job.</span></span><br /><br /> <span data-ttu-id="8ab08-150">O conteúdo dos arquivos na unidade de exportação será verificado com os hashes MD5 contidos nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="8ab08-150">The content of the files on the export drive will be verified with the MD5 hashes contained in this file.</span></span> <span data-ttu-id="8ab08-151">Todos os arquivos determinados como corrompidos serão baixados e reescritos nos diretórios de destino.</span><span class="sxs-lookup"><span data-stu-id="8ab08-151">Any files that are determined to be corrupted will be downloaded and rewritten to the target directories.</span></span>|  
  
## <a name="using-repairexport-mode-to-correct-failed-exports"></a><span data-ttu-id="8ab08-152">Usando o modo RepairExport para corrigir exportações com falha</span><span class="sxs-lookup"><span data-stu-id="8ab08-152">Using RepairExport mode to correct failed exports</span></span>  
<span data-ttu-id="8ab08-153">Você pode usar a Ferramenta de Importação/Exportação do Azure para baixar arquivos cuja exportação falhou.</span><span class="sxs-lookup"><span data-stu-id="8ab08-153">You can use the Azure Import/Export Tool to download files that failed to export.</span></span> <span data-ttu-id="8ab08-154">O arquivo de log da cópia conterá uma lista de arquivos que não foram exportados devido a alguma falha.</span><span class="sxs-lookup"><span data-stu-id="8ab08-154">The copy log file will contain a list of files that failed to export.</span></span>  
  
<span data-ttu-id="8ab08-155">As causas das falhas de exportação incluem as seguintes possibilidades:</span><span class="sxs-lookup"><span data-stu-id="8ab08-155">The causes of export failures include the following possibilities:</span></span>  
  
-   <span data-ttu-id="8ab08-156">Unidades danificadas</span><span class="sxs-lookup"><span data-stu-id="8ab08-156">Damaged drives</span></span>  
  
-   <span data-ttu-id="8ab08-157">A chave da conta de armazenamento mudou durante o processo de transferência</span><span class="sxs-lookup"><span data-stu-id="8ab08-157">The storage account key changed during the transfer process</span></span>  
  
<span data-ttu-id="8ab08-158">Para executar a ferramenta no modo **RepairExport**, primeiro você precisa conectar a unidade que contém os arquivos exportados ao seu computador.</span><span class="sxs-lookup"><span data-stu-id="8ab08-158">To run the tool in **RepairExport** mode, you first need to connect the drive containing the exported files to your computer.</span></span> <span data-ttu-id="8ab08-159">Em seguida, execute a Ferramenta de Importação/Exportação do Azure, especificando o caminho até essa unidade com o parâmetro `/d`.</span><span class="sxs-lookup"><span data-stu-id="8ab08-159">Next, run the Azure Import/Export Tool, specifying the path to that drive with the `/d` parameter.</span></span> <span data-ttu-id="8ab08-160">Você também precisa especificar o caminho até arquivo de log de cópia da unidade que você baixou.</span><span class="sxs-lookup"><span data-stu-id="8ab08-160">You also need to specify the path to the drive's copy log file that you downloaded.</span></span> <span data-ttu-id="8ab08-161">O exemplo de linha de comando abaixo executa a ferramenta para reparar todos os arquivos que não foram exportados devido a alguma falha:</span><span class="sxs-lookup"><span data-stu-id="8ab08-161">The following command line example below runs the tool to repair any files that failed to export:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log  
```  
  
<span data-ttu-id="8ab08-162">Veja a seguir um exemplo de um arquivo de log de cópia mostrando que um bloco no blob falhou durante a exportação:</span><span class="sxs-lookup"><span data-stu-id="8ab08-162">The following is an example of a copy log file that shows that one block in the blob failed to export:</span></span>  
  
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
  
<span data-ttu-id="8ab08-163">O arquivo de log da cópia indica que ocorreu uma falha enquanto o serviço de Importação/Exportação do Windows Azure baixava um dos blocos de blob para o arquivo na unidade de exportação.</span><span class="sxs-lookup"><span data-stu-id="8ab08-163">The copy log file indicates that a failure occurred while the Windows Azure Import/Export service was downloading one of the blob's blocks to the file on the export drive.</span></span> <span data-ttu-id="8ab08-164">Os outros componentes do arquivo foram baixados com êxito, e o tamanho do arquivo foi definido corretamente.</span><span class="sxs-lookup"><span data-stu-id="8ab08-164">The other components of the file downloaded successfully, and the file length was correctly set.</span></span> <span data-ttu-id="8ab08-165">Nesse caso, a ferramenta abrirá o arquivo na unidade, baixará o bloco da conta de armazenamento e o gravará no intervalo de arquivos, a partir do deslocamento 65536 com comprimento 65536.</span><span class="sxs-lookup"><span data-stu-id="8ab08-165">In this case, the tool will open the file on the drive, download the block from the storage account, and write it to the file range starting from offset 65536 with length 65536.</span></span>  
  
## <a name="using-repairexport-to-validate-drive-contents"></a><span data-ttu-id="8ab08-166">Usando o RepairExport para validar o conteúdo da unidade</span><span class="sxs-lookup"><span data-stu-id="8ab08-166">Using RepairExport to validate drive contents</span></span>  
<span data-ttu-id="8ab08-167">Você também pode usar a Importação/Exportação do Azure com a opção **RepairExport** para validar se o conteúdo na unidade está correto.</span><span class="sxs-lookup"><span data-stu-id="8ab08-167">You can also use Azure Import/Export with the **RepairExport** option to validate the contents on the drive are correct.</span></span> <span data-ttu-id="8ab08-168">O arquivo de manifesto em cada unidade de exportação contém MD5s para o conteúdo da unidade.</span><span class="sxs-lookup"><span data-stu-id="8ab08-168">The manifest file on each export drive contains MD5s for the contents of the drive.</span></span>  
  
<span data-ttu-id="8ab08-169">O serviço de Importação/Exportação do Azure também pode salvar os arquivos de manifesto em uma conta de armazenamento durante o processo de exportação.</span><span class="sxs-lookup"><span data-stu-id="8ab08-169">The Azure Import/Export service can also save the manifest files to a storage account during the export process.</span></span> <span data-ttu-id="8ab08-170">O local dos arquivos de manifesto está disponível por meio da operação [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) após a conclusão do trabalho.</span><span class="sxs-lookup"><span data-stu-id="8ab08-170">The location of the manifest files is available via the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation when the job has completed.</span></span> <span data-ttu-id="8ab08-171">Consulte [Formato de arquivo de manifesto do serviço de Importação/Exportação](storage-import-export-file-format-metadata-and-properties.md) para saber mais sobre o formato de um arquivo de manifesto da unidade.</span><span class="sxs-lookup"><span data-stu-id="8ab08-171">See [Import/Export service Manifest File Format](storage-import-export-file-format-metadata-and-properties.md) for more information about the format of a drive manifest file.</span></span>  
  
<span data-ttu-id="8ab08-172">O seguinte exemplo mostra como executar a Ferramenta de Importação/Exportação do Azure com os parâmetros **/ManifestFile** e **/CopyLogFile**:</span><span class="sxs-lookup"><span data-stu-id="8ab08-172">The following example shows how to run the Azure Import/Export Tool with the **/ManifestFile** and **/CopyLogFile** parameters:</span></span>  
  
```  
WAImportExport.exe RepairExport /r:C:\WAImportExport\9WM35C3U.rep /d:G:\ /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /CopyLogFile:C:\WAImportExport\9WM35C3U.log /ManifestFile:G:\9WM35C3U.manifest  
```  
  
<span data-ttu-id="8ab08-173">Veja a seguir um exemplo de um arquivo de manifesto:</span><span class="sxs-lookup"><span data-stu-id="8ab08-173">The following is an example of a manifest file:</span></span>  
  
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
  
<span data-ttu-id="8ab08-174">Depois de concluir o processo de reparo, a ferramenta lerá cada arquivo referenciado no arquivo de manifesto e verificará a integridade do arquivo com os hashes MD5.</span><span class="sxs-lookup"><span data-stu-id="8ab08-174">After finishing the repair process, the tool will read through each file referenced in the manifest file and verify the file's integrity with the MD5 hashes.</span></span> <span data-ttu-id="8ab08-175">No caso do manifesto acima, ele percorrerá os seguintes componentes.</span><span class="sxs-lookup"><span data-stu-id="8ab08-175">For the manifest above, it will go through the following components.</span></span>  

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

<span data-ttu-id="8ab08-176">Qualquer componente que falhar na verificação será baixado pela ferramenta e reescrito no mesmo arquivo na unidade.</span><span class="sxs-lookup"><span data-stu-id="8ab08-176">Any component failing the verification will be downloaded by the tool and rewritten to the same file on the drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="8ab08-177">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8ab08-177">Next steps</span></span>
 
* [<span data-ttu-id="8ab08-178">Configurando a Ferramenta de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="8ab08-178">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="8ab08-179">Preparação de discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="8ab08-179">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="8ab08-180">Revisão do status do trabalho com arquivos de log de cópia</span><span class="sxs-lookup"><span data-stu-id="8ab08-180">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="8ab08-181">Reparação de um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="8ab08-181">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="8ab08-182">Solucionando problemas da Ferramenta de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="8ab08-182">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
