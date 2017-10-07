---
title: "Define aaaDeploy um aplicativo em escala de máquinas virtuais"
description: "Use extensões toodepoy um aplicativo em conjuntos de escala de máquina Virtual do Azure."
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
ms.openlocfilehash: 5f3988b9511d80370a8be1fc042c21fee212506e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-your-application-on-virtual-machine-scale-sets"></a><span data-ttu-id="40161-103">Implantar o aplicativo em conjuntos de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="40161-103">Deploy your application on virtual machine scale sets</span></span>

<span data-ttu-id="40161-104">Este artigo descreve as diferentes maneiras de como definir o software tooinstall escala de saudação do tempo de saudação é provisionado.</span><span class="sxs-lookup"><span data-stu-id="40161-104">This article describes different ways of how tooinstall software at hello time hello scale set is provisioned.</span></span>

<span data-ttu-id="40161-105">Talvez você queira Olá tooreview [visão geral do Design definir escala](virtual-machine-scale-sets-design-overview.md) artigo, que descreve alguns dos limites de saudação impostos por conjuntos de escala de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="40161-105">You may want tooreview hello [Scale Set Design Overview](virtual-machine-scale-sets-design-overview.md) article, which describes some of hello limits imposed by virtual machine scale sets.</span></span>

## <a name="capture-and-reuse-an-image"></a><span data-ttu-id="40161-106">Capturar e reutilizar uma imagem</span><span class="sxs-lookup"><span data-stu-id="40161-106">Capture and reuse an image</span></span>

<span data-ttu-id="40161-107">Você pode usar uma máquina virtual que no Azure tooprepare uma imagem de base para a escala configurou.</span><span class="sxs-lookup"><span data-stu-id="40161-107">You can use a virtual machine you have in Azure tooprepare a base-image for your scale set.</span></span> <span data-ttu-id="40161-108">Esse processo cria um disco gerenciado na sua conta de armazenamento, você pode fazer referência como imagem de base Olá para o conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="40161-108">This process creates a managed disk in your storage account, which you can reference as hello base image for your scale set.</span></span> 

<span data-ttu-id="40161-109">Olá seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="40161-109">Do hello following steps:</span></span>

1. <span data-ttu-id="40161-110">Crie uma Máquina Virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="40161-110">Create an Azure Virtual Machine</span></span>
   * <span data-ttu-id="40161-111">[Linux][linux-vm-create]</span><span class="sxs-lookup"><span data-stu-id="40161-111">[Linux][linux-vm-create]</span></span>
   * <span data-ttu-id="40161-112">[Windows][windows-vm-create]</span><span class="sxs-lookup"><span data-stu-id="40161-112">[Windows][windows-vm-create]</span></span>

2. <span data-ttu-id="40161-113">Remoto em Olá a máquina virtual e personalizar a preferência de tooyour sistema hello.</span><span class="sxs-lookup"><span data-stu-id="40161-113">Remote into hello virtual machine and customize hello system tooyour liking.</span></span>

   <span data-ttu-id="40161-114">Se você quiser, é possível instalar o aplicativo agora.</span><span class="sxs-lookup"><span data-stu-id="40161-114">If you want, you can install your application now.</span></span> <span data-ttu-id="40161-115">No entanto, saiba que ao instalar seu aplicativo agora, você pode fazer upgrade do seu aplicativo mais complicado porque talvez seja necessário tooremove-lo primeiro.</span><span class="sxs-lookup"><span data-stu-id="40161-115">However, know that by installing your application now, you may make upgrading your application more complicated because you may need tooremove it first.</span></span> <span data-ttu-id="40161-116">Em vez disso, você pode usar essa etapa tooinstall todos os pré-requisitos que seu aplicativo pode ser necessário, como um recurso de tempo de execução ou sistema operacional específico.</span><span class="sxs-lookup"><span data-stu-id="40161-116">Instead, you can use this step tooinstall any prerequisites your application may need, like a specific runtime or operating system feature.</span></span>

3. <span data-ttu-id="40161-117">Siga hello "capturar uma máquina" tutorial para o [Linux] [ linux-vm-capture] ou [Windows][windows-vm-capture].</span><span class="sxs-lookup"><span data-stu-id="40161-117">Follow hello "capture a machine" tutorial for either [Linux][linux-vm-capture] or [Windows][windows-vm-capture].</span></span>

4. <span data-ttu-id="40161-118">Criar um [conjunto de escala de máquinas virtuais] [ vmss-create] com hello capturados na etapa anterior de saudação do URI da imagem.</span><span class="sxs-lookup"><span data-stu-id="40161-118">Create a [Virtual Machine Scale Set][vmss-create] with hello image URI you captured in hello previous step.</span></span>

<span data-ttu-id="40161-119">Para obter mais informações, consulte [Visão geral do Managed Disks](../virtual-machines/windows/managed-disks-overview.md) e [Utilizar discos de dados anexados](virtual-machine-scale-sets-attached-disks.md).</span><span class="sxs-lookup"><span data-stu-id="40161-119">For more information about disks, see [Managed Disks Overview](../virtual-machines/windows/managed-disks-overview.md) and [Use Attached Data Disks](virtual-machine-scale-sets-attached-disks.md).</span></span>

## <a name="install-when-hello-scale-set-is-provisioned"></a><span data-ttu-id="40161-120">Instalar ao conjunto de escala de saudação é provisionado</span><span class="sxs-lookup"><span data-stu-id="40161-120">Install when hello scale set is provisioned</span></span>

<span data-ttu-id="40161-121">Extensões de máquinas virtuais podem ser aplicadas tooa conjunto de escalas da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="40161-121">Virtual machine extensions can be applied tooa virtual machine scale set.</span></span> <span data-ttu-id="40161-122">Com uma extensão de máquina virtual, você pode personalizar máquinas virtuais de saudação em uma escala definida como um grupo inteiro.</span><span class="sxs-lookup"><span data-stu-id="40161-122">With a virtual machine extension, you can customize hello virtual machines in a scale set as a whole group.</span></span> <span data-ttu-id="40161-123">Para obter mais informações, consulte [Extensões da máquina virtual](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40161-123">For more information about extensions, see [Virtual Machine Extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="40161-124">Há três extensões principais que podem ser utilizadas, dependendo se o sistema operacional é baseado no Linux ou baseado no Windows.</span><span class="sxs-lookup"><span data-stu-id="40161-124">There are three main extensions you can use, depending on if your operating system is Linux-based or Windows-based.</span></span>

### <a name="windows"></a><span data-ttu-id="40161-125">Windows</span><span class="sxs-lookup"><span data-stu-id="40161-125">Windows</span></span>

<span data-ttu-id="40161-126">Para um sistema operacional baseado no Windows, use o hello **v 1.8 de Script personalizado** extensão ou hello **PowerShell DSC** extensão.</span><span class="sxs-lookup"><span data-stu-id="40161-126">For a Windows-based operating system, use either hello **Custom Script v1.8** extension, or hello **PowerShell DSC** extension.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="40161-127">Custom Script</span><span class="sxs-lookup"><span data-stu-id="40161-127">Custom Script</span></span>

<span data-ttu-id="40161-128">saudação de extensão do Script personalizado executa um script em cada instância de máquina virtual no conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="40161-128">hello Custom Script extension runs a script on each virtual machine instance in hello scale set.</span></span> <span data-ttu-id="40161-129">Um arquivo de configuração ou variável indica quais arquivos são baixados toohello VM e, em seguida, o comando é executado.</span><span class="sxs-lookup"><span data-stu-id="40161-129">A config file or variable indicates which files are downloaded toohello virtual machine, and then what command runs.</span></span> <span data-ttu-id="40161-130">Você pode usar este toorun um instalador, um script, um arquivo em lotes, qualquer executável por exemplo.</span><span class="sxs-lookup"><span data-stu-id="40161-130">You could use this toorun an installer, a script, a batch file, any executable for example.</span></span>

<span data-ttu-id="40161-131">PowerShell usa uma tabela de hash para configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="40161-131">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="40161-132">Este exemplo configura Olá script personalizado extensão toorun um script do PowerShell que instala o IIS.</span><span class="sxs-lookup"><span data-stu-id="40161-132">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span>

```powershell
# Setup extension configuration hashtable variable
$customConfig = @{
  "fileUris" = @("https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1");
  "commandToExecute" = "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> `"%TEMP%\StartupLog.txt`" 2>&1";
};

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Compute -Type CustomScriptExtension -TypeHandlerVersion 1.8 -Name "customscript1" -Setting $customConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "MyVmssTest143"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="40161-133">Saudação de uso `-ProtectedSetting` alternar para as configurações que podem conter informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="40161-133">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

---------


<span data-ttu-id="40161-134">CLI do Azure usa um arquivo json para configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="40161-134">Azure CLI uses a json file for hello settings.</span></span> <span data-ttu-id="40161-135">Este exemplo configura Olá script personalizado extensão toorun um script do PowerShell que instala o IIS.</span><span class="sxs-lookup"><span data-stu-id="40161-135">This example configures hello custom script extension toorun a PowerShell script that installs IIS.</span></span> <span data-ttu-id="40161-136">Salvar Olá arquivo json como a seguir _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="40161-136">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/MicrosoftDocs/azure-cloud-services-files/temp/install-iis.ps1"
  ],
  "commandToExecute": "PowerShell -ExecutionPolicy Unrestricted .\install-iis.ps1 >> \"%TEMP%\StartupLog.txt\" 2>&1"
}
```

<span data-ttu-id="40161-137">Em seguida, execute esse comando da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="40161-137">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Compute --version 1.8 --name CustomScriptExtension --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="40161-138">Saudação de uso `--protected-settings` alternar para as configurações que podem conter informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="40161-138">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="powershell-dsc"></a><span data-ttu-id="40161-139">DSC do PowerShell</span><span class="sxs-lookup"><span data-stu-id="40161-139">PowerShell DSC</span></span>

<span data-ttu-id="40161-140">Você pode usar instâncias de vm do conjunto de escala do DSC do PowerShell toocustomize hello.</span><span class="sxs-lookup"><span data-stu-id="40161-140">You can use PowerShell DSC toocustomize hello scale set vm instances.</span></span> <span data-ttu-id="40161-141">Olá **DSC** extensão publicada por **PowerShell** implanta e executa a configuração de DSC Olá fornecido em cada instância de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="40161-141">hello **DSC** extension published by **Microsoft.Powershell** deploys and runs hello provided DSC configuration on each virtual machine instance.</span></span> <span data-ttu-id="40161-142">Um arquivo de configuração ou variável informa extensão Olá onde *. zip* pacote for e que _função script_ toorun de combinação.</span><span class="sxs-lookup"><span data-stu-id="40161-142">A config file or variable tells hello extension where *.zip* package is, and which _script-function_ combination toorun.</span></span>

<span data-ttu-id="40161-143">PowerShell usa uma tabela de hash para configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="40161-143">PowerShell uses a hashtable for hello settings.</span></span> <span data-ttu-id="40161-144">Esse exemplo implanta um pacote de DSC que instala o IIS.</span><span class="sxs-lookup"><span data-stu-id="40161-144">This example deploys a DSC package that installs IIS.</span></span>

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

# Add hello extension toohello config
Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmssConfig -Publisher Microsoft.Powershell -Type DSC -TypeHandlerVersion 2.24 -Name "dsc1" -Setting $dscConfig

# Send hello new config tooAzure
Update-AzureRmVmss -ResourceGroupName $rg -Name "myscaleset1"  -VirtualMachineScaleSet $vmssConfig
```

>[!IMPORTANT]
><span data-ttu-id="40161-145">Saudação de uso `-ProtectedSetting` alternar para as configurações que podem conter informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="40161-145">Use hello `-ProtectedSetting` switch for any settings that may contain sensitive information.</span></span>

-----------

<span data-ttu-id="40161-146">CLI do Azure usa json para configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="40161-146">Azure CLI uses a json for hello settings.</span></span> <span data-ttu-id="40161-147">Esse exemplo implanta um pacote de DSC que instala o IIS.</span><span class="sxs-lookup"><span data-stu-id="40161-147">This example deploys a DSC package that installs IIS.</span></span> <span data-ttu-id="40161-148">Salvar Olá arquivo json como a seguir _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="40161-148">Save hello following json file as _settings.json_.</span></span>

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

<span data-ttu-id="40161-149">Em seguida, execute esse comando da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="40161-149">Then, run this Azure CLI command.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Powershell --version 2.24 --name DSC --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="40161-150">Saudação de uso `--protected-settings` alternar para as configurações que podem conter informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="40161-150">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

### <a name="linux"></a><span data-ttu-id="40161-151">Linux</span><span class="sxs-lookup"><span data-stu-id="40161-151">Linux</span></span>

<span data-ttu-id="40161-152">Linux pode usar qualquer Olá **v 2.0 do Script personalizado** extensão ou use **init nuvem** durante a criação.</span><span class="sxs-lookup"><span data-stu-id="40161-152">Linux can use either hello **Custom Script v2.0** extension or use **cloud-init** during creation.</span></span>

<span data-ttu-id="40161-153">Script personalizado é uma extensão simple que instâncias de máquina virtual de toohello arquivos de baixa e executa um comando.</span><span class="sxs-lookup"><span data-stu-id="40161-153">Custom script is a simple extension that downloads files toohello virtual machine instances, and runs a command.</span></span>

#### <a name="custom-script"></a><span data-ttu-id="40161-154">Custom Script</span><span class="sxs-lookup"><span data-stu-id="40161-154">Custom Script</span></span>

<span data-ttu-id="40161-155">Salvar Olá arquivo json como a seguir _settings.json_.</span><span class="sxs-lookup"><span data-stu-id="40161-155">Save hello following json file as _settings.json_.</span></span>

```json
{
  "fileUris": [
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
    "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
  ],
  "commandToExecute": "bash installserver.sh"
}
```

<span data-ttu-id="40161-156">Use Olá CLI do Azure tooadd este tooan de extensão existente do conjunto de escalas da máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="40161-156">Use hello Azure CLI tooadd this extension tooan existing virtual machine scale set.</span></span> <span data-ttu-id="40161-157">Cada máquina virtual em escala Olá definidas automaticamente execuções Olá extensão.</span><span class="sxs-lookup"><span data-stu-id="40161-157">Each virtual machine in hello scale set automatically runs hello extension.</span></span>

```azurecli
az vmss extension set --publisher Microsoft.Azure.Extensions --version 2.0 --name CustomScript --resource-group myResourceGroup --vmss-name myScaleSet --settings @settings.json
```

>[!IMPORTANT]
><span data-ttu-id="40161-158">Saudação de uso `--protected-settings` alternar para as configurações que podem conter informações confidenciais.</span><span class="sxs-lookup"><span data-stu-id="40161-158">Use hello `--protected-settings` switch for any settings that may contain sensitive information.</span></span>

#### <a name="cloud-init"></a><span data-ttu-id="40161-159">Inicialização de nuvem</span><span class="sxs-lookup"><span data-stu-id="40161-159">Cloud-Init</span></span>

<span data-ttu-id="40161-160">Nuvem Init é usado quando o conjunto de escala Olá é criado.</span><span class="sxs-lookup"><span data-stu-id="40161-160">Cloud-Init is used when hello scale set is created.</span></span> <span data-ttu-id="40161-161">Primeiro, crie um arquivo local chamado _init.txt nuvem_ e adicione tooit sua configuração.</span><span class="sxs-lookup"><span data-stu-id="40161-161">First, create a local file named _cloud-init.txt_ and add your configuration tooit.</span></span> <span data-ttu-id="40161-162">Por exemplo, consulte [essas linhas gerais](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span><span class="sxs-lookup"><span data-stu-id="40161-162">For example, see [this gist](https://gist.github.com/Thraka/27bd66b1fb79e11904fb62b7de08a8a6#file-cloud-init-txt)</span></span>

<span data-ttu-id="40161-163">Olá Use CLI do Azure toocreate uma escala definida.</span><span class="sxs-lookup"><span data-stu-id="40161-163">Use hello Azure CLI toocreate a scale set.</span></span> <span data-ttu-id="40161-164">Olá `--custom-data` campo aceita o nome de arquivo hello de um script de inicialização de nuvem.</span><span class="sxs-lookup"><span data-stu-id="40161-164">hello `--custom-data` field accepts hello file name of a cloud-init script.</span></span>

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

## <a name="how-do-i-manage-application-updates"></a><span data-ttu-id="40161-165">Como gerenciar atualizações de aplicativos?</span><span class="sxs-lookup"><span data-stu-id="40161-165">How do I manage application updates?</span></span>

<span data-ttu-id="40161-166">Se você implantou seu aplicativo por meio de uma extensão, altere a definição de extensão de saudação de alguma forma.</span><span class="sxs-lookup"><span data-stu-id="40161-166">If you deployed your application through an extension, alter hello extension definition in some way.</span></span> <span data-ttu-id="40161-167">Essa alteração faz com que as instâncias de máquina virtual Olá extensão toobe reimplantado tooall.</span><span class="sxs-lookup"><span data-stu-id="40161-167">This change causes hello extension toobe redeployed tooall virtual machine instances.</span></span> <span data-ttu-id="40161-168">Algo **deve** alterado sobre extensão hello, como renomear um arquivo referenciado, caso contrário, faz do Azure não veja que Olá extensão foi alterada.</span><span class="sxs-lookup"><span data-stu-id="40161-168">Something **must** be changed about hello extension, such as renaming a referenced file, otherwise, Azure does not see that hello extension has changed.</span></span>

<span data-ttu-id="40161-169">Se você implantadas aplicativo hello na sua própria imagem do sistema operacional, use um pipeline de implantação automática para atualizações de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="40161-169">If you baked hello application into your own operating system image, use an automated deployment pipeline for application updates.</span></span> <span data-ttu-id="40161-170">Crie seu toofacilitate arquitetura rápida de troca de uma escala de preparada definido em produção.</span><span class="sxs-lookup"><span data-stu-id="40161-170">Design your architecture toofacilitate rapid swapping of a staged scale set into production.</span></span> <span data-ttu-id="40161-171">Um bom exemplo dessa abordagem é hello [trabalho do Azure Spinnaker driver](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span><span class="sxs-lookup"><span data-stu-id="40161-171">A good example of this approach is hello [Azure Spinnaker driver work](https://github.com/spinnaker/deck/tree/master/app/scripts/modules/azure) - [http://www.spinnaker.io/](http://www.spinnaker.io/).</span></span>

<span data-ttu-id="40161-172">[Packer](https://www.packer.io/) e [Terraform](https://www.terraform.io/) suporte do Azure Resource Manager, para que você também pode definir suas imagens "de código" e criá-las no Azure, em seguida, usar Olá VHD em seu conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="40161-172">[Packer](https://www.packer.io/) and [Terraform](https://www.terraform.io/) support Azure Resource Manager, so you can also define your images "as code" and build them in Azure, then use hello VHD in your scale set.</span></span> <span data-ttu-id="40161-173">No entanto, isso seria problemático para imagens do marketplace, nas quais extensões/scripts personalizados se tornam mais importantes, já que você não manipula diretamente os bits do marketplace.</span><span class="sxs-lookup"><span data-stu-id="40161-173">However, doing so would become problematic for marketplace images, where extensions/custom scripts become more important since you don’t directly manipulate bits from marketplace.</span></span>

## <a name="what-happens-when-a-scale-set-scales-out"></a><span data-ttu-id="40161-174">O que acontece quando um conjunto de dimensionamento é escalado horizontalmente?</span><span class="sxs-lookup"><span data-stu-id="40161-174">What happens when a scale set scales out?</span></span>
<span data-ttu-id="40161-175">Quando você adiciona um ou mais conjuntos de escala tooa de máquinas virtuais, o aplicativo hello é instalado automaticamente.</span><span class="sxs-lookup"><span data-stu-id="40161-175">When you add one or more virtual machines tooa scale set, hello application is automatically installed.</span></span> <span data-ttu-id="40161-176">Para exemplo se o conjunto de escala Olá tem extensões definidas, eles executados em uma nova máquina virtual sempre que ela é criada.</span><span class="sxs-lookup"><span data-stu-id="40161-176">For example if hello scale set has extensions defined, they run on a new virtual machine each time it is created.</span></span> <span data-ttu-id="40161-177">Se o conjunto de escala Olá baseia-se em uma imagem personalizada, qualquer nova máquina virtual é uma cópia da imagem personalizada do hello fonte.</span><span class="sxs-lookup"><span data-stu-id="40161-177">If hello scale set is based on a custom image, any new virtual machine is a copy of hello source custom image.</span></span> <span data-ttu-id="40161-178">Se Olá máquinas de virtuais de conjunto de escala são hosts de contêiner, você pode ter contêineres de saudação do tooload de código de inicialização em uma extensão de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="40161-178">If hello scale set virtual machines are container hosts, then you might have startup code tooload hello containers in a Custom Script Extension.</span></span> <span data-ttu-id="40161-179">Ou, uma extensão poderá instalar um agente que se registre com um orquestrador de cluster, como o Serviço de Contêiner do Azure.</span><span class="sxs-lookup"><span data-stu-id="40161-179">Or, an extension might install an agent that registers with a cluster orchestrator, such as Azure Container Service.</span></span>


## <a name="how-do-you-roll-out-an-os-update-across-update-domains"></a><span data-ttu-id="40161-180">Como você implementa uma atualização de SO em domínios de atualização?</span><span class="sxs-lookup"><span data-stu-id="40161-180">How do you roll out an OS update across update domains?</span></span>
<span data-ttu-id="40161-181">Suponha que você queira tooupdate sua imagem de sistema operacional, mantendo a escala de máquinas virtuais de saudação definido em execução.</span><span class="sxs-lookup"><span data-stu-id="40161-181">Suppose you want tooupdate your OS image while keeping hello virtual machine scale set running.</span></span> <span data-ttu-id="40161-182">PowerShell e hello CLI do Azure podem atualizar imagens de máquinas virtuais hello, uma máquina virtual por vez.</span><span class="sxs-lookup"><span data-stu-id="40161-182">PowerShell and hello Azure CLI can update hello virtual machine images, one virtual machine at a time.</span></span> <span data-ttu-id="40161-183">Olá [atualizar um conjunto de escala de máquinas virtuais](./virtual-machine-scale-sets-upgrade-scale-set.md) artigo também fornece informações adicionais sobre quais opções estão disponível tooperform atualizar um sistema operacional em um conjunto de escala de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="40161-183">hello [Upgrade a Virtual Machine Scale Set](./virtual-machine-scale-sets-upgrade-scale-set.md) article also provides further information on what options are available tooperform an operating system upgrade across a virtual machine scale set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40161-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="40161-184">Next steps</span></span>

* [<span data-ttu-id="40161-185">Use o PowerShell toomanage seu conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="40161-185">Use PowerShell toomanage your scale set.</span></span>](virtual-machine-scale-sets-windows-manage.md)
* [<span data-ttu-id="40161-186">Criar um modelo de conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="40161-186">Create a scale set template.</span></span>](virtual-machine-scale-sets-mvss-start.md)


[linux-vm-create]: ../virtual-machines/linux/tutorial-manage-vm.md
[windows-vm-create]: ../virtual-machines/windows/tutorial-manage-vm.md
[linux-vm-capture]: ../virtual-machines/linux/capture-image.md
[windows-vm-capture]: ../virtual-machines/windows/capture-image.md 
[vmss-create]: virtual-machine-scale-sets-create.md

