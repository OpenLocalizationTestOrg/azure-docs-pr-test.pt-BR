---
title: "aaaSetting propriedades e metadados de importação/exportação do Azure | Microsoft Docs"
description: "Saiba como toospecify toobe de propriedades e metadados definidos em blobs de destino de saudação ao executar Olá ferramenta de importação/exportação do Azure tooprepare suas unidades."
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
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 05c2b13bead793c8ab5aac6ce25816be97fffb14
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="11a5e-103">Processo de importação de definição de propriedades e metadados durante a saudação</span><span class="sxs-lookup"><span data-stu-id="11a5e-103">Setting properties and metadata during hello import process</span></span>

<span data-ttu-id="11a5e-104">Quando você executa Olá ferramenta de importação/exportação do Microsoft Azure tooprepare suas unidades, você pode especificar propriedades e metadados toobe definidos em blobs de destino hello.</span><span class="sxs-lookup"><span data-stu-id="11a5e-104">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="11a5e-105">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="11a5e-105">Follow these steps:</span></span>

1.  <span data-ttu-id="11a5e-106">Propriedades do blob tooset, crie um arquivo de texto no computador local que especifica os nomes de propriedade e valores.</span><span class="sxs-lookup"><span data-stu-id="11a5e-106">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="11a5e-107">tooset metadados de blob, crie um arquivo de texto no computador local que especifica os valores e nomes de metadados.</span><span class="sxs-lookup"><span data-stu-id="11a5e-107">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="11a5e-108">Passar Olá tooone de caminho completo ou ambos esses arquivos toohello ferramenta de importação/exportação do Azure como parte da saudação `PrepImport` operação.</span><span class="sxs-lookup"><span data-stu-id="11a5e-108">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="11a5e-109">Ao especificar um arquivo de propriedades ou de metadados como parte de uma sessão de cópia, essas propriedades ou esses metadados são definidos para cada blob importado como parte da sessão de cópia.</span><span class="sxs-lookup"><span data-stu-id="11a5e-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="11a5e-110">Se você quiser toospecify um conjunto diferente de propriedades ou metadados para alguns dos blobs hello está sendo importados, você precisará toocreate sessão com propriedades diferentes ou arquivos de metadados de copiar um separado.</span><span class="sxs-lookup"><span data-stu-id="11a5e-110">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="11a5e-111">Especificar as propriedades de blob em um arquivo de texto</span><span class="sxs-lookup"><span data-stu-id="11a5e-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="11a5e-112">Propriedades de blob toospecify, criar um arquivo de texto local e inclua XML que especifica os nomes de propriedade como elementos e valores de propriedade como valores.</span><span class="sxs-lookup"><span data-stu-id="11a5e-112">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="11a5e-113">Este é um exemplo que especifica alguns valores de propriedade:</span><span class="sxs-lookup"><span data-stu-id="11a5e-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="11a5e-114">Salvar Olá arquivo tooa local como `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="11a5e-114">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="11a5e-115">Especificar os metadados de blob em um arquivo de texto</span><span class="sxs-lookup"><span data-stu-id="11a5e-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="11a5e-116">Da mesma forma, toospecify metadados de blob, crie um arquivo de texto local que especifica os nomes de metadados como elementos e valores de metadados como valores.</span><span class="sxs-lookup"><span data-stu-id="11a5e-116">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="11a5e-117">Este é um exemplo que especifica alguns valores de metadados:</span><span class="sxs-lookup"><span data-stu-id="11a5e-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="11a5e-118">Salvar Olá arquivo tooa local como `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="11a5e-118">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-hello-path-tooproperties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="11a5e-119">Adicionar Olá caminho tooproperties e arquivos de metadados em dataset.csv</span><span class="sxs-lookup"><span data-stu-id="11a5e-119">Add hello path tooproperties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="11a5e-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="11a5e-120">Next steps</span></span>

* [<span data-ttu-id="11a5e-121">Formato de arquivo de propriedades e metadados de serviço de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="11a5e-121">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
