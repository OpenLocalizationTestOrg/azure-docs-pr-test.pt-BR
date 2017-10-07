---
title: aaaMove tooand de dados do armazenamento de BLOBs do Azure usando AzCopy | Microsoft Docs
description: Mover dados tooand do armazenamento de BLOBs do Azure usando AzCopy
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: c309ceb2-0e83-4a07-b16d-c997dcd62d5c
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: b381ba004ac16879b6c633950d03d13ad82d5b72
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azcopy"></a>Mover dados tooand do armazenamento de BLOBs do Azure usando AzCopy
AzCopy é um utilitário de linha de comando projetado para carregar, baixar e tooand cópia de dados de blob do Microsoft Azure, arquivo e armazenamento de tabela.

Para obter instruções sobre como instalar o AzCopy e informações adicionais em usá-lo com hello plataforma Windows Azure, consulte [guia de Introdução com hello o utilitário de linha de comando AzCopy](../storage/common/storage-use-azcopy.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Se você estiver usando a VM que foi configurado com scripts Olá fornecidos pela [máquinas virtuais de ciência de dados no Azure](machine-learning-data-science-virtual-machines.md), em seguida, AzCopy já está instalado na VM de saudação.
> 
> [!NOTE]
> Para um armazenamento de blob tooAzure introdução completa, consulte muito[Noções básicas de Blob do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e muito[serviço Blob do Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Este documento presume que você tenha uma assinatura do Azure, uma conta de armazenamento e Olá a correspondente chave de armazenamento para essa conta. Antes de carregar/baixar os dados, você deve conhecer o nome e a chave da sua conta do Armazenamento do Azure.

* tooset uma assinatura do Azure, consulte [um mês avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Para obter instruções sobre como criar uma conta de armazenamento e obter informações sobre conta e chave, consulte [Sobre contas do armazenamento do Azure](../storage/common/storage-create-storage-account.md).

## <a name="run-azcopy-commands"></a>Executar comandos do AzCopy
comandos do AzCopy toorun, abra uma janela de comando e navegue toohello AzCopy diretório de instalação no seu computador, em que o executável de AzCopy.exe hello está localizado. 

Olá a sintaxe básica para comandos do AzCopy é:

    AzCopy /Source:<source> /Dest:<destination> [Options]

> [!NOTE]
> Você pode adicionar o caminho de sistema de tooyour Olá AzCopy instalação local e, em seguida, execute os comandos de saudação de qualquer diretório. Por padrão, AzCopy é instalado muito*% ProgramFiles (x86) %\Microsoft SDKs\Azure\AzCopy* ou *%ProgramFiles%\Microsoft SDKs\Azure\AzCopy*.
> 
> 

## <a name="upload-files-tooan-azure-blob"></a>Carregar arquivos tooan BLOBs do Azure
tooupload um arquivo, use Olá comando a seguir:

    # Upload from local file system
    AzCopy /Source:<your_local_directory> /Dest: https://<your_account_name>.blob.core.windows.net/<your_container_name> /DestKey:<your_account_key> /S


## <a name="download-files-from-an-azure-blob"></a>Baixe arquivos em um blob do Azure
toodownload um arquivo de um blob do Azure, use Olá comando a seguir:

    # Downloading blobs toolocal file system
    AzCopy /Source:https://<your_account_name>.blob.core.windows.net/<your_container_name>/<your_sub_directory_at_blob>  /Dest:<your_local_directory> /SourceKey:<your_account_key> /Pattern:<file_pattern> /S


## <a name="transfer-blobs-between-azure-containers"></a>Transferir os blobs entre os contêineres do Azure
blobs tootransfer entre contêineres do Azure, use Olá comando a seguir:

    # Transferring blobs between Azure containers
    AzCopy /Source:https://<your_account_name1>.blob.core.windows.net/<your_container_name1>/<your_sub_directory_at_blob1> /Dest:https://<your_account_name2>.blob.core.windows.net/<your_container_name2>/<your_sub_directory_at_blob2> /SourceKey:<your_account_key1> /DestKey:<your_account_key2> /Pattern:<file_pattern> /S

    <your_account_name>: your storage account name
    <your_account_key>: your storage account key
    <your_container_name>: your container name
    <your_sub_directory_at_blob>: hello sub directory in hello container
    <your_local_directory>: directory of local file system where files toobe uploaded from or hello directory of local file system files toobe downloaded to
    <file_pattern>: pattern of file names toobe transferred. hello standard wildcards are supported


## <a name="tips-for-using-azcopy"></a>Dicas para usar o AzCopy
> [!TIP]
> 1. Ao **carregar** arquivos, */S* carregará arquivos recursivamente. Sem esse parâmetro, arquivos em subpastas não serão carregados.  
> 2. Quando **baixando** arquivo, */S* pesquisas Olá contêiner de forma recursiva até que todos os arquivos no diretório especificado hello e seus subdiretórios, ou todos os arquivos que correspondem a Olá padrão especificado no hello fornecido diretório e seus subdiretórios, são baixadas.  
> 3. Não é possível especificar um **arquivo blob específico** toodownload usando Olá */fonte* parâmetro. toodownload um arquivo específico, especifique usando Olá dos toodownload de nome de arquivo hello blob */padrão* parâmetro. **/S** parâmetro pode ser usado toohave AzCopy procure um recursivamente de padrão de nome de arquivo. Sem o parâmetro de padrão de hello, AzCopy baixa todos os arquivos nesse diretório.
> 
> 

