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
# <a name="provision-linux-compute-nodes-in-batch-pools"></a>Provisionar os nós de computação do Linux em pools do Lote

Você pode usar cargas de trabalho do Azure Batch toorun computação paralela em máquinas virtuais Linux e Windows. Este artigo detalha como pools de toocreate do Linux nós de computação no serviço de lote hello usando ambos os Olá [lote Python] [ py_batch_package] e [Batch .NET] [ api_net] bibliotecas de cliente.

> [!NOTE]
> Os pacotes de aplicativos têm suporte em todos os pools do Lote criados após 5 de julho de 2017. Eles têm suporte em pools de lote criados entre 10 de março de 2016 e 5 de julho de 2017 somente se o pool de saudação foi criado usando uma configuração de serviço de nuvem. Pools de lote criados too10 anterior de março de 2016 não dão suporte a pacotes de aplicativos. Para obter mais informações sobre como usar o aplicativo pacotes toodeploy seus nós de lote de tooyour de aplicativos, consulte [implantar aplicativos toocompute nós com pacotes de aplicativos de lote](batch-application-packages.md).
>
>

## <a name="virtual-machine-configuration"></a>Configuração de máquina virtual
Quando você cria um conjunto de nós de computação em lote, você tem duas opções de tamanho de nó tooselect hello e do sistema operacional: configuração de máquina Virtual e a configuração de serviços de nuvem.

**Configuração dos Serviços de Nuvem** fornece *apenas*. Tamanhos de nós de computação disponíveis são listados na [tamanhos para serviços de nuvem](../cloud-services/cloud-services-sizes-specs.md), e sistemas operacionais disponíveis são listados na Olá [versões do sistema operacional de convidado do Azure e matriz de compatibilidade do SDK](../cloud-services/cloud-services-guestos-update-matrix.md). Quando você cria um pool que contém nós de serviços de nuvem do Azure, especifique o tamanho do nó de saudação e hello família de sistemas operacionais, que são descritos em Olá mencionado anteriormente artigos. No caso de pools de nós de computação do Windows, os Serviços de Nuvem são usados com mais frequência.

**Virtual Machine Configuration** fornece imagens do Linux e do Windows para os nós de computação. Os tamanhos de nó de computação disponíveis estão relacionados em [Tamanhos das máquinas virtuais no Azure](../virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) (Linux) e em [Tamanhos das máquinas virtuais no Azure](../virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (Windows). Quando você cria um pool que contém nós de configuração de máquina Virtual, você deve especificar o tamanho de saudação de nós hello, referência de imagem de máquina virtual hello e Olá lote nó agente SKU toobe instalada em nós de saudação.

### <a name="virtual-machine-image-reference"></a>Referência da imagem da máquina virtual
Olá serviço de lote usa [conjuntos de escala de máquina virtual](../virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) tooprovide Linux nós de computação. Você pode especificar uma imagem de saudação [Azure Marketplace][vm_marketplace], ou forneça uma imagem personalizada que você preparou. Para obter mais detalhes sobre imagens personalizadas, confira [Desenvolver soluções de computação paralela em grande escala com o Lote](batch-api-basics.md#pool).

Quando você configura uma referência de imagem de máquina virtual, você especificar propriedades de saudação da imagem de máquina virtual de saudação. Olá propriedades a seguir é necessária quando você cria uma referência de imagem de máquina virtual:

| **Propriedades de referência de imagem** | **Exemplo** |
| --- | --- |
| Publicador |Canônico |
| Oferta |UbuntuServer |
| SKU |14.04.4-LTS |
| Versão |mais recente |

> [!TIP]
> Você pode aprender mais sobre essas propriedades e como toolist Marketplace imagens no [navegue e selecionadas imagens de máquinas virtuais Linux no Azure com CLI ou o PowerShell](../virtual-machines/linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Observe que nem todas as imagens do Marketplace são compatíveis com o Lote no momento. Para saber mais, confira [SKU do agente do nó](#node-agent-sku).
>
>

### <a name="node-agent-sku"></a>SKU do agente do nó
Agente de nó de lote de saudação é um programa que é executado em cada nó no pool de saudação e fornece a interface de comando e controle de saudação entre nó hello e serviço de lote de saudação. Há várias implementações de agente do nó hello, conhecido como SKUs para diferentes sistemas operacionais. Essencialmente, quando você cria uma configuração de máquina Virtual, você primeiro especificar a referência de imagem de máquina virtual hello e especifique Olá nó agente tooinstall na imagem de saudação. Normalmente, cada SKU do agente do nó é compatível com várias imagens de máquina virtual. Aqui estão alguns exemplos de SKUs do agente do nó:

* batch.node.ubuntu 14.04
* batch.node.centos 7
* batch.node.windows amd64

> [!IMPORTANT]
> Nem todas as imagens de máquinas virtuais que estão disponíveis no mercado de saudação são compatíveis com os agentes de nó em lotes atualmente disponíveis hello. Use o agente Olá SDKs de lote toolist Olá nó disponível SKUs e Olá imagens da máquina virtual com a qual eles são compatíveis. Consulte Olá [imagens da lista de máquina Virtual](#list-of-virtual-machine-images) posteriormente neste artigo para obter mais informações e exemplos de como tooretrieve uma lista de imagens válidas no tempo de execução.
>
>

## <a name="create-a-linux-pool-batch-python"></a>Criar um pool do Linux: Python do Lote
Olá, trecho de código a seguir mostra um exemplo de como Olá toouse [biblioteca de cliente de lote do Microsoft Azure para Python] [ py_batch_package] toocreate um pool de servidor do Ubuntu nós de computação. Documentação para Olá módulo Python de lote pode ser encontrado em [azure.batch pacote] [ py_batch_docs] em documentos de saudação de leitura.

Esse trecho de código cria uma [ImageReference][py_imagereference] explicitamente e especifica cada uma de suas propriedades (editor, oferta, SKU e versão). No código de produção, no entanto, recomendamos que você use Olá [list_node_agent_skus] [ py_list_skus] método toodetermine e select de saudação imagem e nó agente SKU combinações disponíveis em tempo de execução.

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

Conforme mencionado anteriormente, é recomendável que, em vez de criar hello [ImageReference] [ py_imagereference] explicitamente, você pode usar Olá [list_node_agent_skus] [ py_list_skus] método toodynamically selecione Olá atualmente suporte para combinações de imagem de agente/Marketplace do nó. Olá trecho a seguir Python mostra como toouse esse método.

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

## <a name="create-a-linux-pool-batch-net"></a>Criar um pool do Linux: .NET do Lote
Olá, trecho de código a seguir mostra um exemplo de como Olá toouse [Batch .NET] [ nuget_batch_net] nós de computação da biblioteca de cliente toocreate um pool de servidor do Ubuntu. Você pode encontrar hello [documentação de referência do .NET em lotes] [ api_net] no MSDN.

trecho de código a seguir Hello usa Olá [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] tooselect de método da lista de saudação com suporte no momento Marketplace imagem e nó agente SKU combinações. Essa técnica é desejável, porque a lista de saudação de combinações com suporte pode ser alterada de tootime de tempo. Os mais comum é que combinações com suporte sejam adicionadas.

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

Embora o trecho de código anterior Olá usa Olá [PoolOperations][net_pool_ops].[ ListNodeAgentSkus] [ net_list_skus] lista toodynamically de método e selecionar a partir de imagem e o nó combinações de SKU de agente (recomendadas) com suporte, você também pode configurar um [ImageReference] [ net_imagereference] explicitamente:

```csharp
ImageReference imageReference = new ImageReference(
    publisher: "Canonical",
    offer: "UbuntuServer",
    sku: "14.04.2-LTS",
    version: "latest");
```

## <a name="list-of-virtual-machine-images"></a>imagens da Lista de máquinas virtuais
Olá tabela a seguir lista imagens de máquinas virtuais do Marketplace Olá são compatíveis com agentes de nó de lote disponíveis Olá este artigo foi atualizada pela última vez. É importante toonote que esta lista não é definitiva, como imagens e agentes de nó podem ser adicionados ou removidos a qualquer momento. É recomendável que os aplicativos de lote e os serviços sempre usar [list_node_agent_skus] [ py_list_skus] (Python) e [ListNodeAgentSkus] [ net_list_skus] Toodetermine (lote .NET) e selecione uma das Olá SKUs disponíveis no momento.

> [!WARNING]
> Olá lista a seguir pode alterar a qualquer momento. Sempre use Olá **agente do nó de lista SKU** métodos disponíveis no toolist de APIs de lote Olá Olá máquina virtual compatíveis e o agente do nó SKUs quando você executar seus trabalhos em lotes.
>
>

| **Publicador** | **Oferta** | **Imagem do SKU** | **Versão** | **ID do SKU do agente do nó** |
| ------------- | --------- | ------------- | ----------- | --------------------- |
| Canônico | UbuntuServer | 14.04.5-LTS | mais recente | batch.node.ubuntu 14.04 |
| Canônico | UbuntuServer | 16.04.0-LTS | mais recente | batch.node.ubuntu 16.04 |
| Credativ | Debian | 8 | mais recente | batch.node.debian 8 |
| OpenLogic | CentOS | 7.0 | mais recente | batch.node.centos 7 |
| OpenLogic | CentOS | 7.1 | mais recente | batch.node.centos 7 |
| OpenLogic | CentOS-HPC | 7.1 | mais recente | batch.node.centos 7 |
| OpenLogic | CentOS | 7,2 | mais recente | batch.node.centos 7 |
| Oracle | Oracle-Linux | 7.0 | mais recente | batch.node.centos 7 |
| Oracle | Oracle-Linux | 7,2 | mais recente | batch.node.centos 7 |
| SUSE | openSUSE | 13.2 | mais recente | batch.node.opensuse 13.2 |
| SUSE | openSUSE-Leap | 42.1 | mais recente | batch.node.opensuse 42.1 |
| SUSE | SLES | 12-SP1 | mais recente | batch.node.opensuse 42.1 |
| SUSE | SLES-HPC | 12-SP1 | mais recente | batch.node.opensuse 42.1 |
| microsoft-ads | linux-data-science-vm | linuxdsvm | mais recente | batch.node.centos 7 |
| microsoft-ads | standard-data-science-vm | standard-data-science-vm | mais recente | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2008-R2-SP1 | mais recente | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-Datacenter | mais recente | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2012-R2-Datacenter | mais recente | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016-Datacenter | mais recente | batch.node.windows amd64 |
| MicrosoftWindowsServer | WindowsServer | 2016-Datacenter-with-Containers | mais recente | batch.node.windows amd64 |

## <a name="connect-toolinux-nodes-using-ssh"></a>Conectar nós tooLinux usando SSH
Durante o desenvolvimento ou durante a solução de problemas, talvez seja necessário toosign toohello nós em seu pool. Ao contrário de nós de computação do Windows, você não pode usar nós do protocolo de área de trabalho remota (RDP) tooconnect tooLinux. Em vez disso, Olá serviço de lote permite o acesso SSH em cada nó de conexão remota.

Olá trecho de código Python a seguir cria um usuário em cada nó em um pool, que é necessário para a conexão remota. Em seguida, imprime informações de conexão saudação do secure shell (SSH) para cada nó.

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

Aqui está o exemplo de saída de código anterior de saudação para um pool que contém quatro nós do Linux:

```
Password:
tvm-1219235766_1-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50000
tvm-1219235766_2-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50003
tvm-1219235766_3-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50002
tvm-1219235766_4-20160414t192511z | ComputeNodeState.idle | 13.91.7.57 | 50001
```

Em vez de uma senha, você pode especificar uma chave pública SSH ao criar um usuário em um nó. Olá SDK de Python, usar Olá **ssh_public_key** parâmetro em [ComputeNodeUser][py_computenodeuser]. No .NET, use Olá [ComputeNodeUser][net_computenodeuser].[ Parâmetros SshPublicKey] [ net_ssh_key] propriedade.

## <a name="pricing"></a>Preços
O Lote do Azure baseia-se na tecnologia de Serviços de Nuvem do Azure e Máquinas Virtuais do Azure. Olá próprio serviço de lote é oferecido sem custo, o que significa que você é cobrado somente pela Olá os recursos que consomem suas soluções de lote de computação. Quando você escolhe **configuração de serviços de nuvem**, você é cobrado com base em Olá [preços de serviços de nuvem] [ cloud_services_pricing] estrutura. Quando você escolhe **configuração de máquina Virtual**, você é cobrado com base em Olá [preços das máquinas virtuais] [ vm_pricing] estrutura. 

Se você implanta aplicativos tooyour lote nós usando [pacotes de aplicativos](batch-application-packages.md), você também cobrados para recursos de armazenamento do Azure Olá que consumam seus pacotes de aplicativos. Em geral, os custos de armazenamento do Azure Olá são mínimos. 

## <a name="next-steps"></a>Próximas etapas
### <a name="batch-python-tutorial"></a>Tutorial do Python do Lote
Para obter um tutorial mais detalhado sobre como toowork com lotes usando Python, check-out [Introdução ao cliente do Python de lote do Azure Olá](batch-python-tutorial.md). Seu complementar [exemplo de código] [ github_samples_pyclient] inclui uma função auxiliar, `get_vm_config_for_distro`, que mostra outro tooobtain de técnica uma configuração de máquina virtual.

### <a name="batch-python-code-samples"></a>Exemplos de código do Python do Lote
Olá [exemplos de código Python] [ github_samples_py] em Olá [exemplos de lote do azure] [ github_samples] repositório no GitHub contém scripts que mostram como tooperform operações comuns de lote, como criação de tarefa, trabalho e pool. Olá [Leiame] [ github_py_readme] que acompanha as amostras de Python Olá apresenta detalhes sobre como Olá tooinstall necessário pacotes.

### <a name="batch-forum"></a>Fórum do lote
Olá [Fórum do lote do Azure] [ forum] no MSDN é um ótimo colocar toodiscuss em lotes e fazer perguntas sobre o serviço de saudação. Leia publicações úteis “fixas” e poste suas dúvidas conforme elas surgirem enquanto você cria suas soluções do Lote.

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
