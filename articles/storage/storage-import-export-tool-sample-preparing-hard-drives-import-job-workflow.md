---
title: "Fluxo de trabalho de exemplo para preparo dos discos rígidos de um trabalho de importação do serviço de Importação/Exportação do Azure | Microsoft Docs"
description: "Veja um passo a passo para o processo completo de preparo de unidades para um trabalho de importação no serviço de Importação/Exportação do Azure."
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
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: 78d7ce3bbd3205fd995ba331af08d830097c8156
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="c19fa-103">Fluxo de trabalho de exemplo para preparo dos discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="c19fa-103">Sample workflow to prepare hard drives for an import job</span></span>

<span data-ttu-id="c19fa-104">Este artigo explica o processo completo de preparar unidades para um trabalho de importação.</span><span class="sxs-lookup"><span data-stu-id="c19fa-104">This article walks you through the complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="c19fa-105">Dados de amostra</span><span class="sxs-lookup"><span data-stu-id="c19fa-105">Sample data</span></span>

<span data-ttu-id="c19fa-106">Este exemplo importa os seguintes dados para uma conta de armazenamento do Azure denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="c19fa-106">This example imports the following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="c19fa-107">Local</span><span class="sxs-lookup"><span data-stu-id="c19fa-107">Location</span></span>|<span data-ttu-id="c19fa-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="c19fa-108">Description</span></span>|<span data-ttu-id="c19fa-109">Tamanho dos dados</span><span class="sxs-lookup"><span data-stu-id="c19fa-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="c19fa-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="c19fa-110">H:\Video\\</span></span> |<span data-ttu-id="c19fa-111">Uma coleção de vídeos</span><span class="sxs-lookup"><span data-stu-id="c19fa-111">A collection of videos</span></span>|<span data-ttu-id="c19fa-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="c19fa-112">12 TB</span></span>|
|<span data-ttu-id="c19fa-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="c19fa-113">H:\Photo\\</span></span> |<span data-ttu-id="c19fa-114">Uma coleção de fotos</span><span class="sxs-lookup"><span data-stu-id="c19fa-114">A collection of photos</span></span>|<span data-ttu-id="c19fa-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="c19fa-115">30 GB</span></span>|
|<span data-ttu-id="c19fa-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="c19fa-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="c19fa-117">Uma imagem de disco Blu-ray™</span><span class="sxs-lookup"><span data-stu-id="c19fa-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="c19fa-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="c19fa-118">25 GB</span></span>|
|<span data-ttu-id="c19fa-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="c19fa-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="c19fa-120">Uma coleção de arquivos de música em um compartilhamento de rede</span><span class="sxs-lookup"><span data-stu-id="c19fa-120">A collection of music files on a network share</span></span>|<span data-ttu-id="c19fa-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="c19fa-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="c19fa-122">Destinos de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="c19fa-122">Storage account destinations</span></span>

<span data-ttu-id="c19fa-123">O trabalho de importação importará os dados nos destinos a seguir na conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="c19fa-123">The import job will import the data into the following destinations in the storage account:</span></span>

|<span data-ttu-id="c19fa-124">Fonte</span><span class="sxs-lookup"><span data-stu-id="c19fa-124">Source</span></span>|<span data-ttu-id="c19fa-125">Blob de destino ou diretório virtual</span><span class="sxs-lookup"><span data-stu-id="c19fa-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="c19fa-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="c19fa-126">H:\Video\\</span></span> |<span data-ttu-id="c19fa-127">video/</span><span class="sxs-lookup"><span data-stu-id="c19fa-127">video/</span></span>|
|<span data-ttu-id="c19fa-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="c19fa-128">H:\Photo\\</span></span> |<span data-ttu-id="c19fa-129">photo/</span><span class="sxs-lookup"><span data-stu-id="c19fa-129">photo/</span></span>|
|<span data-ttu-id="c19fa-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="c19fa-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="c19fa-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="c19fa-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="c19fa-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="c19fa-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="c19fa-133">music</span><span class="sxs-lookup"><span data-stu-id="c19fa-133">music</span></span>|

<span data-ttu-id="c19fa-134">Com esse mapeamento, o arquivo `H:\Video\Drama\GreatMovie.mov` será importado para o blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="c19fa-134">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` will be imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="c19fa-135">Determinar os requisitos de disco rígido</span><span class="sxs-lookup"><span data-stu-id="c19fa-135">Determine hard drive requirements</span></span>

<span data-ttu-id="c19fa-136">Em seguida, para determinar quantos discos rígidos são necessários, calcule o tamanho dos dados:</span><span class="sxs-lookup"><span data-stu-id="c19fa-136">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="c19fa-137">Neste exemplo, duas unidades de disco rígido de 8TB devem ser suficientes.</span><span class="sxs-lookup"><span data-stu-id="c19fa-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="c19fa-138">No entanto, como o diretório de origem `H:\Video` tem 12 TB de dados e a capacidade do disco rígido único é de apenas 8 TB, você poderá especificar isso da seguinte forma no arquivo **driveset.csv**:</span><span class="sxs-lookup"><span data-stu-id="c19fa-138">However, since the source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able to specify this in the following way in the **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="c19fa-139">A ferramenta distribui dados em dois discos rígidos de forma otimizada.</span><span class="sxs-lookup"><span data-stu-id="c19fa-139">The tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-the-job"></a><span data-ttu-id="c19fa-140">Anexar discos e configurar o trabalho</span><span class="sxs-lookup"><span data-stu-id="c19fa-140">Attach drives and configure the job</span></span>
<span data-ttu-id="c19fa-141">Você anexará ambos os discos ao computador e criará volumes.</span><span class="sxs-lookup"><span data-stu-id="c19fa-141">You will attach both disks to the machine and create volumes.</span></span> <span data-ttu-id="c19fa-142">Em seguida, crie o arquivo **dataset.csv**:</span><span class="sxs-lookup"><span data-stu-id="c19fa-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="c19fa-143">Além disso, você pode definir os metadados para todos os arquivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c19fa-143">In addition, you can set the following metadata for all files:</span></span>

* <span data-ttu-id="c19fa-144">**UploadMethod:** serviço de Importação/Exportação do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="c19fa-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="c19fa-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="c19fa-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="c19fa-146">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="c19fa-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="c19fa-147">Para definir metadados para os arquivos importados, crie um arquivo de texto `c:\WAImportExport\SampleMetadata.txt`, com o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="c19fa-147">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="c19fa-148">Você também pode definir algumas propriedades para o `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="c19fa-148">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="c19fa-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="c19fa-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="c19fa-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="c19fa-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="c19fa-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="c19fa-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="c19fa-152">Para definir essas propriedades, crie um arquivo de texto `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="c19fa-152">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-the-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="c19fa-153">Execute a Ferramenta de Importação/Exportação do Azure (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="c19fa-153">Run the Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="c19fa-154">Agora você está pronto para executar a Ferramenta de Importação/Exportação do Azure para preparar as duas unidades de disco rígido.</span><span class="sxs-lookup"><span data-stu-id="c19fa-154">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span>

<span data-ttu-id="c19fa-155">**Para a primeira sessão:**</span><span class="sxs-lookup"><span data-stu-id="c19fa-155">**For the first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="c19fa-156">Se mais dados precisam ser adicionados, crie outro arquivo de conjunto de dados (mesmo formato que Initialdataset).</span><span class="sxs-lookup"><span data-stu-id="c19fa-156">If any more data needs to be added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="c19fa-157">**Para a segunda sessão:**</span><span class="sxs-lookup"><span data-stu-id="c19fa-157">**For the second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="c19fa-158">Depois de concluir as sessões de cópia, você pode desconectar as duas unidades do computador de cópia e enviá-las para o centro de dados Azure apropriado.</span><span class="sxs-lookup"><span data-stu-id="c19fa-158">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Azure data center.</span></span> <span data-ttu-id="c19fa-159">Você vai carregar os dois arquivos do diário, `<FirstDriveSerialNumber>.xml` e `<SecondDriveSerialNumber>.xml`, quando você cria a tarefa de importação no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c19fa-159">You'll upload the two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create the import job in the Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c19fa-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c19fa-160">Next steps</span></span>

* [<span data-ttu-id="c19fa-161">Preparação de discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="c19fa-161">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="c19fa-162">Referência rápida para comandos usados frequentemente</span><span class="sxs-lookup"><span data-stu-id="c19fa-162">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference.md)
