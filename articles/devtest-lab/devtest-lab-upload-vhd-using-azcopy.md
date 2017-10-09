---
title: aaaUpload VHD arquivo tooAzure DevTest Labs usando AzCopy | Microsoft Docs
description: Carregar conta de armazenamento do toolab do arquivo VHD usando AzCopy
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 14f9e933b0bd27451f6bcb94841ecc381213e578
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-azcopy"></a>Carregar conta de armazenamento do toolab do arquivo VHD usando AzCopy

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

No Azure DevTest Labs, arquivos VHD podem ser imagens personalizadas usadas toocreate, que são máquinas virtuais de tooprovision usado. Olá etapas a seguir orientam usando tooupload de utilitário de linha de comando AzCopy Olá conta de armazenamento de um VHD arquivo tooa lab. Depois de carregar seu arquivo VHD, Olá [próximas etapas seção](#next-steps) lista alguns artigos que ilustram como toocreate uma imagem personalizada do hello carregado o arquivo VHD. Para saber mais sobre discos e VHDs no Azure, confira [Sobre discos e VHDs para máquinas virtuais](../virtual-machines/linux/about-disks-and-vhds.md)

> [!NOTE] 
>  
> O AzCopy é um utilitário de linha de comando somente para Windows.

## <a name="step-by-step-instructions"></a>Instruções passo a passo

Olá seguindo as etapas da extensão de arquivo por meio de carregar um VHD tooAzure DevTest Labs usando [AzCopy](http://aka.ms/downloadazcopy). 

1. Obter nome de saudação do laboratório de saudação conta de armazenamento usando Olá portal do Azure:

1. Entrar toohello [portal do Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).

1. Selecione **mais serviços**e, em seguida, selecione **DevTest Labs** da lista de saudação.

1. Saudação de laboratórios, selecione lista laboratório desejado hello.  

1. Na folha do laboratório hello, selecione **configuração**. 

1. Laboratório Olá **configuração** folha, selecione **imagens personalizadas (VHDs)**.

1. Em Olá **imagens personalizadas** folha, selecione **+ adicionar**. 

1. Em Olá **imagem personalizada** folha, selecione **VHD**.

1. Em Olá **VHD** folha, selecione **carregar um VHD usando o PowerShell**.

    ![Carregar o VHD usando o PowerShell](./media/devtest-lab-upload-vhd-using-azcopy/upload-image-using-psh.png)

1. Olá **carregue uma imagem usando o PowerShell** folha exibe uma chamada toohello **Add-AzureVhd** cmdlet. Olá primeiro parâmetro (*destino*) contém Olá URI para um contêiner de blob (*carrega*) em Olá formato a seguir:

    ```
    https://<STORAGE-ACCOUNT-NAME>.blob.core.windows.net/uploads/...
    ``` 

1. Anote Olá completo URI como ele é usado em etapas posteriores.

1. Carregar arquivo VHD hello usando AzCopy:
 
1. [Baixe e instale a versão mais recente de saudação do AzCopy](http://aka.ms/downloadazcopy).

1. Abra uma janela de comando e navegue diretório de instalação do toohello AzCopy. Opcionalmente, você pode adicionar o caminho de sistema de tooyour Olá AzCopy instalação local. Por padrão, AzCopy é instalado toohello diretório a seguir:

    ```command-line
    %ProgramFiles(x86)%\Microsoft SDKs\Azure\AzCopy
    ```

1. Usando Olá armazenamento conta chave e blob URI do contêiner, execute Olá comando no prompt de comando Olá a seguir. Olá *vhdFileName* valor precisa toobe entre aspas. processo de saudação de carregamento de um arquivo VHD pode ser demorado, dependendo do tamanho de saudação do arquivo VHD hello e a velocidade de conexão.   

    ```command-line
    AzCopy /Source:<sourceDirectory> /Dest:<blobContainerUri> /DestKey:<storageAccountKey> /Pattern:"<vhdFileName>" /BlobType:page
    ```

## <a name="next-steps"></a>Próximas etapas

- [Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando Olá portal do Azure](devtest-lab-create-template.md)
- [Criar uma imagem personalizada no Azure DevTest Labs de um arquivo VHD usando o PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)