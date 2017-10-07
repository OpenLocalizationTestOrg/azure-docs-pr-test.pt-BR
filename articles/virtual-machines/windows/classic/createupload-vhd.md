---
title: aaaCreate e carregar uma VM da imagem usando o Powershell | Microsoft Docs
description: "Saiba toocreate e carregue uma imagem do Windows Server generalizada (VHD) usando o modelo de implantação clássico hello e do Powershell do Azure."
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 8c4a08fe-7714-4bf0-be87-c728a7806d3f
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/23/2017
ms.author: cynthn
ms.openlocfilehash: 093b57c9157cea5f348c8ba02b5700c917adbcdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a>Criar e carregar um VHD do Windows Server tooAzure
Este artigo mostra como tooupload sua própria VM generalizada de imagem como um disco rígido virtual (VHD), você pode usar máquinas virtuais de toocreate. Para mais detalhes sobre discos e os VHDs no Microsoft Azure, confira a seção [Sobre discos e VHDs para Máquinas Virtuais](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md). Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Você também pode [carregar](../upload-generalized-managed.md) uma máquina virtual usando o modelo do Gerenciador de recursos de saudação.

## <a name="prerequisites"></a>Pré-requisitos
Este artigo supõe que você tem:

* **Uma assinatura do Azure** - se não tiver uma, você poderá [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).
* **[Microsoft Azure PowerShell](/powershell/azure/overview)**  -ter Olá Microsoft Azure PowerShell module instalada e configurada toouse sua assinatura.
* **A. Arquivo VHD** - Windows com suporte, armazenado em um arquivo. vhd e a máquina virtual de tooa anexado de sistema operacional. Verifique toosee se funções de servidor de saudação em execução no hello VHD forem compatíveis com Sysprep. Para obter mais informações, consulte [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).

    > [!IMPORTANT]
    > Não há suporte para o formato VHDX Olá no Microsoft Azure. Você pode converter o formato de tooVHD Olá de disco usando o Gerenciador do Hyper-V ou Olá [cmdlet Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx). Consulte esta [publicação de blog](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx)para obter detalhes.

## <a name="step-1-prep-hello-vhd"></a>Etapa 1: Preparar Olá VHD
Antes de carregar Olá VHD tooAzure, ele precisa toobe generalizado usando a ferramenta Sysprep de saudação. Isso prepara Olá toobe VHD usado como uma imagem. Para obter detalhes sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx). Faça backup Olá VM antes de executar o Sysprep.

De máquina virtual Olá Olá o sistema operacional foi instalada para concluir a saudação procedimento a seguir:

1. Faça logon no sistema de operacional toohello.
2. Abra uma janela de prompt de comando como administrador. Altere o diretório de saudação muito**%windir%\system32\sysprep**e, em seguida, execute `sysprep.exe`.

    ![Abrir una janela de Prompt de comando](./media/createupload-vhd/sysprep_commandprompt.png)
3. Olá **ferramenta de preparação do sistema** caixa de diálogo é exibida.

   ![Inicie o Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. Em Olá **ferramenta de preparação do sistema**, selecione **digite sistema de OOBE (configuração)** e certifique-se de que **generalizar** é verificada.
5. Em **Opções de Desligamento**, selecione **Desligar**.
6. Clique em **OK**.

## <a name="step-2-create-a-storage-account-and-a-container"></a>Etapa 2: criar uma conta de armazenamento e um contêiner
Você precisa de uma conta de armazenamento no Azure para que você tenha um arquivo. vhd do local tooupload hello. Esta etapa mostra como toocreate uma conta ou get hello informações você precisa de uma conta existente. Substituir variáveis de saudação em &lsaquo; colchetes &rsaquo; com suas próprias informações.

1. Logon

    ```powershell
    Add-AzureAccount
    ```

2. Defina sua assinatura do Azure.

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. Criar uma nova conta de armazenamento. nome de Olá Olá da conta de armazenamento deve ser exclusivo, 3 a 24 caracteres. nome da saudação pode ser qualquer combinação de letras e números. Você também precisa toospecify um local como "Leste nós"

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. Definir a nova conta de armazenamento hello como padrão de saudação.

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. Criar um novo contêiner.

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a>Etapa 3: Carregar o arquivo. vhd de saudação
Saudação de uso [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) Olá tooupload VHD.

Na janela do PowerShell do Azure de Olá usado na etapa anterior hello, tipo hello comando a seguir e substitua variáveis Olá em &lsaquo; colchetes &rsaquo; com suas próprias informações.

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a>Etapa 4: Adicionar lista de tooyour de imagem de saudação de imagens personalizadas
Saudação de uso [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) lista de toohello de imagem do cmdlet tooadd Olá de imagens personalizadas.

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a>Próximas etapas
Agora você pode [criar uma máquina virtual personalizada](createportal.md) usando Olá imagem que você carregou.
