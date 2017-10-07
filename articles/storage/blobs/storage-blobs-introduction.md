---
title: aaaIntroduction tooAzure armazenamento de Blob | Microsoft Docs
description: "Introdução tooAzure armazenamento de Blob"
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: robinsh
ms.openlocfilehash: 3431f826ae51d42dbced084ee60f9ff70a8168d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooblob-storage"></a><span data-ttu-id="59e50-103">Armazenamento de tooBlob de Introdução</span><span class="sxs-lookup"><span data-stu-id="59e50-103">Introduction tooBlob storage</span></span>

<span data-ttu-id="59e50-104">Armazenamento de BLOBs do Azure é um serviço para armazenar grandes quantidades de dados de objeto não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar Olá, mundo via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="59e50-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="59e50-105">Você pode usar dados de tooexpose de armazenamento de Blob publicamente toohello mundo ou toostore dados de aplicativo em particular.</span><span class="sxs-lookup"><span data-stu-id="59e50-105">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span>

<span data-ttu-id="59e50-106">Usos comuns de armazenamento de Blob incluem:</span><span class="sxs-lookup"><span data-stu-id="59e50-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="59e50-107">Serviço de imagens e documentos diretamente tooa navegador</span><span class="sxs-lookup"><span data-stu-id="59e50-107">Serving images or documents directly tooa browser</span></span>
* <span data-ttu-id="59e50-108">Armazenar arquivos para acesso distribuído</span><span class="sxs-lookup"><span data-stu-id="59e50-108">Storing files for distributed access</span></span>
* <span data-ttu-id="59e50-109">Transmitir por streaming áudio e vídeo</span><span class="sxs-lookup"><span data-stu-id="59e50-109">Streaming video and audio</span></span>
* <span data-ttu-id="59e50-110">Armazenamento de dados de backup e restauração, recuperação de desastres e arquivamento</span><span class="sxs-lookup"><span data-stu-id="59e50-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="59e50-111">Armazenando dados para análise por um serviço local ou hospedado do Azure</span><span class="sxs-lookup"><span data-stu-id="59e50-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="59e50-112">Conceitos do Serviço Blob</span><span class="sxs-lookup"><span data-stu-id="59e50-112">Blob service concepts</span></span>

<span data-ttu-id="59e50-113">Olá serviço Blob contém Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="59e50-113">hello Blob service contains hello following components:</span></span>

![Arquitetura de blob](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="59e50-115">**Conta de armazenamento:** todos os acessos tooAzure armazenamento é feito por meio de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="59e50-115">**Storage Account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="59e50-116">Essa conta de armazenamento pode ser uma **conta de armazenamento** de uso geral ou uma **conta de Armazenamento de Blobs**, que é especializada em armazenar objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="59e50-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="59e50-117">Consulte [Sobre as contas de armazenamento do Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="59e50-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="59e50-118">**Contêiner:** um contêiner fornece um agrupamento de conjunto de blobs.</span><span class="sxs-lookup"><span data-stu-id="59e50-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="59e50-119">Todos os blobs devem ter um contêiner.</span><span class="sxs-lookup"><span data-stu-id="59e50-119">All blobs must be in a container.</span></span> <span data-ttu-id="59e50-120">Uma conta pode conter um número ilimitado de contêineres.</span><span class="sxs-lookup"><span data-stu-id="59e50-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="59e50-121">Um contêiner pode armazenar um número ilimitado de blobs.</span><span class="sxs-lookup"><span data-stu-id="59e50-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="59e50-122">Observe que esse nome de contêiner Olá deve estar em minúscula.</span><span class="sxs-lookup"><span data-stu-id="59e50-122">Note that hello container name must be lowercase.</span></span>

* <span data-ttu-id="59e50-123">**Blob:** um arquivo de qualquer tipo e tamanho.</span><span class="sxs-lookup"><span data-stu-id="59e50-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="59e50-124">O armazenamento do Azure oferece três tipos de blobs: blob de blocos, blob de páginas e blob de anexo.</span><span class="sxs-lookup"><span data-stu-id="59e50-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="59e50-125">*Blobs de blocos* são ideais para armazenar arquivos de texto ou binários, como documentos e arquivos de mídia.</span><span class="sxs-lookup"><span data-stu-id="59e50-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="59e50-126">*Blobs de acréscimo* são semelhantes blobs de tooblock em que eles são compostos de blocos, mas eles são otimizados para operações de acréscimo, para que sejam úteis para cenários de registro em log.</span><span class="sxs-lookup"><span data-stu-id="59e50-126">*Append blobs* are similar tooblock blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="59e50-127">Um blob de bloco único pode conter o too50, 000 blocos de too100 MB cada, para um tamanho total de um pouco mais de 4,75 TB (100 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="59e50-127">A single block blob can contain up too50,000 blocks of up too100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="59e50-128">Um blob de acréscimo único pode conter o too50, 000 blocos de too4 MB cada, para um tamanho total de um pouco mais de 195 GB (4 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="59e50-128">A single append blob can contain up too50,000 blocks of up too4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="59e50-129">*Blobs de página* pode ser até too1 TB de tamanho e são mais eficientes para operações de leitura/gravação frequentes.</span><span class="sxs-lookup"><span data-stu-id="59e50-129">*Page blobs* can be up too1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="59e50-130">Máquinas virtuais do Azure usam blobs de páginas como sistema operacional e discos de dados.</span><span class="sxs-lookup"><span data-stu-id="59e50-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="59e50-131">Para obter detalhes sobre como nomear contêineres e blobs, confira [Nomenclatura e referência de contêineres, blobs e metadados](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span><span class="sxs-lookup"><span data-stu-id="59e50-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="59e50-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="59e50-132">Next steps</span></span>

* [<span data-ttu-id="59e50-133">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="59e50-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="59e50-134">Introdução ao armazenamento de blobs usando .NET</span><span class="sxs-lookup"><span data-stu-id="59e50-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)