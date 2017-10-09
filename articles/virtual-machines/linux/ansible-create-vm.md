---
title: "aaaUse Ansible toocreate uma VM do Linux básica no Azure | Microsoft Docs"
description: "Saiba como toouse Ansible toocreate e gerenciar uma máquina virtual do Linux básica no Azure"
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
ms.openlocfilehash: ffe278b3f846924ff9c4d026120565146f951152
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a><span data-ttu-id="dead3-103">Criar uma máquina virtual básica no Azure com o Ansible</span><span class="sxs-lookup"><span data-stu-id="dead3-103">Create a basic virtual machine in Azure with Ansible</span></span>
<span data-ttu-id="dead3-104">Ansible permite implantação de saudação do tooautomate e a configuração de recursos em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="dead3-104">Ansible allows you tooautomate hello deployment and configuration of resources in your environment.</span></span> <span data-ttu-id="dead3-105">Você pode usar Ansible toomanage suas máquinas virtuais (VMs) no Azure, Olá mesmo como você faria com qualquer outro recurso.</span><span class="sxs-lookup"><span data-stu-id="dead3-105">You can use Ansible toomanage your virtual machines (VMs) in Azure, hello same as you would any other resource.</span></span> <span data-ttu-id="dead3-106">Este artigo mostra como toocreate uma VM básico com Ansible.</span><span class="sxs-lookup"><span data-stu-id="dead3-106">This article shows you how toocreate a basic VM with Ansible.</span></span> <span data-ttu-id="dead3-107">Você também pode aprender como muito[criar um ambiente completo de VM com Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="dead3-107">You can also learn how too[Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="dead3-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dead3-108">Prerequisites</span></span>
<span data-ttu-id="dead3-109">toomanage Azure recursos com Ansible, você precisa Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="dead3-109">toomanage Azure resources with Ansible, you need hello following:</span></span>

- <span data-ttu-id="dead3-110">Ansible e Olá módulos Python do SDK do Azure instalados no sistema host.</span><span class="sxs-lookup"><span data-stu-id="dead3-110">Ansible and hello Azure Python SDK modules installed on your host system.</span></span>
    - <span data-ttu-id="dead3-111">Instalar o Ansible no [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) e [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span><span class="sxs-lookup"><span data-stu-id="dead3-111">Install Ansible on [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73), and [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)</span></span>
- <span data-ttu-id="dead3-112">As credenciais do Azure e Ansible configurado toouse-los.</span><span class="sxs-lookup"><span data-stu-id="dead3-112">Azure credentials, and Ansible configured toouse them.</span></span>
    - [<span data-ttu-id="dead3-113">Criar credenciais do Azure e configurar o Ansible</span><span class="sxs-lookup"><span data-stu-id="dead3-113">Create Azure credentials and configure Ansible</span></span>](ansible-install-configure.md#create-azure-credentials)
- <span data-ttu-id="dead3-114">CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="dead3-114">Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="dead3-115">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="dead3-115">Run `az --version` toofind hello version.</span></span> 
    - <span data-ttu-id="dead3-116">Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dead3-116">If you need tooupgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> <span data-ttu-id="dead3-117">Você também pode usar o [Cloud Shell](/azure/cloud-shell/quickstart) no seu navegador.</span><span class="sxs-lookup"><span data-stu-id="dead3-117">You can also use [Cloud Shell](/azure/cloud-shell/quickstart) from your browser.</span></span>


## <a name="create-supporting-azure-resources"></a><span data-ttu-id="dead3-118">Criar recursos de suporte do Azure</span><span class="sxs-lookup"><span data-stu-id="dead3-118">Create supporting Azure resources</span></span>
<span data-ttu-id="dead3-119">Neste exemplo, criamos um runbook que implanta uma VM em uma infraestrutura existente.</span><span class="sxs-lookup"><span data-stu-id="dead3-119">In this example, we create a runbook that deploys a VM into an existing infrastructure.</span></span> <span data-ttu-id="dead3-120">Primeiro, crie um grupo de recursos com [az group create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="dead3-120">First, create resource group with [az group create](/cli/azure/vm#create).</span></span> <span data-ttu-id="dead3-121">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="dead3-121">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="dead3-122">Crie a rede virtual para sua VM com [az network vnet create](/cli/azure/network/vnet#create).</span><span class="sxs-lookup"><span data-stu-id="dead3-122">Create a virtual network for your VM with [az network vnet create](/cli/azure/network/vnet#create).</span></span> <span data-ttu-id="dead3-123">Olá, exemplo a seguir cria uma rede virtual denominada *myVnet* e uma sub-rede denominada *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="dead3-123">hello following example creates a virtual network named *myVnet* and a subnet named *mySubnet*:</span></span>

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a><span data-ttu-id="dead3-124">Criar e executar o guia estratégico do Ansible</span><span class="sxs-lookup"><span data-stu-id="dead3-124">Create and run Ansible playbook</span></span>
<span data-ttu-id="dead3-125">Criar um guia estratégico de Ansible denominado **azure_create_vm.yml** e colar Olá conteúdo a seguir.</span><span class="sxs-lookup"><span data-stu-id="dead3-125">Create an Ansible playbook named **azure_create_vm.yml** and paste hello following contents.</span></span> <span data-ttu-id="dead3-126">Este exemplo cria uma única VM e configura as credenciais de SSH.</span><span class="sxs-lookup"><span data-stu-id="dead3-126">This example creates a single VM and configures SSH credentials.</span></span> <span data-ttu-id="dead3-127">Insira seus próprios dados de chave públicos no hello *key_data* par da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="dead3-127">Enter your own public key data in hello *key_data* pair as follows:</span></span>

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

<span data-ttu-id="dead3-128">Olá toocreate VM com Ansible, execute o Guia estratégico de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="dead3-128">toocreate hello VM with Ansible, run hello playbook as follows:</span></span>

```bash
ansible-playbook azure_create_vm.yml
```

<span data-ttu-id="dead3-129">saída de Hello parece semelhante toohello exemplo que mostra Olá que VM foi criada com êxito a seguir:</span><span class="sxs-lookup"><span data-stu-id="dead3-129">hello output looks similar toohello following example that shows hello VM has been successfully created:</span></span>

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a><span data-ttu-id="dead3-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dead3-130">Next steps</span></span>
<span data-ttu-id="dead3-131">Este exemplo cria uma máquina virtual em um grupo de recursos existente e com uma rede virtual já implantada.</span><span class="sxs-lookup"><span data-stu-id="dead3-131">This example creates a VM in an existing resource group and with a virtual network already deployed.</span></span> <span data-ttu-id="dead3-132">Para obter um exemplo mais detalhado sobre como toouse Ansible toocreate recursos de suporte, como uma rede virtual e regras do grupo de segurança de rede, consulte [criar um ambiente completo de VM com Ansible](ansible-create-complete-vm.md).</span><span class="sxs-lookup"><span data-stu-id="dead3-132">For a more detailed example on how toouse Ansible toocreate supporting resources such as a virtual network and Network Security Group rules, see [Create a complete VM environment with Ansible](ansible-create-complete-vm.md).</span></span>
