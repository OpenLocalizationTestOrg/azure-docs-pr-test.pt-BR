---
title: "nós de cluster de HPC Pack aaaAutoscale | Microsoft Docs"
description: "Automaticamente aumentar ou reduzir o número de saudação de nós de computação de cluster de HPC Pack no Azure"
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
ms.openlocfilehash: 0bdf55625d337a2bbfe05677682d645a584798d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-grow-and-shrink-hello-hpc-pack-cluster-resources-in-azure-according-toohello-cluster-workload"></a><span data-ttu-id="8d7df-103">Aumentar e reduzir os recursos de cluster de HPC Pack Olá no Azure de acordo com a carga de trabalho de cluster toohello automaticamente</span><span class="sxs-lookup"><span data-stu-id="8d7df-103">Automatically grow and shrink hello HPC Pack cluster resources in Azure according toohello cluster workload</span></span>
<span data-ttu-id="8d7df-104">Se você implantar nós de "Disparo" do Azure em seu cluster de HPC Pack ou criar um cluster de HPC Pack em VMs do Azure, talvez seja uma maneira de aumentar ou reduzir os recursos de cluster hello como nós ou núcleos de acordo com a carga de trabalho Olá no cluster Olá automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8d7df-104">If you deploy Azure “burst” nodes in your HPC Pack cluster, or you create an HPC Pack cluster in Azure VMs, you may want a way to automatically grow or shrink hello cluster resources such as nodes or cores according to hello workload on hello cluster.</span></span> <span data-ttu-id="8d7df-105">Dimensionamento dos recursos de cluster Olá dessa maneira permite que você toouse os recursos do Azure com mais eficiência e controlar os custos.</span><span class="sxs-lookup"><span data-stu-id="8d7df-105">Scaling hello cluster resources in this way allows you toouse your Azure resources more efficiently and control their costs.</span></span>

<span data-ttu-id="8d7df-106">Este artigo mostra duas maneiras de HPC Pack fornece recursos de computação tooautoscale:</span><span class="sxs-lookup"><span data-stu-id="8d7df-106">This article shows you two ways that HPC Pack provides tooautoscale compute resources:</span></span>

* <span data-ttu-id="8d7df-107">saudação de propriedade de cluster de HPC Pack **AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="8d7df-107">hello HPC Pack cluster property **AutoGrowShrink**</span></span>

* <span data-ttu-id="8d7df-108">Olá **AzureAutoGrowShrink.ps1** script do HPC PowerShell</span><span class="sxs-lookup"><span data-stu-id="8d7df-108">hello **AzureAutoGrowShrink.ps1** HPC PowerShell script</span></span>

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="8d7df-109">No momento somente é possível aumentar ou reduzir automaticamente nós de computação HPC Pack que estão em execução em um sistema operacional Windows Server.</span><span class="sxs-lookup"><span data-stu-id="8d7df-109">Currently you can only automatically grow and shrink HPC Pack compute nodes that are running a Windows Server operating system.</span></span>


## <a name="set-hello-autogrowshrink-cluster-property"></a><span data-ttu-id="8d7df-110">Definir a propriedade de cluster AutoGrowShrink Olá</span><span class="sxs-lookup"><span data-stu-id="8d7df-110">Set hello AutoGrowShrink cluster property</span></span>
### <a name="prerequisites"></a><span data-ttu-id="8d7df-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8d7df-111">Prerequisites</span></span>

* <span data-ttu-id="8d7df-112">**HPC Pack 2012 R2 atualização 2 ou posterior cluster** -nó principal do cluster Olá pode ser implantado no local ou em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d7df-112">**HPC Pack 2012 R2 Update 2 or later cluster** - hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="8d7df-113">Consulte [configurar um cluster híbrido com o HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget iniciado conosco de "Disparo" do Azure e um nó principal local.</span><span class="sxs-lookup"><span data-stu-id="8d7df-113">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="8d7df-114">Consulte Olá [script de implantação IaaS do HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly implantar um cluster de HPC Pack em VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d7df-114">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs.</span></span>

* <span data-ttu-id="8d7df-115">**Para um cluster com um nó de cabeçalho no Azure (modelo de implantação do Resource Manager)** – No HPC Pack 2016, a autenticação de certificado em um aplicativo do Azure Active Directory é usada para expandir e reduzir automaticamente as VMs de cluster implantado usando o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8d7df-115">**For a cluster with a head node in Azure (Resource Manager deployment model)** - Starting in HPC Pack 2016, certificate authentication in an Azure Active Directory application is used for automatically growing and shrinking cluster VMs deployed using Azure Resource Manager.</span></span> <span data-ttu-id="8d7df-116">Configure um certificado da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8d7df-116">Configure a certificate as follows:</span></span>

  1. <span data-ttu-id="8d7df-117">Após a implantação de cluster, conecte-se ao nó principal do tooone de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="8d7df-117">After cluster deployment, connect by Remote Desktop tooone head node.</span></span>

  2. <span data-ttu-id="8d7df-118">Carregar o nó principal do tooeach Olá certificado (formato PFX com chave privada) e instale tooCert:\LocalMachine\My e Cert: \LocalMachine\Root.</span><span class="sxs-lookup"><span data-stu-id="8d7df-118">Upload hello certificate (PFX format with private key) tooeach head node and install tooCert:\LocalMachine\My and Cert:\LocalMachine\Root.</span></span>

  3. <span data-ttu-id="8d7df-119">Inicie o PowerShell do Azure como administrador e execute Olá comandos a seguir em um nó principal:</span><span class="sxs-lookup"><span data-stu-id="8d7df-119">Start Azure PowerShell as an administrator and run hello following commands on one head node:</span></span>

    ```powershell
        cd $env:CCP_HOME\bin

        Login-AzureRmAccount
    ```
        
    <span data-ttu-id="8d7df-120">Se sua conta estiver em mais de um locatário do Active Directory do Azure ou assinatura do Azure, você pode executar o seguinte Olá comando locatário correto do tooselect hello e assinatura:</span><span class="sxs-lookup"><span data-stu-id="8d7df-120">If your account is in more than one Azure Active Directory tenant or Azure subscription, you can run hello following command tooselect hello correct tenant and subscription:</span></span>
  
    ```powershell
        Login-AzureRMAccount -TenantId <TenantId> -SubscriptionId <subscriptionId>
    ```     
       
    <span data-ttu-id="8d7df-121">Executar Olá tooview de comando a seguir Olá selecionada locatário e assinatura:</span><span class="sxs-lookup"><span data-stu-id="8d7df-121">Run hello following command tooview hello currently selected tenant and subscription:</span></span>
    
    ```powershell
        Get-AzureRMContext
    ```

  4. <span data-ttu-id="8d7df-122">Executar Olá script a seguir</span><span class="sxs-lookup"><span data-stu-id="8d7df-122">Run hello following script</span></span>

    ```powershell
        .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -CertificateThumbprint "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX" -TenantId xxxxxxxx-xxxxx-xxxxx-xxxxx-xxxxxxxxxxxx
    ```

    <span data-ttu-id="8d7df-123">onde</span><span class="sxs-lookup"><span data-stu-id="8d7df-123">where</span></span>

    <span data-ttu-id="8d7df-124">**DisplayName** – nome de exibição do aplicativo ativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d7df-124">**DisplayName** - Azure Active Application display name.</span></span> <span data-ttu-id="8d7df-125">Se o aplicativo hello não existir, ele é criado no Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d7df-125">If hello application does not exist, it is created in Azure Active Directory.</span></span>

    <span data-ttu-id="8d7df-126">**Home page** -Olá home page do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8d7df-126">**HomePage** - hello home page of hello application.</span></span> <span data-ttu-id="8d7df-127">Você pode configurar uma URL fictícia, como saudação anterior de exemplo.</span><span class="sxs-lookup"><span data-stu-id="8d7df-127">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="8d7df-128">**IdentifierUri** -identificador de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="8d7df-128">**IdentifierUri** - Identifier of hello application.</span></span> <span data-ttu-id="8d7df-129">Você pode configurar uma URL fictícia, como saudação anterior de exemplo.</span><span class="sxs-lookup"><span data-stu-id="8d7df-129">You can configure a dummy URL, as in hello preceding example.</span></span>

    <span data-ttu-id="8d7df-130">**CertificateThumbprint** -impressão digital do certificado Olá instalado no nó de cabeçalho Olá na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="8d7df-130">**CertificateThumbprint** - Thumbprint of hello certificate you installed on hello head node in Step 1.</span></span>

    <span data-ttu-id="8d7df-131">**TenantId** – ID de locatário do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8d7df-131">**TenantId** - Tenant ID of your Azure Active Directory.</span></span> <span data-ttu-id="8d7df-132">Você pode obter Olá ID de locatário no portal do Azure Active Directory Olá **propriedades** página.</span><span class="sxs-lookup"><span data-stu-id="8d7df-132">You can get hello Tenant ID from hello Azure Active Directory portal **Properties** page.</span></span>

    <span data-ttu-id="8d7df-133">Para obter mais detalhes sobre **ConfigARMAutoGrowShrinkCert.ps1**, execute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span><span class="sxs-lookup"><span data-stu-id="8d7df-133">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`.</span></span>


* <span data-ttu-id="8d7df-134">**Para um cluster com um nó principal no Azure (modelo de implantação clássico)** - se você usar o cluster de Olá Olá HPC Pack IaaS implantação script toocreate no modelo de implantação clássico hello, habilitar Olá **AutoGrowShrink** cluster propriedade definindo a opção de AutoGrowShrink Olá no arquivo de configuração de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d7df-134">**For a cluster with a head node in Azure (classic deployment model)** - If you use hello HPC Pack IaaS deployment script toocreate hello cluster in hello classic deployment model, enable hello **AutoGrowShrink** cluster property by setting hello AutoGrowShrink option in hello cluster configuration file.</span></span> <span data-ttu-id="8d7df-135">Para obter detalhes, consulte a documentação de saudação que acompanha Olá [download do script](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="8d7df-135">For details, see hello documentation accompanying hello [script download](https://www.microsoft.com/download/details.aspx?id=44949).</span></span>

    <span data-ttu-id="8d7df-136">Como alternativa, habilitar Olá **AutoGrowShrink** comandos de propriedade de cluster depois de implantar o cluster hello usando o PowerShell HPC descrito em Olá seção a seguir.</span><span class="sxs-lookup"><span data-stu-id="8d7df-136">Alternatively, enable hello **AutoGrowShrink** cluster property after you deploy hello cluster by using HPC PowerShell commands described in hello following section.</span></span> <span data-ttu-id="8d7df-137">tooprepare para isso, primeiro Olá completo seguindo as etapas:</span><span class="sxs-lookup"><span data-stu-id="8d7df-137">tooprepare for this, first complete hello following steps:</span></span>

  1. <span data-ttu-id="8d7df-138">Configure um certificado de gerenciamento do Azure no nó de cabeçalho hello e no hello assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d7df-138">Configure an Azure management certificate on hello head node and in hello Azure subscription.</span></span> <span data-ttu-id="8d7df-139">Para uma implantação de teste, você pode usar saudação padrão do Microsoft HPC Azure certificado autoassinado que instala o HPC Pack no nó principal hello e carregue tooyour esse certificado assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d7df-139">For a test deployment, you can use hello Default Microsoft HPC Azure self-signed certificate that HPC Pack installs on hello head node, and then upload that certificate tooyour Azure subscription.</span></span> <span data-ttu-id="8d7df-140">Para opções e etapas, consulte Olá [orientação de biblioteca do TechNet](https://technet.microsoft.com/library/gg481759.aspx).</span><span class="sxs-lookup"><span data-stu-id="8d7df-140">For options and steps, see hello [TechNet Library guidance](https://technet.microsoft.com/library/gg481759.aspx).</span></span>

  2. <span data-ttu-id="8d7df-141">Executar **regedit** no nó principal do hello, vá tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo e adicione um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="8d7df-141">Run **regedit** on hello head node, go tooHKLM\SOFTWARE\Micorsoft\HPC\IaasInfo, and add a string value.</span></span> <span data-ttu-id="8d7df-142">Defina o nome do valor Olá muito "Impressão digital" e a impressão digital toohello de dados do valor do certificado Olá na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="8d7df-142">Set hello Value name too“ThumbPrint”, and Value data toohello thumbprint of hello certificate in Step 1.</span></span>

### <a name="hpc-powershell-commands-tooset-hello-autogrowshrink-property"></a><span data-ttu-id="8d7df-143">Propriedade AutoGrowShrink do HPC PowerShell comandos tooset Olá</span><span class="sxs-lookup"><span data-stu-id="8d7df-143">HPC PowerShell commands tooset hello AutoGrowShrink property</span></span>
<span data-ttu-id="8d7df-144">A seguir é tooset de comandos do exemplo do HPC PowerShell **AutoGrowShrink** e tootune seu comportamento com parâmetros adicionais.</span><span class="sxs-lookup"><span data-stu-id="8d7df-144">Following are sample HPC PowerShell commands tooset **AutoGrowShrink** and tootune its behavior with additional parameters.</span></span> <span data-ttu-id="8d7df-145">Consulte [AutoGrowShrink parâmetros](#AutoGrowShrink-parameters) posteriormente neste artigo para obter a lista completa Olá das configurações.</span><span class="sxs-lookup"><span data-stu-id="8d7df-145">See [AutoGrowShrink parameters](#AutoGrowShrink-parameters) later in this article for hello complete list of settings.</span></span>

<span data-ttu-id="8d7df-146">toorun esses comandos, inicie o PowerShell do HPC no nó principal do cluster Olá como um administrador.</span><span class="sxs-lookup"><span data-stu-id="8d7df-146">toorun these commands, start HPC PowerShell on hello cluster head node as an administrator.</span></span>

<span data-ttu-id="8d7df-147">**Olá tooenable propriedade AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="8d7df-147">**tooenable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 1
```

<span data-ttu-id="8d7df-148">**Olá toodisable propriedade AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="8d7df-148">**toodisable hello AutoGrowShrink property**</span></span>

```powershell
Set-HpcClusterProperty –EnableGrowShrink 0
```

<span data-ttu-id="8d7df-149">**Olá toochange aumentar o intervalo em minutos**</span><span class="sxs-lookup"><span data-stu-id="8d7df-149">**toochange hello grow interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –GrowInterval <interval>
```

<span data-ttu-id="8d7df-150">**Olá toochange reduzir o intervalo em minutos**</span><span class="sxs-lookup"><span data-stu-id="8d7df-150">**toochange hello shrink interval in minutes**</span></span>

```powershell
Set-HpcClusterProperty –ShrinkInterval <interval>
```

<span data-ttu-id="8d7df-151">**configuração atual do hello tooview de AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="8d7df-151">**tooview hello current configuration of AutoGrowShrink**</span></span>

```powershell
Get-HpcClusterProperty –AutoGrowShrink
```

<span data-ttu-id="8d7df-152">**grupos de nó de tooexclude de AutoGrowShrink**</span><span class="sxs-lookup"><span data-stu-id="8d7df-152">**tooexclude node groups from AutoGrowShrink**</span></span>

```powershell
Set-HpcClusterProperty –ExcludeNodeGroups <group1,group2,group3>
```

>[!NOTE] 
> <span data-ttu-id="8d7df-153">Esse parâmetro tem suporte do HPC Pack 2016</span><span class="sxs-lookup"><span data-stu-id="8d7df-153">This parameter is supported starting in HPC Pack 2016</span></span>
>

### <a name="autogrowshrink-parameters"></a><span data-ttu-id="8d7df-154">parâmetros de AutoGrowShrink</span><span class="sxs-lookup"><span data-stu-id="8d7df-154">AutoGrowShrink parameters</span></span>
<span data-ttu-id="8d7df-155">Olá seguem AutoGrowShrink parâmetros que podem ser modificados usando Olá **HpcClusterProperty conjunto** comando.</span><span class="sxs-lookup"><span data-stu-id="8d7df-155">hello following are AutoGrowShrink parameters that you can modify by using hello **Set-HpcClusterProperty** command.</span></span>

* <span data-ttu-id="8d7df-156">**EnableGrowShrink** - alternar tooenable ou desabilitar Olá **AutoGrowShrink** propriedade.</span><span class="sxs-lookup"><span data-stu-id="8d7df-156">**EnableGrowShrink** - Switch tooenable or disable hello **AutoGrowShrink** property.</span></span>
* <span data-ttu-id="8d7df-157">**ParamSweepTasksPerCore** -número de limpeza paramétrica tarefas toogrow um núcleo.</span><span class="sxs-lookup"><span data-stu-id="8d7df-157">**ParamSweepTasksPerCore** - Number of parametric sweep tasks toogrow one core.</span></span> <span data-ttu-id="8d7df-158">padrão de saudação é um núcleo toogrow por tarefa.</span><span class="sxs-lookup"><span data-stu-id="8d7df-158">hello default is toogrow one core per task.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8d7df-159">Alterações de HPC Pack QFE KB3134307 **ParamSweepTasksPerCore** muito**TasksPerResourceUnit**.</span><span class="sxs-lookup"><span data-stu-id="8d7df-159">HPC Pack QFE KB3134307 changes **ParamSweepTasksPerCore** too**TasksPerResourceUnit**.</span></span> <span data-ttu-id="8d7df-160">Ele se baseia no tipo de recurso de trabalho hello e pode ser nó, soquete ou core.</span><span class="sxs-lookup"><span data-stu-id="8d7df-160">It is based on hello job resource type and can be node, socket, or core.</span></span>
  >
  >
* <span data-ttu-id="8d7df-161">**GrowThreshold** -limite de crescimento automático de tootrigger de tarefas na fila.</span><span class="sxs-lookup"><span data-stu-id="8d7df-161">**GrowThreshold** - Threshold of queued tasks tootrigger automatic growth.</span></span> <span data-ttu-id="8d7df-162">padrão de saudação é 1, o que significa que, se há 1 ou mais tarefas Olá estado na fila, aumentar automaticamente nós.</span><span class="sxs-lookup"><span data-stu-id="8d7df-162">hello default is 1, which means that if there are 1 or more tasks in hello queued state, automatically grow nodes.</span></span>
* <span data-ttu-id="8d7df-163">**GrowInterval** -intervalo de aumento automático de tootrigger minutos.</span><span class="sxs-lookup"><span data-stu-id="8d7df-163">**GrowInterval** - Interval in minutes tootrigger automatic growth.</span></span> <span data-ttu-id="8d7df-164">intervalo padrão de saudação é de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="8d7df-164">hello default interval is 5 minutes.</span></span>
* <span data-ttu-id="8d7df-165">**ShrinkInterval** -intervalo em minutos tootrigger redução automática.</span><span class="sxs-lookup"><span data-stu-id="8d7df-165">**ShrinkInterval** - Interval in minutes tootrigger automatic shrinking.</span></span> <span data-ttu-id="8d7df-166">intervalo padrão de saudação é de 5 minutos. |</span><span class="sxs-lookup"><span data-stu-id="8d7df-166">hello default interval is 5 minutes.|</span></span>
* <span data-ttu-id="8d7df-167">**ShrinkIdleTimes** -número de verificações contínua tooshrink tooindicate Olá nós está ocioso.</span><span class="sxs-lookup"><span data-stu-id="8d7df-167">**ShrinkIdleTimes** - Number of continuous checks tooshrink tooindicate hello nodes are idle.</span></span> <span data-ttu-id="8d7df-168">padrão de saudação é 3 vezes.</span><span class="sxs-lookup"><span data-stu-id="8d7df-168">hello default is 3 times.</span></span> <span data-ttu-id="8d7df-169">Por exemplo, se hello **ShrinkInterval** é de 5 minutos, HPC Pack verifica se o nó de saudação está ocioso a cada 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="8d7df-169">For example, if hello **ShrinkInterval** is 5 minutes, HPC Pack checks whether hello node is idle every 5 minutes.</span></span> <span data-ttu-id="8d7df-170">Se nós Olá estiverem em estado ocioso Olá após 3 contínua verifica (15 minutos), o HPC Pack reduz nesse nó.</span><span class="sxs-lookup"><span data-stu-id="8d7df-170">If hello nodes are in hello idle state after 3 continuous checks (15 minutes), then HPC Pack shrinks that node.</span></span>
* <span data-ttu-id="8d7df-171">**ExtraNodesGrowRatio** -porcentagem adicional de nós toogrow para trabalhos de Interface MPI (Message Passing).</span><span class="sxs-lookup"><span data-stu-id="8d7df-171">**ExtraNodesGrowRatio** - Additional percentage of nodes toogrow for Message Passing Interface (MPI) jobs.</span></span> <span data-ttu-id="8d7df-172">valor padrão de saudação é 1, o que significa que o HPC Pack cresce nós % 1 para trabalhos MPI.</span><span class="sxs-lookup"><span data-stu-id="8d7df-172">hello default value is 1, which means that HPC Pack grows nodes 1% for MPI jobs.</span></span>
* <span data-ttu-id="8d7df-173">**GrowByMin** -alternar tooindicate se a política de aumento automático de saudação baseia-se no mínimo de recursos necessário para o trabalho de saudação do hello.</span><span class="sxs-lookup"><span data-stu-id="8d7df-173">**GrowByMin** - Switch tooindicate whether hello autogrow policy is based on hello minimum resources required for hello job.</span></span> <span data-ttu-id="8d7df-174">padrão de saudação é false, o que significa que o HPC Pack cresce nós para trabalhos com base nos recursos de máximo de saudação necessários para trabalhos de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d7df-174">hello default is false, which means that HPC Pack grows nodes for jobs based on hello maximum resources required for hello jobs.</span></span>
* <span data-ttu-id="8d7df-175">**SoaJobGrowThreshold** -processo de aumento de limite de entrada SOA solicitações tootrigger Olá automática.</span><span class="sxs-lookup"><span data-stu-id="8d7df-175">**SoaJobGrowThreshold** - Threshold of incoming SOA requests tootrigger hello automatic grow process.</span></span> <span data-ttu-id="8d7df-176">valor padrão de saudação é 50000.</span><span class="sxs-lookup"><span data-stu-id="8d7df-176">hello default value is 50000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8d7df-177">Esse parâmetro tem suporte a partir do HPC Pack 2012 R2 Atualização 3.</span><span class="sxs-lookup"><span data-stu-id="8d7df-177">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
  >
* <span data-ttu-id="8d7df-178">**SoaRequestsPerCore** -número de entrada SOA solicitações toogrow um núcleo.</span><span class="sxs-lookup"><span data-stu-id="8d7df-178">**SoaRequestsPerCore** -Number of incoming SOA requests toogrow one core.</span></span> <span data-ttu-id="8d7df-179">valor padrão de saudação é 20.000.</span><span class="sxs-lookup"><span data-stu-id="8d7df-179">hello default value is 20000.</span></span>

  > [!NOTE]
  > <span data-ttu-id="8d7df-180">Esse parâmetro tem suporte a partir do HPC Pack 2012 R2 Atualização 3.</span><span class="sxs-lookup"><span data-stu-id="8d7df-180">This parameter is supported starting in HPC Pack 2012 R2 Update 3.</span></span>
  >
* <span data-ttu-id="8d7df-181">**ExcludeNodeGroups** – nós Olá especificado grupos de nó automaticamente aumentar ou encolher.</span><span class="sxs-lookup"><span data-stu-id="8d7df-181">**ExcludeNodeGroups** – Nodes in hello specified node groups do not automatically grow and shrink.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="8d7df-182">Esse parâmetro tem suporte do HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="8d7df-182">This parameter is supported starting in HPC Pack 2016.</span></span>
  >

### <a name="mpi-example"></a><span data-ttu-id="8d7df-183">Exemplo de MPI</span><span class="sxs-lookup"><span data-stu-id="8d7df-183">MPI example</span></span>
<span data-ttu-id="8d7df-184">Por padrão o HPC Pack cresce % 1 nós extras para trabalhos MPI (**ExtraNodesGrowRatio** está definida too1).</span><span class="sxs-lookup"><span data-stu-id="8d7df-184">By default HPC Pack grows 1% extra nodes for MPI jobs (**ExtraNodesGrowRatio** is set too1).</span></span> <span data-ttu-id="8d7df-185">motivo da saudação é que MPI pode exigir vários nós e trabalho Olá pode ser executada somente quando todos os nós estão prontos.</span><span class="sxs-lookup"><span data-stu-id="8d7df-185">hello reason is that MPI may require multiple nodes, and hello job can only run when all nodes are ready.</span></span> <span data-ttu-id="8d7df-186">Quando o Azure inicia nós, ocasionalmente, um nó talvez seja necessário mais toostart de tempo que outras pessoas, fazendo com que outros toobe nós ocioso enquanto aguarda que tooget nó pronto.</span><span class="sxs-lookup"><span data-stu-id="8d7df-186">When Azure starts nodes, occasionally one node might need more time toostart than others, causing other nodes toobe idle while waiting for that node tooget ready.</span></span> <span data-ttu-id="8d7df-187">Ao aumentar nós extras, o HPC Pack reduz o tempo de espera desse recurso e potencialmente reduz os custos.</span><span class="sxs-lookup"><span data-stu-id="8d7df-187">By growing extra nodes, HPC Pack reduces this resource waiting time, and potentially saves costs.</span></span> <span data-ttu-id="8d7df-188">Porcentagem de saudação tooincrease de nós extras para trabalhos MPI (por exemplo, % too10), execute um comando semelhante a</span><span class="sxs-lookup"><span data-stu-id="8d7df-188">tooincrease hello percentage of extra nodes for MPI jobs (for example, too10%), run a command similar to</span></span>

    Set-HpcClusterProperty -ExtraNodesGrowRatio 10

### <a name="soa-example"></a><span data-ttu-id="8d7df-189">Exemplo de SOA</span><span class="sxs-lookup"><span data-stu-id="8d7df-189">SOA example</span></span>
<span data-ttu-id="8d7df-190">Por padrão, **SoaJobGrowThreshold** é definir too50000 e **SoaRequestsPerCore** está definida too200000.</span><span class="sxs-lookup"><span data-stu-id="8d7df-190">By default, **SoaJobGrowThreshold** is set too50000 and **SoaRequestsPerCore** is set too200000.</span></span> <span data-ttu-id="8d7df-191">Se você enviar um trabalho SOA com 70000 solicitações, há uma tarefa na fila e as solicitações de entrada serão 70000.</span><span class="sxs-lookup"><span data-stu-id="8d7df-191">If you submit one SOA job with 70000 requests, there is one queued task and incoming requests are 70000.</span></span> <span data-ttu-id="8d7df-192">Nesse caso o HPC Pack cresce 1 núcleo para hello na fila de tarefas e solicitações de entrada, cresce (50000 70000) / 20000 = 1 núcleo, no total cresce 2 núcleos para este trabalho SOA.</span><span class="sxs-lookup"><span data-stu-id="8d7df-192">In this case HPC Pack grows 1 core for hello queued task, and for incoming requests, grows (70000 - 50000)/20000 = 1 core, so in total grows 2 cores for this SOA job.</span></span>

## <a name="run-hello-azureautogrowshrinkps1-script"></a><span data-ttu-id="8d7df-193">Executar script de AzureAutoGrowShrink.ps1 Olá</span><span class="sxs-lookup"><span data-stu-id="8d7df-193">Run hello AzureAutoGrowShrink.ps1 script</span></span>
### <a name="prerequisites"></a><span data-ttu-id="8d7df-194">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8d7df-194">Prerequisites</span></span>

* <span data-ttu-id="8d7df-195">**HPC Pack 2012 R2 Update 1 ou posterior cluster** - Olá **AzureAutoGrowShrink.ps1** script está instalado na pasta % CCP_HOME % bin hello.</span><span class="sxs-lookup"><span data-stu-id="8d7df-195">**HPC Pack 2012 R2 Update 1 or later cluster** - hello **AzureAutoGrowShrink.ps1** script is installed in hello %CCP_HOME%bin folder.</span></span> <span data-ttu-id="8d7df-196">nó principal do cluster Olá pode ser implantado no local ou em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d7df-196">hello cluster head node can be deployed either on-premises or in an Azure VM.</span></span> <span data-ttu-id="8d7df-197">Consulte [configurar um cluster híbrido com o HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget iniciado conosco de "Disparo" do Azure e um nó principal local.</span><span class="sxs-lookup"><span data-stu-id="8d7df-197">See [Set up a hybrid cluster with HPC Pack](../../../cloud-services/cloud-services-setup-hybrid-hpcpack-cluster.md) tooget started with an on-premises head node and Azure "burst" nodes.</span></span> <span data-ttu-id="8d7df-198">Consulte Olá [script de implantação IaaS do HPC Pack](hpcpack-cluster-powershell-script.md) tooquickly implantar um cluster de HPC Pack em VMs do Azure ou use um [modelo de início rápido do Azure](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span><span class="sxs-lookup"><span data-stu-id="8d7df-198">See hello [HPC Pack IaaS deployment script](hpcpack-cluster-powershell-script.md) tooquickly deploy an HPC Pack cluster in Azure VMs, or use an [Azure quickstart template](https://azure.microsoft.com/documentation/templates/create-hpc-cluster/).</span></span>
* <span data-ttu-id="8d7df-199">**O Azure PowerShell 1.4.0** -script hello depende atualmente essa versão específica do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d7df-199">**Azure PowerShell 1.4.0** - hello script currently depends on this specific version of Azure PowerShell.</span></span>
* <span data-ttu-id="8d7df-200">**Para um cluster com o Azure burst nós** -executar script hello em um computador cliente onde o HPC Pack está instalado, ou no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="8d7df-200">**For a cluster with Azure burst nodes** - Run hello script on a client computer where HPC Pack is installed, or on hello head node.</span></span> <span data-ttu-id="8d7df-201">Se em execução em um computador cliente, certifique-se de que você defina Olá variável $env: nó de cabeçalho CCP_SCHEDULER toopoint toohello.</span><span class="sxs-lookup"><span data-stu-id="8d7df-201">If running on a client computer, ensure that you set hello variable $env:CCP_SCHEDULER toopoint toohello head node.</span></span> <span data-ttu-id="8d7df-202">Hello Azure "disparar" nós devem ser adicionados toohello cluster, mas elas podem estar no estado não implantado de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d7df-202">hello Azure “burst” nodes must be added toohello cluster, but they may be in hello Not-Deployed state.</span></span>
* <span data-ttu-id="8d7df-203">**Para um cluster implantado em VMs do Azure (modelo de implantação do Gerenciador de recursos)** -para um cluster de máquinas virtuais do Azure implantados no modelo de implantação do Gerenciador de recursos de saudação, o script hello dá suporte a dois métodos de autenticação do Azure: entrar tooyour conta do Azure script de saudação toorun sempre (executando `Login-AzureRmAccount`, ou configurar um tooauthenticate principal do serviço com um certificado.</span><span class="sxs-lookup"><span data-stu-id="8d7df-203">**For a cluster deployed in Azure VMs (Resource Manager deployment model)** - For a cluster of Azure VMs deployed in hello Resource Manager deployment model, hello script supports two methods for Azure authentication: sign in tooyour Azure account toorun hello script every time (by running `Login-AzureRmAccount`, or configure a service principal tooauthenticate with a certificate.</span></span> <span data-ttu-id="8d7df-204">HPC Pack fornece o script hello **ConfigARMAutoGrowShrinkCert.ps** toocreate uma entidade de serviço com o certificado.</span><span class="sxs-lookup"><span data-stu-id="8d7df-204">HPC Pack provides hello script **ConfigARMAutoGrowShrinkCert.ps** toocreate a service principal with certificate.</span></span> <span data-ttu-id="8d7df-205">script Hello cria um aplicativo do Azure Active Directory (AD do Azure) e uma entidade de serviço e atribui a entidade de serviço Olá Colaborador função toohello.</span><span class="sxs-lookup"><span data-stu-id="8d7df-205">hello script creates an Azure Active Directory (Azure AD) application and a service principal, and assigns hello Contributor role toohello service principal.</span></span> <span data-ttu-id="8d7df-206">script de saudação toorun, inicie o PowerShell do Azure como administrador e execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="8d7df-206">toorun hello script, start Azure PowerShell  as administrator and run hello following commands:</span></span>

    ```powershell
    cd $env:CCP_HOME\bin

    Login-AzureRmAccount

    .\ConfigARMAutoGrowShrinkCert.ps1 -DisplayName “YourHpcPackAppName” -HomePage "https://YourHpcPackAppHomePage" -IdentifierUri "https://YourHpcPackAppUri" -PfxFile "d:\yourcertificate.pfx"
    ```

    <span data-ttu-id="8d7df-207">Para obter mais detalhes sobre **ConfigARMAutoGrowShrinkCert.ps1**, execute `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span><span class="sxs-lookup"><span data-stu-id="8d7df-207">For more details about **ConfigARMAutoGrowShrinkCert.ps1**, run `Get-Help .\ConfigARMAutoGrowShrinkCert.ps1 -Detailed`,</span></span>

* <span data-ttu-id="8d7df-208">**Para um cluster implantado em VMs do Azure (modelo de implantação clássico)** -executar script hello no nó de cabeçalho Olá VM, porque depende de saudação **Start-hpciaasnode.ps1** e **Stop-hpciaasnode.ps1**scripts que estão instalados lá.</span><span class="sxs-lookup"><span data-stu-id="8d7df-208">**For a cluster deployed in Azure VMs (classic deployment model)** - Run hello script on hello head node VM, because it depends on hello **Start-HpcIaaSNode.ps1** and **Stop-HpcIaaSNode.ps1** scripts that are installed there.</span></span> <span data-ttu-id="8d7df-209">Além disso, esses scripts exigem um certificado de gerenciamento ou um arquivo de configurações de publicação do Azure (veja [Gerenciar nós de computação em um cluster HPC Pack no Azure](hpcpack-cluster-node-manage.md)).</span><span class="sxs-lookup"><span data-stu-id="8d7df-209">Those scripts additionally require an Azure management certificate or publish settings file (see [Manage compute nodes in an HPC Pack cluster in Azure](hpcpack-cluster-node-manage.md)).</span></span> <span data-ttu-id="8d7df-210">Certifique-se de saudação todas as VMs, você precisa do nó já foram adicionadas toohello cluster de computação.</span><span class="sxs-lookup"><span data-stu-id="8d7df-210">Make sure all hello compute node VMs you need are already added toohello cluster.</span></span> <span data-ttu-id="8d7df-211">Elas podem estar no estado parado de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d7df-211">They may be in hello Stopped state.</span></span>



### <a name="syntax"></a><span data-ttu-id="8d7df-212">Sintaxe</span><span class="sxs-lookup"><span data-stu-id="8d7df-212">Syntax</span></span>
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
### <a name="parameters"></a><span data-ttu-id="8d7df-213">parâmetros</span><span class="sxs-lookup"><span data-stu-id="8d7df-213">Parameters</span></span>
* <span data-ttu-id="8d7df-214">**NodeTemplates** -nomes de toodefine de modelos de nó Olá Olá Olá nós toogrow escopo e reduzir.</span><span class="sxs-lookup"><span data-stu-id="8d7df-214">**NodeTemplates** - Names of hello node templates toodefine hello scope for hello nodes toogrow and shrink.</span></span> <span data-ttu-id="8d7df-215">Se não for especificado (valor padrão de saudação é @()), todos os nós no hello **AzureNodes** grupo de nó estão no escopo quando **NodeType** tem um valor de AzureNodes e todos os nós na Olá **ComputeNodes** grupo de nó estão no escopo quando **NodeType** tem um valor de ComputeNodes.</span><span class="sxs-lookup"><span data-stu-id="8d7df-215">If not specified (hello default value is @()), all nodes in hello **AzureNodes** node group are in scope when **NodeType** has a value of AzureNodes, and all nodes in hello **ComputeNodes** node group are in scope when **NodeType** has a value of ComputeNodes.</span></span>
* <span data-ttu-id="8d7df-216">**Os JobTemplates** -nomes de saudação modelos toodefine Olá escopo Olá toogrow de nós de trabalho.</span><span class="sxs-lookup"><span data-stu-id="8d7df-216">**JobTemplates** - Names of hello job templates toodefine hello scope for hello nodes toogrow.</span></span>
* <span data-ttu-id="8d7df-217">**NodeType** - Olá tipo de nó toogrow e reduzir.</span><span class="sxs-lookup"><span data-stu-id="8d7df-217">**NodeType** - hello type of node toogrow and shrink.</span></span> <span data-ttu-id="8d7df-218">Os valores para os quais há suporte são:</span><span class="sxs-lookup"><span data-stu-id="8d7df-218">Supported values are:</span></span>

  * <span data-ttu-id="8d7df-219">**AzureNodes** – para os nós (de disparo contínuo) de PaaS do Azure em cluster local ou de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d7df-219">**AzureNodes** – for Azure PaaS (burst) nodes in an on-premises or Azure IaaS cluster.</span></span>
  * <span data-ttu-id="8d7df-220">**ComputeNodes** - para VMs de nó de computação apenas em um cluster de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d7df-220">**ComputeNodes** - for compute node VMs only in an Azure IaaS cluster.</span></span>

* <span data-ttu-id="8d7df-221">**NumOfQueuedJobsPerNodeToGrow** -número de trabalhos em fila necessário toogrow um nó.</span><span class="sxs-lookup"><span data-stu-id="8d7df-221">**NumOfQueuedJobsPerNodeToGrow** - Number of queued jobs required toogrow one node.</span></span>
* <span data-ttu-id="8d7df-222">**NumOfQueuedJobsToGrowThreshold** -número de limite de saudação de saudação de toostart trabalhos em fila cresça processo.</span><span class="sxs-lookup"><span data-stu-id="8d7df-222">**NumOfQueuedJobsToGrowThreshold** - hello threshold number of queued jobs toostart hello grow process.</span></span>
* <span data-ttu-id="8d7df-223">**NumOfActiveQueuedTasksPerNodeToGrow** -número de saudação de tarefas ativas em fila necessário toogrow um nó.</span><span class="sxs-lookup"><span data-stu-id="8d7df-223">**NumOfActiveQueuedTasksPerNodeToGrow** - hello number of active queued tasks required toogrow one node.</span></span> <span data-ttu-id="8d7df-224">Se **NumOfQueuedJobsPerNodeToGrow** for especificado com um valor maior que 0, esse parâmetro será ignorado.</span><span class="sxs-lookup"><span data-stu-id="8d7df-224">If **NumOfQueuedJobsPerNodeToGrow** is specified with a value greater than 0, this parameter is ignored.</span></span>
* <span data-ttu-id="8d7df-225">**NumOfActiveQueuedTasksToGrowThreshold** -número de limite de saudação de saudação do toostart tarefas ativas em fila cresça processo.</span><span class="sxs-lookup"><span data-stu-id="8d7df-225">**NumOfActiveQueuedTasksToGrowThreshold** - hello threshold number of active queued tasks toostart hello grow process.</span></span>
* <span data-ttu-id="8d7df-226">**NumOfInitialNodesToGrow** - Olá inicial número mínimo de nós toogrow se todos os nós de saudação no escopo são **não implantado** ou **parado (desalocado)**.</span><span class="sxs-lookup"><span data-stu-id="8d7df-226">**NumOfInitialNodesToGrow** - hello initial minimum number of nodes toogrow if all hello nodes in scope are **Not-Deployed** or **Stopped (Deallocated)**.</span></span>
* <span data-ttu-id="8d7df-227">**GrowCheckIntervalMins** -intervalo de saudação em minutos entre verifica toogrow.</span><span class="sxs-lookup"><span data-stu-id="8d7df-227">**GrowCheckIntervalMins** - hello interval in minutes between checks toogrow.</span></span>
* <span data-ttu-id="8d7df-228">**ShrinkCheckIntervalMins** -intervalo de saudação em minutos entre verifica tooshrink.</span><span class="sxs-lookup"><span data-stu-id="8d7df-228">**ShrinkCheckIntervalMins** - hello interval in minutes between checks tooshrink.</span></span>
* <span data-ttu-id="8d7df-229">**ShrinkCheckIdleTimes** -Olá número de verificações de redução contínuas (separadas por **ShrinkCheckIntervalMins**) tooindicate Olá nós estão ociosos.</span><span class="sxs-lookup"><span data-stu-id="8d7df-229">**ShrinkCheckIdleTimes** - hello number of continuous shrink checks (separated by **ShrinkCheckIntervalMins**) tooindicate hello nodes are idle.</span></span>
* <span data-ttu-id="8d7df-230">**UseLastConfigurations** -Olá configurações anteriores salvas no arquivo de argumento de saudação.</span><span class="sxs-lookup"><span data-stu-id="8d7df-230">**UseLastConfigurations** - hello previous configurations saved in hello argument file.</span></span>
* <span data-ttu-id="8d7df-231">**ArgFile**- Olá nome da saudação argumento arquivo usado toosave e Olá configurações toorun Olá script de atualização.</span><span class="sxs-lookup"><span data-stu-id="8d7df-231">**ArgFile**- hello name of hello argument file used toosave and update hello configurations toorun hello script.</span></span>
* <span data-ttu-id="8d7df-232">**LogFilePrefix** -nome do prefixo Olá Olá do arquivo de log.</span><span class="sxs-lookup"><span data-stu-id="8d7df-232">**LogFilePrefix** - hello prefix name of hello log file.</span></span> <span data-ttu-id="8d7df-233">Você pode especificar um caminho.</span><span class="sxs-lookup"><span data-stu-id="8d7df-233">You can specify a path.</span></span> <span data-ttu-id="8d7df-234">Por padrão o log de saudação é escrito toohello diretório de trabalho atual.</span><span class="sxs-lookup"><span data-stu-id="8d7df-234">By default hello log is written toohello current working directory.</span></span>

### <a name="example-1"></a><span data-ttu-id="8d7df-235">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="8d7df-235">Example 1</span></span>
<span data-ttu-id="8d7df-236">Olá, exemplo a seguir configura hello Azure intermitente nós implantados com o modelo AzureNode padrão toogrow e reduzir automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8d7df-236">hello following example configures hello Azure burst nodes deployed with the Default AzureNode Template toogrow and shrink automatically.</span></span> <span data-ttu-id="8d7df-237">Se todos os nós estão inicialmente em Olá **não implantado** estado, pelo menos 3 nós serão iniciados.</span><span class="sxs-lookup"><span data-stu-id="8d7df-237">If all the nodes are initially in hello **Not-Deployed** state, at least 3 nodes are started.</span></span> <span data-ttu-id="8d7df-238">Se o número de saudação de trabalhos em fila exceder 8, o script hello inicia nós até seu número excede a taxa de saudação de trabalhos em fila para **NumOfQueuedJobsPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="8d7df-238">If hello number of queued jobs exceeds 8, hello script starts nodes until their number exceeds hello ratio of queued jobs to **NumOfQueuedJobsPerNodeToGrow**.</span></span> <span data-ttu-id="8d7df-239">Se um nó for encontrado toobe ocioso por 3 vezes consecutivas, ele será interrompido.</span><span class="sxs-lookup"><span data-stu-id="8d7df-239">If a node is found toobe idle in 3 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates @('Default AzureNode
 Template') -NodeType AzureNodes -NumOfQueuedJobsPerNodeToGrow 5
 -NumOfQueuedJobsToGrowThreshold 8 -NumOfInitialNodesToGrow 3
 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 3
```

### <a name="example-2"></a><span data-ttu-id="8d7df-240">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="8d7df-240">Example 2</span></span>
<span data-ttu-id="8d7df-241">Olá, exemplo a seguir configura hello Azure implantadas com hello modelo ComputeNode padrão toogrow VMs do nó de computação e reduzir automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8d7df-241">hello following example configures hello Azure compute node VMs deployed with hello Default ComputeNode Template toogrow and shrink automatically.</span></span>
<span data-ttu-id="8d7df-242">trabalhos Olá configurados pelo modelo de trabalho padrão Olá definem escopo de saudação da carga de trabalho no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="8d7df-242">hello jobs configured by hello Default job template define hello scope of the workload on hello cluster.</span></span> <span data-ttu-id="8d7df-243">Se todos os nós de saudação forem interrompidos inicialmente, pelo menos 5 nós serão iniciados.</span><span class="sxs-lookup"><span data-stu-id="8d7df-243">If all hello nodes are initially stopped, at least 5 nodes are started.</span></span> <span data-ttu-id="8d7df-244">Se o número de saudação de tarefas ativas em fila exceder 15, o script hello inicia nós até seu número excede a taxa de saudação de tarefas ativas em fila muito**NumOfActiveQueuedTasksPerNodeToGrow**.</span><span class="sxs-lookup"><span data-stu-id="8d7df-244">If hello number of active queued tasks exceeds 15, hello script starts nodes until their number exceeds hello ratio of active queued tasks too**NumOfActiveQueuedTasksPerNodeToGrow**.</span></span> <span data-ttu-id="8d7df-245">Se um nó for encontrado toobe ocioso em 10 vezes consecutivas, ele será interrompido.</span><span class="sxs-lookup"><span data-stu-id="8d7df-245">If a node is found toobe idle in 10 consecutive idle times, it is stopped.</span></span>

```powershell
.\AzureAutoGrowShrink.ps1 -NodeTemplates 'Default ComputeNode Template' -JobTemplates 'Default' -NodeType ComputeNodes -NumOfActiveQueuedTasksPerNodeToGrow 10 -NumOfActiveQueuedTasksToGrowThreshold 15 -NumOfInitialNodesToGrow 5 -GrowCheckIntervalMins 1 -ShrinkCheckIntervalMins 1 -ShrinkCheckIdleTimes 10 -ArgFile 'IaaSVMComputeNodes_Arg.xml' -LogFilePrefix 'IaaSVMComputeNodes_log'
```
