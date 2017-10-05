---
title: "Gerenciar nós de computação do cluster HPC Pack | Microsoft Docs"
description: "Saiba mais sobre as ferramentas de script do PowerShell para adicionar, remover, iniciar e interromper nós de computação do cluster HPC Pack 2012 R2 no Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: dc9f354191b9e80ff6a01bd401a874c6998bda79
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-the-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="02d23-103">Gerenciar o número e a disponibilidade de nós de computação em um cluster HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="02d23-103">Manage the number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="02d23-104">Se você criou um cluster HPC Pack 2012 R2 em VMs do Azure, pode ser conveniente encontrar maneiras de adicionar, remover, iniciar (provisionar) ou interromper (desprovisionar) facilmente algumas VMs de nó de computação no cluster.</span><span class="sxs-lookup"><span data-stu-id="02d23-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways to easily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="02d23-105">Para executar essas tarefas, execute scripts do Azure PowerShell que estão instalados na VM de nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="02d23-105">To do these tasks, run Azure PowerShell scripts that are installed on the head node VM.</span></span> <span data-ttu-id="02d23-106">Esses scripts ajudam a controlar o número e a disponibilidade dos recursos do cluster HPC Pack para que você possa controlar os custos.</span><span class="sxs-lookup"><span data-stu-id="02d23-106">These scripts help you control the number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="02d23-107">Este artigo se aplica apenas aos clusters HPC Pack 2012 R2 no Azure criados usando o modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="02d23-107">This article applies only to HPC Pack 2012 R2 clusters in Azure created using the classic deployment model.</span></span> <span data-ttu-id="02d23-108">A Microsoft recomenda que a maioria das implantações novas use o modelo do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="02d23-108">Microsoft recommends that most new deployments use the Resource Manager model.</span></span>
> <span data-ttu-id="02d23-109">Além disso, os scripts do PowerShell descritos neste artigo não estão disponíveis no HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="02d23-109">In addition, the PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02d23-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="02d23-110">Prerequisites</span></span>
* <span data-ttu-id="02d23-111">**Cluster HPC Pack 2012 R2 em VMs do Azure**: crie um cluster HPC Pack 2012 R2 no modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="02d23-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in the classic deployment model.</span></span> <span data-ttu-id="02d23-112">Por exemplo, é possível automatizar a implantação usando a imagem de VM do HPC Pack 2012 R2 no Azure Marketplace e um script do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="02d23-112">For example, you can automate the deployment by using the HPC Pack 2012 R2 VM image in the Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="02d23-113">Para obter informações e pré-requisitos, veja [Criar um cluster HPC com o script de implantação de IaaS do HPC Pack](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="02d23-113">For information and prerequisites, see [Create an HPC Cluster with the HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="02d23-114">Após a implantação, localize os scripts de gerenciamento do nó na pasta %CCP\_HOME%bin no nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="02d23-114">After deployment, find the node management scripts in the %CCP\_HOME%bin folder on the head node.</span></span> <span data-ttu-id="02d23-115">Execute cada um dos scripts como um administrador.</span><span class="sxs-lookup"><span data-stu-id="02d23-115">Run each of the scripts as an administrator.</span></span>
* <span data-ttu-id="02d23-116">**Certificado de gerenciamento ou arquivo de configurações de publicação do Azure**: você precisa executar uma das tarefas a seguir no nó de cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="02d23-116">**Azure publish settings file or management certificate**: You need to do one of the following on the head node:</span></span>
  
  * <span data-ttu-id="02d23-117">**Importe o arquivo de configurações de publicação do Azure**.</span><span class="sxs-lookup"><span data-stu-id="02d23-117">**Import the Azure publish settings file**.</span></span> <span data-ttu-id="02d23-118">Para fazer isso, execute os seguintes cmdlets do Azure PowerShell no nó de cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="02d23-118">To do this, run the following Azure PowerShell cmdlets on the head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="02d23-119">**Configure o certificado de gerenciamento do Azure no nó de cabeçalho**.</span><span class="sxs-lookup"><span data-stu-id="02d23-119">**Configure the Azure management certificate on the head node**.</span></span> <span data-ttu-id="02d23-120">Se você tiver o arquivo .cer, importe-o no repositório de certificados CurrentUser\My e, em seguida, execute o seguinte cmdlet do Azure PowerShell para seu ambiente do Azure (AzureCloud ou AzureChinaCloud):</span><span class="sxs-lookup"><span data-stu-id="02d23-120">If you have the .cer file, import it in the CurrentUser\My certificate store and then run the following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="02d23-121">Adicionar VMs de nó de computação</span><span class="sxs-lookup"><span data-stu-id="02d23-121">Add compute node VMs</span></span>
<span data-ttu-id="02d23-122">Adicionar nós de computação com o script **Add-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="02d23-122">Add compute nodes with the **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="02d23-123">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="02d23-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="02d23-124">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="02d23-124">Parameters</span></span>
* <span data-ttu-id="02d23-125">**ServiceName**: nome do serviço de nuvem ao qual novas VMs do nó de computação são adicionadas.</span><span class="sxs-lookup"><span data-stu-id="02d23-125">**ServiceName**: Name of the cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="02d23-126">**ImageName**: o nome da imagem da VM do Azure, que pode ser obtido por meio do Portal Clássico do Azure ou do cmdlet **Get-AzureVMImage** do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="02d23-126">**ImageName**: Azure VM image name, which can be obtained through the Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="02d23-127">A imagem deve atender aos seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="02d23-127">The image must meet the following requirements:</span></span>
  
  1. <span data-ttu-id="02d23-128">Um sistema operacional Windows deve ser instalado.</span><span class="sxs-lookup"><span data-stu-id="02d23-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="02d23-129">O HPC Pack deve ser instalado na função de nó de computação.</span><span class="sxs-lookup"><span data-stu-id="02d23-129">HPC Pack must be installed in the compute node role.</span></span>
  3. <span data-ttu-id="02d23-130">A imagem deve ser uma imagem privada na categoria Usuário, não uma imagem pública da VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="02d23-130">The image must be a private image in the User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="02d23-131">**Quantity**: número de VMs do nó de computação a serem adicionadas.</span><span class="sxs-lookup"><span data-stu-id="02d23-131">**Quantity**: Number of compute node VMs to be added.</span></span>
* <span data-ttu-id="02d23-132">**InstanceSize**: tamanho das VMs do nó de computação.</span><span class="sxs-lookup"><span data-stu-id="02d23-132">**InstanceSize**: Size of the compute node VMs.</span></span>
* <span data-ttu-id="02d23-133">**DomainUserName**: nome de usuário do domínio que é usado para adicionar as novas VMs ao domínio.</span><span class="sxs-lookup"><span data-stu-id="02d23-133">**DomainUserName**: Domain user name, which is used to join the new VMs to the domain.</span></span>
* <span data-ttu-id="02d23-134">**DomainUserPassword**: senha do usuário do domínio.</span><span class="sxs-lookup"><span data-stu-id="02d23-134">**DomainUserPassword**: Password of the domain user.</span></span>
* <span data-ttu-id="02d23-135">**NodeNameSeries** (opcional): padrão de nomenclatura para os nós de computação.</span><span class="sxs-lookup"><span data-stu-id="02d23-135">**NodeNameSeries** (optional): Naming pattern for the compute nodes.</span></span> <span data-ttu-id="02d23-136">O formato deve ser &lt;*Raiz\_Nome*&gt;&lt;*Iniciar\_Número*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="02d23-136">The format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="02d23-137">Por exemplo, MyCN%10% significa uma série de nomes de nó de computação com início em MyCN11.</span><span class="sxs-lookup"><span data-stu-id="02d23-137">For example, MyCN%10% means a series of the compute node names starting from MyCN11.</span></span> <span data-ttu-id="02d23-138">Se não for especificado, o script usará a série de nomenclatura do nó configurado no cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="02d23-138">If not specified, the script uses the configured node naming series in the HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="02d23-139">Exemplo</span><span class="sxs-lookup"><span data-stu-id="02d23-139">Example</span></span>
<span data-ttu-id="02d23-140">O exemplo a seguir adiciona 20 VMs de nó de computação de tamanho Grande no serviço de nuvem *hpcservice1*, com base na imagem de VM *hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="02d23-140">The following example adds 20 size Large compute node VMs in the cloud service *hpcservice1*, based on the VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="02d23-141">Remover VMs de nó de computação</span><span class="sxs-lookup"><span data-stu-id="02d23-141">Remove compute node VMs</span></span>
<span data-ttu-id="02d23-142">Remova os nós de computação com o script **Remove-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="02d23-142">Remove compute nodes with the **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="02d23-143">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="02d23-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="02d23-144">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="02d23-144">Parameters</span></span>
* <span data-ttu-id="02d23-145">**Name**: nomes dos nós do cluster a serem removidos.</span><span class="sxs-lookup"><span data-stu-id="02d23-145">**Name**: Names of cluster nodes to be removed.</span></span> <span data-ttu-id="02d23-146">Há suporte para caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="02d23-146">Wildcards are supported.</span></span> <span data-ttu-id="02d23-147">O nome do conjunto de parâmetros é Nome.</span><span class="sxs-lookup"><span data-stu-id="02d23-147">The parameter set name is Name.</span></span> <span data-ttu-id="02d23-148">Não é possível especificar os dois parâmetros **Name** e **Node**.</span><span class="sxs-lookup"><span data-stu-id="02d23-148">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="02d23-149">**Node**: o objeto HpcNode para os nós a serem removidos, que pode ser obtido por meio do cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx) do PowerShell no HPC.</span><span class="sxs-lookup"><span data-stu-id="02d23-149">**Node**: The HpcNode object for the nodes to be removed, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="02d23-150">O nome do conjunto de parâmetros é Nó.</span><span class="sxs-lookup"><span data-stu-id="02d23-150">The parameter set name is Node.</span></span> <span data-ttu-id="02d23-151">Não é possível especificar os dois parâmetros **Name** e **Node**.</span><span class="sxs-lookup"><span data-stu-id="02d23-151">You can't specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="02d23-152">**DeleteVHD** (opcional): configuração usada para excluir os discos associados das VMs que foram removidas.</span><span class="sxs-lookup"><span data-stu-id="02d23-152">**DeleteVHD** (optional): Setting to delete the associated disks for the VMs that are removed.</span></span>
* <span data-ttu-id="02d23-153">**Force** (opcional): configuração usada para forçar os nós HPC a ficarem offline antes de removê-los.</span><span class="sxs-lookup"><span data-stu-id="02d23-153">**Force** (optional): Setting to force HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="02d23-154">**Confirm** (opcional): solicitação de confirmação antes de executar o comando.</span><span class="sxs-lookup"><span data-stu-id="02d23-154">**Confirm** (optional): Prompt for confirmation before executing the command.</span></span>
* <span data-ttu-id="02d23-155">**WhatIf**: configuração usada para descrever o que aconteceria se você executasse o comando sem realmente executar o comando.</span><span class="sxs-lookup"><span data-stu-id="02d23-155">**WhatIf**: Setting to describe what would happen if you executed the command without actually executing the command.</span></span>

### <a name="example"></a><span data-ttu-id="02d23-156">Exemplo</span><span class="sxs-lookup"><span data-stu-id="02d23-156">Example</span></span>
<span data-ttu-id="02d23-157">O exemplo a seguir força os nós com nomes começando com *HPCNode-CN-* a ficarem offline e, em seguida, remove os nós e seus discos associados.</span><span class="sxs-lookup"><span data-stu-id="02d23-157">The following example forces offline the nodes with names beginning *HPCNode-CN-* and them removes the nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="02d23-158">Iniciar VMs de nó de computação</span><span class="sxs-lookup"><span data-stu-id="02d23-158">Start compute node VMs</span></span>
<span data-ttu-id="02d23-159">Inicie os nós de computação com o script **Start-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="02d23-159">Start compute nodes with the **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="02d23-160">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="02d23-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="02d23-161">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="02d23-161">Parameters</span></span>
* <span data-ttu-id="02d23-162">**Name**: nomes dos nós do cluster a serem iniciados.</span><span class="sxs-lookup"><span data-stu-id="02d23-162">**Name**: Names of the cluster nodes to be started.</span></span> <span data-ttu-id="02d23-163">Há suporte para caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="02d23-163">Wildcards are supported.</span></span> <span data-ttu-id="02d23-164">O nome do conjunto de parâmetros é Nome.</span><span class="sxs-lookup"><span data-stu-id="02d23-164">The parameter set name is Name.</span></span> <span data-ttu-id="02d23-165">Não é possível especificar os dois parâmetros **Name** e **Node**.</span><span class="sxs-lookup"><span data-stu-id="02d23-165">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="02d23-166">**Node**- O objeto HpcNode para os nós a serem iniciados, que pode ser obtido por meio do cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx)do HPC PowerShell.</span><span class="sxs-lookup"><span data-stu-id="02d23-166">**Node**- The HpcNode object for the nodes to be started, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="02d23-167">O nome do conjunto de parâmetros é Nó.</span><span class="sxs-lookup"><span data-stu-id="02d23-167">The parameter set name is Node.</span></span> <span data-ttu-id="02d23-168">Não é possível especificar os dois parâmetros **Name** e **Node**.</span><span class="sxs-lookup"><span data-stu-id="02d23-168">You cannot specify both the **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="02d23-169">Exemplo</span><span class="sxs-lookup"><span data-stu-id="02d23-169">Example</span></span>
<span data-ttu-id="02d23-170">O exemplo a seguir inicia os nós com nomes começando com *HPCNode-CN-*.</span><span class="sxs-lookup"><span data-stu-id="02d23-170">The following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="02d23-171">Interromper VMs de nó de computação</span><span class="sxs-lookup"><span data-stu-id="02d23-171">Stop compute node VMs</span></span>
<span data-ttu-id="02d23-172">Interrompa os nós de computação com o script **Stop-HpcIaaSNode.ps1** .</span><span class="sxs-lookup"><span data-stu-id="02d23-172">Stop compute nodes with the **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="02d23-173">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="02d23-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="02d23-174">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="02d23-174">Parameters</span></span>
* <span data-ttu-id="02d23-175">**Name**- Nomes dos nós do cluster a serem interrompidos.</span><span class="sxs-lookup"><span data-stu-id="02d23-175">**Name**- Names of the cluster nodes to be stopped.</span></span> <span data-ttu-id="02d23-176">Há suporte para caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="02d23-176">Wildcards are supported.</span></span> <span data-ttu-id="02d23-177">O nome do conjunto de parâmetros é Nome.</span><span class="sxs-lookup"><span data-stu-id="02d23-177">The parameter set name is Name.</span></span> <span data-ttu-id="02d23-178">Não é possível especificar os dois parâmetros **Name** e **Node**.</span><span class="sxs-lookup"><span data-stu-id="02d23-178">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="02d23-179">**Node**: o objeto HpcNode para os nós a serem interrompidos, que pode ser obtido por meio do cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx) do PowerShell no HPC.</span><span class="sxs-lookup"><span data-stu-id="02d23-179">**Node**: The HpcNode object for the nodes to be stopped, which can be obtained through the HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="02d23-180">O nome do conjunto de parâmetros é Nó.</span><span class="sxs-lookup"><span data-stu-id="02d23-180">The parameter set name is Node.</span></span> <span data-ttu-id="02d23-181">Não é possível especificar os dois parâmetros **Name** e **Node**.</span><span class="sxs-lookup"><span data-stu-id="02d23-181">You cannot specify both the **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="02d23-182">**Force** (opcional): configuração usada para forçar os nós HPC a ficarem offline antes de interrompê-los.</span><span class="sxs-lookup"><span data-stu-id="02d23-182">**Force** (optional): Setting to force HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="02d23-183">Exemplo</span><span class="sxs-lookup"><span data-stu-id="02d23-183">Example</span></span>
<span data-ttu-id="02d23-184">O exemplo a seguir força os nós a ficarem offline com nomes começando com *HPCNode-CN-* e, em seguida, interrompe os nós.</span><span class="sxs-lookup"><span data-stu-id="02d23-184">The following example forces offline nodes with names beginning *HPCNode-CN-* and then stops the nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="02d23-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="02d23-185">Next steps</span></span>
* <span data-ttu-id="02d23-186">Para aumentar ou reduzir automaticamente os nós de cluster de acordo com a atual carga de trabalhos e tarefas no cluster, confira [Aumentar e reduzir automaticamente os recursos de cluster do HPC Pack no Azure conforme a carga de trabalho de cluster](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="02d23-186">To automatically grow or shrink the cluster nodes according to the current workload of jobs and tasks on the cluster, see [Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

