---
title: "Fluxo de trabalho de exemplo para preparo dos discos rígidos de um trabalho de importação do serviço de Importação/Exportação do Azure — v1 | Microsoft Docs"
description: "Veja um passo a passo para o processo completo de preparo de unidades para um trabalho de importação no serviço de Importação/Exportação do Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 6eb1b1b7-c69f-4365-b5ef-3cd5e05eb72a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 179c6bac9a2d9509baa0007a7008d75d0874a25e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="sample-workflow-to-prepare-hard-drives-for-an-import-job"></a><span data-ttu-id="fa135-103">Fluxo de trabalho de exemplo para preparo dos discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="fa135-103">Sample workflow to prepare hard drives for an import job</span></span>
<span data-ttu-id="fa135-104">Este tópico explica o processo completo de preparar unidades para um trabalho de importação.</span><span class="sxs-lookup"><span data-stu-id="fa135-104">This topic walks you through the complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="fa135-105">Este exemplo importa os seguintes dados para uma conta de armazenamento do Azure no Windows denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="fa135-105">This example imports the following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="fa135-106">Local</span><span class="sxs-lookup"><span data-stu-id="fa135-106">Location</span></span>|<span data-ttu-id="fa135-107">Descrição</span><span class="sxs-lookup"><span data-stu-id="fa135-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="fa135-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="fa135-108">H:\Video</span></span>|<span data-ttu-id="fa135-109">Uma coleção de vídeos, 5 TB no total.</span><span class="sxs-lookup"><span data-stu-id="fa135-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="fa135-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="fa135-110">H:\Photo</span></span>|<span data-ttu-id="fa135-111">Uma coleção de fotos, 30 GB no total.</span><span class="sxs-lookup"><span data-stu-id="fa135-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="fa135-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="fa135-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="fa135-113">Uma imagem de disco Blu-ray™, 25 GB.</span><span class="sxs-lookup"><span data-stu-id="fa135-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="fa135-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="fa135-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="fa135-115">Uma coleção de arquivos de música em um compartilhamento de rede, 10 GB no total.</span><span class="sxs-lookup"><span data-stu-id="fa135-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="fa135-116">O trabalho de importação importa estes dados nos destinos a seguir na conta de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="fa135-116">The import job imports this data into the following destinations in the storage account:</span></span>  
  
|<span data-ttu-id="fa135-117">Fonte</span><span class="sxs-lookup"><span data-stu-id="fa135-117">Source</span></span>|<span data-ttu-id="fa135-118">Blob de destino ou diretório virtual</span><span class="sxs-lookup"><span data-stu-id="fa135-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="fa135-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="fa135-119">H:\Video</span></span>|<span data-ttu-id="fa135-120">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="fa135-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="fa135-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="fa135-121">H:\Photo</span></span>|<span data-ttu-id="fa135-122">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="fa135-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="fa135-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="fa135-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="fa135-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="fa135-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="fa135-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="fa135-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="fa135-126">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="fa135-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="fa135-127">Com esse mapeamento, o arquivo `H:\Video\Drama\GreatMovie.mov` é importado para o blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="fa135-127">With this mapping, the file `H:\Video\Drama\GreatMovie.mov` is imported to the blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="fa135-128">Em seguida, para determinar quantos discos rígidos são necessários, calcule o tamanho dos dados:</span><span class="sxs-lookup"><span data-stu-id="fa135-128">Next, to determine how many hard drives are needed, compute the size of the data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="fa135-129">Neste exemplo, duas unidades de disco rígido de 3 TB devem ser suficientes.</span><span class="sxs-lookup"><span data-stu-id="fa135-129">For this example, two 3-TB hard drives should be sufficient.</span></span> <span data-ttu-id="fa135-130">No entanto, como o diretório de origem `H:\Video` tem 5 TB de dados e a capacidade do disco rígido único é de apenas 3 TB, será necessário dividir `H:\Video` em dois diretórios menores, `H:\Video1` e `H:\Video2`, antes de executar a Ferramenta de Importação/Exportação do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="fa135-130">However, since the source directory `H:\Video` has 5 TB of data and your single hard drive's capacity is only 3 TB, it's necessary to break `H:\Video` into two smaller directories: `H:\Video1` and `H:\Video2`, before running the Microsoft Azure Import/Export Tool.</span></span> <span data-ttu-id="fa135-131">Esta etapa gera os seguintes diretórios de origem:</span><span class="sxs-lookup"><span data-stu-id="fa135-131">This step yields the following source directories:</span></span>  
  
|<span data-ttu-id="fa135-132">Local</span><span class="sxs-lookup"><span data-stu-id="fa135-132">Location</span></span>|<span data-ttu-id="fa135-133">Tamanho</span><span class="sxs-lookup"><span data-stu-id="fa135-133">Size</span></span>|<span data-ttu-id="fa135-134">Blob de destino ou diretório virtual</span><span class="sxs-lookup"><span data-stu-id="fa135-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="fa135-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="fa135-135">H:\Video1</span></span>|<span data-ttu-id="fa135-136">2.5 TB</span><span class="sxs-lookup"><span data-stu-id="fa135-136">2.5 TB</span></span>|<span data-ttu-id="fa135-137">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="fa135-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="fa135-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="fa135-138">H:\Video2</span></span>|<span data-ttu-id="fa135-139">2.5 TB</span><span class="sxs-lookup"><span data-stu-id="fa135-139">2.5 TB</span></span>|<span data-ttu-id="fa135-140">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="fa135-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="fa135-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="fa135-141">H:\Photo</span></span>|<span data-ttu-id="fa135-142">30 GB</span><span class="sxs-lookup"><span data-stu-id="fa135-142">30 GB</span></span>|<span data-ttu-id="fa135-143">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="fa135-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="fa135-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="fa135-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="fa135-145">25 GB</span><span class="sxs-lookup"><span data-stu-id="fa135-145">25 GB</span></span>|<span data-ttu-id="fa135-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="fa135-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="fa135-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="fa135-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="fa135-148">10 GB</span><span class="sxs-lookup"><span data-stu-id="fa135-148">10 GB</span></span>|<span data-ttu-id="fa135-149">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="fa135-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="fa135-150">Embora o diretório `H:\Video` tenha sido dividido em dois diretórios, eles apontam para o mesmo diretório virtual de destino na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fa135-150">Even though the `H:\Video`directory has been split to two directories, they point to the same destination virtual directory in the storage account.</span></span> <span data-ttu-id="fa135-151">Dessa forma, todos os arquivos de vídeo são mantidos em um único `video` contêiner na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="fa135-151">This way, all video files are maintained under a single `video` container in the storage account.</span></span>  
  
 <span data-ttu-id="fa135-152">Em seguida, os diretórios de origem anteriores são distribuídos uniformemente nos dois discos rígidos:</span><span class="sxs-lookup"><span data-stu-id="fa135-152">Next, the previous source directories are evenly distributed to the two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="fa135-153">Disco rígido</span><span class="sxs-lookup"><span data-stu-id="fa135-153">Hard drive</span></span>|<span data-ttu-id="fa135-154">Diretórios de origem</span><span class="sxs-lookup"><span data-stu-id="fa135-154">Source directories</span></span>|<span data-ttu-id="fa135-155">Tamanho total</span><span class="sxs-lookup"><span data-stu-id="fa135-155">Total size</span></span>|  
|<span data-ttu-id="fa135-156">Primeira unidade</span><span class="sxs-lookup"><span data-stu-id="fa135-156">First Drive</span></span>|<span data-ttu-id="fa135-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="fa135-157">H:\Video1</span></span>|<span data-ttu-id="fa135-158">2,5 TB + 30 GB</span><span class="sxs-lookup"><span data-stu-id="fa135-158">2.5 TB + 30 GB</span></span>|  
||<span data-ttu-id="fa135-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="fa135-159">H:\Photo</span></span>||  
|<span data-ttu-id="fa135-160">Segunda unidade</span><span class="sxs-lookup"><span data-stu-id="fa135-160">Second Drive</span></span>|<span data-ttu-id="fa135-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="fa135-161">H:\Video2</span></span>|<span data-ttu-id="fa135-162">2,5 TB + 35 GB</span><span class="sxs-lookup"><span data-stu-id="fa135-162">2.5 TB + 35 GB</span></span>|  
||<span data-ttu-id="fa135-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="fa135-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="fa135-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="fa135-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="fa135-165">Além disso, você pode definir os metadados para todos os arquivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa135-165">In addition, you can set the following metadata for all files:</span></span>  
  
-   <span data-ttu-id="fa135-166">**UploadMethod:** serviço de Importação/Exportação do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="fa135-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="fa135-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="fa135-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="fa135-168">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="fa135-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="fa135-169">Para definir metadados para os arquivos importados, crie um arquivo de texto `c:\WAImportExport\SampleMetadata.txt`, com o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="fa135-169">To set metadata for the imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with the following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="fa135-170">Você também pode definir algumas propriedades para o `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="fa135-170">You can also set some properties for the `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="fa135-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="fa135-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="fa135-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="fa135-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="fa135-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="fa135-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="fa135-174">Para definir essas propriedades, crie um arquivo de texto `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="fa135-174">To set these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="fa135-175">Agora você está pronto para executar a Ferramenta de Importação/Exportação do Azure para preparar as duas unidades de disco rígido.</span><span class="sxs-lookup"><span data-stu-id="fa135-175">Now you are ready to run the Azure Import/Export Tool to prepare the two hard drives.</span></span> <span data-ttu-id="fa135-176">Observe que:</span><span class="sxs-lookup"><span data-stu-id="fa135-176">Note that:</span></span>  
  
-   <span data-ttu-id="fa135-177">A primeira unidade é montada como unidade X.</span><span class="sxs-lookup"><span data-stu-id="fa135-177">The first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="fa135-178">A segunda unidade é montada como unidade Y.</span><span class="sxs-lookup"><span data-stu-id="fa135-178">The second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="fa135-179">A chave da conta de armazenamento `mystorageaccount` é `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="fa135-179">The key for the storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="fa135-180">Preparando o disco para importação quando dados são carregados previamente</span><span class="sxs-lookup"><span data-stu-id="fa135-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="fa135-181">Se os dados a serem importados já estão presentes no disco, use o sinalizador /skipwrite.</span><span class="sxs-lookup"><span data-stu-id="fa135-181">If the data to be imported is already present on the disk, use the flag /skipwrite.</span></span> <span data-ttu-id="fa135-182">O valor de /t e /srcdir deve apontar para o disco que está sendo preparado para importação.</span><span class="sxs-lookup"><span data-stu-id="fa135-182">The value of /t and /srcdir should both point to the disk being prepared for import.</span></span> <span data-ttu-id="fa135-183">Se todos os dados a serem importados não forem para o mesmo diretório virtual de destino ou raiz da conta de armazenamento, execute o mesmo comando para cada diretório de destino separadamente, mantendo o valor de /id o mesmo em todas as execuções.</span><span class="sxs-lookup"><span data-stu-id="fa135-183">If all of the data to be imported is not going to the same destination virtual directory or root of the storage account, run the same command for each destination directory separately, keeping the value of /id the same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="fa135-184">Não especifique /format, pois ele apagará os dados no disco.</span><span class="sxs-lookup"><span data-stu-id="fa135-184">Do not specify /format as it will wipe the data on the disk.</span></span> <span data-ttu-id="fa135-185">Você pode especificar / criptografar ou /bk dependendo se o disco já está criptografado ou não.</span><span class="sxs-lookup"><span data-stu-id="fa135-185">You can specify /encrypt or /bk depending on whether the disk is already encrypted or not.</span></span> 
>

```
    When data is already present on the disk for each drive run the following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="fa135-186">Sessões de cópia — primeira unidade</span><span class="sxs-lookup"><span data-stu-id="fa135-186">Copy sessions - first drive</span></span>

<span data-ttu-id="fa135-187">Para a primeira unidade, execute a Ferramenta de Importação/Exportação do Azure duas vezes para copiar os dois diretórios de origem:</span><span class="sxs-lookup"><span data-stu-id="fa135-187">For the first drive, run the Azure Import/Export Tool twice to copy the two source directories:</span></span>  

<span data-ttu-id="fa135-188">**Primeira sessão de cópia**</span><span class="sxs-lookup"><span data-stu-id="fa135-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="fa135-189">**Segunda sessão de cópia**</span><span class="sxs-lookup"><span data-stu-id="fa135-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="fa135-190">Sessões de cópia — segunda unidade</span><span class="sxs-lookup"><span data-stu-id="fa135-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="fa135-191">Para a segunda unidade, execute a Ferramenta de Importação/Exportação do Azure três vezes, uma vez para cada diretório de origem e uma vez para o arquivo de imagem autônomo Blu-Ray™):</span><span class="sxs-lookup"><span data-stu-id="fa135-191">For the second drive, run the Azure Import/Export Tool three times, once each for the source directories, and once for the standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="fa135-192">**Primeira sessão de cópia**</span><span class="sxs-lookup"><span data-stu-id="fa135-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="fa135-193">**Segunda sessão de cópia**</span><span class="sxs-lookup"><span data-stu-id="fa135-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="fa135-194">**Terceira sessão de cópia**</span><span class="sxs-lookup"><span data-stu-id="fa135-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="fa135-195">Conclusão da sessão de cópia</span><span class="sxs-lookup"><span data-stu-id="fa135-195">Copy session completion</span></span>

<span data-ttu-id="fa135-196">Depois de concluir as sessões de cópia, você pode desconectar as duas unidades do computador de cópia e enviá-las para o datacenter do Microsoft Azure apropriado.</span><span class="sxs-lookup"><span data-stu-id="fa135-196">Once the copy sessions have completed, you can disconnect the two drives from the copy computer and ship them to the appropriate Windows Azure data center.</span></span> <span data-ttu-id="fa135-197">Carregue os dois arquivos do diário, `FirstDrive.jrn` e `SecondDrive.jrn`, quando criar o trabalho de importação no [Portal do Microsoft Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="fa135-197">Upload the two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create the import job in the [Windows Azure portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="fa135-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fa135-198">Next steps</span></span>

* [<span data-ttu-id="fa135-199">Preparação de discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="fa135-199">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="fa135-200">Referência rápida para comandos usados frequentemente</span><span class="sxs-lookup"><span data-stu-id="fa135-200">Quick reference for frequently used commands</span></span>](../storage-import-export-tool-quick-reference-v1.md) 
