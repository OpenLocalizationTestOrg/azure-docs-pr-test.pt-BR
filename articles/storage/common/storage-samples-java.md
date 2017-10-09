---
title: exemplos de armazenamento aaaAzure usando Java | Microsoft Docs
description: "Exiba, baixe e execute exemplos de código e aplicativos para o Armazenamento do Azure. Descobrir Introdução exemplos para blobs, filas, tabelas e arquivos, usando bibliotecas de cliente de armazenamento Olá Java."
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
ms.openlocfilehash: 6aec326cbfedc1166fc61037ac39d33c15d28d2c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-java"></a><span data-ttu-id="95f9a-104">Exemplos de armazenamento do Azure usando Java</span><span class="sxs-lookup"><span data-stu-id="95f9a-104">Azure Storage samples using Java</span></span>

## <a name="java-sample-index"></a><span data-ttu-id="95f9a-105">Índice de exemplos de Java</span><span class="sxs-lookup"><span data-stu-id="95f9a-105">Java sample index</span></span>

<span data-ttu-id="95f9a-106">Hello tabela a seguir fornece uma visão geral dos nossos exemplos de cenários de repositório e hello abordadas em cada exemplo.</span><span class="sxs-lookup"><span data-stu-id="95f9a-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="95f9a-107">Clique em Olá links tooview Olá correspondente código de exemplo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="95f9a-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="95f9a-108">Ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="95f9a-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="95f9a-109">Cenário</span><span class="sxs-lookup"><span data-stu-id="95f9a-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="95f9a-110">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="95f9a-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="95f9a-111"><b>Blob</b></span><span class="sxs-lookup"><span data-stu-id="95f9a-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="95f9a-112">Acrescentar blob</span><span class="sxs-lookup"><span data-stu-id="95f9a-112">Append Blob</span></span></td> 
<td><span data-ttu-id="95f9a-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-113"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-114">Blob de blocos</span><span class="sxs-lookup"><span data-stu-id="95f9a-114">Block Blob</span></span></td>
<td><span data-ttu-id="95f9a-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-115"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-116">Criptografia do cliente</span><span class="sxs-lookup"><span data-stu-id="95f9a-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="95f9a-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Introdução à criptografia no lado do cliente do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-117"><a href="https://github.com/Azure-Samples/storage-java-client-side-encryption">Getting Started with Azure Client Side Encryption in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-118">Copiar blob</span><span class="sxs-lookup"><span data-stu-id="95f9a-118">Copy Blob</span></span></td>
<td><span data-ttu-id="95f9a-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-119"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-120">Create Container</span><span class="sxs-lookup"><span data-stu-id="95f9a-120">Create Container</span></span></td>
<td><span data-ttu-id="95f9a-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-121"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-122">Delete Blob</span><span class="sxs-lookup"><span data-stu-id="95f9a-122">Delete Blob</span></span></td>
<td><span data-ttu-id="95f9a-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-123"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-124">Delete Container</span><span class="sxs-lookup"><span data-stu-id="95f9a-124">Delete Container</span></span></td>
<td><span data-ttu-id="95f9a-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-125"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-126">Metadados/propriedades/estatísticas de blob</span><span class="sxs-lookup"><span data-stu-id="95f9a-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="95f9a-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-127"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-128">ACL/metadados/propriedades de contêiner</span><span class="sxs-lookup"><span data-stu-id="95f9a-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="95f9a-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-129"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-130">Get Page Ranges</span><span class="sxs-lookup"><span data-stu-id="95f9a-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="95f9a-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Exemplo para testes de blob de páginas</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-131"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/CloudPageBlobTests.java">Page Blob Tests Sample</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-132">Blob/contêiner de concessão</span><span class="sxs-lookup"><span data-stu-id="95f9a-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="95f9a-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-133"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-134">Blob/contêiner de lista</span><span class="sxs-lookup"><span data-stu-id="95f9a-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="95f9a-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-135"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-136">Blob de páginas</span><span class="sxs-lookup"><span data-stu-id="95f9a-136">Page Blob</span></span></td>
<td><span data-ttu-id="95f9a-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-137"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="95f9a-138">SAS</span><span class="sxs-lookup"><span data-stu-id="95f9a-138">SAS</span></span></td>
<td><span data-ttu-id="95f9a-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">Exemplo para testes de SAS</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-139"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-test/src/com/microsoft/azure/storage/blob/SasTests.java">SAS Tests Sample</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="95f9a-140">Propriedades do serviço</span><span class="sxs-lookup"><span data-stu-id="95f9a-140">Service Properties</span></span></td>
<td><span data-ttu-id="95f9a-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-141"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobAdvanced.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="95f9a-142">Blob de instantâneo</span><span class="sxs-lookup"><span data-stu-id="95f9a-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="95f9a-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Introdução ao Serviço Blob do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-143"><a href="https://github.com/Azure-Samples/storage-blob-java-getting-started/blob/master/src/BlobBasics.java">Getting Started with Azure Blob Service in Java</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="95f9a-144"><b>Arquivo</b></span><span class="sxs-lookup"><span data-stu-id="95f9a-144"><b>File</b></span></span></td>
<td><span data-ttu-id="95f9a-145">Criar compartilhamentos/diretórios/arquivos</span><span class="sxs-lookup"><span data-stu-id="95f9a-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="95f9a-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-146"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="95f9a-147">Excluir compartilhamentos/diretórios/arquivos</span><span class="sxs-lookup"><span data-stu-id="95f9a-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="95f9a-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-148"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-149">Propriedades/metadados de diretório</span><span class="sxs-lookup"><span data-stu-id="95f9a-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="95f9a-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-150"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-151">Baixar arquivos</span><span class="sxs-lookup"><span data-stu-id="95f9a-151">Download Files</span></span></td> 
<td><span data-ttu-id="95f9a-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-152"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-153">Metadados/propriedades/métricas de arquivo</span><span class="sxs-lookup"><span data-stu-id="95f9a-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="95f9a-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-154"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-155">Propriedades do serviço de arquivo</span><span class="sxs-lookup"><span data-stu-id="95f9a-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="95f9a-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-156"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-157">Listar diretórios e arquivos</span><span class="sxs-lookup"><span data-stu-id="95f9a-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="95f9a-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-158"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="95f9a-159">Listar compartilhamentos</span><span class="sxs-lookup"><span data-stu-id="95f9a-159">List Shares</span></span></td> 
<td><span data-ttu-id="95f9a-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-160"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileBasics.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="95f9a-161">Compartilhar metadados/propriedades/estatísticas</span><span class="sxs-lookup"><span data-stu-id="95f9a-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="95f9a-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Introdução ao Serviço Arquivo do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-162"><a href="https://github.com/Azure-Samples/storage-file-java-getting-started/blob/master/src/FileAdvanced.java">Getting Started with Azure File Service in Java</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="95f9a-163"><b>Fila</b></span><span class="sxs-lookup"><span data-stu-id="95f9a-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="95f9a-164">Adicionar mensagem</span><span class="sxs-lookup"><span data-stu-id="95f9a-164">Add Message</span></span></td> 
<td><span data-ttu-id="95f9a-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Amostras da Biblioteca do Cliente Java de Armazenamento</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-165"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/queue/gettingstarted/QueueBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-166">Criptografia do cliente</span><span class="sxs-lookup"><span data-stu-id="95f9a-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="95f9a-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Amostras da Biblioteca do Cliente Java de Armazenamento</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-167"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/encryption/queue/gettingstarted/QueueGettingStarted.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-168">Criar filas</span><span class="sxs-lookup"><span data-stu-id="95f9a-168">Create Queues</span></span></td> 
<td><span data-ttu-id="95f9a-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introdução ao Serviço Fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-169"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-170">Excluir mensagem/fila</span><span class="sxs-lookup"><span data-stu-id="95f9a-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="95f9a-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introdução ao Serviço Fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-171"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-172">Espiar mensagem</span><span class="sxs-lookup"><span data-stu-id="95f9a-172">Peek Message</span></span></td> 
<td><span data-ttu-id="95f9a-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introdução ao Serviço Fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-173"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-174">ACL/metadados/estatísticas de fila</span><span class="sxs-lookup"><span data-stu-id="95f9a-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="95f9a-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Introdução ao Serviço Fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-175"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-176">Propriedades do serviço de fila</span><span class="sxs-lookup"><span data-stu-id="95f9a-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="95f9a-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Introdução ao Serviço Fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-177"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueAdvanced.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-178">Atualização de mensagem</span><span class="sxs-lookup"><span data-stu-id="95f9a-178">Update Message</span></span></td> 
<td><span data-ttu-id="95f9a-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Introdução ao Serviço Fila do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-179"><a href="https://github.com/Azure-Samples/storage-queue-java-getting-started/blob/master/src/QueueBasics.java">Getting Started with Azure Queue Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="95f9a-180"><b>Tabela</b></span><span class="sxs-lookup"><span data-stu-id="95f9a-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="95f9a-181">Criar tabela</span><span class="sxs-lookup"><span data-stu-id="95f9a-181">Create Table</span></span></td> 
<td><span data-ttu-id="95f9a-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Introdução ao Serviço Tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-182"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-183">Excluir entidade/tabela</span><span class="sxs-lookup"><span data-stu-id="95f9a-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="95f9a-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Introdução ao Serviço Tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-184"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-185">Inserir/mesclar/substituir entidade</span><span class="sxs-lookup"><span data-stu-id="95f9a-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="95f9a-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Amostras da Biblioteca do Cliente Java de Armazenamento</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-186"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-187">Query Entities</span><span class="sxs-lookup"><span data-stu-id="95f9a-187">Query Entities</span></span></td> 
<td><span data-ttu-id="95f9a-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Introdução ao Serviço Tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-188"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-189">Consultar tabelas</span><span class="sxs-lookup"><span data-stu-id="95f9a-189">Query Tables</span></span></td> 
<td><span data-ttu-id="95f9a-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Introdução ao Serviço Tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-190"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableBasics.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-191">Propriedades/ACL de tabela</span><span class="sxs-lookup"><span data-stu-id="95f9a-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="95f9a-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Introdução ao Serviço Tabela do Azure em Java</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-192"><a href="https://github.com/Azure-Samples/storage-table-java-getting-started/blob/master/src/TableAdvanced.java">Getting Started with Azure Table Service in Java</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="95f9a-193">Update Entity</span><span class="sxs-lookup"><span data-stu-id="95f9a-193">Update Entity</span></span></td> 
<td><span data-ttu-id="95f9a-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Amostras da Biblioteca do Cliente Java de Armazenamento</a></span><span class="sxs-lookup"><span data-stu-id="95f9a-194"><a href="https://github.com/Azure/azure-storage-java/blob/master/microsoft-azure-storage-samples/src/com/microsoft/azure/storage/table/gettingtstarted/TableBasics.java">Storage Java Client Library Samples</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="95f9a-195">Biblioteca de Exemplos de Código do Azure</span><span class="sxs-lookup"><span data-stu-id="95f9a-195">Azure Code Samples library</span></span>

<span data-ttu-id="95f9a-196">biblioteca de exemplo completo tooview hello, vá toohello [exemplos de código do Azure](https://azure.microsoft.com/resources/samples/?service=storage) biblioteca, que inclui exemplos de armazenamento do Azure que você pode baixar e executar localmente.</span><span class="sxs-lookup"><span data-stu-id="95f9a-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="95f9a-197">Olá biblioteca de código de exemplo fornece código de exemplo em formato. zip.</span><span class="sxs-lookup"><span data-stu-id="95f9a-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="95f9a-198">Como alternativa, você pode procurar e clonar o repositório do GitHub Olá para cada exemplo.</span><span class="sxs-lookup"><span data-stu-id="95f9a-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-java-samples-include](../../../includes/storage-java-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="95f9a-199">Guias de introdução</span><span class="sxs-lookup"><span data-stu-id="95f9a-199">Getting started guides</span></span>

<span data-ttu-id="95f9a-200">Check-out Olá guias a seguir se você está procurando obter instruções sobre como tooinstall e introdução a saudação bibliotecas de cliente de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="95f9a-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="95f9a-201">Introdução ao Serviço Blob do Azure em Java</span><span class="sxs-lookup"><span data-stu-id="95f9a-201">Getting Started with Azure Blob Service in Java</span></span>](../blobs/storage-java-how-to-use-blob-storage.md)
* [<span data-ttu-id="95f9a-202">Introdução ao Serviço Fila do Azure em Java</span><span class="sxs-lookup"><span data-stu-id="95f9a-202">Getting Started with Azure Queue Service in Java</span></span>](../storage-java-how-to-use-queue-storage.md)
* [<span data-ttu-id="95f9a-203">Introdução ao Serviço Tabela do Azure em Java</span><span class="sxs-lookup"><span data-stu-id="95f9a-203">Getting Started with Azure Table Service in Java</span></span>](../../cosmos-db/table-storage-how-to-use-java.md)
* [<span data-ttu-id="95f9a-204">Introdução ao Serviço Arquivo do Azure em Java</span><span class="sxs-lookup"><span data-stu-id="95f9a-204">Getting Started with Azure File Service in Java</span></span>](../storage-java-how-to-use-file-storage.md)

## <a name="next-steps"></a><span data-ttu-id="95f9a-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="95f9a-205">Next steps</span></span>

<span data-ttu-id="95f9a-206">Para saber mais sobre exemplos para outras linguagens:</span><span class="sxs-lookup"><span data-stu-id="95f9a-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="95f9a-207">.NET: [Exemplos de armazenamento do Azure usando .NET](../storage-samples-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="95f9a-207">.NET: [Azure Storage samples using .NET](../storage-samples-dotnet.md)</span></span>
* <span data-ttu-id="95f9a-208">Todas as outras linguagens: [Exemplos de Armazenamento do Azure](../storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="95f9a-208">All other languages: [Azure Storage samples](../storage-samples.md)</span></span>
