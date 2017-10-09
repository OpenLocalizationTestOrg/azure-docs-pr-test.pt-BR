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
# <a name="create-a-basic-virtual-machine-in-azure-with-ansible"></a>Criar uma máquina virtual básica no Azure com o Ansible
Ansible permite implantação de saudação do tooautomate e a configuração de recursos em seu ambiente. Você pode usar Ansible toomanage suas máquinas virtuais (VMs) no Azure, Olá mesmo como você faria com qualquer outro recurso. Este artigo mostra como toocreate uma VM básico com Ansible. Você também pode aprender como muito[criar um ambiente completo de VM com Ansible](ansible-create-complete-vm.md).


## <a name="prerequisites"></a>Pré-requisitos
toomanage Azure recursos com Ansible, você precisa Olá a seguir:

- Ansible e Olá módulos Python do SDK do Azure instalados no sistema host.
    - Instalar o Ansible no [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) e [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)
- As credenciais do Azure e Ansible configurado toouse-los.
    - [Criar credenciais do Azure e configurar o Ansible](ansible-install-configure.md#create-azure-credentials)
- CLI do Azure versão 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. 
    - Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). Você também pode usar o [Cloud Shell](/azure/cloud-shell/quickstart) no seu navegador.


## <a name="create-supporting-azure-resources"></a>Criar recursos de suporte do Azure
Neste exemplo, criamos um runbook que implanta uma VM em uma infraestrutura existente. Primeiro, crie um grupo de recursos com [az group create](/cli/azure/vm#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:

```azurecli
az group create --name myResourceGroup --location eastus
```

Crie a rede virtual para sua VM com [az network vnet create](/cli/azure/network/vnet#create). Olá, exemplo a seguir cria uma rede virtual denominada *myVnet* e uma sub-rede denominada *mySubnet*:

```azurecli
az network vnet create \
  --resource-group myResourceGroup \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnet \
  --subnet-prefix 10.0.1.0/24
```


## <a name="create-and-run-ansible-playbook"></a>Criar e executar o guia estratégico do Ansible
Criar um guia estratégico de Ansible denominado **azure_create_vm.yml** e colar Olá conteúdo a seguir. Este exemplo cria uma única VM e configura as credenciais de SSH. Insira seus próprios dados de chave públicos no hello *key_data* par da seguinte maneira:

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

Olá toocreate VM com Ansible, execute o Guia estratégico de saudação da seguinte maneira:

```bash
ansible-playbook azure_create_vm.yml
```

saída de Hello parece semelhante toohello exemplo que mostra Olá que VM foi criada com êxito a seguir:

```bash
PLAY [Create Azure VM] ****************************************************

TASK [Gathering Facts] ****************************************************
ok: [localhost]

TASK [Create VM] **********************************************************
changed: [localhost]

PLAY RECAP ****************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
```


## <a name="next-steps"></a>Próximas etapas
Este exemplo cria uma máquina virtual em um grupo de recursos existente e com uma rede virtual já implantada. Para obter um exemplo mais detalhado sobre como toouse Ansible toocreate recursos de suporte, como uma rede virtual e regras do grupo de segurança de rede, consulte [criar um ambiente completo de VM com Ansible](ansible-create-complete-vm.md).
