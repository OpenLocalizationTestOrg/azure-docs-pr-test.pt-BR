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
# <a name="create-and-upload-a-windows-server-vhd-tooazure"></a><span data-ttu-id="39f3e-103">Criar e carregar um VHD do Windows Server tooAzure</span><span class="sxs-lookup"><span data-stu-id="39f3e-103">Create and upload a Windows Server VHD tooAzure</span></span>
<span data-ttu-id="39f3e-104">Este artigo mostra como tooupload sua própria VM generalizada de imagem como um disco rígido virtual (VHD), você pode usar máquinas virtuais de toocreate.</span><span class="sxs-lookup"><span data-stu-id="39f3e-104">This article shows you how tooupload your own generalized VM image as a virtual hard disk (VHD) so you can use it toocreate virtual machines.</span></span> <span data-ttu-id="39f3e-105">Para mais detalhes sobre discos e os VHDs no Microsoft Azure, confira a seção [Sobre discos e VHDs para Máquinas Virtuais](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="39f3e-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="39f3e-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="39f3e-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="39f3e-107">Este artigo aborda usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="39f3e-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="39f3e-108">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="39f3e-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="39f3e-109">Você também pode [carregar](../upload-generalized-managed.md) uma máquina virtual usando o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="39f3e-109">You can also [upload](../upload-generalized-managed.md) a virtual machine using hello Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="39f3e-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="39f3e-110">Prerequisites</span></span>
<span data-ttu-id="39f3e-111">Este artigo supõe que você tem:</span><span class="sxs-lookup"><span data-stu-id="39f3e-111">This article assumes you have:</span></span>

* <span data-ttu-id="39f3e-112">**Uma assinatura do Azure** - se não tiver uma, você poderá [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="39f3e-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="39f3e-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)**  -ter Olá Microsoft Azure PowerShell module instalada e configurada toouse sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="39f3e-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - You have hello Microsoft Azure PowerShell module installed and configured toouse your subscription.</span></span>
* <span data-ttu-id="39f3e-114">**A. Arquivo VHD** - Windows com suporte, armazenado em um arquivo. vhd e a máquina virtual de tooa anexado de sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="39f3e-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached tooa virtual machine.</span></span> <span data-ttu-id="39f3e-115">Verifique toosee se funções de servidor de saudação em execução no hello VHD forem compatíveis com Sysprep.</span><span class="sxs-lookup"><span data-stu-id="39f3e-115">Check toosee if hello server roles running on hello VHD are supported by Sysprep.</span></span> <span data-ttu-id="39f3e-116">Para obter mais informações, consulte [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="39f3e-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="39f3e-117">Não há suporte para o formato VHDX Olá no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="39f3e-117">hello VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="39f3e-118">Você pode converter o formato de tooVHD Olá de disco usando o Gerenciador do Hyper-V ou Olá [cmdlet Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="39f3e-118">You can convert hello disk tooVHD format using Hyper-V Manager or hello [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="39f3e-119">Consulte esta [publicação de blog](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx)para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="39f3e-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-hello-vhd"></a><span data-ttu-id="39f3e-120">Etapa 1: Preparar Olá VHD</span><span class="sxs-lookup"><span data-stu-id="39f3e-120">Step 1: Prep hello VHD</span></span>
<span data-ttu-id="39f3e-121">Antes de carregar Olá VHD tooAzure, ele precisa toobe generalizado usando a ferramenta Sysprep de saudação.</span><span class="sxs-lookup"><span data-stu-id="39f3e-121">Before you upload hello VHD tooAzure, it needs toobe generalized by using hello Sysprep tool.</span></span> <span data-ttu-id="39f3e-122">Isso prepara Olá toobe VHD usado como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="39f3e-122">This prepares hello VHD toobe used as an image.</span></span> <span data-ttu-id="39f3e-123">Para obter detalhes sobre o Sysprep, consulte [como tooUse Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="39f3e-123">For details about Sysprep, see [How tooUse Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="39f3e-124">Faça backup Olá VM antes de executar o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="39f3e-124">Back up hello VM before running Sysprep.</span></span>

<span data-ttu-id="39f3e-125">De máquina virtual Olá Olá o sistema operacional foi instalada para concluir a saudação procedimento a seguir:</span><span class="sxs-lookup"><span data-stu-id="39f3e-125">From hello virtual machine that hello operating system was installed to, complete hello following procedure:</span></span>

1. <span data-ttu-id="39f3e-126">Faça logon no sistema de operacional toohello.</span><span class="sxs-lookup"><span data-stu-id="39f3e-126">Sign in toohello operating system.</span></span>
2. <span data-ttu-id="39f3e-127">Abra uma janela de prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="39f3e-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="39f3e-128">Altere o diretório de saudação muito**%windir%\system32\sysprep**e, em seguida, execute `sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="39f3e-128">Change hello directory too**%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![Abrir una janela de Prompt de comando](./media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="39f3e-130">Olá **ferramenta de preparação do sistema** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="39f3e-130">hello **System Preparation Tool** dialog box appears.</span></span>

   ![Inicie o Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="39f3e-132">Em Olá **ferramenta de preparação do sistema**, selecione **digite sistema de OOBE (configuração)** e certifique-se de que **generalizar** é verificada.</span><span class="sxs-lookup"><span data-stu-id="39f3e-132">In hello **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="39f3e-133">Em **Opções de Desligamento**, selecione **Desligar**.</span><span class="sxs-lookup"><span data-stu-id="39f3e-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="39f3e-134">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="39f3e-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="39f3e-135">Etapa 2: criar uma conta de armazenamento e um contêiner</span><span class="sxs-lookup"><span data-stu-id="39f3e-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="39f3e-136">Você precisa de uma conta de armazenamento no Azure para que você tenha um arquivo. vhd do local tooupload hello.</span><span class="sxs-lookup"><span data-stu-id="39f3e-136">You need a storage account in Azure so you have a place tooupload hello .vhd file.</span></span> <span data-ttu-id="39f3e-137">Esta etapa mostra como toocreate uma conta ou get hello informações você precisa de uma conta existente.</span><span class="sxs-lookup"><span data-stu-id="39f3e-137">This step shows you how toocreate an account, or get hello info you need from an existing account.</span></span> <span data-ttu-id="39f3e-138">Substituir variáveis de saudação em &lsaquo; colchetes &rsaquo; com suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="39f3e-138">Replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="39f3e-139">Logon</span><span class="sxs-lookup"><span data-stu-id="39f3e-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="39f3e-140">Defina sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="39f3e-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="39f3e-141">Criar uma nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="39f3e-141">Create a new storage account.</span></span> <span data-ttu-id="39f3e-142">nome de Olá Olá da conta de armazenamento deve ser exclusivo, 3 a 24 caracteres.</span><span class="sxs-lookup"><span data-stu-id="39f3e-142">hello name of hello storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="39f3e-143">nome da saudação pode ser qualquer combinação de letras e números.</span><span class="sxs-lookup"><span data-stu-id="39f3e-143">hello name can be any combination of letters and numbers.</span></span> <span data-ttu-id="39f3e-144">Você também precisa toospecify um local como "Leste nós"</span><span class="sxs-lookup"><span data-stu-id="39f3e-144">You also need toospecify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="39f3e-145">Definir a nova conta de armazenamento hello como padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="39f3e-145">Set hello new storage account as hello default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="39f3e-146">Criar um novo contêiner.</span><span class="sxs-lookup"><span data-stu-id="39f3e-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-hello-vhd-file"></a><span data-ttu-id="39f3e-147">Etapa 3: Carregar o arquivo. vhd de saudação</span><span class="sxs-lookup"><span data-stu-id="39f3e-147">Step 3: Upload hello .vhd file</span></span>
<span data-ttu-id="39f3e-148">Saudação de uso [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) Olá tooupload VHD.</span><span class="sxs-lookup"><span data-stu-id="39f3e-148">Use hello [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) tooupload hello VHD.</span></span>

<span data-ttu-id="39f3e-149">Na janela do PowerShell do Azure de Olá usado na etapa anterior hello, tipo hello comando a seguir e substitua variáveis Olá em &lsaquo; colchetes &rsaquo; com suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="39f3e-149">From hello Azure PowerShell window you used in hello previous step, type hello following command and replace hello variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-hello-image-tooyour-list-of-custom-images"></a><span data-ttu-id="39f3e-150">Etapa 4: Adicionar lista de tooyour de imagem de saudação de imagens personalizadas</span><span class="sxs-lookup"><span data-stu-id="39f3e-150">Step 4: Add hello image tooyour list of custom images</span></span>
<span data-ttu-id="39f3e-151">Saudação de uso [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) lista de toohello de imagem do cmdlet tooadd Olá de imagens personalizadas.</span><span class="sxs-lookup"><span data-stu-id="39f3e-151">Use hello [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet tooadd hello image toohello list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="39f3e-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="39f3e-152">Next steps</span></span>
<span data-ttu-id="39f3e-153">Agora você pode [criar uma máquina virtual personalizada](createportal.md) usando Olá imagem que você carregou.</span><span class="sxs-lookup"><span data-stu-id="39f3e-153">You can now [create a custom VM](createportal.md) using hello image you uploaded.</span></span>
