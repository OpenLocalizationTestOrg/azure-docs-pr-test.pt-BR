---
title: formato de arquivo aaaAzure importar/exportar metadados e propriedades | Microsoft Docs
description: "Saiba como toospecify metadados e propriedades para um ou mais blobs que fazem parte de uma importação ou exportação de trabalho."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="0f3ef-103">Formato de arquivo de propriedades e metadados de serviço de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="0f3ef-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="0f3ef-104">É possível especificar metadados e propriedades para um ou mais blobs como parte de um trabalho de importação ou exportação.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="0f3ef-105">tooset metadados ou propriedades para blobs que está sendo criados como parte de um trabalho de importação, você fornecer um arquivo de metadados ou propriedades na unidade de disco rígido Olá contendo Olá toobe de dados importado.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-105">tooset metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on hello hard drive containing hello data toobe imported.</span></span> <span data-ttu-id="0f3ef-106">Para um trabalho de exportação, propriedades e os metadados são gravadas tooa metadados ou propriedades de arquivo que está incluído no disco rígido de saudação retornado tooyou.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-106">For an export job, metadata and properties are written tooa metadata or properties file that is included on hello hard drive returned tooyou.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="0f3ef-107">Formato de arquivo de metadados</span><span class="sxs-lookup"><span data-stu-id="0f3ef-107">Metadata file format</span></span>  
<span data-ttu-id="0f3ef-108">formato de saudação de um arquivo de metadados é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0f3ef-108">hello format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="0f3ef-109">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="0f3ef-109">XML Element</span></span>|<span data-ttu-id="0f3ef-110">Tipo</span><span class="sxs-lookup"><span data-stu-id="0f3ef-110">Type</span></span>|<span data-ttu-id="0f3ef-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="0f3ef-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="0f3ef-112">Elemento raiz</span><span class="sxs-lookup"><span data-stu-id="0f3ef-112">Root element</span></span>|<span data-ttu-id="0f3ef-113">elemento de raiz Olá Olá do arquivo de metadados.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-113">hello root element of hello metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="0f3ef-114">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0f3ef-114">String</span></span>|<span data-ttu-id="0f3ef-115">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-115">Optional.</span></span> <span data-ttu-id="0f3ef-116">elemento XML de saudação especifica o nome de saudação de metadados de saudação blob hello e seu valor Especifica o valor de saudação da configuração de metadados de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-116">hello XML element specifies hello name of hello metadata for hello blob, and its value specifies hello value of hello metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="0f3ef-117">Formato de arquivo de propriedades</span><span class="sxs-lookup"><span data-stu-id="0f3ef-117">Properties file format</span></span>  
<span data-ttu-id="0f3ef-118">formato de saudação de um arquivo de propriedades é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="0f3ef-118">hello format of a properties file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|<span data-ttu-id="0f3ef-119">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="0f3ef-119">XML Element</span></span>|<span data-ttu-id="0f3ef-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="0f3ef-120">Type</span></span>|<span data-ttu-id="0f3ef-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="0f3ef-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="0f3ef-122">Elemento raiz</span><span class="sxs-lookup"><span data-stu-id="0f3ef-122">Root element</span></span>|<span data-ttu-id="0f3ef-123">elemento raiz de saudação do arquivo de propriedades de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-123">hello root element of hello properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="0f3ef-124">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0f3ef-124">String</span></span>|<span data-ttu-id="0f3ef-125">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-125">Optional.</span></span> <span data-ttu-id="0f3ef-126">Olá hora da última modificação para blob hello.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-126">hello last-modified time for hello blob.</span></span> <span data-ttu-id="0f3ef-127">Somente para trabalhos de exportação.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="0f3ef-128">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0f3ef-128">String</span></span>|<span data-ttu-id="0f3ef-129">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-129">Optional.</span></span> <span data-ttu-id="0f3ef-130">Olá valor ETag do blob.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-130">hello blob's ETag value.</span></span> <span data-ttu-id="0f3ef-131">Somente para trabalhos de exportação.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="0f3ef-132">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0f3ef-132">String</span></span>|<span data-ttu-id="0f3ef-133">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-133">Optional.</span></span> <span data-ttu-id="0f3ef-134">tamanho de saudação do blob Olá em bytes.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-134">hello size of hello blob in bytes.</span></span> <span data-ttu-id="0f3ef-135">Somente para trabalhos de exportação.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="0f3ef-136">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0f3ef-136">String</span></span>|<span data-ttu-id="0f3ef-137">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-137">Optional.</span></span> <span data-ttu-id="0f3ef-138">tipo de conteúdo de saudação do blob hello.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-138">hello content type of hello blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="0f3ef-139">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0f3ef-139">String</span></span>|<span data-ttu-id="0f3ef-140">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-140">Optional.</span></span> <span data-ttu-id="0f3ef-141">Olá hash MD5 do blob.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-141">hello blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="0f3ef-142">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0f3ef-142">String</span></span>|<span data-ttu-id="0f3ef-143">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-143">Optional.</span></span> <span data-ttu-id="0f3ef-144">Olá conteúdo do blob de codificação.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-144">hello blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="0f3ef-145">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0f3ef-145">String</span></span>|<span data-ttu-id="0f3ef-146">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-146">Optional.</span></span> <span data-ttu-id="0f3ef-147">Olá idioma do conteúdo do blob.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-147">hello blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="0f3ef-148">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="0f3ef-148">String</span></span>|<span data-ttu-id="0f3ef-149">Opcional.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-149">Optional.</span></span> <span data-ttu-id="0f3ef-150">sequência de controle de cache Olá blob hello.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-150">hello cache control string for hello blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="0f3ef-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0f3ef-151">Next steps</span></span>

<span data-ttu-id="0f3ef-152">Confira [Set Blob Properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata) e [Setting and Retrieving Properties and Metadata for Blob Resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) (Definição e recuperação de propriedades e de metadados para recursos de blob) para obter as regras detalhadas sobre como definir as propriedades e os metadados do blob.</span><span class="sxs-lookup"><span data-stu-id="0f3ef-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
