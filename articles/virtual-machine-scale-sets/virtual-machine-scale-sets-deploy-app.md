---
title: "Implantar um aplicativo em conjuntos de escala de máquina virtual"
description: "Use as extensões para implantar um aplicativo nos Conjuntos de Dimensionamento de Máquinas Virtuais do Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f8892199-f2e2-4b82-988a-28ca8a7fd1eb
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/26/2017
ms.author: adegeo
ms.openlocfilehash: fa7d9d3bef4cb326844ede76171e8c566e87116b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="b6031-103">Implantar o aplicativo em conjuntos de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="b6031-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="b6031-104">Este artigo descreve diferentes maneiras de instalar software no momento em que o conjunto de dimensionamento é provisionado.</span><span class="sxs-lookup"><span data-stu-id="b6031-104">This article describes different ways of how to install software at the time the scale set is provisioned.</span></span>

<span data-ttu-id="b6031-105">Pode ser necessário revisar o artigo [Visão geral do design do conjunto de dimensionamento](virtual-machine-scale-sets-design-overview.md), o qual descreve alguns dos limites impostos pelos conjuntos de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="b6031-105">You may want to review the [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of the limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="b6031-106">Capturar e reutilizar uma imagem</span><span class="sxs-lookup"><span data-stu-id="b6031-106">Capture and reuse an image</span></span>

<span data-ttu-id="b6031-107">É possível utilizar uma máquina virtual que você tem no Azure para preparar uma imagem base para o conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b6031-107">You can use a virtual machine you have in Azure to prepare a base-image for your scale set.</span></span> <span data-ttu-id="b6031-108">Esse processo cria um disco gerenciado na sua conta de armazenamento, o qual é possível referenciar como a imagem base para o conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b6031-108">This process creates a managed disk in your storage account, which you can reference as the base image for your scale set.</span></span> 

<span data-ttu-id="b6031-109">Execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="b6031-109">Do the following steps:</span></span>

1. <span data-ttu-id="b6031-110">Crie uma Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="b6031-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="b6031-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="b6031-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="b6031-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="b6031-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="b6031-113">Acesse remotamente a máquina virtual e personalize o sistema de acordo com seu interesse.</span><span class="sxs-lookup"><span data-stu-id="b6031-113">Remote into the virtual machine and customize the system to your liking.</span></span>

   <span data-ttu-id="b6031-114">Se você quiser, é possível instalar o aplicativo agora.</span><span class="sxs-lookup"><span data-stu-id="b6031-114">If you want, you can install your application now.</span></span> <span data-ttu-id="b6031-115">No entanto, saiba que ao instalar o aplicativo agora, a atualização do seu aplicativo poderá ficar mais complicada porque talvez seja necessário removê-lo primeiro.</span><span class="sxs-lookup"><span data-stu-id="b6031-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need to remove it first.</span></span> <span data-ttu-id="b6031-116">Em vez disso, é possível utilizar esta etapa para instalar quaisquer pré-requisitos que possam ser necessários ao aplicativo, como um tempo de execução específico ou recurso do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="b6031-116">Instead, you can use this step to install any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="b6031-117">Siga o tutorial "capturar uma máquina" tanto para [Linux][linux-vm-capture] como para [Windows][windows-vm-capture].</span><span class="sxs-lookup"><span data-stu-id="b6031-117">Follow the "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="b6031-118">Crie um [Conjunto de Dimensionamento de Máquinas Virtuais][vmss-create] com o URI de imagem capturado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="b6031-118">Create a [Virtual Machine Scale Set][vmss-create] with the image URI you captured in the previous step.</span></span>

<span data-ttu-id="b6031-119">Para obter mais informações, consulte [Visão geral do Managed Disks](../virtual-machines/windows/managed-disks-overview.md) e [Utilizar discos de dados anexados](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="b6031-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-the-scale-set-is-provisioned"></a><span data-ttu-id="b6031-120">Instalar quando o conjunto de dimensionamento é provisionado</span><span class="sxs-lookup"><span data-stu-id="b6031-120">Install when the scale set is provisioned</span></span>

<span data-ttu-id="b6031-121">As extensões da máquina virtual podem ser aplicadas a um conjunto de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="b6031-121">Virtual machine extensions can be applied to a virtual machine scale set.</span></span> <span data-ttu-id="b6031-122">Com uma extensão da máquina virtual, é possível personalizar as máquinas virtuais em um conjunto de dimensionamento como um grupo inteiro.</span><span class="sxs-lookup"><span data-stu-id="b6031-122">With a virtual machine extension, you can customize the virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="b6031-123">Para obter mais informações, consulte [Extensões da máquina virtual](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="b6031-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="b6031-124">Há três extensões principais que podem ser utilizadas, dependendo se o sistema operacional é baseado no Linux ou baseado no Windows.</span><span class="sxs-lookup"><span data-stu-id="b6031-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="b6031-125">Windows</span><span class="sxs-lookup"><span data-stu-id="b6031-125">Windows</span></span>

<span data-ttu-id="b6031-126">Para um sistema operacional baseado no Windows, utilize a extensão de **Script personalizado v1.8** ou a extensão **DSC do PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b6031-126">For a Windows-based operating system, use either the **Custom Script v1.8** extension, or the **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="b6031-127">Custom Script</span><span class="sxs-lookup"><span data-stu-id="b6031-127">Custom Script</span></span>

<span data-ttu-id="b6031-128">A extensão de script personalizado executa um script em cada instância da máquina virtual no conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b6031-128">The Custom Script extension runs a script on each virtual machine instance in the scale set.</span></span> <span data-ttu-id="b6031-129">Um arquivo de configuração ou variável indica quais arquivos são baixados para a máquina virtual e, em seguida, o comando é executado.</span><span class="sxs-lookup"><span data-stu-id="b6031-129">A config file or variable indicates which files are downloaded to the virtual machine, and then what command runs.</span></span> <span data-ttu-id="b6031-130">Você pode usar isso para executar um instalador, um script, um arquivo em lotes, quaisquer executáveis, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="b6031-130">You could use this to run an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="b6031-131">O PowerShell utiliza uma tabela de hash para as configurações.</span><span class="sxs-lookup"><span data-stu-id="b6031-131">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="b6031-132">Esse exemplo configura a extensão de script personalizado para executar um script do PowerShell que instala o IIS.</span><span class="sxs-lookup"><span data-stu-id="b6031-132">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="b6031-133">Utilize a opção `-ProtectedSetting` para as configurações que podem conter informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="b6031-133">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="b6031-134">A CLI do Azure utiliza um arquivo json para as configurações.</span><span class="sxs-lookup"><span data-stu-id="b6031-134">Azure CLI uses a json file for the settings.</span></span> <span data-ttu-id="b6031-135">Esse exemplo configura a extensão de script personalizado para executar um script do PowerShell que instala o IIS.</span><span class="sxs-lookup"><span data-stu-id="b6031-135">This example configures the custom script extension to run a PowerShell script that installs IIS.</span></span> <span data-ttu-id="b6031-136">Salve o arquivo json a seguir como _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="b6031-136">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="b6031-137">Em seguida, execute esse comando da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6031-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="b6031-138">Utilize a opção `--protected-settings` para as configurações que podem conter informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="b6031-138">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="b6031-139">DSC do PowerShell</span><span class="sxs-lookup"><span data-stu-id="b6031-139">PowerShell DSC</span></span>

<span data-ttu-id="b6031-140">Você pode utilizar DSC do PowerShell para personalizar as instâncias das VMs do conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b6031-140">You can use PowerShell DSC to customize the scale set vm instances.</span></span> <span data-ttu-id="b6031-141">A extensão **DSC** publicada pelo **Microsoft.Powershell** implanta e executa a configuração DSC fornecida em cada instância da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="b6031-141">The **DSC** extension published by **Microsoft.Powershell** deploys and runs the provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="b6031-142">Um arquivo de configuração ou variável informa a extensão onde o pacote *.zip* está e qual a combinação _script-function_ a executar.</span><span class="sxs-lookup"><span data-stu-id="b6031-142">A config file or variable tells the extension where *.zip* package is, and which _script-function_ combination to run.</span></span>

<span data-ttu-id="b6031-143">O PowerShell utiliza uma tabela de hash para as configurações.</span><span class="sxs-lookup"><span data-stu-id="b6031-143">PowerShell uses a hashtable for the settings.</span></span> <span data-ttu-id="b6031-144">Esse exemplo implanta um pacote de DSC que instala o IIS.</span><span class="sxs-lookup"><span data-stu-id="b6031-144">This example deploys a DSC package that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$dscConfig = @{
  "wmfVersion" = "latest";
  "configuration" = @{
    "url" = "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip";
    "script" = "configure-http.ps1";
    "function" = "WebsiteTest";
  };
}

# Add the extension to the config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send the new config to Azure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="b6031-145">Utilize a opção `-ProtectedSetting` para as configurações que podem conter informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="b6031-145">Use the `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="b6031-146">A CLI do Azure utiliza um json para as configurações.</span><span class="sxs-lookup"><span data-stu-id="b6031-146">Azure CLI uses a json for the settings.</span></span> <span data-ttu-id="b6031-147">Esse exemplo implanta um pacote de DSC que instala o IIS.</span><span class="sxs-lookup"><span data-stu-id="b6031-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="b6031-148">Salve o arquivo json a seguir como _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="b6031-148">Save the following json file as _settings.json_.</span></span>

```json
{
  "wmfVersion": "latest",
  "configuration": {
    "url": "https://github.com/MicrosoftDocs/azure-cloud-services-files/raw/temp/dsc.zip",
    "script": "configure-http.ps1",
    "function": "WebsiteTest"
  }
}
```

<span data-ttu-id="b6031-149">Em seguida, execute esse comando da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6031-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="b6031-150">Utilize a opção `--protected-settings` para as configurações que podem conter informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="b6031-150">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="b6031-151">Linux</span><span class="sxs-lookup"><span data-stu-id="b6031-151">Linux</span></span>

<span data-ttu-id="b6031-152">O Linux pode utilizar a extensão de **Script personalizado v2.0** ou usar a **inicialização de nuvem** durante a criação.</span><span class="sxs-lookup"><span data-stu-id="b6031-152">Linux can use either the **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="b6031-153">O script personalizado é uma extensão simples que baixa arquivos para as instâncias da máquina virtual e executa um comando.</span><span class="sxs-lookup"><span data-stu-id="b6031-153">Custom script is a simple extension that downloads files to the virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="b6031-154">Custom Script</span><span class="sxs-lookup"><span data-stu-id="b6031-154">Custom Script</span></span>

<span data-ttu-id="b6031-155">Salve o arquivo json a seguir como _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="b6031-155">Save the following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="b6031-156">Utilize a CLI do Azure para adicionar essa extensão a um conjunto de dimensionamento de máquinas virtuais existentes.</span><span class="sxs-lookup"><span data-stu-id="b6031-156">Use the Azure CLI to add this extension to an existing virtual machine scale set.</span></span> <span data-ttu-id="b6031-157">Cada máquina virtual no conjunto de dimensionamento executa automaticamente a extensão.</span><span class="sxs-lookup"><span data-stu-id="b6031-157">Each virtual machine in the scale set automatically runs the extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="b6031-158">Utilize a opção `--protected-settings` para as configurações que podem conter informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="b6031-158">Use the `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="b6031-159">Inicialização de nuvem</span><span class="sxs-lookup"><span data-stu-id="b6031-159">Cloud-Init</span></span>

<span data-ttu-id="b6031-160">A inicialização de nuvem é utilizada quando o conjunto de dimensionamento é criado.</span><span class="sxs-lookup"><span data-stu-id="b6031-160">Cloud-Init is used when the scale set is created.</span></span> <span data-ttu-id="b6031-161">Primeiro, crie um arquivo local chamado _cloud-init.txt_ e adicione sua configuração a esse aquivo.</span><span class="sxs-lookup"><span data-stu-id="b6031-161">First, create a local file named _cloud-init.txt_ and add your configuration to it.</span></span> <span data-ttu-id="b6031-162">Por exemplo, consulte [essas linhas gerais](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span><span class="sxs-lookup"><span data-stu-id="b6031-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="b6031-163">Utilize a CLI do Azure para criar um conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b6031-163">Use the Azure CLI to create a scale set.</span></span> <span data-ttu-id="b6031-164">O `--custom-data` campo aceita o nome de arquivo de um script de inicialização de nuvem.</span><span class="sxs-lookup"><span data-stu-id="b6031-164">The `--custom-data` field accepts the file name of a cloud-init script.</span></span>

```azurecli
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="b6031-165">Como gerenciar atualizações de aplicativos?</span><span class="sxs-lookup"><span data-stu-id="b6031-165">How do I manage application updates?</span></span>

<span data-ttu-id="b6031-166">Se o aplicativo foi implantado através de uma extensão, altere a definição da extensão de alguma forma.</span><span class="sxs-lookup"><span data-stu-id="b6031-166">If you deployed your application through an extension, alter the extension definition in some way.</span></span> <span data-ttu-id="b6031-167">Essa alteração faz com que a extensão seja reimplantada a todas as instâncias das máquina virtuais.</span><span class="sxs-lookup"><span data-stu-id="b6031-167">This change causes the extension to be redeployed to all virtual machine instances.</span></span> <span data-ttu-id="b6031-168">Algo **deverá** ser alterado sobre a extensão, como renomear um arquivo referenciado, caso contrário, o Azure não reconhecerá que a extensão foi alterada.</span><span class="sxs-lookup"><span data-stu-id="b6031-168">Something **must** be changed about the extension, such as renaming a referenced file, otherwise, Azure does not see that the extension has changed.</span></span>

<span data-ttu-id="b6031-169">Se o aplicativo foi incorporado em sua própria imagem do sistema operacional, utilize uma pipeline de implantação automatizada para atualizações do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b6031-169">If you baked the application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="b6031-170">Projete sua arquitetura para facilitar a troca rápida de um conjunto de dimensionamento em etapas na produção.</span><span class="sxs-lookup"><span data-stu-id="b6031-170">Design your architecture to facilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="b6031-171">Um bom exemplo dessa abordagem é o [trabalho de driver do Azure Spinnaker](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span><span class="sxs-lookup"><span data-stu-id="b6031-171">A good example of this approach is the [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="b6031-172">[Packer](https://www.packer.io/) e [Terraform](https://www.terraform.io/) suportam o Azure Resource Manager para que seja possível definir suas imagens "como código" e compilá-las no Azure, então, utilize o VHD no seu conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b6031-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use the VHD in your scale set.</span></span> <span data-ttu-id="b6031-173">No entanto, isso seria problemático para imagens do marketplace, nas quais extensões/scripts personalizados se tornam mais importantes, já que você não manipula diretamente os bits do marketplace.</span><span class="sxs-lookup"><span data-stu-id="b6031-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="b6031-174">O que acontece quando um conjunto de dimensionamento é escalado horizontalmente?</span><span class="sxs-lookup"><span data-stu-id="b6031-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="b6031-175">Quando você adiciona uma ou mais máquinas virtuais a um conjunto de dimensionamento, o aplicativo é instalado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="b6031-175">When you add one or more virtual machines to a scale set, the application is automatically installed.</span></span> <span data-ttu-id="b6031-176">Por exemplo, se o conjunto de dimensionamento tiver extensões definidas, elas serão executadas em uma nova máquina virtual sempre que for criada.</span><span class="sxs-lookup"><span data-stu-id="b6031-176">For example if the scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="b6031-177">Se o conjunto de dimensionamento for baseado em uma imagem personalizada, qualquer nova máquina virtual será uma cópia da imagem personalizada de origem.</span><span class="sxs-lookup"><span data-stu-id="b6031-177">If the scale set is based on a custom image, any new virtual machine is a copy of the source custom image.</span></span> <span data-ttu-id="b6031-178">Se as máquinas virtuais do conjunto de dimensionamento forem hosts de contêineres, então, será possível ter o código de inicialização para carregar os contêineres em uma extensão de script personalizada.</span><span class="sxs-lookup"><span data-stu-id="b6031-178">If the scale set virtual machines are container hosts, then you might have startup code to load the containers in a Custom Script Extension.</span></span> <span data-ttu-id="b6031-179">Ou, uma extensão poderá instalar um agente que se registre com um orquestrador de cluster, como o Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="b6031-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="b6031-180">Como você implementa uma atualização de SO em domínios de atualização?</span><span class="sxs-lookup"><span data-stu-id="b6031-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="b6031-181">Suponha que você deseja atualizar a imagem do seu SO enquanto mantém o conjunto de dimensionamento de máquinas virtuais em execução.</span><span class="sxs-lookup"><span data-stu-id="b6031-181">Suppose you want to update your OS image while keeping the virtual machine scale set running.</span></span> <span data-ttu-id="b6031-182">O PowerShell e a CLI do Azure podem atualizar as imagens da máquina virtual, uma máquina virtual de cada vez.</span><span class="sxs-lookup"><span data-stu-id="b6031-182">PowerShell and the Azure CLI can update the virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="b6031-183">O artigo [Atualizar um conjunto de dimensionamento de máquinas virtuais](./virtual-machine-scale-sets-upgrade-scale-set.md) também fornece mais informações sobre quais opções estão disponíveis para executar uma atualização do sistema operacional através de um conjunto de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="b6031-183">The [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available to perform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b6031-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b6031-184">Next steps</span></span>

* [<span data-ttu-id="b6031-185">Utilizar o PowerShell para gerenciar seu conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b6031-185">Use PowerShell to manage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="b6031-186">Criar um modelo de conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="b6031-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

