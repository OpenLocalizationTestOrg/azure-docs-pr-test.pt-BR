---
title: "trabalho - v1 de importação de aaaSample fluxo de trabalho tooprep unidades de disco rígido para uma importação/exportação do Azure | Microsoft Docs"
description: "Veja um passo a passo para o processo completo de saudação preparar unidades para um trabalho de importação no hello serviço de importação/exportação do Azure."
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
ms.openlocfilehash: f836fc6104d8b4ad5660cb110a62f61b40b0b7ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="044ad-103">Discos rígidos de tooprepare do fluxo de trabalho de exemplo para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="044ad-103">Sample workflow tooprepare hard drives for an import job</span></span>
<span data-ttu-id="044ad-104">Este tópico o orienta pelo processo de conclusão de saudação preparar unidades para um trabalho de importação.</span><span class="sxs-lookup"><span data-stu-id="044ad-104">This topic walks you through hello complete process of preparing drives for an import job.</span></span>  
  
<span data-ttu-id="044ad-105">Este exemplo importa Olá seguintes dados em uma conta de armazenamento do Windows Azure denominada `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="044ad-105">This example imports hello following data into a Window Azure storage account named `mystorageaccount`:</span></span>  
  
|<span data-ttu-id="044ad-106">Local</span><span class="sxs-lookup"><span data-stu-id="044ad-106">Location</span></span>|<span data-ttu-id="044ad-107">Descrição</span><span class="sxs-lookup"><span data-stu-id="044ad-107">Description</span></span>|  
|--------------|-----------------|  
|<span data-ttu-id="044ad-108">H:\Video</span><span class="sxs-lookup"><span data-stu-id="044ad-108">H:\Video</span></span>|<span data-ttu-id="044ad-109">Uma coleção de vídeos, 5 TB no total.</span><span class="sxs-lookup"><span data-stu-id="044ad-109">A collection of videos, 5 TB in total.</span></span>|  
|<span data-ttu-id="044ad-110">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="044ad-110">H:\Photo</span></span>|<span data-ttu-id="044ad-111">Uma coleção de fotos, 30 GB no total.</span><span class="sxs-lookup"><span data-stu-id="044ad-111">A collection of photos, 30 GB in total.</span></span>|  
|<span data-ttu-id="044ad-112">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="044ad-112">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="044ad-113">Uma imagem de disco Blu-ray™, 25 GB.</span><span class="sxs-lookup"><span data-stu-id="044ad-113">A Blu-Ray™ disk image, 25 GB.</span></span>|  
|<span data-ttu-id="044ad-114">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="044ad-114">\\\bigshare\john\music</span></span>|<span data-ttu-id="044ad-115">Uma coleção de arquivos de música em um compartilhamento de rede, 10 GB no total.</span><span class="sxs-lookup"><span data-stu-id="044ad-115">A collection of music files on a network share, 10 GB in total.</span></span>|  
  
<span data-ttu-id="044ad-116">trabalho de importação Olá importará esses dados para Olá destinos na conta de armazenamento Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="044ad-116">hello import job will import this data into hello following destinations in hello storage account:</span></span>  
  
|<span data-ttu-id="044ad-117">Fonte</span><span class="sxs-lookup"><span data-stu-id="044ad-117">Source</span></span>|<span data-ttu-id="044ad-118">Blob de destino ou diretório virtual</span><span class="sxs-lookup"><span data-stu-id="044ad-118">Destination virtual directory or blob</span></span>|  
|------------|-------------------------------------------|  
|<span data-ttu-id="044ad-119">H:\Video</span><span class="sxs-lookup"><span data-stu-id="044ad-119">H:\Video</span></span>|<span data-ttu-id="044ad-120">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="044ad-120">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="044ad-121">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="044ad-121">H:\Photo</span></span>|<span data-ttu-id="044ad-122">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="044ad-122">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="044ad-123">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="044ad-123">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="044ad-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="044ad-124">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="044ad-125">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="044ad-125">\\\bigshare\john\music</span></span>|<span data-ttu-id="044ad-126">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="044ad-126">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
<span data-ttu-id="044ad-127">Com esse mapeamento, Olá arquivo `H:\Video\Drama\GreatMovie.mov` serão importados toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="044ad-127">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>  
  
<span data-ttu-id="044ad-128">Em seguida, toodetermine quantos discos rígidos necessários, computação Olá tamanho dos dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="044ad-128">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>  
  
`5TB + 30GB + 25GB + 10GB = 5TB + 65GB`  
  
<span data-ttu-id="044ad-129">Neste exemplo, duas unidades de disco rígido de 3TB devem ser suficientes.</span><span class="sxs-lookup"><span data-stu-id="044ad-129">For this example, two 3TB hard drives should be sufficient.</span></span> <span data-ttu-id="044ad-130">No entanto, como o diretório de origem Olá `H:\Video` tem 5TB de dados e a capacidade do disco rígido único é apenas 3TB, é necessário toobreak `H:\Video` em dois diretórios secundários antes de executar Olá ferramenta de importação/exportação do Microsoft Azure: `H:\Video1` e `H:\Video2`.</span><span class="sxs-lookup"><span data-stu-id="044ad-130">However, since hello source directory `H:\Video` has 5TB of data and your single hard drive's capacity is only 3TB, it's necessary toobreak `H:\Video` into two smaller directories before running hello Microsoft Azure Import/Export Tool: `H:\Video1` and `H:\Video2`.</span></span> <span data-ttu-id="044ad-131">Esta etapa gera Olá diretórios de origem a seguir:</span><span class="sxs-lookup"><span data-stu-id="044ad-131">This step yields hello following source directories:</span></span>  
  
|<span data-ttu-id="044ad-132">Local</span><span class="sxs-lookup"><span data-stu-id="044ad-132">Location</span></span>|<span data-ttu-id="044ad-133">Tamanho</span><span class="sxs-lookup"><span data-stu-id="044ad-133">Size</span></span>|<span data-ttu-id="044ad-134">Blob de destino ou diretório virtual</span><span class="sxs-lookup"><span data-stu-id="044ad-134">Destination virtual directory or blob</span></span>|  
|--------------|----------|-------------------------------------------|  
|<span data-ttu-id="044ad-135">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="044ad-135">H:\Video1</span></span>|<span data-ttu-id="044ad-136">2,5 TB</span><span class="sxs-lookup"><span data-stu-id="044ad-136">2.5TB</span></span>|<span data-ttu-id="044ad-137">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="044ad-137">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="044ad-138">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="044ad-138">H:\Video2</span></span>|<span data-ttu-id="044ad-139">2,5 TB</span><span class="sxs-lookup"><span data-stu-id="044ad-139">2.5TB</span></span>|<span data-ttu-id="044ad-140">https://mystorageaccount.blob.core.windows.net/video</span><span class="sxs-lookup"><span data-stu-id="044ad-140">https://mystorageaccount.blob.core.windows.net/video</span></span>|  
|<span data-ttu-id="044ad-141">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="044ad-141">H:\Photo</span></span>|<span data-ttu-id="044ad-142">30GB</span><span class="sxs-lookup"><span data-stu-id="044ad-142">30GB</span></span>|<span data-ttu-id="044ad-143">https://mystorageaccount.blob.core.windows.net/photo</span><span class="sxs-lookup"><span data-stu-id="044ad-143">https://mystorageaccount.blob.core.windows.net/photo</span></span>|  
|<span data-ttu-id="044ad-144">K:\Temp\FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="044ad-144">K:\Temp\FavoriteMovies.ISO</span></span>|<span data-ttu-id="044ad-145">25 GB</span><span class="sxs-lookup"><span data-stu-id="044ad-145">25GB</span></span>|<span data-ttu-id="044ad-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="044ad-146">https://mystorageaccount.blob.core.windows.net/favorite/FavoriteMovies.ISO</span></span>|  
|<span data-ttu-id="044ad-147">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="044ad-147">\\\bigshare\john\music</span></span>|<span data-ttu-id="044ad-148">10GB</span><span class="sxs-lookup"><span data-stu-id="044ad-148">10GB</span></span>|<span data-ttu-id="044ad-149">https://mystorageaccount.blob.core.windows.net/music</span><span class="sxs-lookup"><span data-stu-id="044ad-149">https://mystorageaccount.blob.core.windows.net/music</span></span>|  
  
 <span data-ttu-id="044ad-150">Observe que, embora Olá `H:\Video`diretório seja dividido tootwo diretórios, eles apontam toohello mesmo diretório virtual de destino na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="044ad-150">Note that even though hello `H:\Video`directory has been split tootwo directories, they point toohello same destination virtual directory in hello storage account.</span></span> <span data-ttu-id="044ad-151">Dessa forma, todos os arquivos de vídeos são mantidos em um único `video` contêiner na conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="044ad-151">This way, all video files are maintained under a single `video` container in hello storage account.</span></span>  
  
 <span data-ttu-id="044ad-152">Em seguida, Olá acima fonte diretórios são uniformemente distribuído toohello dois discos rígidos:</span><span class="sxs-lookup"><span data-stu-id="044ad-152">Next, hello above source directories are evenly distributed toohello two hard drives:</span></span>  
  
||||  
|-|-|-|  
|<span data-ttu-id="044ad-153">Disco rígido</span><span class="sxs-lookup"><span data-stu-id="044ad-153">Hard drive</span></span>|<span data-ttu-id="044ad-154">Diretórios de origem</span><span class="sxs-lookup"><span data-stu-id="044ad-154">Source directories</span></span>|<span data-ttu-id="044ad-155">Tamanho total</span><span class="sxs-lookup"><span data-stu-id="044ad-155">Total size</span></span>|  
|<span data-ttu-id="044ad-156">Primeira unidade</span><span class="sxs-lookup"><span data-stu-id="044ad-156">First Drive</span></span>|<span data-ttu-id="044ad-157">H:\Video1</span><span class="sxs-lookup"><span data-stu-id="044ad-157">H:\Video1</span></span>|<span data-ttu-id="044ad-158">2.5TB + 30GB</span><span class="sxs-lookup"><span data-stu-id="044ad-158">2.5TB + 30GB</span></span>|  
||<span data-ttu-id="044ad-159">H:\Photo</span><span class="sxs-lookup"><span data-stu-id="044ad-159">H:\Photo</span></span>||  
|<span data-ttu-id="044ad-160">Segunda unidade</span><span class="sxs-lookup"><span data-stu-id="044ad-160">Second Drive</span></span>|<span data-ttu-id="044ad-161">H:\Video2</span><span class="sxs-lookup"><span data-stu-id="044ad-161">H:\Video2</span></span>|<span data-ttu-id="044ad-162">2.5TB + 35GB</span><span class="sxs-lookup"><span data-stu-id="044ad-162">2.5TB + 35GB</span></span>|  
||<span data-ttu-id="044ad-163">K:\Temp\BlueRay.ISO</span><span class="sxs-lookup"><span data-stu-id="044ad-163">K:\Temp\BlueRay.ISO</span></span>||  
||<span data-ttu-id="044ad-164">\\\bigshare\john\music</span><span class="sxs-lookup"><span data-stu-id="044ad-164">\\\bigshare\john\music</span></span>||  
  
<span data-ttu-id="044ad-165">Além disso, você pode definir Olá metadados para todos os arquivos a seguir:</span><span class="sxs-lookup"><span data-stu-id="044ad-165">In addition, you can set hello following metadata for all files:</span></span>  
  
-   <span data-ttu-id="044ad-166">**UploadMethod:** serviço de Importação/Exportação do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="044ad-166">**UploadMethod:** Windows Azure Import/Export service</span></span>  
  
-   <span data-ttu-id="044ad-167">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="044ad-167">**DataSetName:** SampleData</span></span>  
  
-   <span data-ttu-id="044ad-168">**CreationDate:** 10/1/2013</span><span class="sxs-lookup"><span data-stu-id="044ad-168">**CreationDate:** 10/1/2013</span></span>  
  
<span data-ttu-id="044ad-169">tooset metadados para arquivos de saudação importado, crie um arquivo de texto, `c:\WAImportExport\SampleMetadata.txt`, com hello conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="044ad-169">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="044ad-170">Você também pode definir algumas propriedades para Olá `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="044ad-170">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>  
  
-   <span data-ttu-id="044ad-171">**Content-Type:** application/octet-stream</span><span class="sxs-lookup"><span data-stu-id="044ad-171">**Content-Type:** application/octet-stream</span></span>  
  
-   <span data-ttu-id="044ad-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span><span class="sxs-lookup"><span data-stu-id="044ad-172">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>  
  
-   <span data-ttu-id="044ad-173">**Cache-Control:** no-cache</span><span class="sxs-lookup"><span data-stu-id="044ad-173">**Cache-Control:** no-cache</span></span>  
  
<span data-ttu-id="044ad-174">tooset essas propriedades, crie um arquivo de texto, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="044ad-174">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="044ad-175">Agora você está pronto toorun Olá ferramenta de importação/exportação do Azure tooprepare Olá duas unidades de disco rígido.</span><span class="sxs-lookup"><span data-stu-id="044ad-175">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span> <span data-ttu-id="044ad-176">Observe que:</span><span class="sxs-lookup"><span data-stu-id="044ad-176">Note that:</span></span>  
  
-   <span data-ttu-id="044ad-177">Olá primeira unidade é gerada como a unidade X.</span><span class="sxs-lookup"><span data-stu-id="044ad-177">hello first drive is mounted as drive X.</span></span>  
  
-   <span data-ttu-id="044ad-178">Olá segunda unidade é gerada como a unidade Y.</span><span class="sxs-lookup"><span data-stu-id="044ad-178">hello second drive is mounted as drive Y.</span></span>  
  
-   <span data-ttu-id="044ad-179">Olá chave Olá conta de armazenamento `mystorageaccount` é `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span><span class="sxs-lookup"><span data-stu-id="044ad-179">hello key for hello storage account `mystorageaccount` is `8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg==`.</span></span>  

## <a name="preparing-disk-for-import-when-data-is-pre-loaded"></a><span data-ttu-id="044ad-180">Preparando o disco para importação quando dados são carregados previamente</span><span class="sxs-lookup"><span data-stu-id="044ad-180">Preparing disk for import when data is pre-loaded</span></span>
 
 <span data-ttu-id="044ad-181">Se Olá dados toobe importado já está presente no disco hello, use Olá sinalizador /skipwrite.</span><span class="sxs-lookup"><span data-stu-id="044ad-181">If hello data toobe imported is already present on hello disk, use hello flag /skipwrite.</span></span> <span data-ttu-id="044ad-182">Valor de /t e /srcdir deve apontar toohello disco que está sendo preparado para importação.</span><span class="sxs-lookup"><span data-stu-id="044ad-182">Value of /t and /srcdir both should point toohello disk being prepared for import.</span></span> <span data-ttu-id="044ad-183">Se nem todos os Olá dados em disco Olá precisa toogo toohello mesmo diretório virtual de destino ou raiz da conta de armazenamento de Olá Olá execução mesmo comando para cada diretório separadamente mantendo o valor de saudação do /id mesmo em todas as execuções.</span><span class="sxs-lookup"><span data-stu-id="044ad-183">If not all hello data on hello disk needs toogo toohello same destination virtual directory or root of hello storage account, run hello same command for each directory separately keeping hello value of /id same across all runs.</span></span>

>[!NOTE] 
><span data-ttu-id="044ad-184">Não especifique /format como ele será apagar dados de Olá no disco hello.</span><span class="sxs-lookup"><span data-stu-id="044ad-184">Do not specify /format as it will wipe hello data on hello disk.</span></span> <span data-ttu-id="044ad-185">Você pode especificar / criptografar ou /bk dependendo se o disco de saudação já está criptografado ou não.</span><span class="sxs-lookup"><span data-stu-id="044ad-185">You can specify /encrypt or /bk depending on whether hello disk is already encrypted or not.</span></span> 
>

```
    When data is already present on hello disk for each drive run hello following command.
    WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:x:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt /skipwrite
```

## <a name="copy-sessions---first-drive"></a><span data-ttu-id="044ad-186">Sessões de cópia — primeira unidade</span><span class="sxs-lookup"><span data-stu-id="044ad-186">Copy sessions - first drive</span></span>

<span data-ttu-id="044ad-187">Para a primeira unidade de hello, execute Olá, ferramenta de importação/exportação do Azure da fonte de duas vezes Olá toocopy dois diretórios:</span><span class="sxs-lookup"><span data-stu-id="044ad-187">For hello first drive, run hello Azure Import/Export Tool twice toocopy hello two source directories:</span></span>  

<span data-ttu-id="044ad-188">**Primeira sessão de cópia**</span><span class="sxs-lookup"><span data-stu-id="044ad-188">**First copy session**</span></span>
  
```
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Video1 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:H:\Video1 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```

<span data-ttu-id="044ad-189">**Segunda sessão de cópia**</span><span class="sxs-lookup"><span data-stu-id="044ad-189">**Second copy session**</span></span>

```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:Photo /srcdir:H:\Photo /dstdir:photo/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt
```

## <a name="copy-sessions---second-drive"></a><span data-ttu-id="044ad-190">Sessões de cópia — segunda unidade</span><span class="sxs-lookup"><span data-stu-id="044ad-190">Copy sessions - second drive</span></span>
 
<span data-ttu-id="044ad-191">Para Olá segunda unidade, execute Olá ferramenta de importação/exportação do Azure três vezes, uma vez para Olá diretórios de origem e uma vez para Olá autônomo Blu-Ray™ arquivo de imagem):</span><span class="sxs-lookup"><span data-stu-id="044ad-191">For hello second drive, run hello Azure Import/Export Tool three times, once each for hello source directories, and once for hello standalone Blu-Ray™ image file):</span></span>  
  
<span data-ttu-id="044ad-192">**Primeira sessão de cópia**</span><span class="sxs-lookup"><span data-stu-id="044ad-192">**First copy session**</span></span> 

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Video2 /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:y /format /encrypt /srcdir:H:\Video2 /dstdir:video/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```
  
<span data-ttu-id="044ad-193">**Segunda sessão de cópia**</span><span class="sxs-lookup"><span data-stu-id="044ad-193">**Second copy session**</span></span>

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:Music /srcdir:\\bigshare\john\music /dstdir:music/ /MetadataFile:c:\WAImportExport\SampleMetadata.txt  
```  
  
<span data-ttu-id="044ad-194">**Terceira sessão de cópia**</span><span class="sxs-lookup"><span data-stu-id="044ad-194">**Third copy session**</span></span>  

```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```

## <a name="copy-session-completion"></a><span data-ttu-id="044ad-195">Conclusão da sessão de cópia</span><span class="sxs-lookup"><span data-stu-id="044ad-195">Copy session completion</span></span>

<span data-ttu-id="044ad-196">Depois de concluir as sessões de cópia de Olá, você pode desconectar duas unidades de saudação do computador de cópia hello e enviá-las toohello apropriado do Windows Azure Datacenter.</span><span class="sxs-lookup"><span data-stu-id="044ad-196">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Windows Azure data center.</span></span> <span data-ttu-id="044ad-197">Você vai carregar arquivos de diário de saudação dois `FirstDrive.jrn` e `SecondDrive.jrn`, ao criar trabalho de importação Olá Olá [Portal de gerenciamento do Windows Azure](https://manage.windowsazure.com/).</span><span class="sxs-lookup"><span data-stu-id="044ad-197">You'll upload hello two journal files, `FirstDrive.jrn` and `SecondDrive.jrn`, when you create hello import job in hello [Windows Azure Management Portal](https://manage.windowsazure.com/).</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="044ad-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="044ad-198">Next steps</span></span>

* [<span data-ttu-id="044ad-199">Preparação de discos rígidos para um trabalho de importação</span><span class="sxs-lookup"><span data-stu-id="044ad-199">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="044ad-200">Referência rápida para comandos usados frequentemente</span><span class="sxs-lookup"><span data-stu-id="044ad-200">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference-v1.md) 
