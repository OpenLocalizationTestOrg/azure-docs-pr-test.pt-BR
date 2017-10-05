---
title: Exemplos do Armazenamento do Azure usando .NET | Microsoft Docs
description: "Exiba, baixe e execute exemplos de código e aplicativos para o Armazenamento do Azure. Descubra exemplos de introdução a blobs, filas, tabelas e arquivos usando as bibliotecas do cliente de armazenamento do .NET."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: d2b6b3d9483f230ad25ae47255a4f28c1a67e064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="2a8dc-104">Exemplos de Armazenamento do Azure usando .NET</span><span class="sxs-lookup"><span data-stu-id="2a8dc-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="2a8dc-105">Exemplo de índice do .NET</span><span class="sxs-lookup"><span data-stu-id="2a8dc-105">.NET sample index</span></span>

<span data-ttu-id="2a8dc-106">A tabela a seguir fornece uma visão geral do nosso repositório de exemplos e os cenários abordados em cada exemplo.</span><span class="sxs-lookup"><span data-stu-id="2a8dc-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="2a8dc-107">Clique nos links para exibir o código de exemplo correspondente no GitHub.</span><span class="sxs-lookup"><span data-stu-id="2a8dc-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="2a8dc-108">Ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="2a8dc-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="2a8dc-109">Cenário</span><span class="sxs-lookup"><span data-stu-id="2a8dc-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="2a8dc-110">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="2a8dc-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="2a8dc-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="2a8dc-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="2a8dc-112">Acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="2a8dc-112">Append Blob</span></span></td> 
<td><span data-ttu-id="2a8dc-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Exemplo do método CloudBlobContainer.GetAppendBlobReference</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-114">Blob de blocos</span><span class="sxs-lookup"><span data-stu-id="2a8dc-114">Block Blob</span></span></td>
<td><span data-ttu-id="2a8dc-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicativo Web de Galeria de Fotos do Armazenamento de Blobs do Azure</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-116">Criptografia do cliente</span><span class="sxs-lookup"><span data-stu-id="2a8dc-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="2a8dc-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Exemplos de criptografia de blob</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-118">Copiar blob</span><span class="sxs-lookup"><span data-stu-id="2a8dc-118">Copy Blob</span></span></td>
<td><span data-ttu-id="2a8dc-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-120">Create Container</span><span class="sxs-lookup"><span data-stu-id="2a8dc-120">Create Container</span></span></td>
<td><span data-ttu-id="2a8dc-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicativo Web de Galeria de Fotos do Armazenamento de Blobs do Azure</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-122">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="2a8dc-122">Delete Blob</span></span></td>
<td><span data-ttu-id="2a8dc-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicativo Web de Galeria de Fotos do Armazenamento de Blobs do Azure</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-124">Delete Container</span><span class="sxs-lookup"><span data-stu-id="2a8dc-124">Delete Container</span></span></td>
<td><span data-ttu-id="2a8dc-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-126">Metadados/propriedades/estatísticas de blob</span><span class="sxs-lookup"><span data-stu-id="2a8dc-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="2a8dc-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-128">ACL/metadados/propriedades de contêiner</span><span class="sxs-lookup"><span data-stu-id="2a8dc-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="2a8dc-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicativo Web de Galeria de Fotos do Armazenamento de Blobs do Azure</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-130">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="2a8dc-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="2a8dc-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-132">Blob/contêiner de concessão</span><span class="sxs-lookup"><span data-stu-id="2a8dc-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="2a8dc-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-134">Blob/contêiner de lista</span><span class="sxs-lookup"><span data-stu-id="2a8dc-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="2a8dc-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-136">Blob de páginas</span><span class="sxs-lookup"><span data-stu-id="2a8dc-136">Page Blob</span></span></td>
<td><span data-ttu-id="2a8dc-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="2a8dc-138">SAS</span><span class="sxs-lookup"><span data-stu-id="2a8dc-138">SAS</span></span></td>
<td><span data-ttu-id="2a8dc-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="2a8dc-140">Propriedades do serviço</span><span class="sxs-lookup"><span data-stu-id="2a8dc-140">Service Properties</span></span></td>
<td><span data-ttu-id="2a8dc-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="2a8dc-142">Blob de instantâneo</span><span class="sxs-lookup"><span data-stu-id="2a8dc-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="2a8dc-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Fazer backup de discos de máquina virtual do Azure com instantâneos incrementais</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="2a8dc-144"><b>Arquivo</b></span><span class="sxs-lookup"><span data-stu-id="2a8dc-144"><b>File</b></span></span></td>
<td><span data-ttu-id="2a8dc-145">Criar compartilhamentos/diretórios/arquivos</span><span class="sxs-lookup"><span data-stu-id="2a8dc-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="2a8dc-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="2a8dc-147">Excluir compartilhamentos/diretórios/arquivos</span><span class="sxs-lookup"><span data-stu-id="2a8dc-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="2a8dc-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Introdução ao Serviço de Arquivos do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-149">Propriedades/metadados de diretório</span><span class="sxs-lookup"><span data-stu-id="2a8dc-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="2a8dc-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-151">Baixar arquivos</span><span class="sxs-lookup"><span data-stu-id="2a8dc-151">Download Files</span></span></td> 
<td><span data-ttu-id="2a8dc-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-153">Metadados/propriedades/métricas de arquivo</span><span class="sxs-lookup"><span data-stu-id="2a8dc-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="2a8dc-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-155">Propriedades do serviço de arquivo</span><span class="sxs-lookup"><span data-stu-id="2a8dc-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="2a8dc-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-157">Listar diretórios e arquivos</span><span class="sxs-lookup"><span data-stu-id="2a8dc-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="2a8dc-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="2a8dc-159">Listar compartilhamentos</span><span class="sxs-lookup"><span data-stu-id="2a8dc-159">List Shares</span></span></td> 
<td><span data-ttu-id="2a8dc-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="2a8dc-161">Compartilhar metadados/propriedades/estatísticas</span><span class="sxs-lookup"><span data-stu-id="2a8dc-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="2a8dc-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="2a8dc-163"><b>Fila</b></span><span class="sxs-lookup"><span data-stu-id="2a8dc-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="2a8dc-164">Adicionar mensagem</span><span class="sxs-lookup"><span data-stu-id="2a8dc-164">Add Message</span></span></td> 
<td><span data-ttu-id="2a8dc-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-166">Criptografia do cliente</span><span class="sxs-lookup"><span data-stu-id="2a8dc-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="2a8dc-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Criptografia de fila do lado do cliente do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-168">Criar filas</span><span class="sxs-lookup"><span data-stu-id="2a8dc-168">Create Queues</span></span></td> 
<td><span data-ttu-id="2a8dc-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-170">Excluir mensagem/fila</span><span class="sxs-lookup"><span data-stu-id="2a8dc-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="2a8dc-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-172">Espiar mensagem</span><span class="sxs-lookup"><span data-stu-id="2a8dc-172">Peek Message</span></span></td> 
<td><span data-ttu-id="2a8dc-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-174">ACL/metadados/estatísticas de fila</span><span class="sxs-lookup"><span data-stu-id="2a8dc-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="2a8dc-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Introdução ao Serviço Fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-176">Propriedades do serviço de fila</span><span class="sxs-lookup"><span data-stu-id="2a8dc-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="2a8dc-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Introdução ao Serviço Fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-178">Atualização de mensagem</span><span class="sxs-lookup"><span data-stu-id="2a8dc-178">Update Message</span></span></td> 
<td><span data-ttu-id="2a8dc-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="2a8dc-180"><b>Tabela</b></span><span class="sxs-lookup"><span data-stu-id="2a8dc-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="2a8dc-181">Criar tabela</span><span class="sxs-lookup"><span data-stu-id="2a8dc-181">Create Table</span></span></td> 
<td><span data-ttu-id="2a8dc-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gerenciando a simultaneidade usando o Armazenamento do Azure — aplicativo de amostra</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-183">Excluir entidade/tabela</span><span class="sxs-lookup"><span data-stu-id="2a8dc-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="2a8dc-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabela do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-185">Inserir/mesclar/substituir entidade</span><span class="sxs-lookup"><span data-stu-id="2a8dc-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="2a8dc-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gerenciando a simultaneidade usando o Armazenamento do Azure — aplicativo de amostra</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-187">Query Entities</span><span class="sxs-lookup"><span data-stu-id="2a8dc-187">Query Entities</span></span></td> 
<td><span data-ttu-id="2a8dc-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabela do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-189">Consultar tabelas</span><span class="sxs-lookup"><span data-stu-id="2a8dc-189">Query Tables</span></span></td> 
<td><span data-ttu-id="2a8dc-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabela do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-191">Propriedades/ACL de tabela</span><span class="sxs-lookup"><span data-stu-id="2a8dc-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="2a8dc-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Introdução ao Armazenamento de Tabela do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2a8dc-193">Update Entity</span><span class="sxs-lookup"><span data-stu-id="2a8dc-193">Update Entity</span></span></td> 
<td><span data-ttu-id="2a8dc-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gerenciando a simultaneidade usando o Armazenamento do Azure — aplicativo de amostra</a></span><span class="sxs-lookup"><span data-stu-id="2a8dc-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="2a8dc-195">Biblioteca de Exemplos de Código do Azure</span><span class="sxs-lookup"><span data-stu-id="2a8dc-195">Azure Code Samples library</span></span>

<span data-ttu-id="2a8dc-196">Para visualizar a biblioteca completa de exemplos, vá para a biblioteca [Exemplos de código do Azure](https://azure.microsoft.com/resources/samples/?service=storage), que contém exemplos para o Armazenamento do Azure que podem ser baixados e executados localmente.</span><span class="sxs-lookup"><span data-stu-id="2a8dc-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="2a8dc-197">A Biblioteca de Exemplo de Código fornece exemplo de código em formato .zip.</span><span class="sxs-lookup"><span data-stu-id="2a8dc-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="2a8dc-198">Como alternativa, você pode navegar e clonar o repositório GitHub para cada exemplo.</span><span class="sxs-lookup"><span data-stu-id="2a8dc-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="2a8dc-199">Guias de introdução</span><span class="sxs-lookup"><span data-stu-id="2a8dc-199">Getting started guides</span></span>

<span data-ttu-id="2a8dc-200">Confira os guias a seguir se você estiver procurando por instruções sobre como instalar e começar a usar as Bibliotecas de cliente de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a8dc-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="2a8dc-201">Introdução ao Serviço Blob do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="2a8dc-201">Getting Started with Azure Blob Service in .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="2a8dc-202">Introdução ao Serviço Fila do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="2a8dc-202">Getting Started with Azure Queue Service in .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="2a8dc-203">Introdução ao Serviço Tabela do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="2a8dc-203">Getting Started with Azure Table Service in .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="2a8dc-204">Introdução ao Serviço de Arquivos do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="2a8dc-204">Getting Started with Azure File Service in .NET</span></span>](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="2a8dc-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2a8dc-205">Next steps</span></span>

<span data-ttu-id="2a8dc-206">Para saber mais sobre exemplos para outras linguagens:</span><span class="sxs-lookup"><span data-stu-id="2a8dc-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="2a8dc-207">Java: [Exemplos de Armazenamento do Azure usando Java](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="2a8dc-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="2a8dc-208">Todas as outras linguagens: [Exemplos de Armazenamento do Azure](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="2a8dc-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
