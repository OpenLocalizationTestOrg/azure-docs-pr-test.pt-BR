---
title: "aaaCreating uma imagem de máquina virtual local para hello Azure Marketplace | Microsoft Docs"
description: "Compreender e executar Olá etapas toocreate uma imagem VM no local e implantar toohello Azure Marketplace para outros toopurchase."
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: 26dfbd5a-8685-4b19-987e-c20ca60540ec
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c7a265330f1e494db8d0e981a38ee00d85746bb1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-an-on-premises-virtual-machine-image-for-hello-azure-marketplace"></a>Desenvolver uma imagem de máquina virtual local para hello Azure Marketplace
É altamente recomendável que você desenvolver Azure discos rígidos virtuais (VHDs) diretamente na nuvem hello usando o protocolo de área de trabalho remota. No entanto, se for necessário, é possível toodownload um VHD e desenvolvê-lo usando a infraestrutura local.  

Para o desenvolvimento local, você deve baixar o VHD de saudação criada do sistema operacional do hello VM. Essas etapas podem ocorrer como parte da etapa 3.3 acima.  

## <a name="download-a-vhd-image"></a>Baixar uma imagem VHD
### <a name="locate-a-blob-url"></a>Localize uma URL para Blobs
Em Olá VHD do toodownload ordem, primeiro localize Olá URL do blob de disco do sistema operacional hello.

Localizar a URL de blob de saudação da saudação novo [portal do Microsoft Azure](https://portal.azure.com):

1. Vá muito**procurar** > **VMs**, e, em seguida, selecione Olá implantado VM.
2. Em **configurar**, selecione Olá **discos** lado a lado, que abre a folha de discos de saudação.
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img01.png)
3. Selecione Olá **disco do sistema operacional**, que abre outra folha que exibe as propriedades do disco, incluindo o local do VHD hello.
4. Copie a URL do blob.
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img02.png)
5. Agora, excluir Olá implantado VM sem excluir os discos de backup hello. Você também pode interromper Olá VM em vez de excluí-lo. Não baixe o VHD do sistema operacional hello quando Olá VM está em execução.
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img03.png)

### <a name="download-a-vhd"></a>Baixe um VHD
Depois que você souber a URL do blob Olá, você pode baixar Olá VHD usando Olá [portal do Azure](http://manage.windowsazure.com/) ou o PowerShell.  

> [!NOTE]
> Em tempo de saudação da criação deste guia, toodownload de funcionalidade Olá um VHD ainda não está presente no novo portal do Microsoft Azure hello.  
> 
> 

**Baixar Olá VHD do sistema operacional por meio de saudação atual [portal do Azure](http://manage.windowsazure.com/)**

1. Entrar no portal do Azure de toohello se você ainda não fez isso.
2. Clique em Olá **armazenamento** guia.
3. Selecione a conta de armazenamento de saudação em qual Olá VHD é armazenado.
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img04.png)
4. Isso exibe as propriedades da conta de armazenamento. Selecione Olá **contêineres** guia.
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img05.png)
5. Selecione Olá contêiner no qual Olá VHD é armazenado. Por padrão, quando criadas no portal de saudação Olá VHD é armazenado em um contêiner de vhds.
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img06.png)
6. Selecione Olá correto VHD do sistema operacional, comparando Olá URL toohello um que é salvo.
7. Clique em **Download**.
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img07.png)

### <a name="download-a-vhd-by-using-powershell"></a>Baixar um VHD usando o PowerShell
Além disso toousing Olá portal do Azure, você pode usar o hello [Save-AzureVhd](http://msdn.microsoft.com/library/dn495297.aspx) cmdlet toodownload Olá VHD do sistema operacional.

        Save-AzureVhd –Source <storageURIOfVhd> `
        -LocalFilePath <diskLocationOnWorkstation> `
        -StorageKey <keyForStorageAccount>
Por exemplo, Save-AzureVhd -Source “https://baseimagevm.blob.core.windows.net/vhds/BaseImageVM-6820cq00-BaseImageVM-os-1411003770191.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\baseimagevm.vhd” -StorageKey <String>

> [!NOTE]
> **Save-AzureVhd** também tem um **NumberOfThreads** opção que pode ser usado tooincrease paralelismo toomake Olá melhor uso de largura de banda disponível para download de saudação.
> 
> 

## <a name="upload-vhds-tooan-azure-storage-account"></a>Carregar VHDs tooan conta de armazenamento Azure
Se você preparou seus VHDs locais, você precisa tooupload-los em um armazenamento de conta no Azure. Esta etapa ocorre depois de criar o VHD local, mas antes de obter a certificação para a imagem da VM.

### <a name="create-a-storage-account-and-container"></a>Criar uma conta e um contêiner de armazenamento
É recomendável que os VHDs ser carregado em uma conta de armazenamento em uma região de saudação dos Estados Unidos. Todos os VHDs para uma única SKU devem ser colocados em um único contêiner dentro de uma única conta de armazenamento.

toocreate uma conta de armazenamento, você pode usar o hello [portal do Microsoft Azure](https://portal.azure.com/), PowerShell ou ferramenta de linha de comando do Linux hello.  

**Criar uma conta de armazenamento do portal do Microsoft Azure Olá**

1. Clique em **Novo**.
2. Selecione **Armazenamento**.
3. Preencha o nome de conta de armazenamento hello e, em seguida, selecione um local.
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img08.png)
4. Clique em **Criar**.
5. folha de saudação para Olá criado a conta de armazenamento deve estar aberta. Caso contrário, selecione **Procurar** > **Contas de Armazenamento**. Olá armazenamento conta folha, selecione a conta de armazenamento Olá criada.
6. Selecione **Contêineres**.
   
   ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img09.png) 
7. Na folha de contêineres hello, selecione **adicionar**e, em seguida, insira um permissões de contêiner de nome e a saudação do contêiner. Selecione **Particular** nas permissões do contêiner.

> [!TIP]
> É recomendável que você crie um contêiner de por que você está planejando toopublish SKU.
> 
> 

  ![desenho](media/marketplace-publishing-vm-image-creation-on-premise/img10.png)

### <a name="create-a-storage-account-by-using-powershell"></a>Criar uma conta de armazenamento usando o PowerShell
Usando o PowerShell, crie uma conta de armazenamento usando Olá [AzureStorageAccount novo](http://msdn.microsoft.com/library/dn495115.aspx) cmdlet.

        New-AzureStorageAccount -StorageAccountName “mystorageaccount” -Location “West US”

Em seguida, você pode criar um contêiner dentro dessa conta de armazenamento usando Olá [NewAzureStorageContainer](http://msdn.microsoft.com/library/dn495291.aspx) cmdlet.

        New-AzureStorageContainer -Name “containername” -Permission “Off”

> [!NOTE]
> Esses comandos pressupõem que contexto de conta de armazenamento atual da saudação já foi definido no PowerShell.   Consulte também[Configurando o Azure PowerShell](marketplace-publishing-powershell-setup.md) para obter mais detalhes sobre a instalação do PowerShell.  
> 
> ### <a name="create-a-storage-account-by-using-hello-command-line-tool-for-mac-and-linux"></a>Criar uma conta de armazenamento usando a ferramenta de linha de comando Olá para Mac e Linux
> A partir da [ferramenta de linha de comando do Linux](../virtual-machines/linux/cli-manage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), crie uma conta de armazenamento da seguinte maneira.
> 
> 

        azure storage account create mystorageaccount --location "West US"

Crie um contêiner da seguinte maneira.

        azure storage container create containername --account-name mystorageaccount --accountkey <accountKey>

## <a name="upload-a-vhd"></a>Carregar um VHD
Depois que o contêiner e a conta de armazenamento Olá são criados, você pode carregar seus VHDs preparadas. Você pode usar o PowerShell, a ferramenta de linha de comando do Linux hello ou outras ferramentas de gerenciamento de armazenamento do Azure.

### <a name="upload-a-vhd-via-powershell"></a>Carregar um VHD por meio do PowerShell
Saudação de uso [Add-AzureVhd](http://msdn.microsoft.com/library/dn495173.aspx) cmdlet.

        Add-AzureVhd –Destination “http://mystorageaccount.blob.core.windows.net/containername/vmsku.vhd” -LocalFilePath “C:\Users\Administrator\Desktop\vmsku.vhd”

### <a name="upload-a-vhd-by-using-hello-command-line-tool-for-mac-and-linux"></a>Carregar um VHD usando a ferramenta de linha de comando Olá para Mac e Linux
Com hello [ferramenta de linha de comando do Linux](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2), use Olá seguinte: criar a imagem da vm do azure <image name> – local <Location of hello data center> – sistema operacional Linux<LocationOfLocalVHD>

## <a name="see-also"></a>Consulte também
* [Criar uma imagem de máquina virtual para Olá Marketplace](marketplace-publishing-vm-image-creation.md)
* [Configurando o PowerShell do Azure](marketplace-publishing-powershell-setup.md)

