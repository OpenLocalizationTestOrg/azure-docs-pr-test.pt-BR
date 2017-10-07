---
title: aaaHow toocreate um compartilhamento de arquivos do Azure | Microsoft Docs
description: "Como toocreate um arquivo do Azure compartilham no armazenamento de arquivo do Azure usando Olá portal do Azure, PowerShell e Olá CLI do Azure."
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
ms.openlocfilehash: c4c59966b82d743fb4ecf79f48c0c8e61295d03d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-file-share-in-azure-file-storage"></a>Criar um Compartilhamento de Arquivos no Armazenamento de arquivos do Azure
Você pode criar compartilhamentos de arquivos do Azure usando [portal do Azure](https://portal.azure.com/), Olá cmdlets do PowerShell do armazenamento do Azure, Olá bibliotecas de cliente de armazenamento do Azure ou Olá API de REST do armazenamento do Azure. Neste tutorial, você aprenderá:
* [Como toocreate um arquivo Azure compartilhar usando Olá portal do Azure](#Create file share through hello Portal)
* [Como toocreate um Azure compartilhamento de arquivos usando o Powershell](#Create file share using PowerShell)
* [Como toocreate um arquivo Azure compartilhar usando a CLI](#create-file-share-using-command-line-interface-cli)

## <a name="prerequisites"></a>Pré-requisitos
toocreate um compartilhamento de arquivos do Azure, você pode usar uma conta de armazenamento que já existe, ou [criar uma nova conta de armazenamento do Azure](storage-create-storage-account.md). toocreate um compartilhamento de arquivos do Azure com o PowerShell, você precisará de chave da conta de saudação e o nome da sua conta de armazenamento. Chave de conta de armazenamento será necessário se você planejar toouse Powershell ou CLI.

## <a name="create-file-share-through-hello-portal"></a>Criar compartilhamento de arquivos por meio do Portal de saudação
1. **Folha de conta de tooStorage vá no Portal do Azure**:    
    ![Folha Conta de Armazenamento](media/storage-file-how-to-create-file-share/create-file-share-portal1.png)

2. **Clique no botão Adicionar Compartilhamento de arquivos**:    
    ![Clique em Olá adicionar um botão de compartilhamento de arquivo](media/storage-file-how-to-create-file-share/create-file-share-portal2.png)

3. **Forneça o Nome e a Cota. A cota atualmente pode ter um máximo de 5 TB**:    
    ![Forneça um nome e uma cota desejada para o novo compartilhamento de arquivo hello](media/storage-file-how-to-create-file-share/create-file-share-portal3.png)

4. **Exiba o novo compartilhamento de arquivos**: ![Exiba o novo compartilhamento de arquivos](media/storage-file-how-to-create-file-share/create-file-share-portal4.png)

5. **Carregue um arquivo**: ![Carregue um arquivo](media/storage-file-how-to-create-file-share/create-file-share-portal5.png)

6. **Navegue o compartilhamento de arquivos e gerencie seus diretórios e arquivos**: ![Navegue o compartilhamento de arquivos](media/storage-file-how-to-create-file-share/create-file-share-portal6.png)


## <a name="create-file-share-through-powershell"></a>Criar um compartilhamento de arquivos com o PowerShell
tooprepare toouse PowerShell, baixe e instale Olá cmdlets do PowerShell do Azure. Consulte [como tooinstall e configurar o Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) para Olá instalar ponto e instruções de instalação.

> [!Note]  
> É recomendável baixar e instalar ou atualizar toohello último módulo do PowerShell do Azure.

1. **Criar um contexto para a conta de armazenamento e a chave** contexto Olá encapsula a chave de nome e uma conta de conta de armazenamento do hello. Para obter instruções sobre como copiar a chave da conta no [portal do Azure](https://portal.azure.com/), veja [Exibir e copiar chaves de acesso de armazenamento](storage-create-storage-account.md#view-and-copy-storage-access-keys).

    ```powershell
    $storageContext = New-AzureStorageContext <storage-account-name> <storage-account-key>
    ```
    
2. **Criar um novo compartilhamento de arquivos**:    
    
    ```powershell
    $share = New-AzureStorageShare logs -Context $storageContext
    ```

> [!Note]  
> nome de saudação do seu compartilhamento de arquivo deve ser todas minúscula. Para obter detalhes completos sobre como nomear arquivos e compartilhamentos de arquivos, confira [Nomenclatura e referência de compartilhamentos, diretórios, arquivos e metadados](https://msdn.microsoft.com/library/azure/dn167011.aspx).

## <a name="create-file-share-through-command-line-interface-cli"></a>Criar um compartilhamento de arquivos com a Interface da Linha de Comando (CLI)
1. **tooprepare toouse uma Interface de linha de comando (CLI), baixe e instale Olá CLI do Azure.**  
    Consulte [Instalar a CLI do Azure 2.0](/cli/azure/install-az-cli2.md) e [Introdução à CLI do Azure 2.0](/cli/azure/get-started-with-azure-cli.md).

2. **Crie uma conta de armazenamento conexão cadeia de caracteres toohello onde você deseja que o compartilhamento de saudação toocreate.**  
    Substituir ```<storage-account>``` e ```<resource_group>``` com seu grupo de recursos e o nome da conta de armazenamento no hello exemplo a seguir.

   ```azurecli
    current_env_conn_string = $(az storage account show-connection-string -n <storage-account> -g <resource-group> --query 'connectionString' -o tsv)

    if [[ $current_env_conn_string == "" ]]; then  
        echo "Couldn't retrieve hello connection string."
    fi
    ```

3. **Criar um compartilhamento de arquivos**
    ```azurecli
    az storage share create --name files --quota 2048 --connection-string $current_env_conn_string 1 > /dev/null
    ```

## <a name="next-steps"></a>Próximas etapas
* [Conecte e Monte o Compartilhamento de Arquivos - Windows](storage-file-how-to-use-files-windows.md)
* [Conecte e Monte o Compartilhamento de Arquivos - Linux](storage-how-to-use-files-linux.md)
* [Conecte e Monte o Compartilhamento de Arquivos - macOS](storage-file-how-to-use-files-mac.md)

Consulte estes links para obter mais informações sobre o armazenamento de arquivo do Azure.

* [Perguntas frequentes](storage-files-faq.md)
* [Solução de problemas](storage-troubleshoot-file-connection-problems.md)