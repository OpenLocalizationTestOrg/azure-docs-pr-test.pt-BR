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
# <a name="create-and-manage-windows-vms-in-azure-using-python"></a>Criar e gerenciar VMs Windows no Azure usando Python

Uma [VM (Máquina Virtual) do Azure](overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) precisa de vários recursos do Azure suporte. Este artigo aborda a criação, o gerenciamento e a exclusão de recursos da VM usando Python. Você aprenderá como:

> [!div class="checklist"]
> * Criar um projeto do Visual Studio
> * Instalar Pacotes
> * Criar credenciais
> * Criar recursos
> * Executar tarefas de gerenciamento
> * Excluir recursos
> * Executar o aplicativo hello

Demora cerca de 20 minutos toodo essas etapas.

## <a name="create-a-visual-studio-project"></a>Criar um projeto do Visual Studio

1. Se você ainda não fez isso, instale o [Visual Studio](https://docs.microsoft.com/visualstudio/install/install-visual-studio). Selecione **desenvolvimento do Python** Olá página cargas de trabalho e, em seguida, clique em **instalar**. Olá resumo, você verá que **Python 3 64 bits (3.6.0)** é selecionado automaticamente para você. Se você já tiver instalado o Visual Studio, você pode adicionar carga de trabalho do Python hello usando Olá iniciador do Visual Studio.
2. Depois de instalar e iniciar o Visual Studio, clique em **Arquivo** > **Novo** > **Projeto**.
3. Clique em **modelos** > **Python** > **aplicativo Python**, digite *myPythonProject* nome Olá saudação do projeto do, selecionar local de saudação do projeto hello e, em seguida, clique em **Okey**.

## <a name="install-packages"></a>Instalar Pacotes

1. No Gerenciador de Soluções, em *myPythonProject*, clique com botão direito do mouse em **Ambientes do Python** e selecione **Adicionar Ambiente Virtual**.
2. Na tela de ambiente Virtual adicionar hello, aceite o nome do padrão de saudação do *env*, certifique-se de que *Python 3.6 (64 bits)* é selecionado para o interpretador de saudação base e, em seguida, clique em **criar**.
3. Saudação do botão direito do mouse *env* ambiente que você criou, clique em **instalar pacote da Python**, digite *azure* Olá caixa de pesquisa e pressione Enter.

Você deve ver em janelas de saída Olá pacotes de saudação do azure foram instalados com êxito. 

## <a name="create-credentials"></a>Criar credenciais

Antes de começar essa etapa, verifique se você tem uma [entidade de serviço do Active Directory](../../azure-resource-manager/resource-group-create-service-principal-portal.md). Você também deve registrar a ID do aplicativo hello, chave de autenticação hello e ID de locatário Olá que você precisa em uma etapa posterior.

1. Abra *myPythonProject.py* arquivo foi criado e em seguida, adicione este código tooenable toorun seu aplicativo:

    ```python
    if __name__ == "__main__":
    ```

2. código de saudação tooimport que é necessário, adicionar esses superior de toohello instruções do arquivo de py hello:

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.compute import ComputeManagementClient
    from azure.mgmt.network import NetworkManagementClient
    from azure.mgmt.compute.models import DiskCreateOption
    ```

3. Em seguida no arquivo de py hello, adicione variáveis após instruções de importação de saudação toospecify os valores comuns usados em Olá código:
   
    ```
    SUBSCRIPTION_ID = 'subscription-id'
    GROUP_NAME = 'myResourceGroup'
    LOCATION = 'westus'
    VM_NAME = 'myVM'
    ```

    Substitua **subscription-id** pelo identificador da assinatura.

4. credenciais do Active Directory Olá toocreate que você precisa de solicitações de toomake, adicione essa função depois variáveis Olá no arquivo de py hello:

    ```python
    def get_credentials():
        credentials = ServicePrincipalCredentials(
            client_id = 'application-id',
            secret = 'authentication-key',
            tenant = 'tenant-id'
        )

        return credentials
    ```

    Substituir **id do aplicativo**, **chave de autenticação**, e **id de locatário** com valores hello coletados anteriormente quando você criou o Active Directory do Azure entidade de serviço.

5. função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:

    ```python
    credentials = get_credentials()
    ```

## <a name="create-resources"></a>Criar recursos
 
### <a name="initialize-management-clients"></a>Inicializar clientes de gerenciamento

Clientes de gerenciamento são necessária toocreate e gerenciar recursos usando Olá SDK de Python no Azure. clientes do gerenciamento de saudação toocreate, adicione este código em Olá **se** instrução, em seguida, final do arquivo de py hello:

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

### <a name="create-hello-vm-and-supporting-resources"></a>Criar hello VM e recursos de suporte

Todos os recursos devem estar contidos em um [Grupo de recursos](../../azure-resource-manager/resource-group-overview.md).

1. toocreate um grupo de recursos, adicione essa função depois variáveis Olá no arquivo de py hello:

    ```python
    def create_resource_group(resource_group_client):
        resource_group_params = { 'location':LOCATION }
        resource_group_result = resource_group_client.resource_groups.create_or_update(
            GROUP_NAME, 
            resource_group_params
        )
    ```

2. função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:

    ```python
    create_resource_group(resource_group_client)
    input('Resource group created. Press enter toocontinue...')
    ```

[Conjuntos de disponibilidade](tutorial-availability-sets.md) tornar mais fácil para você toomaintain Olá VMs usados pelo seu aplicativo.

1. toocreate uma disponibilidade definida, adicione essa função após variáveis Olá no arquivo de py hello:
   
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

2. função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:

    ```python
    create_availability_set(compute_client)
    print("------------------------------------------------------")
    input('Availability set created. Press enter toocontinue...')
    ```

Um [endereço IP público](../../virtual-network/virtual-network-ip-addresses-overview-arm.md) é necessário toocommunicate com a máquina virtual de saudação.

1. toocreate um endereço IP público para a máquina virtual de hello, adicione essa função depois variáveis Olá no arquivo de py hello:

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

2. função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:

    ```python
    creation_result = create_public_ip_address(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Uma máquina virtual precisa estar em uma sub-rede de uma [Rede virtual](../../virtual-network/virtual-networks-overview.md).

1. toocreate uma rede virtual, adicione essa função depois variáveis Olá no arquivo de py hello:

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

2. função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:
   
    ```python
    creation_result = create_vnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

3. tooadd uma rede virtual do toohello de sub-rede, adicione essa função depois variáveis Olá no arquivo de py hello:
    
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
        
4. função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:
   
    ```python
    creation_result = create_subnet(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Uma máquina virtual precisa de um toocommunicate de interface de rede na rede virtual hello.

1. toocreate uma interface de rede, adicione essa função depois variáveis Olá no arquivo de py hello:

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

2. função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:

    ```python
    creation_result = create_nic(network_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

Agora que você criou Olá todos os recursos de suporte, você pode criar uma máquina virtual.

1. toocreate Olá a máquina virtual, adicione essa função após variáveis Olá no arquivo de py hello:
   
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
    > Este tutorial cria uma máquina virtual executando uma versão do sistema de operacional de servidor do Windows hello. toolearn mais sobre como selecionar outras imagens, consulte [navegue e selecione as imagens de máquina virtual do Azure com o Windows PowerShell e hello CLI do Azure](../linux/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
    > 
    > 

2. função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:

    ```python
    creation_result = create_vm(network_client, compute_client)
    print("------------------------------------------------------")
    print(creation_result)
    input('Press enter toocontinue...')
    ```

## <a name="perform-management-tasks"></a>Executar outras tarefas de gerenciamento

Durante a saudação do ciclo de vida de uma máquina virtual, talvez você queira toorun tarefas de gerenciamento como iniciar, parar ou excluir uma máquina virtual. Além disso, talvez você queira toocreate código tooautomate repetitivas ou complexas tarefas.

### <a name="get-information-about-hello-vm"></a>Obter informações sobre Olá VM

1. tooget informações sobre a máquina virtual de hello, adicione essa função depois variáveis Olá no arquivo de py hello:

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
2. função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:

    ```python
    get_vm(compute_client)
    print("------------------------------------------------------")
    input('Press enter toocontinue...')
    ```

### <a name="stop-hello-vm"></a>Parar Olá VM

Você pode parar uma máquina virtual e mantenha todas as suas configurações, mas continuar toobe cobrado por ele, ou você pode parar uma máquina virtual e desalocar a ele. Quando uma máquina virtual é desalocada, todos os recursos associados a ela também são desalocadas e a cobrança para eles termina.

1. máquina de virtual toostop Olá sem desalocá-lo, adicione essa função depois variáveis Olá no arquivo de py hello:

    ```python
    def stop_vm(compute_client):
        compute_client.virtual_machines.power_off(GROUP_NAME, VM_NAME)
    ```

    Se você quiser toodeallocate Olá virtual machine, altere o código de toothis Olá power_off chamada:

    ```python
    compute_client.virtual_machines.deallocate(GROUP_NAME, VM_NAME)
    ```

2. função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:

    ```python
    stop_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="start-hello-vm"></a>Olá iniciar VM

1. toostart Olá a máquina virtual, adicione essa função após variáveis Olá no arquivo de py hello:

    ```python
    def start_vm(compute_client):
        compute_client.virtual_machines.start(GROUP_NAME, VM_NAME)
    ```

2. função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:

    ```python
    start_vm(compute_client)
    input('Press enter toocontinue...')
    ```

### <a name="resize-hello-vm"></a>Redimensionar Olá VM

Muitos aspectos da implantação devem ser considerados ao decidir sobre um tamanho para sua máquina virtual. Para obter mais informações, consulte [Tamanhos de VM](sizes.md).

1. toochange Olá tamanho da saudação máquina virtual, adicione essa função depois variáveis Olá no arquivo de py hello:

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

2. função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:

    ```python
    update_result = update_vm(compute_client)
    print("------------------------------------------------------")
    print(update_result)
    input('Press enter toocontinue...')
    ```

### <a name="add-a-data-disk-toohello-vm"></a>Adicionar um disco de dados toohello VM

Máquinas virtuais podem ter um ou mais [discos de dados](about-disks-and-vhds.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) que são armazenados como VHDs.

1. tooadd uma máquina de virtual de toohello de disco de dados, adicione essa função depois variáveis Olá no arquivo de py hello: 

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

2. função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:

    ```python
    add_result = add_datadisk(compute_client)
    print("------------------------------------------------------")
    print(add_result)
    input('Press enter toocontinue...')
    ```

## <a name="delete-resources"></a>Excluir recursos

Como você é cobrado pelos recursos usados no Azure, sempre é um recurso de toodelete de práticas recomendadas que não é mais necessários. Se você quiser toodelete Olá VMs e Olá todos os recursos de suporte, você tem toodo é Olá exclusão do grupo de recursos.

1. grupo de recursos de saudação toodelete e todos os recursos, adicione essa função depois variáveis Olá no arquivo de py hello:
   
    ```python
    def delete_resources(resource_group_client):
        resource_group_client.resource_groups.delete(GROUP_NAME)
    ```

2. função hello toocall que você adicionou anteriormente, adicione este código em Olá **se** instrução final de saudação do arquivo de py hello:
   
    ```python
    delete_resources(resource_group_client)
    ```

3. Salve *myPythonProject.py*.

## <a name="run-hello-application"></a>Executar o aplicativo hello

1. aplicativo de console hello toorun, clique em **iniciar** no Visual Studio.

2. Pressione **Enter** depois Olá status de cada recurso é retornado. Informações de status de saudação, você verá um **êxito** estado de provisionamento. Após a criação de máquina virtual de saudação, você tem Olá oportunidade toodelete todos os recursos de saudação que você criar. Antes de pressionar **Enter** toostart recursos de exclusão, você pode levar tooverify de alguns minutos sua criação no hello portal do Azure. Se tiver hello Abrir portal do Azure, você pode ter toorefresh Olá folha toosee novos recursos.  

    Ele deve levar cerca de cinco minutos para este toorun do aplicativo de console completamente do início toofinish. Pode levar vários minutos após o aplicativo hello foi concluída antes de todos os recursos de saudação e grupo de recursos de saudação são excluídos.


## <a name="next-steps"></a>Próximas etapas

- Se houver problemas com a implantação de hello, a próxima etapa seria toolook em [Solucionando problemas de implantações de grupo de recursos com o portal do Azure](../../resource-manager-troubleshoot-deployments-portal.md)
- Saiba mais sobre Olá [biblioteca do Python do Azure](https://docs.microsoft.com/python/api/overview/azure/?view=azure-python)

