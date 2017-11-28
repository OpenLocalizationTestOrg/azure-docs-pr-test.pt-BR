---
title: "nós - Azure lote de computação aaaRun Linux na máquina virtual | Microsoft Docs"
description: "Saiba como tooprocess paralela computação cargas de trabalho em grupos de máquinas virtuais Linux no lote do Azure."
services: batch
documentationcenter: python
author: tamram
manager: timlt
editor: 
ms.assetid: dc6ba151-1718-468a-b455-2da549225ab2
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: na
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3daabd5c577baaafd0544f9f7913cb7b116d74d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="provision-linux-compute-nodes-in-batch-pools"></a><span data-ttu-id="e10f7-103">Provisionar os nós de computação do Linux em pools do Lote</span><span class="sxs-lookup"><span data-stu-id="e10f7-103">Provision Linux compute nodes in Batch pools</span></span>

<span data-ttu-id="e10f7-104">Você pode usar cargas de trabalho do Azure Batch toorun computação paralela em máquinas virtuais Linux e Windows.</span><span class="sxs-lookup"><span data-stu-id="e10f7-104">You can use Azure Batch toorun parallel compute workloads on both Linux and Windows virtual machines.</span></span> <span data-ttu-id="e10f7-105">Este artigo detalha como pools de toocreate do Linux nós de computação no serviço de lote hello usando ambos os Olá [lote Python] [ py_batch_package] e [Batch .NET] [ api_net] bibliotecas de cliente.</span><span class="sxs-lookup"><span data-stu-id="e10f7-105">This article details how toocreate pools of Linux compute nodes in hello Batch service by using both hello [Batch Python][py_batch_package] and [Batch .NET][api_net] client libraries.</span></span>

> [!NOTE]
> <span data-ttu-id="e10f7-106">Os pacotes de aplicativos têm suporte em todos os pools do Lote criados após 5 de julho de 2017.</span><span class="sxs-lookup"><span data-stu-id="e10f7-106">Application packages are supported on all Batch pools created after 5 July 2017.</span></span> <span data-ttu-id="e10f7-107">Eles têm suporte em pools de lote criados entre 10 de março de 2016 e 5 de julho de 2017 somente se o pool de saudação foi criado usando uma configuração de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e10f7-107">They are supported on Batch pools created between 10 March 2016 and 5 July 2017 only if hello pool was created using a Cloud Service configuration.</span></span> <span data-ttu-id="e10f7-108">Pools de lote criados too10 anterior de março de 2016 não dão suporte a pacotes de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e10f7-108">Batch pools created prior too10 March 2016 do not support application packages.</span></span> <span data-ttu-id="e10f7-109">Para obter mais informações sobre como usar o aplicativo pacotes toodeploy seus nós de lote de tooyour de aplicativos, consulte [implantar aplicativos toocompute nós com pacotes de aplicativos de lote](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="e10f7-109">For more information about using application packages toodeploy your applications tooyour Batch nodes, see [Deploy applications toocompute nodes with Batch application packages](batch-application-packages.md).</span></span>
>
>

## <a name="virtual-machine-configuration"></a><span data-ttu-id="e10f7-110">Configuração de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e10f7-110">Virtual machine configuration</span></span>
<span data-ttu-id="e10f7-111">Quando você cria um conjunto de nós de computação em lote, você tem duas opções de tamanho de nó tooselect hello e do sistema operacional: configuração de máquina Virtual e a configuração de serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="e10f7-111">When you create a pool of compute nodes in Batch, you have two options from which tooselect hello node size and operating system: Cloud Services Configuration and Virtual Machine Configuration.</span></span>

<span data-ttu-id="e10f7-112">**Configuração dos Serviços de Nuvem** fornece *apenas*.</span><span class="sxs-lookup"><span data-stu-id="e10f7-112">**Cloud Services Configuration** provides Windows compute nodes *only*.</span></span> <span data-ttu-id="e10f7-113">Tamanhos de nós de computação disponíveis são listados na [tamanhos para serviços de nuvem](../cloud-services/cloud-services-sizes-specs.md), e sistemas operacionais disponíveis são listados na Olá [versões do sistema operacional de convidado do Azure e matriz de compatibilidade do SDK](../cloud-services/cloud-services-guestos-update-matrix.md).</span><span class="sxs-lookup"><span data-stu-id="e10f7-113">Available compute node sizes are listed in [Sizes for Cloud Services](../cloud-services/cloud-services-sizes-specs.md), and available operating systems are listed in hello [Azure Guest OS releases and SDK compatibility matrix](../cloud-services/cloud-services-guestos-update-matrix.md).</span></span> <span data-ttu-id="e10f7-114">Quando você cria um pool que contém nós de serviços de nuvem do Azure, especifique o tamanho do nó de saudação e hello família de sistemas operacionais, que são descritos em Olá mencionado anteriormente artigos.</span><span class="sxs-lookup"><span data-stu-id="e10f7-114">When you create a pool that contains Azure Cloud Services nodes, you specify hello node size and hello OS family, which are described in hello previously mentioned articles.</span></span> <span data-ttu-id="e10f7-115">No caso de pools de nós de computação do Windows, os Serviços de Nuvem são usados com mais frequência.</span><span class="sxs-lookup"><span data-stu-id="e10f7-115">For pools of Windows compute nodes, Cloud Services is most commonly used.</span></span>

<span data-ttu-id="e10f7-116">**Virtual Machine Configuration** fornece imagens do Linux e do Windows para os nós de computação.</span><span class="sxs-lookup"><span data-stu-id="e10f7-116">**Virtual Machine Configuration** provides both Linux and Windows images for compute nodes.</span></span> <span data-ttu-id="e10f7-117">Os tamanhos de nó de computação disponíveis estão relacionados em [Tamanhos das máquinas virtuais no Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) e em [Tamanhos das máquinas virtuais no Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span><span class="sxs-lookup"><span data-stu-id="e10f7-117">Available compute node sizes are listed in [Sizes for virtual machines in Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) and [Sizes for virtual machines in Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows).</span></span> <span data-ttu-id="e10f7-118">Quando você cria um pool que contém nós de configuração de máquina Virtual, você deve especificar o tamanho de saudação de nós hello, referência de imagem de máquina virtual hello e Olá lote nó agente SKU toobe instalada em nós de saudação.</span><span class="sxs-lookup"><span data-stu-id="e10f7-118">When you create a pool that contains Virtual Machine Configuration nodes, you must specify hello size of hello nodes, hello virtual machine image reference, and hello Batch node agent SKU toobe installed on hello nodes.</span></span>

### <a name="virtual-machine-image-reference"></a><span data-ttu-id="e10f7-119">Referência da imagem da máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e10f7-119">Virtual machine image reference</span></span>
<span data-ttu-id="e10f7-120">Olá serviço de lote usa [conjuntos de escala de máquina virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux nós de computação.</span><span class="sxs-lookup"><span data-stu-id="e10f7-120">hello Batch service uses [virtual machine scale sets](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux compute nodes.</span></span> <span data-ttu-id="e10f7-121">Você pode especificar uma imagem de saudação [Azure Marketplace][vm_marketplace], ou forneça uma imagem personalizada que você preparou.</span><span class="sxs-lookup"><span data-stu-id="e10f7-121">You can specify an image from hello [Azure Marketplace][vm_marketplace], or provide a custom image that you have prepared.</span></span> <span data-ttu-id="e10f7-122">Para obter mais detalhes sobre imagens personalizadas, confira [Desenvolver soluções de computação paralela em grande escala com o Lote](batch-api-basics.md#pool).</span><span class="sxs-lookup"><span data-stu-id="e10f7-122">For more details about custom images, see [Develop large-scale parallel compute solutions with Batch](batch-api-basics.md#pool).</span></span>

<span data-ttu-id="e10f7-123">Quando você configura uma referência de imagem de máquina virtual, você especificar propriedades de saudação da imagem de máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="e10f7-123">When you configure a virtual machine image reference, you specify hello properties of hello virtual machine image.</span></span> <span data-ttu-id="e10f7-124">Olá propriedades a seguir é necessária quando você cria uma referência de imagem de máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="e10f7-124">hello following properties are required when you create a virtual machine image reference:</span></span>

| <span data-ttu-id="e10f7-125">**Propriedades de referência de imagem**</span><span class="sxs-lookup"><span data-stu-id="e10f7-125">**Image reference properties**</span></span> | <span data-ttu-id="e10f7-126">**Exemplo**</span><span class="sxs-lookup"><span data-stu-id="e10f7-126">**Example**</span></span> |
| --- | --- |
| <span data-ttu-id="e10f7-127">Publicador</span><span class="sxs-lookup"><span data-stu-id="e10f7-127">Publisher</span></span> |<span data-ttu-id="e10f7-128">Canônico</span><span class="sxs-lookup"><span data-stu-id="e10f7-128">Canonical</span></span> |
| <span data-ttu-id="e10f7-129">Oferta</span><span class="sxs-lookup"><span data-stu-id="e10f7-129">Offer</span></span> |<span data-ttu-id="e10f7-130">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="e10f7-130">UbuntuServer</span></span> |
| <span data-ttu-id="e10f7-131">SKU</span><span class="sxs-lookup"><span data-stu-id="e10f7-131">SKU</span></span> |<span data-ttu-id="e10f7-132">14.04.4-LTS</span><span class="sxs-lookup"><span data-stu-id="e10f7-132">14.04.4-LTS</span></span> |
| <span data-ttu-id="e10f7-133">Versão</span><span class="sxs-lookup"><span data-stu-id="e10f7-133">Version</span></span> |<span data-ttu-id="e10f7-134">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-134">latest</span></span> |

> [!TIP]
> <span data-ttu-id="e10f7-135">Você pode aprender mais sobre essas propriedades e como toolist Marketplace imagens no [navegue e selecionadas imagens de máquinas virtuais Linux no Azure com CLI ou o PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e10f7-135">You can learn more about these properties and how toolist Marketplace images in [Navigate and select Linux virtual machine images in Azure with CLI or PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="e10f7-136">Observe que nem todas as imagens do Marketplace são compatíveis com o Lote no momento.</span><span class="sxs-lookup"><span data-stu-id="e10f7-136">Note that not all Marketplace images are currently compatible with Batch.</span></span> <span data-ttu-id="e10f7-137">Para saber mais, confira [SKU do agente do nó](#node-agent-sku).</span><span class="sxs-lookup"><span data-stu-id="e10f7-137">For more information, see [Node agent SKU](#node-agent-sku).</span></span>
>
>

### <a name="node-agent-sku"></a><span data-ttu-id="e10f7-138">SKU do agente do nó</span><span class="sxs-lookup"><span data-stu-id="e10f7-138">Node agent SKU</span></span>
<span data-ttu-id="e10f7-139">Agente de nó de lote de saudação é um programa que é executado em cada nó no pool de saudação e fornece a interface de comando e controle de saudação entre nó hello e serviço de lote de saudação.</span><span class="sxs-lookup"><span data-stu-id="e10f7-139">hello Batch node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="e10f7-140">Há várias implementações de agente do nó hello, conhecido como SKUs para diferentes sistemas operacionais.</span><span class="sxs-lookup"><span data-stu-id="e10f7-140">There are different implementations of hello node agent, known as SKUs, for different operating systems.</span></span> <span data-ttu-id="e10f7-141">Essencialmente, quando você cria uma configuração de máquina Virtual, você primeiro especificar a referência de imagem de máquina virtual hello e especifique Olá nó agente tooinstall na imagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="e10f7-141">Essentially, when you create a Virtual Machine Configuration, you first specify hello virtual machine image reference, and then you specify hello node agent tooinstall on hello image.</span></span> <span data-ttu-id="e10f7-142">Normalmente, cada SKU do agente do nó é compatível com várias imagens de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e10f7-142">Typically, each node agent SKU is compatible with multiple virtual machine images.</span></span> <span data-ttu-id="e10f7-143">Aqui estão alguns exemplos de SKUs do agente do nó:</span><span class="sxs-lookup"><span data-stu-id="e10f7-143">Here are a few examples of node agent SKUs:</span></span>

* <span data-ttu-id="e10f7-144">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="e10f7-144">batch.node.ubuntu 14.04</span></span>
* <span data-ttu-id="e10f7-145">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="e10f7-145">batch.node.centos 7</span></span>
* <span data-ttu-id="e10f7-146">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="e10f7-146">batch.node.windows amd64</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e10f7-147">Nem todas as imagens de máquinas virtuais que estão disponíveis no mercado de saudação são compatíveis com os agentes de nó em lotes atualmente disponíveis hello.</span><span class="sxs-lookup"><span data-stu-id="e10f7-147">Not all virtual machine images that are available in hello Marketplace are compatible with hello currently available Batch node agents.</span></span> <span data-ttu-id="e10f7-148">Use o agente Olá SDKs de lote toolist Olá nó disponível SKUs e Olá imagens da máquina virtual com a qual eles são compatíveis.</span><span class="sxs-lookup"><span data-stu-id="e10f7-148">Use hello Batch SDKs toolist hello available node agent SKUs and hello virtual machine images with which they are compatible.</span></span> <span data-ttu-id="e10f7-149">Consulte Olá [imagens da lista de máquina Virtual](#list-of-virtual-machine-images) posteriormente neste artigo para obter mais informações e exemplos de como tooretrieve uma lista de imagens válidas no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="e10f7-149">See hello [List of Virtual Machine images](#list-of-virtual-machine-images) later in this article for more information and examples of how tooretrieve a list of valid images at runtime.</span></span>
>
>

## <a name="create-a-linux-pool-batch-python"></a><span data-ttu-id="e10f7-150">Criar um pool do Linux: Python do Lote</span><span class="sxs-lookup"><span data-stu-id="e10f7-150">Create a Linux pool: Batch Python</span></span>
<span data-ttu-id="e10f7-151">Olá, trecho de código a seguir mostra um exemplo de como Olá toouse [biblioteca de cliente de lote do Microsoft Azure para Python] [ py_batch_package] toocreate um pool de servidor do Ubuntu nós de computação.</span><span class="sxs-lookup"><span data-stu-id="e10f7-151">hello following code snippet shows an example of how toouse hello [Microsoft Azure Batch Client Library for Python][py_batch_package] toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="e10f7-152">Documentação para Olá módulo Python de lote pode ser encontrado em [azure.batch pacote] [ py_batch_docs] em documentos de saudação de leitura.</span><span class="sxs-lookup"><span data-stu-id="e10f7-152">Reference documentation for hello Batch Python module can be found at [azure.batch package][py_batch_docs] on Read hello Docs.</span></span>

<span data-ttu-id="e10f7-153">Esse trecho de código cria uma [ImageReference][py_imagereference] explicitamente e especifica cada uma de suas propriedades (editor, oferta, SKU e versão).</span><span class="sxs-lookup"><span data-stu-id="e10f7-153">This snippet creates an [ImageReference][py_imagereference] explicitly and specifies each of its properties (publisher, offer, SKU, version).</span></span> <span data-ttu-id="e10f7-154">No código de produção, no entanto, recomendamos que você use Olá [list_node_agent_skus] [ py_list_skus] método toodetermine e select de saudação imagem e nó agente SKU combinações disponíveis em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="e10f7-154">In production code, however, we recommend that you use hello [list_node_agent_skus][py_list_skus] method toodetermine and select from hello available image and node agent SKU combinations at runtime.</span></span>

```python
# Import hello required modules from the
# Azure Batch Client Library for Python
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify Batch account credentials
account = "<batch-account-name>"
key = "<batch-account-key>"
batch_url = "<batch-account-url>"

# Pool settings
pool_id = "LinuxNodesSamplePoolPython"
vm_size = "STANDARD_A1"
node_count = 1

# Initialize hello Batch client
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create hello unbound pool
new_pool = batchmodels.PoolAddParameter(id = pool_id, vm_size = vm_size)
new_pool.target_dedicated = node_count

# Configure hello start task for hello pool
start_task = batchmodels.StartTask()
start_task.run_elevated = True
start_task.command_line = "printenv AZ_BATCH_NODE_STARTUP_DIR"
new_pool.start_task = start_task

# Create an ImageReference which specifies hello Marketplace
# virtual machine image tooinstall on hello nodes.
ir = batchmodels.ImageReference(
    publisher = "Canonical",
    offer = "UbuntuServer",
    sku = "14.04.2-LTS",
    version = "latest")

# Create hello VirtualMachineConfiguration, specifying
# hello VM image reference and hello Batch node agent to
# be installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign hello virtual machine configuration toohello pool
new_pool.virtual_machine_configuration = vmc

# Create pool in hello Batch service
client.pool.add(new_pool)
```

<span data-ttu-id="e10f7-155">Conforme mencionado anteriormente, é recomendável que, em vez de criar hello [ImageReference] [ py_imagereference] explicitamente, você pode usar Olá [list_node_agent_skus] [ py_list_skus] método toodynamically selecione Olá atualmente suporte para combinações de imagem de agente/Marketplace do nó.</span><span class="sxs-lookup"><span data-stu-id="e10f7-155">As mentioned previously, we recommend that instead of creating hello [ImageReference][py_imagereference] explicitly, you use hello [list_node_agent_skus][py_list_skus] method toodynamically select from hello currently supported node agent/Marketplace image combinations.</span></span> <span data-ttu-id="e10f7-156">Olá trecho a seguir Python mostra como toouse esse método.</span><span class="sxs-lookup"><span data-stu-id="e10f7-156">hello following Python snippet shows how toouse this method.</span></span>

```python
# Get hello list of node agents from hello Batch service
nodeagents = client.account.list_node_agent_skus()

# Obtain hello desired node agent
ubuntu1404agent = next(agent for agent in nodeagents if "ubuntu 14.04" in agent.id)

# Pick hello first image reference from hello list of verified references
ir = ubuntu1404agent.verified_image_references[0]

# Create hello VirtualMachineConfiguration, specifying hello VM image
# reference and hello Batch node agent toobe installed on hello node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = ubuntu1404agent.id)
```

## <a name="create-a-linux-pool-batch-net"></a><span data-ttu-id="e10f7-157">Criar um pool do Linux: .NET do Lote</span><span class="sxs-lookup"><span data-stu-id="e10f7-157">Create a Linux pool: Batch .NET</span></span>
<span data-ttu-id="e10f7-158">Olá, trecho de código a seguir mostra um exemplo de como Olá toouse [Batch .NET] [ nuget_batch_net] nós de computação da biblioteca de cliente toocreate um pool de servidor do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e10f7-158">hello following code snippet shows an example of how toouse hello [Batch .NET][nuget_batch_net] client library toocreate a pool of Ubuntu Server compute nodes.</span></span> <span data-ttu-id="e10f7-159">Você pode encontrar hello [documentação de referência do .NET em lotes] [ api_net] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="e10f7-159">You can find hello [Batch .NET reference documentation][api_net] on MSDN.</span></span>

<span data-ttu-id="e10f7-160">trecho de código a seguir Hello usa Olá [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] tooselect de método da lista de saudação com suporte no momento Marketplace imagem e nó agente SKU combinações.</span><span class="sxs-lookup"><span data-stu-id="e10f7-160">hello following code snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method tooselect from hello list of currently supported Marketplace image and node agent SKU combinations.</span></span> <span data-ttu-id="e10f7-161">Essa técnica é desejável, porque a lista de saudação de combinações com suporte pode ser alterada de tootime de tempo.</span><span class="sxs-lookup"><span data-stu-id="e10f7-161">This technique is desirable because hello list of supported combinations may change from time tootime.</span></span> <span data-ttu-id="e10f7-162">Os mais comum é que combinações com suporte sejam adicionadas.</span><span class="sxs-lookup"><span data-stu-id="e10f7-162">Most commonly, supported combinations are added.</span></span>

```csharp
// Pool settings
const string poolId = "LinuxNodesSamplePoolDotNet";
const string vmSize = "STANDARD_A1";
const int nodeCount = 1;

// Obtain a collection of all available node agent SKUs.
// This allows us tooselect from a list of supported
// VM image/node agent combinations.
List<NodeAgentSku> nodeAgentSkus =
    batchClient.PoolOperations.ListNodeAgentSkus().ToList();

// Define a delegate specifying properties of hello VM image
// that we wish toouse.
Func<ImageReference, bool> isUbuntu1404 = imageRef =>
    imageRef.Publisher == "Canonical" &&
    imageRef.Offer == "UbuntuServer" &&
    imageRef.Sku.Contains("14.04");

// Obtain hello first node agent SKU in hello collection that matches
// Ubuntu Server 14.04. Note that there are one or more image
// references associated with this node agent SKU.
NodeAgentSku ubuntuAgentSku = nodeAgentSkus.First(sku =>
    sku.VerifiedImageReferences.Any(isUbuntu1404));

// Select an ImageReference from those available for node agent.
ImageReference imageReference =
    ubuntuAgentSku.VerifiedImageReferences.First(isUbuntu1404);

// Create hello VirtualMachineConfiguration for use when actually
// creating hello pool
VirtualMachineConfiguration virtualMachineConfiguration =
    new VirtualMachineConfiguration(imageReference, ubuntuAgentSku.Id);

// Create hello unbound pool object using hello VirtualMachineConfiguration
// created above
CloudPool pool = batchClient.PoolOperations.CreatePool(
    poolId: poolId,
    virtualMachineSize: vmSize,
    virtualMachineConfiguration: virtualMachineConfiguration,
    targetDedicatedComputeNodes: nodeCount);

// Commit hello pool toohello Batch service
await pool.CommitAsync();
```

<span data-ttu-id="e10f7-163">Embora o trecho de código anterior Olá usa Olá [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] lista toodynamically de método e selecionar a partir de imagem e o nó combinações de SKU de agente (recomendadas) com suporte, você também pode configurar um [ImageReference] [ net_imagereference] explicitamente:</span><span class="sxs-lookup"><span data-stu-id="e10f7-163">Although hello previous snippet uses hello [PoolOperations][net_pool_ops].[ListNodeAgentSkus][net_list_skus] method toodynamically list and select from supported image and node agent SKU combinations (recommended), you can also configure an [ImageReference][net_imagereference] explicitly:</span></span>

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a><span data-ttu-id="e10f7-164">imagens da Lista de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="e10f7-164">List of virtual machine images</span></span>
<span data-ttu-id="e10f7-165">Olá tabela a seguir lista imagens de máquinas virtuais do Marketplace Olá são compatíveis com agentes de nó de lote disponíveis Olá este artigo foi atualizada pela última vez.</span><span class="sxs-lookup"><span data-stu-id="e10f7-165">hello following table lists hello Marketplace virtual machine images that are compatible with hello available Batch node agents when this article was last updated.</span></span> <span data-ttu-id="e10f7-166">É importante toonote que esta lista não é definitiva, como imagens e agentes de nó podem ser adicionados ou removidos a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="e10f7-166">It is important toonote that this list is not definitive because images and node agents may be added or removed at any time.</span></span> <span data-ttu-id="e10f7-167">É recomendável que os aplicativos de lote e os serviços sempre usar [list_node_agent_skus] [ py_list_skus] (Python) e [ListNodeAgentSkus] [ net_list_skus] Toodetermine (lote .NET) e selecione uma das Olá SKUs disponíveis no momento.</span><span class="sxs-lookup"><span data-stu-id="e10f7-167">We recommend that your Batch applications and services always use [list_node_agent_skus][py_list_skus] (Python) and [ListNodeAgentSkus][net_list_skus] (Batch .NET) toodetermine and select from hello currently available SKUs.</span></span>

> [!WARNING]
> <span data-ttu-id="e10f7-168">Olá lista a seguir pode alterar a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="e10f7-168">hello following list may change at any time.</span></span> <span data-ttu-id="e10f7-169">Sempre use Olá **agente do nó de lista SKU** métodos disponíveis no toolist de APIs de lote Olá Olá máquina virtual compatíveis e o agente do nó SKUs quando você executar seus trabalhos em lotes.</span><span class="sxs-lookup"><span data-stu-id="e10f7-169">Always use hello **list node agent SKU** methods available in hello Batch APIs toolist hello compatible virtual machine and node agent SKUs when you run your Batch jobs.</span></span>
>
>

| <span data-ttu-id="e10f7-170">**Publicador**</span><span class="sxs-lookup"><span data-stu-id="e10f7-170">**Publisher**</span></span> | <span data-ttu-id="e10f7-171">**Oferta**</span><span class="sxs-lookup"><span data-stu-id="e10f7-171">**Offer**</span></span> | <span data-ttu-id="e10f7-172">**Imagem do SKU**</span><span class="sxs-lookup"><span data-stu-id="e10f7-172">**Image SKU**</span></span> | <span data-ttu-id="e10f7-173">**Versão**</span><span class="sxs-lookup"><span data-stu-id="e10f7-173">**Version**</span></span> | <span data-ttu-id="e10f7-174">**ID do SKU do agente do nó**</span><span class="sxs-lookup"><span data-stu-id="e10f7-174">**Node agent SKU ID**</span></span> |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| <span data-ttu-id="e10f7-175">Canônico</span><span class="sxs-lookup"><span data-stu-id="e10f7-175">Canonical</span></span> | <span data-ttu-id="e10f7-176">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="e10f7-176">UbuntuServer</span></span> | <span data-ttu-id="e10f7-177">14.04.5-LTS</span><span class="sxs-lookup"><span data-stu-id="e10f7-177">14.04.5-LTS</span></span> | <span data-ttu-id="e10f7-178">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-178">latest</span></span> | <span data-ttu-id="e10f7-179">batch.node.ubuntu 14.04</span><span class="sxs-lookup"><span data-stu-id="e10f7-179">batch.node.ubuntu 14.04</span></span> |
| <span data-ttu-id="e10f7-180">Canônico</span><span class="sxs-lookup"><span data-stu-id="e10f7-180">Canonical</span></span> | <span data-ttu-id="e10f7-181">UbuntuServer</span><span class="sxs-lookup"><span data-stu-id="e10f7-181">UbuntuServer</span></span> | <span data-ttu-id="e10f7-182">16.04.0-LTS</span><span class="sxs-lookup"><span data-stu-id="e10f7-182">16.04.0-LTS</span></span> | <span data-ttu-id="e10f7-183">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-183">latest</span></span> | <span data-ttu-id="e10f7-184">batch.node.ubuntu 16.04</span><span class="sxs-lookup"><span data-stu-id="e10f7-184">batch.node.ubuntu 16.04</span></span> |
| <span data-ttu-id="e10f7-185">Credativ</span><span class="sxs-lookup"><span data-stu-id="e10f7-185">Credativ</span></span> | <span data-ttu-id="e10f7-186">Debian</span><span class="sxs-lookup"><span data-stu-id="e10f7-186">Debian</span></span> | <span data-ttu-id="e10f7-187">8</span><span class="sxs-lookup"><span data-stu-id="e10f7-187">8</span></span> | <span data-ttu-id="e10f7-188">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-188">latest</span></span> | <span data-ttu-id="e10f7-189">batch.node.debian 8</span><span class="sxs-lookup"><span data-stu-id="e10f7-189">batch.node.debian 8</span></span> |
| <span data-ttu-id="e10f7-190">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="e10f7-190">OpenLogic</span></span> | <span data-ttu-id="e10f7-191">CentOS</span><span class="sxs-lookup"><span data-stu-id="e10f7-191">CentOS</span></span> | <span data-ttu-id="e10f7-192">7.0</span><span class="sxs-lookup"><span data-stu-id="e10f7-192">7.0</span></span> | <span data-ttu-id="e10f7-193">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-193">latest</span></span> | <span data-ttu-id="e10f7-194">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="e10f7-194">batch.node.centos 7</span></span> |
| <span data-ttu-id="e10f7-195">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="e10f7-195">OpenLogic</span></span> | <span data-ttu-id="e10f7-196">CentOS</span><span class="sxs-lookup"><span data-stu-id="e10f7-196">CentOS</span></span> | <span data-ttu-id="e10f7-197">7.1</span><span class="sxs-lookup"><span data-stu-id="e10f7-197">7.1</span></span> | <span data-ttu-id="e10f7-198">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-198">latest</span></span> | <span data-ttu-id="e10f7-199">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="e10f7-199">batch.node.centos 7</span></span> |
| <span data-ttu-id="e10f7-200">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="e10f7-200">OpenLogic</span></span> | <span data-ttu-id="e10f7-201">CentOS-HPC</span><span class="sxs-lookup"><span data-stu-id="e10f7-201">CentOS-HPC</span></span> | <span data-ttu-id="e10f7-202">7.1</span><span class="sxs-lookup"><span data-stu-id="e10f7-202">7.1</span></span> | <span data-ttu-id="e10f7-203">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-203">latest</span></span> | <span data-ttu-id="e10f7-204">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="e10f7-204">batch.node.centos 7</span></span> |
| <span data-ttu-id="e10f7-205">OpenLogic</span><span class="sxs-lookup"><span data-stu-id="e10f7-205">OpenLogic</span></span> | <span data-ttu-id="e10f7-206">CentOS</span><span class="sxs-lookup"><span data-stu-id="e10f7-206">CentOS</span></span> | <span data-ttu-id="e10f7-207">7,2</span><span class="sxs-lookup"><span data-stu-id="e10f7-207">7.2</span></span> | <span data-ttu-id="e10f7-208">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-208">latest</span></span> | <span data-ttu-id="e10f7-209">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="e10f7-209">batch.node.centos 7</span></span> |
| <span data-ttu-id="e10f7-210">Oracle</span><span class="sxs-lookup"><span data-stu-id="e10f7-210">Oracle</span></span> | <span data-ttu-id="e10f7-211">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="e10f7-211">Oracle-Linux</span></span> | <span data-ttu-id="e10f7-212">7.0</span><span class="sxs-lookup"><span data-stu-id="e10f7-212">7.0</span></span> | <span data-ttu-id="e10f7-213">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-213">latest</span></span> | <span data-ttu-id="e10f7-214">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="e10f7-214">batch.node.centos 7</span></span> |
| <span data-ttu-id="e10f7-215">Oracle</span><span class="sxs-lookup"><span data-stu-id="e10f7-215">Oracle</span></span> | <span data-ttu-id="e10f7-216">Oracle-Linux</span><span class="sxs-lookup"><span data-stu-id="e10f7-216">Oracle-Linux</span></span> | <span data-ttu-id="e10f7-217">7,2</span><span class="sxs-lookup"><span data-stu-id="e10f7-217">7.2</span></span> | <span data-ttu-id="e10f7-218">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-218">latest</span></span> | <span data-ttu-id="e10f7-219">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="e10f7-219">batch.node.centos 7</span></span> |
| <span data-ttu-id="e10f7-220">SUSE</span><span class="sxs-lookup"><span data-stu-id="e10f7-220">SUSE</span></span> | <span data-ttu-id="e10f7-221">openSUSE</span><span class="sxs-lookup"><span data-stu-id="e10f7-221">openSUSE</span></span> | <span data-ttu-id="e10f7-222">13.2</span><span class="sxs-lookup"><span data-stu-id="e10f7-222">13.2</span></span> | <span data-ttu-id="e10f7-223">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-223">latest</span></span> | <span data-ttu-id="e10f7-224">batch.node.opensuse 13.2</span><span class="sxs-lookup"><span data-stu-id="e10f7-224">batch.node.opensuse 13.2</span></span> |
| <span data-ttu-id="e10f7-225">SUSE</span><span class="sxs-lookup"><span data-stu-id="e10f7-225">SUSE</span></span> | <span data-ttu-id="e10f7-226">openSUSE-Leap</span><span class="sxs-lookup"><span data-stu-id="e10f7-226">openSUSE-Leap</span></span> | <span data-ttu-id="e10f7-227">42.1</span><span class="sxs-lookup"><span data-stu-id="e10f7-227">42.1</span></span> | <span data-ttu-id="e10f7-228">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-228">latest</span></span> | <span data-ttu-id="e10f7-229">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="e10f7-229">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="e10f7-230">SUSE</span><span class="sxs-lookup"><span data-stu-id="e10f7-230">SUSE</span></span> | <span data-ttu-id="e10f7-231">SLES</span><span class="sxs-lookup"><span data-stu-id="e10f7-231">SLES</span></span> | <span data-ttu-id="e10f7-232">12-SP1</span><span class="sxs-lookup"><span data-stu-id="e10f7-232">12-SP1</span></span> | <span data-ttu-id="e10f7-233">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-233">latest</span></span> | <span data-ttu-id="e10f7-234">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="e10f7-234">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="e10f7-235">SUSE</span><span class="sxs-lookup"><span data-stu-id="e10f7-235">SUSE</span></span> | <span data-ttu-id="e10f7-236">SLES-HPC</span><span class="sxs-lookup"><span data-stu-id="e10f7-236">SLES-HPC</span></span> | <span data-ttu-id="e10f7-237">12-SP1</span><span class="sxs-lookup"><span data-stu-id="e10f7-237">12-SP1</span></span> | <span data-ttu-id="e10f7-238">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-238">latest</span></span> | <span data-ttu-id="e10f7-239">batch.node.opensuse 42.1</span><span class="sxs-lookup"><span data-stu-id="e10f7-239">batch.node.opensuse 42.1</span></span> |
| <span data-ttu-id="e10f7-240">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="e10f7-240">microsoft-ads</span></span> | <span data-ttu-id="e10f7-241">linux-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="e10f7-241">linux-data-science-vm</span></span> | <span data-ttu-id="e10f7-242">linuxdsvm</span><span class="sxs-lookup"><span data-stu-id="e10f7-242">linuxdsvm</span></span> | <span data-ttu-id="e10f7-243">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-243">latest</span></span> | <span data-ttu-id="e10f7-244">batch.node.centos 7</span><span class="sxs-lookup"><span data-stu-id="e10f7-244">batch.node.centos 7</span></span> |
| <span data-ttu-id="e10f7-245">microsoft-ads</span><span class="sxs-lookup"><span data-stu-id="e10f7-245">microsoft-ads</span></span> | <span data-ttu-id="e10f7-246">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="e10f7-246">standard-data-science-vm</span></span> | <span data-ttu-id="e10f7-247">standard-data-science-vm</span><span class="sxs-lookup"><span data-stu-id="e10f7-247">standard-data-science-vm</span></span> | <span data-ttu-id="e10f7-248">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-248">latest</span></span> | <span data-ttu-id="e10f7-249">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="e10f7-249">batch.node.windows amd64</span></span> |
| <span data-ttu-id="e10f7-250">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e10f7-250">MicrosoftWindowsServer</span></span> | <span data-ttu-id="e10f7-251">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e10f7-251">WindowsServer</span></span> | <span data-ttu-id="e10f7-252">2008-R2-SP1</span><span class="sxs-lookup"><span data-stu-id="e10f7-252">2008-R2-SP1</span></span> | <span data-ttu-id="e10f7-253">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-253">latest</span></span> | <span data-ttu-id="e10f7-254">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="e10f7-254">batch.node.windows amd64</span></span> |
| <span data-ttu-id="e10f7-255">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e10f7-255">MicrosoftWindowsServer</span></span> | <span data-ttu-id="e10f7-256">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e10f7-256">WindowsServer</span></span> | <span data-ttu-id="e10f7-257">2012-Datacenter</span><span class="sxs-lookup"><span data-stu-id="e10f7-257">2012-Datacenter</span></span> | <span data-ttu-id="e10f7-258">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-258">latest</span></span> | <span data-ttu-id="e10f7-259">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="e10f7-259">batch.node.windows amd64</span></span> |
| <span data-ttu-id="e10f7-260">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e10f7-260">MicrosoftWindowsServer</span></span> | <span data-ttu-id="e10f7-261">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e10f7-261">WindowsServer</span></span> | <span data-ttu-id="e10f7-262">2012-R2-Datacenter</span><span class="sxs-lookup"><span data-stu-id="e10f7-262">2012-R2-Datacenter</span></span> | <span data-ttu-id="e10f7-263">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-263">latest</span></span> | <span data-ttu-id="e10f7-264">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="e10f7-264">batch.node.windows amd64</span></span> |
| <span data-ttu-id="e10f7-265">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e10f7-265">MicrosoftWindowsServer</span></span> | <span data-ttu-id="e10f7-266">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e10f7-266">WindowsServer</span></span> | <span data-ttu-id="e10f7-267">2016-Datacenter</span><span class="sxs-lookup"><span data-stu-id="e10f7-267">2016-Datacenter</span></span> | <span data-ttu-id="e10f7-268">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-268">latest</span></span> | <span data-ttu-id="e10f7-269">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="e10f7-269">batch.node.windows amd64</span></span> |
| <span data-ttu-id="e10f7-270">MicrosoftWindowsServer</span><span class="sxs-lookup"><span data-stu-id="e10f7-270">MicrosoftWindowsServer</span></span> | <span data-ttu-id="e10f7-271">WindowsServer</span><span class="sxs-lookup"><span data-stu-id="e10f7-271">WindowsServer</span></span> | <span data-ttu-id="e10f7-272">2016-Datacenter-with-Containers</span><span class="sxs-lookup"><span data-stu-id="e10f7-272">2016-Datacenter-with-Containers</span></span> | <span data-ttu-id="e10f7-273">mais recente</span><span class="sxs-lookup"><span data-stu-id="e10f7-273">latest</span></span> | <span data-ttu-id="e10f7-274">batch.node.windows amd64</span><span class="sxs-lookup"><span data-stu-id="e10f7-274">batch.node.windows amd64</span></span> |

## <a name="connect-toolinux-nodes-using-ssh"></a><span data-ttu-id="e10f7-275">Conectar nós tooLinux usando SSH</span><span class="sxs-lookup"><span data-stu-id="e10f7-275">Connect tooLinux nodes using SSH</span></span>
<span data-ttu-id="e10f7-276">Durante o desenvolvimento ou durante a solução de problemas, talvez seja necessário toosign toohello nós em seu pool.</span><span class="sxs-lookup"><span data-stu-id="e10f7-276">During development or while troubleshooting, you may find it necessary toosign in toohello nodes in your pool.</span></span> <span data-ttu-id="e10f7-277">Ao contrário de nós de computação do Windows, você não pode usar nós do protocolo de área de trabalho remota (RDP) tooconnect tooLinux.</span><span class="sxs-lookup"><span data-stu-id="e10f7-277">Unlike Windows compute nodes, you cannot use Remote Desktop Protocol (RDP) tooconnect tooLinux nodes.</span></span> <span data-ttu-id="e10f7-278">Em vez disso, Olá serviço de lote permite o acesso SSH em cada nó de conexão remota.</span><span class="sxs-lookup"><span data-stu-id="e10f7-278">Instead, hello Batch service enables SSH access on each node for remote connection.</span></span>

<span data-ttu-id="e10f7-279">Olá trecho de código Python a seguir cria um usuário em cada nó em um pool, que é necessário para a conexão remota.</span><span class="sxs-lookup"><span data-stu-id="e10f7-279">hello following Python code snippet creates a user on each node in a pool, which is required for remote connection.</span></span> <span data-ttu-id="e10f7-280">Em seguida, imprime informações de conexão saudação do secure shell (SSH) para cada nó.</span><span class="sxs-lookup"><span data-stu-id="e10f7-280">It then prints hello secure shell (SSH) connection information for each node.</span></span>

```python
import datetime
import getpass
import azure.batch.batch_service_client as batch
import azure.batch.batch_auth as batchauth
import azure.batch.models as batchmodels

# Specify your own account credentials
batch_account_name = ''
batch_account_key = ''
batch_account_url = ''

# Specify hello ID of an existing pool containing Linux nodes
# currently in hello 'idle' state
pool_id = ''

# Specify hello username and prompt for a password
username = 'linuxuser'
password = getpass.getpass()

# Create a BatchClient
credentials = batchauth.SharedKeyCredentials(
    batch_account_name,
    batch_account_key
)
batch_client = batch.BatchServiceClient(
        credentials,
        base_url=batch_account_url
)

# Create hello user that will be added tooeach node in hello pool
user = batchmodels.ComputeNodeUser(username)
user.password = password
user.is_admin = True
user.expiry_time = \
    (datetime.datetime.today() + datetime.timedelta(days=30)).isoformat()

# Get hello list of nodes in hello pool
nodes = batch_client.compute_node.list(pool_id)

# Add hello user tooeach node in hello pool and print
# hello connection information for hello node
for node in nodes:
    # Add hello user toohello node
    batch_client.compute_node.add_user(pool_id, node.id, user)

    # Obtain SSH login information for hello node
    login = batch_client.compute_node.get_remote_login_settings(pool_id,
                                                                node.id)

    # Print hello connection info for hello node
    print("{0} | {1} | {2} | {3}".format(node.id,
                                         node.state,
                                         login.remote_login_ip_address,
                                         login.remote_login_port))
```

<span data-ttu-id="e10f7-281">Aqui está o exemplo de saída de código anterior de saudação para um pool que contém quatro nós do Linux:</span><span class="sxs-lookup"><span data-stu-id="e10f7-281">Here is sample output for hello previous code for a pool that contains four Linux nodes:</span></span>

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

<span data-ttu-id="e10f7-282">Em vez de uma senha, você pode especificar uma chave pública SSH ao criar um usuário em um nó.</span><span class="sxs-lookup"><span data-stu-id="e10f7-282">Instead of a password, you can specify an SSH public key when you create a user on a node.</span></span> <span data-ttu-id="e10f7-283">Olá SDK de Python, usar Olá **ssh_public_key** parâmetro em [ComputeNodeUser][py_computenodeuser].</span><span class="sxs-lookup"><span data-stu-id="e10f7-283">In hello Python SDK, use hello **ssh_public_key** parameter on [ComputeNodeUser][py_computenodeuser].</span></span> <span data-ttu-id="e10f7-284">No .NET, use Olá [ComputeNodeUser][net_computenodeuser].[ Parâmetros SshPublicKey] [ net_ssh_key] propriedade.</span><span class="sxs-lookup"><span data-stu-id="e10f7-284">In .NET, use hello [ComputeNodeUser][net_computenodeuser].[SshPublicKey][net_ssh_key] property.</span></span>

## <a name="pricing"></a><span data-ttu-id="e10f7-285">Preços</span><span class="sxs-lookup"><span data-stu-id="e10f7-285">Pricing</span></span>
<span data-ttu-id="e10f7-286">O Lote do Azure baseia-se na tecnologia de Serviços de Nuvem do Azure e Máquinas Virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="e10f7-286">Azure Batch is built on Azure Cloud Services and Azure Virtual Machines technology.</span></span> <span data-ttu-id="e10f7-287">Olá próprio serviço de lote é oferecido sem custo, o que significa que você é cobrado somente pela Olá os recursos que consomem suas soluções de lote de computação.</span><span class="sxs-lookup"><span data-stu-id="e10f7-287">hello Batch service itself is offered at no cost, which means you are charged only for hello compute resources that your Batch solutions consume.</span></span> <span data-ttu-id="e10f7-288">Quando você escolhe **configuração de serviços de nuvem**, você é cobrado com base em Olá [preços de serviços de nuvem] [ cloud_services_pricing] estrutura.</span><span class="sxs-lookup"><span data-stu-id="e10f7-288">When you choose **Cloud Services Configuration**, you are charged based on hello [Cloud Services pricing][cloud_services_pricing] structure.</span></span> <span data-ttu-id="e10f7-289">Quando você escolhe **configuração de máquina Virtual**, você é cobrado com base em Olá [preços das máquinas virtuais] [ vm_pricing] estrutura.</span><span class="sxs-lookup"><span data-stu-id="e10f7-289">When you choose **Virtual Machine Configuration**, you are charged based on hello [Virtual Machines pricing][vm_pricing] structure.</span></span> 

<span data-ttu-id="e10f7-290">Se você implanta aplicativos tooyour lote nós usando [pacotes de aplicativos](batch-application-packages.md), você também cobrados para recursos de armazenamento do Azure Olá que consumam seus pacotes de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="e10f7-290">If you deploy applications tooyour Batch nodes using [application packages](batch-application-packages.md), you are also charged for hello Azure Storage resources that your application packages consume.</span></span> <span data-ttu-id="e10f7-291">Em geral, os custos de armazenamento do Azure Olá são mínimos.</span><span class="sxs-lookup"><span data-stu-id="e10f7-291">In general, hello Azure Storage costs are minimal.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e10f7-292">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e10f7-292">Next steps</span></span>
### <a name="batch-python-tutorial"></a><span data-ttu-id="e10f7-293">Tutorial do Python do Lote</span><span class="sxs-lookup"><span data-stu-id="e10f7-293">Batch Python tutorial</span></span>
<span data-ttu-id="e10f7-294">Para obter um tutorial mais detalhado sobre como toowork com lotes usando Python, check-out [Introdução ao cliente do Python de lote do Azure Olá](batch-python-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="e10f7-294">For a more in-depth tutorial about how toowork with Batch by using Python, check out [Get started with hello Azure Batch Python client](batch-python-tutorial.md).</span></span> <span data-ttu-id="e10f7-295">Seu complementar [exemplo de código] [ github_samples_pyclient] inclui uma função auxiliar, `get_vm_config_for_distro`, que mostra outro tooobtain de técnica uma configuração de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="e10f7-295">Its companion [code sample][github_samples_pyclient] includes a helper function, `get_vm_config_for_distro`, that shows another technique tooobtain a virtual machine configuration.</span></span>

### <a name="batch-python-code-samples"></a><span data-ttu-id="e10f7-296">Exemplos de código do Python do Lote</span><span class="sxs-lookup"><span data-stu-id="e10f7-296">Batch Python code samples</span></span>
<span data-ttu-id="e10f7-297">Olá [exemplos de código Python] [ github_samples_py] em Olá [exemplos de lote do azure] [ github_samples] repositório no GitHub contém scripts que mostram como tooperform operações comuns de lote, como criação de tarefa, trabalho e pool.</span><span class="sxs-lookup"><span data-stu-id="e10f7-297">hello [Python code samples][github_samples_py] in hello [azure-batch-samples][github_samples] repository on GitHub contain scripts that show you how tooperform common Batch operations, such as pool, job, and task creation.</span></span> <span data-ttu-id="e10f7-298">Olá [Leiame] [ github_py_readme] que acompanha as amostras de Python Olá apresenta detalhes sobre como Olá tooinstall necessário pacotes.</span><span class="sxs-lookup"><span data-stu-id="e10f7-298">hello [README][github_py_readme] that accompanies hello Python samples has details about how tooinstall hello required packages.</span></span>

### <a name="batch-forum"></a><span data-ttu-id="e10f7-299">Fórum do lote</span><span class="sxs-lookup"><span data-stu-id="e10f7-299">Batch forum</span></span>
<span data-ttu-id="e10f7-300">Olá [Fórum do lote do Azure] [ forum] no MSDN é um ótimo colocar toodiscuss em lotes e fazer perguntas sobre o serviço de saudação.</span><span class="sxs-lookup"><span data-stu-id="e10f7-300">hello [Azure Batch Forum][forum] on MSDN is a great place toodiscuss Batch and ask questions about hello service.</span></span> <span data-ttu-id="e10f7-301">Leia publicações úteis “fixas” e poste suas dúvidas conforme elas surgirem enquanto você cria suas soluções do Lote.</span><span class="sxs-lookup"><span data-stu-id="e10f7-301">Read helpful "pinned" posts, and post your questions as they arise while you build your Batch solutions.</span></span>

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_mgmt]: https://msdn.microsoft.com/library/azure/mt463120.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[cloud_services_pricing]: https://azure.microsoft.com/pricing/details/cloud-services/
[forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_py_readme]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/README.md
[github_samples]: https://github.com/Azure/azure-batch-samples
[github_samples_py]: https://github.com/Azure/azure-batch-samples/tree/master/Python/Batch
[github_samples_pyclient]: https://github.com/Azure/azure-batch-samples/blob/master/Python/Batch/article_samples/python_tutorial_client.py
[portal]: https://portal.azure.com
[net_cloudpool]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.aspx
[net_computenodeuser]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.aspx
[net_imagereference]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.imagereference.aspx
[net_list_skus]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listnodeagentskus.aspx
[net_pool_ops]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.aspx
[net_ssh_key]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.computenodeuser.sshpublickey.aspx
[nuget_batch_net]: https://www.nuget.org/packages/Azure.Batch/
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
[py_account_ops]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations
[py_azure_sdk]: https://pypi.python.org/pypi/azure
[py_batch_docs]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.html
[py_batch_package]: https://pypi.python.org/pypi/azure-batch
[py_computenodeuser]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ComputeNodeUser
[py_imagereference]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.models.html#azure.batch.models.ImageReference
[py_list_skus]: http://azure-sdk-for-python.readthedocs.org/en/dev/ref/azure.batch.operations.html#azure.batch.operations.AccountOperations.list_node_agent_skus
[vm_marketplace]: https://azure.microsoft.com/marketplace/virtual-machines/
[vm_pricing]: https://azure.microsoft.com/pricing/details/virtual-machines/
