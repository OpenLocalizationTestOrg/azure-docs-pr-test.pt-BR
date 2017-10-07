---
title: "formato de arquivo de log de importação/exportação aaaAzure | Microsoft Docs"
description: "Saiba mais sobre o formato Olá Olá de arquivos de log criados quando as etapas são executadas para um trabalho do serviço de importação/exportação."
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
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="5b96b-103">Formato de arquivo de log de serviço de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="5b96b-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="5b96b-104">Quando Olá serviço de importação/exportação do Microsoft Azure executa uma ação em uma unidade como parte de um trabalho de importação ou exportação, os logs são gravados tooblock blobs na conta de armazenamento Olá associada ao trabalho.</span><span class="sxs-lookup"><span data-stu-id="5b96b-104">When hello Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written tooblock blobs in hello storage account associated with that job.</span></span>  
  
<span data-ttu-id="5b96b-105">Há dois logs que podem ser gravados pelo Olá serviço de importação/exportação:</span><span class="sxs-lookup"><span data-stu-id="5b96b-105">There are two logs that may be written by hello Import/Export service:</span></span>  
  
-   <span data-ttu-id="5b96b-106">log de erros de saudação sempre é gerada no evento de saudação do erro.</span><span class="sxs-lookup"><span data-stu-id="5b96b-106">hello error log is always generated in hello event of an error.</span></span>  
  
-   <span data-ttu-id="5b96b-107">Hello log detalhado não é habilitado por padrão, mas pode ser habilitado pela configuração Olá `EnableVerboseLog` propriedade em uma [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-107">hello verbose log is not enabled by default, but may be enabled by setting hello `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="5b96b-108">Local do arquivo de log</span><span class="sxs-lookup"><span data-stu-id="5b96b-108">Log file location</span></span>  
<span data-ttu-id="5b96b-109">Olá os logs são gravados tooblock blobs no contêiner de saudação ou diretório virtual especificado pelo Olá `ImportExportStatesPath` configuração, que você pode definir em uma `Put Job` operação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-109">hello logs are written tooblock blobs in hello container or virtual directory specified by hello `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="5b96b-110">Olá local toowhich Olá os logs são gravados depende de como a autenticação é especificada para o trabalho de hello, junto com o valor de saudação especificado para `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="5b96b-110">hello location toowhich hello logs are written depends on how authentication is specified for hello job, together with hello value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="5b96b-111">A autenticação para o trabalho de saudação pode ser especificada por meio de uma chave de conta de armazenamento ou um contêiner de SAS (assinatura de acesso compartilhado).</span><span class="sxs-lookup"><span data-stu-id="5b96b-111">Authentication for hello job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="5b96b-112">nome de saudação do diretório virtual ou contêiner Olá pode ser o nome padrão de saudação do `waimportexport`, ou em outro contêiner ou nome do diretório virtual que você especificar.</span><span class="sxs-lookup"><span data-stu-id="5b96b-112">hello name of hello container or virtual directory may either be hello default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="5b96b-113">Olá tabela a seguir mostra as opções possíveis hello:</span><span class="sxs-lookup"><span data-stu-id="5b96b-113">hello table below shows hello possible options:</span></span>  
  
|<span data-ttu-id="5b96b-114">Método de autenticação</span><span class="sxs-lookup"><span data-stu-id="5b96b-114">Authentication Method</span></span>|<span data-ttu-id="5b96b-115">Valor de `ImportExportStatesPath`Elemento</span><span class="sxs-lookup"><span data-stu-id="5b96b-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="5b96b-116">Local dos Blobs de Log</span><span class="sxs-lookup"><span data-stu-id="5b96b-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="5b96b-117">Chave da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5b96b-117">Storage account key</span></span>|<span data-ttu-id="5b96b-118">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="5b96b-118">Default value</span></span>|<span data-ttu-id="5b96b-119">Um contêiner denominado `waimportexport`, que é o contêiner padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-119">A container named `waimportexport`, which is hello default container.</span></span> <span data-ttu-id="5b96b-120">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5b96b-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="5b96b-121">Chave da conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5b96b-121">Storage account key</span></span>|<span data-ttu-id="5b96b-122">Valores especificados pelo usuário</span><span class="sxs-lookup"><span data-stu-id="5b96b-122">User-specified value</span></span>|<span data-ttu-id="5b96b-123">Um contêiner nomeado pelo usuário hello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-123">A container named by hello user.</span></span> <span data-ttu-id="5b96b-124">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="5b96b-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="5b96b-125">SAS do contêiner</span><span class="sxs-lookup"><span data-stu-id="5b96b-125">Container SAS</span></span>|<span data-ttu-id="5b96b-126">Valor padrão</span><span class="sxs-lookup"><span data-stu-id="5b96b-126">Default value</span></span>|<span data-ttu-id="5b96b-127">Um diretório virtual chamado `waimportexport`, que é o nome do padrão de saudação, recipiente de saudação especificado no hello SAS.</span><span class="sxs-lookup"><span data-stu-id="5b96b-127">A virtual directory named `waimportexport`, which is hello default name, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="5b96b-128">Por exemplo, se Olá SAS especificada para o trabalho de Olá for `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, Olá log local será`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="5b96b-128">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="5b96b-129">SAS do contêiner</span><span class="sxs-lookup"><span data-stu-id="5b96b-129">Container SAS</span></span>|<span data-ttu-id="5b96b-130">Valores especificados pelo usuário</span><span class="sxs-lookup"><span data-stu-id="5b96b-130">User-specified value</span></span>|<span data-ttu-id="5b96b-131">Um diretório virtual denominado pelo usuário hello, recipiente de saudação especificado no hello SAS.</span><span class="sxs-lookup"><span data-stu-id="5b96b-131">A virtual directory named by hello user, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="5b96b-132">Por exemplo, se Olá SAS especificada para o trabalho de Olá for `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, e Olá especificado o diretório virtual é denominado `mylogblobs`, Olá log local será `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="5b96b-132">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and hello specified virtual directory is named `mylogblobs`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="5b96b-133">Você pode recuperar Olá URL logs detalhados e de erro Olá Olá chamada [obter trabalho](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-133">You can retrieve hello URL for hello error and verbose logs by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="5b96b-134">Olá logs estão disponíveis após a conclusão do processamento da unidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-134">hello logs are available after processing of hello drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="5b96b-135">Formato do arquivo de log</span><span class="sxs-lookup"><span data-stu-id="5b96b-135">Log file format</span></span>  
<span data-ttu-id="5b96b-136">Olá formato para ambos os logs é Olá mesmo: um blob que contém descrições XML dos eventos de Olá ocorridos ao copiar blobs entre o disco rígido hello e conta saudação do cliente.</span><span class="sxs-lookup"><span data-stu-id="5b96b-136">hello format for both logs is hello same: a blob containing XML descriptions of hello events that occurred while copying blobs between hello hard drive and hello customer's account.</span></span>  
  
<span data-ttu-id="5b96b-137">log detalhado Olá contém informações completas sobre o status de Olá Olá operação de cópia para cada blob (para um trabalho de importação) ou arquivo (para um trabalho de exportação), enquanto o log de erros de saudação contém apenas informações de saudação de blobs ou arquivos que encontraram erros durante a saudação Importar ou exportar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="5b96b-137">hello verbose log contains complete information about hello status of hello copy operation for every blob (for an import job) or file (for an export job), whereas hello error log contains only hello information for blobs or files that encountered errors during hello import or export job.</span></span>  
  
<span data-ttu-id="5b96b-138">formato de log detalhado de saudação é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="5b96b-138">hello verbose log format is shown below.</span></span> <span data-ttu-id="5b96b-139">log de erros de saudação tem Olá a mesma estrutura, mas filtra operações bem-sucedidas.</span><span class="sxs-lookup"><span data-stu-id="5b96b-139">hello error log has hello same structure, but filters out successful operations.</span></span>  

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

<span data-ttu-id="5b96b-140">Olá tabela a seguir descreve os elementos de Olá Olá do arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="5b96b-140">hello following table describes hello elements of hello log file.</span></span>  
  
|<span data-ttu-id="5b96b-141">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="5b96b-141">XML Element</span></span>|<span data-ttu-id="5b96b-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="5b96b-142">Type</span></span>|<span data-ttu-id="5b96b-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="5b96b-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="5b96b-144">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="5b96b-144">XML Element</span></span>|<span data-ttu-id="5b96b-145">Representa um log de unidade.</span><span class="sxs-lookup"><span data-stu-id="5b96b-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="5b96b-146">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-146">Attribute, String</span></span>|<span data-ttu-id="5b96b-147">versão de saudação do formato de log hello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-147">hello version of hello log format.</span></span>|  
|`DriveId`|<span data-ttu-id="5b96b-148">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-148">String</span></span>|<span data-ttu-id="5b96b-149">Olá número de série do hardware da unidade.</span><span class="sxs-lookup"><span data-stu-id="5b96b-149">hello drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="5b96b-150">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-150">String</span></span>|<span data-ttu-id="5b96b-151">Status do processamento de unidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-151">Status of hello drive processing.</span></span> <span data-ttu-id="5b96b-152">Consulte Olá `Drive Status Codes` tabela abaixo para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="5b96b-152">See hello `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="5b96b-153">Elemento XML aninhado</span><span class="sxs-lookup"><span data-stu-id="5b96b-153">Nested XML element</span></span>|<span data-ttu-id="5b96b-154">Representa um blob.</span><span class="sxs-lookup"><span data-stu-id="5b96b-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="5b96b-155">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-155">String</span></span>|<span data-ttu-id="5b96b-156">Olá URI do blob hello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-156">hello URI of hello blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="5b96b-157">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-157">String</span></span>|<span data-ttu-id="5b96b-158">arquivo de toohello de caminho relativo de saudação na unidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-158">hello relative path toohello file on hello drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="5b96b-159">Datetime</span><span class="sxs-lookup"><span data-stu-id="5b96b-159">DateTime</span></span>|<span data-ttu-id="5b96b-160">versão do instantâneo de saudação do blob hello, para um trabalho de exportação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-160">hello snapshot version of hello blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="5b96b-161">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="5b96b-161">Integer</span></span>|<span data-ttu-id="5b96b-162">tamanho total de saudação do blob de saudação em bytes.</span><span class="sxs-lookup"><span data-stu-id="5b96b-162">hello total length of hello blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="5b96b-163">Datetime</span><span class="sxs-lookup"><span data-stu-id="5b96b-163">DateTime</span></span>|<span data-ttu-id="5b96b-164">saudação de data/hora blob Olá da última modificação, para um trabalho de exportação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-164">hello date/time that hello blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="5b96b-165">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-165">String</span></span>|<span data-ttu-id="5b96b-166">Olá disposição de blob hello, para um trabalho de importação de importação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-166">hello import disposition of hello blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="5b96b-167">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-167">Attribute, String</span></span>|<span data-ttu-id="5b96b-168">status de saudação do hello disposição de importação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-168">hello status of hello import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="5b96b-169">Elemento XML aninhado</span><span class="sxs-lookup"><span data-stu-id="5b96b-169">Nested XML element</span></span>|<span data-ttu-id="5b96b-170">Representa uma lista de intervalos de página para um blobs de página.</span><span class="sxs-lookup"><span data-stu-id="5b96b-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="5b96b-171">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="5b96b-171">XML element</span></span>|<span data-ttu-id="5b96b-172">Representa um intervalo de páginas.</span><span class="sxs-lookup"><span data-stu-id="5b96b-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="5b96b-173">Atributo, inteiro</span><span class="sxs-lookup"><span data-stu-id="5b96b-173">Attribute, Integer</span></span>|<span data-ttu-id="5b96b-174">Iniciando o deslocamento do intervalo de página Olá no blob hello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-174">Starting offset of hello page range in hello blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="5b96b-175">Atributo, inteiro</span><span class="sxs-lookup"><span data-stu-id="5b96b-175">Attribute, Integer</span></span>|<span data-ttu-id="5b96b-176">Comprimento em bytes do intervalo de páginas de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-176">Length in bytes of hello page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="5b96b-177">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-177">Attribute, String</span></span>|<span data-ttu-id="5b96b-178">Hash de MD5 codificado para Base16 do intervalo de página hello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-178">Base16-encoded MD5 hash of hello page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="5b96b-179">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-179">Attribute, String</span></span>|<span data-ttu-id="5b96b-180">Status do processamento do intervalo de páginas de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-180">Status of processing hello page range.</span></span>|  
|`BlockList`|<span data-ttu-id="5b96b-181">Elemento XML aninhado</span><span class="sxs-lookup"><span data-stu-id="5b96b-181">Nested XML element</span></span>|<span data-ttu-id="5b96b-182">Representa uma lista de blocos para um blobs de bloco.</span><span class="sxs-lookup"><span data-stu-id="5b96b-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="5b96b-183">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="5b96b-183">XML element</span></span>|<span data-ttu-id="5b96b-184">Representa um bloco.</span><span class="sxs-lookup"><span data-stu-id="5b96b-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="5b96b-185">Atributo, inteiro</span><span class="sxs-lookup"><span data-stu-id="5b96b-185">Attribute, Integer</span></span>|<span data-ttu-id="5b96b-186">Iniciando o deslocamento do bloco de saudação no blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-186">Starting offset of hello block in hello blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="5b96b-187">Atributo, inteiro</span><span class="sxs-lookup"><span data-stu-id="5b96b-187">Attribute, Integer</span></span>|<span data-ttu-id="5b96b-188">Comprimento em bytes do bloco de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-188">Length in bytes of hello block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="5b96b-189">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-189">Attribute, String</span></span>|<span data-ttu-id="5b96b-190">ID do bloco de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-190">hello block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="5b96b-191">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-191">Attribute, String</span></span>|<span data-ttu-id="5b96b-192">Hash de MD5 codificado para Base16 do bloco de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-192">Base16-encoded MD5 hash of hello block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="5b96b-193">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-193">Attribute, String</span></span>|<span data-ttu-id="5b96b-194">Status do processamento de bloco hello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-194">Status of processing hello block.</span></span>|  
|`Metadata`|<span data-ttu-id="5b96b-195">Elemento XML aninhado</span><span class="sxs-lookup"><span data-stu-id="5b96b-195">Nested XML element</span></span>|<span data-ttu-id="5b96b-196">Representa os metadados do blob hello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-196">Represents hello blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="5b96b-197">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-197">Attribute, String</span></span>|<span data-ttu-id="5b96b-198">Status do processamento dos metadados de blob hello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-198">Status of processing of hello blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="5b96b-199">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-199">String</span></span>|<span data-ttu-id="5b96b-200">Arquivo de metadados globais de toohello caminho relativo.</span><span class="sxs-lookup"><span data-stu-id="5b96b-200">Relative path toohello global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="5b96b-201">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-201">Attribute, String</span></span>|<span data-ttu-id="5b96b-202">Hash de MD5 codificado para Base16 do arquivo de metadados globais hello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-202">Base16-encoded MD5 hash of hello global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="5b96b-203">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-203">String</span></span>|<span data-ttu-id="5b96b-204">Arquivo de metadados do caminho relativo toohello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-204">Relative path toohello metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="5b96b-205">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-205">Attribute, String</span></span>|<span data-ttu-id="5b96b-206">Hash de MD5 codificado para Base16 do arquivo de metadados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-206">Base16-encoded MD5 hash of hello metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="5b96b-207">Elemento XML aninhado</span><span class="sxs-lookup"><span data-stu-id="5b96b-207">Nested XML element</span></span>|<span data-ttu-id="5b96b-208">Representa as propriedades de blob hello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-208">Represents hello blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="5b96b-209">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-209">Attribute, String</span></span>|<span data-ttu-id="5b96b-210">Status do processamento propriedades de blob hello, por exemplo, o arquivo não encontrado, concluído.</span><span class="sxs-lookup"><span data-stu-id="5b96b-210">Status of processing hello blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="5b96b-211">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-211">String</span></span>|<span data-ttu-id="5b96b-212">Arquivo de propriedades globais de toohello caminho relativo.</span><span class="sxs-lookup"><span data-stu-id="5b96b-212">Relative path toohello global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="5b96b-213">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-213">Attribute, String</span></span>|<span data-ttu-id="5b96b-214">Hash de MD5 codificado para Base16 do arquivo de propriedades globais de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-214">Base16-encoded MD5 hash of hello global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="5b96b-215">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-215">String</span></span>|<span data-ttu-id="5b96b-216">Arquivo de propriedades de toohello de caminho relativo.</span><span class="sxs-lookup"><span data-stu-id="5b96b-216">Relative path toohello properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="5b96b-217">Atributo, cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-217">Attribute, String</span></span>|<span data-ttu-id="5b96b-218">Hash de MD5 codificado para Base16 do arquivo de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-218">Base16-encoded MD5 hash of hello properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="5b96b-219">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="5b96b-219">String</span></span>|<span data-ttu-id="5b96b-220">Status do processamento Olá blob.</span><span class="sxs-lookup"><span data-stu-id="5b96b-220">Status of processing hello blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="5b96b-221">Códigos de status da unidade</span><span class="sxs-lookup"><span data-stu-id="5b96b-221">Drive status codes</span></span>  
<span data-ttu-id="5b96b-222">Olá tabela a seguir lista os códigos de status de saudação para uma unidade de processamento.</span><span class="sxs-lookup"><span data-stu-id="5b96b-222">hello following table lists hello status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="5b96b-223">Código de status</span><span class="sxs-lookup"><span data-stu-id="5b96b-223">Status code</span></span>|<span data-ttu-id="5b96b-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="5b96b-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="5b96b-225">Olá unidade concluiu o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="5b96b-225">hello drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="5b96b-226">Olá unidade concluiu o processamento com avisos em um ou mais blobs por disposições de importação de saudação especificados para blobs de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-226">hello drive has finished processing with warnings in one or more blobs per hello import dispositions specified for hello blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="5b96b-227">Olá unidade foi concluída com erros em um ou mais blobs ou partes.</span><span class="sxs-lookup"><span data-stu-id="5b96b-227">hello drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="5b96b-228">Nenhum disco foi encontrado na unidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-228">No disk is found on hello drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="5b96b-229">Olá primeiro volume de dados em disco Olá não está no formato NTFS.</span><span class="sxs-lookup"><span data-stu-id="5b96b-229">hello first data volume on hello disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="5b96b-230">Falha desconhecida ocorreu ao executar operações na unidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-230">An unknown failure occurred when performing operations on hello drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="5b96b-231">Nenhum volume criptografável BitLocker foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="5b96b-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="5b96b-232">O BitLocker não está habilitado no volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-232">BitLocker is not enabled on hello volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="5b96b-233">protetor de senha numérica de saudação não existe no volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-233">hello numerical password key protector does not exist on hello volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="5b96b-234">senha numérica de saudação fornecida não é possível desbloquear o volume de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-234">hello numerical password provided cannot unlock hello volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="5b96b-235">Falha desconhecida ocorreu durante a tentativa de volume de saudação toounlock.</span><span class="sxs-lookup"><span data-stu-id="5b96b-235">Unknown failure has happened when trying toounlock hello volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="5b96b-236">Uma falha desconhecida ocorreu ao executar operações BitLocker.</span><span class="sxs-lookup"><span data-stu-id="5b96b-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="5b96b-237">Olá nome de arquivo de manifesto é inválido.</span><span class="sxs-lookup"><span data-stu-id="5b96b-237">hello manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="5b96b-238">nome do arquivo de manifesto de saudação é muito longo.</span><span class="sxs-lookup"><span data-stu-id="5b96b-238">hello manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="5b96b-239">arquivo de manifesto Olá não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="5b96b-239">hello manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="5b96b-240">Arquivo de manifesto de toohello de acesso é negado.</span><span class="sxs-lookup"><span data-stu-id="5b96b-240">Access toohello manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="5b96b-241">Olá arquivo de manifesto está corrompido (Olá conteúdo não corresponde ao seu hash).</span><span class="sxs-lookup"><span data-stu-id="5b96b-241">hello manifest file is corrupted (hello content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="5b96b-242">conteúdo do manifesto Olá não está de acordo com formato necessário toohello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-242">hello manifest content does not conform toohello required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="5b96b-243">unidade Olá ID no arquivo de manifesto Olá não coincide Olá leitura da unidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-243">hello drive ID in hello manifest file does not match hello one read from hello drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="5b96b-244">Ocorreu uma falha de e/s de disco durante a leitura do manifesto de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-244">A disk I/O failure occurred while reading from hello manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="5b96b-245">Olá exportar lista de blob não está de acordo com formato necessário toohello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-245">hello export blob list blob does not conform toohello required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="5b96b-246">Acessar toohello blobs na conta de armazenamento Olá é proibido.</span><span class="sxs-lookup"><span data-stu-id="5b96b-246">Access toohello blobs in hello storage account is forbidden.</span></span> <span data-ttu-id="5b96b-247">Isso pode ser devido a chave de conta de armazenamento tooinvalid ou SAS do contêiner.</span><span class="sxs-lookup"><span data-stu-id="5b96b-247">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="5b96b-248">E ocorreu um erro interno durante o processamento da unidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-248">And internal error occurred while processing hello drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="5b96b-249">Códigos de status de blobs</span><span class="sxs-lookup"><span data-stu-id="5b96b-249">Blob status codes</span></span>  
<span data-ttu-id="5b96b-250">Olá tabela a seguir lista os códigos de status de saudação para processamento de um blob.</span><span class="sxs-lookup"><span data-stu-id="5b96b-250">hello following table lists hello status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="5b96b-251">Código de status</span><span class="sxs-lookup"><span data-stu-id="5b96b-251">Status code</span></span>|<span data-ttu-id="5b96b-252">Descrição</span><span class="sxs-lookup"><span data-stu-id="5b96b-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="5b96b-253">Olá blob concluiu o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="5b96b-253">hello blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="5b96b-254">Olá blob concluiu o processamento com erros em um ou mais intervalos de páginas ou blocos, metadados ou propriedades.</span><span class="sxs-lookup"><span data-stu-id="5b96b-254">hello blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="5b96b-255">nome de arquivo Hello é inválido.</span><span class="sxs-lookup"><span data-stu-id="5b96b-255">hello file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="5b96b-256">nome do arquivo Hello é muito longo.</span><span class="sxs-lookup"><span data-stu-id="5b96b-256">hello file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="5b96b-257">não foi encontrado o arquivo Hello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-257">hello file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="5b96b-258">Arquivo de toohello de acesso é negado.</span><span class="sxs-lookup"><span data-stu-id="5b96b-258">Access toohello file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="5b96b-259">Falha na solicitação de serviço de Blob Olá tooaccess Olá blob.</span><span class="sxs-lookup"><span data-stu-id="5b96b-259">hello Blob service request tooaccess hello blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="5b96b-260">solicitação de serviço de Blob Olá tooaccess Olá blob é proibida.</span><span class="sxs-lookup"><span data-stu-id="5b96b-260">hello Blob service request tooaccess hello blob is forbidden.</span></span> <span data-ttu-id="5b96b-261">Isso pode ser devido a chave de conta de armazenamento tooinvalid ou SAS do contêiner.</span><span class="sxs-lookup"><span data-stu-id="5b96b-261">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="5b96b-262">Falha ao blob de saudação toorename (para um trabalho de importação) ou arquivo de saudação (para um trabalho de exportação).</span><span class="sxs-lookup"><span data-stu-id="5b96b-262">Failed toorename hello blob (for an import job) or hello file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="5b96b-263">Uma alteração inesperada ocorreu com o blob de saudação (para um trabalho de exportação).</span><span class="sxs-lookup"><span data-stu-id="5b96b-263">An unexpected change has occurred with hello blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="5b96b-264">Há uma concessão no blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-264">There is a lease present on hello blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="5b96b-265">Um disco ou uma falha de e/s de rede ocorreu durante o processamento de blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-265">A disk or network I/O failure occurred while processing hello blob.</span></span>|  
|`Failed`|<span data-ttu-id="5b96b-266">Falha desconhecida ocorreu ao processar o blob de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-266">An unknown failure occurred while processing hello blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="5b96b-267">Códigos de status de disposição de importação</span><span class="sxs-lookup"><span data-stu-id="5b96b-267">Import disposition status codes</span></span>  
<span data-ttu-id="5b96b-268">Olá tabela a seguir lista os códigos de status de saudação para resolver uma disposição de importação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-268">hello following table lists hello status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="5b96b-269">Código de status</span><span class="sxs-lookup"><span data-stu-id="5b96b-269">Status code</span></span>|<span data-ttu-id="5b96b-270">Descrição</span><span class="sxs-lookup"><span data-stu-id="5b96b-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="5b96b-271">Olá blob foi criado.</span><span class="sxs-lookup"><span data-stu-id="5b96b-271">hello blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="5b96b-272">Olá blob foi renomeado por disposição de importação de renomeação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-272">hello blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="5b96b-273">Olá `Blob/BlobPath` elemento contém Olá URI de blob Olá renomeado.</span><span class="sxs-lookup"><span data-stu-id="5b96b-273">hello `Blob/BlobPath` element contains hello URI for hello renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="5b96b-274">Olá blob foi ignorado por `no-overwrite` disposição de importação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-274">hello blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="5b96b-275">blob Olá substituiu um blob existente por `overwrite` disposição de importação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-275">hello blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="5b96b-276">Uma falha anterior interrompeu o processamento da disposição de importação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-276">A prior failure has stopped further processing of hello import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="5b96b-277">Códigos de status do intervalo de página/bloco</span><span class="sxs-lookup"><span data-stu-id="5b96b-277">Page range/block status codes</span></span>  
<span data-ttu-id="5b96b-278">Olá tabela a seguir lista os códigos de status de saudação para processamento de um intervalo de página ou bloco.</span><span class="sxs-lookup"><span data-stu-id="5b96b-278">hello following table lists hello status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="5b96b-279">Código de status</span><span class="sxs-lookup"><span data-stu-id="5b96b-279">Status code</span></span>|<span data-ttu-id="5b96b-280">Descrição</span><span class="sxs-lookup"><span data-stu-id="5b96b-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="5b96b-281">Olá intervalo de página ou bloco concluiu o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="5b96b-281">hello page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="5b96b-282">Olá bloco foi confirmado, mas não no hello lista completa de bloco porque outros blocos tem falha ou colocar a própria lista completa de bloco falhou.</span><span class="sxs-lookup"><span data-stu-id="5b96b-282">hello block has been committed,  but not in hello full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="5b96b-283">bloco de saudação é carregado, mas não foi confirmado.</span><span class="sxs-lookup"><span data-stu-id="5b96b-283">hello block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="5b96b-284">Olá intervalo de página ou bloco está corrompido (Olá conteúdo não corresponde ao seu hash).</span><span class="sxs-lookup"><span data-stu-id="5b96b-284">hello page range or block is corrupted (hello content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="5b96b-285">Fim de arquivo inesperado foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="5b96b-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="5b96b-286">Fim de blob inesperado foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="5b96b-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="5b96b-287">Olá solicitar o serviço Blob tooaccess Olá intervalo de página ou bloco falhou.</span><span class="sxs-lookup"><span data-stu-id="5b96b-287">hello Blob service request tooaccess hello page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="5b96b-288">Um disco ou uma falha de e/s de rede ocorreu durante o processamento Olá intervalo de página ou bloco.</span><span class="sxs-lookup"><span data-stu-id="5b96b-288">A disk or network I/O failure occurred while processing hello page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="5b96b-289">Falha desconhecida ocorreu ao processar Olá intervalo de página ou bloco.</span><span class="sxs-lookup"><span data-stu-id="5b96b-289">An unknown failure occurred while processing hello page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="5b96b-290">Uma falha anterior interrompeu o processamento do intervalo de páginas de saudação ou bloco.</span><span class="sxs-lookup"><span data-stu-id="5b96b-290">A prior failure has stopped further processing of hello page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="5b96b-291">Códigos de status de metadados</span><span class="sxs-lookup"><span data-stu-id="5b96b-291">Metadata status codes</span></span>  
<span data-ttu-id="5b96b-292">Olá tabela a seguir lista os códigos de status de saudação para metadados de blob de processamento.</span><span class="sxs-lookup"><span data-stu-id="5b96b-292">hello following table lists hello status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="5b96b-293">Código de status</span><span class="sxs-lookup"><span data-stu-id="5b96b-293">Status code</span></span>|<span data-ttu-id="5b96b-294">Descrição</span><span class="sxs-lookup"><span data-stu-id="5b96b-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="5b96b-295">Olá metadados concluiu o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="5b96b-295">hello metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="5b96b-296">nome do arquivo de metadados de saudação é inválido.</span><span class="sxs-lookup"><span data-stu-id="5b96b-296">hello metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="5b96b-297">nome do arquivo de metadados de saudação é muito longo.</span><span class="sxs-lookup"><span data-stu-id="5b96b-297">hello metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="5b96b-298">arquivo de metadados de saudação não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="5b96b-298">hello metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="5b96b-299">Arquivo de metadados de toohello de acesso é negado.</span><span class="sxs-lookup"><span data-stu-id="5b96b-299">Access toohello metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="5b96b-300">arquivo de metadados de saudação está corrompido (Olá conteúdo não corresponde ao seu hash).</span><span class="sxs-lookup"><span data-stu-id="5b96b-300">hello metadata file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="5b96b-301">conteúdo da saudação de metadados não está de acordo com formato necessário toohello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-301">hello metadata content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="5b96b-302">Gravando Olá metadados que XML falhou.</span><span class="sxs-lookup"><span data-stu-id="5b96b-302">Writing hello metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="5b96b-303">Falha na solicitação de serviço de Blob Olá tooaccess Olá metadados.</span><span class="sxs-lookup"><span data-stu-id="5b96b-303">hello Blob service request tooaccess hello metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="5b96b-304">Uma falha de e/s de disco ou rede ocorreu durante o processamento de metadados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-304">A disk or network I/O failure occurred while processing hello metadata.</span></span>|  
|`Failed`|<span data-ttu-id="5b96b-305">Falha desconhecida ocorreu ao processar metadados hello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-305">An unknown failure occurred while processing hello metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="5b96b-306">Uma falha anterior interrompeu o processamento dos metadados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-306">A prior failure has stopped further processing of hello metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="5b96b-307">Códigos de status das propriedades</span><span class="sxs-lookup"><span data-stu-id="5b96b-307">Properties status codes</span></span>  
<span data-ttu-id="5b96b-308">Olá tabela a seguir lista os códigos de status de saudação para propriedades de blob de processamento.</span><span class="sxs-lookup"><span data-stu-id="5b96b-308">hello following table lists hello status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="5b96b-309">Código de status</span><span class="sxs-lookup"><span data-stu-id="5b96b-309">Status code</span></span>|<span data-ttu-id="5b96b-310">Descrição</span><span class="sxs-lookup"><span data-stu-id="5b96b-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="5b96b-311">Propriedades de saudação concluiu o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="5b96b-311">hello properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="5b96b-312">nome do arquivo de propriedades de saudação é inválido.</span><span class="sxs-lookup"><span data-stu-id="5b96b-312">hello properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="5b96b-313">nome do arquivo de propriedades de saudação é muito longo.</span><span class="sxs-lookup"><span data-stu-id="5b96b-313">hello properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="5b96b-314">arquivo de propriedades de saudação não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="5b96b-314">hello properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="5b96b-315">Arquivo de propriedades de toohello de acesso é negado.</span><span class="sxs-lookup"><span data-stu-id="5b96b-315">Access toohello properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="5b96b-316">arquivo de propriedades de saudação está corrompido (Olá conteúdo não corresponde ao seu hash).</span><span class="sxs-lookup"><span data-stu-id="5b96b-316">hello properties file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="5b96b-317">conteúdo das propriedades Olá não está de acordo com formato necessário toohello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-317">hello properties content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="5b96b-318">Gravar propriedades Olá que XML falhou.</span><span class="sxs-lookup"><span data-stu-id="5b96b-318">Writing hello properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="5b96b-319">Falha na solicitação de serviço de Blob Olá tooaccess Olá propriedades.</span><span class="sxs-lookup"><span data-stu-id="5b96b-319">hello Blob service request tooaccess hello properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="5b96b-320">Uma falha de e/s de disco ou rede ocorreu durante o processamento de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-320">A disk or network I/O failure occurred while processing hello properties.</span></span>|  
|`Failed`|<span data-ttu-id="5b96b-321">Falha desconhecida ocorreu ao processar as propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-321">An unknown failure occurred while processing hello properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="5b96b-322">Uma falha anterior interrompeu o processamento das propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-322">A prior failure has stopped further processing of hello properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="5b96b-323">Logs de exemplo</span><span class="sxs-lookup"><span data-stu-id="5b96b-323">Sample logs</span></span>  
<span data-ttu-id="5b96b-324">a seguir Olá é um exemplo de log detalhado.</span><span class="sxs-lookup"><span data-stu-id="5b96b-324">hello following is an example of verbose log.</span></span>  
  
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
  
<span data-ttu-id="5b96b-325">log de erros Olá correspondente é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="5b96b-325">hello corresponding error log is shown below.</span></span>  
  
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

 <span data-ttu-id="5b96b-326">log de erros de acompanhamento Olá para um trabalho de importação contém um erro sobre um arquivo não encontrado na unidade de importação de saudação.</span><span class="sxs-lookup"><span data-stu-id="5b96b-326">hello follow error log for an import job contains an error about a file not found on hello import drive.</span></span> <span data-ttu-id="5b96b-327">Observe que o status de saudação dos componentes subsequentes é `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="5b96b-327">Note that hello status of subsequent components is `Cancelled`.</span></span>  
  
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

<span data-ttu-id="5b96b-328">Olá seguinte o log de erros para um trabalho de exportação indica que o conteúdo do blob Olá tem foi gravado com êxito toohello unidade, mas ocorreu um erro durante a exportação de propriedades do blob hello.</span><span class="sxs-lookup"><span data-stu-id="5b96b-328">hello following error log for an export job indicates that hello blob content has been successfully written toohello drive, but that an error occurred while exporting hello blob's properties.</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="5b96b-329">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5b96b-329">Next steps</span></span>
 
* [<span data-ttu-id="5b96b-330">API REST de Importação/Exportação do Armazenamento</span><span class="sxs-lookup"><span data-stu-id="5b96b-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
