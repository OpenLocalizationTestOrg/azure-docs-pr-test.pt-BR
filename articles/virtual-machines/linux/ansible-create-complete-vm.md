---
title: aaaUse Ansible toocreate uma VM do Linux completa no Azure | Microsoft Docs
description: "Saiba como toouse Ansible toocreate e gerenciar um ambiente de máquina virtual Linux completo no Azure"
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
ms.openlocfilehash: 970b0427f39fc23240f9faab868196ca4f444e0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a><span data-ttu-id="e0620-103">Criar um ambiente completo de máquina virtual do Linux no Azure com o Ansible</span><span class="sxs-lookup"><span data-stu-id="e0620-103">Create a complete Linux virtual machine environment in Azure with Ansible</span></span>
<span data-ttu-id="e0620-104">Ansible permite implantação de saudação do tooautomate e a configuração de recursos em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="e0620-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="e0620-105">Você pode usar Ansible toomanage suas máquinas virtuais (VMs) no Azure, Olá mesmo como você faria com qualquer outro recurso.</span><span class="sxs-lookup"><span data-stu-id="e0620-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="e0620-106">Este artigo mostra como toocreate um ambiente completo do Linux e suporte a recursos com Ansible.</span><span class="sxs-lookup"><span data-stu-id="e0620-106">This article shows you how toocreate a complete Linux environment and supporting resources with Ansible.</span></span> <span data-ttu-id="e0620-107">Você também pode aprender como muito[criar uma VM básico com Ansible](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="e0620-107">You can also learn how too[Create a basic VM with Ansible](ansible-create-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="e0620-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e0620-108">Prerequisites</span></span>
<span data-ttu-id="e0620-109">toomanage Azure recursos com Ansible, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0620-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="e0620-110">Ansible e Olá módulos Python do SDK do Azure instalados no sistema host.</span><span class="sxs-lookup"><span data-stu-id="e0620-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="e0620-111">Instalar o Ansible no [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) e [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="e0620-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="e0620-112">As credenciais do Azure e Ansible configurado toouse-los.</span><span class="sxs-lookup"><span data-stu-id="e0620-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="e0620-113">Criar credenciais do Azure e configurar o Ansible</span><span class="sxs-lookup"><span data-stu-id="e0620-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="e0620-114">CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e0620-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="e0620-115">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0620-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="e0620-116">Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e0620-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="e0620-117">Você também pode usar o [Cloud Shell](/azure/cloud-shell/quickstart) no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="e0620-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-virtual-network"></a><span data-ttu-id="e0620-118">Criar rede virtual</span><span class="sxs-lookup"><span data-stu-id="e0620-118">Create virtual network</span></span>
<span data-ttu-id="e0620-119">seção a seguir um guia estratégico de Ansible Hello cria uma rede virtual denominada *myVnet* em Olá *10.0.0.0/16* espaço de endereço:</span><span class="sxs-lookup"><span data-stu-id="e0620-119">hello following section in an Ansible playbook creates a virtual network named *myVnet* in hello *10.0.0.0/16* address space:</span></span>

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

<span data-ttu-id="e0620-120">tooadd uma sub-rede, Olá seção a seguir cria uma sub-rede denominada *mySubnet* em Olá *myVnet* rede virtual:</span><span class="sxs-lookup"><span data-stu-id="e0620-120">tooadd a subnet, hello following section creates a subnet named *mySubnet* in hello *myVnet* virtual network:</span></span>

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a><span data-ttu-id="e0620-121">Criar um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="e0620-121">Create public IP address</span></span>
<span data-ttu-id="e0620-122">recursos de tooaccess em Olá Internet, crie e atribua uma tooyour de endereço IP público VM.</span><span class="sxs-lookup"><span data-stu-id="e0620-122">tooaccess resources across hello Internet, create and assign a public IP address tooyour VM.</span></span> <span data-ttu-id="e0620-123">seção a seguir um guia estratégico de Ansible Hello cria um endereço IP público denominado *myPublicIP*:</span><span class="sxs-lookup"><span data-stu-id="e0620-123">hello following section in an Ansible playbook creates a public IP address named *myPublicIP*:</span></span>

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a><span data-ttu-id="e0620-124">Criar um grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="e0620-124">Create Network Security Group</span></span>
<span data-ttu-id="e0620-125">Grupos de segurança de rede controlar o fluxo de saudação do tráfego de rede dentro e fora de sua VM.</span><span class="sxs-lookup"><span data-stu-id="e0620-125">Network Security Groups control hello flow of network traffic in and out of your VM.</span></span> <span data-ttu-id="e0620-126">seção a seguir um guia estratégico de Ansible Hello cria um grupo de segurança de rede denominado *myNetworkSecurityGroup* e define um tráfego de regra de SSH tooallow na porta TCP 22:</span><span class="sxs-lookup"><span data-stu-id="e0620-126">hello following section in an Ansible playbook creates a network security group named *myNetworkSecurityGroup* and defines a rule tooallow SSH traffic on TCP port 22:</span></span>

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


## <a name="create-virtual-network-interface-card"></a><span data-ttu-id="e0620-127">Criar placa de adaptador de rede virtual</span><span class="sxs-lookup"><span data-stu-id="e0620-127">Create virtual network interface card</span></span>
<span data-ttu-id="e0620-128">Uma placa de interface de rede virtual (NIC) conecta-se a sua tooa VM fornecido a rede virtual, o endereço IP público e o grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="e0620-128">A virtual network interface card (NIC) connects your VM tooa given virtual network, public IP address, and network security group.</span></span> <span data-ttu-id="e0620-129">seção a seguir um guia estratégico de Ansible Hello cria uma NIC virtual denominada *myNIC* conectado toohello virtual recursos de rede você criou:</span><span class="sxs-lookup"><span data-stu-id="e0620-129">hello following section in an Ansible playbook creates a virtual NIC named *myNIC* connected toohello virtual networking resources you have created:</span></span>

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


## <a name="create-virtual-machine"></a><span data-ttu-id="e0620-130">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="e0620-130">Create virtual machine</span></span>
<span data-ttu-id="e0620-131">etapa final Olá é toocreate uma máquina virtual e usar todos os recursos de saudação criados.</span><span class="sxs-lookup"><span data-stu-id="e0620-131">hello final step is toocreate a VM and use all hello resources created.</span></span> <span data-ttu-id="e0620-132">seção a seguir um guia estratégico de Ansible Hello cria uma VM denominada *myVM* e anexa Olá NIC virtual denominado *myNIC*.</span><span class="sxs-lookup"><span data-stu-id="e0620-132">hello following section in an Ansible playbook creates a VM named *myVM* and attaches hello virtual NIC named *myNIC*.</span></span> <span data-ttu-id="e0620-133">Insira seus próprios dados de chave públicos no hello *key_data* par da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e0620-133">Enter your own public key data in hello *key_data* pair as follows:</span></span>

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

## <a name="complete-ansible-playbook"></a><span data-ttu-id="e0620-134">Guia estratégico completo do Ansible</span><span class="sxs-lookup"><span data-stu-id="e0620-134">Complete Ansible playbook</span></span>
<span data-ttu-id="e0620-135">toobring todas essas seções juntos, criam um guia estratégico de Ansible denominado *azure_create_complete_vm.yml* e colar Olá conteúdo a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0620-135">toobring all these sections together, create an Ansible playbook named *azure_create_complete_vm.yml* and paste hello following contents:</span></span>

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

<span data-ttu-id="e0620-136">Ansible precisa um toodeploy do grupo de recursos de todos os seus recursos em.</span><span class="sxs-lookup"><span data-stu-id="e0620-136">Ansible needs a resource group toodeploy all your resources into.</span></span> <span data-ttu-id="e0620-137">Crie um grupo de recursos com [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="e0620-137">Create a resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="e0620-138">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="e0620-138">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="e0620-139">ambiente completo de VM com Ansible, execute o Guia estratégico de saudação da seguinte maneira da saudação toocreate:</span><span class="sxs-lookup"><span data-stu-id="e0620-139">toocreate hello complete VM environment with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_complete_vm.yml
```

<span data-ttu-id="e0620-140">saída de Hello parece semelhante toohello exemplo que mostra Olá que VM foi criada com êxito a seguir:</span><span class="sxs-lookup"><span data-stu-id="e0620-140">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="e0620-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e0620-141">Next steps</span></span>
<span data-ttu-id="e0620-142">Este exemplo cria um ambiente de VM completo, incluindo recursos de rede virtual Olá necessário.</span><span class="sxs-lookup"><span data-stu-id="e0620-142">This example creates a complete VM environment including hello required virtual networking resources.</span></span> <span data-ttu-id="e0620-143">Para toocreate um exemplo mais direto uma VM em recursos de rede existentes com as opções padrão, consulte [criar uma VM](ansible-create-vm.md).</span><span class="sxs-lookup"><span data-stu-id="e0620-143">For a more direct example toocreate a VM into existing network resources with default options, see [Create a VM](ansible-create-vm.md).</span></span>
