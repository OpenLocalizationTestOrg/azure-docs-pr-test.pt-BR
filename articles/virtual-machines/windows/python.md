---
title: aaaCreate e gerenciar uma VM do Windows Azure usando Python | Microsoft Docs
description: Saiba toouse Python toocreate e gerenciar uma VM do Windows Azure.
services: virtual-machines-windows
documentationcenter: 
author: davidmu1
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.workload: na
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: davidmu
ms.openlocfilehash: c5553e4e7361e6b9a7183cd935be382f967160cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a><span data-ttu-id="0f329-103">Criar e gerenciar VMs Windows no Azure usando Python</span><span class="sxs-lookup"><span data-stu-id="0f329-103">Create and manage Windows VMs in Azure using Python</span></span>

<span data-ttu-id="0f329-104">Uma [VM (Máquina Virtual) do Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) precisa de vários recursos do Azure suporte.</span><span class="sxs-lookup"><span data-stu-id="0f329-104">An [Azure Virtual Machine](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) (VM) needs several supporting Azure resources.</span></span> <span data-ttu-id="0f329-105">Este artigo aborda a criação, o gerenciamento e a exclusão de recursos da VM usando Python.</span><span class="sxs-lookup"><span data-stu-id="0f329-105">This article covers creating, managing, and deleting VM resources using Python.</span></span> <span data-ttu-id="0f329-106">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="0f329-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0f329-107">Criar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0f329-107">Create a Visual Studio project</span></span>
> * <span data-ttu-id="0f329-108">Instalar Pacotes</span><span class="sxs-lookup"><span data-stu-id="0f329-108">Install packages</span></span>
> * <span data-ttu-id="0f329-109">Criar credenciais</span><span class="sxs-lookup"><span data-stu-id="0f329-109">Create credentials</span></span>
> * <span data-ttu-id="0f329-110">Criar recursos</span><span class="sxs-lookup"><span data-stu-id="0f329-110">Create resources</span></span>
> * <span data-ttu-id="0f329-111">Executar tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="0f329-111">Perform management tasks</span></span>
> * <span data-ttu-id="0f329-112">Excluir recursos</span><span class="sxs-lookup"><span data-stu-id="0f329-112">Delete resources</span></span>
> * <span data-ttu-id="0f329-113">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="0f329-113">Run hello application</span></span>

<span data-ttu-id="0f329-114">Demora cerca de 20 minutos toodo essas etapas.</span><span class="sxs-lookup"><span data-stu-id="0f329-114">It takes about 20 minutes toodo these steps.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="0f329-115">Criar um projeto do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="0f329-115">Create a Visual Studio project</span></span>

1. <span data-ttu-id="0f329-116">Se você ainda não fez isso, instale o [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span><span class="sxs-lookup"><span data-stu-id="0f329-116">If you haven't already, install [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio).</span></span> <span data-ttu-id="0f329-117">Selecione **desenvolvimento do Python** Olá página cargas de trabalho e, em seguida, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="0f329-117">Select **Python development** on hello Workloads page, and then click **Install**.</span></span> <span data-ttu-id="0f329-118">Olá resumo, você verá que **Python 3 64 bits (3.6.0)** é selecionado automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="0f329-118">In hello summary, you can see that **Python 3 64-bit (3.6.0)** is automatically selected for you.</span></span> <span data-ttu-id="0f329-119">Se você já tiver instalado o Visual Studio, você pode adicionar carga de trabalho do Python hello usando Olá iniciador do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f329-119">If you have already installed Visual Studio, you can add hello Python workload using hello Visual Studio Launcher.</span></span>
2. <span data-ttu-id="0f329-120">Depois de instalar e iniciar o Visual Studio, clique em **Arquivo** > **Novo** > **Projeto**.</span><span class="sxs-lookup"><span data-stu-id="0f329-120">After installing and starting Visual Studio, click **File** > **New** > **Project**.</span></span>
3. <span data-ttu-id="0f329-121">Clique em **modelos** > **Python** > **aplicativo Python**, digite *myPythonProject* nome Olá saudação do projeto do, selecionar local de saudação do projeto hello e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="0f329-121">Click **Templates** > **Python** > **Python Application**, enter *myPythonProject* for hello name of hello project, select hello location of hello project, and then click **OK**.</span></span>

## <a name="install-packages"></a><span data-ttu-id="0f329-122">Instalar Pacotes</span><span class="sxs-lookup"><span data-stu-id="0f329-122">Install packages</span></span>

1. <span data-ttu-id="0f329-123">No Gerenciador de Soluções, em *myPythonProject*, clique com botão direito do mouse em **Ambientes do Python** e selecione **Adicionar Ambiente Virtual**.</span><span class="sxs-lookup"><span data-stu-id="0f329-123">In Solution Explorer, under *myPythonProject*, right-click **Python Environments**, and then select **Add virtual environment**.</span></span>
2. <span data-ttu-id="0f329-124">Na tela de ambiente Virtual adicionar hello, aceite o nome do padrão de saudação do *env*, certifique-se de que *Python 3.6 (64 bits)* é selecionado para o interpretador de saudação base e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="0f329-124">On hello Add Virtual Environment screen, accept hello default name of *env*, make sure that *Python 3.6 (64-bit)* is selected for hello base interpreter, and then click **Create**.</span></span>
3. <span data-ttu-id="0f329-125">Saudação do botão direito do mouse *env* ambiente que você criou, clique em **instalar pacote da Python**, digite *azure* Olá caixa de pesquisa e pressione Enter.</span><span class="sxs-lookup"><span data-stu-id="0f329-125">Right-click hello *env* environment that you created, click **Install Python Package**, enter *azure* in hello search box, and then press Enter.</span></span>

<span data-ttu-id="0f329-126">Você deve ver em janelas de saída Olá pacotes de saudação do azure foram instalados com êxito.</span><span class="sxs-lookup"><span data-stu-id="0f329-126">You should see in hello output windows that hello azure packages were successfully installed.</span></span> 

## <a name="create-credentials"></a><span data-ttu-id="0f329-127">Criar credenciais</span><span class="sxs-lookup"><span data-stu-id="0f329-127">Create credentials</span></span>

<span data-ttu-id="0f329-128">Antes de começar essa etapa, verifique se você tem uma [entidade de serviço do Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0f329-128">Before you start this step, make sure that you have an [Active Directory service principal](../../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span> <span data-ttu-id="0f329-129">Você também deve registrar a ID do aplicativo hello, chave de autenticação hello e ID de locatário Olá que você precisa em uma etapa posterior.</span><span class="sxs-lookup"><span data-stu-id="0f329-129">You should also record hello application ID, hello authentication key, and hello tenant ID that you need in a later step.</span></span>

1. <span data-ttu-id="0f329-130">Abra *myPythonProject.py* arquivo foi criado e em seguida, adicione este código tooenable toorun seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="0f329-130">Open *myPythonProject.py* file that was created, and then add this code tooenable your application toorun:</span></span>

    ```python
    if __name__ == "__main__":
    ```

2. <span data-ttu-id="0f329-131">código de saudação tooimport que é necessário, adicionar esses superior de toohello instruções do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-131">tooimport hello code that is needed, add these statements toohello top of hello .py file:</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. <span data-ttu-id="0f329-132">Em seguida no arquivo de py hello, adicione variáveis após instruções de importação de saudação toospecify os valores comuns usados em Olá código:</span><span class="sxs-lookup"><span data-stu-id="0f329-132">Next in hello .py file, add variables after hello import statements toospecify common values used in hello code:</span></span>
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    <span data-ttu-id="0f329-133">Substitua **subscription-id** pelo identificador da assinatura.</span><span class="sxs-lookup"><span data-stu-id="0f329-133">Replace **subscription-id** with your subscription identifier.</span></span>

4. <span data-ttu-id="0f329-134">credenciais do Active Directory Olá toocreate que você precisa de solicitações de toomake, adicione essa função depois variáveis Olá no arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-134">toocreate hello Active Directory credentials that you need toomake requests, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    <span data-ttu-id="0f329-135">Substituir **id do aplicativo**, **chave de autenticação**, e **id de locatário** com valores hello coletados anteriormente quando você criou o Active Directory do Azure entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="0f329-135">Replace **application-id**, **authentication-key**, and **tenant-id** with hello values that you previously collected when you created your Azure Active Directory service principal.</span></span>

5. <span data-ttu-id="0f329-136">função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-136">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a><span data-ttu-id="0f329-137">Criar recursos</span><span class="sxs-lookup"><span data-stu-id="0f329-137">Create resources</span></span>
 
### <a name="initialize-management-clients"></a><span data-ttu-id="0f329-138">Inicializar clientes de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="0f329-138">Initialize management clients</span></span>

<span data-ttu-id="0f329-139">Clientes de gerenciamento são necessária toocreate e gerenciar recursos usando Olá SDK de Python no Azure.</span><span class="sxs-lookup"><span data-stu-id="0f329-139">Management clients are needed toocreate and manage resources using hello Python SDK in Azure.</span></span> <span data-ttu-id="0f329-140">clientes do gerenciamento de saudação toocreate, adicione este código em Olá **se** instrução, em seguida, final do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-140">toocreate hello management clients, add this code under hello **if** statement at then end of hello .py file:</span></span>

```python
resource_group_client = ResourceManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
network_client = NetworkManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
compute_client = ComputeManagementClient(
    credentials, 
    SUBSCRIPTION_ID
)
```

### <a name="create-hello-vm-and-supporting-resources"></a><span data-ttu-id="0f329-141">Criar hello VM e recursos de suporte</span><span class="sxs-lookup"><span data-stu-id="0f329-141">Create hello VM and supporting resources</span></span>

<span data-ttu-id="0f329-142">Todos os recursos devem estar contidos em um [Grupo de recursos](../../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f329-142">All resources must be contained in a [Resource group](../../azure-resource-manager/resource-group-overview.md).</span></span>

1. <span data-ttu-id="0f329-143">toocreate um grupo de recursos, adicione essa função depois variáveis Olá no arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-143">toocreate a resource group, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. <span data-ttu-id="0f329-144">função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-144">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

<span data-ttu-id="0f329-145">[Conjuntos de disponibilidade](tutorial-availability-sets.md) tornar mais fácil para você toomaintain Olá VMs usados pelo seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0f329-145">[Availability sets](tutorial-availability-sets.md) make it easier for you toomaintain hello virtual machines used by your application.</span></span>

1. <span data-ttu-id="0f329-146">toocreate uma disponibilidade definida, adicione essa função após variáveis Olá no arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-146">toocreate an availability set, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def create_availability_set(compute_client):
        avset_params = {
            'location': LOCATION,
            'sku': { 'name': 'Aligned' },
            'platform_fault_domain_count': 3
        }
        availability_set_result = compute_client.availability_sets.create_or_update(
            GROUP_NAME,
            'myAVSet',
            avset_params
        )
    ```

2. <span data-ttu-id="0f329-147">função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-147">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

<span data-ttu-id="0f329-148">Um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) é necessário toocommunicate com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="0f329-148">A [Public IP address](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) is needed toocommunicate with hello virtual machine.</span></span>

1. <span data-ttu-id="0f329-149">toocreate um endereço IP público para a máquina virtual de hello, adicione essa função depois variáveis Olá no arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-149">toocreate a public IP address for hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_public_ip_address(network_client):
        public_ip_addess_params = {
            'location': LOCATION,
            'public_ip_allocation_method': 'Dynamic'
        }
        creation_result = network_client.public_ip_addresses.create_or_update(
            GROUP_NAME,
            'myIPAddress',
            public_ip_addess_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="0f329-150">função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-150">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="0f329-151">Uma máquina virtual precisa estar em uma sub-rede de uma [Rede virtual](../../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0f329-151">A virtual machine must be in a subnet of a [Virtual network](../../virtual-network/virtual-networks-overview.md).</span></span>

1. <span data-ttu-id="0f329-152">toocreate uma rede virtual, adicione essa função depois variáveis Olá no arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-152">toocreate a virtual network, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_vnet(network_client):
        vnet_params = {
            'location': LOCATION,
            'address_space': {
                'address_prefixes': ['10.0.0.0/16']
            }
        }
        creation_result = network_client.virtual_networks.create_or_update(
            GROUP_NAME,
            'myVNet',
            vnet_params
        )
        return creation_result.result()
    ```

2. <span data-ttu-id="0f329-153">função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-153">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. <span data-ttu-id="0f329-154">tooadd uma rede virtual do toohello de sub-rede, adicione essa função depois variáveis Olá no arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-154">tooadd a subnet toohello virtual network, add this function after hello variables in hello .py file:</span></span>
    
    ```python
    def create_subnet(network_client):
        subnet_params = {
            'address_prefix': '10.0.0.0/24'
        }
        creation_result = network_client.subnets.create_or_update(
            GROUP_NAME,
            'myVNet',
            'mySubnet',
            subnet_params
        )

        return creation_result.result()
    ```
        
4. <span data-ttu-id="0f329-155">função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-155">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="0f329-156">Uma máquina virtual precisa de um toocommunicate de interface de rede na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="0f329-156">A virtual machine needs a network interface toocommunicate on hello virtual network.</span></span>

1. <span data-ttu-id="0f329-157">toocreate uma interface de rede, adicione essa função depois variáveis Olá no arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-157">toocreate a network interface, add this function after hello variables in hello .py file:</span></span>

    ```python
    def create_nic(network_client):
        subnet_info = network_client.subnets.get(
            GROUP_NAME, 
            'myVNet', 
            'mySubnet'
        )
        publicIPAddress = network_client.public_ip_addresses.get(
            GROUP_NAME,
            'myIPAddress'
        )
        nic_params = {
            'location': LOCATION,
            'ip_configurations': [{
                'name': 'myIPConfig',
                'public_ip_address': publicIPAddress,
                'subnet': {
                    'id': subnet_info.id
                }
            }]
        }
        creation_result = network_client.network_interfaces.create_or_update(
            GROUP_NAME,
            'myNic',
            nic_params
        )

        return creation_result.result()
    ```

2. <span data-ttu-id="0f329-158">função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-158">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

<span data-ttu-id="0f329-159">Agora que você criou Olá todos os recursos de suporte, você pode criar uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f329-159">Now that you created all hello supporting resources, you can create a virtual machine.</span></span>

1. <span data-ttu-id="0f329-160">toocreate Olá a máquina virtual, adicione essa função após variáveis Olá no arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-160">toocreate hello virtual machine, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def create_vm(network_client, compute_client):  
        nic = network_client.network_interfaces.get(
            GROUP_NAME, 
            'myNic'
        )
        avset = compute_client.availability_sets.get(
            GROUP_NAME,
            'myAVSet'
        )
        vm_parameters = {
            'location': LOCATION,
            'os_profile': {
                'computer_name': VM_NAME,
                'admin_username': 'azureuser',
                'admin_password': 'Azure12345678'
            },
            'hardware_profile': {
                'vm_size': 'Standard_DS1'
            },
            'storage_profile': {
                'image_reference': {
                    'publisher': 'MicrosoftWindowsServer',
                    'offer': 'WindowsServer',
                    'sku': '2012-R2-Datacenter',
                    'version': 'latest'
                }
            },
            'network_profile': {
                'network_interfaces': [{
                    'id': nic.id
                }]
            },
            'availability_set': {
                'id': avset.id
            }
        }
        creation_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm_parameters
        )
    
        return creation_result.result()
    ```

    > [!NOTE]
    > <span data-ttu-id="0f329-161">Este tutorial cria uma máquina virtual executando uma versão do sistema de operacional de servidor do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="0f329-161">This tutorial creates a virtual machine running a version of hello Windows Server operating system.</span></span> <span data-ttu-id="0f329-162">toolearn mais sobre como selecionar outras imagens, consulte [navegue e selecione as imagens de máquina virtual do Azure com o Windows PowerShell e hello CLI do Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0f329-162">toolearn more about selecting other images, see [Navigate and select Azure virtual machine images with Windows PowerShell and hello Azure CLI](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
    > 
    > 

2. <span data-ttu-id="0f329-163">função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-163">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a><span data-ttu-id="0f329-164">Executar outras tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="0f329-164">Perform management tasks</span></span>

<span data-ttu-id="0f329-165">Durante a saudação do ciclo de vida de uma máquina virtual, talvez você queira toorun tarefas de gerenciamento como iniciar, parar ou excluir uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f329-165">During hello lifecycle of a virtual machine, you may want toorun management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="0f329-166">Além disso, talvez você queira toocreate código tooautomate repetitivas ou complexas tarefas.</span><span class="sxs-lookup"><span data-stu-id="0f329-166">Additionally, you may want toocreate code tooautomate repetitive or complex tasks.</span></span>

### <a name="get-information-about-hello-vm"></a><span data-ttu-id="0f329-167">Obter informações sobre Olá VM</span><span class="sxs-lookup"><span data-stu-id="0f329-167">Get information about hello VM</span></span>

1. <span data-ttu-id="0f329-168">tooget informações sobre a máquina virtual de hello, adicione essa função depois variáveis Olá no arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-168">tooget information about hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def get_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME, expand='instanceView')
        print("hardwareProfile")
        print("   vmSize: ", vm.hardware_profile.vm_size)
        print("\nstorageProfile")
        print("  imageReference")
        print("    publisher: ", vm.storage_profile.image_reference.publisher)
        print("    offer: ", vm.storage_profile.image_reference.offer)
        print("    sku: ", vm.storage_profile.image_reference.sku)
        print("    version: ", vm.storage_profile.image_reference.version)
        print("  osDisk")
        print("    osType: ", vm.storage_profile.os_disk.os_type.value)
        print("    name: ", vm.storage_profile.os_disk.name)
        print("    createOption: ", vm.storage_profile.os_disk.create_option.value)
        print("    caching: ", vm.storage_profile.os_disk.caching.value)
        print("\nosProfile")
        print("  computerName: ", vm.os_profile.computer_name)
        print("  adminUsername: ", vm.os_profile.admin_username)
        print("  provisionVMAgent: {0}".format(vm.os_profile.windows_configuration.provision_vm_agent))
        print("  enableAutomaticUpdates: {0}".format(vm.os_profile.windows_configuration.enable_automatic_updates))
        print("\nnetworkProfile")
        for nic in vm.network_profile.network_interfaces:
            print("  networkInterface id: ", nic.id)
        print("\nvmAgent")
        print("  vmAgentVersion", vm.instance_view.vm_agent.vm_agent_version)
        print("    statuses")
        for stat in vm_result.instance_view.vm_agent.statuses:
            print("    code: ", stat.code)
            print("    displayStatus: ", stat.display_status)
            print("    message: ", stat.message)
            print("    time: ", stat.time)
        print("\ndisks");
        for disk in vm.instance_view.disks:
            print("  name: ", disk.name)
            print("  statuses")
            for stat in disk.statuses:
                print("    code: ", stat.code)
                print("    displayStatus: ", stat.display_status)
                print("    time: ", stat.time)
        print("\nVM general status")
        print("  provisioningStatus: ", vm.provisioning_state)
        print("  id: ", vm.id)
        print("  name: ", vm.name)
        print("  type: ", vm.type)
        print("  location: ", vm.location)
        print("\nVM instance status")
        for stat in vm.instance_view.statuses:
            print("  code: ", stat.code)
            print("  displayStatus: ", stat.display_status)
    ```
2. <span data-ttu-id="0f329-169">função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-169">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a><span data-ttu-id="0f329-170">Parar Olá VM</span><span class="sxs-lookup"><span data-stu-id="0f329-170">Stop hello VM</span></span>

<span data-ttu-id="0f329-171">Você pode parar uma máquina virtual e mantenha todas as suas configurações, mas continuar toobe cobrado por ele, ou você pode parar uma máquina virtual e desalocar a ele.</span><span class="sxs-lookup"><span data-stu-id="0f329-171">You can stop a virtual machine and keep all its settings, but continue toobe charged for it, or you can stop a virtual machine and deallocate it.</span></span> <span data-ttu-id="0f329-172">Quando uma máquina virtual é desalocada, todos os recursos associados a ela também são desalocadas e a cobrança para eles termina.</span><span class="sxs-lookup"><span data-stu-id="0f329-172">When a virtual machine is deallocated, all resources associated with it are also deallocated and billing ends for it.</span></span>

1. <span data-ttu-id="0f329-173">máquina de virtual toostop Olá sem desalocá-lo, adicione essa função depois variáveis Olá no arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-173">toostop hello virtual machine without deallocating it, add this function after hello variables in hello .py file:</span></span>

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    <span data-ttu-id="0f329-174">Se você quiser toodeallocate Olá virtual machine, altere o código de toothis Olá power_off chamada:</span><span class="sxs-lookup"><span data-stu-id="0f329-174">If you want toodeallocate hello virtual machine, change hello power_off call toothis code:</span></span>

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="0f329-175">função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-175">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a><span data-ttu-id="0f329-176">Olá iniciar VM</span><span class="sxs-lookup"><span data-stu-id="0f329-176">Start hello VM</span></span>

1. <span data-ttu-id="0f329-177">toostart Olá a máquina virtual, adicione essa função após variáveis Olá no arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-177">toostart hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. <span data-ttu-id="0f329-178">função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-178">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a><span data-ttu-id="0f329-179">Redimensionar Olá VM</span><span class="sxs-lookup"><span data-stu-id="0f329-179">Resize hello VM</span></span>

<span data-ttu-id="0f329-180">Muitos aspectos da implantação devem ser considerados ao decidir sobre um tamanho para sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="0f329-180">Many aspects of deployment should be considered when deciding on a size for your virtual machine.</span></span> <span data-ttu-id="0f329-181">Para obter mais informações, consulte [Tamanhos de VM](sizes.md).</span><span class="sxs-lookup"><span data-stu-id="0f329-181">For more information, see [VM sizes](sizes.md).</span></span>

1. <span data-ttu-id="0f329-182">toochange Olá tamanho da saudação máquina virtual, adicione essa função depois variáveis Olá no arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-182">toochange hello size of hello virtual machine, add this function after hello variables in hello .py file:</span></span>

    ```python
    def update_vm(compute_client):
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        vm.hardware_profile.vm_size = 'Standard_DS3'
        update_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME, 
            VM_NAME, 
            vm
        )

    return update_result.result()
    ```

2. <span data-ttu-id="0f329-183">função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-183">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a><span data-ttu-id="0f329-184">Adicionar um disco de dados toohello VM</span><span class="sxs-lookup"><span data-stu-id="0f329-184">Add a data disk toohello VM</span></span>

<span data-ttu-id="0f329-185">Máquinas virtuais podem ter um ou mais [discos de dados](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) que são armazenados como VHDs.</span><span class="sxs-lookup"><span data-stu-id="0f329-185">Virtual machines can have one or more [data disks](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) that are stored as VHDs.</span></span>

1. <span data-ttu-id="0f329-186">tooadd uma máquina de virtual de toohello de disco de dados, adicione essa função depois variáveis Olá no arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-186">tooadd a data disk toohello virtual machine, add this function after hello variables in hello .py file:</span></span> 

    ```python
    def add_datadisk(compute_client):
        disk_creation = compute_client.disks.create_or_update(
            GROUP_NAME,
            'myDataDisk1',
            {
                'location': LOCATION,
                'disk_size_gb': 1,
                'creation_data': {
                    'create_option': DiskCreateOption.empty
                }
            }
        )
        data_disk = disk_creation.result()
        vm = compute_client.virtual_machines.get(GROUP_NAME, VM_NAME)
        add_result = vm.storage_profile.data_disks.append({
            'lun': 1,
            'name': 'myDataDisk1',
            'create_option': DiskCreateOption.attach,
            'managed_disk': {
                'id': data_disk.id
            }
        })
        add_result = compute_client.virtual_machines.create_or_update(
            GROUP_NAME,
            VM_NAME,
            vm)

        return add_result.result()
    ```

2. <span data-ttu-id="0f329-187">função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-187">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a><span data-ttu-id="0f329-188">Excluir recursos</span><span class="sxs-lookup"><span data-stu-id="0f329-188">Delete resources</span></span>

<span data-ttu-id="0f329-189">Como você é cobrado pelos recursos usados no Azure, sempre é um recurso de toodelete de práticas recomendadas que não é mais necessários.</span><span class="sxs-lookup"><span data-stu-id="0f329-189">Because you are charged for resources used in Azure, it's always a good practice toodelete resources that are no longer needed.</span></span> <span data-ttu-id="0f329-190">Se você quiser toodelete Olá VMs e Olá todos os recursos de suporte, você tem toodo é Olá exclusão do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0f329-190">If you want toodelete hello virtual machines and all hello supporting resources, all you have toodo is delete hello resource group.</span></span>

1. <span data-ttu-id="0f329-191">grupo de recursos de saudação toodelete e todos os recursos, adicione essa função depois variáveis Olá no arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-191">toodelete hello resource group and all resources, add this function after hello variables in hello .py file:</span></span>
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. <span data-ttu-id="0f329-192">função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:</span><span class="sxs-lookup"><span data-stu-id="0f329-192">toocall hello function that you previously added, add this code under hello **if** statement at hello end of hello .py file:</span></span>
   
    ```python
    delete_resources(resource_group_client)
    ```

3. <span data-ttu-id="0f329-193">Salve *myPythonProject.py*.</span><span class="sxs-lookup"><span data-stu-id="0f329-193">Save *myPythonProject.py*.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="0f329-194">Executar o aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="0f329-194">Run hello application</span></span>

1. <span data-ttu-id="0f329-195">aplicativo de console hello toorun, clique em **iniciar** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0f329-195">toorun hello console application, click **Start** in Visual Studio.</span></span>

2. <span data-ttu-id="0f329-196">Pressione **Enter** depois Olá status de cada recurso é retornado.</span><span class="sxs-lookup"><span data-stu-id="0f329-196">Press **Enter** after hello status of each resource is returned.</span></span> <span data-ttu-id="0f329-197">Informações de status de saudação, você verá um **êxito** estado de provisionamento.</span><span class="sxs-lookup"><span data-stu-id="0f329-197">In hello status information, you should see a **Succeeded** provisioning state.</span></span> <span data-ttu-id="0f329-198">Após a criação de máquina virtual de saudação, você tem Olá oportunidade toodelete todos os recursos de saudação que você criar.</span><span class="sxs-lookup"><span data-stu-id="0f329-198">After hello virtual machine is created, you have hello opportunity toodelete all hello resources that you create.</span></span> <span data-ttu-id="0f329-199">Antes de pressionar **Enter** toostart recursos de exclusão, você pode levar tooverify de alguns minutos sua criação no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="0f329-199">Before you press **Enter** toostart deleting resources, you could take a few minutes tooverify their creation in hello Azure portal.</span></span> <span data-ttu-id="0f329-200">Se tiver hello Abrir portal do Azure, você pode ter toorefresh Olá folha toosee novos recursos.</span><span class="sxs-lookup"><span data-stu-id="0f329-200">If you have hello Azure portal open, you might have toorefresh hello blade toosee new resources.</span></span>  

    <span data-ttu-id="0f329-201">Ele deve levar cerca de cinco minutos para este toorun do aplicativo de console completamente do início toofinish.</span><span class="sxs-lookup"><span data-stu-id="0f329-201">It should take about five minutes for this console application toorun completely from start toofinish.</span></span> <span data-ttu-id="0f329-202">Pode levar vários minutos após o aplicativo hello foi concluída antes de todos os recursos de saudação e grupo de recursos de saudação são excluídos.</span><span class="sxs-lookup"><span data-stu-id="0f329-202">It may take several minutes after hello application has finished before all hello resources and hello resource group are deleted.</span></span>


## <a name="next-steps"></a><span data-ttu-id="0f329-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0f329-203">Next steps</span></span>

- <span data-ttu-id="0f329-204">Se houver problemas com a implantação de hello, a próxima etapa seria toolook em [Solucionando problemas de implantações de grupo de recursos com o portal do Azure](../../resource-manager-troubleshoot-deployments-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0f329-204">If there were issues with hello deployment, a next step would be toolook at [Troubleshooting resource group deployments with Azure portal](../../resource-manager-troubleshoot-deployments-portal.md)</span></span>
- <span data-ttu-id="0f329-205">Saiba mais sobre Olá [biblioteca do Python do Azure](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="0f329-205">Learn more about hello [Azure Python Library](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)</span></span>

