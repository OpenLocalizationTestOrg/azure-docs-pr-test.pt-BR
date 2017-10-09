---
title: aaaHow toouse PowerShell toomanage armazenamento de arquivo do Azure | Microsoft Docs
description: Saiba o armazenamento de arquivo do Azure toouse PowerShell toomanage.
services: storage
documentationcenter: 
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 7bd84c9cfa31782aedf4a209cb15d4b8d92e2737
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-powershell-toomanage-azure-file-storage"></a>Como toouse PowerShell toomanage armazenamento de arquivo do Azure
Você pode usar o Azure PowerShell toocreate e gerenciar compartilhamentos de arquivos.

## <a name="install-hello-powershell-cmdlets-for-azure-storage"></a>Instalar cmdlets do PowerShell Olá para o armazenamento do Azure
tooprepare toouse PowerShell, baixe e instale Olá cmdlets do PowerShell do Azure. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) para Olá instalar ponto e instruções de instalação.

> [!NOTE]
> É recomendável baixar e instalar ou atualizar toohello último módulo do PowerShell do Azure.
> 
> 

Abra uma janela do Azure PowerShell clicando em **Iniciar** e digitando **Windows PowerShell**. janela do PowerShell Olá carrega o módulo do Powershell do Azure Olá para você.

## <a name="create-a-context-for-your-storage-account-and-key"></a>Criar um contexto para sua conta e chave de armazenamento
Crie o contexto de conta de armazenamento hello. contexto de saudação encapsula a chave de nome e uma conta de conta de armazenamento do hello. Para obter instruções sobre como copiar a chave da conta de saudação [portal do Azure](https://portal.azure.com), consulte [exibir e copiar chaves de acesso de armazenamento](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#view-and-copy-storage-access-keys).

Substituir `storage-account-name` e `storage-account-key` com o nome da conta de armazenamento e a chave no exemplo a seguir de saudação.

```powershell
# create a context for account and key
$ctx=New-AzureStorageContext storage-account-name storage-account-key
```

## <a name="create-a-new-file-share"></a>Criar um novo compartilhamento de arquivo
Criar novo compartilhamento hello, denominado `logs`.

```powershell
# create a new share
$s = New-AzureStorageShare logs -Context $ctx
```

Agora você tem um compartilhamento de arquivo no armazenamento de arquivos. Em seguida, adicionaremos um diretório e um arquivo.

> [!IMPORTANT]
> nome de saudação do seu compartilhamento de arquivo deve ser todas minúscula. Para obter detalhes completos sobre como nomear arquivos e compartilhamentos de arquivos, confira [Nomenclatura e referência de compartilhamentos, diretórios, arquivos e metadados](https://msdn.microsoft.com/library/azure/dn167011.aspx).
> 
> 

## <a name="create-a-directory-in-hello-file-share"></a>Criar um diretório no compartilhamento de arquivo hello
Crie um diretório no compartilhamento de saudação. Olá exemplo a seguir, o diretório de saudação é denominado `CustomLogs`.

```powershell
# create a directory in hello share
New-AzureStorageDirectory -Share $s -Path CustomLogs
```

## <a name="upload-a-local-file-toohello-directory"></a>Carregar um diretório do arquivo local toohello
Agora, carregar um diretório de toohello arquivo local. Olá, exemplo a seguir carrega um arquivo de `C:\temp\Log1.txt`. Edite o caminho do arquivo hello para que ele aponte tooa de arquivo válido na sua máquina local.

```powershell
# upload a local file toohello new directory
Set-AzureStorageFileContent -Share $s -Source C:\temp\Log1.txt -Path CustomLogs
```

## <a name="list-hello-files-in-hello-directory"></a>Listar Olá arquivos no diretório de saudação
arquivo de saudação do toosee no diretório de saudação, você pode listar todos os arquivos do diretório hello. Esse comando retorna subdiretórios e arquivos de saudação (se houver) no diretório de CustomLogs hello.

```powershell
# list files in hello new directory
Get-AzureStorageFile -Share $s -Path CustomLogs | Get-AzureStorageFile
```

Get-AzureStorageFile retorna uma lista de arquivos e diretórios para qualquer objeto de diretório que é passado. "Get-AzureStorageFile-compartilhar $s" retorna uma lista de arquivos e diretórios no diretório raiz de saudação. tooget uma lista de arquivos em um subdiretório, você tem toopass Olá subdiretório tooGet-AzureStorageFile. --Que é o que isso faz a primeira parte saudação do comando Olá o pipe toohello retorna uma instância de diretório do subdiretório Olá CustomLogs. Em seguida, que é passado para Get-AzureStorageFile, que retorna Olá arquivos e diretórios em CustomLogs.

## <a name="copy-files"></a>Copiar arquivos
A partir da versão 0.9.7 do PowerShell do Azure, você pode copiar um arquivo de tooanother, um blob de tooa de arquivo ou um arquivo de tooa de blob. Abaixo, demonstraremos como tooperform esses copiam operações usando cmdlets do PowerShell.

```powershell
# copy a file toohello new directory
Start-AzureStorageFileCopy -SrcShareName srcshare -SrcFilePath srcdir/hello.txt -DestShareName destshare -DestFilePath destdir/hellocopy.txt -Context $srcCtx -DestContext $destCtx

# copy a blob tooa file directory
Start-AzureStorageFileCopy -SrcContainerName srcctn -SrcBlobName hello2.txt -DestShareName hello -DestFilePath hellodir/hello2copy.txt -DestContext $ctx -Context $ctx
```
## <a name="next-steps"></a>Próximas etapas
Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.

* [Perguntas frequentes](../storage-files-faq.md)
* [Solução de problemas no Windows](storage-troubleshoot-windows-file-connection-problems.md)      
* [Solução de problemas no Linux](storage-troubleshoot-linux-file-connection-problems.md)    