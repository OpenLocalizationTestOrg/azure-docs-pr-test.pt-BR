---
title: "uso da unidade aaaPreviewing para um trabalho de exportação de importação/exportação do Azure - v1 | Microsoft Docs"
description: "Saiba como lista de saudação toopreview de blobs que você tiver selecionado para um trabalho de exportação no serviço de importação/exportação do Azure hello."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 7378c159f6d11702cda9ae7654e84d85f9b671b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="2151b-103">Visualizando o uso da unidade de um trabalho de exportação</span><span class="sxs-lookup"><span data-stu-id="2151b-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="2151b-104">Antes de criar um trabalho de exportação, você precisa toochoose um conjunto de blobs toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="2151b-104">Before you create an export job, you need toochoose a set of blobs toobe exported.</span></span> <span data-ttu-id="2151b-105">Olá serviço de importação/exportação do Microsoft Azure permite que você toouse uma lista de caminhos de blob ou prefixos de blob blobs de saudação toorepresent que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="2151b-105">hello Microsoft Azure Import/Export service allows you toouse a list of blob paths or blob prefixes toorepresent hello blobs you've selected.</span></span>  
  
<span data-ttu-id="2151b-106">Em seguida, você precisa toodetermine quantas unidades você precisa toosend.</span><span class="sxs-lookup"><span data-stu-id="2151b-106">Next, you need toodetermine how many drives you need toosend.</span></span> <span data-ttu-id="2151b-107">Olá, ferramenta de importação/exportação fornece Olá `PreviewExport` uso de unidade do comando toopreview para blobs de saudação que você selecionou, com base no tamanho Olá Olá unidades que serão toouse.</span><span class="sxs-lookup"><span data-stu-id="2151b-107">hello Import/Export Tool provides hello `PreviewExport` command toopreview drive usage for hello blobs you selected, based on hello size of hello drives you are going toouse.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="2151b-108">Parâmetros de linha de comando</span><span class="sxs-lookup"><span data-stu-id="2151b-108">Command-line parameters</span></span>

<span data-ttu-id="2151b-109">Você pode usar o hello parâmetros a seguir ao usar o hello `PreviewExport` comando da ferramenta de importação/exportação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2151b-109">You can use hello following parameters when using hello `PreviewExport` command of hello Import/Export Tool.</span></span>

|<span data-ttu-id="2151b-110">Parâmetro de linha de comando</span><span class="sxs-lookup"><span data-stu-id="2151b-110">Command-line parameter</span></span>|<span data-ttu-id="2151b-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="2151b-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="2151b-112">**/logdir:**<LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="2151b-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="2151b-113">Opcional.</span><span class="sxs-lookup"><span data-stu-id="2151b-113">Optional.</span></span> <span data-ttu-id="2151b-114">diretório de log Hello.</span><span class="sxs-lookup"><span data-stu-id="2151b-114">hello log directory.</span></span> <span data-ttu-id="2151b-115">Arquivos de log detalhados serão gravados toothis directory.</span><span class="sxs-lookup"><span data-stu-id="2151b-115">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="2151b-116">Se nenhum diretório de log for especificado, diretório atual Olá será usado como diretório de log hello.</span><span class="sxs-lookup"><span data-stu-id="2151b-116">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="2151b-117">**/sn:**<StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="2151b-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="2151b-118">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2151b-118">Required.</span></span> <span data-ttu-id="2151b-119">trabalho de exportação de nome de Olá Olá da conta de armazenamento para hello.</span><span class="sxs-lookup"><span data-stu-id="2151b-119">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="2151b-120">**/sk:**<StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="2151b-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="2151b-121">Necessário somente se uma SAS do contêiner não for especificada.</span><span class="sxs-lookup"><span data-stu-id="2151b-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="2151b-122">trabalho de exportação da chave da conta Olá para conta de armazenamento Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="2151b-122">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="2151b-123">**/csas:**<ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="2151b-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="2151b-124">Necessário somente se uma chave de conta de armazenamento não for especificada.</span><span class="sxs-lookup"><span data-stu-id="2151b-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="2151b-125">SAS do contêiner Olá para listagem Olá blobs toobe exportados no trabalho de exportação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2151b-125">hello container SAS for listing hello blobs toobe exported in hello export job.</span></span>|  
|<span data-ttu-id="2151b-126">**/ExportBlobListFile:**<ExportBlobListFile\></span><span class="sxs-lookup"><span data-stu-id="2151b-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="2151b-127">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2151b-127">Required.</span></span> <span data-ttu-id="2151b-128">Toohello caminho XML arquivo contendo a lista de caminhos de blob ou prefixos de caminho para Olá blobs toobe exportados de blob.</span><span class="sxs-lookup"><span data-stu-id="2151b-128">Path toohello XML file containing list of blob paths or blob path prefixes for hello blobs toobe exported.</span></span> <span data-ttu-id="2151b-129">formato de arquivo Hello usado em Olá `BlobListBlobPath` elemento Olá [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação da API REST do serviço de importação/exportação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2151b-129">hello file format used in hello `BlobListBlobPath` element in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of hello Import/Export service REST API.</span></span>|  
|<span data-ttu-id="2151b-130">**/DriveSize:**<DriveSize\></span><span class="sxs-lookup"><span data-stu-id="2151b-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="2151b-131">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2151b-131">Required.</span></span> <span data-ttu-id="2151b-132">Olá tamanho de unidades toouse para um trabalho de exportação, *, por exemplo,*, 500GB, 1,5 TB.</span><span class="sxs-lookup"><span data-stu-id="2151b-132">hello size of drives toouse for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="2151b-133">Exemplo de linha de comando</span><span class="sxs-lookup"><span data-stu-id="2151b-133">Command-line example</span></span>

<span data-ttu-id="2151b-134">Olá, exemplo a seguir demonstra Olá `PreviewExport` comando:</span><span class="sxs-lookup"><span data-stu-id="2151b-134">hello following example demonstrates hello `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="2151b-135">Olá arquivo de lista de blob de exportação pode conter nomes de blob e prefixos de blob, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="2151b-135">hello export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="2151b-136">Olá, ferramenta de importação/exportação do Azure lista todos os toobe blobs exportados e calcula como toopack-los em unidades de saudação especificado tamanho, levando em consideração qualquer sobrecarga necessária, em seguida, calcula o número de saudação de unidades necessárias blobs de saudação toohold e o uso da unidade informações.</span><span class="sxs-lookup"><span data-stu-id="2151b-136">hello Azure Import/Export Tool lists all blobs toobe exported and calculates how toopack them into drives of hello specified size, taking into account any necessary overhead, then estimates hello number of drives needed toohold hello blobs and drive usage information.</span></span>  
  
<span data-ttu-id="2151b-137">Aqui está um exemplo de saída de hello, com logs informativos omitidos:</span><span class="sxs-lookup"><span data-stu-id="2151b-137">Here is an example of hello output, with informational logs omitted:</span></span>  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a><span data-ttu-id="2151b-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2151b-138">Next steps</span></span>

* [<span data-ttu-id="2151b-139">Referência da Ferramenta de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="2151b-139">Azure Import/Export Tool reference</span></span>](../storage-import-export-tool-how-to-v1.md)
