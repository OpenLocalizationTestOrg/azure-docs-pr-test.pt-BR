---
title: aaaMove tooand de dados do armazenamento de BLOBs do Azure usando Python | Microsoft Docs
description: Mover dados tooand do armazenamento de BLOBs do Azure usando Python
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 24276252-b3dd-4edf-9e5d-f6803f8ccccc
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: c2be9600e0d6cb05bcf4109a8d554db522704ecb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-python"></a>Mover dados tooand do armazenamento de BLOBs do Azure usando Python
Este tópico descreve como toolist, carregar e baixar blobs usando Olá API de Python. Com hello API Python fornecido no SDK do Azure, você pode:

* Criar um contêiner
* Carregar um blob em um contêiner
* Baixar blobs
* Saudação de listar blobs em um contêiner
* Excluir um blob

Para obter mais informações sobre como usar o hello Python API, consulte [como tooUse Olá serviço de armazenamento de Blob do Python](../storage/blobs/storage-python-how-to-use-blob-storage.md).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> Se você estiver usando a VM que foi configurado com scripts Olá fornecidos pela [máquinas virtuais de ciência de dados no Azure](machine-learning-data-science-virtual-machines.md), em seguida, AzCopy já está instalado na VM de saudação.
> 
> [!NOTE]
> Para um armazenamento de blob tooAzure introdução completa, consulte muito[Noções básicas de Blob do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) e muito[serviço Blob do Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
Este documento assume que você tenha uma assinatura do Azure, uma conta de armazenamento e chave de armazenamento correspondente Olá para essa conta. Antes de carregar/baixar os dados, você deve conhecer o nome e a chave da sua conta do Armazenamento do Azure.

* tooset uma assinatura do Azure, consulte [um mês avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).
* Para obter instruções sobre como criar uma conta de armazenamento e obter informações sobre conta e chave, consulte [Sobre contas do armazenamento do Azure](../storage/common/storage-create-storage-account.md).

## <a name="upload-data-tooblob"></a>Carregar dados tooBlob
Adicione Olá trecho superior Olá de qualquer código Python no qual você deseja acesso tooprogrammatically armazenamento do Azure a seguir:

    from azure.storage.blob import BlobService

Olá **BlobService** objeto permite que você trabalhe com contêineres e blobs. saudação de código a seguir cria um objeto de BlobService usando a chave de nome e uma conta de conta de armazenamento do hello. Substitua o nome e a chave de conta pela sua conta e chave reais.

    blob_service = BlobService(account_name="<your_account_name>", account_key="<your_account_key>")

Use Olá blob de tooa métodos tooupload dados a seguir:

1. colocar\_bloco\_blob\_de\_caminho (carrega o conteúdo de saudação de um arquivo do caminho especificado Olá)
2. colocar\_block_blob\_de\_(carrega o conteúdo de saudação de um arquivo já aberto/fluxo) de arquivo
3. put\_block\_blob\_from\_bytes (carrega uma matriz de bytes)
4. colocar\_bloco\_blob\_de\_texto (carrega Olá especificado valor de texto usando Olá codificação especificada)

Olá, código de exemplo a seguir carrega um contêiner de tooa arquivo local:

    blob_service.put_block_blob_from_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Olá seguinte exemplo de código carrega todos os arquivos de saudação (excluindo diretórios) em um armazenamento de tooblob do diretório local:

    from azure.storage.blob import BlobService
    from os import listdir
    from os.path import isfile, join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)
    # find all files in hello LOCAL_DIRECT (excluding directory)
    local_file_list = [f for f in listdir(LOCAL_DIRECT) if isfile(join(LOCAL_DIRECT, f))]

    file_num = len(local_file_list)
    for i in range(file_num):
        local_file = join(LOCAL_DIRECT, local_file_list[i])
        blob_name = local_file_list[i]
        try:
            blob_service.put_block_blob_from_path(CONTAINER_NAME, blob_name, local_file)
        except:
            print "something wrong happened when uploading hello data %s"%blob_name


## <a name="download-data-from-blob"></a>Baixar Dados de Blob
Use Olá seguintes dados de toodownload de métodos de um blob:

1. get\_blob\_to\_path
2. get\_blob\_to\_file
3. get\_blob\_to\_bytes
4. get\_blob\_to\_text

Esses métodos que executam o agrupamento necessário hello quando o tamanho de saudação de dados Olá exceder 64 MB.

Olá, código de exemplo seguinte baixa conteúdo Olá de um blob em um arquivo local do contêiner tooa:

    blob_service.get_blob_to_path("<your_container_name>", "<your_blob_name>", "<your_local_file_name>")

Olá seguinte código de exemplo baixa todos os blobs de um contêiner. Ele usa a lista\_blobs tooget lista de saudação de blobs disponíveis no contêiner hello e baixar os arquivos tooa diretório de local.

    from azure.storage.blob import BlobService
    from os.path import join

    # Set parameters here
    ACCOUNT_NAME = "<your_account_name>"
    ACCOUNT_KEY = "<your_account_key>"
    CONTAINER_NAME = "<your_container_name>"
    LOCAL_DIRECT = "<your_local_directory>"        

    blob_service = BlobService(account_name=ACCOUNT_NAME, account_key=ACCOUNT_KEY)

    # List all blobs and download them one by one
    blobs = blob_service.list_blobs(CONTAINER_NAME)
    for blob in blobs:
        local_file = join(LOCAL_DIRECT, blob.name)
        try:
            blob_service.get_blob_to_path(CONTAINER_NAME, blob.name, local_file)
        except:
            print "something wrong happened when downloading hello data %s"%blob.name
