---
title: "Introdução ao armazenamento de Blobs do Azure | Microsoft Docs"
description: "Introdução ao armazenamento de Blobs do Azure"
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
ms.openlocfilehash: 051f1b37eab254d4ab4f806166ac8d0b8cab944d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-blob-storage"></a><span data-ttu-id="a37bf-103">Introdução ao armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="a37bf-103">Introduction to Blob storage</span></span>

<span data-ttu-id="a37bf-104">A Armazenamento de Blobs do Azure é um serviço para armazenar grandes quantidades de dados de objeto não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar do mundo por meio de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a37bf-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="a37bf-105">Você pode usar o armazenamento de Blob para expor dados publicamente para o mundo ou para armazenar dados do aplicativo de forma privada.</span><span class="sxs-lookup"><span data-stu-id="a37bf-105">You can use Blob storage to expose data publicly to the world, or to store application data privately.</span></span>

<span data-ttu-id="a37bf-106">Usos comuns de armazenamento de Blob incluem:</span><span class="sxs-lookup"><span data-stu-id="a37bf-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="a37bf-107">Fornecer imagens ou documentos diretamente a um navegador</span><span class="sxs-lookup"><span data-stu-id="a37bf-107">Serving images or documents directly to a browser</span></span>
* <span data-ttu-id="a37bf-108">Armazenar arquivos para acesso distribuído</span><span class="sxs-lookup"><span data-stu-id="a37bf-108">Storing files for distributed access</span></span>
* <span data-ttu-id="a37bf-109">Transmitir por streaming áudio e vídeo</span><span class="sxs-lookup"><span data-stu-id="a37bf-109">Streaming video and audio</span></span>
* <span data-ttu-id="a37bf-110">Armazenamento de dados de backup e restauração, recuperação de desastres e arquivamento</span><span class="sxs-lookup"><span data-stu-id="a37bf-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="a37bf-111">Armazenando dados para análise por um serviço local ou hospedado do Azure</span><span class="sxs-lookup"><span data-stu-id="a37bf-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="a37bf-112">Conceitos do Serviço Blob</span><span class="sxs-lookup"><span data-stu-id="a37bf-112">Blob service concepts</span></span>

<span data-ttu-id="a37bf-113">O serviço Blob contém os seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="a37bf-113">The Blob service contains the following components:</span></span>

![Arquitetura de blob](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="a37bf-115">**Conta de Armazenamento:** todo o acesso ao Armazenamento do Azure é feito através de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a37bf-115">**Storage Account:** All access to Azure Storage is done through a storage account.</span></span> <span data-ttu-id="a37bf-116">Essa conta de armazenamento pode ser uma **conta de armazenamento** de uso geral ou uma **conta de Armazenamento de Blobs**, que é especializada em armazenar objetos/blobs.</span><span class="sxs-lookup"><span data-stu-id="a37bf-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="a37bf-117">Consulte [Sobre as contas de armazenamento do Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="a37bf-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="a37bf-118">**Contêiner:** um contêiner fornece um agrupamento de conjunto de blobs.</span><span class="sxs-lookup"><span data-stu-id="a37bf-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="a37bf-119">Todos os blobs devem ter um contêiner.</span><span class="sxs-lookup"><span data-stu-id="a37bf-119">All blobs must be in a container.</span></span> <span data-ttu-id="a37bf-120">Uma conta pode conter um número ilimitado de contêineres.</span><span class="sxs-lookup"><span data-stu-id="a37bf-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="a37bf-121">Um contêiner pode armazenar um número ilimitado de blobs.</span><span class="sxs-lookup"><span data-stu-id="a37bf-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="a37bf-122">Observe que o nome do contêiner deve estar em letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="a37bf-122">Note that the container name must be lowercase.</span></span>

* <span data-ttu-id="a37bf-123">**Blob:** um arquivo de qualquer tipo e tamanho.</span><span class="sxs-lookup"><span data-stu-id="a37bf-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="a37bf-124">O armazenamento do Azure oferece três tipos de blobs: blob de blocos, blob de páginas e blob de anexo.</span><span class="sxs-lookup"><span data-stu-id="a37bf-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="a37bf-125">*Blobs de blocos* são ideais para armazenar arquivos de texto ou binários, como documentos e arquivos de mídia.</span><span class="sxs-lookup"><span data-stu-id="a37bf-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="a37bf-126">*Blobs de anexo* são semelhantes aos blobs de blocos, pois são constituídos de blocos, mas são otimizados para anexas operações. Portanto, são úteis em cenários de registro em log.</span><span class="sxs-lookup"><span data-stu-id="a37bf-126">*Append blobs* are similar to block blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="a37bf-127">Um blob de blocos único pode conter até 50.000 blocos de até 100 MB cada um, com um tamanho total de pouco mais de 4,75 TB (100 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="a37bf-127">A single block blob can contain up to 50,000 blocks of up to 100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="a37bf-128">Um blob de acréscimo único pode conter até 50.000 blocos de até 4 MB cada um, com um tamanho total de pouco mais de 195 GB (4 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="a37bf-128">A single append blob can contain up to 50,000 blocks of up to 4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="a37bf-129">*Blobs de páginas* podem ter até 1 TB e são mais eficientes para operações frequentes de leitura/gravação.</span><span class="sxs-lookup"><span data-stu-id="a37bf-129">*Page blobs* can be up to 1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="a37bf-130">Máquinas virtuais do Azure usam blobs de páginas como sistema operacional e discos de dados.</span><span class="sxs-lookup"><span data-stu-id="a37bf-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="a37bf-131">Para obter detalhes sobre como nomear contêineres e blobs, confira [Nomenclatura e referência de contêineres, blobs e metadados](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span><span class="sxs-lookup"><span data-stu-id="a37bf-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a37bf-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a37bf-132">Next steps</span></span>

* [<span data-ttu-id="a37bf-133">Criar uma conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a37bf-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="a37bf-134">Introdução ao armazenamento de blobs usando .NET</span><span class="sxs-lookup"><span data-stu-id="a37bf-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)