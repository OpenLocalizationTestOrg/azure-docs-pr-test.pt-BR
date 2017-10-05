---
title: "Configurando propriedades e metadados usando a Importação/Exportação do Azure | Microsoft Docs"
description: "Saiba como especificar as propriedades e os metadados a serem definidos nos blobs de destino durante a execução da Ferramenta de Importação/Exportação do Azure para preparar as unidades."
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
ms.openlocfilehash: bdc7a53f82d1fbbb726e2b1bd5d96678a8563566
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="8fd27-103">Configurando propriedades e metadados durante o processo de importação</span><span class="sxs-lookup"><span data-stu-id="8fd27-103">Setting properties and metadata during the import process</span></span>

<span data-ttu-id="8fd27-104">Quando você executa a Ferramenta de Importação/Exportação do Microsoft Azure para preparar as unidades, é possível especificar as propriedades e os metadados a serem definidos nos blobs de destino.</span><span class="sxs-lookup"><span data-stu-id="8fd27-104">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="8fd27-105">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="8fd27-105">Follow these steps:</span></span>

1.  <span data-ttu-id="8fd27-106">Para definir propriedades de blob, crie um arquivo de texto no computador local que especifica os nomes e valores das propriedades.</span><span class="sxs-lookup"><span data-stu-id="8fd27-106">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>
2.  <span data-ttu-id="8fd27-107">Para definir metadados de blob, crie um arquivo de texto no computador local que especifica os nomes e valores dos metadados.</span><span class="sxs-lookup"><span data-stu-id="8fd27-107">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>
3.  <span data-ttu-id="8fd27-108">Passe o caminho completo para um ou ambos os arquivos à Ferramenta de Importação/Exportação do Azure como parte da operação `PrepImport`.</span><span class="sxs-lookup"><span data-stu-id="8fd27-108">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>

> [!NOTE]
>  <span data-ttu-id="8fd27-109">Ao especificar um arquivo de propriedades ou de metadados como parte de uma sessão de cópia, essas propriedades ou esses metadados são definidos para cada blob importado como parte da sessão de cópia.</span><span class="sxs-lookup"><span data-stu-id="8fd27-109">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="8fd27-110">Se desejar especificar outro conjunto de propriedades ou de metadados para alguns dos blobs importados, você precisará criar uma sessão de cópia separada com arquivos de propriedades ou de metadados diferentes.</span><span class="sxs-lookup"><span data-stu-id="8fd27-110">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>

## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="8fd27-111">Especificar as propriedades de blob em um arquivo de texto</span><span class="sxs-lookup"><span data-stu-id="8fd27-111">Specify blob properties in a text file</span></span>

<span data-ttu-id="8fd27-112">Para especificar as propriedades de blob, crie um arquivo de texto local e inclua um XML que especifica os nomes da propriedade como elementos e os valores da propriedade como valores.</span><span class="sxs-lookup"><span data-stu-id="8fd27-112">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="8fd27-113">Este é um exemplo que especifica alguns valores de propriedade:</span><span class="sxs-lookup"><span data-stu-id="8fd27-113">Here's an example that specifies some property values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

<span data-ttu-id="8fd27-114">Salve o arquivo em uma localização local como `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="8fd27-114">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>

## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="8fd27-115">Especificar os metadados de blob em um arquivo de texto</span><span class="sxs-lookup"><span data-stu-id="8fd27-115">Specify blob metadata in a text file</span></span>

<span data-ttu-id="8fd27-116">Da mesma forma, para especificar os metadados de blob, crie um arquivo de texto local que especifica os nomes dos metadados como elementos e os valores dos metadados como valores.</span><span class="sxs-lookup"><span data-stu-id="8fd27-116">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="8fd27-117">Este é um exemplo que especifica alguns valores de metadados:</span><span class="sxs-lookup"><span data-stu-id="8fd27-117">Here's an example that specifies some metadata values:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="8fd27-118">Salve o arquivo em uma localização local como `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="8fd27-118">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>

## <a name="add-the-path-to-properties-and-metadata-files-in-datasetcsv"></a><span data-ttu-id="8fd27-119">Adicionar o caminho para os arquivos de propriedades e metadados no dataset.csv</span><span class="sxs-lookup"><span data-stu-id="8fd27-119">Add the path to properties and metadata files in dataset.csv</span></span>

```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,https://mystorageaccount.blob.core.windows.net/video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,https://mystorageaccount.blob.core.windows.net/photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,https://mystorageaccount.blob.core.windows.net/favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,https://mystorageaccount.blob.core.windows.net/music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

## <a name="next-steps"></a><span data-ttu-id="8fd27-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8fd27-120">Next steps</span></span>

* [<span data-ttu-id="8fd27-121">Formato de arquivo de propriedades e metadados de serviço de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="8fd27-121">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
