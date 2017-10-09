---
title: "trabalho de importação de aaaSample fluxo de trabalho tooprep unidades de disco rígido para uma importação/exportação do Azure | Microsoft Docs"
description: "Veja um passo a passo para o processo completo de saudação preparar unidades para um trabalho de importação no hello serviço de importação/exportação do Azure."
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
ms.openlocfilehash: 560220b7dc9f87416f1fec1ff30fa5cd65812ce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="e2fbe-103">Discos rígidos de tooprepare do fluxo de trabalho de exemplo para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="e2fbe-103">Sample workflow tooprepare hard drives for an import job</span></span>

<span data-ttu-id="e2fbe-104">Este artigo o orienta pelo processo de conclusão de saudação preparar unidades para um trabalho de importação.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-104">This article walks you through hello complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="e2fbe-105">Dados de amostra</span><span class="sxs-lookup"><span data-stu-id="e2fbe-105">Sample data</span></span>

<span data-ttu-id="e2fbe-106">Este exemplo importa Olá seguintes dados em uma conta de armazenamento do Azure denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="e2fbe-106">This example imports hello following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="e2fbe-107">Local</span><span class="sxs-lookup"><span data-stu-id="e2fbe-107">Location</span></span>|<span data-ttu-id="e2fbe-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="e2fbe-108">Description</span></span>|<span data-ttu-id="e2fbe-109">Tamanho dos dados</span><span class="sxs-lookup"><span data-stu-id="e2fbe-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="e2fbe-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="e2fbe-110">H:\Video\\</span></span> |<span data-ttu-id="e2fbe-111">Uma coleção de vídeos</span><span class="sxs-lookup"><span data-stu-id="e2fbe-111">A collection of videos</span></span>|<span data-ttu-id="e2fbe-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="e2fbe-112">12 TB</span></span>|
|<span data-ttu-id="e2fbe-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="e2fbe-113">H:\Photo\\</span></span> |<span data-ttu-id="e2fbe-114">Uma coleção de fotos</span><span class="sxs-lookup"><span data-stu-id="e2fbe-114">A collection of photos</span></span>|<span data-ttu-id="e2fbe-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="e2fbe-115">30 GB</span></span>|
|<span data-ttu-id="e2fbe-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="e2fbe-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="e2fbe-117">Uma imagem de disco Blu-ray™</span><span class="sxs-lookup"><span data-stu-id="e2fbe-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="e2fbe-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="e2fbe-118">25 GB</span></span>|
|<span data-ttu-id="e2fbe-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="e2fbe-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="e2fbe-120">Uma coleção de arquivos de música em um compartilhamento de rede</span><span class="sxs-lookup"><span data-stu-id="e2fbe-120">A collection of music files on a network share</span></span>|<span data-ttu-id="e2fbe-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="e2fbe-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="e2fbe-122">Destinos de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e2fbe-122">Storage account destinations</span></span>

<span data-ttu-id="e2fbe-123">trabalho de importação Olá importará dados saudação para Olá destinos na conta de armazenamento Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2fbe-123">hello import job will import hello data into hello following destinations in hello storage account:</span></span>

|<span data-ttu-id="e2fbe-124">Fonte</span><span class="sxs-lookup"><span data-stu-id="e2fbe-124">Source</span></span>|<span data-ttu-id="e2fbe-125">Blob de destino ou diretório virtual</span><span class="sxs-lookup"><span data-stu-id="e2fbe-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="e2fbe-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="e2fbe-126">H:\Video\\</span></span> |<span data-ttu-id="e2fbe-127">video/</span><span class="sxs-lookup"><span data-stu-id="e2fbe-127">video/</span></span>|
|<span data-ttu-id="e2fbe-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="e2fbe-128">H:\Photo\\</span></span> |<span data-ttu-id="e2fbe-129">photo/</span><span class="sxs-lookup"><span data-stu-id="e2fbe-129">photo/</span></span>|
|<span data-ttu-id="e2fbe-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="e2fbe-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="e2fbe-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="e2fbe-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="e2fbe-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="e2fbe-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="e2fbe-133">music</span><span class="sxs-lookup"><span data-stu-id="e2fbe-133">music</span></span>|

<span data-ttu-id="e2fbe-134">Com esse mapeamento, Olá arquivo `H:\Video\Drama\GreatMovie.mov` serão importados toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-134">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="e2fbe-135">Determinar os requisitos de disco rígido</span><span class="sxs-lookup"><span data-stu-id="e2fbe-135">Determine hard drive requirements</span></span>

<span data-ttu-id="e2fbe-136">Em seguida, toodetermine quantos discos rígidos necessários, computação Olá tamanho dos dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="e2fbe-136">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="e2fbe-137">Neste exemplo, duas unidades de disco rígido de 8TB devem ser suficientes.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="e2fbe-138">No entanto, como o diretório de origem Olá `H:\Video` tem 12TB de dados e a capacidade de seu único disco rígido é apenas 8TB, você será capaz de toospecify isso em Olá após a forma como o hello **driveset.csv** arquivo:</span><span class="sxs-lookup"><span data-stu-id="e2fbe-138">However, since hello source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able toospecify this in hello following way in hello **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="e2fbe-139">ferramenta de saudação distribui dados em dois discos rígidos de forma otimizada.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-139">hello tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-hello-job"></a><span data-ttu-id="e2fbe-140">Anexar discos e configurar o trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="e2fbe-140">Attach drives and configure hello job</span></span>
<span data-ttu-id="e2fbe-141">Você anexar a máquina de toohello ambos os discos e criar volumes.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-141">You will attach both disks toohello machine and create volumes.</span></span> <span data-ttu-id="e2fbe-142">Em seguida, crie o arquivo **dataset.csv**:</span><span class="sxs-lookup"><span data-stu-id="e2fbe-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="e2fbe-143">Além disso, você pode definir Olá metadados para todos os arquivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2fbe-143">In addition, you can set hello following metadata for all files:</span></span>

* <span data-ttu-id="e2fbe-144">**UploadMethod:** serviço de Importação/Exportação do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="e2fbe-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="e2fbe-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="e2fbe-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="e2fbe-146">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="e2fbe-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="e2fbe-147">tooset metadados para arquivos de saudação importado, crie um arquivo de texto, `c:\WAImportExport\SampleMetadata.txt`, com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e2fbe-147">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="e2fbe-148">Você também pode definir algumas propriedades para Olá `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="e2fbe-148">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="e2fbe-149">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="e2fbe-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="e2fbe-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="e2fbe-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="e2fbe-151">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="e2fbe-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="e2fbe-152">tooset essas propriedades, crie um arquivo de texto, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="e2fbe-152">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="e2fbe-153">Olá execução ferramenta de importação/exportação do Azure (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="e2fbe-153">Run hello Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="e2fbe-154">Agora você está pronto toorun Olá ferramenta de importação/exportação do Azure tooprepare Olá duas unidades de disco rígido.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-154">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span>

<span data-ttu-id="e2fbe-155">**Para a primeira sessão de saudação:**</span><span class="sxs-lookup"><span data-stu-id="e2fbe-155">**For hello first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="e2fbe-156">Se precisarem de mais dados toobe adicionado, crie outro arquivo de conjunto de dados (mesmo formato Initialdataset).</span><span class="sxs-lookup"><span data-stu-id="e2fbe-156">If any more data needs toobe added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="e2fbe-157">**Para Olá segunda sessão:**</span><span class="sxs-lookup"><span data-stu-id="e2fbe-157">**For hello second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="e2fbe-158">Depois de concluir as sessões de cópia de Olá, você pode desconectar duas unidades de saudação do computador de cópia hello e enviá-las toohello do Azure data center apropriado.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-158">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Azure data center.</span></span> <span data-ttu-id="e2fbe-159">Você vai carregar arquivos de diário de saudação dois `<FirstDriveSerialNumber>.xml` e `<SecondDriveSerialNumber>.xml`, ao criar trabalho de importação Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2fbe-159">You'll upload hello two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create hello import job in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2fbe-160">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2fbe-160">Next steps</span></span>

* [<span data-ttu-id="e2fbe-161">Preparação de discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="e2fbe-161">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="e2fbe-162">Referência rápida para comandos usados frequentemente</span><span class="sxs-lookup"><span data-stu-id="e2fbe-162">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference.md)
