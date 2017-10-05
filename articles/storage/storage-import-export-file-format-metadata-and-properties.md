---
title: "Formato de arquivo de propriedades e metadados da Importação/Exportação do Azure | Microsoft Docs"
description: "Saiba como especificar metadados e propriedades para um ou mais blobs que fazem parte de um trabalho de importação ou exportação."
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
ms.openlocfilehash: 3f728ad94cdcbd32092b677f11a737ae91376720
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="d4c95-103">Formato de arquivo de propriedades e metadados de serviço de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="d4c95-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="d4c95-104">É possível especificar metadados e propriedades para um ou mais blobs como parte de um trabalho de importação ou exportação.</span><span class="sxs-lookup"><span data-stu-id="d4c95-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="d4c95-105">Para definir metadados ou propriedades para blobs criados como parte de um trabalho de importação, você fornece um arquivo de metadados ou de propriedades no disco rígido que contém os dados a serem importados.</span><span class="sxs-lookup"><span data-stu-id="d4c95-105">To set metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on the hard drive containing the data to be imported.</span></span> <span data-ttu-id="d4c95-106">Para um trabalho de exportação, os metadados e as propriedades são gravados em um arquivo de metadados ou de propriedades incluído no disco rígido retornado para você.</span><span class="sxs-lookup"><span data-stu-id="d4c95-106">For an export job, metadata and properties are written to a metadata or properties file that is included on the hard drive returned to you.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="d4c95-107">Formato de arquivo de metadados</span><span class="sxs-lookup"><span data-stu-id="d4c95-107">Metadata file format</span></span>  
<span data-ttu-id="d4c95-108">O formato de um arquivo de metadados é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d4c95-108">The format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="d4c95-109">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="d4c95-109">XML Element</span></span>|<span data-ttu-id="d4c95-110">Tipo</span><span class="sxs-lookup"><span data-stu-id="d4c95-110">Type</span></span>|<span data-ttu-id="d4c95-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="d4c95-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="d4c95-112">Elemento raiz</span><span class="sxs-lookup"><span data-stu-id="d4c95-112">Root element</span></span>|<span data-ttu-id="d4c95-113">O elemento raiz do arquivo de metadados.</span><span class="sxs-lookup"><span data-stu-id="d4c95-113">The root element of the metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="d4c95-114">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d4c95-114">String</span></span>|<span data-ttu-id="d4c95-115">Opcional.</span><span class="sxs-lookup"><span data-stu-id="d4c95-115">Optional.</span></span> <span data-ttu-id="d4c95-116">O elemento XML especifica o nome dos metadados do blob e seu valor especifica o valor da configuração dos metadados.</span><span class="sxs-lookup"><span data-stu-id="d4c95-116">The XML element specifies the name of the metadata for the blob, and its value specifies the value of the metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="d4c95-117">Formato de arquivo de propriedades</span><span class="sxs-lookup"><span data-stu-id="d4c95-117">Properties file format</span></span>  
<span data-ttu-id="d4c95-118">O formato de um arquivo de propriedades é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="d4c95-118">The format of a properties file is as follows:</span></span>  
  
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
  
|<span data-ttu-id="d4c95-119">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="d4c95-119">XML Element</span></span>|<span data-ttu-id="d4c95-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="d4c95-120">Type</span></span>|<span data-ttu-id="d4c95-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="d4c95-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="d4c95-122">Elemento raiz</span><span class="sxs-lookup"><span data-stu-id="d4c95-122">Root element</span></span>|<span data-ttu-id="d4c95-123">O elemento raiz do arquivo de propriedades.</span><span class="sxs-lookup"><span data-stu-id="d4c95-123">The root element of the properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="d4c95-124">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d4c95-124">String</span></span>|<span data-ttu-id="d4c95-125">Opcional.</span><span class="sxs-lookup"><span data-stu-id="d4c95-125">Optional.</span></span> <span data-ttu-id="d4c95-126">A hora da última modificação do blob.</span><span class="sxs-lookup"><span data-stu-id="d4c95-126">The last-modified time for the blob.</span></span> <span data-ttu-id="d4c95-127">Somente para trabalhos de exportação.</span><span class="sxs-lookup"><span data-stu-id="d4c95-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="d4c95-128">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d4c95-128">String</span></span>|<span data-ttu-id="d4c95-129">Opcional.</span><span class="sxs-lookup"><span data-stu-id="d4c95-129">Optional.</span></span> <span data-ttu-id="d4c95-130">O valor da Etag do blob.</span><span class="sxs-lookup"><span data-stu-id="d4c95-130">The blob's ETag value.</span></span> <span data-ttu-id="d4c95-131">Somente para trabalhos de exportação.</span><span class="sxs-lookup"><span data-stu-id="d4c95-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="d4c95-132">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d4c95-132">String</span></span>|<span data-ttu-id="d4c95-133">Opcional.</span><span class="sxs-lookup"><span data-stu-id="d4c95-133">Optional.</span></span> <span data-ttu-id="d4c95-134">O tamanho do blob em bytes.</span><span class="sxs-lookup"><span data-stu-id="d4c95-134">The size of the blob in bytes.</span></span> <span data-ttu-id="d4c95-135">Somente para trabalhos de exportação.</span><span class="sxs-lookup"><span data-stu-id="d4c95-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="d4c95-136">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d4c95-136">String</span></span>|<span data-ttu-id="d4c95-137">Opcional.</span><span class="sxs-lookup"><span data-stu-id="d4c95-137">Optional.</span></span> <span data-ttu-id="d4c95-138">O tipo de conteúdo do blob.</span><span class="sxs-lookup"><span data-stu-id="d4c95-138">The content type of the blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="d4c95-139">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d4c95-139">String</span></span>|<span data-ttu-id="d4c95-140">Opcional.</span><span class="sxs-lookup"><span data-stu-id="d4c95-140">Optional.</span></span> <span data-ttu-id="d4c95-141">O hash MD5 do blob.</span><span class="sxs-lookup"><span data-stu-id="d4c95-141">The blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="d4c95-142">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d4c95-142">String</span></span>|<span data-ttu-id="d4c95-143">Opcional.</span><span class="sxs-lookup"><span data-stu-id="d4c95-143">Optional.</span></span> <span data-ttu-id="d4c95-144">A codificação do conteúdo do blob.</span><span class="sxs-lookup"><span data-stu-id="d4c95-144">The blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="d4c95-145">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d4c95-145">String</span></span>|<span data-ttu-id="d4c95-146">Opcional.</span><span class="sxs-lookup"><span data-stu-id="d4c95-146">Optional.</span></span> <span data-ttu-id="d4c95-147">O idioma do conteúdo do blob.</span><span class="sxs-lookup"><span data-stu-id="d4c95-147">The blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="d4c95-148">Cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="d4c95-148">String</span></span>|<span data-ttu-id="d4c95-149">Opcional.</span><span class="sxs-lookup"><span data-stu-id="d4c95-149">Optional.</span></span> <span data-ttu-id="d4c95-150">A cadeia de caracteres de controle de cache do blob.</span><span class="sxs-lookup"><span data-stu-id="d4c95-150">The cache control string for the blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="d4c95-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4c95-151">Next steps</span></span>

<span data-ttu-id="d4c95-152">Confira [Set Blob Properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata) e [Setting and Retrieving Properties and Metadata for Blob Resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) (Definição e recuperação de propriedades e de metadados para recursos de blob) para obter as regras detalhadas sobre como definir as propriedades e os metadados do blob.</span><span class="sxs-lookup"><span data-stu-id="d4c95-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
