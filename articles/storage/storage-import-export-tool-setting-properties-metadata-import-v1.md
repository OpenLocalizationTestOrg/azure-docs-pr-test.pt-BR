---
title: "aaaSetting propriedades e metadados de importação/exportação do Azure - v1 | Microsoft Docs"
description: "Saiba como toospecify toobe de propriedades e metadados definidos em blobs de destino de saudação ao executar Olá ferramenta de importação/exportação do Azure tooprepare suas unidades. Isso se refere a toov1 de Olá, ferramenta de importação/exportação."
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
ms.openlocfilehash: 66e55c2076fbcda9b78302f17b5ff2cf96bb24e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="7106b-104">Processo de importação de definição de propriedades e metadados durante a saudação</span><span class="sxs-lookup"><span data-stu-id="7106b-104">Setting properties and metadata during hello import process</span></span>
<span data-ttu-id="7106b-105">Quando você executa Olá ferramenta de importação/exportação do Microsoft Azure tooprepare suas unidades, você pode especificar propriedades e metadados toobe definidos em blobs de destino hello.</span><span class="sxs-lookup"><span data-stu-id="7106b-105">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="7106b-106">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="7106b-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="7106b-107">Propriedades do blob tooset, crie um arquivo de texto no computador local que especifica os nomes de propriedade e valores.</span><span class="sxs-lookup"><span data-stu-id="7106b-107">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="7106b-108">tooset metadados de blob, crie um arquivo de texto no computador local que especifica os valores e nomes de metadados.</span><span class="sxs-lookup"><span data-stu-id="7106b-108">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="7106b-109">Passar Olá tooone de caminho completo ou ambos esses arquivos toohello ferramenta de importação/exportação do Azure como parte da saudação `PrepImport` operação.</span><span class="sxs-lookup"><span data-stu-id="7106b-109">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="7106b-110">Ao especificar um arquivo de propriedades ou de metadados como parte de uma sessão de cópia, essas propriedades ou esses metadados são definidos para cada blob importado como parte da sessão de cópia.</span><span class="sxs-lookup"><span data-stu-id="7106b-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="7106b-111">Se você quiser toospecify um conjunto diferente de propriedades ou metadados para alguns dos blobs hello está sendo importados, você precisará toocreate sessão com propriedades diferentes ou arquivos de metadados de copiar um separado.</span><span class="sxs-lookup"><span data-stu-id="7106b-111">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="7106b-112">Especificar as propriedades de blob em um arquivo de texto</span><span class="sxs-lookup"><span data-stu-id="7106b-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="7106b-113">Propriedades de blob toospecify, criar um arquivo de texto local e inclua XML que especifica os nomes de propriedade como elementos e valores de propriedade como valores.</span><span class="sxs-lookup"><span data-stu-id="7106b-113">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="7106b-114">Este é um exemplo que especifica alguns valores de propriedade:</span><span class="sxs-lookup"><span data-stu-id="7106b-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="7106b-115">Salvar Olá arquivo tooa local como `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="7106b-115">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="7106b-116">Especificar os metadados de blob em um arquivo de texto</span><span class="sxs-lookup"><span data-stu-id="7106b-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="7106b-117">Da mesma forma, toospecify metadados de blob, crie um arquivo de texto local que especifica os nomes de metadados como elementos e valores de metadados como valores.</span><span class="sxs-lookup"><span data-stu-id="7106b-117">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="7106b-118">Este é um exemplo que especifica alguns valores de metadados:</span><span class="sxs-lookup"><span data-stu-id="7106b-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="7106b-119">Salvar Olá arquivo tooa local como `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="7106b-119">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a><span data-ttu-id="7106b-120">Criar uma saudação incluindo da sessão de cópia propriedades ou arquivos de metadados</span><span class="sxs-lookup"><span data-stu-id="7106b-120">Create a Copy Session Including hello Properties or Metadata Files</span></span>  
<span data-ttu-id="7106b-121">Quando você executa o trabalho de importação do hello ferramenta de importação/exportação do Azure tooprepare hello, especifique o arquivo de propriedades de Olá na linha de comando hello usando Olá `PropertyFile` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="7106b-121">When you run hello Azure Import/Export Tool tooprepare hello import job, specify hello properties file on hello command line using hello `PropertyFile` parameter.</span></span> <span data-ttu-id="7106b-122">Especificar arquivo de metadados de saudação na linha de comando hello usando Olá `/MetadataFile` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="7106b-122">Specify hello metadata file on hello command line using hello `/MetadataFile` parameter.</span></span> <span data-ttu-id="7106b-123">Este é um exemplo que especifica os dois arquivos:</span><span class="sxs-lookup"><span data-stu-id="7106b-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="7106b-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7106b-124">Next steps</span></span>

* [<span data-ttu-id="7106b-125">Formato de arquivo de propriedades e metadados de serviço de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="7106b-125">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
