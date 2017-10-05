---
title: Exemplos do Armazenamento do Azure | Microsoft Docs
description: "Exiba, baixe e execute exemplos de código e aplicativos para o Armazenamento do Azure. Descubra exemplos de introdução a blobs, filas, tabelas e arquivos usando as bibliotecas do cliente de armazenamento do Java."
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: fd27e1ac9a773e7b0f5245aa74acdb0521cd098c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="2d266-104">Exemplos de armazenamento do Azure usando Java</span><span class="sxs-lookup"><span data-stu-id="2d266-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="2d266-105">Índice de exemplos de Java</span><span class="sxs-lookup"><span data-stu-id="2d266-105">Java sample index</span></span>

<span data-ttu-id="2d266-106">A tabela a seguir fornece uma visão geral do nosso repositório de exemplos e os cenários abordados em cada exemplo.</span><span class="sxs-lookup"><span data-stu-id="2d266-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="2d266-107">Clique nos links para exibir o código de exemplo correspondente no GitHub.</span><span class="sxs-lookup"><span data-stu-id="2d266-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="2d266-108">Ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="2d266-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="2d266-109">Cenário</span><span class="sxs-lookup"><span data-stu-id="2d266-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="2d266-110">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="2d266-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="2d266-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="2d266-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="2d266-112">Acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="2d266-112">Append Blob</span></span></td> 
<td><span data-ttu-id="2d266-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-114">Blob de blocos</span><span class="sxs-lookup"><span data-stu-id="2d266-114">Block Blob</span></span></td>
<td><span data-ttu-id="2d266-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2d266-116">Criptografia do cliente</span><span class="sxs-lookup"><span data-stu-id="2d266-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="2d266-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Introdução à criptografia no lado do cliente do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2d266-118">Copiar blob</span><span class="sxs-lookup"><span data-stu-id="2d266-118">Copy Blob</span></span></td>
<td><span data-ttu-id="2d266-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2d266-120">Create Container</span><span class="sxs-lookup"><span data-stu-id="2d266-120">Create Container</span></span></td>
<td><span data-ttu-id="2d266-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2d266-122">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="2d266-122">Delete Blob</span></span></td>
<td><span data-ttu-id="2d266-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2d266-124">Delete Container</span><span class="sxs-lookup"><span data-stu-id="2d266-124">Delete Container</span></span></td>
<td><span data-ttu-id="2d266-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2d266-126">Metadados/propriedades/estatísticas de blob</span><span class="sxs-lookup"><span data-stu-id="2d266-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="2d266-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2d266-128">ACL/metadados/propriedades de contêiner</span><span class="sxs-lookup"><span data-stu-id="2d266-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="2d266-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2d266-130">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="2d266-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="2d266-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Exemplo para testes de blob de páginas</a></span><span class="sxs-lookup"><span data-stu-id="2d266-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2d266-132">Blob/contêiner de concessão</span><span class="sxs-lookup"><span data-stu-id="2d266-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="2d266-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2d266-134">Blob/contêiner de lista</span><span class="sxs-lookup"><span data-stu-id="2d266-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="2d266-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="2d266-136">Blob de páginas</span><span class="sxs-lookup"><span data-stu-id="2d266-136">Page Blob</span></span></td>
<td><span data-ttu-id="2d266-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="2d266-138">SAS</span><span class="sxs-lookup"><span data-stu-id="2d266-138">SAS</span></span></td>
<td><span data-ttu-id="2d266-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Exemplo para testes de SAS</a></span><span class="sxs-lookup"><span data-stu-id="2d266-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="2d266-140">Propriedades do serviço</span><span class="sxs-lookup"><span data-stu-id="2d266-140">Service Properties</span></span></td>
<td><span data-ttu-id="2d266-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="2d266-142">Blob de instantâneo</span><span class="sxs-lookup"><span data-stu-id="2d266-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="2d266-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="2d266-144"><b>Arquivo</b></span><span class="sxs-lookup"><span data-stu-id="2d266-144"><b>File</b></span></span></td>
<td><span data-ttu-id="2d266-145">Criar compartilhamentos/diretórios/arquivos</span><span class="sxs-lookup"><span data-stu-id="2d266-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="2d266-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="2d266-147">Excluir compartilhamentos/diretórios/arquivos</span><span class="sxs-lookup"><span data-stu-id="2d266-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="2d266-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-149">Propriedades/metadados de diretório</span><span class="sxs-lookup"><span data-stu-id="2d266-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="2d266-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-151">Baixar arquivos</span><span class="sxs-lookup"><span data-stu-id="2d266-151">Download Files</span></span></td> 
<td><span data-ttu-id="2d266-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-153">Metadados/propriedades/métricas de arquivo</span><span class="sxs-lookup"><span data-stu-id="2d266-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="2d266-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-155">Propriedades do serviço de arquivo</span><span class="sxs-lookup"><span data-stu-id="2d266-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="2d266-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-157">Listar diretórios e arquivos</span><span class="sxs-lookup"><span data-stu-id="2d266-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="2d266-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="2d266-159">Listar compartilhamentos</span><span class="sxs-lookup"><span data-stu-id="2d266-159">List Shares</span></span></td> 
<td><span data-ttu-id="2d266-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="2d266-161">Compartilhar metadados/propriedades/estatísticas</span><span class="sxs-lookup"><span data-stu-id="2d266-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="2d266-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="2d266-163"><b>Fila</b></span><span class="sxs-lookup"><span data-stu-id="2d266-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="2d266-164">Adicionar mensagem</span><span class="sxs-lookup"><span data-stu-id="2d266-164">Add Message</span></span></td> 
<td><span data-ttu-id="2d266-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Amostras da Biblioteca do Cliente Java de Armazenamento</a></span><span class="sxs-lookup"><span data-stu-id="2d266-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-166">Criptografia do cliente</span><span class="sxs-lookup"><span data-stu-id="2d266-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="2d266-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Amostras da Biblioteca do Cliente Java de Armazenamento</a></span><span class="sxs-lookup"><span data-stu-id="2d266-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-168">Criar filas</span><span class="sxs-lookup"><span data-stu-id="2d266-168">Create Queues</span></span></td> 
<td><span data-ttu-id="2d266-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introdução ao Serviço Fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-170">Excluir mensagem/fila</span><span class="sxs-lookup"><span data-stu-id="2d266-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="2d266-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introdução ao Serviço Fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-172">Espiar mensagem</span><span class="sxs-lookup"><span data-stu-id="2d266-172">Peek Message</span></span></td> 
<td><span data-ttu-id="2d266-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introdução ao Serviço Fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-174">ACL/metadados/estatísticas de fila</span><span class="sxs-lookup"><span data-stu-id="2d266-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="2d266-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Introdução ao Serviço Fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-176">Propriedades do serviço de fila</span><span class="sxs-lookup"><span data-stu-id="2d266-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="2d266-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Introdução ao Serviço Fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-178">Atualização de mensagem</span><span class="sxs-lookup"><span data-stu-id="2d266-178">Update Message</span></span></td> 
<td><span data-ttu-id="2d266-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introdução ao Serviço Fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="2d266-180"><b>Tabela</b></span><span class="sxs-lookup"><span data-stu-id="2d266-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="2d266-181">Criar tabela</span><span class="sxs-lookup"><span data-stu-id="2d266-181">Create Table</span></span></td> 
<td><span data-ttu-id="2d266-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Introdução ao Serviço Tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-183">Excluir entidade/tabela</span><span class="sxs-lookup"><span data-stu-id="2d266-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="2d266-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Introdução ao Serviço Tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-185">Inserir/mesclar/substituir entidade</span><span class="sxs-lookup"><span data-stu-id="2d266-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="2d266-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Amostras da Biblioteca do Cliente Java de Armazenamento</a></span><span class="sxs-lookup"><span data-stu-id="2d266-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-187">Query Entities</span><span class="sxs-lookup"><span data-stu-id="2d266-187">Query Entities</span></span></td> 
<td><span data-ttu-id="2d266-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Introdução ao Serviço Tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-189">Consultar tabelas</span><span class="sxs-lookup"><span data-stu-id="2d266-189">Query Tables</span></span></td> 
<td><span data-ttu-id="2d266-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Introdução ao Serviço Tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-191">Propriedades/ACL de tabela</span><span class="sxs-lookup"><span data-stu-id="2d266-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="2d266-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Introdução ao Serviço Tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="2d266-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="2d266-193">Update Entity</span><span class="sxs-lookup"><span data-stu-id="2d266-193">Update Entity</span></span></td> 
<td><span data-ttu-id="2d266-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Amostras da Biblioteca do Cliente Java de Armazenamento</a></span><span class="sxs-lookup"><span data-stu-id="2d266-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="2d266-195">Biblioteca de Exemplos de Código do Azure</span><span class="sxs-lookup"><span data-stu-id="2d266-195">Azure Code Samples library</span></span>

<span data-ttu-id="2d266-196">Para visualizar a biblioteca completa de exemplos, vá para a biblioteca [Exemplos de código do Azure](https://azure.microsoft.com/resources/samples/?service=storage), que contém exemplos para o Armazenamento do Azure que podem ser baixados e executados localmente.</span><span class="sxs-lookup"><span data-stu-id="2d266-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="2d266-197">A Biblioteca de Exemplo de Código fornece exemplo de código em formato .zip.</span><span class="sxs-lookup"><span data-stu-id="2d266-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="2d266-198">Como alternativa, você pode navegar e clonar o repositório GitHub para cada exemplo.</span><span class="sxs-lookup"><span data-stu-id="2d266-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="2d266-199">Guias de introdução</span><span class="sxs-lookup"><span data-stu-id="2d266-199">Getting started guides</span></span>

<span data-ttu-id="2d266-200">Confira os guias a seguir se você estiver procurando por instruções sobre como instalar e começar a usar as Bibliotecas de cliente de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="2d266-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="2d266-201">Introdução ao Serviço Blob do Azure em Java</span><span class="sxs-lookup"><span data-stu-id="2d266-201">Getting Started with Azure Blob Service in Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="2d266-202">Introdução ao Serviço Fila do Azure em Java</span><span class="sxs-lookup"><span data-stu-id="2d266-202">Getting Started with Azure Queue Service in Java</span></span>](../storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="2d266-203">Introdução ao Serviço Tabela do Azure em Java</span><span class="sxs-lookup"><span data-stu-id="2d266-203">Getting Started with Azure Table Service in Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="2d266-204">Introdução ao Serviço Arquivo do Azure em Java</span><span class="sxs-lookup"><span data-stu-id="2d266-204">Getting Started with Azure File Service in Java</span></span>](../storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="2d266-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2d266-205">Next steps</span></span>

<span data-ttu-id="2d266-206">Para saber mais sobre exemplos para outras linguagens:</span><span class="sxs-lookup"><span data-stu-id="2d266-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="2d266-207">.NET: [Exemplos de armazenamento do Azure usando .NET](../storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="2d266-207">.NET: [Azure Storage samples using .NET](../storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="2d266-208">Todas as outras linguagens: [Exemplos de Armazenamento do Azure](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="2d266-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
