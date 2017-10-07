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
# <a name="create-a-complete-linux-virtual-machine-environment-in-azure-with-ansible"></a>Criar um ambiente completo de máquina virtual do Linux no Azure com o Ansible
Ansible permite implantação de saudação do tooautomate e a configuração de recursos em seu ambiente. Você pode usar Ansible toomanage suas máquinas virtuais (VMs) no Azure, Olá mesmo como você faria com qualquer outro recurso. Este artigo mostra como toocreate um ambiente completo do Linux e suporte a recursos com Ansible. Você também pode aprender como muito[criar uma VM básico com Ansible](ansible-create-vm.md).


## <a name="prerequisites"></a>Pré-requisitos
toomanage Azure recursos com Ansible, você precisa Olá a seguir:

- Ansible e Olá módulos Python do SDK do Azure instalados no sistema host.
    - Instalar o Ansible no [Ubuntu 16.04 LTS](ansible-install-configure.md#ubuntu-1604-lts), [CentOS 7.3](ansible-install-configure.md#centos-73) e [SLES 12.2 SP2](ansible-install-configure.md#sles-122-sp2)
- As credenciais do Azure e Ansible configurado toouse-los.
    - [Criar credenciais do Azure e configurar o Ansible](ansible-install-configure.md#create-azure-credentials)
- CLI do Azure versão 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. 
    - Se você precisar tooupgrade, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). Você também pode usar o [Cloud Shell](/azure/cloud-shell/quickstart) no seu navegador.


## <a name="create-virtual-network"></a>Criar rede virtual
seção a seguir um guia estratégico de Ansible Hello cria uma rede virtual denominada *myVnet* em Olá *10.0.0.0/16* espaço de endereço:

```yaml
- name: Create virtual network
  azure_rm_virtualnetwork:
    resource_group: myResourceGroup
    name: myVnet
    address_prefixes: "10.10.0.0/16"
```

tooadd uma sub-rede, Olá seção a seguir cria uma sub-rede denominada *mySubnet* em Olá *myVnet* rede virtual:

```yaml
- name: Add subnet
  azure_rm_subnet:
    resource_group: myResourceGroup
    name: mySubnet
    address_prefix: "10.0.1.0/24"
    virtual_network: myVnet
```


## <a name="create-public-ip-address"></a>Criar um endereço IP público
recursos de tooaccess em Olá Internet, crie e atribua uma tooyour de endereço IP público VM. seção a seguir um guia estratégico de Ansible Hello cria um endereço IP público denominado *myPublicIP*:

```yaml
- name: Create public IP address
  azure_rm_publicipaddress:
    resource_group: myResourceGroup
    allocation_method: Static
    name: myPublicIP
```


## <a name="create-network-security-group"></a>Criar um grupo de segurança de rede
Grupos de segurança de rede controlar o fluxo de saudação do tráfego de rede dentro e fora de sua VM. seção a seguir um guia estratégico de Ansible Hello cria um grupo de segurança de rede denominado *myNetworkSecurityGroup* e define um tráfego de regra de SSH tooallow na porta TCP 22:

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


## <a name="create-virtual-network-interface-card"></a>Criar placa de adaptador de rede virtual
Uma placa de interface de rede virtual (NIC) conecta-se a sua tooa VM fornecido a rede virtual, o endereço IP público e o grupo de segurança de rede. seção a seguir um guia estratégico de Ansible Hello cria uma NIC virtual denominada *myNIC* conectado toohello virtual recursos de rede você criou:

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


## <a name="create-virtual-machine"></a>Criar máquina virtual
etapa final Olá é toocreate uma máquina virtual e usar todos os recursos de saudação criados. seção a seguir um guia estratégico de Ansible Hello cria uma VM denominada *myVM* e anexa Olá NIC virtual denominado *myNIC*. Insira seus próprios dados de chave públicos no hello *key_data* par da seguinte maneira:

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

## <a name="complete-ansible-playbook"></a>Guia estratégico completo do Ansible
toobring todas essas seções juntos, criam um guia estratégico de Ansible denominado *azure_create_complete_vm.yml* e colar Olá conteúdo a seguir:

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

Ansible precisa um toodeploy do grupo de recursos de todos os seus recursos em. Crie um grupo de recursos com [az group create](/cli/azure/vm#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local:

```azurecli
az group create --name myResourceGroup --location eastus
```

ambiente completo de VM com Ansible, execute o Guia estratégico de saudação da seguinte maneira da saudação toocreate:

```bash
ansible-playbook azure_create_complete_vm.yml
```

saída de Hello parece semelhante toohello exemplo que mostra Olá que VM foi criada com êxito a seguir:

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

## <a name="next-steps"></a>Próximas etapas
Este exemplo cria um ambiente de VM completo, incluindo recursos de rede virtual Olá necessário. Para toocreate um exemplo mais direto uma VM em recursos de rede existentes com as opções padrão, consulte [criar uma VM](ansible-create-vm.md).
