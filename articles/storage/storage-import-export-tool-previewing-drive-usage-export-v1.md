---
title: "Visualizando o uso da unidade de um trabalho de exportação do serviço de Importação/Exportação do Azure — v1 | Microsoft Docs"
description: "Saiba como visualizar a lista de blobs selecionada para um trabalho de exportação no serviço de Importação/Exportação do Azure."
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
ms.openlocfilehash: 7bf74247090f91e17f81a9bc98ebfa78334c8c10
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="d09ec-103">Visualizando o uso da unidade de um trabalho de exportação</span><span class="sxs-lookup"><span data-stu-id="d09ec-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="d09ec-104">Antes de criar um trabalho de exportação, você precisa escolher um conjunto de blobs a ser exportado.</span><span class="sxs-lookup"><span data-stu-id="d09ec-104">Before you create an export job, you need to choose a set of blobs to be exported.</span></span> <span data-ttu-id="d09ec-105">O serviço de Importação/Exportação do Microsoft Azure permite que você use uma lista de caminhos ou prefixos de blob para representar os blobs selecionados.</span><span class="sxs-lookup"><span data-stu-id="d09ec-105">The Microsoft Azure Import/Export service allows you to use a list of blob paths or blob prefixes to represent the blobs you've selected.</span></span>  
  
<span data-ttu-id="d09ec-106">Em seguida, é necessário determinar quantas unidades você precisa enviar.</span><span class="sxs-lookup"><span data-stu-id="d09ec-106">Next, you need to determine how many drives you need to send.</span></span> <span data-ttu-id="d09ec-107">A Ferramenta de Importação/Exportação fornece o comando `PreviewExport` para visualização do uso da unidade dos blobs selecionados, com base no tamanho das unidades que você pretende usar.</span><span class="sxs-lookup"><span data-stu-id="d09ec-107">The Import/Export Tool provides the `PreviewExport` command to preview drive usage for the blobs you selected, based on the size of the drives you are going to use.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="d09ec-108">Parâmetros de linha de comando</span><span class="sxs-lookup"><span data-stu-id="d09ec-108">Command-line parameters</span></span>

<span data-ttu-id="d09ec-109">Você pode usar os parâmetros a seguir com o comando `PreviewExport` da Ferramenta de Importação/Exportação.</span><span class="sxs-lookup"><span data-stu-id="d09ec-109">You can use the following parameters when using the `PreviewExport` command of the Import/Export Tool.</span></span>

|<span data-ttu-id="d09ec-110">Parâmetro de linha de comando</span><span class="sxs-lookup"><span data-stu-id="d09ec-110">Command-line parameter</span></span>|<span data-ttu-id="d09ec-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="d09ec-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="d09ec-112">**/logdir:**<LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="d09ec-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="d09ec-113">Opcional.</span><span class="sxs-lookup"><span data-stu-id="d09ec-113">Optional.</span></span> <span data-ttu-id="d09ec-114">O diretório de log.</span><span class="sxs-lookup"><span data-stu-id="d09ec-114">The log directory.</span></span> <span data-ttu-id="d09ec-115">Os arquivos de log detalhados serão gravados nesse diretório.</span><span class="sxs-lookup"><span data-stu-id="d09ec-115">Verbose log files will be written to this directory.</span></span> <span data-ttu-id="d09ec-116">Se nenhum diretório de log for especificado, o diretório atual será usado como o diretório de log.</span><span class="sxs-lookup"><span data-stu-id="d09ec-116">If no log directory is specified, the current directory will be used as the log directory.</span></span>|  
|<span data-ttu-id="d09ec-117">**/sn:**<StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="d09ec-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="d09ec-118">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="d09ec-118">Required.</span></span> <span data-ttu-id="d09ec-119">O nome da conta de armazenamento do trabalho de exportação.</span><span class="sxs-lookup"><span data-stu-id="d09ec-119">The name of the storage account for the export job.</span></span>|  
|<span data-ttu-id="d09ec-120">**/sk:**<StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="d09ec-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="d09ec-121">Necessário somente se uma SAS do contêiner não for especificada.</span><span class="sxs-lookup"><span data-stu-id="d09ec-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="d09ec-122">A chave de conta da conta de armazenamento do trabalho de exportação.</span><span class="sxs-lookup"><span data-stu-id="d09ec-122">The account key for the storage account for the export job.</span></span>|  
|<span data-ttu-id="d09ec-123">**/csas:**<ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="d09ec-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="d09ec-124">Necessário somente se uma chave de conta de armazenamento não for especificada.</span><span class="sxs-lookup"><span data-stu-id="d09ec-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="d09ec-125">A SAS do contêiner para listar os blobs a serem exportados no trabalho de exportação.</span><span class="sxs-lookup"><span data-stu-id="d09ec-125">The container SAS for listing the blobs to be exported in the export job.</span></span>|  
|<span data-ttu-id="d09ec-126">**/ExportBlobListFile:**<ExportBlobListFile\></span><span class="sxs-lookup"><span data-stu-id="d09ec-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="d09ec-127">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="d09ec-127">Required.</span></span> <span data-ttu-id="d09ec-128">Caminho até o arquivo XML que contém a lista de caminhos de blob ou prefixos de caminhos de blob para os blobs a serem exportados.</span><span class="sxs-lookup"><span data-stu-id="d09ec-128">Path to the XML file containing list of blob paths or blob path prefixes for the blobs to be exported.</span></span> <span data-ttu-id="d09ec-129">O formato de arquivo usado no elemento `BlobListBlobPath` da operação [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) da API REST do serviço de Importação/Exportação.</span><span class="sxs-lookup"><span data-stu-id="d09ec-129">The file format used in the `BlobListBlobPath` element in the [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of the Import/Export service REST API.</span></span>|  
|<span data-ttu-id="d09ec-130">**/DriveSize:**<DriveSize\></span><span class="sxs-lookup"><span data-stu-id="d09ec-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="d09ec-131">Obrigatório.</span><span class="sxs-lookup"><span data-stu-id="d09ec-131">Required.</span></span> <span data-ttu-id="d09ec-132">O tamanho das unidades a ser usado para um trabalho de exportação, *por exemplo*, 500 GB, 1,5 TB.</span><span class="sxs-lookup"><span data-stu-id="d09ec-132">The size of drives to use for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="d09ec-133">Exemplo de linha de comando</span><span class="sxs-lookup"><span data-stu-id="d09ec-133">Command-line example</span></span>

<span data-ttu-id="d09ec-134">O seguinte exemplo demonstra o comando `PreviewExport`:</span><span class="sxs-lookup"><span data-stu-id="d09ec-134">The following example demonstrates the `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="d09ec-135">O arquivo de lista de blobs de exportação pode conter nomes e prefixos de blob, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="d09ec-135">The export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="d09ec-136">A Ferramenta de Importação/Exportação do Azure lista todos os blobs a serem exportados e calcula como empacotá-los em unidades do tamanho especificado, levando em consideração qualquer sobrecarga necessária. Em seguida, estima o número de unidades necessárias para manter os blobs e as informações de uso da unidade.</span><span class="sxs-lookup"><span data-stu-id="d09ec-136">The Azure Import/Export Tool lists all blobs to be exported and calculates how to pack them into drives of the specified size, taking into account any necessary overhead, then estimates the number of drives needed to hold the blobs and drive usage information.</span></span>  
  
<span data-ttu-id="d09ec-137">Este é um exemplo da saída, com a omissão dos logs informativos:</span><span class="sxs-lookup"><span data-stu-id="d09ec-137">Here is an example of the output, with informational logs omitted:</span></span>  
  
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
  
## <a name="next-steps"></a><span data-ttu-id="d09ec-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d09ec-138">Next steps</span></span>

* [<span data-ttu-id="d09ec-139">Referência da Ferramenta de Importação/Exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="d09ec-139">Azure Import/Export Tool reference</span></span>](storage-import-export-tool-how-to-v1.md)
