---
title: aaaUse init nuvem toocustomize uma VM do Linux | Microsoft Docs
description: "Como toocustomize de nuvem init toouse uma VM do Linux durante a criação com hello 2.0 do CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 195c22cd-4629-4582-9ee3-9749493f1d72
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e7297e162fc73f0da42f195bec2fcbe23b310c1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation"></a>Use a nuvem init toocustomize uma VM do Linux durante a criação
Este artigo mostra como toomake uma tooset de script de inicialização de nuvem Olá hostname, atualizar os pacotes instalados e gerenciar contas de usuário com hello 2.0 do CLI do Azure. scripts de inicialização de nuvem Olá são chamados quando você criar uma máquina virtual (VM) da CLI do Azure. Para obter uma visão mais detalhada sobre como instalar aplicativos, gravar arquivos de configuração e injetar chaves do Key Vault, consulte [este tutorial](tutorial-automate-vm-deployment.md). Você também pode executar essas etapas com hello [Azure CLI 1.0](using-cloud-init-nodejs.md).

## <a name="quick-commands"></a>Comandos rápidos
Crie um script de nuvem init.txt que define o nome de host hello, todos os pacotes de atualizações e adiciona um tooLinux de usuário sudo.

```yaml
#cloud-config
hostname: myVMhostname
apt_upgrade: true
users:
  - name: myNewAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myVM
```

Criar um toolaunch do grupo de recursos VMs em com [criar grupo az](/cli/azure/group#create). Olá, exemplo a seguir cria grupo de recursos de saudação chamado *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Criar uma VM do Linux com [criar vm az](/cli/azure/vm#create) usando tooconfigure nuvem init-lo durante a inicialização com hello `--custom-data` parâmetro.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="detailed-walkthrough"></a>Passo a passo detalhado
Quando você inicia uma nova VM do Linux, você obtém uma VM padrão do Linux sem nada personalizado nem pronta para suas necessidades. [Nuvem init](https://cloudinit.readthedocs.org) é tooinject uma maneira padrão um script ou configurações na VM Linux como ele está sendo inicializado para Olá primeira vez.

No Azure, há algumas maneiras diferentes toomake alterações em uma VM do Linux que está sendo implantado ou inicializado.

* Insira scripts usando a inicialização de nuvem.
* Inserir scripts usando hello Azure [extensão VMAccess](using-vmaccess-extension.md).
* Um modelo do Azure usando a inicialização de nuvem.
* Um modelo do Azure usando [CustomScriptExtention](extensions-customscript.md).

scripts de tooinject a qualquer momento após a inicialização:

* Comandos diretamente do SSH toorun
* Inserir scripts usando hello Azure [extensão VMAccess](using-vmaccess-extension.md), imperativa ou em um modelo do Azure
* Ferramentas de gerenciamento de configuração, como Ansible, Salt, Chef e Puppet.

> [!NOTE]
> Extensão VMAccess executa um script, como a raiz de saudação do mesmo modo usando SSH pode. No entanto, usando a extensão de VM Olá permite que vários recursos que ofertas do Azure que podem ser úteis dependendo do cenário.

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Disponibilidade de inicialização de nuvem em aliases de imagem de criação rápida de uma VM do Azure:
| Alias | Editor | Oferta | SKU | Versão | inicialização de nuvem |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7,2 |mais recente |não |
| CoreOS |CoreOS |CoreOS |Estável |mais recente |sim |
| Debian |credativ |Debian |8 |mais recente |não |
| openSUSE |SUSE |openSUSE |13.2 |mais recente |não |
| RHEL |Redhat |RHEL |7,2 |mais recente |não |
| UbuntuLTS |Canônico |UbuntuServer |14.04.4-LTS |mais recente |sim |

Estamos trabalhando com nossos parceiros tooget nuvem-init incluído e trabalhar com imagens Olá que eles fornecem tooAzure.

## <a name="add-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>Adicionar uma criação de VM nuvem init script toohello com hello CLI do Azure
toolaunch um script de inicialização de nuvem ao criar uma VM no Azure, especifique o arquivo de inicialização de nuvem de hello usando Olá CLI do Azure `--custom-data` alternar.

Criar um toolaunch do grupo de recursos VMs em com [criar grupo az](/cli/azure/group#create). Olá, exemplo a seguir cria grupo de recursos de saudação chamado *myResourceGroup*:

```azurecli
az group create --name myResourceGroup --location eastus
```

Criar uma VM do Linux com [criar vm az](/cli/azure/vm#create) usando tooconfigure nuvem init-lo durante a inicialização.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

## <a name="create-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Criar uma nuvem init script tooset Olá nome de host de uma VM do Linux
Uma das configurações mais importantes para qualquer VM do Linux e hello mais simples seria Olá hostname. Podemos defini-la com facilidade usando o cloud-init com este script.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Script de inicialização de nuvem de exemplo chamado `cloud_config_hostname.txt`.
```yaml
#cloud-config
hostname: myservername
```

Durante a inicialização inicial de saudação do hello VM, esse script de inicialização de nuvem define Olá hostname muito*myservername*. Criar uma VM do Linux com [criar vm az](/cli/azure/vm#create) usando tooconfigure nuvem init-lo durante a inicialização.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud-init.txt
```

Logon e verifique se o nome de host de saudação do hello nova VM.

```bash
ssh myVM
hostname
myservername
```

## <a name="create-a-cloud-init-script"></a>Criar um script cloud-init
Para segurança, convém seu tooupdate Ubuntu VM na primeira inicialização de saudação. Usando a nuvem init podemos fazer que com hello siga script, dependendo da distribuição de Linux Olá que você está usando.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>Exemplo de script de inicialização de nuvem `cloud_config_apt_upgrade.txt` para Olá família Debian
```yaml
#cloud-config
apt_upgrade: true
```

Depois de Linux foi inicializado, todos os pacotes de saudação instalado são atualizados por meio de **apt get**. Criar uma VM do Linux com [criar vm az](/cli/azure/vm#create) usando tooconfigure nuvem init-lo durante a inicialização.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_apt_upgrade.txt
```

Faça logon e verifique se todos os pacotes foram atualizados.

```bash
ssh myUbuntuVM
sudo apt-get upgrade
Reading package lists... Done
Building dependency tree
Reading state information... Done
Calculating upgrade... Done
hello following packages have been kept back:
  linux-generic linux-headers-generic linux-image-generic
0 upgraded, 0 newly installed, 0 tooremove and 0 not upgraded.
```

## <a name="create-a-cloud-init-script-tooadd-a-user-toolinux"></a>Criar um tooadd de script de inicialização de nuvem tooLinux um usuário
Uma das primeiras tarefas hello em qualquer nova VM do Linux é tooadd um usuário para si mesmo ou tooavoid usando *raiz*. Chaves de SSH são uma prática recomendada de segurança e facilidade de uso e elas são adicionadas toohello *~/.ssh/authorized_keys* arquivo com esse script de inicialização de nuvem.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Script de inicialização de nuvem de exemplo `cloud_config_add_users.txt` para a família Debian
```yaml
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Depois de Linux foi inicializado, todos os usuários de saudação listado são toohello criado e adicionado sudo grupo. Criar uma VM do Linux com [criar vm az](/cli/azure/vm#create) usando tooconfigure nuvem init-lo durante a inicialização.

```azurecli
az vm create \
    --resource-group myResourceGroup \
    --name myVM \
    --image UbuntuLTS \
    --admin-username azureuser \
    --generate-ssh-keys \
    --custom-data cloud_config_add_users.txt
```

Logon e verifique se o usuário Olá recém-criado.

```bash
ssh myVM
cat /etc/group
```

Saída

```bash
root:x:0:
<snip />
sudo:x:27:myCloudInitAddedAdminUser
<snip />
myCloudInitAddedAdminUser:x:1000:
```

## <a name="next-steps"></a>Próximas etapas
Inicialização de nuvem está se tornando um toomodify de maneira padrão sua VM do Linux na inicialização. O Azure também tem extensões VM, que permitem que você toomodify sua LinuxVM na inicialização ou durante a execução. Por exemplo, você pode usar hello Azure VMAccessExtension tooreset SSH ou informações do usuário enquanto Olá VM está em execução. Com a inicialização de nuvem, você precisaria de uma senha de saudação do tooreset de reinicialização.

[Sobre os recursos e extensões de máquina virtual](extensions-features.md)

[Gerenciar usuários, SSH e seleção ou discos de reparo em máquinas virtuais do Linux do Azure usando Olá extensão VMAccess](using-vmaccess-extension.md)
