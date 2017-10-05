---
title: "Configuração de propriedades e metadados usando a Importação/Exportação do Azure - v1 | Microsoft Docs"
description: "Saiba como especificar as propriedades e os metadados a serem definidos nos blobs de destino durante a execução da Ferramenta de Importação/Exportação do Azure para preparar as unidades. Este documento refere-se à v1 da Ferramenta de Importação/Exportação."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 77bdaa5559de86cd1de9f30e70656e47fd5719e2
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="setting-properties-and-metadata-during-the-import-process"></a><span data-ttu-id="e5a5d-104">Configurando propriedades e metadados durante o processo de importação</span><span class="sxs-lookup"><span data-stu-id="e5a5d-104">Setting properties and metadata during the import process</span></span>
<span data-ttu-id="e5a5d-105">Quando você executa a Ferramenta de Importação/Exportação do Microsoft Azure para preparar as unidades, é possível especificar as propriedades e os metadados a serem definidos nos blobs de destino.</span><span class="sxs-lookup"><span data-stu-id="e5a5d-105">When you run the Microsoft Azure Import/Export Tool to prepare your drives, you can specify properties and metadata to be set on the destination blobs.</span></span> <span data-ttu-id="e5a5d-106">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e5a5d-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="e5a5d-107">Para definir propriedades de blob, crie um arquivo de texto no computador local que especifica os nomes e valores das propriedades.</span><span class="sxs-lookup"><span data-stu-id="e5a5d-107">To set blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="e5a5d-108">Para definir metadados de blob, crie um arquivo de texto no computador local que especifica os nomes e valores dos metadados.</span><span class="sxs-lookup"><span data-stu-id="e5a5d-108">To set blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="e5a5d-109">Passe o caminho completo para um ou ambos os arquivos à Ferramenta de Importação/Exportação do Azure como parte da operação `PrepImport`.</span><span class="sxs-lookup"><span data-stu-id="e5a5d-109">Pass the full path to one or both of these files to the Azure Import/Export Tool as part of the `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="e5a5d-110">Ao especificar um arquivo de propriedades ou de metadados como parte de uma sessão de cópia, essas propriedades ou esses metadados são definidos para cada blob importado como parte da sessão de cópia.</span><span class="sxs-lookup"><span data-stu-id="e5a5d-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="e5a5d-111">Se desejar especificar outro conjunto de propriedades ou de metadados para alguns dos blobs importados, você precisará criar uma sessão de cópia separada com arquivos de propriedades ou de metadados diferentes.</span><span class="sxs-lookup"><span data-stu-id="e5a5d-111">If you want to specify a different set of properties or metadata for some of the blobs being imported, you'll need to create a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="e5a5d-112">Especificar as propriedades de blob em um arquivo de texto</span><span class="sxs-lookup"><span data-stu-id="e5a5d-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="e5a5d-113">Para especificar as propriedades de blob, crie um arquivo de texto local e inclua um XML que especifica os nomes da propriedade como elementos e os valores da propriedade como valores.</span><span class="sxs-lookup"><span data-stu-id="e5a5d-113">To specify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="e5a5d-114">Este é um exemplo que especifica alguns valores de propriedade:</span><span class="sxs-lookup"><span data-stu-id="e5a5d-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="e5a5d-115">Salve o arquivo em uma localização local como `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="e5a5d-115">Save the file to a local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="e5a5d-116">Especificar os metadados de blob em um arquivo de texto</span><span class="sxs-lookup"><span data-stu-id="e5a5d-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="e5a5d-117">Da mesma forma, para especificar os metadados de blob, crie um arquivo de texto local que especifica os nomes dos metadados como elementos e os valores dos metadados como valores.</span><span class="sxs-lookup"><span data-stu-id="e5a5d-117">Similarly, to specify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="e5a5d-118">Este é um exemplo que especifica alguns valores de metadados:</span><span class="sxs-lookup"><span data-stu-id="e5a5d-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="e5a5d-119">Salve o arquivo em uma localização local como `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="e5a5d-119">Save the file to a local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-the-properties-or-metadata-files"></a><span data-ttu-id="e5a5d-120">Criar uma sessão de cópia, incluindo os arquivos de propriedades ou metadados</span><span class="sxs-lookup"><span data-stu-id="e5a5d-120">Create a Copy Session Including the Properties or Metadata Files</span></span>  
<span data-ttu-id="e5a5d-121">Ao executar a Ferramenta de Importação/Exportação do Azure para preparar o trabalho de importação, especifique o arquivo de propriedades na linha de comando usando o parâmetro `PropertyFile`.</span><span class="sxs-lookup"><span data-stu-id="e5a5d-121">When you run the Azure Import/Export Tool to prepare the import job, specify the properties file on the command line using the `PropertyFile` parameter.</span></span> <span data-ttu-id="e5a5d-122">Especifique o arquivo de metadados na linha de comando usando o parâmetro `/MetadataFile`.</span><span class="sxs-lookup"><span data-stu-id="e5a5d-122">Specify the metadata file on the command line using the `/MetadataFile` parameter.</span></span> <span data-ttu-id="e5a5d-123">Este é um exemplo que especifica os dois arquivos:</span><span class="sxs-lookup"><span data-stu-id="e5a5d-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="e5a5d-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e5a5d-124">Next steps</span></span>

* [<span data-ttu-id="e5a5d-125">Formato de arquivo de propriedades e metadados de serviço de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="e5a5d-125">Import/Export service metadata and properties file format</span></span>](../storage-import-export-file-format-metadata-and-properties.md)
