---
title: "nós de computação de cluster de HPC Pack aaaManage | Microsoft Docs"
description: "Saiba mais sobre tooadd de ferramentas de script do PowerShell, remover, iniciar e parar nós de computação de cluster de HPC Pack 2012 R2 no Azure"
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
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="3f0ab-103">Gerenciar o número de saudação e a disponibilidade de nós de computação em um cluster de HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="3f0ab-103">Manage hello number and availability of compute nodes in an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="3f0ab-104">Se você criou um cluster de HPC Pack 2012 R2 em VMs do Azure, convém maneiras tooeasily adicionar, remover, iniciar (provisionar) ou pare (desprovisione) algumas VMs do nó do cluster de computação.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-104">If you created an HPC Pack 2012 R2 cluster in Azure VMs, you might want ways tooeasily add, remove, start (provision), or stop (deprovision) some compute node VMs in the cluster.</span></span> <span data-ttu-id="3f0ab-105">toodo essas tarefas, executar scripts do PowerShell do Azure que são instalados na VM do nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-105">toodo these tasks, run Azure PowerShell scripts that are installed on hello head node VM.</span></span> <span data-ttu-id="3f0ab-106">Esses scripts ajudam a controlar o número de saudação e a disponibilidade de seus recursos de cluster de HPC Pack para que você pode controlar os custos.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-106">These scripts help you control hello number and availability of your HPC Pack cluster resources so you can control costs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="3f0ab-107">Este artigo se aplica apenas tooHPC os clusters Pack 2012 R2 no Azure criados usando o modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-107">This article applies only tooHPC Pack 2012 R2 clusters in Azure created using hello classic deployment model.</span></span> <span data-ttu-id="3f0ab-108">A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span>
> <span data-ttu-id="3f0ab-109">Além disso, os scripts do PowerShell Olá descritos neste artigo não estão disponíveis no HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-109">In addition, hello PowerShell scripts described in this article are not available in HPC Pack 2016.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f0ab-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="3f0ab-110">Prerequisites</span></span>
* <span data-ttu-id="3f0ab-111">**Cluster de HPC Pack 2012 R2 em VMs do Azure**: criar um cluster de HPC Pack 2012 R2 no modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-111">**HPC Pack 2012 R2 cluster in Azure VMs**: Create an HPC Pack 2012 R2 cluster in hello classic deployment model.</span></span> <span data-ttu-id="3f0ab-112">Por exemplo, você pode automatizar a implantação de saudação usando a imagem de VM do HPC Pack 2012 R2 Olá no hello Azure Marketplace e um script do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-112">For example, you can automate hello deployment by using hello HPC Pack 2012 R2 VM image in hello Azure Marketplace and an Azure PowerShell script.</span></span> <span data-ttu-id="3f0ab-113">Para obter informações e pré-requisitos, consulte [criar um Cluster de HPC com hello script de implantação IaaS do HPC Pack](hpcpack-cluster-powershell-script.md).</span><span class="sxs-lookup"><span data-stu-id="3f0ab-113">For information and prerequisites, see [Create an HPC Cluster with hello HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md).</span></span>
  
    <span data-ttu-id="3f0ab-114">Após a implantação, localize Olá scripts de gerenciamento do nó em Olá % CCP\_pasta inicial % bin no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-114">After deployment, find hello node management scripts in hello %CCP\_HOME%bin folder on hello head node.</span></span> <span data-ttu-id="3f0ab-115">Execute cada um dos scripts hello como um administrador.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-115">Run each of hello scripts as an administrator.</span></span>
* <span data-ttu-id="3f0ab-116">**Certificado de arquivo ou o gerenciamento de configurações de publicação no Azure**: necessário toodo Olá seguinte no nó de cabeçalho hello:</span><span class="sxs-lookup"><span data-stu-id="3f0ab-116">**Azure publish settings file or management certificate**: You need toodo one of hello following on hello head node:</span></span>
  
  * <span data-ttu-id="3f0ab-117">**Saudação de importação do Azure publica o arquivo de configurações**.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-117">**Import hello Azure publish settings file**.</span></span> <span data-ttu-id="3f0ab-118">toodo, Olá executar cmdlets do Azure PowerShell a seguir no nó de cabeçalho de saudação:</span><span class="sxs-lookup"><span data-stu-id="3f0ab-118">toodo this, run hello following Azure PowerShell cmdlets on hello head node:</span></span>
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * <span data-ttu-id="3f0ab-119">**Configurar o certificado de gerenciamento do Azure Olá no nó de cabeçalho Olá**.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-119">**Configure hello Azure management certificate on hello head node**.</span></span> <span data-ttu-id="3f0ab-120">Se você tiver um arquivo. cer de hello, importe-Olá de certificados currentuser\my e execute Olá cmdlet do PowerShell do Azure para seu ambiente do Azure (AzureCloud ou AzureChinaCloud) a seguir:</span><span class="sxs-lookup"><span data-stu-id="3f0ab-120">If you have hello .cer file, import it in hello CurrentUser\My certificate store and then run hello following Azure PowerShell cmdlet for your Azure environment (either AzureCloud or AzureChinaCloud):</span></span>
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a><span data-ttu-id="3f0ab-121">Adicionar VMs de nó de computação</span><span class="sxs-lookup"><span data-stu-id="3f0ab-121">Add compute node VMs</span></span>
<span data-ttu-id="3f0ab-122">Adicionar nós de computação com hello **Add-hpciaasnode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-122">Add compute nodes with hello **Add-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="3f0ab-123">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="3f0ab-123">Syntax</span></span>
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a><span data-ttu-id="3f0ab-124">parâmetros</span><span class="sxs-lookup"><span data-stu-id="3f0ab-124">Parameters</span></span>
* <span data-ttu-id="3f0ab-125">**ServiceName**: nome do serviço de nuvem Olá novas VMs do nó de computação são adicionados ao.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-125">**ServiceName**: Name of hello cloud service that new compute node VMs are added to.</span></span>
* <span data-ttu-id="3f0ab-126">**ImageName**: nome de imagem de VM do Azure, que pode ser obtido por meio de saudação portal clássico do Azure ou o cmdlet do PowerShell do Azure **Get-AzureVMImage**.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-126">**ImageName**: Azure VM image name, which can be obtained through hello Azure classic portal or Azure PowerShell cmdlet **Get-AzureVMImage**.</span></span> <span data-ttu-id="3f0ab-127">imagem de Olá deve atender a saudação requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3f0ab-127">hello image must meet hello following requirements:</span></span>
  
  1. <span data-ttu-id="3f0ab-128">Um sistema operacional Windows deve ser instalado.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-128">A Windows operating system must be installed.</span></span>
  2. <span data-ttu-id="3f0ab-129">HPC Pack deve ser instalado na função de nó de computação hello.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-129">HPC Pack must be installed in hello compute node role.</span></span>
  3. <span data-ttu-id="3f0ab-130">imagem de saudação deve ser uma imagem privada na categoria de usuário hello, não uma imagem de VM do Azure pública.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-130">hello image must be a private image in hello User category, not a public Azure VM image.</span></span>
* <span data-ttu-id="3f0ab-131">**Quantidade**: número de toobe de VMs de nó de computação adicionado.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-131">**Quantity**: Number of compute node VMs toobe added.</span></span>
* <span data-ttu-id="3f0ab-132">**InstanceSize**: tamanho da saudação VMs do nó de computação.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-132">**InstanceSize**: Size of hello compute node VMs.</span></span>
* <span data-ttu-id="3f0ab-133">**DomainUserName**: nome de usuário de domínio, que é usado toojoin Olá novas VMs toohello domínio.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-133">**DomainUserName**: Domain user name, which is used toojoin hello new VMs toohello domain.</span></span>
* <span data-ttu-id="3f0ab-134">**DomainUserPassword**: senha de usuário de domínio hello.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-134">**DomainUserPassword**: Password of hello domain user.</span></span>
* <span data-ttu-id="3f0ab-135">**NodeNameSeries** (opcional): padrão de nomenclatura para Olá nós de computação.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-135">**NodeNameSeries** (optional): Naming pattern for hello compute nodes.</span></span> <span data-ttu-id="3f0ab-136">saudação de formato deve ser &lt; *raiz\_nome*&gt;&lt;*iniciar\_número*&gt;%.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-136">hello format must be &lt;*Root\_Name*&gt;&lt;*Start\_Number*&gt;%.</span></span> <span data-ttu-id="3f0ab-137">Por exemplo, MyCN % 10% significa uma série de saudação MyCN11 a partir de nomes de nó de computação.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-137">For example, MyCN%10% means a series of hello compute node names starting from MyCN11.</span></span> <span data-ttu-id="3f0ab-138">Se não for especificado, Olá script usa Olá configurado série de nomeação de nó no cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-138">If not specified, hello script uses hello configured node naming series in hello HPC cluster.</span></span>

### <a name="example"></a><span data-ttu-id="3f0ab-139">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3f0ab-139">Example</span></span>
<span data-ttu-id="3f0ab-140">Olá exemplo a seguir adiciona nós de computação grandes tamanho 20 VMs no serviço de nuvem Olá *hpcservice1*, com base na imagem VM Olá *hpccnimage1*.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-140">hello following example adds 20 size Large compute node VMs in hello cloud service *hpcservice1*, based on hello VM image *hpccnimage1*.</span></span>

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a><span data-ttu-id="3f0ab-141">Remover VMs de nó de computação</span><span class="sxs-lookup"><span data-stu-id="3f0ab-141">Remove compute node VMs</span></span>
<span data-ttu-id="3f0ab-142">Remover nós de computação com hello **remove-hpciaasnode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-142">Remove compute nodes with hello **Remove-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="3f0ab-143">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="3f0ab-143">Syntax</span></span>
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="3f0ab-144">parâmetros</span><span class="sxs-lookup"><span data-stu-id="3f0ab-144">Parameters</span></span>
* <span data-ttu-id="3f0ab-145">**Nome**: nomes de toobe de nós de cluster removidos.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-145">**Name**: Names of cluster nodes toobe removed.</span></span> <span data-ttu-id="3f0ab-146">Há suporte para caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-146">Wildcards are supported.</span></span> <span data-ttu-id="3f0ab-147">nome do conjunto de parâmetro Hello é nome.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-147">hello parameter set name is Name.</span></span> <span data-ttu-id="3f0ab-148">Não é possível especificar ambos os Olá **nome** e **nó** parâmetros.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-148">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="3f0ab-149">**Nó**: objeto HpcNode Olá para Olá nós toobe removido, que pode ser obtido por meio do cmdlet PowerShell HPC Olá [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f0ab-149">**Node**: hello HpcNode object for hello nodes toobe removed, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="3f0ab-150">nome do conjunto de parâmetro Hello é o nó.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-150">hello parameter set name is Node.</span></span> <span data-ttu-id="3f0ab-151">Não é possível especificar ambos os Olá **nome** e **nó** parâmetros.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-151">You can't specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="3f0ab-152">**DeleteVHD** (opcional): configuração toodelete discos Olá associado Olá VMs que são removidos.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-152">**DeleteVHD** (optional): Setting toodelete hello associated disks for hello VMs that are removed.</span></span>
* <span data-ttu-id="3f0ab-153">**Forçar** (opcional): configuração tooforce nós HPC a ficarem offline antes de removê-los.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-153">**Force** (optional): Setting tooforce HPC nodes offline before removing them.</span></span>
* <span data-ttu-id="3f0ab-154">**Confirmar** (opcional): solicitar confirmação antes de executar o comando hello.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-154">**Confirm** (optional): Prompt for confirmation before executing hello command.</span></span>
* <span data-ttu-id="3f0ab-155">**WhatIf**: configuração toodescribe o que aconteceria se você executasse o comando Olá sem realmente executar comando de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-155">**WhatIf**: Setting toodescribe what would happen if you executed hello command without actually executing hello command.</span></span>

### <a name="example"></a><span data-ttu-id="3f0ab-156">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3f0ab-156">Example</span></span>
<span data-ttu-id="3f0ab-157">Olá exemplo a seguir força nós offline Olá com nomes começando *HPCNode-CN -* e eles remove nós hello e os discos associados.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-157">hello following example forces offline hello nodes with names beginning *HPCNode-CN-* and them removes hello nodes and their associated disks.</span></span>

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a><span data-ttu-id="3f0ab-158">Iniciar VMs de nó de computação</span><span class="sxs-lookup"><span data-stu-id="3f0ab-158">Start compute node VMs</span></span>
<span data-ttu-id="3f0ab-159">Início de computação nós com hello **Start-hpciaasnode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-159">Start compute nodes with hello **Start-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="3f0ab-160">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="3f0ab-160">Syntax</span></span>
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="3f0ab-161">parâmetros</span><span class="sxs-lookup"><span data-stu-id="3f0ab-161">Parameters</span></span>
* <span data-ttu-id="3f0ab-162">**Nome**: nomes de saudação toobe de nós de cluster é iniciado.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-162">**Name**: Names of hello cluster nodes toobe started.</span></span> <span data-ttu-id="3f0ab-163">Há suporte para caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-163">Wildcards are supported.</span></span> <span data-ttu-id="3f0ab-164">nome do conjunto de parâmetro Hello é nome.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-164">hello parameter set name is Name.</span></span> <span data-ttu-id="3f0ab-165">Não é possível especificar ambos os Olá **nome** e **nó** parâmetros.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-165">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="3f0ab-166">**Nó**-objeto HpcNode Olá para Olá nós toobe iniciado, que pode ser obtido por meio do cmdlet PowerShell HPC Olá [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f0ab-166">**Node**- hello HpcNode object for hello nodes toobe started, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="3f0ab-167">nome do conjunto de parâmetro Hello é o nó.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-167">hello parameter set name is Node.</span></span> <span data-ttu-id="3f0ab-168">Não é possível especificar ambos os Olá **nome** e **nó** parâmetros.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-168">You cannot specify both hello **Name** and **Node** parameters.</span></span>

### <a name="example"></a><span data-ttu-id="3f0ab-169">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3f0ab-169">Example</span></span>
<span data-ttu-id="3f0ab-170">Olá exemplo a seguir inicia nós com nomes começando *HPCNode-CN -*.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-170">hello following example starts nodes with names beginning *HPCNode-CN-*.</span></span>

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a><span data-ttu-id="3f0ab-171">Interromper VMs de nó de computação</span><span class="sxs-lookup"><span data-stu-id="3f0ab-171">Stop compute node VMs</span></span>
<span data-ttu-id="3f0ab-172">Parar nós de computação com hello **Stop-hpciaasnode.ps1** script.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-172">Stop compute nodes with hello **Stop-HpcIaaSNode.ps1** script.</span></span>

### <a name="syntax"></a><span data-ttu-id="3f0ab-173">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="3f0ab-173">Syntax</span></span>
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a><span data-ttu-id="3f0ab-174">parâmetros</span><span class="sxs-lookup"><span data-stu-id="3f0ab-174">Parameters</span></span>
* <span data-ttu-id="3f0ab-175">**Nome**-nomes de saudação toobe de nós de cluster é interrompido.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-175">**Name**- Names of hello cluster nodes toobe stopped.</span></span> <span data-ttu-id="3f0ab-176">Há suporte para caracteres curinga.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-176">Wildcards are supported.</span></span> <span data-ttu-id="3f0ab-177">nome do conjunto de parâmetro Hello é nome.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-177">hello parameter set name is Name.</span></span> <span data-ttu-id="3f0ab-178">Não é possível especificar ambos os Olá **nome** e **nó** parâmetros.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-178">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="3f0ab-179">**Nó**: objeto HpcNode Olá para Olá nós toobe interrompido, que pode ser obtido por meio do cmdlet PowerShell HPC Olá [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span><span class="sxs-lookup"><span data-stu-id="3f0ab-179">**Node**: hello HpcNode object for hello nodes toobe stopped, which can be obtained through hello HPC PowerShell cmdlet [Get-HpcNode](https://technet.microsoft.com/library/dn887927.aspx).</span></span> <span data-ttu-id="3f0ab-180">nome do conjunto de parâmetro Hello é o nó.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-180">hello parameter set name is Node.</span></span> <span data-ttu-id="3f0ab-181">Não é possível especificar ambos os Olá **nome** e **nó** parâmetros.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-181">You cannot specify both hello **Name** and **Node** parameters.</span></span>
* <span data-ttu-id="3f0ab-182">**Forçar** (opcional): configuração tooforce nós HPC a ficarem offline antes de interrompê-los.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-182">**Force** (optional): Setting tooforce HPC nodes offline before stopping them.</span></span>

### <a name="example"></a><span data-ttu-id="3f0ab-183">Exemplo</span><span class="sxs-lookup"><span data-stu-id="3f0ab-183">Example</span></span>
<span data-ttu-id="3f0ab-184">Olá exemplo a seguir força nós offline com nomes começando *HPCNode-CN -* e, em seguida, interrompe Olá nós.</span><span class="sxs-lookup"><span data-stu-id="3f0ab-184">hello following example forces offline nodes with names beginning *HPCNode-CN-* and then stops hello nodes.</span></span>

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a><span data-ttu-id="3f0ab-185">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3f0ab-185">Next steps</span></span>
* <span data-ttu-id="3f0ab-186">tooautomatically aumentar ou reduzir nós de cluster de saudação de acordo com a carga de trabalho atual de trabalhos e tarefas no cluster Olá Olá, consulte [automaticamente ampliar ou reduzir os recursos de cluster de HPC Pack hello Azure acordo toohello cluster cargas de trabalho](hpcpack-cluster-node-autogrowshrink.md).</span><span class="sxs-lookup"><span data-stu-id="3f0ab-186">tooautomatically grow or shrink hello cluster nodes according to hello current workload of jobs and tasks on hello cluster, see [Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload](hpcpack-cluster-node-autogrowshrink.md).</span></span>

