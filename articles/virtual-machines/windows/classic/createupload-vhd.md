---
title: Criar e carregar uma imagem de VM usando o PowerShell | Microsoft Docs
description: "Saiba como criar e carregar uma imagem do Windows Server generalizada usando o modelo de implantação clássico e o Azure PowerShell."
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
ms.openlocfilehash: bc75c8cdd98b0ea0fbff6483c0e3c9d4468d3941
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-upload-a-windows-server-vhd-to-azure"></a><span data-ttu-id="d9e26-103">Criar e carregar um VHD do Windows Server no Azure</span><span class="sxs-lookup"><span data-stu-id="d9e26-103">Create and upload a Windows Server VHD to Azure</span></span>
<span data-ttu-id="d9e26-104">Esse artigo mostra como carregar sua própria imagem de VM generalizada como um VHD (disco rígido virtual) para que o use para criar outras máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="d9e26-104">This article shows you how to upload your own generalized VM image as a virtual hard disk (VHD) so you can use it to create virtual machines.</span></span> <span data-ttu-id="d9e26-105">Para mais detalhes sobre discos e os VHDs no Microsoft Azure, confira a seção [Sobre discos e VHDs para Máquinas Virtuais](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d9e26-105">For more details about disks and VHDs in Microsoft Azure, see [About Disks and VHDs for Virtual Machines](../about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d9e26-106">O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="d9e26-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="d9e26-107">Este artigo aborda o uso do modelo de implantação Clássica.</span><span class="sxs-lookup"><span data-stu-id="d9e26-107">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="d9e26-108">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="d9e26-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="d9e26-109">Você também pode [carregar](../upload-generalized-managed.md) uma máquina virtual usando o modelo do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d9e26-109">You can also [upload](../upload-generalized-managed.md) a virtual machine using the Resource Manager model.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d9e26-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="d9e26-110">Prerequisites</span></span>
<span data-ttu-id="d9e26-111">Este artigo supõe que você tem:</span><span class="sxs-lookup"><span data-stu-id="d9e26-111">This article assumes you have:</span></span>

* <span data-ttu-id="d9e26-112">**Uma assinatura do Azure** - se não tiver uma, você poderá [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span><span class="sxs-lookup"><span data-stu-id="d9e26-112">**An Azure subscription** - If you don't have one, you can [open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>
* <span data-ttu-id="d9e26-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** – você tem o módulo do Microsoft Azure PowerShell instalado e configurado para usar sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="d9e26-113">**[Microsoft Azure PowerShell](/powershell/azure/overview)** - You have the Microsoft Azure PowerShell module installed and configured to use your subscription.</span></span>
* <span data-ttu-id="d9e26-114">**Um arquivo .VHD** - sistema operacional Windows para o qual há suporte, armazenado em um arquivo .vhd e anexado a uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="d9e26-114">**A .VHD file** - supported Windows operating system stored in a .vhd file and attached to a virtual machine.</span></span> <span data-ttu-id="d9e26-115">Verifique se há suporte para as funções de servidor em execução no VHD no Sysprep.</span><span class="sxs-lookup"><span data-stu-id="d9e26-115">Check to see if the server roles running on the VHD are supported by Sysprep.</span></span> <span data-ttu-id="d9e26-116">Para obter mais informações, consulte [Suporte do Sysprep para funções de servidor](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span><span class="sxs-lookup"><span data-stu-id="d9e26-116">For more information, see [Sysprep Support for Server Roles](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d9e26-117">Não há suporte para o formato VHDX no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d9e26-117">The VHDX format is not supported in Microsoft Azure.</span></span> <span data-ttu-id="d9e26-118">Você pode converter o disco em formato VHD usando o Gerenciador do Hyper-V ou o [cmdlet convert-vhd](http://technet.microsoft.com/library/hh848454.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9e26-118">You can convert the disk to VHD format using Hyper-V Manager or the [Convert-VHD cmdlet](http://technet.microsoft.com/library/hh848454.aspx).</span></span> <span data-ttu-id="d9e26-119">Consulte esta [publicação de blog](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx)para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="d9e26-119">For details, see this [blogpost](http://blogs.msdn.com/b/virtual_pc_guy/archive/2012/10/03/using-powershell-to-convert-a-vhd-to-a-vhdx.aspx).</span></span>

## <a name="step-1-prep-the-vhd"></a><span data-ttu-id="d9e26-120">Etapa 1: preparar o VHD</span><span class="sxs-lookup"><span data-stu-id="d9e26-120">Step 1: Prep the VHD</span></span>
<span data-ttu-id="d9e26-121">Antes de carregar o VHD no Azure, ele precisa ser generalizado usando a ferramenta Sysprep.</span><span class="sxs-lookup"><span data-stu-id="d9e26-121">Before you upload the VHD to Azure, it needs to be generalized by using the Sysprep tool.</span></span> <span data-ttu-id="d9e26-122">Ela prepara o VHD a ser usado como uma imagem.</span><span class="sxs-lookup"><span data-stu-id="d9e26-122">This prepares the VHD to be used as an image.</span></span> <span data-ttu-id="d9e26-123">Para obter detalhes sobre o Sysprep, consulte [Como usar o Sysprep: uma introdução](http://technet.microsoft.com/library/bb457073.aspx).</span><span class="sxs-lookup"><span data-stu-id="d9e26-123">For details about Sysprep, see [How to Use Sysprep: An Introduction](http://technet.microsoft.com/library/bb457073.aspx).</span></span> <span data-ttu-id="d9e26-124">Faça backup da VM antes de executar o Sysprep.</span><span class="sxs-lookup"><span data-stu-id="d9e26-124">Back up the VM before running Sysprep.</span></span>

<span data-ttu-id="d9e26-125">Na máquina virtual na qual o sistema operacional foi instalado, conclua o procedimento a seguir:</span><span class="sxs-lookup"><span data-stu-id="d9e26-125">From the virtual machine that the operating system was installed to, complete the following procedure:</span></span>

1. <span data-ttu-id="d9e26-126">Entre no sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="d9e26-126">Sign in to the operating system.</span></span>
2. <span data-ttu-id="d9e26-127">Abra uma janela de prompt de comando como administrador.</span><span class="sxs-lookup"><span data-stu-id="d9e26-127">Open a command prompt window as an administrator.</span></span> <span data-ttu-id="d9e26-128">Altere o diretório para **%windir%\system32\sysprep** e, a seguir, execute`sysprep.exe`.</span><span class="sxs-lookup"><span data-stu-id="d9e26-128">Change the directory to **%windir%\system32\sysprep**, and then run `sysprep.exe`.</span></span>

    ![Abrir una janela de Prompt de comando](./media/createupload-vhd/sysprep_commandprompt.png)
3. <span data-ttu-id="d9e26-130">A caixa de diálogo **Ferramenta de Preparação do Sistema** é aberta.</span><span class="sxs-lookup"><span data-stu-id="d9e26-130">The **System Preparation Tool** dialog box appears.</span></span>

   ![Inicie o Sysprep](./media/createupload-vhd/sysprepgeneral.png)
4. <span data-ttu-id="d9e26-132">Em **Ferramenta de Preparação do Sistema**, selecione **Entrar no Sistema OOBE (Configuração inicial pelo usuário)** e verifique se a opção **Generalizar** está marcada.</span><span class="sxs-lookup"><span data-stu-id="d9e26-132">In the **System Preparation Tool**, select **Enter System Out of Box Experience (OOBE)** and make sure that **Generalize** is checked.</span></span>
5. <span data-ttu-id="d9e26-133">Em **Opções de Desligamento**, selecione **Desligar**.</span><span class="sxs-lookup"><span data-stu-id="d9e26-133">In **Shutdown Options**, select **Shutdown**.</span></span>
6. <span data-ttu-id="d9e26-134">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="d9e26-134">Click **OK**.</span></span>

## <a name="step-2-create-a-storage-account-and-a-container"></a><span data-ttu-id="d9e26-135">Etapa 2: criar uma conta de armazenamento e um contêiner</span><span class="sxs-lookup"><span data-stu-id="d9e26-135">Step 2: Create a storage account and a container</span></span>
<span data-ttu-id="d9e26-136">Você precisa de uma conta de armazenamento no Azure para que você tenha um local para carregar o arquivo .vhd.</span><span class="sxs-lookup"><span data-stu-id="d9e26-136">You need a storage account in Azure so you have a place to upload the .vhd file.</span></span> <span data-ttu-id="d9e26-137">Esta etapa mostra como criar uma conta, ou obter as informações de que você precisa de uma conta existente.</span><span class="sxs-lookup"><span data-stu-id="d9e26-137">This step shows you how to create an account, or get the info you need from an existing account.</span></span> <span data-ttu-id="d9e26-138">Substitua as variáveis entre &lsaquo; colchetes &rsaquo; com suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="d9e26-138">Replace the variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

1. <span data-ttu-id="d9e26-139">Logon</span><span class="sxs-lookup"><span data-stu-id="d9e26-139">Login</span></span>

    ```powershell
    Add-AzureAccount
    ```

2. <span data-ttu-id="d9e26-140">Defina sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="d9e26-140">Set your Azure subscription.</span></span>

    ```powershell
    Select-AzureSubscription -SubscriptionName <SubscriptionName>
    ```

3. <span data-ttu-id="d9e26-141">Criar uma nova conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="d9e26-141">Create a new storage account.</span></span> <span data-ttu-id="d9e26-142">O nome da conta de armazenamento deve ser exclusivo, contendo 3 a 24 caracteres.</span><span class="sxs-lookup"><span data-stu-id="d9e26-142">The name of the storage account should be unique, 3-24 characters.</span></span> <span data-ttu-id="d9e26-143">O nome pode ser qualquer combinação de letras e números.</span><span class="sxs-lookup"><span data-stu-id="d9e26-143">The name can be any combination of letters and numbers.</span></span> <span data-ttu-id="d9e26-144">Você também precisará especificar uma localização, como "Leste dos EUA"</span><span class="sxs-lookup"><span data-stu-id="d9e26-144">You also need to specify a location like "East US"</span></span>

    ```powershell
    New-AzureStorageAccount –StorageAccountName <StorageAccountName> -Location <Location>
    ```

4. <span data-ttu-id="d9e26-145">Defina a nova conta de armazenamento como a padrão.</span><span class="sxs-lookup"><span data-stu-id="d9e26-145">Set the new storage account as the default.</span></span>

    ```powershell
    Set-AzureSubscription -CurrentStorageAccountName <StorageAccountName> -SubscriptionName <SubscriptionName>
    ```

5. <span data-ttu-id="d9e26-146">Criar um novo contêiner.</span><span class="sxs-lookup"><span data-stu-id="d9e26-146">Create a new container.</span></span>

    ```powershell
    New-AzureStorageContainer -Name <ContainerName> -Permission Off
    ```

## <a name="step-3-upload-the-vhd-file"></a><span data-ttu-id="d9e26-147">Etapa 3: Carregar o arquivo .vhd</span><span class="sxs-lookup"><span data-stu-id="d9e26-147">Step 3: Upload the .vhd file</span></span>
<span data-ttu-id="d9e26-148">Você usará o cmdlet [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) para carregar o VHD.</span><span class="sxs-lookup"><span data-stu-id="d9e26-148">Use the [Add-AzureVhd](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevhd) to upload the VHD.</span></span>

<span data-ttu-id="d9e26-149">Na janela do Azure PowerShell usada na etapa anterior, digite o comando a seguir e substitua as variáveis entre &lsaquo; colchetes &rsaquo; por suas próprias informações.</span><span class="sxs-lookup"><span data-stu-id="d9e26-149">From the Azure PowerShell window you used in the previous step, type the following command and replace the variables in &lsaquo; brackets &rsaquo; with your own information.</span></span>

```powershell
Add-AzureVhd -Destination "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -LocalFilePath <LocalPathtoVHDFile>
```

## <a name="step-4-add-the-image-to-your-list-of-custom-images"></a><span data-ttu-id="d9e26-150">Etapa 4: adicionar a imagem à sua lista de imagens personalizadas</span><span class="sxs-lookup"><span data-stu-id="d9e26-150">Step 4: Add the image to your list of custom images</span></span>
<span data-ttu-id="d9e26-151">Use o cmdlet [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) para adicionar a imagem à lista de suas imagens personalizadas.</span><span class="sxs-lookup"><span data-stu-id="d9e26-151">Use the [Add-AzureVMImage](https://docs.microsoft.com/en-us/powershell/module/azure/add-azurevmimage) cmdlet to add the image to the list of your custom images.</span></span>

```powershell
Add-AzureVMImage -ImageName <ImageName> -MediaLocation "https://<StorageAccountName>.blob.core.windows.net/<ContainerName>/<vhdName>.vhd" -OS "Windows"
```

## <a name="next-steps"></a><span data-ttu-id="d9e26-152">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d9e26-152">Next steps</span></span>
<span data-ttu-id="d9e26-153">Agora você pode [criar uma VM personalizada](createportal.md) usando a imagem carregada.</span><span class="sxs-lookup"><span data-stu-id="d9e26-153">You can now [create a custom VM](createportal.md) using the image you uploaded.</span></span>
