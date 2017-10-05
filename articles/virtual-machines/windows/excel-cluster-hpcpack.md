---
title: Cluster HPC Pack para Excel e SOA | Microsoft Docs
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
ms.openlocfilehash: 63babd94fdab15217cfb0757e4cd6efe458a628d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-running-excel-and-soa-workloads-on-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="18eca-103">Introdução à execução de cargas de trabalho do Excel e SOA em um cluster HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="18eca-103">Get started running Excel and SOA workloads on an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="18eca-104">Este artigo mostra como implantar um cluster do Microsoft HPC Pack 2012 R2 em máquinas virtuais do Azure usando um modelo de início rápido do Azure ou, opcionalmente, um script de implantação do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="18eca-104">This article shows you how to deploy a Microsoft HPC Pack 2012 R2 cluster on Azure virtual machines by using an Azure quickstart template, or optionally an Azure PowerShell deployment script.</span></span> <span data-ttu-id="18eca-105">O cluster usa as imagens de VM do Azure Marketplace projetadas para executar cargas de trabalho da arquitetura SOA ou do Microsoft Excel com o HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="18eca-105">The cluster uses Azure Marketplace VM images designed to run Microsoft Excel or service-oriented architecture (SOA) workloads with HPC Pack.</span></span> <span data-ttu-id="18eca-106">Você pode usar o cluster para executar serviços de SOA e HPC do Excel de um computador cliente local.</span><span class="sxs-lookup"><span data-stu-id="18eca-106">You can use the cluster to run Excel HPC and SOA services from an on-premises client computer.</span></span> <span data-ttu-id="18eca-107">Os serviços do Excel HPC incluem descarregamento de pasta de trabalho do Excel e funções definidas pelo usuário do Excel ou UDFs.</span><span class="sxs-lookup"><span data-stu-id="18eca-107">The Excel HPC services include Excel workbook offloading and Excel user-defined functions, or UDFs.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="18eca-108">Este artigo se baseia em recursos, modelos e scripts do HPC Pack 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="18eca-108">This article is based on features, templates, and scripts for HPC Pack 2012 R2.</span></span> <span data-ttu-id="18eca-109">Atualmente, este cenário não tem suporte no HPC Pack 2016.</span><span class="sxs-lookup"><span data-stu-id="18eca-109">This scenario is not currently supported in HPC Pack 2016.</span></span>
>

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="18eca-110">Em um alto nível, o diagrama a seguir mostra o cluster HPC Pack criado.</span><span class="sxs-lookup"><span data-stu-id="18eca-110">At a high level, the following diagram shows the HPC Pack cluster you create.</span></span>

![Cluster HPC com nós que executam cargas de trabalho do Excel][scenario]

## <a name="prerequisites"></a><span data-ttu-id="18eca-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="18eca-112">Prerequisites</span></span>
* <span data-ttu-id="18eca-113">**Computador cliente** – você precisa de um computador cliente baseado no Windows para enviar trabalhos de exemplo do Excel e SOA ao cluster.</span><span class="sxs-lookup"><span data-stu-id="18eca-113">**Client computer** - You need a Windows-based client computer to submit sample Excel and SOA jobs to the cluster.</span></span> <span data-ttu-id="18eca-114">Você também precisa de um computador Windows para executar o script de implantação de cluster do Azure PowerShell (caso escolha esse método de implantação).</span><span class="sxs-lookup"><span data-stu-id="18eca-114">You also need a Windows computer to run the Azure PowerShell cluster deployment script (if you choose that deployment method).</span></span>
* <span data-ttu-id="18eca-115">**Assinatura do Azure** – Se não tiver uma, você poderá criar uma [conta gratuita](https://azure.microsoft.com/pricing/free-trial/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="18eca-115">**Azure subscription** - If you don't have an Azure subscription, you can create a [free account](https://azure.microsoft.com/pricing/free-trial/) in just a couple of minutes.</span></span>
* <span data-ttu-id="18eca-116">**Cota para núcleos** : talvez seja necessário aumentar a cota de núcleos, especialmente se você implantar vários nós de cluster com tamanhos de VM de vários núcleos.</span><span class="sxs-lookup"><span data-stu-id="18eca-116">**Cores quota** - You might need to increase the quota of cores, especially if you deploy several cluster nodes with multicore VM sizes.</span></span> <span data-ttu-id="18eca-117">Se você estiver usando um modelo de início rápido do Azure, a cota de núcleos no Resource Manager será calculada por região do Azure.</span><span class="sxs-lookup"><span data-stu-id="18eca-117">If you are using an Azure quickstart template, the cores quota in Resource Manager is per Azure region.</span></span> <span data-ttu-id="18eca-118">Nesse caso, talvez você precise aumentar a cota em uma região específica.</span><span class="sxs-lookup"><span data-stu-id="18eca-118">In that case, you might need to increase the quota in a specific region.</span></span> <span data-ttu-id="18eca-119">Consulte [Assinatura do Azure e limite de serviços, cotas e restrições](../../azure-subscription-service-limits.md).</span><span class="sxs-lookup"><span data-stu-id="18eca-119">See [Azure subscription limits, quotas, and constraints](../../azure-subscription-service-limits.md).</span></span> <span data-ttu-id="18eca-120">Para aumentar a cota, [abra uma solicitação de atendimento ao cliente online](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) gratuitamente.</span><span class="sxs-lookup"><span data-stu-id="18eca-120">To increase a quota, [open an online customer support request](https://azure.microsoft.com/blog/2014/06/04/azure-limits-quotas-increase-requests/) at no charge.</span></span>
* <span data-ttu-id="18eca-121">**Licença do Microsoft Office** – se você implantar nós de computação usando uma imagem de VM do Marketplace HPC Pack 2012 R2 com Microsoft Excel, uma versão de avaliação de 30 dias do Microsoft Excel Professional Plus 2013 será instalada.</span><span class="sxs-lookup"><span data-stu-id="18eca-121">**Microsoft Office license** - If you deploy compute nodes using a Marketplace HPC Pack 2012 R2 VM image with Microsoft Excel, a 30-day evaluation version of Microsoft Excel Professional Plus 2013 is installed.</span></span> <span data-ttu-id="18eca-122">Após o período de avaliação, você precisa fornecer uma licença válida do Microsoft Office para ativar o Excel e continuar executando cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="18eca-122">After the evaluation period, you need to provide a valid Microsoft Office license to activate Excel to continue to run workloads.</span></span> <span data-ttu-id="18eca-123">Confira [Ativação do Excel](#excel-activation) mais adiante neste artigo.</span><span class="sxs-lookup"><span data-stu-id="18eca-123">See [Excel activation](#excel-activation) later in this article.</span></span> 

## <a name="step-1-set-up-an-hpc-pack-cluster-in-azure"></a><span data-ttu-id="18eca-124">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="18eca-124">Step 1.</span></span> <span data-ttu-id="18eca-125">Configurar um cluster de HPC Pack no Azure</span><span class="sxs-lookup"><span data-stu-id="18eca-125">Set up an HPC Pack cluster in Azure</span></span>
<span data-ttu-id="18eca-126">Mostramos duas opções para configurar o cluster do HPC Pack 2012 R2: primeiro, usando um modelo de início rápido do Azure e o portal do Azure; e segundo, usando um script de implantação do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="18eca-126">We show two options to set up the HPC Pack 2012 R2 cluster: first, using an Azure quickstart template and the Azure portal; and second, using an Azure PowerShell deployment script.</span></span>

### <a name="option-1-use-a-quickstart-template"></a><span data-ttu-id="18eca-127">Opção 1.</span><span class="sxs-lookup"><span data-stu-id="18eca-127">Option 1.</span></span> <span data-ttu-id="18eca-128">Usar um modelo de início rápido</span><span class="sxs-lookup"><span data-stu-id="18eca-128">Use a quickstart template</span></span>
<span data-ttu-id="18eca-129">Use um modelo de início rápido do Azure para implantar de maneira rápida um cluster do HPC Pack no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="18eca-129">Use an Azure quickstart template to quickly deploy an HPC Pack cluster in the Azure portal.</span></span> <span data-ttu-id="18eca-130">Ao abrir o modelo no portal, você obtém uma interface do usuário simples onde inserir as configurações para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="18eca-130">When you open the template in the portal, you get a simple UI where you enter the settings for your cluster.</span></span> <span data-ttu-id="18eca-131">Siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="18eca-131">Here are the steps.</span></span> 

> [!TIP]
> <span data-ttu-id="18eca-132">Se quiser, use um [modelo do Azure Marketplace](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) que cria um cluster semelhante, especificamente para cargas de trabalho do Excel.</span><span class="sxs-lookup"><span data-stu-id="18eca-132">If you want, use an [Azure Marketplace template](https://portal.azure.com/?feature.relex=*%2CHubsExtension#create/microsofthpc.newclusterexcelcn) that creates a similar cluster specifically for Excel workloads.</span></span> <span data-ttu-id="18eca-133">As etapas diferem ligeiramente das que se seguem.</span><span class="sxs-lookup"><span data-stu-id="18eca-133">The steps differ slightly from the following.</span></span>
> 
> 

1. <span data-ttu-id="18eca-134">Visite a [página Criar modelo de Cluster de HPC no GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span><span class="sxs-lookup"><span data-stu-id="18eca-134">Visit the [Create HPC Cluster template page on GitHub](https://github.com/Azure/azure-quickstart-templates/tree/master/create-hpc-cluster).</span></span> <span data-ttu-id="18eca-135">Se quiser, reveja as informações sobre o modelo e o código-fonte.</span><span class="sxs-lookup"><span data-stu-id="18eca-135">If you want, review information about the template and the source code.</span></span>
2. <span data-ttu-id="18eca-136">Clique em **Implantar no Azure** para iniciar uma implantação com o modelo no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="18eca-136">Click **Deploy to Azure** to start a deployment with the template in the Azure portal.</span></span>
   
   ![Implantar o modelo no Azure][github]
3. <span data-ttu-id="18eca-138">No portal, siga estas etapas para especificar os parâmetros para o modelo de cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="18eca-138">In the portal, follow these steps to enter the parameters for the HPC cluster template.</span></span>
   
   <span data-ttu-id="18eca-139">a.</span><span class="sxs-lookup"><span data-stu-id="18eca-139">a.</span></span> <span data-ttu-id="18eca-140">Na página **Parâmetros** , insira ou modifique os valores para os parâmetros de modelo.</span><span class="sxs-lookup"><span data-stu-id="18eca-140">On the **Parameters** page, enter or modify values for the template parameters.</span></span> <span data-ttu-id="18eca-141">Clique no ícone ao lado de cada configuração para obter informações de Ajuda. Os valores de exemplo são mostrados na tela a seguir.</span><span class="sxs-lookup"><span data-stu-id="18eca-141">(Click the icon next to each setting for help information.) Sample values are shown in the following screen.</span></span> <span data-ttu-id="18eca-142">Este exemplo cria um cluster denominado *hpc01* no domínio *hpc.local*, que consiste em um nó do cabeçalho e dois nós de computação.</span><span class="sxs-lookup"><span data-stu-id="18eca-142">This example creates a cluster named *hpc01* in the *hpc.local* domain consisting of a head node and 2 compute nodes.</span></span> <span data-ttu-id="18eca-143">Os nós de computação são criados com base em uma imagem de VM do HPC Pack que inclui o Microsoft Excel.</span><span class="sxs-lookup"><span data-stu-id="18eca-143">The compute nodes are created from an HPC Pack VM image that includes Microsoft Excel.</span></span>
   
   ![Inserir parâmetros][parameters-new-portal]
   
   > [!NOTE]
   > <span data-ttu-id="18eca-145">A VM do nó de cabeçalho é criada automaticamente com base na [imagem mais recente do Marketplace](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) do HPC Pack 2012 R2 no Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="18eca-145">The head node VM is created automatically from the [latest Marketplace image](https://azure.microsoft.com/marketplace/partners/microsoft/hpcpack2012r2onwindowsserver2012r2/) of HPC Pack 2012 R2 on Windows Server 2012 R2.</span></span> <span data-ttu-id="18eca-146">Atualmente, a imagem se baseia no HPC Pack 2012 R2 Update 3.</span><span class="sxs-lookup"><span data-stu-id="18eca-146">Currently the image is based on HPC Pack 2012 R2 Update 3.</span></span>
   > 
   > <span data-ttu-id="18eca-147">As VMs do nó de computação são criadas com base na imagem mais recente da família do nó de computação selecionada.</span><span class="sxs-lookup"><span data-stu-id="18eca-147">Compute node VMs are created from the latest image of the selected compute node family.</span></span> <span data-ttu-id="18eca-148">Selecione a opção **ComputeNodeWithExcel** para a imagem do nó de computação HPC Pack mais recente que inclui uma versão de avaliação do Microsoft Excel Professional Plus 2013.</span><span class="sxs-lookup"><span data-stu-id="18eca-148">Select the **ComputeNodeWithExcel** option for the latest HPC Pack compute node image that includes an evaluation version of Microsoft Excel Professional Plus 2013.</span></span> <span data-ttu-id="18eca-149">Para implantar um cluster para sessões gerais de SOA ou para o descarregamento de UDF do Excel, escolha a opção **ComputeNode** (sem o Excel instalado).</span><span class="sxs-lookup"><span data-stu-id="18eca-149">To deploy a cluster for general SOA sessions or for Excel UDF offloading, choose the **ComputeNode** option (without Excel installed).</span></span>
   > 
   > 
   
   <span data-ttu-id="18eca-150">b.</span><span class="sxs-lookup"><span data-stu-id="18eca-150">b.</span></span> <span data-ttu-id="18eca-151">Selecione a assinatura.</span><span class="sxs-lookup"><span data-stu-id="18eca-151">Choose the subscription.</span></span>
   
   <span data-ttu-id="18eca-152">c.</span><span class="sxs-lookup"><span data-stu-id="18eca-152">c.</span></span> <span data-ttu-id="18eca-153">Crie um novo grupo de recursos para o cluster, como *hpc01RG*.</span><span class="sxs-lookup"><span data-stu-id="18eca-153">Create a resource group for the cluster, such as *hpc01RG*.</span></span>
   
   <span data-ttu-id="18eca-154">d.</span><span class="sxs-lookup"><span data-stu-id="18eca-154">d.</span></span> <span data-ttu-id="18eca-155">Escolha um local para o grupo de recursos, como EUA Central.</span><span class="sxs-lookup"><span data-stu-id="18eca-155">Choose a location for the resource group, such as Central US.</span></span>
   
   <span data-ttu-id="18eca-156">e.</span><span class="sxs-lookup"><span data-stu-id="18eca-156">e.</span></span> <span data-ttu-id="18eca-157">Na página **Termos legais** , analise os termos.</span><span class="sxs-lookup"><span data-stu-id="18eca-157">On the **Legal terms** page, review the terms.</span></span> <span data-ttu-id="18eca-158">Se concordar, clique em **Comprar**.</span><span class="sxs-lookup"><span data-stu-id="18eca-158">If you agree, click **Purchase**.</span></span> <span data-ttu-id="18eca-159">Quando tiver terminado de definir os valores para o modelo, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="18eca-159">Then, when you are finished setting the values for the template, click **Create**.</span></span>
4. <span data-ttu-id="18eca-160">Quando a implantação for concluída (normalmente leva cerca de 30 minutos), exporte o arquivo de certificado de cluster do nó principal do cluster.</span><span class="sxs-lookup"><span data-stu-id="18eca-160">When the deployment completes (it typically takes around 30 minutes), export the cluster certificate file from the cluster head node.</span></span> <span data-ttu-id="18eca-161">Em uma etapa posterior, este certificado público será importado no computador cliente para fornecer a autenticação no servidor para a associação segura de HTTP.</span><span class="sxs-lookup"><span data-stu-id="18eca-161">In a later step, you import this public certificate on the client computer to provide the server-side authentication for secure HTTP binding.</span></span>
   
   <span data-ttu-id="18eca-162">a.</span><span class="sxs-lookup"><span data-stu-id="18eca-162">a.</span></span> <span data-ttu-id="18eca-163">No portal do Azure, vá para o painel, selecione o nó principal e, em seguida, clique em **Conectar** na parte superior da página para se conectar usando a Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="18eca-163">In the Azure portal, go to the dashboard, select the head node, and click **Connect** at the top of the page to connect using Remote Desktop.</span></span>
   
    <!-- ![Connect to the head node][connect] -->
   
   <span data-ttu-id="18eca-164">b.</span><span class="sxs-lookup"><span data-stu-id="18eca-164">b.</span></span> <span data-ttu-id="18eca-165">Use os procedimentos padrão no Gerenciador de Certificados para exportar o certificado de nó principal (localizado em Cert:\LocalMachine\My) sem a chave privada.</span><span class="sxs-lookup"><span data-stu-id="18eca-165">Use standard procedures in Certificate Manager to export the head node certificate (located under Cert:\LocalMachine\My) without the private key.</span></span> <span data-ttu-id="18eca-166">Neste exemplo, exporte *CN = hpc01.eastus.cloudapp.azure.com*.</span><span class="sxs-lookup"><span data-stu-id="18eca-166">In this example, export *CN = hpc01.eastus.cloudapp.azure.com*.</span></span>
   
   ![Exportar o certificado][cert]

### <a name="option-2-use-the-hpc-pack-iaas-deployment-script"></a><span data-ttu-id="18eca-168">Opção 2.</span><span class="sxs-lookup"><span data-stu-id="18eca-168">Option 2.</span></span> <span data-ttu-id="18eca-169">Use o script de implantação do HPC Pack IaaS</span><span class="sxs-lookup"><span data-stu-id="18eca-169">Use the HPC Pack IaaS Deployment script</span></span>
<span data-ttu-id="18eca-170">O script de implantação do HPC Pack IaaS é outra forma versátil para implantar um cluster de HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="18eca-170">The HPC Pack IaaS deployment script provides another versatile way to deploy an HPC Pack cluster.</span></span> <span data-ttu-id="18eca-171">Ele cria um cluster no modelo de implantação clássica, enquanto o modelo usa o modelo de implantação do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="18eca-171">It creates a cluster in the classic deployment model, whereas the template uses the Azure Resource Manager deployment model.</span></span> <span data-ttu-id="18eca-172">Além disso, o script é compatível com uma assinatura no serviço Azure Global ou Azure China.</span><span class="sxs-lookup"><span data-stu-id="18eca-172">Also, the script is compatible with a subscription in either the Azure Global or Azure China service.</span></span>

<span data-ttu-id="18eca-173">**Pré-requisitos adicionais**</span><span class="sxs-lookup"><span data-stu-id="18eca-173">**Additional prerequisites**</span></span>

* <span data-ttu-id="18eca-174">**Azure PowerShell** - [Instale e configure o Azure PowerShell](/powershell/azure/overview) (versão 0.8.10 ou posterior) no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="18eca-174">**Azure PowerShell** - [Install and configure Azure PowerShell](/powershell/azure/overview) (version 0.8.10 or later) on your client computer.</span></span>
* <span data-ttu-id="18eca-175">**Script de implantação do Pacote HPC IaaS** : baixe e descompacte a versão mais recente do script no [Centro de Download da Microsoft](https://www.microsoft.com/download/details.aspx?id=44949).</span><span class="sxs-lookup"><span data-stu-id="18eca-175">**HPC Pack IaaS deployment script** - Download and unpack the latest version of the script from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=44949).</span></span> <span data-ttu-id="18eca-176">Verifique a versão do script executando `New-HPCIaaSCluster.ps1 –Version`.</span><span class="sxs-lookup"><span data-stu-id="18eca-176">Check the version of the script by running `New-HPCIaaSCluster.ps1 –Version`.</span></span> <span data-ttu-id="18eca-177">Este artigo se baseia na versão 4.5.0 ou posterior do script.</span><span class="sxs-lookup"><span data-stu-id="18eca-177">This article is based on version 4.5.0 or later of the script.</span></span>

<span data-ttu-id="18eca-178">**Criar o arquivo de configuração**</span><span class="sxs-lookup"><span data-stu-id="18eca-178">**Create the configuration file**</span></span>

 <span data-ttu-id="18eca-179">O script de implantação do HPC Pack de IaaS usa um arquivo de configuração XML como entrada que descreve a infraestrutura do cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="18eca-179">The HPC Pack IaaS deployment script uses an XML configuration file as input that describes the infrastructure of the HPC cluster.</span></span> <span data-ttu-id="18eca-180">Para implantar um cluster que consiste em um nó principal e 18 nós de computação criados a partir da imagem do nó de computação que inclui o Microsoft Excel, substitua os valores para o seu ambiente no seguinte arquivo de configuração de exemplo.</span><span class="sxs-lookup"><span data-stu-id="18eca-180">To deploy a cluster consisting of a head node and 18 compute nodes created from the compute node image that includes Microsoft Excel, substitute values for your environment into the following sample configuration file.</span></span> <span data-ttu-id="18eca-181">Para obter mais informações sobre o arquivo de configuração, consulte o arquivo Manual.rtf na pasta de script e [Criar um cluster HPC com o script de implantação de IaaS do HPC Pack](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="18eca-181">For more information about the configuration file, see the Manual.rtf file in the script folder and [Create an HPC cluster with the HPC Pack IaaS deployment script](classic/hpcpack-cluster-powershell-script.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

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

<span data-ttu-id="18eca-182">**Notas sobre o arquivo de configuração**</span><span class="sxs-lookup"><span data-stu-id="18eca-182">**Notes about the configuration file**</span></span>

* <span data-ttu-id="18eca-183">O **VMName** do nó do cabeçalho **DEVE** ser igual ao **ServiceName** ou os trabalhos SOA não funcionarão.</span><span class="sxs-lookup"><span data-stu-id="18eca-183">The **VMName** of the head node **MUST** be the same as the **ServiceName**, or SOA jobs fail to run.</span></span>
* <span data-ttu-id="18eca-184">Verifique se você especificou **EnableWebPortal** para que o certificado de nó principal seja gerado e exportado.</span><span class="sxs-lookup"><span data-stu-id="18eca-184">Make sure you specify **EnableWebPortal** so that the head node certificate is generated and exported.</span></span>
* <span data-ttu-id="18eca-185">O arquivo especifica um script do PowerShell pós-configuração PostConfig.ps1 que é executado no nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="18eca-185">The file specifies a post-configuration PowerShell script PostConfig.ps1 that runs on the head node.</span></span> <span data-ttu-id="18eca-186">O script de exemplo a seguir configura a cadeia de conexão do armazenamento do Azure, remove a função do nó de computação do nó de cabeçalho e coloca todos os nós online quando são implantados.</span><span class="sxs-lookup"><span data-stu-id="18eca-186">THe following sample script configures the Azure storage connection string, removes the compute node role from the head node, and brings all nodes online when they are deployed.</span></span> 

```
    # add the HPC Pack powershell cmdlets
        Add-PSSnapin Microsoft.HPC

    # set the Azure storage connection string for the cluster
        Set-HpcClusterProperty -AzureStorageConnectionString 'DefaultEndpointsProtocol=https;AccountName=<yourstorageaccountname>;AccountKey=<yourstorageaccountkey>'

    # remove the compute node role for head node to make sure the Excel workbook won’t run on head node
        Get-HpcNode -GroupName HeadNodes | Set-HpcNodeState -State offline | Set-HpcNode -Role BrokerNode

    # total number of nodes in the deployment including the head node and compute nodes, which should match the number specified in the XML configuration file
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

<span data-ttu-id="18eca-187">**Execute o script**</span><span class="sxs-lookup"><span data-stu-id="18eca-187">**Run the script**</span></span>

1. <span data-ttu-id="18eca-188">Abra o console do PowerShell no computador cliente como administrador.</span><span class="sxs-lookup"><span data-stu-id="18eca-188">Open the PowerShell console on the client computer as an administrator.</span></span>
2. <span data-ttu-id="18eca-189">Altere o diretório para a pasta de scripts (E:\IaaSClusterScript neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="18eca-189">Change directory to the script folder (E:\IaaSClusterScript in this example).</span></span>
   
   ```
   cd E:\IaaSClusterScript
   ```
3. <span data-ttu-id="18eca-190">Para implantar o cluster HPC Pack, execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="18eca-190">To deploy the HPC Pack cluster, run the following command.</span></span> <span data-ttu-id="18eca-191">Este exemplo supõe que o arquivo de configuração esteja localizado em E:\HPCDemoConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="18eca-191">This example assumes that the configuration file is located in E:\HPCDemoConfig.xml.</span></span>
   
   ```
   .\New-HpcIaaSCluster.ps1 –ConfigFile E:\HPCDemoConfig.xml –AdminUserName MyAdminName
   ```

<span data-ttu-id="18eca-192">O script de implantação do HPC Pack é executado por algum tempo.</span><span class="sxs-lookup"><span data-stu-id="18eca-192">The HPC Pack deployment script runs for some time.</span></span> <span data-ttu-id="18eca-193">Uma das ações do script é exportar e baixar o certificado do cluster e salvá-lo na pasta Documentos do usuário atual no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="18eca-193">One thing the script does is to export and download the cluster certificate and save it in the current user’s Documents folder on the client computer.</span></span> <span data-ttu-id="18eca-194">O script gera uma mensagem semelhante a mostrada a seguir.</span><span class="sxs-lookup"><span data-stu-id="18eca-194">The script generates a message similar to the following.</span></span> <span data-ttu-id="18eca-195">Em uma etapa posterior, você importa o certificado no repositório de certificados apropriado.</span><span class="sxs-lookup"><span data-stu-id="18eca-195">In a following step, you import the certificate in the appropriate certificate store.</span></span>    

    You have enabled REST API or web portal on HPC Pack head node. Please import the following certificate in the Trusted Root Certification Authorities certificate store on the computer where you are submitting job or accessing the HPC web portal:
    C:\Users\hpcuser\Documents\HPCWebComponent_HPCExcelHN004_20150707162011.cer

## <a name="step-2-offload-excel-workbooks-and-run-udfs-from-an-on-premises-client"></a><span data-ttu-id="18eca-196">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="18eca-196">Step 2.</span></span> <span data-ttu-id="18eca-197">Descarregaras pastas de trabalho do Excel e executar UDFs de um cliente local</span><span class="sxs-lookup"><span data-stu-id="18eca-197">Offload Excel workbooks and run UDFs from an on-premises client</span></span>
### <a name="excel-activation"></a><span data-ttu-id="18eca-198">Ativação do Excel</span><span class="sxs-lookup"><span data-stu-id="18eca-198">Excel activation</span></span>
<span data-ttu-id="18eca-199">Ao usar a imagem da VM ComputeNodeWithExcel para cargas de trabalho de produção, você precisa fornecer uma chave de licença válida do Microsoft Office para ativar o Excel nos nós de computação.</span><span class="sxs-lookup"><span data-stu-id="18eca-199">When using the ComputeNodeWithExcel VM image for production workloads, you need to provide a valid Microsoft Office license key to activate Excel on the compute nodes.</span></span> <span data-ttu-id="18eca-200">Caso contrário, a versão de avaliação do Excel expira após 30 dias e a execução das pastas de trabalho do Excel falhará com a COMException (0x800AC472).</span><span class="sxs-lookup"><span data-stu-id="18eca-200">Otherwise, the evaluation version of Excel expires after 30 days, and running Excel workbooks will fail with the COMException (0x800AC472).</span></span> 

<span data-ttu-id="18eca-201">É possível rearmar o Excel por mais 30 dias de tempo de avaliação: faça logon no nó de cabeçalho e execute clusrun em `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` em todos os nós de computação do Excel por meio do Gerenciador de Cluster HPC.</span><span class="sxs-lookup"><span data-stu-id="18eca-201">You can rearm Excel for another 30 days of evaluation time: Log on to the head node and clusrun `%ProgramFiles(x86)%\Microsoft Office\Office15\OSPPREARM.exe` on all Excel compute nodes via HPC Cluster Manager.</span></span> <span data-ttu-id="18eca-202">É possível rearmar, no máximo, duas vezes.</span><span class="sxs-lookup"><span data-stu-id="18eca-202">You can rearm a maximum of two times.</span></span> <span data-ttu-id="18eca-203">Depois disso, é necessário fornecer uma chave de licença válida do Office.</span><span class="sxs-lookup"><span data-stu-id="18eca-203">After that, you must provide a valid Office license key.</span></span>

<span data-ttu-id="18eca-204">O Office Professional Plus 2013 instalado na imagem de VM é uma edição de volume com uma GVLK (Chave de Licença de Volume Genérico).</span><span class="sxs-lookup"><span data-stu-id="18eca-204">The Office Professional Plus 2013 installed on the VM image is a volume edition with a Generic Volume License Key (GVLK).</span></span> <span data-ttu-id="18eca-205">Você pode ativá-la por meio do KMS (Serviço de Gerenciamento de Chaves)/da AD-BA (Ativação Baseada no Active Directory) ou de uma MAK (Chave de Ativação Múltipla).</span><span class="sxs-lookup"><span data-stu-id="18eca-205">You can activate it via Key Management Service (KMS)/Active Directory-Based Activation (AD-BA) or Multiple Activation Key (MAK).</span></span> 

    * <span data-ttu-id="18eca-206">Para usar o KMS/AD-BA, use um servidor KSM existente ou configure um novo usando o Pacote de Licença de Volume do Microsoft Office 2013.</span><span class="sxs-lookup"><span data-stu-id="18eca-206">To use KMS/AD-BA, use an existing KMS server or set up a new one by using the Microsoft Office 2013 Volume License Pack.</span></span> <span data-ttu-id="18eca-207">(Se você quiser, configure o servidor no nó do cabeçalho.) Em seguida, ative a chave do host KMS via Internet ou por telefone.</span><span class="sxs-lookup"><span data-stu-id="18eca-207">(If you want to, set up the server on the head node.) Then, activate the KMS host key via the Internet or telephone.</span></span> <span data-ttu-id="18eca-208">Em seguida, execute o cluster `ospp.vbs` para definir o servidor KMS e a porta, e ative o Office em todos os nós de computação do Excel.</span><span class="sxs-lookup"><span data-stu-id="18eca-208">Then clusrun `ospp.vbs` to set the KMS server and port and activate Office on all the Excel compute nodes.</span></span> 

    * <span data-ttu-id="18eca-209">Para usar a MAK, primeiramente execute o cluster `ospp.vbs` para inserir a chave e ative todos os nós de computação do Excel via Internet ou telefone.</span><span class="sxs-lookup"><span data-stu-id="18eca-209">To use MAK, first clusrun `ospp.vbs` to input the key and then activate all the Excel compute nodes via the Internet or telephone.</span></span> 

> [!NOTE]
> <span data-ttu-id="18eca-210">As chaves de produto de varejo do Office Professional Plus 2013 não podem ser usadas com essa imagem de VM.</span><span class="sxs-lookup"><span data-stu-id="18eca-210">Retail product keys for Office Professional Plus 2013 cannot be used with this VM image.</span></span> <span data-ttu-id="18eca-211">Se você tiver chaves válidas e mídia de instalação para as edições do Office ou do Excel diferentes desta edição de volume do Office Professional Plus 2013, será possível usá-las em seu lugar.</span><span class="sxs-lookup"><span data-stu-id="18eca-211">If you have valid keys and installation media for Office or Excel editions other than this Office Professional Plus 2013 volume edition, you can use them instead.</span></span> <span data-ttu-id="18eca-212">Primeiro desinstale esta edição de volume e instale a edição que você tem.</span><span class="sxs-lookup"><span data-stu-id="18eca-212">First uninstall this volume edition and install the edition that you have.</span></span> <span data-ttu-id="18eca-213">O nó de computação do Excel reinstalado pode ser capturado como uma imagem de VM personalizada para ser usada em uma implantação em escala.</span><span class="sxs-lookup"><span data-stu-id="18eca-213">The reinstalled Excel compute node can be captured as a customized VM image to use in a deployment at scale.</span></span>
> 
> 

### <a name="offload-excel-workbooks"></a><span data-ttu-id="18eca-214">Descarregar pastas de trabalho do Excel</span><span class="sxs-lookup"><span data-stu-id="18eca-214">Offload Excel workbooks</span></span>
<span data-ttu-id="18eca-215">Siga estas etapas para descarregar uma pasta de trabalho do Excel para que ela seja executada no cluster HPC Pack no Azure.</span><span class="sxs-lookup"><span data-stu-id="18eca-215">Follow these steps to offload an Excel workbook so that it runs on the HPC Pack cluster in Azure.</span></span> <span data-ttu-id="18eca-216">Para fazer isso, você deve ter o Excel 2010 ou 2013 já instalado no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="18eca-216">To do this, you must have Excel 2010 or 2013 already installed on the client computer.</span></span>

1. <span data-ttu-id="18eca-217">Use um dos métodos da Etapa 1 para implantar um cluster HPC Pack com a imagem do nó de computação do Excel.</span><span class="sxs-lookup"><span data-stu-id="18eca-217">Use one of the options in Step 1 to deploy an HPC Pack cluster with the Excel compute node image.</span></span> <span data-ttu-id="18eca-218">Obter o arquivo de certificado (.cer) do cluster e o nome de usuário e a senha.</span><span class="sxs-lookup"><span data-stu-id="18eca-218">Obtain the cluster certificate file (.cer) and cluster username and password.</span></span>
2. <span data-ttu-id="18eca-219">No computador cliente, importe o certificado de cluster em Cert:\CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="18eca-219">On the client computer, import the cluster certificate under Cert:\CurrentUser\Root.</span></span>
3. <span data-ttu-id="18eca-220">Verifique se o Excel está instalado.</span><span class="sxs-lookup"><span data-stu-id="18eca-220">Make sure Excel is installed.</span></span> <span data-ttu-id="18eca-221">Crie um arquivo Excel.exe.config com o conteúdo a seguir na mesma pasta do Excel.exe no computador cliente.</span><span class="sxs-lookup"><span data-stu-id="18eca-221">Create an Excel.exe.config file with the following contents in the same folder as Excel.exe on the client computer.</span></span> <span data-ttu-id="18eca-222">Essa etapa garante que o suplemento COM do Excel no HPC Pack 2012 R2 é carregado com êxito.</span><span class="sxs-lookup"><span data-stu-id="18eca-222">This step ensures that the HPC Pack 2012 R2 Excel COM add-in loads successfully.</span></span>
   
    ```
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.0"/>
        </startup>
    </configuration>
    ```
4. <span data-ttu-id="18eca-223">Configure o cliente para enviar trabalhos para o cluster HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="18eca-223">Set up the client to submit jobs to the HPC Pack cluster.</span></span> <span data-ttu-id="18eca-224">Uma opção é baixar a [instalação completa do HPC Pack 2012 R2 Atualização 3](http://www.microsoft.com/download/details.aspx?id=49922) e instalar o cliente do HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="18eca-224">One option is to download the full [HPC Pack 2012 R2 Update 3 installation](http://www.microsoft.com/download/details.aspx?id=49922) and install the HPC Pack client.</span></span> <span data-ttu-id="18eca-225">Como alternativa, baixe e instale os [utilitários de cliente do HPC Pack 2012 R2 Atualização 3](https://www.microsoft.com/download/details.aspx?id=49923) e o Visual C++ 2010 redistribuível adequado para seu computador ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span><span class="sxs-lookup"><span data-stu-id="18eca-225">Alternatively, download and install the [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923) and the appropriate Visual C++ 2010 redistributable for your computer ([x64](http://www.microsoft.com/download/details.aspx?id=14632), [x86](https://www.microsoft.com/download/details.aspx?id=5555)).</span></span>
5. <span data-ttu-id="18eca-226">Neste exemplo, usamos uma pasta de trabalho do Excel de exemplo chamada ConvertiblePricing_Complete.xlsb.</span><span class="sxs-lookup"><span data-stu-id="18eca-226">In this example, we use a sample Excel workbook named ConvertiblePricing_Complete.xlsb.</span></span> <span data-ttu-id="18eca-227">Você pode baixá-lo [aqui](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span><span class="sxs-lookup"><span data-stu-id="18eca-227">You can download it [here](https://www.microsoft.com/en-us/download/details.aspx?id=2939).</span></span>
6. <span data-ttu-id="18eca-228">Copie a pasta de trabalho do Excel para uma pasta de trabalho, como D:\Excel\Run.</span><span class="sxs-lookup"><span data-stu-id="18eca-228">Copy the Excel workbook to a working folder such as D:\Excel\Run.</span></span>
7. <span data-ttu-id="18eca-229">Abra a pasta de trabalho do Excel.</span><span class="sxs-lookup"><span data-stu-id="18eca-229">Open the Excel workbook.</span></span> <span data-ttu-id="18eca-230">Na faixa de opções **Desenvolver**, clique em **Suplementos COM** e confirme se o suplemento COM do HPC Pack do Excel foi carregado com êxito.</span><span class="sxs-lookup"><span data-stu-id="18eca-230">On the **Develop** ribbon, click **COM Add-Ins** and confirm that the HPC Pack Excel COM add-in is loaded successfully.</span></span>
   
   ![Suplemento do Excel para o HPC Pack][addin]
8. <span data-ttu-id="18eca-232">Edite a macro do VBA HPCControlMacros no Excel, alterando as linhas comentadas, conforme mostrado no script a seguir.</span><span class="sxs-lookup"><span data-stu-id="18eca-232">Edit the VBA macro HPCControlMacros in Excel by changing the commented lines as shown in the following script.</span></span> <span data-ttu-id="18eca-233">Substitua os valores apropriados para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="18eca-233">Substitute appropriate values for your environment.</span></span>
   
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
9. <span data-ttu-id="18eca-235">Copie a pasta de trabalho do Excel e, um diretório de upload como D:\Excel\Upload.</span><span class="sxs-lookup"><span data-stu-id="18eca-235">Copy the Excel workbook to an upload directory such as D:\Excel\Upload.</span></span> <span data-ttu-id="18eca-236">Esse diretório é especificado na constante HPC_DependsFiles na macro VBA.</span><span class="sxs-lookup"><span data-stu-id="18eca-236">This directory is specified in the HPC_DependsFiles constant in the VBA macro.</span></span>
10. <span data-ttu-id="18eca-237">Para executar a pasta de trabalho no cluster do Azure, clique no botão **Cluster** na planilha.</span><span class="sxs-lookup"><span data-stu-id="18eca-237">To run the workbook on the cluster in Azure, click the **Cluster** button on the worksheet.</span></span>

### <a name="run-excel-udfs"></a><span data-ttu-id="18eca-238">Executar UDFs do Excel</span><span class="sxs-lookup"><span data-stu-id="18eca-238">Run Excel UDFs</span></span>
<span data-ttu-id="18eca-239">Para executar UDFs do Excel, siga as etapas de 1 a 3 acima para configurar o computador cliente.</span><span class="sxs-lookup"><span data-stu-id="18eca-239">To run Excel UDFs, follow the preceding steps 1 – 3 to set up the client computer.</span></span> <span data-ttu-id="18eca-240">Para UDFs do Excel, não é necessário ter o aplicativo do Excel instalado em nós de computação.</span><span class="sxs-lookup"><span data-stu-id="18eca-240">For Excel UDFs, you don't need to have the Excel application installed on compute nodes.</span></span> <span data-ttu-id="18eca-241">Portanto, ao criar os nós de computação do cluster, você poderá escolher uma imagem de nó de computação normal em vez da imagem do nó de computação com o Excel.</span><span class="sxs-lookup"><span data-stu-id="18eca-241">So, when creating your cluster compute nodes, you could choose a normal compute node image instead of the compute node image with Excel.</span></span>

> [!NOTE]
> <span data-ttu-id="18eca-242">Há um limite de 34 caracteres no Excel 2010 e a caixa de diálogo do conector de cluster 2013.</span><span class="sxs-lookup"><span data-stu-id="18eca-242">There is a 34 character limit in the Excel 2010 and 2013 cluster connector dialog box.</span></span> <span data-ttu-id="18eca-243">Use essa caixa de diálogo para especificar o cluster que executa as UDFs.</span><span class="sxs-lookup"><span data-stu-id="18eca-243">You use this dialog box to specify the cluster that runs the UDFs.</span></span> <span data-ttu-id="18eca-244">Se o nome completo do cluster for maior (por exemplo, hpcexcelhn01.southeastasia.cloudapp.azure.com), ele não caberá na caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="18eca-244">If the full cluster name is longer (for example, hpcexcelhn01.southeastasia.cloudapp.azure.com), it does not fit in the dialog box.</span></span> <span data-ttu-id="18eca-245">A solução alternativa é definir uma variável de todo o computador, como *CCP_IAASHN* com o valor do nome de cluster longo.</span><span class="sxs-lookup"><span data-stu-id="18eca-245">The workaround is to set a machine-wide variable such as *CCP_IAASHN* with the value of the long cluster name.</span></span> <span data-ttu-id="18eca-246">Em seguida, digite *%CCP_IAASHN%* na caixa de diálogo como o nome do nó do cabeçalho do cluster.</span><span class="sxs-lookup"><span data-stu-id="18eca-246">Then, enter *%CCP_IAASHN%* in the dialog box as the cluster head node name.</span></span> 
> 
> 

<span data-ttu-id="18eca-247">Depois que o cluster for implantado com êxito, continue com as etapas a seguir para executar um exemplo interno do UDF do Excel.</span><span class="sxs-lookup"><span data-stu-id="18eca-247">After the cluster is successfully deployed, continue with the following steps to run a sample built-in Excel UDF.</span></span> <span data-ttu-id="18eca-248">Para UDFs personalizados do Excel, consulte estes [recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) para compilar os XLLs e implantá-los no cluster IaaS.</span><span class="sxs-lookup"><span data-stu-id="18eca-248">For customized Excel UDFs, see these [resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) to build the XLLs and deploy them on the IaaS cluster.</span></span>

1. <span data-ttu-id="18eca-249">Abra uma nova pasta de trabalho do Excel.</span><span class="sxs-lookup"><span data-stu-id="18eca-249">Open a new Excel workbook.</span></span> <span data-ttu-id="18eca-250">Na faixa de opções **Desenvolver**, clique em **Suplementos**.</span><span class="sxs-lookup"><span data-stu-id="18eca-250">On the **Develop** ribbon, click **Add-Ins**.</span></span> <span data-ttu-id="18eca-251">Em seguida, na caixa de diálogo, clique em **Procurar**, navegue até a pasta %CCP_HOME%Bin\XLL32 e selecione o exemplo ClusterUDF32.xll.</span><span class="sxs-lookup"><span data-stu-id="18eca-251">Then, in the dialog box, click **Browse**, navigate to the %CCP_HOME%Bin\XLL32 folder, and select the sample ClusterUDF32.xll.</span></span> <span data-ttu-id="18eca-252">Se o ClusterUDF32 não existir no computador cliente, copie-o da pasta %CCP_HOME%Bin\XLL32 no nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="18eca-252">If the ClusterUDF32 doesn't exist on the client machine, copy it from the %CCP_HOME%Bin\XLL32 folder on the head node.</span></span>
   
   ![Selecionar o UDF][udf]
2. <span data-ttu-id="18eca-254">Clique em **Arquivo** > **Opções** > **Avançadas**.</span><span class="sxs-lookup"><span data-stu-id="18eca-254">Click **File** > **Options** > **Advanced**.</span></span> <span data-ttu-id="18eca-255">Em **Fórmulas**, marque a opção **Permitir que as funções XLL definidas pelo usuário executem um cluster de cálculo**.</span><span class="sxs-lookup"><span data-stu-id="18eca-255">Under **Formulas**, check **Allow user-defined XLL functions to run a compute cluster**.</span></span> <span data-ttu-id="18eca-256">Então, clique em **Opções** e digite o nome completo do cluster em **Nome do nó do cabeçalho do cluster**.</span><span class="sxs-lookup"><span data-stu-id="18eca-256">Then click **Options** and enter the full cluster name in **Cluster head node name**.</span></span> <span data-ttu-id="18eca-257">Conforme observado anteriormente, essa caixa de entrada é limitada a 34 caracteres, de modo que um nome de cluster longo pode não caber.</span><span class="sxs-lookup"><span data-stu-id="18eca-257">(As noted previously this input box is limited to 34 characters, so a long cluster name may not fit.</span></span> <span data-ttu-id="18eca-258">Você pode usar variáveis de todo o computador aqui para nomes de cluster longos.</span><span class="sxs-lookup"><span data-stu-id="18eca-258">You may use a machine-wide variable here for a long cluster name.)</span></span>
   
   ![Configurar o UDF][options]
3. <span data-ttu-id="18eca-260">Para executar o cálculo de UDF no cluster, clique na célula com o valor =XllGetComputerNameC() e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="18eca-260">To run the UDF calculation on the cluster, click the cell with value =XllGetComputerNameC() and press Enter.</span></span> <span data-ttu-id="18eca-261">A função apenas recupera o nome do nó de computação no qual uma UDF é executada.</span><span class="sxs-lookup"><span data-stu-id="18eca-261">The function simply retrieves the name of the compute node on which the UDF runs.</span></span> <span data-ttu-id="18eca-262">Para a primeira execução, uma caixa de diálogo de credenciais solicita o nome de usuário e a senha para se conectar ao cluster IaaS.</span><span class="sxs-lookup"><span data-stu-id="18eca-262">For the first run, a credentials dialog box prompts for the username and password to connect to the IaaS cluster.</span></span>
   
   ![Executar UDF][run]
   
   <span data-ttu-id="18eca-264">Quando houver uma grande quantidade de células para calcular, pressione Alt-Shift-Ctrl + F9 para executar o cálculo em todas as células.</span><span class="sxs-lookup"><span data-stu-id="18eca-264">When there are many cells to calculate, press Alt-Shift-Ctrl + F9 to run the calculation on all cells.</span></span>

## <a name="step-3-run-a-soa-workload-from-an-on-premises-client"></a><span data-ttu-id="18eca-265">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="18eca-265">Step 3.</span></span> <span data-ttu-id="18eca-266">Executar uma carga de trabalho SOA a partir de um cliente local</span><span class="sxs-lookup"><span data-stu-id="18eca-266">Run a SOA workload from an on-premises client</span></span>
<span data-ttu-id="18eca-267">Para executar aplicativos gerais de SOA no cluster HPC Pack de IaaS, primeiro use um dos métodos da Etapa 1 para implantar o cluster.</span><span class="sxs-lookup"><span data-stu-id="18eca-267">To run general SOA applications on the HPC Pack IaaS cluster, first use one of the methods in Step 1 to deploy the cluster.</span></span> <span data-ttu-id="18eca-268">Nesse caso, especifique uma imagem genérica de nó de computação, pois você não precisará do Excel nos nós de computação.</span><span class="sxs-lookup"><span data-stu-id="18eca-268">Specify a generic compute node image in this case, because you do not need Excel on the compute nodes.</span></span> <span data-ttu-id="18eca-269">Depois, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="18eca-269">Then follow these steps.</span></span>

1. <span data-ttu-id="18eca-270">Após receber o certificado do cluster, importe-o para o computador cliente em Cert:\CurrentUser\Root.</span><span class="sxs-lookup"><span data-stu-id="18eca-270">After retrieving the cluster certificate, import it on the client computer under Cert:\CurrentUser\Root.</span></span>
2. <span data-ttu-id="18eca-271">Instale o [SDK do HPC Pack 2012 R2 Atualização 3](http://www.microsoft.com/download/details.aspx?id=49921) e [Utilitários de cliente do HPC Pack 2012 R2 Atualização 3](https://www.microsoft.com/download/details.aspx?id=49923).</span><span class="sxs-lookup"><span data-stu-id="18eca-271">Install the [HPC Pack 2012 R2 Update 3 SDK](http://www.microsoft.com/download/details.aspx?id=49921) and [HPC Pack 2012 R2 Update 3 client utilities](https://www.microsoft.com/download/details.aspx?id=49923).</span></span> <span data-ttu-id="18eca-272">Essas ferramentas permitem que você desenvolva e execute aplicativos cliente de SOA.</span><span class="sxs-lookup"><span data-stu-id="18eca-272">These tools enable you to develop and run SOA client applications.</span></span>
3. <span data-ttu-id="18eca-273">Baixe o [código de exemplo](https://www.microsoft.com/download/details.aspx?id=41633)HelloWorldR2.</span><span class="sxs-lookup"><span data-stu-id="18eca-273">Download the HelloWorldR2 [sample code](https://www.microsoft.com/download/details.aspx?id=41633).</span></span> <span data-ttu-id="18eca-274">Abra o HelloWorldR2.sln no Visual Studio 2010 ou 2012.</span><span class="sxs-lookup"><span data-stu-id="18eca-274">Open the HelloWorldR2.sln in Visual Studio 2010 or 2012.</span></span> <span data-ttu-id="18eca-275">(Atualmente, este exemplo não é compatível com versões mais recentes do Visual Studio.)</span><span class="sxs-lookup"><span data-stu-id="18eca-275">(This sample is not currently compatible with more recent versions of Visual Studio.)</span></span>
4. <span data-ttu-id="18eca-276">Crie o projeto EchoService primeiro.</span><span class="sxs-lookup"><span data-stu-id="18eca-276">Build the EchoService project first.</span></span> <span data-ttu-id="18eca-277">Em seguida, implante o serviço no cluster de IaaS da mesma maneira que você o implanta em um cluster local.</span><span class="sxs-lookup"><span data-stu-id="18eca-277">Then, deploy the service to the IaaS cluster in the same way you deploy to an on-premises cluster.</span></span> <span data-ttu-id="18eca-278">Para obter etapas detalhadas, consulte o Leiame.doc no HelloWordR2.</span><span class="sxs-lookup"><span data-stu-id="18eca-278">For detailed steps, see the Readme.doc in HelloWordR2.</span></span> <span data-ttu-id="18eca-279">Modifique e crie o HelloWorldR2 e outros projetos, conforme descrito na seção a seguir, para gerar os aplicativos cliente de SOA que são executados em um cluster de IaaS do Azure.</span><span class="sxs-lookup"><span data-stu-id="18eca-279">Modify and build the HellWorldR2 and other projects as described in the following section to generate the SOA client applications that run on an Azure IaaS cluster.</span></span>

### <a name="use-http-binding-with-azure-storage-queue"></a><span data-ttu-id="18eca-280">Usar associação Http com fila de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="18eca-280">Use Http binding with Azure storage queue</span></span>
<span data-ttu-id="18eca-281">Para usar a associação de Http com uma fila de armazenamento do Azure, faça algumas alterações no código de exemplo.</span><span class="sxs-lookup"><span data-stu-id="18eca-281">To use Http binding with an Azure storage queue, make a few changes to the sample code.</span></span>

* <span data-ttu-id="18eca-282">Atualize o nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="18eca-282">Update the cluster name.</span></span>
  
    ```
  // Before
  const string headnode = "[headnode]";
  // After e.g.
  const string headnode = "hpc01.eastus.cloudapp.azure.com";
  or
  const string headnode = "hpc01.cloudapp.net";
  ```
* <span data-ttu-id="18eca-283">Se preferir, use o TransportScheme padrão em SessionStartInfo ou defina-o explicitamente como Http.</span><span class="sxs-lookup"><span data-stu-id="18eca-283">Optionally, use the default TransportScheme in SessionStartInfo or explicitly set it to Http.</span></span>

```
    info.TransportScheme = TransportScheme.Http;
```

* <span data-ttu-id="18eca-284">Use a associação padrão para o BrokerClient.</span><span class="sxs-lookup"><span data-stu-id="18eca-284">Use default binding for the BrokerClient.</span></span>
  
    ```
  // Before
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session, binding))
  // After
  using (BrokerClient<IService1> client = new BrokerClient<IService1>(session))
  ```
  
    <span data-ttu-id="18eca-285">Ou defina explicitamente usando o basicHttpBinding.</span><span class="sxs-lookup"><span data-stu-id="18eca-285">Or set explicitly using the basicHttpBinding.</span></span>
  
    ```
  BasicHttpBinding binding = new BasicHttpBinding(BasicHttpSecurityMode.TransportWithMessageCredential);
  binding.Security.Message.ClientCredentialType = BasicHttpMessageCredentialType.UserName;    binding.Security.Transport.ClientCredentialType = HttpClientCredentialType.None;
  ```
* <span data-ttu-id="18eca-286">Opcionalmente, defina o sinalizador UseAzureQueue como verdadeiro na SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="18eca-286">Optionally, set the UseAzureQueue flag to true in SessionStartInfo.</span></span> <span data-ttu-id="18eca-287">Se não estiver configurado, ele será definido como true por padrão quando o nome do cluster tiver sufixos de domínio do Azure e o TransportScheme for Http.</span><span class="sxs-lookup"><span data-stu-id="18eca-287">If not set, it will be set to true by default when the cluster name has Azure domain suffixes and the TransportScheme is Http.</span></span>
  
    ```
    info.UseAzureQueue = true;
  ```

### <a name="use-http-binding-without-azure-storage-queue"></a><span data-ttu-id="18eca-288">Usar associação Http sem fila de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="18eca-288">Use Http binding without Azure storage queue</span></span>
<span data-ttu-id="18eca-289">Para usar a associação de HTTP sem uma fila de armazenamento do Azure, defina explicitamente o sinalizador UseAzureQueue como false em SessionStartInfo.</span><span class="sxs-lookup"><span data-stu-id="18eca-289">To use Http binding without an Azure storage queue, explicitly set the UseAzureQueue flag to false in the SessionStartInfo.</span></span>

```
    info.UseAzureQueue = false;
```

### <a name="use-nettcp-binding"></a><span data-ttu-id="18eca-290">Usar associação NetTcp</span><span class="sxs-lookup"><span data-stu-id="18eca-290">Use NetTcp binding</span></span>
<span data-ttu-id="18eca-291">Para usar a associação NetTcp, a configuração é semelhante a conectar-se a um cluster local.</span><span class="sxs-lookup"><span data-stu-id="18eca-291">To use NetTcp binding, the configuration is similar to connecting to an on-premises cluster.</span></span> <span data-ttu-id="18eca-292">Você precisa abrir alguns pontos de extremidade na VM do nó de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="18eca-292">You need to open a few endpoints on the head node VM.</span></span> <span data-ttu-id="18eca-293">Se você usou o script de implantação de IaaS do HPC Pack para criar o cluster, por exemplo, defina os pontos de extremidade no portal do Azure, conforme descrito a seguir.</span><span class="sxs-lookup"><span data-stu-id="18eca-293">If you used the HPC Pack IaaS deployment script to create the cluster, for example, set the endpoints in the Azure portal as follows.</span></span>

1. <span data-ttu-id="18eca-294">Pare a VM.</span><span class="sxs-lookup"><span data-stu-id="18eca-294">Stop the VM.</span></span>
2. <span data-ttu-id="18eca-295">Adicione as portas TCP 9090, 9087, 9091 e 9094 para a Sessão, Agente, trabalho do Agente e Serviços de dados, respectivamente</span><span class="sxs-lookup"><span data-stu-id="18eca-295">Add the TCP ports 9090, 9087, 9091, 9094 for the Session, Broker, Broker worker, and Data services, respectively</span></span>
   
    ![Configurar pontos de extremidade][endpoint-new-portal]
3. <span data-ttu-id="18eca-297">Inicie a VM.</span><span class="sxs-lookup"><span data-stu-id="18eca-297">Start the VM.</span></span>

<span data-ttu-id="18eca-298">O aplicativo cliente SOA não requer alterações, exceto do nome principal para o nome completo do cluster IaaS.</span><span class="sxs-lookup"><span data-stu-id="18eca-298">The SOA client application requires no changes except altering the head name to the IaaS cluster full name.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18eca-299">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="18eca-299">Next steps</span></span>
* <span data-ttu-id="18eca-300">Consulte [estes recursos](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) para saber mais sobre como executar cargas de trabalho do Excel com o HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="18eca-300">See [these resources](http://social.technet.microsoft.com/wiki/contents/articles/1198.windows-hpc-and-microsoft-excel-resources-for-building-cluster-ready-workbooks.aspx) for more information about running Excel workloads with HPC Pack.</span></span>
* <span data-ttu-id="18eca-301">Consulte [Gerenciamento de serviços SOA no Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) para saber mais sobre como implantar e gerenciar serviços SOA com HPC Pack.</span><span class="sxs-lookup"><span data-stu-id="18eca-301">See [Managing SOA Services in Microsoft HPC Pack](https://technet.microsoft.com/library/ff919412.aspx) for more about deploying and managing SOA services with HPC Pack.</span></span>

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
