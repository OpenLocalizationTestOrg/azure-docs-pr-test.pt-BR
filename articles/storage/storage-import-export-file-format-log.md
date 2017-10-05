---
title: "Formato do arquivo de log da Importação/Exportação do Azure | Microsoft Docs"
description: "Saiba mais sobre o formato dos arquivos de log criados quando etapas são executadas para um trabalho do serviço de Importação/Exportação."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 16234ccaf13ce1d85cfd207ed4734e683070faa6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="fbdd9-103">Formato de arquivo de log de serviço de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="fbdd9-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="fbdd9-104">Quando o serviço de importação/exportação do Microsoft Azure executa uma ação em uma unidade como parte de um trabalho de importação ou exportação, os logs são gravados para bloquear blobs na conta de armazenamento associado ao trabalho.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-104">When the Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written to block blobs in the storage account associated with that job.</span></span>  
  
<span data-ttu-id="fbdd9-105">Há dois logs que podem ser gravados pelo serviço de importação/exportação:</span><span class="sxs-lookup"><span data-stu-id="fbdd9-105">There are two logs that may be written by the Import/Export service:</span></span>  
  
-   <span data-ttu-id="fbdd9-106">O log de erros sempre é gerado se ocorrer um erro.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-106">The error log is always generated in the event of an error.</span></span>  
  
-   <span data-ttu-id="fbdd9-107">O log detalhado não é habilitado por padrão, mas pode ser habilitado configurando a propriedade `EnableVerboseLog` em um [Trabalho Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou em uma operação de [Atualização de Propriedades do Trabalho](/rest/api/storageimportexport/jobs#Jobs_Update).</span><span class="sxs-lookup"><span data-stu-id="fbdd9-107">The verbose log is not enabled by default, but may be enabled by setting the `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="fbdd9-108">Local do arquivo de log</span><span class="sxs-lookup"><span data-stu-id="fbdd9-108">Log file location</span></span>  
<span data-ttu-id="fbdd9-109">Os logs são gravados para bloquear blobs no contêiner ou diretório virtual especificado pela configuração `ImportExportStatesPath`, que pode ser definida em um operação `Put Job`.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-109">The logs are written to block blobs in the container or virtual directory specified by the `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="fbdd9-110">O local no qual os logs são gravados depende de como a autenticação é especificada para o trabalho, junto com o valor especificado para `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-110">The location to which the logs are written depends on how authentication is specified for the job, together with the value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="fbdd9-111">A autenticação para o trabalho pode ser especificada por meio de uma chave de conta de armazenamento ou um contêiner SAS (assinatura de acesso compartilhado).</span><span class="sxs-lookup"><span data-stu-id="fbdd9-111">Authentication for the job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="fbdd9-112">O nome do contêiner ou diretório virtual pode ser o nome padrão de `waimportexport` ou outro nome de contêiner ou diretório virtual que você especificar.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-112">The name of the container or virtual directory may either be the default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="fbdd9-113">A tabela a seguir mostra as opções possíveis:</span><span class="sxs-lookup"><span data-stu-id="fbdd9-113">The table below shows the possible options:</span></span>  
  
|<span data-ttu-id="fbdd9-114">Método de autenticação</span><span class="sxs-lookup"><span data-stu-id="fbdd9-114">Authentication Method</span></span>|<span data-ttu-id="fbdd9-115">Valor de `ImportExportStatesPath`Elemento</span><span class="sxs-lookup"><span data-stu-id="fbdd9-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="fbdd9-116">Local dos Blobs de Log</span><span class="sxs-lookup"><span data-stu-id="fbdd9-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="fbdd9-117">Chave da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="fbdd9-117">Storage account key</span></span>|<span data-ttu-id="fbdd9-118">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="fbdd9-118">Default value</span></span>|<span data-ttu-id="fbdd9-119">Um contêiner denominado `waimportexport`, que é o contêiner padrão.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-119">A container named `waimportexport`, which is the default container.</span></span> <span data-ttu-id="fbdd9-120">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fbdd9-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="fbdd9-121">Chave da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="fbdd9-121">Storage account key</span></span>|<span data-ttu-id="fbdd9-122">Valores especificados pelo usuário</span><span class="sxs-lookup"><span data-stu-id="fbdd9-122">User-specified value</span></span>|<span data-ttu-id="fbdd9-123">Um contêiner nomeado pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-123">A container named by the user.</span></span> <span data-ttu-id="fbdd9-124">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="fbdd9-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="fbdd9-125">SAS do contêiner</span><span class="sxs-lookup"><span data-stu-id="fbdd9-125">Container SAS</span></span>|<span data-ttu-id="fbdd9-126">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="fbdd9-126">Default value</span></span>|<span data-ttu-id="fbdd9-127">Um diretório virtual chamado `waimportexport`, que é o nome padrão, sob o contêiner especificado na SAS.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-127">A virtual directory named `waimportexport`, which is the default name, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="fbdd9-128">Por exemplo, se a SAS especificada para o trabalho é `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, então o local do log será`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="fbdd9-128">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="fbdd9-129">SAS do contêiner</span><span class="sxs-lookup"><span data-stu-id="fbdd9-129">Container SAS</span></span>|<span data-ttu-id="fbdd9-130">Valores especificados pelo usuário</span><span class="sxs-lookup"><span data-stu-id="fbdd9-130">User-specified value</span></span>|<span data-ttu-id="fbdd9-131">Um diretório virtual nomeado pelo usuário, sob o contêiner especificado na SAS.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-131">A virtual directory named by the user, beneath the container specified in the SAS.</span></span><br /><br /> <span data-ttu-id="fbdd9-132">Por exemplo, se a SAS especificada para o trabalho é `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, e o diretório virtual especificado for denominado `mylogblobs`, então o local do log será `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-132">For example, if the SAS specified for the job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and the specified virtual directory is named `mylogblobs`, then the log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="fbdd9-133">Você pode recuperar a URL de erro e logs detalhados chamando a operação [Obter Trabalho](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate).</span><span class="sxs-lookup"><span data-stu-id="fbdd9-133">You can retrieve the URL for the error and verbose logs by calling the [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="fbdd9-134">Os logs estão disponíveis após a conclusão do processamento da unidade.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-134">The logs are available after processing of the drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="fbdd9-135">Formato do arquivo de log</span><span class="sxs-lookup"><span data-stu-id="fbdd9-135">Log file format</span></span>  
<span data-ttu-id="fbdd9-136">O formato para ambos os logs é o mesmo: um blob que contém descrições XML dos eventos ocorridos ao copiar blobs entre o disco rígido e a conta do cliente.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-136">The format for both logs is the same: a blob containing XML descriptions of the events that occurred while copying blobs between the hard drive and the customer's account.</span></span>  
  
<span data-ttu-id="fbdd9-137">O log detalhado contém informações completas sobre o status da operação de cópia para cada blob (para um trabalho de importação) ou arquivo (para um trabalho de exportação), enquanto que o log de erros contém apenas as informações para blobs ou arquivos que tiveram erros durante o trabalho de importação ou exportação.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-137">The verbose log contains complete information about the status of the copy operation for every blob (for an import job) or file (for an export job), whereas the error log contains only the information for blobs or files that encountered errors during the import or export job.</span></span>  
  
<span data-ttu-id="fbdd9-138">O formato de log detalhado é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-138">The verbose log format is shown below.</span></span> <span data-ttu-id="fbdd9-139">O log de erros tem a mesma estrutura, mas filtra operações bem-sucedidas.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-139">The error log has the same structure, but filters out successful operations.</span></span>  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

<span data-ttu-id="fbdd9-140">A tabela a seguir descreve os elementos do arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-140">The following table describes the elements of the log file.</span></span>  
  
|<span data-ttu-id="fbdd9-141">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="fbdd9-141">XML Element</span></span>|<span data-ttu-id="fbdd9-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="fbdd9-142">Type</span></span>|<span data-ttu-id="fbdd9-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="fbdd9-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="fbdd9-144">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="fbdd9-144">XML Element</span></span>|<span data-ttu-id="fbdd9-145">Representa um log de unidade.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="fbdd9-146">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-146">Attribute, String</span></span>|<span data-ttu-id="fbdd9-147">A versão do formato do log.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-147">The version of the log format.</span></span>|  
|`DriveId`|<span data-ttu-id="fbdd9-148">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-148">String</span></span>|<span data-ttu-id="fbdd9-149">Número de série do hardware da unidade.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-149">The drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="fbdd9-150">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-150">String</span></span>|<span data-ttu-id="fbdd9-151">Status do processamento da unidade.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-151">Status of the drive processing.</span></span> <span data-ttu-id="fbdd9-152">Consulte a tabela `Drive Status Codes` abaixo para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-152">See the `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="fbdd9-153">Elemento XML aninhado</span><span class="sxs-lookup"><span data-stu-id="fbdd9-153">Nested XML element</span></span>|<span data-ttu-id="fbdd9-154">Representa um blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="fbdd9-155">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-155">String</span></span>|<span data-ttu-id="fbdd9-156">O URI do blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-156">The URI of the blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="fbdd9-157">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-157">String</span></span>|<span data-ttu-id="fbdd9-158">Caminho relativo até o arquivo na unidade.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-158">The relative path to the file on the drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="fbdd9-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="fbdd9-159">DateTime</span></span>|<span data-ttu-id="fbdd9-160">A versão de instantâneo do blob, apenas para um trabalho de exportação.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-160">The snapshot version of the blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="fbdd9-161">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="fbdd9-161">Integer</span></span>|<span data-ttu-id="fbdd9-162">O comprimento total do blob em bytes.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-162">The total length of the blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="fbdd9-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="fbdd9-163">DateTime</span></span>|<span data-ttu-id="fbdd9-164">A data/hora em que o blob foi modificado pela última vez, apenas para um trabalho de exportação.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-164">The date/time that the blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="fbdd9-165">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-165">String</span></span>|<span data-ttu-id="fbdd9-166">A disposição de importação do blob, para um trabalho de importação.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-166">The import disposition of the blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="fbdd9-167">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-167">Attribute, String</span></span>|<span data-ttu-id="fbdd9-168">O status de disposição de importação.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-168">The status of the import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="fbdd9-169">Elemento XML aninhado</span><span class="sxs-lookup"><span data-stu-id="fbdd9-169">Nested XML element</span></span>|<span data-ttu-id="fbdd9-170">Representa uma lista de intervalos de página para um blobs de página.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="fbdd9-171">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="fbdd9-171">XML element</span></span>|<span data-ttu-id="fbdd9-172">Representa um intervalo de páginas.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="fbdd9-173">Atributo, inteiro</span><span class="sxs-lookup"><span data-stu-id="fbdd9-173">Attribute, Integer</span></span>|<span data-ttu-id="fbdd9-174">Iniciando o deslocamento do intervalo de página no blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-174">Starting offset of the page range in the blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="fbdd9-175">Atributo, inteiro</span><span class="sxs-lookup"><span data-stu-id="fbdd9-175">Attribute, Integer</span></span>|<span data-ttu-id="fbdd9-176">Comprimento em bytes do intervalo de página.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-176">Length in bytes of the page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="fbdd9-177">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-177">Attribute, String</span></span>|<span data-ttu-id="fbdd9-178">Hash de MD5 codificado para Base16 do intervalo de página.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-178">Base16-encoded MD5 hash of the page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="fbdd9-179">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-179">Attribute, String</span></span>|<span data-ttu-id="fbdd9-180">Status do processamento do intervalo de páginas.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-180">Status of processing the page range.</span></span>|  
|`BlockList`|<span data-ttu-id="fbdd9-181">Elemento XML aninhado</span><span class="sxs-lookup"><span data-stu-id="fbdd9-181">Nested XML element</span></span>|<span data-ttu-id="fbdd9-182">Representa uma lista de blocos para um blobs de bloco.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="fbdd9-183">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="fbdd9-183">XML element</span></span>|<span data-ttu-id="fbdd9-184">Representa um bloco.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="fbdd9-185">Atributo, inteiro</span><span class="sxs-lookup"><span data-stu-id="fbdd9-185">Attribute, Integer</span></span>|<span data-ttu-id="fbdd9-186">Iniciando o deslocamento do bloco no blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-186">Starting offset of the block in the blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="fbdd9-187">Atributo, inteiro</span><span class="sxs-lookup"><span data-stu-id="fbdd9-187">Attribute, Integer</span></span>|<span data-ttu-id="fbdd9-188">Comprimento em bytes do bloco.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-188">Length in bytes of the block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="fbdd9-189">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-189">Attribute, String</span></span>|<span data-ttu-id="fbdd9-190">ID do bloco.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-190">The block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="fbdd9-191">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-191">Attribute, String</span></span>|<span data-ttu-id="fbdd9-192">Hash de MD5 codificado para Base16 do bloco.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-192">Base16-encoded MD5 hash of the block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="fbdd9-193">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-193">Attribute, String</span></span>|<span data-ttu-id="fbdd9-194">Status do processamento do bloco.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-194">Status of processing the block.</span></span>|  
|`Metadata`|<span data-ttu-id="fbdd9-195">Elemento XML aninhado</span><span class="sxs-lookup"><span data-stu-id="fbdd9-195">Nested XML element</span></span>|<span data-ttu-id="fbdd9-196">Representa os metadados do blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-196">Represents the blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="fbdd9-197">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-197">Attribute, String</span></span>|<span data-ttu-id="fbdd9-198">Status de processamento dos metadados do blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-198">Status of processing of the blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="fbdd9-199">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-199">String</span></span>|<span data-ttu-id="fbdd9-200">Caminho relativo para o arquivo de metadados globais.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-200">Relative path to the global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="fbdd9-201">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-201">Attribute, String</span></span>|<span data-ttu-id="fbdd9-202">Hash de MD5 codificado para Base16 do arquivo global de metadados.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-202">Base16-encoded MD5 hash of the global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="fbdd9-203">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-203">String</span></span>|<span data-ttu-id="fbdd9-204">Caminho relativo para o arquivo de metadados.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-204">Relative path to the metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="fbdd9-205">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-205">Attribute, String</span></span>|<span data-ttu-id="fbdd9-206">Hash de MD5 codificado para Base16 do arquivo de metadados.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-206">Base16-encoded MD5 hash of the metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="fbdd9-207">Elemento XML aninhado</span><span class="sxs-lookup"><span data-stu-id="fbdd9-207">Nested XML element</span></span>|<span data-ttu-id="fbdd9-208">Representa as propriedades do blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-208">Represents the blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="fbdd9-209">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-209">Attribute, String</span></span>|<span data-ttu-id="fbdd9-210">Status do processamento de propriedades de blob, por exemplo, arquivo não encontrado, concluído.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-210">Status of processing the blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="fbdd9-211">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-211">String</span></span>|<span data-ttu-id="fbdd9-212">Caminho relativo para o arquivo global de propriedades.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-212">Relative path to the global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="fbdd9-213">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-213">Attribute, String</span></span>|<span data-ttu-id="fbdd9-214">Hash de MD5 codificado para Base16 do arquivo global de propriedades.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-214">Base16-encoded MD5 hash of the global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="fbdd9-215">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-215">String</span></span>|<span data-ttu-id="fbdd9-216">Caminho relativo para o arquivo de propriedades.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-216">Relative path to the properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="fbdd9-217">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-217">Attribute, String</span></span>|<span data-ttu-id="fbdd9-218">Hash de MD5 codificado para Base16 do arquivo de propriedades.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-218">Base16-encoded MD5 hash of the properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="fbdd9-219">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="fbdd9-219">String</span></span>|<span data-ttu-id="fbdd9-220">Status do processamento do blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-220">Status of processing the blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="fbdd9-221">Códigos de status da unidade</span><span class="sxs-lookup"><span data-stu-id="fbdd9-221">Drive status codes</span></span>  
<span data-ttu-id="fbdd9-222">A tabela a seguir lista os códigos de status para o processamento de uma unidade.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-222">The following table lists the status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="fbdd9-223">Código de status</span><span class="sxs-lookup"><span data-stu-id="fbdd9-223">Status code</span></span>|<span data-ttu-id="fbdd9-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="fbdd9-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="fbdd9-225">A unidade concluiu o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-225">The drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="fbdd9-226">A unidade concluiu o processamento com avisos em um ou mais blobs de acordo com as disposições de importação especificadas para os blobs.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-226">The drive has finished processing with warnings in one or more blobs per the import dispositions specified for the blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="fbdd9-227">A unidade foi concluída com erros em um ou mais blobs ou partes.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-227">The drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="fbdd9-228">Nenhum disco foi encontrado na unidade.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-228">No disk is found on the drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="fbdd9-229">O primeiro volume de dados no disco não está no formato NTFS.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-229">The first data volume on the disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="fbdd9-230">Uma falha desconhecida ocorreu ao executar operações na unidade.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-230">An unknown failure occurred when performing operations on the drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="fbdd9-231">Nenhum volume criptografável BitLocker foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="fbdd9-232">O BitLocker não está habilitado no volume.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-232">BitLocker is not enabled on the volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="fbdd9-233">O protetor de chave de senha numérica não existe no volume.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-233">The numerical password key protector does not exist on the volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="fbdd9-234">A senha numérica fornecida não é pode desbloquear o volume.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-234">The numerical password provided cannot unlock the volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="fbdd9-235">Uma falha desconhecida ocorreu ao tentar desbloquear o volume.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-235">Unknown failure has happened when trying to unlock the volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="fbdd9-236">Uma falha desconhecida ocorreu ao executar operações BitLocker.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="fbdd9-237">O nome do arquivo de manifesto é inválido.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-237">The manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="fbdd9-238">O nome do arquivo de manifesto é muito longo.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-238">The manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="fbdd9-239">O arquivo de manifesto não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-239">The manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="fbdd9-240">Acesso ao arquivo de manifesto foi negado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-240">Access to the manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="fbdd9-241">O arquivo de manifesto está corrompido (o conteúdo não corresponde ao seu hash).</span><span class="sxs-lookup"><span data-stu-id="fbdd9-241">The manifest file is corrupted (the content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="fbdd9-242">O conteúdo do manifesto não corresponde ao formato necessário.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-242">The manifest content does not conform to the required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="fbdd9-243">A ID de unidade no arquivo de manifesto não corresponde à leitura do disco.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-243">The drive ID in the manifest file does not match the one read from the drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="fbdd9-244">Ocorreu uma falha de E/S de disco durante a leitura do manifesto.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-244">A disk I/O failure occurred while reading from the manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="fbdd9-245">A lista de blob de exportação não corresponde ao formato necessário.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-245">The export blob list blob does not conform to the required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="fbdd9-246">O acesso aos blobs na conta de armazenamento é proibido.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-246">Access to the blobs in the storage account is forbidden.</span></span> <span data-ttu-id="fbdd9-247">Isso pode ser devido a uma chave da conta de armazenamento inválida ou SAS do contêiner.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-247">This might be due to invalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="fbdd9-248">Ocorreu um erro interno durante o processamento da unidade.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-248">And internal error occurred while processing the drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="fbdd9-249">Códigos de status de blobs</span><span class="sxs-lookup"><span data-stu-id="fbdd9-249">Blob status codes</span></span>  
<span data-ttu-id="fbdd9-250">A tabela a seguir lista os códigos de status para o processamento de um blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-250">The following table lists the status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="fbdd9-251">Código de status</span><span class="sxs-lookup"><span data-stu-id="fbdd9-251">Status code</span></span>|<span data-ttu-id="fbdd9-252">Descrição</span><span class="sxs-lookup"><span data-stu-id="fbdd9-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="fbdd9-253">O blob concluiu o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-253">The blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="fbdd9-254">O blob concluiu o processamento com erros em um ou mais intervalos de páginas ou blocos, metadados ou propriedades.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-254">The blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="fbdd9-255">O nome do arquivo é inválido.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-255">The file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="fbdd9-256">O nome do arquivo é muito longo.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-256">The file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="fbdd9-257">O arquivo não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-257">The file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="fbdd9-258">Acesso ao arquivo foi negado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-258">Access to the file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="fbdd9-259">A solicitação de serviço Blob para acessar o blob falhou.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-259">The Blob service request to access the blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="fbdd9-260">A solicitação de serviço Blob para acessar o blob é proibida.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-260">The Blob service request to access the blob is forbidden.</span></span> <span data-ttu-id="fbdd9-261">Isso pode ser devido a uma chave da conta de armazenamento inválida ou SAS do contêiner.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-261">This might be due to invalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="fbdd9-262">Falha ao renomear o blob (para um trabalho de importação) ou o arquivo (para um trabalho de exportação).</span><span class="sxs-lookup"><span data-stu-id="fbdd9-262">Failed to rename the blob (for an import job) or the file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="fbdd9-263">Ocorreu uma alteração inesperada com o blob (para um trabalho de exportação).</span><span class="sxs-lookup"><span data-stu-id="fbdd9-263">An unexpected change has occurred with the blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="fbdd9-264">Há uma concessão no blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-264">There is a lease present on the blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="fbdd9-265">Uma falha de E/S de disco ou rede ocorreu durante o processamento de blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-265">A disk or network I/O failure occurred while processing the blob.</span></span>|  
|`Failed`|<span data-ttu-id="fbdd9-266">Uma falha desconhecida ocorreu durante o processamento de blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-266">An unknown failure occurred while processing the blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="fbdd9-267">Códigos de status de disposição de importação</span><span class="sxs-lookup"><span data-stu-id="fbdd9-267">Import disposition status codes</span></span>  
<span data-ttu-id="fbdd9-268">A tabela a seguir lista os códigos de status para resolver uma disposição de importação.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-268">The following table lists the status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="fbdd9-269">Código de status</span><span class="sxs-lookup"><span data-stu-id="fbdd9-269">Status code</span></span>|<span data-ttu-id="fbdd9-270">Descrição</span><span class="sxs-lookup"><span data-stu-id="fbdd9-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="fbdd9-271">O blob foi criado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-271">The blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="fbdd9-272">O blob foi renomeado de acordo com a disposição de importação de renomeação.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-272">The blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="fbdd9-273">O elemento `Blob/BlobPath` contém o URI para o blob renomeado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-273">The `Blob/BlobPath` element contains the URI for the renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="fbdd9-274">O blob foi ignorado de acordo com a disposição de importação `no-overwrite`.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-274">The blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="fbdd9-275">O blob substituiu um blob existente de acordo com a disposição de importação `overwrite`.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-275">The blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="fbdd9-276">Uma falha anterior interrompeu o processamento da disposição de importação.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-276">A prior failure has stopped further processing of the import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="fbdd9-277">Códigos de status do intervalo de página/bloco</span><span class="sxs-lookup"><span data-stu-id="fbdd9-277">Page range/block status codes</span></span>  
<span data-ttu-id="fbdd9-278">A tabela a seguir lista os códigos de status para o processamento de um intervalo de páginas ou de um bloco.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-278">The following table lists the status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="fbdd9-279">Código de status</span><span class="sxs-lookup"><span data-stu-id="fbdd9-279">Status code</span></span>|<span data-ttu-id="fbdd9-280">Descrição</span><span class="sxs-lookup"><span data-stu-id="fbdd9-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="fbdd9-281">O intervalo de páginas ou bloco concluiu o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-281">The page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="fbdd9-282">O bloco foi confirmado, mas não na lista completa de blocos porque outros blocos têm falha ou a própria lista de blocos falhou.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-282">The block has been committed,  but not in the full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="fbdd9-283">O bloco foi carregado, mas não foi confirmado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-283">The block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="fbdd9-284">O intervalo de páginas ou bloco está corrompido (o conteúdo não corresponde ao seu hash).</span><span class="sxs-lookup"><span data-stu-id="fbdd9-284">The page range or block is corrupted (the content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="fbdd9-285">Fim de arquivo inesperado foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="fbdd9-286">Fim de blob inesperado foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="fbdd9-287">A solicitação de serviço Blob para acessar o intervalo de páginas ou bloco falhou.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-287">The Blob service request to access the page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="fbdd9-288">Uma falha de E/S de disco ou rede ocorreu durante o processamento do intervalo de páginas ou bloco.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-288">A disk or network I/O failure occurred while processing the page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="fbdd9-289">Uma falha desconhecida ocorreu durante o processamento do intervalo de páginas ou bloco.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-289">An unknown failure occurred while processing the page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="fbdd9-290">Uma falha anterior interrompeu o processamento do intervalo de páginas ou bloco.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-290">A prior failure has stopped further processing of the page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="fbdd9-291">Códigos de status de metadados</span><span class="sxs-lookup"><span data-stu-id="fbdd9-291">Metadata status codes</span></span>  
<span data-ttu-id="fbdd9-292">A tabela a seguir lista os códigos de status para o processamento dos metadados do blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-292">The following table lists the status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="fbdd9-293">Código de status</span><span class="sxs-lookup"><span data-stu-id="fbdd9-293">Status code</span></span>|<span data-ttu-id="fbdd9-294">Descrição</span><span class="sxs-lookup"><span data-stu-id="fbdd9-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="fbdd9-295">Os metadados concluíram o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-295">The metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="fbdd9-296">O nome do arquivo de metadados é inválido.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-296">The metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="fbdd9-297">O nome do arquivo de metadados é muito longo.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-297">The metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="fbdd9-298">O arquivo de metadados não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-298">The metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="fbdd9-299">Acesso ao arquivo de metadados foi negado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-299">Access to the metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="fbdd9-300">O arquivo de metadados está corrompido (o conteúdo não corresponde ao seu hash).</span><span class="sxs-lookup"><span data-stu-id="fbdd9-300">The metadata file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="fbdd9-301">O conteúdo dos metadados não corresponde ao formato necessário.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-301">The metadata content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="fbdd9-302">A gravação de metadados XML falhou.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-302">Writing the metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="fbdd9-303">A solicitação de serviço Blob para acessar os metadados falhou.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-303">The Blob service request to access the metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="fbdd9-304">Uma falha de E/S de disco ou rede ocorreu durante o processamento dos metadados.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-304">A disk or network I/O failure occurred while processing the metadata.</span></span>|  
|`Failed`|<span data-ttu-id="fbdd9-305">Uma falha desconhecida ocorreu durante o processamento dos metadados.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-305">An unknown failure occurred while processing the metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="fbdd9-306">Uma falha anterior interrompeu o processamento dos metadados.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-306">A prior failure has stopped further processing of the metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="fbdd9-307">Códigos de status das propriedades</span><span class="sxs-lookup"><span data-stu-id="fbdd9-307">Properties status codes</span></span>  
<span data-ttu-id="fbdd9-308">A tabela a seguir lista os códigos de status para o processamento das propriedades do blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-308">The following table lists the status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="fbdd9-309">Código de status</span><span class="sxs-lookup"><span data-stu-id="fbdd9-309">Status code</span></span>|<span data-ttu-id="fbdd9-310">Descrição</span><span class="sxs-lookup"><span data-stu-id="fbdd9-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="fbdd9-311">As propriedades concluíram o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-311">The properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="fbdd9-312">O nome do arquivo de propriedades é inválido.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-312">The properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="fbdd9-313">O nome do arquivo de propriedades é muito longo.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-313">The properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="fbdd9-314">O arquivo de propriedades não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-314">The properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="fbdd9-315">O acesso ao arquivo de propriedades foi negado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-315">Access to the properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="fbdd9-316">O arquivo de propriedades está corrompido (o conteúdo não corresponde ao seu hash).</span><span class="sxs-lookup"><span data-stu-id="fbdd9-316">The properties file is corrupted (the content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="fbdd9-317">O conteúdo das propriedades não corresponde ao formato necessário.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-317">The properties content does not conform to the required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="fbdd9-318">Falha ao gravar as propriedades XML.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-318">Writing the properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="fbdd9-319">A solicitação de serviço Blob para acessar as propriedades falhou.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-319">The Blob service request to access the properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="fbdd9-320">Uma falha de E/S de disco ou rede ocorreu durante o processamento das propriedades.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-320">A disk or network I/O failure occurred while processing the properties.</span></span>|  
|`Failed`|<span data-ttu-id="fbdd9-321">Uma falha desconhecida ocorreu durante o processamento das propriedades.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-321">An unknown failure occurred while processing the properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="fbdd9-322">Uma falha anterior interrompeu o processamento das propriedades.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-322">A prior failure has stopped further processing of the properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="fbdd9-323">Logs de exemplo</span><span class="sxs-lookup"><span data-stu-id="fbdd9-323">Sample logs</span></span>  
<span data-ttu-id="fbdd9-324">A seguir está um exemplo de log detalhado.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-324">The following is an example of verbose log.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="fbdd9-325">O log de erros correspondente é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-325">The corresponding error log is shown below.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 <span data-ttu-id="fbdd9-326">O log de erros a seguir para um trabalho de importação contém um erro sobre um arquivo não encontrado na unidade de importação.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-326">The follow error log for an import job contains an error about a file not found on the import drive.</span></span> <span data-ttu-id="fbdd9-327">Observe que o status dos componentes subsequentes é `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-327">Note that the status of subsequent components is `Cancelled`.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

<span data-ttu-id="fbdd9-328">O log de erros a seguir para um trabalho de exportação indica que o conteúdo do blob foi gravado com êxito na unidade, mas ocorreu um erro ao exportar as propriedades do blob.</span><span class="sxs-lookup"><span data-stu-id="fbdd9-328">The following error log for an export job indicates that the blob content has been successfully written to the drive, but that an error occurred while exporting the blob's properties.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a><span data-ttu-id="fbdd9-329">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fbdd9-329">Next steps</span></span>
 
* [<span data-ttu-id="fbdd9-330">API REST de Importação/Exportação do Armazenamento</span><span class="sxs-lookup"><span data-stu-id="fbdd9-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
