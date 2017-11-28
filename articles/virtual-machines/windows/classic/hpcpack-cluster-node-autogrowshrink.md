---
title: "Dimensionar automaticamente nós de cluster do HPC Pack | Microsoft Docs"
description: "Aumentar e reduzir automaticamente o número de nós de computação de cluster do HPC Pack no Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: 
editor: tysonn
ms.assetid: 38762cd1-f917-464c-ae5d-b02b1eb21e3f
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/08/2016
ms.author: danlep
ms.openlocfilehash: 0dc0d15c64d8951c3c457df73588c37418a3c8a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-grow-and-shrink-the-hpc-pack-cluster-resources-in-azure-according-to-the-cluster-workload"></a><span data-ttu-id="14363-103">Aumentar e reduzir automaticamente os recursos de cluster do HPC Pack no Azure conforme a carga de trabalho de cluster</span><span class="sxs-lookup"><span data-stu-id="14363-103">Automatically grow and shrink the HPC Pack cluster resources in Azure according to the cluster workload</span></span>
<span data-ttu-id="14363-104">Se você implantar nós de "intermitência" no seu cluster do HPC Pack ou criar um cluster HPC Pack em VMs do Azure, poderá ser conveniente encontrar uma maneira de aumentar ou reduzir automaticamente os recursos do cluster, como nós ou núcleos, de acordo com a carga de trabalho no cluster.</span><span class="sxs-lookup"><span data-stu-id="14363-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink the cluster resources such as nodes or cores according to the workload on the cluster.</span></span> <span data-ttu-id="14363-105">Dimensionar os recursos de cluster dessa maneira permite que você use os recursos do Azure com mais eficiência e controle seus custos.</span><span class="sxs-lookup"><span data-stu-id="14363-105">Scaling the cluster resources in this way allows you to use your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="14363-106">Este artigo mostra duas maneiras que o HPC Pack fornece para dimensionamento automático de recursos de computação:</span><span class="sxs-lookup"><span data-stu-id="14363-106">This article shows you two ways that HPC Pack provides to autoscale compute resources:</span></span>

* <span data-ttu-id="14363-107">A propriedade **AutoGrowShrink** de cluster do HPC Pack</span><span class="sxs-lookup"><span data-stu-id="14363-107">The HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="14363-108">O script PowerShell do HPC **AzureAutoGrowShrink.ps1**</span><span class="sxs-lookup"><span data-stu-id="14363-108">The **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="14363-109">No momento somente é possível aumentar ou reduzir automaticamente nós de computação HPC Pack que estão em execução em um sistema operacional Windows Server.</span><span class="sxs-lookup"><span data-stu-id="14363-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-the-autogrowshrink-cluster-property"></a><span data-ttu-id="14363-110">Definir a propriedade de cluster AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="14363-110">Set the AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="14363-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="14363-111">Prerequisites</span></span>

* <span data-ttu-id="14363-112">**Cluster do HPC Pack 2012 R2 Atualização 2 ou posterior** : o nó de cabeçalho do cluster pode ser implantado localmente ou em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="14363-112">**HPC Pack 2012 R2 Update 2 or later cluster** - The cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="14363-113">Veja [Configurar um cluster híbrido com o HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) para começar com um nó de cabeçalho local e os nós de “disparo contínuo” do Azure.</span><span class="sxs-lookup"><span data-stu-id="14363-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="14363-114">Consulte o [script de implantação de IaaS do HPC Pack](hpcpack-cluster-powershell-script.md) para implantar rapidamente um cluster HPC Pack em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="14363-114">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="14363-115">**Para um cluster com um nó de cabeçalho no Azure (modelo de implantação do Resource Manager)** – No HPC Pack 2016, a autenticação de certificado em um aplicativo do Azure Active Directory é usada para expandir e reduzir automaticamente as VMs de cluster implantado usando o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="14363-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="14363-116">Configure um certificado da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="14363-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="14363-117">Após a implantação do cluster, conecte-se a um nó de cabeçalho pela Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="14363-117">After cluster deployment, connect by Remote Desktop to one head node.</span></span>

  2. <span data-ttu-id="14363-118">Faça upload do certificado (formato PFX com chave privada) em cada nó de cabeçalho e instale em Cert:\LocalMachine\My e Cert:\LocalMachine\Root.</span><span class="sxs-lookup"><span data-stu-id="14363-118">Upload the certificate (PFX format with private key) to each head node and install to Cert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="14363-119">Inicie o Azure PowerShell como administrador e execute os seguintes comandos em um nó de cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="14363-119">Start Azure PowerShell as an administrator and run the following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="14363-120">Se sua conta estiver em mais de um locatário do Azure Active Directory ou em mais de uma assinatura do Azure, execute o seguinte comando para selecionar o locatário e a assinatura corretos:</span><span class="sxs-lookup"><span data-stu-id="14363-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run the following command to select the correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="14363-121">Execute o seguinte comando para exibir o locatário e a assinatura atualmente selecionados:</span><span class="sxs-lookup"><span data-stu-id="14363-121">Run the following command to view the currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="14363-122">Execute o seguinte script</span><span class="sxs-lookup"><span data-stu-id="14363-122">Run the following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="14363-123">onde</span><span class="sxs-lookup"><span data-stu-id="14363-123">where</span></span>

    <span data-ttu-id="14363-124">**DisplayName** – nome de exibição do aplicativo ativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="14363-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="14363-125">Se o aplicativo não existir, ele será criado no Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="14363-125">If the application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="14363-126">**Home page** – a home page do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="14363-126">**HomePage** - The home page of the application.</span></span> <span data-ttu-id="14363-127">Você pode configurar uma URL fictícia, como no exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="14363-127">You can configure a dummy URL, as in the preceding example.</span></span>

    <span data-ttu-id="14363-128">**IdentifierUri** – identificador do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="14363-128">**IdentifierUri** - Identifier of the application.</span></span> <span data-ttu-id="14363-129">Você pode configurar uma URL fictícia, como no exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="14363-129">You can configure a dummy URL, as in the preceding example.</span></span>

    <span data-ttu-id="14363-130">**CertificateThumbprint** – impressão digital do certificado instalado no nó de cabeçalho na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="14363-130">**CertificateThumbprint** - Thumbprint of the certificate you installed on the head node in Step 1.</span></span>

    <span data-ttu-id="14363-131">**TenantId** – ID de locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="14363-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="14363-132">Obtenha a ID de Locatário na página **Propriedades** do portal do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="14363-132">You can get the Tenant ID from the Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="14363-133">Para obter mais detalhes sobre **ConfigARMAutoGrowShrinkCert.ps1**, execute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="14363-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="14363-134">**Para um cluster com um nó de cabeçalho no Azure (modelo de implantação clássico)** – Se você usar o script de implantação do IaaS HPC Pack para criar o cluster no modelo de implantação clássico, habilite a propriedade de cluster **AutoGrowShrink** definindo a opção AutoGrowShrink no arquivo de configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="14363-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use the HPC Pack IaaS deployment script to create the cluster in the classic deployment model, enable the **AutoGrowShrink** cluster property by setting the AutoGrowShrink option in the cluster configuration file.</span></span> <span data-ttu-id="14363-135">Para obter detalhes, consulte a documentação que acompanha o [download do script](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="14363-135">For details, see the documentation accompanying the [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="14363-136">Como alternativa, habilite a propriedade de cluster **AutoGrowShrink** depois de implantá-lo usando os comandos do PowerShell HPC descritos na seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="14363-136">Alternatively, enable the **AutoGrowShrink** cluster property after you deploy the cluster by using HPC PowerShell commands described in the following section.</span></span> <span data-ttu-id="14363-137">Para se preparar para isso, primeiro conclua as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="14363-137">To prepare for this, first complete the following steps:</span></span>

  1. <span data-ttu-id="14363-138">Configure o certificado de gerenciamento do Azure no nó de cabeçalho na assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="14363-138">Configure an Azure management certificate on the head node and in the Azure subscription.</span></span> <span data-ttu-id="14363-139">Para uma implantação de teste, você pode usar o certificado autoassinado padrão do Microsoft HPC Azure que instala o HPC Pack no nó de cabeçalho e então carregar esse certificado para a sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="14363-139">For a test deployment, you can use the Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on the head node, and then upload that certificate to your Azure subscription.</span></span> <span data-ttu-id="14363-140">Para ver as opções e as etapas, consulte a [diretriz da Biblioteca do TechNet](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="14363-140">For options and steps, see the [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="14363-141">Execute **regedit** no nó de cabeçalho, vá para HKLM\SOFTWARE\Micorsoft\HPC\IaasInfo e adicione um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="14363-141">Run **regedit** on the head node, go to HKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="14363-142">Defina o nome do valor como "Impressão digital" e dados de Valor para a impressão digital do certificado na Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="14363-142">Set the Value name to “ThumbPrint”, and Value data to the thumbprint of the certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-to-set-the-autogrowshrink-property"></a><span data-ttu-id="14363-143">Comandos do PowerShell HPC para definir a propriedade AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="14363-143">HPC PowerShell commands to set the AutoGrowShrink property</span></span>
<span data-ttu-id="14363-144">A seguir estão exemplos de comandos do PowerShell HPC para definir **AutoGrowShrink** e ajustar seu comportamento com parâmetros adicionais.</span><span class="sxs-lookup"><span data-stu-id="14363-144">Following are sample HPC PowerShell commands to set **AutoGrowShrink** and to tune its behavior with additional parameters.</span></span> <span data-ttu-id="14363-145">Consulte [parâmetros de AutoGrowShrink](#AutoGrowShrink-parameters) posteriormente neste artigo para obter uma lista de configurações.</span><span class="sxs-lookup"><span data-stu-id="14363-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for the complete list of settings.</span></span>

<span data-ttu-id="14363-146">Para executar esses comandos, inicie o PowerShell HPC no nó principal do cluster como um administrador.</span><span class="sxs-lookup"><span data-stu-id="14363-146">To run these commands, start HPC PowerShell on the cluster head node as an administrator.</span></span>

<span data-ttu-id="14363-147">**Para habilitar a propriedade AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="14363-147">**To enable the AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="14363-148">**Para desabilitar a propriedade AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="14363-148">**To disable the AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="14363-149">**Para alterar o intervalo de crescimento em minutos**</span><span class="sxs-lookup"><span data-stu-id="14363-149">**To change the grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="14363-150">**Para alterar o intervalo de diminuição em minutos**</span><span class="sxs-lookup"><span data-stu-id="14363-150">**To change the shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="14363-151">**Para exibir a configuração atual de AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="14363-151">**To view the current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="14363-152">**Para excluir grupos de nó de AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="14363-152">**To exclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="14363-153">Esse parâmetro tem suporte do HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="14363-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="14363-154">parâmetros de AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="14363-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="14363-155">A seguir estão os parâmetros de AutoGrowShrink que podem ser modificados usando o comando **Set-HpcClusterProperty** .</span><span class="sxs-lookup"><span data-stu-id="14363-155">The following are AutoGrowShrink parameters that you can modify by using the **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="14363-156">**EnableGrowShrink** – Mude para habilitar ou desabilitar a propriedade **AutoGrowShrink**.</span><span class="sxs-lookup"><span data-stu-id="14363-156">**EnableGrowShrink** - Switch to enable or disable the **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="14363-157">**ParamSweepTasksPerCore** : número de tarefas de limpeza paramétrica para aumentar um núcleo.</span><span class="sxs-lookup"><span data-stu-id="14363-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks to grow one core.</span></span> <span data-ttu-id="14363-158">O padrão é a aumentar um núcleo por tarefa.</span><span class="sxs-lookup"><span data-stu-id="14363-158">The default is to grow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="14363-159">O QFE KB3134307 do HPC Pack altera o **ParamSweepTasksPerCore** para **TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="14363-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** to **TasksPerResourceUnit**.</span></span> <span data-ttu-id="14363-160">Ele se baseia no tipo de recurso de trabalho e pode ser nó, soquete ou núcleo.</span><span class="sxs-lookup"><span data-stu-id="14363-160">It is based on the job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="14363-161">**GrowThreshold** : limite de tarefas em fila para disparar o crescimento automático.</span><span class="sxs-lookup"><span data-stu-id="14363-161">**GrowThreshold** - Threshold of queued tasks to trigger automatic growth.</span></span> <span data-ttu-id="14363-162">O padrão é 1, o que significa que, se houver 1 ou mais tarefas no estado em fila, os nós aumentarão automaticamente.</span><span class="sxs-lookup"><span data-stu-id="14363-162">The default is 1, which means that if there are 1 or more tasks in the queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="14363-163">**GrowInterval** : intervalo em minutos para disparar o crescimento automático.</span><span class="sxs-lookup"><span data-stu-id="14363-163">**GrowInterval** - Interval in minutes to trigger automatic growth.</span></span> <span data-ttu-id="14363-164">O intervalo padrão é 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="14363-164">The default interval is 5 minutes.</span></span>
* <span data-ttu-id="14363-165">**ShrinkInterval** : intervalo em minutos para disparar a redução automática.</span><span class="sxs-lookup"><span data-stu-id="14363-165">**ShrinkInterval** - Interval in minutes to trigger automatic shrinking.</span></span> <span data-ttu-id="14363-166">O intervalo padrão é 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="14363-166">The default interval is 5 minutes.|</span></span>
* <span data-ttu-id="14363-167">**ShrinkIdleTimes** : o número de verificações contínuas para reduzir para indicar que os nós estão ociosos.</span><span class="sxs-lookup"><span data-stu-id="14363-167">**ShrinkIdleTimes** - Number of continuous checks to shrink to indicate the nodes are idle.</span></span> <span data-ttu-id="14363-168">O padrão é 3.</span><span class="sxs-lookup"><span data-stu-id="14363-168">The default is 3 times.</span></span> <span data-ttu-id="14363-169">Por exemplo, se o **ShrinkInterval** for de 5 minutos, o HPC Pack verifica se o nó está ocioso a cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="14363-169">For example, if the **ShrinkInterval** is 5 minutes, HPC Pack checks whether the node is idle every 5 minutes.</span></span> <span data-ttu-id="14363-170">Se os nós estiverem no estado ocioso após 3 verificações contínuas (15 minutos), o HPC Pack reduzirá esse nó.</span><span class="sxs-lookup"><span data-stu-id="14363-170">If the nodes are in the idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="14363-171">**ExtraNodesGrowRatio** : percentual adicional de nós para crescimento de trabalhos de MPI (Interface Transferência de Mensagens).</span><span class="sxs-lookup"><span data-stu-id="14363-171">**ExtraNodesGrowRatio** - Additional percentage of nodes to grow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="14363-172">O valor padrão é 1, o que significa que o HPC Pack aumenta 1% dos nós para trabalhos MPI.</span><span class="sxs-lookup"><span data-stu-id="14363-172">The default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="14363-173">**GrowByMin** : alterne para indicar se a política de crescimento automático se baseia nos recursos mínimos necessários para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="14363-173">**GrowByMin** - Switch to indicate whether the autogrow policy is based on the minimum resources required for the job.</span></span> <span data-ttu-id="14363-174">O padrão é false, o que significa que o HPC Pack aumenta os nós para trabalhos com base nos recursos máximo necessários para os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="14363-174">The default is false, which means that HPC Pack grows nodes for jobs based on the maximum resources required for the jobs.</span></span>
* <span data-ttu-id="14363-175">**SoaJobGrowThreshold** : limite de solicitações SOA de entrada para disparar o processo de crescimento automático.</span><span class="sxs-lookup"><span data-stu-id="14363-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests to trigger the automatic grow process.</span></span> <span data-ttu-id="14363-176">O valor padrão é 50000.</span><span class="sxs-lookup"><span data-stu-id="14363-176">The default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="14363-177">Esse parâmetro tem suporte a partir do HPC Pack 2012 R2 Atualização 3.</span><span class="sxs-lookup"><span data-stu-id="14363-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="14363-178">**SoaRequestsPerCore** : o número de solicitações SOA de entrada para aumentar um núcleo.</span><span class="sxs-lookup"><span data-stu-id="14363-178">**SoaRequestsPerCore** -Number of incoming SOA requests to grow one core.</span></span> <span data-ttu-id="14363-179">O valor padrão é 20000.</span><span class="sxs-lookup"><span data-stu-id="14363-179">The default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="14363-180">Esse parâmetro tem suporte a partir do HPC Pack 2012 R2 Atualização 3.</span><span class="sxs-lookup"><span data-stu-id="14363-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="14363-181">**ExcludeNodeGroups** – Nós nos grupos de nó especificados não aumentam ou reduzem automaticamente.</span><span class="sxs-lookup"><span data-stu-id="14363-181">**ExcludeNodeGroups** – Nodes in the specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="14363-182">Esse parâmetro tem suporte do HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="14363-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="14363-183">Exemplo de MPI</span><span class="sxs-lookup"><span data-stu-id="14363-183">MPI example</span></span>
<span data-ttu-id="14363-184">Por padrão, o HPC Pack aumenta 1% de nós extras para trabalhos MPI (**ExtraNodesGrowRatio** está definido como 1).</span><span class="sxs-lookup"><span data-stu-id="14363-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set to 1).</span></span> <span data-ttu-id="14363-185">O motivo é que MPI pode exigir vários nós e o trabalho pode ser executado somente quando todos os nós estiverem prontos.</span><span class="sxs-lookup"><span data-stu-id="14363-185">The reason is that MPI may require multiple nodes, and the job can only run when all nodes are ready.</span></span> <span data-ttu-id="14363-186">Quando o Azure inicia os nós, ocasionalmente, um nó pode precisar de mais tempo para iniciar que os outros, fazendo com que outros nós fiquem ociosos enquanto aguardam esse nó ficar pronto.</span><span class="sxs-lookup"><span data-stu-id="14363-186">When Azure starts nodes, occasionally one node might need more time to start than others, causing other nodes to be idle while waiting for that node to get ready.</span></span> <span data-ttu-id="14363-187">Ao aumentar nós extras, o HPC Pack reduz o tempo de espera desse recurso e potencialmente reduz os custos.</span><span class="sxs-lookup"><span data-stu-id="14363-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="14363-188">Para aumentar o percentual de nós extras para trabalhos de MPI (por exemplo, para 10%), execute um comando semelhante a</span><span class="sxs-lookup"><span data-stu-id="14363-188">To increase the percentage of extra nodes for MPI jobs (for example, to 10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="14363-189">Exemplo de SOA</span><span class="sxs-lookup"><span data-stu-id="14363-189">SOA example</span></span>
<span data-ttu-id="14363-190">Por padrão, **SoaJobGrowThreshold** é definido como 50000 e **SoaRequestsPerCore** é definido como 200000.</span><span class="sxs-lookup"><span data-stu-id="14363-190">By default, **SoaJobGrowThreshold** is set to 50000 and **SoaRequestsPerCore** is set to 200000.</span></span> <span data-ttu-id="14363-191">Se você enviar um trabalho SOA com 70000 solicitações, há uma tarefa na fila e as solicitações de entrada serão 70000.</span><span class="sxs-lookup"><span data-stu-id="14363-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="14363-192">Nesse caso, o HPC Pack aumenta 1 núcleo para a tarefa em fila e para solicitações de entrada aumenta (70000 - 50000)/20000 = 1 núcleo, portanto o total aumenta em 2 núcleos para este trabalho SOA.</span><span class="sxs-lookup"><span data-stu-id="14363-192">In this case HPC Pack grows 1 core for the queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-the-azureautogrowshrinkps1-script"></a><span data-ttu-id="14363-193">Executar o script AzureAutoGrowShrink.ps1</span><span class="sxs-lookup"><span data-stu-id="14363-193">Run the AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="14363-194">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="14363-194">Prerequisites</span></span>

* <span data-ttu-id="14363-195">**Cluster HPC Pack 2012 R2 Atualização 1 ou cluster posterior** – O script **AzureAutoGrowShrink.ps1** está instalado na pasta %CCP_HOME%bin.</span><span class="sxs-lookup"><span data-stu-id="14363-195">**HPC Pack 2012 R2 Update 1 or later cluster** - The **AzureAutoGrowShrink.ps1** script is installed in the %CCP_HOME%bin folder.</span></span> <span data-ttu-id="14363-196">O nó de cabeçalho do cluster pode ser implantado localmente ou em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="14363-196">The cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="14363-197">Veja [Configurar um cluster híbrido com o HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) para começar com um nó de cabeçalho local e os nós de “disparo contínuo” do Azure.</span><span class="sxs-lookup"><span data-stu-id="14363-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) to get started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="14363-198">Consulte o [script de implantação IaaS do HPC Pack](hpcpack-cluster-powershell-script.md) para implantar rapidamente um cluster HPC Pack em VMs do Azure ou use um [modelo de início rápido do Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="14363-198">See the [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) to quickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="14363-199">**Azure PowerShell 1.4.0** – O script depende atualmente desta versão específica do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="14363-199">**Azure PowerShell 1.4.0** - The script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="14363-200">**Para um cluster com nós de disparo contínuo do Azure** - Execute o script em um computador cliente em que o HPC Pack está instalado ou no nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="14363-200">**For a cluster with Azure burst nodes** - Run the script on a client computer where HPC Pack is installed, or on the head node.</span></span> <span data-ttu-id="14363-201">Se executado em um computador cliente, certifique-se de que você defina a variável $env:CCP_SCHEDULER para apontar para o nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="14363-201">If running on a client computer, ensure that you set the variable $env:CCP_SCHEDULER to point to the head node.</span></span> <span data-ttu-id="14363-202">Os nós de "intermitência" do Azure devem ter sido adicionados ao cluster, mas podem estar no estado Não Implantado.</span><span class="sxs-lookup"><span data-stu-id="14363-202">The Azure “burst” nodes must be added to the cluster, but they may be in the Not-Deployed state.</span></span>
* <span data-ttu-id="14363-203">**Para um cluster implantado em VMs do Azure (modelo de implantação do Resource Manager)** – Para um cluster de VMs do Azure implantado no modelo de implantação do Resource Manager, o script oferece suporte a dois métodos de autenticação do Azure: entrar em sua conta do Azure para executar o script todas as vezes (executando `Login-AzureRmAccount`, ou configurar uma entidade de serviço para autenticar com um certificado.</span><span class="sxs-lookup"><span data-stu-id="14363-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in the Resource Manager deployment model, the script supports two methods for Azure authentication: sign in to your Azure account to run the script every time (by running `Login-AzureRmAccount`, or configure a service principal to authenticate with a certificate.</span></span> <span data-ttu-id="14363-204">O HPC Pack fornece o script **ConfigARMAutoGrowShrinkCert.ps** para criar uma entidade de serviço com certificado.</span><span class="sxs-lookup"><span data-stu-id="14363-204">HPC Pack provides the script **ConfigARMAutoGrowShrinkCert.ps** to create a service principal with certificate.</span></span> <span data-ttu-id="14363-205">O script cria um aplicativo do Azure Active Directory (Azure AD) e uma entidade de serviço e atribui a função de Colaborador para a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="14363-205">The script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns the Contributor role to the service principal.</span></span> <span data-ttu-id="14363-206">Para executar o script, inicie o Azure PowerShell como administrador e execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="14363-206">To run the script, start Azure PowerShell  as administrator and run the following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="14363-207">Para obter mais detalhes sobre **ConfigARMAutoGrowShrinkCert.ps1**, execute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span><span class="sxs-lookup"><span data-stu-id="14363-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="14363-208">**Para um cluster implantado em VMs do Azure (modelo de implantação clássico)** – Execute o script no nó de cabeçalho da VM, pois ele depende dos scripts **Start-HpcIaaSNode.ps1** e **Stop-HpcIaaSNode.ps1** que estão instalados ali.</span><span class="sxs-lookup"><span data-stu-id="14363-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run the script on the head node VM, because it depends on the **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="14363-209">Além disso, esses scripts exigem um certificado de gerenciamento ou um arquivo de configurações de publicação do Azure (veja [Gerenciar nós de computação em um cluster HPC Pack no Azure](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="14363-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="14363-210">Verifique se todas as VMs de nó de computação necessárias já foram adicionadas ao cluster.</span><span class="sxs-lookup"><span data-stu-id="14363-210">Make sure all the compute node VMs you need are already added to the cluster.</span></span> <span data-ttu-id="14363-211">Eles podem estar no estado Parado.</span><span class="sxs-lookup"><span data-stu-id="14363-211">They may be in the Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="14363-212">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="14363-212">Syntax</span></span>
```powershell
AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfActiveQueuedTasksPerNodeToGrow <Single> [-NumOfActiveQueuedTasksToGrowThreshold <Int32>]
    [-NumOfInitialNodesToGrow <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>]
    [-ShrinkCheckIdleTimes <Int32>] [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>]
    [<CommonParameters>]

AzureAutoGrowShrink.ps1 [-NodeTemplates <String[]>] [-JobTemplates <String[]>] [-NodeType <String>]
    -NumOfQueuedJobsPerNodeToGrow <Single> [-NumOfQueuedJobsToGrowThreshold <Int32>] [-NumOfInitialNodesToGrow
    <Int32>] [-GrowCheckIntervalMins <Int32>] [-ShrinkCheckIntervalMins <Int32>] [-ShrinkCheckIdleTimes <Int32>]
    [-ExtraNodesGrowRatio <Int32>] [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]

AzureAutoGrowShrink.ps1 -UseLastConfigurations [-ArgFile <String>] [-LogFilePrefix <String>] [<CommonParameters>]
```
### <a name="parameters"></a><span data-ttu-id="14363-213">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="14363-213">Parameters</span></span>
* <span data-ttu-id="14363-214">**NodeTemplates** - Nomes dos modelos de nó para definir o escopo para que os nós sejam aumentados ou reduzidos.</span><span class="sxs-lookup"><span data-stu-id="14363-214">**NodeTemplates** - Names of the node templates to define the scope for the nodes to grow and shrink.</span></span> <span data-ttu-id="14363-215">Se não for especificado (o valor padrão é @()), todos os nós no grupo de nós **AzureNodes** estarão no escopo quando **NodeType** tiver um valor de AzureNodes e todos os nós do grupo de nós **ComputeNodes** estarão no escopo quando **NodeType** tiver um valor de ComputeNodes.</span><span class="sxs-lookup"><span data-stu-id="14363-215">If not specified (the default value is @()), all nodes in the **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in the **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="14363-216">**JobTemplates** - Nomes dos modelos de trabalho para definir o escopo para que os nós sejam aumentados.</span><span class="sxs-lookup"><span data-stu-id="14363-216">**JobTemplates** - Names of the job templates to define the scope for the nodes to grow.</span></span>
* <span data-ttu-id="14363-217">**NodeType** - O tipo de nó para ser aumentado ou reduzido.</span><span class="sxs-lookup"><span data-stu-id="14363-217">**NodeType** - The type of node to grow and shrink.</span></span> <span data-ttu-id="14363-218">Os valores para os quais há suporte são:</span><span class="sxs-lookup"><span data-stu-id="14363-218">Supported values are:</span></span>

  * <span data-ttu-id="14363-219">**AzureNodes** – para os nós (de disparo contínuo) de PaaS do Azure em cluster local ou de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="14363-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="14363-220">**ComputeNodes** - para VMs de nó de computação apenas em um cluster de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="14363-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="14363-221">**NumOfQueuedJobsPerNodeToGrow** - Número de trabalhos em fila necessários para aumentar um nó.</span><span class="sxs-lookup"><span data-stu-id="14363-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required to grow one node.</span></span>
* <span data-ttu-id="14363-222">**NumOfQueuedJobsToGrowThreshold** - O número de trabalhos em fila para iniciar o processo de aumento.</span><span class="sxs-lookup"><span data-stu-id="14363-222">**NumOfQueuedJobsToGrowThreshold** - The threshold number of queued jobs to start the grow process.</span></span>
* <span data-ttu-id="14363-223">**NumOfActiveQueuedTasksPerNodeToGrow** - O número de tarefas em fila ativas necessárias para aumentar um nó.</span><span class="sxs-lookup"><span data-stu-id="14363-223">**NumOfActiveQueuedTasksPerNodeToGrow** - The number of active queued tasks required to grow one node.</span></span> <span data-ttu-id="14363-224">Se **NumOfQueuedJobsPerNodeToGrow** for especificado com um valor maior que 0, esse parâmetro será ignorado.</span><span class="sxs-lookup"><span data-stu-id="14363-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="14363-225">**NumOfActiveQueuedTasksToGrowThreshold** - O número de tarefas em fila ativas para iniciar o processo de aumento.</span><span class="sxs-lookup"><span data-stu-id="14363-225">**NumOfActiveQueuedTasksToGrowThreshold** - The threshold number of active queued tasks to start the grow process.</span></span>
* <span data-ttu-id="14363-226">**NumOfInitialNodesToGrow** – O número mínimo inicial de nós a ser aumentado se todos os nós no escopo forem **Não Implantados** ou **Interrompidos (Desalocados)**.</span><span class="sxs-lookup"><span data-stu-id="14363-226">**NumOfInitialNodesToGrow** - The initial minimum number of nodes to grow if all the nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="14363-227">**GrowCheckIntervalMins** - O intervalo em minutos entre as verificações a ser aumentado.</span><span class="sxs-lookup"><span data-stu-id="14363-227">**GrowCheckIntervalMins** - The interval in minutes between checks to grow.</span></span>
* <span data-ttu-id="14363-228">**ShrinkCheckIntervalMins** - O intervalo em minutos entre as verificações a ser reduzido.</span><span class="sxs-lookup"><span data-stu-id="14363-228">**ShrinkCheckIntervalMins** - The interval in minutes between checks to shrink.</span></span>
* <span data-ttu-id="14363-229">**ShrinkCheckIdleTimes** – O número de verificações de redução contínuas (separado por **ShrinkCheckIntervalMins**) para indicar que os nós estão ociosos.</span><span class="sxs-lookup"><span data-stu-id="14363-229">**ShrinkCheckIdleTimes** - The number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) to indicate the nodes are idle.</span></span>
* <span data-ttu-id="14363-230">**UseLastConfigurations** : as configurações anteriores salvas no arquivo de argumento.</span><span class="sxs-lookup"><span data-stu-id="14363-230">**UseLastConfigurations** - The previous configurations saved in the argument file.</span></span>
* <span data-ttu-id="14363-231">**ArgFile**- O nome do arquivo argumento usado para salvar e atualizar as configurações para executar o script.</span><span class="sxs-lookup"><span data-stu-id="14363-231">**ArgFile**- The name of the argument file used to save and update the configurations to run the script.</span></span>
* <span data-ttu-id="14363-232">**LogFilePrefix** - O nome do prefixo do arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="14363-232">**LogFilePrefix** - The prefix name of the log file.</span></span> <span data-ttu-id="14363-233">Você pode especificar um caminho.</span><span class="sxs-lookup"><span data-stu-id="14363-233">You can specify a path.</span></span> <span data-ttu-id="14363-234">Por padrão, o log é gravado no atual diretório de trabalho.</span><span class="sxs-lookup"><span data-stu-id="14363-234">By default the log is written to the current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="14363-235">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="14363-235">Example 1</span></span>
<span data-ttu-id="14363-236">O exemplo a seguir configura os nós de disparo contínuo do Azure implantados com o Modelo Padrão AzureNode para aumentar ou reduzir automaticamente.</span><span class="sxs-lookup"><span data-stu-id="14363-236">The following example configures the Azure burst nodes deployed with the Default AzureNode Template to grow and shrink automatically.</span></span> <span data-ttu-id="14363-237">Se todos os nós estiverem inicialmente no estado **Não Implantado** , pelo menos três nós serão iniciados.</span><span class="sxs-lookup"><span data-stu-id="14363-237">If all the nodes are initially in the **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="14363-238">Se o número de trabalhos em fila exceder oito, o script iniciará os nós até seu número exceder a taxa de trabalhos em fila para **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="14363-238">If the number of queued jobs exceeds 8, the script starts nodes until their number exceeds the ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="14363-239">Se for descoberto que um nó está ocioso em 3 tempos ociosos consecutivos, ele será interrompido.</span><span class="sxs-lookup"><span data-stu-id="14363-239">If a node is found to be idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="14363-240">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="14363-240">Example 2</span></span>
<span data-ttu-id="14363-241">O exemplo a seguir configura as VMs de nó de computação do Azure implantadas com o Modelo Padrão ComputeNode para serem aumentadas ou reduzidas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="14363-241">The following example configures the Azure compute node VMs deployed with the Default ComputeNode Template to grow and shrink automatically.</span></span>
<span data-ttu-id="14363-242">Os trabalhos configurados pelo modelo de trabalho Padrão definem o escopo da carga de trabalho no cluster.</span><span class="sxs-lookup"><span data-stu-id="14363-242">The jobs configured by the Default job template define the scope of the workload on the cluster.</span></span> <span data-ttu-id="14363-243">Se todos os nós forem interrompidos inicialmente, pelo menos cinco nós serão iniciados.</span><span class="sxs-lookup"><span data-stu-id="14363-243">If all the nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="14363-244">Se o número de tarefas em fila ativas exceder quinze, o script iniciará os nós até seu número exceder a taxa de tarefas em fila ativas para **NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="14363-244">If the number of active queued tasks exceeds 15, the script starts nodes until their number exceeds the ratio of active queued tasks to **NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="14363-245">Se for descoberto que um nó está ocioso em 10 tempos ociosos consecutivos, ele será interrompido.</span><span class="sxs-lookup"><span data-stu-id="14363-245">If a node is found to be idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
