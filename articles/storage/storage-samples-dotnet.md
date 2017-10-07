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
ms.openlocfilehash: 9a7055645b0f0658b850f024b8b19ab19840330e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-net"></a>Exemplos de Armazenamento do Azure usando .NET

## <a name="net-sample-index"></a>Exemplo de índice do .NET

Hello tabela a seguir fornece uma visão geral dos nossos exemplos de cenários de repositório e hello abordadas em cada exemplo. Clique em Olá links tooview Olá correspondente código de exemplo no GitHub.

<table style="font-size:90%"><thead><tr><th style="font-size:110%">Ponto de extremidade</th><th style="font-size:110%">Cenário</th><th style="font-size:110%">Exemplo de código</th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><b>Blob</b></td>
<td>Acrescentar blob</td> 
<td><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">Exemplo do método CloudBlobContainer.GetAppendBlobReference</a></td> 
</tr> 
<tr> 
<td>Blob de blocos</td>
<td><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicativo Web de Galeria de Fotos do Armazenamento de Blobs do Azure</a></td>
</tr> 
<tr> 
<td>Criptografia do cliente</td>
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Exemplos de criptografia de blob</a></td>
</tr> 
<tr> 
<td>Copiar blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></td>
</tr> 
<tr> 
<td>Create Container</td>
<td><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicativo Web de Galeria de Fotos do Armazenamento de Blobs do Azure</a></td>
</tr> 
<tr> 
<td>Delete Blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicativo Web de Galeria de Fotos do Armazenamento de Blobs do Azure</a></td>
</tr> 
<tr> 
<td>Delete Container</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></td>
</tr> 
<tr> 
<td>Metadados/propriedades/estatísticas de blob</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></td>
</tr> 
<tr> 
<td>ACL/metadados/propriedades de contêiner</td>
<td><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Aplicativo Web de Galeria de Fotos do Armazenamento de Blobs do Azure</a></td>
</tr> 
<tr> 
<td>Get Page Ranges</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></td>
</tr> 
<tr> 
<td>Blob/contêiner de concessão</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></td>
</tr> 
<tr> 
<td>Blob/contêiner de lista</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Introdução aos blobs</a></td>
</tr> 
<tr> 
<td>Blob de páginas</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Introdução aos blobs</a></td>
</tr>
<tr> 
<td>SAS</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></td>
</tr>   
<tr> 
<td>Propriedades do serviço</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Introdução aos blobs</a></td>
</tr>           
<tr> 
<td>Blob de instantâneo</td>
<td><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Fazer backup de discos de máquina virtual do Azure com instantâneos incrementais</a></td>
</tr> 
<tr> 
<td rowspan="9"><b>Arquivo</b></td>
<td>Criar compartilhamentos/diretórios/arquivos</td> 
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></td> 
</tr>
<tr> 
<td>Excluir compartilhamentos/diretórios/arquivos</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Introdução ao Serviço de Arquivos do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Propriedades/metadados de diretório</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></td> 
</tr> 
<tr> 
<td>Baixar arquivos</td> 
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></td> 
</tr> 
<tr> 
<td>Metadados/propriedades/métricas de arquivo</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></td> 
</tr> 
<tr> 
<td>Propriedades do serviço de arquivo</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></td> 
</tr> 
<tr> 
<td>Listar diretórios e arquivos</td> 
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></td> 
</tr>
<tr> 
<td>Listar compartilhamentos</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></td> 
</tr>
<tr> 
<td>Compartilhar metadados/propriedades/estatísticas</td> 
<td><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Exemplo de Armazenamento de Arquivos do .NET para Armazenamento do Azure</a></td> 
</tr>
<tr> 
<td rowspan="8"><b>Fila</b></td>
<td>Adicionar mensagem</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Criptografia do cliente</td> 
<td><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Criptografia de fila do lado do cliente do .NET para Armazenamento do Azure</a></td> 
</tr> 
<tr> 
<td>Criar filas</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Excluir mensagem/fila</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Espiar mensagem</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>ACL/metadados/estatísticas de fila</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Introdução ao Serviço Fila do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Propriedades do serviço de fila</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Introdução ao Serviço Fila do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Atualização de mensagem</td> 
<td><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Introdução ao Serviço Fila do Azure no .NET</a></td> 
</tr> 
<tr> 
<td rowspan="7"><b>Tabela</b></td>
<td>Criar tabela</td> 
<td><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gerenciando a simultaneidade usando o Armazenamento do Azure — aplicativo de amostra</a></td> 
</tr> 
<tr> 
<td>Excluir entidade/tabela</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabela do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Inserir/mesclar/substituir entidade</td> 
<td><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gerenciando a simultaneidade usando o Armazenamento do Azure — aplicativo de amostra</a></td> 
</tr> 
<tr> 
<td>Query Entities</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabela do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Consultar tabelas</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introdução ao Armazenamento de Tabela do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Propriedades/ACL de tabela</td> 
<td><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Introdução ao Armazenamento de Tabela do Azure no .NET</a></td> 
</tr> 
<tr> 
<td>Update Entity</td> 
<td><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gerenciando a simultaneidade usando o Armazenamento do Azure — aplicativo de amostra</a></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a>Biblioteca de Exemplos de Código do Azure

biblioteca de exemplo completo tooview hello, vá toohello [exemplos de código do Azure](https://azure.microsoft.com/resources/samples/?service=storage) biblioteca, que inclui exemplos de armazenamento do Azure que você pode baixar e executar localmente. Olá biblioteca de código de exemplo fornece código de exemplo em formato. zip. Como alternativa, você pode procurar e clonar o repositório do GitHub Olá para cada exemplo.

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a>Guias de introdução

Check-out Olá guias a seguir se você está procurando obter instruções sobre como tooinstall e introdução a saudação bibliotecas de cliente de armazenamento do Azure.

* [Introdução ao Serviço Blob do Azure no .NET](storage-dotnet-how-to-use-blobs.md)
* [Introdução ao Serviço Fila do Azure no .NET](storage-dotnet-how-to-use-queues.md)
* [Introdução ao Serviço Tabela do Azure no .NET](storage-dotnet-how-to-use-tables.md)
* [Introdução ao Serviço de Arquivos do Azure no .NET](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a>Próximas etapas

Para saber mais sobre exemplos para outras linguagens:

* Java: [Exemplos de Armazenamento do Azure usando Java](storage-samples-java.md)
* Todas as outras linguagens: [Exemplos de Armazenamento do Azure](storage-samples.md)
