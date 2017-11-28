---
title: exemplos de armazenamento aaaAzure usando .NET | Microsoft Docs
description: "Exiba, baixe e execute exemplos de código e aplicativos para o Armazenamento do Azure. Descobrir Introdução exemplos para blobs, filas, tabelas e arquivos, usando bibliotecas de cliente de armazenamento Olá .NET."
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
ms.openlocfilehash: 6b02b596f77845fc5fa474fa235c2b5df6e94ad7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="1c934-104">Exemplos de Armazenamento do Azure usando .NET</span><span class="sxs-lookup"><span data-stu-id="1c934-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="1c934-105">Exemplo de índice do .NET</span><span class="sxs-lookup"><span data-stu-id="1c934-105">.NET sample index</span></span>

<span data-ttu-id="1c934-106">Hello tabela a seguir fornece uma visão geral dos nossos exemplos de cenários de repositório e hello abordadas em cada exemplo.</span><span class="sxs-lookup"><span data-stu-id="1c934-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="1c934-107">Clique em Olá links tooview Olá correspondente código de exemplo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="1c934-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="1c934-108">Ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="1c934-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="1c934-109">Cenário</span><span class="sxs-lookup"><span data-stu-id="1c934-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="1c934-110">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="1c934-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="1c934-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="1c934-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="1c934-112">Acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="1c934-112">Append Blob</span></span></td> 
<td><span data-ttu-id="1c934-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Exemplo do método CloudBlobContainer.GetAppendBlobReference</a></span><span class="sxs-lookup"><span data-stu-id="1c934-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-114">Blob de blocos</span><span class="sxs-lookup"><span data-stu-id="1c934-114">Block Blob</span></span></td>
<td><span data-ttu-id="1c934-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicativo Web de Galeria de Fotos do Armazenamento de Blobs do Azure</a></span><span class="sxs-lookup"><span data-stu-id="1c934-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1c934-116">Criptografia do cliente</span><span class="sxs-lookup"><span data-stu-id="1c934-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="1c934-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Exemplos de criptografia de blob</a></span><span class="sxs-lookup"><span data-stu-id="1c934-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1c934-118">Copiar blob</span><span class="sxs-lookup"><span data-stu-id="1c934-118">Copy Blob</span></span></td>
<td><span data-ttu-id="1c934-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="1c934-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1c934-120">Create Container</span><span class="sxs-lookup"><span data-stu-id="1c934-120">Create Container</span></span></td>
<td><span data-ttu-id="1c934-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicativo Web de Galeria de Fotos do Armazenamento de Blobs do Azure</a></span><span class="sxs-lookup"><span data-stu-id="1c934-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1c934-122">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="1c934-122">Delete Blob</span></span></td>
<td><span data-ttu-id="1c934-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicativo Web de Galeria de Fotos do Armazenamento de Blobs do Azure</a></span><span class="sxs-lookup"><span data-stu-id="1c934-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1c934-124">Delete Container</span><span class="sxs-lookup"><span data-stu-id="1c934-124">Delete Container</span></span></td>
<td><span data-ttu-id="1c934-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="1c934-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1c934-126">Metadados/propriedades/estatísticas de blob</span><span class="sxs-lookup"><span data-stu-id="1c934-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="1c934-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="1c934-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1c934-128">ACL/metadados/propriedades de contêiner</span><span class="sxs-lookup"><span data-stu-id="1c934-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="1c934-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicativo Web de Galeria de Fotos do Armazenamento de Blobs do Azure</a></span><span class="sxs-lookup"><span data-stu-id="1c934-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1c934-130">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="1c934-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="1c934-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="1c934-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1c934-132">Blob/contêiner de concessão</span><span class="sxs-lookup"><span data-stu-id="1c934-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="1c934-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="1c934-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1c934-134">Blob/contêiner de lista</span><span class="sxs-lookup"><span data-stu-id="1c934-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="1c934-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="1c934-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="1c934-136">Blob de páginas</span><span class="sxs-lookup"><span data-stu-id="1c934-136">Page Blob</span></span></td>
<td><span data-ttu-id="1c934-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="1c934-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="1c934-138">SAS</span><span class="sxs-lookup"><span data-stu-id="1c934-138">SAS</span></span></td>
<td><span data-ttu-id="1c934-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="1c934-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="1c934-140">Propriedades do serviço</span><span class="sxs-lookup"><span data-stu-id="1c934-140">Service Properties</span></span></td>
<td><span data-ttu-id="1c934-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></span><span class="sxs-lookup"><span data-stu-id="1c934-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="1c934-142">Blob de instantâneo</span><span class="sxs-lookup"><span data-stu-id="1c934-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="1c934-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Fazer backup de discos de máquina virtual do Azure com instantâneos incrementais</a></span><span class="sxs-lookup"><span data-stu-id="1c934-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="1c934-144"><b>Arquivo</b></span><span class="sxs-lookup"><span data-stu-id="1c934-144"><b>File</b></span></span></td>
<td><span data-ttu-id="1c934-145">Criar compartilhamentos/diretórios/arquivos</span><span class="sxs-lookup"><span data-stu-id="1c934-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="1c934-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="1c934-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="1c934-147">Excluir compartilhamentos/diretórios/arquivos</span><span class="sxs-lookup"><span data-stu-id="1c934-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="1c934-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Introdução ao Serviço de Arquivos do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="1c934-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-149">Propriedades/metadados de diretório</span><span class="sxs-lookup"><span data-stu-id="1c934-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="1c934-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="1c934-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-151">Baixar arquivos</span><span class="sxs-lookup"><span data-stu-id="1c934-151">Download Files</span></span></td> 
<td><span data-ttu-id="1c934-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="1c934-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-153">Metadados/propriedades/métricas de arquivo</span><span class="sxs-lookup"><span data-stu-id="1c934-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="1c934-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="1c934-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-155">Propriedades do serviço de arquivo</span><span class="sxs-lookup"><span data-stu-id="1c934-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="1c934-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="1c934-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-157">Listar diretórios e arquivos</span><span class="sxs-lookup"><span data-stu-id="1c934-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="1c934-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="1c934-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="1c934-159">Listar compartilhamentos</span><span class="sxs-lookup"><span data-stu-id="1c934-159">List Shares</span></span></td> 
<td><span data-ttu-id="1c934-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="1c934-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="1c934-161">Compartilhar metadados/propriedades/estatísticas</span><span class="sxs-lookup"><span data-stu-id="1c934-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="1c934-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="1c934-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="1c934-163"><b>Fila</b></span><span class="sxs-lookup"><span data-stu-id="1c934-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="1c934-164">Adicionar mensagem</span><span class="sxs-lookup"><span data-stu-id="1c934-164">Add Message</span></span></td> 
<td><span data-ttu-id="1c934-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="1c934-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-166">Criptografia do cliente</span><span class="sxs-lookup"><span data-stu-id="1c934-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="1c934-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Criptografia de fila do lado do cliente do .NET para Armazenamento do Azure</a></span><span class="sxs-lookup"><span data-stu-id="1c934-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-168">Criar filas</span><span class="sxs-lookup"><span data-stu-id="1c934-168">Create Queues</span></span></td> 
<td><span data-ttu-id="1c934-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="1c934-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-170">Excluir mensagem/fila</span><span class="sxs-lookup"><span data-stu-id="1c934-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="1c934-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="1c934-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-172">Espiar mensagem</span><span class="sxs-lookup"><span data-stu-id="1c934-172">Peek Message</span></span></td> 
<td><span data-ttu-id="1c934-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="1c934-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-174">ACL/metadados/estatísticas de fila</span><span class="sxs-lookup"><span data-stu-id="1c934-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="1c934-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Introdução ao Serviço Fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="1c934-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-176">Propriedades do serviço de fila</span><span class="sxs-lookup"><span data-stu-id="1c934-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="1c934-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Introdução ao Serviço Fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="1c934-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-178">Atualização de mensagem</span><span class="sxs-lookup"><span data-stu-id="1c934-178">Update Message</span></span></td> 
<td><span data-ttu-id="1c934-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="1c934-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="1c934-180"><b>Tabela</b></span><span class="sxs-lookup"><span data-stu-id="1c934-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="1c934-181">Criar tabela</span><span class="sxs-lookup"><span data-stu-id="1c934-181">Create Table</span></span></td> 
<td><span data-ttu-id="1c934-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gerenciando a simultaneidade usando o Armazenamento do Azure — aplicativo de amostra</a></span><span class="sxs-lookup"><span data-stu-id="1c934-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-183">Excluir entidade/tabela</span><span class="sxs-lookup"><span data-stu-id="1c934-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="1c934-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabela do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="1c934-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-185">Inserir/mesclar/substituir entidade</span><span class="sxs-lookup"><span data-stu-id="1c934-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="1c934-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gerenciando a simultaneidade usando o Armazenamento do Azure — aplicativo de amostra</a></span><span class="sxs-lookup"><span data-stu-id="1c934-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-187">Query Entities</span><span class="sxs-lookup"><span data-stu-id="1c934-187">Query Entities</span></span></td> 
<td><span data-ttu-id="1c934-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabela do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="1c934-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-189">Consultar tabelas</span><span class="sxs-lookup"><span data-stu-id="1c934-189">Query Tables</span></span></td> 
<td><span data-ttu-id="1c934-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabela do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="1c934-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-191">Propriedades/ACL de tabela</span><span class="sxs-lookup"><span data-stu-id="1c934-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="1c934-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Introdução ao Armazenamento de Tabela do Azure no .NET</a></span><span class="sxs-lookup"><span data-stu-id="1c934-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="1c934-193">Update Entity</span><span class="sxs-lookup"><span data-stu-id="1c934-193">Update Entity</span></span></td> 
<td><span data-ttu-id="1c934-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gerenciando a simultaneidade usando o Armazenamento do Azure — aplicativo de amostra</a></span><span class="sxs-lookup"><span data-stu-id="1c934-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="1c934-195">Biblioteca de Exemplos de Código do Azure</span><span class="sxs-lookup"><span data-stu-id="1c934-195">Azure Code Samples library</span></span>

<span data-ttu-id="1c934-196">biblioteca de exemplo completo tooview hello, vá toohello [exemplos de código do Azure](https://azure.microsoft.com/resources/samples/?service=storage) biblioteca, que inclui exemplos de armazenamento do Azure que você pode baixar e executar localmente.</span><span class="sxs-lookup"><span data-stu-id="1c934-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="1c934-197">Olá biblioteca de código de exemplo fornece código de exemplo em formato. zip.</span><span class="sxs-lookup"><span data-stu-id="1c934-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="1c934-198">Como alternativa, você pode procurar e clonar o repositório do GitHub Olá para cada exemplo.</span><span class="sxs-lookup"><span data-stu-id="1c934-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="1c934-199">Guias de introdução</span><span class="sxs-lookup"><span data-stu-id="1c934-199">Getting started guides</span></span>

<span data-ttu-id="1c934-200">Check-out Olá guias a seguir se você está procurando obter instruções sobre como tooinstall e introdução a saudação bibliotecas de cliente de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="1c934-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="1c934-201">Introdução ao Serviço Blob do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="1c934-201">Getting Started with Azure Blob Service in .NET</span></span>](../blobs/storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="1c934-202">Introdução ao Serviço Fila do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="1c934-202">Getting Started with Azure Queue Service in .NET</span></span>](../storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="1c934-203">Introdução ao Serviço Tabela do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="1c934-203">Getting Started with Azure Table Service in .NET</span></span>](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [<span data-ttu-id="1c934-204">Introdução ao Serviço de Arquivos do Azure no .NET</span><span class="sxs-lookup"><span data-stu-id="1c934-204">Getting Started with Azure File Service in .NET</span></span>](../storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="1c934-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1c934-205">Next steps</span></span>

<span data-ttu-id="1c934-206">Para saber mais sobre exemplos para outras linguagens:</span><span class="sxs-lookup"><span data-stu-id="1c934-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="1c934-207">Java: [Exemplos de Armazenamento do Azure usando Java](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="1c934-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="1c934-208">Todas as outras linguagens: [Exemplos de Armazenamento do Azure](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="1c934-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
