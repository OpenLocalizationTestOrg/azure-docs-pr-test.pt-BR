---
title: "Usar o Ansible para criar uma VM do Linux básica no Azure | Microsoft Docs"
description: "Saber como usar o Ansible para criar e gerenciar uma máquina virtual básica do Linux no Azure"
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
ms.openlocfilehash: 526f3522334450564500c4ba0e401a683cae55f6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="a8792-103">Criar uma máquina virtual básica no Azure com o Ansible</span><span class="sxs-lookup"><span data-stu-id="a8792-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="a8792-104">O Ansible permite que você automatize a implantação e a configuração de recursos em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="a8792-104">Ansible allows you to automate the deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="a8792-105">Você pode usar o Ansible para gerenciar suas máquinas virtuais (VMs) no Azure, da mesma forma que faria com qualquer outro recurso.</span><span class="sxs-lookup"><span data-stu-id="a8792-105">You can use Ansible to manage your virtual machines (VMs) in Azure, the same as you would any other resource.</span></span> <span data-ttu-id="a8792-106">Este artigo mostra como criar uma VM básica com o Ansible.</span><span class="sxs-lookup"><span data-stu-id="a8792-106">This article shows you how to create a basic VM with Ansible.</span></span> <span data-ttu-id="a8792-107">Você também pode aprender a [Criar um ambiente completo de VM com o Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a8792-107">You can also learn how to [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a8792-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a8792-108">Prerequisites</span></span>
<span data-ttu-id="a8792-109">Para gerenciar recursos do Azure com o Ansible, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="a8792-109">To manage Azure resources with Ansible, you need the following:</span></span>

- <span data-ttu-id="a8792-110">Ansible e os módulos do SDK do Python do Azure instalados no sistema host.</span><span class="sxs-lookup"><span data-stu-id="a8792-110">Ansible and the Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="a8792-111">Instalar o Ansible no [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) e [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="a8792-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="a8792-112">Credenciais do Azure e o Ansible configurados para usá-las.</span><span class="sxs-lookup"><span data-stu-id="a8792-112">Azure credentials, and Ansible configured to use them.</span></span>
    - [<span data-ttu-id="a8792-113">Criar credenciais do Azure e configurar o Ansible</span><span class="sxs-lookup"><span data-stu-id="a8792-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="a8792-114">CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a8792-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="a8792-115">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="a8792-115">Run `az --version` to find the version.</span></span> 
    - <span data-ttu-id="a8792-116">Se você precisar atualizar, confira [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a8792-116">If you need to upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="a8792-117">Você também pode usar o [Cloud Shell](/azure/cloud-shell/quickstart) no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="a8792-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="a8792-118">Criar recursos de suporte do Azure</span><span class="sxs-lookup"><span data-stu-id="a8792-118">Create supporting Azure resources</span></span>
<span data-ttu-id="a8792-119">Neste exemplo, criamos um runbook que implanta uma VM em uma infraestrutura existente.</span><span class="sxs-lookup"><span data-stu-id="a8792-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="a8792-120">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="a8792-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="a8792-121">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* na localização *eastus*:</span><span class="sxs-lookup"><span data-stu-id="a8792-121">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="a8792-122">Crie a rede virtual para sua VM com [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="a8792-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="a8792-123">O exemplo a seguir cria uma rede virtual chamada *myVnet* e uma sub-rede chamada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="a8792-123">The following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="a8792-124">Criar e executar o guia estratégico do Ansible</span><span class="sxs-lookup"><span data-stu-id="a8792-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="a8792-125">Crie um guia estratégico do Ansible chamado **azure_create_vm.yml** e cole o seguinte conteúdo.</span><span class="sxs-lookup"><span data-stu-id="a8792-125">Create an Ansible playbook named **azure_create_vm.yml** and paste the following contents.</span></span> <span data-ttu-id="a8792-126">Este exemplo cria uma única VM e configura as credenciais de SSH.</span><span class="sxs-lookup"><span data-stu-id="a8792-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="a8792-127">Insira seus próprios dados de chave pública no par *key_data* da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a8792-127">Enter your own public key data in the *key_data* pair as follows:</span></span>

```yaml
- name: Create Azure VM
  hosts: localhost
  connection: local
  tasks:
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
      image:
        offer: CentOS
        publisher: OpenLogic
        sku: '7.3'
        version: latest
```

<span data-ttu-id="a8792-128">Para criar a VM com o Ansible, execute o guia estratégico da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="a8792-128">To create the VM with Ansible, run the playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="a8792-129">A saída é semelhante ao seguinte exemplo que mostra que a máquina virtual foi criada com êxito:</span><span class="sxs-lookup"><span data-stu-id="a8792-129">The output looks similar to the following example that shows the VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="a8792-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a8792-130">Next steps</span></span>
<span data-ttu-id="a8792-131">Este exemplo cria uma máquina virtual em um grupo de recursos existente e com uma rede virtual já implantada.</span><span class="sxs-lookup"><span data-stu-id="a8792-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="a8792-132">Para obter um exemplo mais detalhado sobre como usar o Ansible para criar recursos de suporte, como uma rede virtual e regras do grupo de segurança de rede, veja [Criar um ambiente completo de VM com o Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="a8792-132">For a more detailed example on how to use Ansible to create supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>