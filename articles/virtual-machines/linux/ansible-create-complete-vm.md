---
title: Usar o Ansible para criar uma VM do Linux completa no Azure | Microsoft Docs
description: "Saber como usar o Ansible para criar e gerenciar um ambiente completo de máquina virtual do Linux no Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: na
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/25/2017
ms.author: iainfou
ms.openlocfilehash: b2fcc288b40c12a9b3f966156ee2eedf4acca313
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a><span data-ttu-id="0961d-103">Criar um ambiente completo de máquina virtual do Linux no Azure com o Ansible</span><span class="sxs-lookup"><span data-stu-id="0961d-103">Create a complete Linux virtual machine environment in Azure with Ansible</span></span>
<span data-ttu-id="0961d-104">O Ansible permite que você automatize a implantação e a configuração de recursos em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="0961d-104">Ansible allows you to automate the deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="0961d-105">Você pode usar o Ansible para gerenciar suas máquinas virtuais (VMs) no Azure, da mesma forma que faria com qualquer outro recurso.</span><span class="sxs-lookup"><span data-stu-id="0961d-105">You can use Ansible to manage your virtual machines (VMs) in Azure, the same as you would any other resource.</span></span> <span data-ttu-id="0961d-106">Este artigo mostra como criar um ambiente Linux completo e os recursos de apoio com o Ansible.</span><span class="sxs-lookup"><span data-stu-id="0961d-106">This article shows you how to create a complete Linux environment and supporting resources with Ansible.</span></span> <span data-ttu-id="0961d-107">Você também pode aprender a [Criar uma VM básica com o Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="0961d-107">You can also learn how to [Create a basic VM with Ansible](ansible-create-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0961d-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0961d-108">Prerequisites</span></span>
<span data-ttu-id="0961d-109">Para gerenciar recursos do Azure com o Ansible, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="0961d-109">To manage Azure resources with Ansible, you need the following:</span></span>

- <span data-ttu-id="0961d-110">Ansible e os módulos do SDK do Python do Azure instalados no sistema host.</span><span class="sxs-lookup"><span data-stu-id="0961d-110">Ansible and the Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="0961d-111">Instalar o Ansible no [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) e [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="0961d-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="0961d-112">Credenciais do Azure e o Ansible configurados para usá-las.</span><span class="sxs-lookup"><span data-stu-id="0961d-112">Azure credentials, and Ansible configured to use them.</span></span>
    - [<span data-ttu-id="0961d-113">Criar credenciais do Azure e configurar o Ansible</span><span class="sxs-lookup"><span data-stu-id="0961d-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="0961d-114">CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="0961d-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="0961d-115">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="0961d-115">Run `az --version` to find the version.</span></span> 
    - <span data-ttu-id="0961d-116">Se você precisar atualizar, confira [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="0961d-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="0961d-117">Você também pode usar o [Cloud Shell](/azure/cloud-shell/quickstart) no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="0961d-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-virtual-network"></a><span data-ttu-id="0961d-118">Criar rede virtual</span><span class="sxs-lookup"><span data-stu-id="0961d-118">Create virtual network</span></span>
<span data-ttu-id="0961d-119">A seção a seguir em um guia estratégico do Ansible cria uma rede virtual chamada *myVnet* no espaço de endereço *10.0.0.0/16*:</span><span class="sxs-lookup"><span data-stu-id="0961d-119">The following section in an Ansible playbook creates a virtual network named *myVnet* in the *10.0.0.0/16* address space:</span></span>

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

<span data-ttu-id="0961d-120">Para adicionar uma sub-rede, a seção a seguir cria uma sub-rede denominada *mySubnet* na rede virtual *myVnet*:</span><span class="sxs-lookup"><span data-stu-id="0961d-120">To add a subnet, the following section creates a subnet named *mySubnet* in the *myVnet* virtual network:</span></span>

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a><span data-ttu-id="0961d-121">Criar um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="0961d-121">Create public IP address</span></span>
<span data-ttu-id="0961d-122">Para acessar os recursos na Internet, crie e atribua um endereço IP público para a sua VM.</span><span class="sxs-lookup"><span data-stu-id="0961d-122">To access resources across the Internet, create and assign a public IP address to your VM.</span></span> <span data-ttu-id="0961d-123">A seção a seguir em um guia estratégico do Ansible cria um endereço IP público chamado *myPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="0961d-123">The following section in an Ansible playbook creates a public IP address named *myPublicIP*:</span></span>

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a><span data-ttu-id="0961d-124">Criar um grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="0961d-124">Create Network Security Group</span></span>
<span data-ttu-id="0961d-125">Os grupos de segurança de rede controlam o fluxo de entrada e saída de tráfego de rede de sua VM.</span><span class="sxs-lookup"><span data-stu-id="0961d-125">Network Security Groups control the flow of network traffic in and out of your VM.</span></span> <span data-ttu-id="0961d-126">A seção a seguir em um guia estratégico do Ansible cria um grupo de segurança de rede denominado *myNetworkSecurityGroup* e define uma regra para permitir o tráfego de SSH na porta TCP 22:</span><span class="sxs-lookup"><span data-stu-id="0961d-126">The following section in an Ansible playbook creates a network security group named *myNetworkSecurityGroup* and defines a rule to allow SSH traffic on TCP port 22:</span></span>

```yaml
- name: Create Network Security Group that allows SSH
  azure_rm_securitygroup:
    resource_group: myResourceGroup
    name: myNetworkSecurityGroup
    rules:
      - name: SSH
        protocol: TCP
        destination_port_range: 22
        access: Allow
        priority: 1001
        direction: Inbound
```


## <a name="create-virtual-network-interface-card"></a><span data-ttu-id="0961d-127">Criar placa de adaptador de rede virtual</span><span class="sxs-lookup"><span data-stu-id="0961d-127">Create virtual network interface card</span></span>
<span data-ttu-id="0961d-128">Uma placa de adaptador de rede virtual (NIC) conecta-se à VM para uma determinada rede virtual, um endereço IP público e um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="0961d-128">A virtual network interface card (NIC) connects your VM to a given virtual network, public IP address, and network security group.</span></span> <span data-ttu-id="0961d-129">A seção a seguir em um guia estratégico do Ansible cria uma NIC virtual denominada *myNIC* conectada aos recursos da rede virtual que você criou:</span><span class="sxs-lookup"><span data-stu-id="0961d-129">The following section in an Ansible playbook creates a virtual NIC named *myNIC* connected to the virtual networking resources you have created:</span></span>

```yaml
- name: Create virtual network inteface card
  azure_rm_networkinterface:
    resource_group: myResourceGroup
    name: myNIC
    virtual_network: myVnet
    subnet: mySubnet
    public_ip_name: myPublicIP
    security_group: myNetworkSecurityGroup
```


## <a name="create-virtual-machine"></a><span data-ttu-id="0961d-130">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="0961d-130">Create virtual machine</span></span>
<span data-ttu-id="0961d-131">A etapa final é criar uma máquina virtual e usar todos os recursos criados.</span><span class="sxs-lookup"><span data-stu-id="0961d-131">The final step is to create a VM and use all the resources created.</span></span> <span data-ttu-id="0961d-132">A seção a seguir em um guia estratégico do Ansible cria uma VM denominada *myVM* e anexa a NIC virtual denominada *myNIC*.</span><span class="sxs-lookup"><span data-stu-id="0961d-132">The following section in an Ansible playbook creates a VM named *myVM* and attaches the virtual NIC named *myNIC*.</span></span> <span data-ttu-id="0961d-133">Insira seus próprios dados de chave pública no par *key_data* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0961d-133">Enter your own public key data in the *key_data* pair as follows:</span></span>

```yaml
- name: Create VM
  azure_rm_virtualmachine:
    resource_group: myResourceGroup
    name: myVM
    vm_size: Standard_DS1_v2
    admin_username: azureuser
    ssh_password_enabled: false
    ssh_public_keys: 
      - path: /home/azureuser/.ssh/authorized_keys
        key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
    network_interfaces: myNIC
    image:
      offer: CentOS
      publisher: OpenLogic
      sku: '7.3'
      version: latest
```

## <a name="complete-ansible-playbook"></a><span data-ttu-id="0961d-134">Guia estratégico completo do Ansible</span><span class="sxs-lookup"><span data-stu-id="0961d-134">Complete Ansible playbook</span></span>
<span data-ttu-id="0961d-135">Para reunir todas essas seções, crie um guia estratégico do Ansible chamado *azure_create_complete_vm.yml* e cole o seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="0961d-135">To bring all these sections together, create an Ansible playbook named *azure_create_complete_vm.yml* and paste the following contents:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
  - name: Create virtual network
    azure_rm_virtualnetwork:
      resource_group: myResourceGroup
      name: myVnet
      address_prefixes: "10.0.0.0/16"
  - name: Add subnet
    azure_rm_subnet:
      resource_group: myResourceGroup
      name: mySubnet
      address_prefix: "10.0.1.0/24"
      virtual_network: myVnet
  - name: Create public IP address
    azure_rm_publicipaddress:
      resource_group: myResourceGroup
      allocation_method: Static
      name: myPublicIP
  - name: Create Network Security Group that allows SSH
    azure_rm_securitygroup:
      resource_group: myResourceGroup
      name: myNetworkSecurityGroup
      rules:
        - name: SSH
          protocol: Tcp
          destination_port_range: 22
          access: Allow
          priority: 1001
          direction: Inbound
  - name: Create virtual network inteface card
    azure_rm_networkinterface:
      resource_group: myResourceGroup
      name: myNIC
      virtual_network: myVnet
      subnet: mySubnet
      public_ip_name: myPublicIP
      security_group: myNetworkSecurityGroup
  - name: Create VM
    azure_rm_virtualmachine:
      resource_group: myResourceGroup
      name: myVM
      vm_size: Standard_DS1_v2
      admin_username: azureuser
      ssh_password_enabled: false
      ssh_public_keys: 
        - path: /home/azureuser/.ssh/authorized_keys
          key_data: "ssh-rsa AAAAB3Nz{snip}hwhqT9h"
      network_interfaces: myNIC
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="0961d-136">O Ansible precisa de um grupo de recursos para implantar todos os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="0961d-136">Ansible needs a resource group to deploy all your resources into.</span></span> <span data-ttu-id="0961d-137">Crie um grupo de recursos com [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="0961d-137">Create a resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="0961d-138">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* na localização *eastus*:</span><span class="sxs-lookup"><span data-stu-id="0961d-138">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="0961d-139">Para criar o ambiente completo de VM com o Ansible, execute o guia estratégico da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="0961d-139">To create the complete VM environment with Ansible, run the playbook as follows:</span></span>

```bash
ansible-playbook azure_create_complete_vm.yml
```

<span data-ttu-id="0961d-140">A saída é semelhante ao seguinte exemplo que mostra que a máquina virtual foi criada com êxito:</span><span class="sxs-lookup"><span data-stu-id="0961d-140">The output looks similar to the following example that shows the VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create virtual network] *********************************************
changed: [localhost]

TASK [Add subnet] *********************************************************
changed: [localhost]

TASK [Create public IP address] *******************************************
changed: [localhost]

TASK [Create Network Security Group that allows SSH] **********************
changed: [localhost]

TASK [Create virtual network inteface card] *******************************
changed: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=7    changed=6    unreachable=0    failed=0
```

## <a name="next-steps"></a><span data-ttu-id="0961d-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0961d-141">Next steps</span></span>
<span data-ttu-id="0961d-142">Este exemplo cria um ambiente completo de VM, incluindo os recursos necessários de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="0961d-142">This example creates a complete VM environment including the required virtual networking resources.</span></span> <span data-ttu-id="0961d-143">Para obter um exemplo mais direto para criar uma máquina virtual em recursos de rede existentes com as opções padrão, veja [Criar uma máquina virtual](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="0961d-143">For a more direct example to create a VM into existing network resources with default options, see [Create a VM](ansible-create-vm.md).</span></span>