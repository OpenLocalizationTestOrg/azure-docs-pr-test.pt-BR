---
title: aaaHPC pacote de cluster para o Excel e SOA | Microsoft Docs
description: "Introdução à execução de cargas de trabalho SOA e Excel em larga escala em um cluster HPC Pack no Azure"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-resource-manager,hpc-pack
ms.assetid: cb6a9abe-caf3-44da-b911-849a50f6cfb3
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/01/2017
ms.author: danlep
ms.openlocfilehash: 55b4b2c25fe65d06b75025cc23c3c13b8b764238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="0fa00-103">Introdução à execução de cargas de trabalho do Excel e SOA em um cluster HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="0fa00-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="0fa00-104">Este artigo mostra como toodeploy um Microsoft HPC Pack 2012 R2 cluster em máquinas virtuais do Azure usando um modelo de início rápido do Azure, ou, opcionalmente, um script de implantação do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0fa00-104">This article shows you how toodeploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="0fa00-105">cluster Olá usa toorun projetadas de imagens de VM do Azure Marketplace Microsoft Excel ou cargas de trabalho de arquitetura orientada a serviços (SOA) com o HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="0fa00-105">hello cluster uses Azure Marketplace VM images designed toorun Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="0fa00-106">Você pode usar o hello toorun de cluster HPC do Excel e serviços SOA de um computador de cliente local.</span><span class="sxs-lookup"><span data-stu-id="0fa00-106">You can use hello cluster toorun Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="0fa00-107">serviços do Excel HPC Olá incluem descarregamento de pasta de trabalho do Excel e funções definidas pelo usuário do Excel ou UDFs.</span><span class="sxs-lookup"><span data-stu-id="0fa00-107">hello Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="0fa00-108">Este artigo se baseia em recursos, modelos e scripts do HPC Pack 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="0fa00-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="0fa00-109">Atualmente, este cenário não tem suporte no HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="0fa00-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="0fa00-110">Em um nível alto, hello diagrama a seguir mostra o cluster de HPC Pack Olá que você criar.</span><span class="sxs-lookup"><span data-stu-id="0fa00-110">At a high level, hello following diagram shows hello HPC Pack cluster you create.</span></span>

![Cluster HPC com nós que executam cargas de trabalho do Excel][scenario]

## <a name="prerequisites"></a><span data-ttu-id="0fa00-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0fa00-112">Prerequisites</span></span>
* <span data-ttu-id="0fa00-113">**Computador cliente** -pode ser necessário um cliente baseado em Windows computador toosubmit exemplo do Excel e SOA trabalhos toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa00-113">**Client computer** - You need a Windows-based client computer toosubmit sample Excel and SOA jobs toohello cluster.</span></span> <span data-ttu-id="0fa00-114">Você também precisará uma saudação de toorun de computador do Windows Azure PowerShell script de implantação de cluster (se você escolher esse método de implantação).</span><span class="sxs-lookup"><span data-stu-id="0fa00-114">You also need a Windows computer toorun hello Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="0fa00-115">**Assinatura do Azure** – Se não tiver uma, você poderá criar uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="0fa00-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="0fa00-116">**Cota de núcleos** -você pode precisar de uma cota de Olá tooincrease de núcleos, especialmente se você implantar vários nós de cluster com tamanhos VM com vários núcleos.</span><span class="sxs-lookup"><span data-stu-id="0fa00-116">**Cores quota** - You might need tooincrease hello quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="0fa00-117">Se você estiver usando um modelo de início rápido do Azure, a cota de núcleos Olá no Gerenciador de recursos é por região do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fa00-117">If you are using an Azure quickstart template, hello cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="0fa00-118">Nesse caso, você pode precisar de uma cota de saudação tooincrease em uma região específica.</span><span class="sxs-lookup"><span data-stu-id="0fa00-118">In that case, you might need tooincrease hello quota in a specific region.</span></span> <span data-ttu-id="0fa00-119">Consulte [Assinatura do Azure e limite de serviços, cotas e restrições](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="0fa00-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="0fa00-120">uma cota de tooincrease [abrir uma solicitação de suporte do cliente online](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) sem custo adicional.</span><span class="sxs-lookup"><span data-stu-id="0fa00-120">tooincrease a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="0fa00-121">**Licença do Microsoft Office** – se você implantar nós de computação usando uma imagem de VM do Marketplace HPC Pack 2012 R2 com Microsoft Excel, uma versão de avaliação de 30 dias do Microsoft Excel Professional Plus 2013 será instalada.</span><span class="sxs-lookup"><span data-stu-id="0fa00-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="0fa00-122">Após o período de avaliação do hello, você precisa tooprovide um válido Microsoft Office licença tooactivate Excel toocontinue toorun cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0fa00-122">After hello evaluation period, you need tooprovide a valid Microsoft Office license tooactivate Excel toocontinue toorun workloads.</span></span> <span data-ttu-id="0fa00-123">Confira [Ativação do Excel](#excel-activation) mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="0fa00-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="0fa00-124">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="0fa00-124">Step 1.</span></span> <span data-ttu-id="0fa00-125">Configurar um cluster de HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="0fa00-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="0fa00-126">Mostramos dois tooset opções cluster de HPC Pack 2012 R2 Olá: primeiro, usando um modelo de início rápido do Azure e Olá portal do Azure; e, segundo, usando um script de implantação do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="0fa00-126">We show two options tooset up hello HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and hello Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="0fa00-127">Opção 1.</span><span class="sxs-lookup"><span data-stu-id="0fa00-127">Option 1.</span></span> <span data-ttu-id="0fa00-128">Usar um modelo de início rápido</span><span class="sxs-lookup"><span data-stu-id="0fa00-128">Use a quickstart template</span></span>
<span data-ttu-id="0fa00-129">Use um tooquickly de modelo de início rápido do Azure implantar um cluster de HPC Pack em Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fa00-129">Use an Azure quickstart template tooquickly deploy an HPC Pack cluster in hello Azure portal.</span></span> <span data-ttu-id="0fa00-130">Quando você abre o modelo de saudação no portal de saudação, você obtém uma interface do usuário simple em que você insira configurações de saudação para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa00-130">When you open hello template in hello portal, you get a simple UI where you enter hello settings for your cluster.</span></span> <span data-ttu-id="0fa00-131">Aqui estão as etapas de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-131">Here are hello steps.</span></span> 

> [!TIP]
> <span data-ttu-id="0fa00-132">Se quiser, use um [modelo do Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) que cria um cluster semelhante, especificamente para cargas de trabalho do Excel.</span><span class="sxs-lookup"><span data-stu-id="0fa00-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="0fa00-133">Olá etapas um pouco diferentes do seguinte hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-133">hello steps differ slightly from hello following.</span></span>
> 
> 

1. <span data-ttu-id="0fa00-134">Visite Olá [página de modelo de criação de Cluster de HPC no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="0fa00-134">Visit hello [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="0fa00-135">Se você quiser, examine as informações sobre o modelo hello e código-fonte hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-135">If you want, review information about hello template and hello source code.</span></span>
2. <span data-ttu-id="0fa00-136">Clique em **implantar tooAzure** toostart uma implantação com modelo Olá Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fa00-136">Click **Deploy tooAzure** toostart a deployment with hello template in hello Azure portal.</span></span>
   
   ![Implantar o modelo tooAzure][github]
3. <span data-ttu-id="0fa00-138">No portal de hello, siga esses parâmetros de saudação tooenter etapas para o modelo de cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-138">In hello portal, follow these steps tooenter hello parameters for hello HPC cluster template.</span></span>
   
   <span data-ttu-id="0fa00-139">a.</span><span class="sxs-lookup"><span data-stu-id="0fa00-139">a.</span></span> <span data-ttu-id="0fa00-140">Em Olá **parâmetros** página, digite ou modifique os valores para parâmetros de modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-140">On hello **Parameters** page, enter or modify values for hello template parameters.</span></span> <span data-ttu-id="0fa00-141">(Clique Olá ícone próximo tooeach configuração para obter informações de Ajuda.) Valores de exemplo são mostrados no hello tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="0fa00-141">(Click hello icon next tooeach setting for help information.) Sample values are shown in hello following screen.</span></span> <span data-ttu-id="0fa00-142">Este exemplo cria um cluster denominado *hpc01* em Olá *hpc.local* domínio consiste em um nó de cabeçalho e de 2 nós de computação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-142">This example creates a cluster named *hpc01* in hello *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="0fa00-143">nós de computação Olá são criados de uma imagem de VM do HPC Pack que inclui o Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="0fa00-143">hello compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Inserir parâmetros][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="0fa00-145">nó de cabeçalho Olá VM é criada automaticamente da saudação [última imagem do Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) do HPC Pack 2012 R2 no Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="0fa00-145">hello head node VM is created automatically from hello [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="0fa00-146">Atualmente a imagem de saudação é baseada em HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="0fa00-146">Currently hello image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="0fa00-147">VMs do nó de computação são criadas de imagem mais recente de saudação da família de nó de computação de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="0fa00-147">Compute node VMs are created from hello latest image of hello selected compute node family.</span></span> <span data-ttu-id="0fa00-148">Selecione Olá **ComputeNodeWithExcel** opção hello mais recente HPC Pack computação nó imagem que inclui uma versão de avaliação do Microsoft Excel Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="0fa00-148">Select hello **ComputeNodeWithExcel** option for hello latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="0fa00-149">toodeploy um cluster para sessões SOA gerais ou para o descarregamento de UDF do Excel, escolha Olá **ComputeNode** opção (sem o Excel instalado).</span><span class="sxs-lookup"><span data-stu-id="0fa00-149">toodeploy a cluster for general SOA sessions or for Excel UDF offloading, choose hello **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="0fa00-150">b.</span><span class="sxs-lookup"><span data-stu-id="0fa00-150">b.</span></span> <span data-ttu-id="0fa00-151">Escolha a assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-151">Choose hello subscription.</span></span>
   
   <span data-ttu-id="0fa00-152">c.</span><span class="sxs-lookup"><span data-stu-id="0fa00-152">c.</span></span> <span data-ttu-id="0fa00-153">Criar um grupo de recursos de cluster hello, como *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="0fa00-153">Create a resource group for hello cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="0fa00-154">d.</span><span class="sxs-lookup"><span data-stu-id="0fa00-154">d.</span></span> <span data-ttu-id="0fa00-155">Escolha um local para o grupo de recursos hello, como centro dos EUA.</span><span class="sxs-lookup"><span data-stu-id="0fa00-155">Choose a location for hello resource group, such as Central US.</span></span>
   
   <span data-ttu-id="0fa00-156">e.</span><span class="sxs-lookup"><span data-stu-id="0fa00-156">e.</span></span> <span data-ttu-id="0fa00-157">Em Olá **termos legais** , examine os termos de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-157">On hello **Legal terms** page, review hello terms.</span></span> <span data-ttu-id="0fa00-158">Se concordar, clique em **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="0fa00-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="0fa00-159">Em seguida, quando você terminar de definir valores de saudação para o modelo de saudação, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="0fa00-159">Then, when you are finished setting hello values for hello template, click **Create**.</span></span>
4. <span data-ttu-id="0fa00-160">Ao concluir a implantação da saudação (normalmente demora cerca de 30 minutos), Exportar arquivo de certificado de cluster Olá Olá principal do nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa00-160">When hello deployment completes (it typically takes around 30 minutes), export hello cluster certificate file from hello cluster head node.</span></span> <span data-ttu-id="0fa00-161">Em uma etapa posterior, você importar o certificado público no hello tooprovide saudação do servidor autenticação do computador cliente para a associação de HTTP segura.</span><span class="sxs-lookup"><span data-stu-id="0fa00-161">In a later step, you import this public certificate on hello client computer tooprovide hello server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="0fa00-162">a.</span><span class="sxs-lookup"><span data-stu-id="0fa00-162">a.</span></span> <span data-ttu-id="0fa00-163">No portal do Azure de Olá, vá toohello painel, o nó principal do hello select e clique em **conectar** na parte superior de saudação do hello tooconnect de página usando a área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="0fa00-163">In hello Azure portal, go toohello dashboard, select hello head node, and click **Connect** at hello top of hello page tooconnect using Remote Desktop.</span></span>
   
    <!-- ![Connect toohello head node][connect] -->
   
   <span data-ttu-id="0fa00-164">b.</span><span class="sxs-lookup"><span data-stu-id="0fa00-164">b.</span></span> <span data-ttu-id="0fa00-165">Use procedimentos padrão no Gerenciador de certificados tooexport Olá nó principal certificado (localizado em Cert: \localmachine\my.) sem chave privada hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-165">Use standard procedures in Certificate Manager tooexport hello head node certificate (located under Cert:\LocalMachine\My) without hello private key.</span></span> <span data-ttu-id="0fa00-166">Neste exemplo, exporte *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="0fa00-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Exportar certificado Olá][cert]

### <a name="option-2-use-hello-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="0fa00-168">Opção 2.</span><span class="sxs-lookup"><span data-stu-id="0fa00-168">Option 2.</span></span> <span data-ttu-id="0fa00-169">Usar script de implantação de IaaS do HPC Pack Olá</span><span class="sxs-lookup"><span data-stu-id="0fa00-169">Use hello HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="0fa00-170">Olá script de implantação IaaS do HPC Pack fornece toodeploy de outra forma versátil um cluster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="0fa00-170">hello HPC Pack IaaS deployment script provides another versatile way toodeploy an HPC Pack cluster.</span></span> <span data-ttu-id="0fa00-171">Ele cria um cluster no modelo de implantação clássico Olá, enquanto o modelo de saudação usa o modelo de implantação do Azure Resource Manager hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-171">It creates a cluster in hello classic deployment model, whereas hello template uses hello Azure Resource Manager deployment model.</span></span> <span data-ttu-id="0fa00-172">Além disso, o script hello é compatível com uma assinatura no hello Global do Azure ou serviço do Azure na China.</span><span class="sxs-lookup"><span data-stu-id="0fa00-172">Also, hello script is compatible with a subscription in either hello Azure Global or Azure China service.</span></span>

<span data-ttu-id="0fa00-173">**Pré-requisitos adicionais**</span><span class="sxs-lookup"><span data-stu-id="0fa00-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="0fa00-174">**Azure PowerShell** - [Instale e configure o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="0fa00-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="0fa00-175">**Script de implantação IaaS do HPC Pack** - baixar e descompactar a versão mais recente de saudação do script Olá Olá [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="0fa00-175">**HPC Pack IaaS deployment script** - Download and unpack hello latest version of hello script from hello [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="0fa00-176">Verifique a versão de saudação do script hello executando `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="0fa00-176">Check hello version of hello script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="0fa00-177">Este artigo se baseia na versão 4.5.0 ou posterior do script hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-177">This article is based on version 4.5.0 or later of hello script.</span></span>

<span data-ttu-id="0fa00-178">**Criar arquivo de configuração de saudação**</span><span class="sxs-lookup"><span data-stu-id="0fa00-178">**Create hello configuration file**</span></span>

 <span data-ttu-id="0fa00-179">Olá script de implantação IaaS do HPC Pack usa um arquivo de configuração XML como entrada que descreve a infraestrutura de saudação do cluster HPC hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-179">hello HPC Pack IaaS deployment script uses an XML configuration file as input that describes hello infrastructure of hello HPC cluster.</span></span> <span data-ttu-id="0fa00-180">toodeploy criados a partir da imagem do nó de computação Olá que inclui o Microsoft Excel, de nós de computação de um cluster consiste em um nó principal e 18 substituir valores para o ambiente em Olá arquivo de configuração de exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="0fa00-180">toodeploy a cluster consisting of a head node and 18 compute nodes created from hello compute node image that includes Microsoft Excel, substitute values for your environment into hello following sample configuration file.</span></span> <span data-ttu-id="0fa00-181">Para obter mais informações sobre o arquivo de configuração hello, consulte o arquivo de Manual.rtf Olá na pasta de script hello e [criar um cluster HPC com hello script de implantação IaaS do HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0fa00-181">For more information about hello configuration file, see hello Manual.rtf file in hello script folder and [Create an HPC cluster with hello HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

```
<?xml version="1.0" encoding="utf-8"?>
<IaaSClusterConfig>
  <Subscription>
    <SubscriptionName>MySubscription</SubscriptionName>
    <StorageAccount>hpc01</StorageAccount>
  </Subscription>
  <Location>West US</Location>
  <VNet>
    <VNetName>hpc-vnet01</VNetName>
    <SubnetName>Subnet-1</SubnetName>
  </VNet>
  <Domain>
    <DCOption>NewDC</DCOption>
    <DomainFQDN>hpc.local</DomainFQDN>
    <DomainController>
      <VMName>HPCExcelDC01</VMName>
      <ServiceName>HPCExcelDC01</ServiceName>
      <VMSize>Medium</VMSize>
    </DomainController>
  </Domain>
   <Database>
    <DBOption>LocalDB</DBOption>
  </Database>
  <HeadNode>
    <VMName>HPCExcelHN01</VMName>
    <ServiceName>HPCExcelHN01</ServiceName>
    <VMSize>Large</VMSize>
    <EnableRESTAPI/>
    <EnableWebPortal/>
    <PostConfigScript>C:\tests\PostConfig.ps1</PostConfigScript>
  </HeadNode>
  <ComputeNodes>
    <VMNamePattern>HPCExcelCN%00%</VMNamePattern>
    <ServiceName>HPCExcelCN01</ServiceName>
    <VMSize>Medium</VMSize>
    <NodeCount>18</NodeCount>
    <ImageName>HPCPack2012R2_ComputeNodeWithExcel</ImageName>
  </ComputeNodes>
</IaaSClusterConfig>
```

<span data-ttu-id="0fa00-182">**Observações sobre o arquivo de configuração de saudação**</span><span class="sxs-lookup"><span data-stu-id="0fa00-182">**Notes about hello configuration file**</span></span>

* <span data-ttu-id="0fa00-183">Olá **VMName** do nó principal Olá **deve** Olá mesmo como Olá **ServiceName**, ou toorun realizá-SOA.</span><span class="sxs-lookup"><span data-stu-id="0fa00-183">hello **VMName** of hello head node **MUST** be hello same as hello **ServiceName**, or SOA jobs fail toorun.</span></span>
* <span data-ttu-id="0fa00-184">Verifique se você especificar **EnableWebPortal** para que hello certificado do nó principal é gerado e exportado.</span><span class="sxs-lookup"><span data-stu-id="0fa00-184">Make sure you specify **EnableWebPortal** so that hello head node certificate is generated and exported.</span></span>
* <span data-ttu-id="0fa00-185">arquivo de saudação especifica um script do PowerShell pós-configuração PostConfig.ps1 que é executado no nó principal hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-185">hello file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on hello head node.</span></span> <span data-ttu-id="0fa00-186">Olá script de exemplo a seguir define a cadeia de caracteres de conexão de armazenamento do Azure hello, remove a função de nó de computação de saudação do nó principal hello e coloca todos os nós online quando eles são implantados.</span><span class="sxs-lookup"><span data-stu-id="0fa00-186">hello following sample script configures hello Azure storage connection string, removes hello compute node role from hello head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add hello HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set hello Azure storage connection string for hello cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove hello compute node role for head node toomake sure hello Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in hello deployment including hello head node and compute nodes, which should match hello number specified in hello XML configuration file
        $TotalNumOfNodes = 19

        $ErrorActionPreference = 'SilentlyContinue'

    # bring nodes online when they are deployed until all nodes are online
        while ($true)
        {
          Get-HpcNode -State Offline | Set-HpcNodeState -State Online -Confirm:$false
          $OnlineNodes = @(Get-HpcNode -State Online)
          if ($OnlineNodes.Count -eq $TotalNumOfNodes)
          {
             break
          }
          sleep 60
        }
```

<span data-ttu-id="0fa00-187">**Execute o script hello**</span><span class="sxs-lookup"><span data-stu-id="0fa00-187">**Run hello script**</span></span>

1. <span data-ttu-id="0fa00-188">Abra o console do PowerShell de saudação no computador do cliente hello como um administrador.</span><span class="sxs-lookup"><span data-stu-id="0fa00-188">Open hello PowerShell console on hello client computer as an administrator.</span></span>
2. <span data-ttu-id="0fa00-189">Alterar pasta de scripts do diretório toohello (E:\IaaSClusterScript neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="0fa00-189">Change directory toohello script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="0fa00-190">cluster de HPC Pack em Olá toodeploy, execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="0fa00-190">toodeploy hello HPC Pack cluster, run hello following command.</span></span> <span data-ttu-id="0fa00-191">Este exemplo supõe que o arquivo de configuração hello está localizado em E:\HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="0fa00-191">This example assumes that hello configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="0fa00-192">Olá script de implantação do HPC Pack é executado por algum tempo.</span><span class="sxs-lookup"><span data-stu-id="0fa00-192">hello HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="0fa00-193">Um script de saudação coisa faz é tooexport e baixar o certificado de cluster hello e salvá-lo na pasta documentos saudação do usuário atual no computador do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-193">One thing hello script does is tooexport and download hello cluster certificate and save it in hello current user’s Documents folder on hello client computer.</span></span> <span data-ttu-id="0fa00-194">script Hello gera uma mensagem semelhante toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="0fa00-194">hello script generates a message similar toohello following.</span></span> <span data-ttu-id="0fa00-195">Em uma etapa seguinte, importe o certificado de saudação no repositório de certificado apropriado hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-195">In a following step, you import hello certificate in hello appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import hello following certificate in hello Trusted Root Certification Authorities certificate store on hello computer where you are submitting job or accessing hello HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="0fa00-196">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="0fa00-196">Step 2.</span></span> <span data-ttu-id="0fa00-197">Descarregaras pastas de trabalho do Excel e executar UDFs de um cliente local</span><span class="sxs-lookup"><span data-stu-id="0fa00-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="0fa00-198">Ativação do Excel</span><span class="sxs-lookup"><span data-stu-id="0fa00-198">Excel activation</span></span>
<span data-ttu-id="0fa00-199">Ao usar o hello imagem VM ComputeNodeWithExcel para cargas de trabalho de produção, você deve tooprovide uma válido Microsoft Office licença chave tooactivate Excel em nós de computação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-199">When using hello ComputeNodeWithExcel VM image for production workloads, you need tooprovide a valid Microsoft Office license key tooactivate Excel on hello compute nodes.</span></span> <span data-ttu-id="0fa00-200">Caso contrário, versão de avaliação de saudação do Excel expira após 30 dias, e que executa pastas de trabalho do Excel apresentará Olá COMException (0x800AC472).</span><span class="sxs-lookup"><span data-stu-id="0fa00-200">Otherwise, hello evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with hello COMException (0x800AC472).</span></span> 

<span data-ttu-id="0fa00-201">É possível rearmar Excel por mais 30 dias de tempo de avaliação: faça logon no nó principal toohello e clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` no Excel todos os nós por meio do Gerenciador de Cluster de HPC de computação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-201">You can rearm Excel for another 30 days of evaluation time: Log on toohello head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="0fa00-202">É possível rearmar, no máximo, duas vezes.</span><span class="sxs-lookup"><span data-stu-id="0fa00-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="0fa00-203">Depois disso, é necessário fornecer uma chave de licença válida do Office.</span><span class="sxs-lookup"><span data-stu-id="0fa00-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="0fa00-204">Olá Office Professional Plus 2013 instalado na imagem VM Olá é uma edição de volume com um genérico Volume licença GVLK (chave).</span><span class="sxs-lookup"><span data-stu-id="0fa00-204">hello Office Professional Plus 2013 installed on hello VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="0fa00-205">Você pode ativá-la por meio do KMS (Serviço de Gerenciamento de Chaves)/da AD-BA (Ativação Baseada no Active Directory) ou de uma MAK (Chave de Ativação Múltipla).</span><span class="sxs-lookup"><span data-stu-id="0fa00-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="0fa00-206">toouse AD/KMS-BA, usar um servidor KMS existente ou configure um novo usando Olá o pacote de licenças de Volume do Microsoft Office 2013.</span><span class="sxs-lookup"><span data-stu-id="0fa00-206">toouse KMS/AD-BA, use an existing KMS server or set up a new one by using hello Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="0fa00-207">(Se você quiser, configurar Olá servidor no nó de cabeçalho hello.) Em seguida, ative a chave do host KMS Olá via Olá da Internet ou por telefone.</span><span class="sxs-lookup"><span data-stu-id="0fa00-207">(If you want to, set up hello server on hello head node.) Then, activate hello KMS host key via hello Internet or telephone.</span></span> <span data-ttu-id="0fa00-208">Em seguida, clusrun `ospp.vbs` tooset Olá servidor KMS e a porta e ativar o Office em todos os nós de computação do Excel hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-208">Then clusrun `ospp.vbs` tooset hello KMS server and port and activate Office on all hello Excel compute nodes.</span></span> 

    * <span data-ttu-id="0fa00-209">toouse MAK, primeiro clusrun `ospp.vbs` tooinput Olá chave e, em seguida, ativar todos os nós de computação de Excel Olá via Olá da Internet ou por telefone.</span><span class="sxs-lookup"><span data-stu-id="0fa00-209">toouse MAK, first clusrun `ospp.vbs` tooinput hello key and then activate all hello Excel compute nodes via hello Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="0fa00-210">As chaves de produto de varejo do Office Professional Plus 2013 não podem ser usadas com essa imagem de VM.</span><span class="sxs-lookup"><span data-stu-id="0fa00-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="0fa00-211">Se você tiver chaves válidas e mídia de instalação para as edições do Office ou do Excel diferentes desta edição de volume do Office Professional Plus 2013, será possível usá-las em seu lugar.</span><span class="sxs-lookup"><span data-stu-id="0fa00-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="0fa00-212">Primeiro desinstale esta edição de volume e instalar a edição Olá que você possui.</span><span class="sxs-lookup"><span data-stu-id="0fa00-212">First uninstall this volume edition and install hello edition that you have.</span></span> <span data-ttu-id="0fa00-213">Olá reinstalado Excel do nó de computação pode ser capturado como uma toouse de imagem VM personalizada em uma implantação em escala.</span><span class="sxs-lookup"><span data-stu-id="0fa00-213">hello reinstalled Excel compute node can be captured as a customized VM image toouse in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="0fa00-214">Descarregar pastas de trabalho do Excel</span><span class="sxs-lookup"><span data-stu-id="0fa00-214">Offload Excel workbooks</span></span>
<span data-ttu-id="0fa00-215">Siga essas toooffload etapas uma pasta de trabalho do Excel para que ele seja executado no cluster de HPC Pack Olá no Azure.</span><span class="sxs-lookup"><span data-stu-id="0fa00-215">Follow these steps toooffload an Excel workbook so that it runs on hello HPC Pack cluster in Azure.</span></span> <span data-ttu-id="0fa00-216">toodo isso, você deve ter o Excel 2010 ou 2013 já instalado no computador do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-216">toodo this, you must have Excel 2010 or 2013 already installed on hello client computer.</span></span>

1. <span data-ttu-id="0fa00-217">Use uma das opções de saudação na etapa 1 toodeploy um cluster de HPC Pack com hello Excel imagem do nó de computação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-217">Use one of hello options in Step 1 toodeploy an HPC Pack cluster with hello Excel compute node image.</span></span> <span data-ttu-id="0fa00-218">Obter arquivo de certificado de cluster hello (. cer) e o nome de usuário de cluster e a senha.</span><span class="sxs-lookup"><span data-stu-id="0fa00-218">Obtain hello cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="0fa00-219">No computador do cliente hello, importe o certificado de cluster de saudação em Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="0fa00-219">On hello client computer, import hello cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="0fa00-220">Verifique se o Excel está instalado.</span><span class="sxs-lookup"><span data-stu-id="0fa00-220">Make sure Excel is installed.</span></span> <span data-ttu-id="0fa00-221">Criar um arquivo Excel.exe.config com hello seguindo o conteúdo no hello mesma pasta Excel.exe no computador do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-221">Create an Excel.exe.config file with hello following contents in hello same folder as Excel.exe on hello client computer.</span></span> <span data-ttu-id="0fa00-222">Essa etapa garante que Olá HPC Pack 2012 R2 Excel suplemento é carregado com êxito.</span><span class="sxs-lookup"><span data-stu-id="0fa00-222">This step ensures that hello HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="0fa00-223">Configure o cluster de HPC Pack Olá cliente toosubmit trabalhos toohello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-223">Set up hello client toosubmit jobs toohello HPC Pack cluster.</span></span> <span data-ttu-id="0fa00-224">Uma opção é completo de saudação toodownload [instalação HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49922) e instalar o cliente do HPC Pack hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-224">One option is toodownload hello full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install hello HPC Pack client.</span></span> <span data-ttu-id="0fa00-225">Como alternativa, baixe e instale Olá [utilitários de cliente do HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923) e Olá apropriado Visual C++ 2010 redistributable do computador ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="0fa00-225">Alternatively, download and install hello [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and hello appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="0fa00-226">Neste exemplo, usamos uma pasta de trabalho do Excel de exemplo chamada ConvertiblePricing_Complete.xlsb.</span><span class="sxs-lookup"><span data-stu-id="0fa00-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="0fa00-227">Você pode baixá-lo [aqui](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="0fa00-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="0fa00-228">Copie a pasta de trabalho de tooa Olá Excel pasta de trabalho como D:\Excel\Run.</span><span class="sxs-lookup"><span data-stu-id="0fa00-228">Copy hello Excel workbook tooa working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="0fa00-229">Abra a pasta de trabalho do Excel hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-229">Open hello Excel workbook.</span></span> <span data-ttu-id="0fa00-230">Em Olá **desenvolver** de faixa de opções, clique em **suplementos COM** e confirme que Olá HPC Pack Excel suplemento é carregado com êxito.</span><span class="sxs-lookup"><span data-stu-id="0fa00-230">On hello **Develop** ribbon, click **COM Add-Ins** and confirm that hello HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![Suplemento do Excel para o HPC Pack][addin]
8. <span data-ttu-id="0fa00-232">Editar saudação VBA macro HPCControlMacros no Excel alterando Olá comentários linhas conforme Olá script a seguir.</span><span class="sxs-lookup"><span data-stu-id="0fa00-232">Edit hello VBA macro HPCControlMacros in Excel by changing hello commented lines as shown in hello following script.</span></span> <span data-ttu-id="0fa00-233">Substitua os valores apropriados para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="0fa00-233">Substitute appropriate values for your environment.</span></span>
   
   ![Macro do Excel para o HPC Pack][macro]
   
   ```
   'Private Const HPC_ClusterScheduler = "HEADNODE_NAME"
   Private Const HPC_ClusterScheduler = "hpc01.eastus.cloudapp.azure.com"
   
   'Private Const HPC_NetworkShare = "\\PATH\TO\SHARE\DIRECTORY"
   Private Const HPC_DependFiles = "D:\Excel\Upload\ConvertiblePricing_Complete.xlsb=ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.Initialize ActiveWorkbook
   HPCExcelClient.Initialize ActiveWorkbook, HPC_DependFiles
   
   'HPCWorkbookPath = HPC_NetworkShare & Application.PathSeparator & ActiveWorkbook.name
   HPCWorkbookPath = "ConvertiblePricing_Complete.xlsb"
   
   'HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath
   HPCExcelClient.OpenSession headNode:=HPC_ClusterScheduler, remoteWorkbookPath:=HPCWorkbookPath, UserName:="hpc\azureuser", Password:="<YourPassword>"
   ```
9. <span data-ttu-id="0fa00-235">Copie o diretório de carregamento de tooan Olá Excel pasta de trabalho como D:\Excel\Upload.</span><span class="sxs-lookup"><span data-stu-id="0fa00-235">Copy hello Excel workbook tooan upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="0fa00-236">Esse diretório é especificado na constante de HPC_DependsFiles Olá em macro VBA hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-236">This directory is specified in hello HPC_DependsFiles constant in hello VBA macro.</span></span>
10. <span data-ttu-id="0fa00-237">pasta de trabalho do toorun Olá no cluster Olá no Azure, clique em Olá **Cluster** botão na planilha de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-237">toorun hello workbook on hello cluster in Azure, click hello **Cluster** button on hello worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="0fa00-238">Executar UDFs do Excel</span><span class="sxs-lookup"><span data-stu-id="0fa00-238">Run Excel UDFs</span></span>
<span data-ttu-id="0fa00-239">toorun UDFs do Excel, siga etapas anteriores de saudação tooset de 1 a 3 no computador do cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-239">toorun Excel UDFs, follow hello preceding steps 1 – 3 tooset up hello client computer.</span></span> <span data-ttu-id="0fa00-240">Para UDFs do Excel, você não precisa aplicativo do Excel Olá toohave instalado em nós de computação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-240">For Excel UDFs, you don't need toohave hello Excel application installed on compute nodes.</span></span> <span data-ttu-id="0fa00-241">Portanto, ao criar o cluster de nós de computação, você pode escolher a imagem de um nó de computação normal, em vez da saudação computação imagem do nó com o Excel.</span><span class="sxs-lookup"><span data-stu-id="0fa00-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of hello compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="0fa00-242">Há um limite de 34 caractere Olá Excel 2010 e 2013 caixa de diálogo de conector de cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa00-242">There is a 34 character limit in hello Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="0fa00-243">Você usar esse cluster de Olá de toospecify caixa de diálogo que executa Olá UDFs.</span><span class="sxs-lookup"><span data-stu-id="0fa00-243">You use this dialog box toospecify hello cluster that runs hello UDFs.</span></span> <span data-ttu-id="0fa00-244">Se o nome completo do cluster de saudação é maior (por exemplo, hpcexcelhn01.southeastasia.cloudapp.azure.com), ele não se ajustar na caixa de diálogo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0fa00-244">If hello full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in hello dialog box.</span></span> <span data-ttu-id="0fa00-245">Olá solução alternativa é tooset uma variável de máquina, como *CCP_IAASHN* com valor de saudação do nome de cluster longo hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-245">hello workaround is tooset a machine-wide variable such as *CCP_IAASHN* with hello value of hello long cluster name.</span></span> <span data-ttu-id="0fa00-246">Em seguida, insira *CCP_IAASHN %* na caixa de diálogo hello como o nome de nó principal do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-246">Then, enter *%CCP_IAASHN%* in hello dialog box as hello cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="0fa00-247">Depois que o cluster Olá é implantado com êxito, continue com Olá toorun as etapas a seguir internos exemplo UDF do Excel.</span><span class="sxs-lookup"><span data-stu-id="0fa00-247">After hello cluster is successfully deployed, continue with hello following steps toorun a sample built-in Excel UDF.</span></span> <span data-ttu-id="0fa00-248">Para UDFs personalizado do Excel, consulte estes [recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild Olá XLLs e implantá-los no cluster de IaaS hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) toobuild hello XLLs and deploy them on hello IaaS cluster.</span></span>

1. <span data-ttu-id="0fa00-249">Abra uma nova pasta de trabalho do Excel.</span><span class="sxs-lookup"><span data-stu-id="0fa00-249">Open a new Excel workbook.</span></span> <span data-ttu-id="0fa00-250">Em Olá **desenvolver** de faixa de opções, clique em **Add-Ins**. Em seguida, na caixa de diálogo hello, clique em **procurar**, navegar toohello %CCP_HOME%Bin\XLL32 pasta e selecione o exemplo hello ClusterUDF32.xll.</span><span class="sxs-lookup"><span data-stu-id="0fa00-250">On hello **Develop** ribbon, click **Add-Ins**. Then, in hello dialog box, click **Browse**, navigate toohello %CCP_HOME%Bin\XLL32 folder, and select hello sample ClusterUDF32.xll.</span></span> <span data-ttu-id="0fa00-251">Se hello ClusterUDF32 não existe na máquina do cliente hello, copie-o na pasta de %CCP_HOME%Bin\XLL32 Olá no nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-251">If hello ClusterUDF32 doesn't exist on hello client machine, copy it from hello %CCP_HOME%Bin\XLL32 folder on hello head node.</span></span>
   
   ![Selecione Olá UDF][udf]
2. <span data-ttu-id="0fa00-253">Clique em **Arquivo** > **Opções** > **Avançadas**.</span><span class="sxs-lookup"><span data-stu-id="0fa00-253">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="0fa00-254">Em **fórmulas**, verifique **permitir toorun de funções XLL definidas pelo usuário em um cluster de computação**.</span><span class="sxs-lookup"><span data-stu-id="0fa00-254">Under **Formulas**, check **Allow user-defined XLL functions toorun a compute cluster**.</span></span> <span data-ttu-id="0fa00-255">Em seguida, clique em **opções** e insira o nome completo do cluster de saudação em **nome de nó principal do Cluster**.</span><span class="sxs-lookup"><span data-stu-id="0fa00-255">Then click **Options** and enter hello full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="0fa00-256">(Conforme observado anteriormente essa caixa de entrada é limitado too34 caracteres, para que um nome de cluster longo não caber.</span><span class="sxs-lookup"><span data-stu-id="0fa00-256">(As noted previously this input box is limited too34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="0fa00-257">Você pode usar variáveis de todo o computador aqui para nomes de cluster longos.</span><span class="sxs-lookup"><span data-stu-id="0fa00-257">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Configurar Olá UDF][options]
3. <span data-ttu-id="0fa00-259">Olá toorun cálculo UDF no cluster hello, clique na célula de saudação com =XllGetComputerNameC() de valor e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="0fa00-259">toorun hello UDF calculation on hello cluster, click hello cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="0fa00-260">função Hello simplesmente recupera o nome de saudação do nó de computação Olá no qual Olá UDF for executada.</span><span class="sxs-lookup"><span data-stu-id="0fa00-260">hello function simply retrieves hello name of hello compute node on which hello UDF runs.</span></span> <span data-ttu-id="0fa00-261">Para Olá executado pela primeira vez, uma caixa de diálogo de credenciais solicita Olá username e password tooconnect toohello cluster IaaS.</span><span class="sxs-lookup"><span data-stu-id="0fa00-261">For hello first run, a credentials dialog box prompts for hello username and password tooconnect toohello IaaS cluster.</span></span>
   
   ![Executar UDF][run]
   
   <span data-ttu-id="0fa00-263">Quando há muitos toocalculate de células, pressione Ctrl-Shift-Alt + F9 cálculo de saudação de toorun em todas as células.</span><span class="sxs-lookup"><span data-stu-id="0fa00-263">When there are many cells toocalculate, press Alt-Shift-Ctrl + F9 toorun hello calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="0fa00-264">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="0fa00-264">Step 3.</span></span> <span data-ttu-id="0fa00-265">Executar uma carga de trabalho SOA a partir de um cliente local</span><span class="sxs-lookup"><span data-stu-id="0fa00-265">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="0fa00-266">aplicativos de SOA gerais toorun no cluster de HPC Pack IaaS Olá, primeiro use um dos métodos de Olá no cluster de saudação toodeploy etapa 1.</span><span class="sxs-lookup"><span data-stu-id="0fa00-266">toorun general SOA applications on hello HPC Pack IaaS cluster, first use one of hello methods in Step 1 toodeploy hello cluster.</span></span> <span data-ttu-id="0fa00-267">Especifique a imagem de um nó de computação genérico nesse caso, porque você não precisa do Excel em nós de computação hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-267">Specify a generic compute node image in this case, because you do not need Excel on hello compute nodes.</span></span> <span data-ttu-id="0fa00-268">Depois, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="0fa00-268">Then follow these steps.</span></span>

1. <span data-ttu-id="0fa00-269">Depois de recuperar o certificado de cluster hello, importá-lo no computador do cliente de saudação em Cert: \CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="0fa00-269">After retrieving hello cluster certificate, import it on hello client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="0fa00-270">Instalar Olá [SDK do HPC Pack 2012 R2 Update 3](http://www.microsoft.com/download/details.aspx?id=49921) e [utilitários de cliente do HPC Pack 2012 R2 Update 3](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="0fa00-270">Install hello [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="0fa00-271">Essas ferramentas permitem que você toodevelop e executam aplicativos de cliente SOA.</span><span class="sxs-lookup"><span data-stu-id="0fa00-271">These tools enable you toodevelop and run SOA client applications.</span></span>
3. <span data-ttu-id="0fa00-272">Baixar Olá HelloWorldR2 [código de exemplo](https://www.microsoft.com/download/details.aspx?id=41633).</span><span class="sxs-lookup"><span data-stu-id="0fa00-272">Download hello HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="0fa00-273">Abra Olá HelloWorldR2.sln no Visual Studio 2010 ou 2012.</span><span class="sxs-lookup"><span data-stu-id="0fa00-273">Open hello HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="0fa00-274">(Atualmente, este exemplo não é compatível com versões mais recentes do Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="0fa00-274">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="0fa00-275">Compilação do projeto EchoService Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="0fa00-275">Build hello EchoService project first.</span></span> <span data-ttu-id="0fa00-276">Em seguida, implante o cluster de IaaS Olá serviço toohello em Olá mesma maneira como você implanta tooan local cluster.</span><span class="sxs-lookup"><span data-stu-id="0fa00-276">Then, deploy hello service toohello IaaS cluster in hello same way you deploy tooan on-premises cluster.</span></span> <span data-ttu-id="0fa00-277">Para obter etapas detalhadas, consulte Olá Leiame no HelloWordR2.</span><span class="sxs-lookup"><span data-stu-id="0fa00-277">For detailed steps, see hello Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="0fa00-278">Modificar e criar hello HellWorldR2 e outros projetos, conforme descrito em Olá seguinte seção toogenerate saudação SOA aplicativos cliente que são executados em um cluster de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="0fa00-278">Modify and build hello HellWorldR2 and other projects as described in hello following section toogenerate hello SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="0fa00-279">Usar associação Http com fila de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="0fa00-279">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="0fa00-280">associação de Http toouse com uma fila de armazenamento do Azure, fazer algumas alterações de código de exemplo toohello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-280">toouse Http binding with an Azure storage queue, make a few changes toohello sample code.</span></span>

* <span data-ttu-id="0fa00-281">Atualize o nome do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0fa00-281">Update hello cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="0fa00-282">Opcionalmente, use o padrão de saudação TransportScheme em SessionStartInfo ou definir explicitamente tooHttp.</span><span class="sxs-lookup"><span data-stu-id="0fa00-282">Optionally, use hello default TransportScheme in SessionStartInfo or explicitly set it tooHttp.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="0fa00-283">Use a associação padrão para Olá BrokerClient.</span><span class="sxs-lookup"><span data-stu-id="0fa00-283">Use default binding for hello BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="0fa00-284">Ou defina explicitamente usando Olá basicHttpBinding.</span><span class="sxs-lookup"><span data-stu-id="0fa00-284">Or set explicitly using hello basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="0fa00-285">Opcionalmente, defina Olá UseAzureQueue sinalizador tootrue em SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="0fa00-285">Optionally, set hello UseAzureQueue flag tootrue in SessionStartInfo.</span></span> <span data-ttu-id="0fa00-286">Se não for definido, será definido tootrue por padrão quando o nome de cluster Olá tem sufixos de domínio do Azure e Olá TransportScheme é Http.</span><span class="sxs-lookup"><span data-stu-id="0fa00-286">If not set, it will be set tootrue by default when hello cluster name has Azure domain suffixes and hello TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="0fa00-287">Usar associação Http sem fila de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="0fa00-287">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="0fa00-288">associação de Http toouse sem uma fila de armazenamento do Azure, explicitamente conjunto Olá UseAzureQueue sinalizador toofalse no hello SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="0fa00-288">toouse Http binding without an Azure storage queue, explicitly set hello UseAzureQueue flag toofalse in hello SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="0fa00-289">Usar associação NetTcp</span><span class="sxs-lookup"><span data-stu-id="0fa00-289">Use NetTcp binding</span></span>
<span data-ttu-id="0fa00-290">toouse NetTcp associação, configuração de saudação é semelhante cluster do tooconnecting tooan local.</span><span class="sxs-lookup"><span data-stu-id="0fa00-290">toouse NetTcp binding, hello configuration is similar tooconnecting tooan on-premises cluster.</span></span> <span data-ttu-id="0fa00-291">Você precisa de alguns pontos de extremidade na VM do nó principal Olá tooopen.</span><span class="sxs-lookup"><span data-stu-id="0fa00-291">You need tooopen a few endpoints on hello head node VM.</span></span> <span data-ttu-id="0fa00-292">Se você usou o cluster de Olá Olá HPC Pack IaaS implantação script toocreate, por exemplo, definir pontos de extremidade de saudação em Olá portal do Azure da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="0fa00-292">If you used hello HPC Pack IaaS deployment script toocreate hello cluster, for example, set hello endpoints in hello Azure portal as follows.</span></span>

1. <span data-ttu-id="0fa00-293">Pare Olá VM.</span><span class="sxs-lookup"><span data-stu-id="0fa00-293">Stop hello VM.</span></span>
2. <span data-ttu-id="0fa00-294">Adicionar as portas TCP Olá 9090, 9087, 9091, 9094 de sessão, de saudação do agente, agente de trabalho e serviços de dados, respectivamente</span><span class="sxs-lookup"><span data-stu-id="0fa00-294">Add hello TCP ports 9090, 9087, 9091, 9094 for hello Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Configurar pontos de extremidade][endpoint-new-portal]
3. <span data-ttu-id="0fa00-296">Inicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="0fa00-296">Start hello VM.</span></span>

<span data-ttu-id="0fa00-297">Olá aplicativo de cliente SOA não requer alterações exceto alterando o nome completo do cluster de IaaS de toohello do hello nome principal.</span><span class="sxs-lookup"><span data-stu-id="0fa00-297">hello SOA client application requires no changes except altering hello head name toohello IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0fa00-298">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0fa00-298">Next steps</span></span>
* <span data-ttu-id="0fa00-299">Consulte [estes recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) para saber mais sobre como executar cargas de trabalho do Excel com o HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="0fa00-299">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="0fa00-300">Consulte [Gerenciamento de serviços SOA no Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) para saber mais sobre como implantar e gerenciar serviços SOA com HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="0fa00-300">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

<!--Image references-->
[scenario]: ./media/excel-cluster-hpcpack/scenario.png
[github]: ./media/excel-cluster-hpcpack/github.png
[template]: ./media/excel-cluster-hpcpack/template.png
[parameters]: ./media/excel-cluster-hpcpack/parameters.png
[parameters-new-portal]: ./media/excel-cluster-hpcpack/parameters-new-portal.png
[create]: ./media/excel-cluster-hpcpack/create.png
[connect]: ./media/excel-cluster-hpcpack/connect.png
[cert]: ./media/excel-cluster-hpcpack/cert.png
[addin]: ./media/excel-cluster-hpcpack/addin.png
[macro]: ./media/excel-cluster-hpcpack/macro.png
[options]: ./media/excel-cluster-hpcpack/options.png
[run]: ./media/excel-cluster-hpcpack/run.png
[endpoint]: ./media/excel-cluster-hpcpack/endpoint.png
[endpoint-new-portal]: ./media/excel-cluster-hpcpack/endpoint-new-portal.png
[udf]: ./media/excel-cluster-hpcpack/udf.png
