---
title: "aaaUsing init nuvem toocustomize uma VM do Linux durante a criação no Azure | Microsoft Docs"
description: "Como toocustomize de nuvem init toouse uma VM do Linux durante a criação com hello 1.0 da CLI do Azure"
services: virtual-machines-linux
documentationcenter: 
author: vlivech
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 10/26/2016
ms.author: v-livech
ms.openlocfilehash: b9f480bd04029956d0593bbef931795733cbc2f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-cloud-init-toocustomize-a-linux-vm-during-creation-with-hello-azure-cli-10"></a>Use a nuvem init toocustomize uma VM do Linux durante a criação com hello 1.0 da CLI do Azure
Este artigo mostra como toomake uma tooset de script de inicialização de nuvem Olá hostname, atualizar os pacotes instalados e gerenciar contas de usuário.  scripts de inicialização de nuvem Olá são chamados durante a saudação criação de VM da CLI do Azure.  artigo Olá requer:

* uma conta do Azure ([obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)).
* Olá [CLI do Azure](../../cli-install-nodejs.md) conectado `azure login`.
* Olá CLI do Azure *devem estar no* modo do Azure Resource Manager `azure config mode arm`.

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação

## <a name="quick-commands"></a>Comandos rápidos
Crie um script de nuvem init.txt que define o nome de host hello, todos os pacotes de atualizações e adiciona um tooLinux de usuário sudo.

```sh
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
Crie um toolaunch do grupo de recursos de VMs em.

```azurecli
azure group create myResourceGroup westus
```

Criar uma VM do Linux usando a nuvem init tooconfigure-lo durante a inicialização.

```azurecli
azure vm create \
  -g myResourceGroup \
  -n myVM \
  -l westus \
  -y Linux \
  -f myVMnic \
  -F myVNet \
  -P 10.0.0.0/22 \
  -j mySubnet \
  -k 10.0.0.0/24 \
  -Q canonical:ubuntuserver:14.04.2-LTS:latest \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -C cloud-init.txt
```

## <a name="detailed-walkthrough"></a>Passo a passo detalhado
### <a name="introduction"></a>Introdução
Quando você inicia uma nova VM do Linux, você obtém uma VM padrão do Linux sem nada personalizado nem pronta para suas necessidades. [Nuvem init](https://cloudinit.readthedocs.org) é tooinject uma maneira padrão um script ou configurações na VM Linux como ele está sendo inicializado para Olá primeira vez.

No Azure, há três maneiras toomake alterações em uma VM do Linux enquanto ele é implantado ou inicializado.

* Insira scripts usando a inicialização de nuvem.
* Inserir scripts usando hello Azure [extensão VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
* Um modelo do Azure usando a inicialização de nuvem.
* Um modelo do Azure usando [CustomScriptExtention](extensions-customscript.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

scripts de tooinject a qualquer momento após a inicialização:

* Comandos diretamente do SSH toorun
* Inserir scripts usando hello Azure [extensão VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json), imperativa ou em um modelo do Azure
* Ferramentas de gerenciamento de configuração, como Ansible, Salt, Chef e Puppet.

> [!NOTE]
> : Extensão VMAccess executa um script, como a raiz de saudação do mesmo modo usando SSH pode.  No entanto, usando a extensão de VM Olá permite que vários recursos que ofertas do Azure que podem ser úteis dependendo do cenário.
> 
> 

## <a name="cloud-init-availability-on-azure-vm-quick-create-image-aliases"></a>Disponibilidade de inicialização de nuvem em aliases de imagem de criação rápida de uma VM do Azure:
| Alias | Editor | Oferta | SKU | Versão | inicialização de nuvem |
|:--- |:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7,2 |mais recente |não |
| CoreOS |CoreOS |CoreOS |Estável |mais recente |sim |
| Debian |credativ |Debian |8 |mais recente |não |
| openSUSE |SUSE |openSUSE |13.2 |mais recente |não |
| RHEL |Redhat |RHEL |7,2 |mais recente |não |
| UbuntuLTS |Canônico |UbuntuServer |14.04.4-LTS |mais recente |sim |

A Microsoft está trabalhando com nossos parceiros tooget nuvem-init incluído e trabalhando em imagens de saudação que eles fornecem tooAzure.

## <a name="adding-a-cloud-init-script-toohello-vm-creation-with-hello-azure-cli"></a>Adicionando uma criação de VM nuvem init script toohello com hello CLI do Azure
toolaunch um script de inicialização de nuvem ao criar uma VM no Azure, especifique o arquivo de inicialização de nuvem de hello usando Olá CLI do Azure `--custom-data` alternar.

Crie um toolaunch do grupo de recursos de VMs em.

```azurecli
azure group create myResourceGroup westus
```

Criar uma VM do Linux usando a nuvem init tooconfigure-lo durante a inicialização.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubnet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud-init.txt
```

## <a name="creating-a-cloud-init-script-tooset-hello-hostname-of-a-linux-vm"></a>Criando uma nuvem init script tooset Olá nome de host de uma VM do Linux
Uma das configurações mais importantes para qualquer VM do Linux e hello mais simples seria Olá hostname. Podemos defini-la com facilidade usando o cloud-init com este script.  

### <a name="example-cloud-init-script-named-cloudconfighostnametxt"></a>Script de inicialização de nuvem de exemplo chamado `cloud_config_hostname.txt`.
```sh
#cloud-config
hostname: myservername
```

Durante a inicialização inicial de saudação do hello VM, esse script de inicialização de nuvem define Olá hostname muito`myservername`.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
  --custom-data cloud_config_hostname.txt
```

Logon e verifique se o nome de host de saudação do hello nova VM.

```bash
ssh myVM
hostname
myservername
```

## <a name="creating-a-cloud-init-script-tooupdate-linux"></a>Criar um script de inicialização de nuvem tooupdate Linux
Para segurança, convém seu tooupdate Ubuntu VM na primeira inicialização de saudação.  Usando a nuvem init podemos fazer que com hello siga script, dependendo da distribuição de Linux Olá que você está usando.

### <a name="example-cloud-init-script-cloudconfigaptupgradetxt-for-hello-debian-family"></a>Exemplo de script de inicialização de nuvem `cloud_config_apt_upgrade.txt` para Olá família Debian
```sh
#cloud-config
apt_upgrade: true
```

Depois de Linux foi inicializado, todos os pacotes de saudação instalado são atualizados por meio de `apt-get`.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
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

## <a name="creating-a-cloud-init-script-tooadd-a-user-toolinux"></a>Criando um tooadd de script de inicialização de nuvem tooLinux um usuário
Uma das primeiras tarefas hello em qualquer nova VM do Linux é tooadd um usuário para si mesmo ou tooavoid usando `root`. Chaves de SSH são uma prática recomendada de segurança e facilidade de uso e elas são adicionadas toohello `~/.ssh/authorized_keys` arquivo com esse script de inicialização de nuvem.

### <a name="example-cloud-init-script-cloudconfigadduserstxt-for-debian-family"></a>Script de inicialização de nuvem de exemplo `cloud_config_add_users.txt` para a família Debian
```sh
#cloud-config
users:
  - name: myCloudInitAddedAdminUser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>==myAdminUser@myUbuntuVM
```

Depois de Linux foi inicializado, todos os usuários de saudação listado são toohello criado e adicionado sudo grupo.

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --location westus \
  --os-type Linux \
  --nic-name myVMnic \
  --vnet-name myVNet \
  --vnet-address-prefix 10.0.0.0/22 \
  --vnet-subnet-name mySubNet \
  --vnet-subnet-address-prefix 10.0.0.0/24 \
  --image-urn canonical:ubuntuserver:14.04.2-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username myAdminUser \
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

[Sobre os recursos e extensões de máquina virtual](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[Gerenciar usuários, SSH e seleção ou discos de reparo em máquinas virtuais do Linux do Azure usando Olá extensão VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

