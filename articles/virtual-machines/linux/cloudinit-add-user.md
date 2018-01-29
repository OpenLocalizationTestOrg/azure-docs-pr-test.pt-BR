---
title: "Usar cloud-init para adicionar um usuário a uma VM Linux no Azure | Microsoft Docs"
description: "Como usar cloud-init para adicionar um usuário a uma VM Linux durante a criação com a CLI do Azure 2.0"
services: virtual-machines-linux
documentationcenter: 
author: rickstercdn
manager: jeconnoc
editor: 
tags: azure-resource-manager
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 11/29/2017
ms.author: rclaus
ms.openlocfilehash: 728ffed27747cb298d5da312014a3c9e98b44f1e
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="use-cloud-init-to-add-a-user-to-a-linux-vm-in-azure"></a>Usar cloud-init para adicionar um usuário a uma VM Linux no Azure
Este artigo mostra como usar [cloud-init](https://cloudinit.readthedocs.io) para adicionar um usuário em uma VM (máquina virtual) ou VMSS (conjuntos de dimensionamento de máquinas virtuais) no tempo de provisionamento no Azure. Esse script cloud-init é executado na primeira inicialização uma vez que os recursos tiverem sido provisionados pelo Azure. Para obter mais informações sobre como o cloud-init funciona nativamente no Azure e as distribuições do Linux compatíveis, consulte [Visão geral de cloud-init](using-cloud-init.md).

## <a name="add-a-user-to-a-vm-with-cloud-init"></a>Adicionar um usuário a uma VM com a inicialização de nuvem
Uma das primeiras tarefas em qualquer nova VM Linux é adicionar um usuário adicional para você para evitar o uso do *root*. As chaves de SSH são uma prática recomendada para segurança e usabilidade. As chaves são adicionadas ao arquivo *~/.ssh/authorized_keys* com esse script de inicialização de nuvem.

Para adicionar um usuário a uma VM Linux, crie um arquivo no shell atual chamado *cloud_init_add_user.txt* e cole a configuração a seguir. Para este exemplo, crie o arquivo no Cloud Shell, não no computador local. Você pode usar qualquer editor que queira. Insira `sensible-editor cloud_init_add_user.txt` para criar o arquivo e ver uma lista de editores disponíveis. Escolha #1 para usar o editor **nano**. Verifique se o arquivo cloud-init inteiro foi copiado corretamente, principalmente a primeira linha.  Você precisa fornecer sua própria chave pública (como o conteúdo de *~/.ssh/id_rsa.pub*) para o valor de `ssh-authorized-keys:`, ela foi reduzida aqui para simplificar o exemplo.

```yaml
#cloud-config
users:
  - default
  - name: myadminuser
    groups: sudo
    shell: /bin/bash
    sudo: ['ALL=(ALL) NOPASSWD:ALL']
    ssh-authorized-keys:
      - ssh-rsa AAAAB3<snip>
```
> [!NOTE] 
> O arquivo #cloud-config inclui o parâmetro `- default` incluído. Isso acrescentará o usuário ao usuário administrador existente criado durante o provisionamento. Se você criar um usuário sem o parâmetro `- default`, o usuário administrador gerado automaticamente criado pela plataforma Azure será substituído. 

Antes de implantar essa imagem, você precisa criar um grupo de recursos com o comando [az group create](/cli/azure/group#create). Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* no local *eastus*.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

Agora, crie uma VM com [az vm create](/cli/azure/vm#create) e especifique o arquivo de inicialização de nuvem com `--custom-data cloud_init_add_user.txt` da seguinte maneira:

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroup \
  --name centos74 \
  --image OpenLogic:CentOS:7-CI:latest \
  --custom-data cloud_init_add_user.txt \
  --generate-ssh-keys 
```

Conecte-se por SSH ao endereço IP público da VM mostrado na saída do comando anterior. Insira seu próprio **publicIpAddress** da seguinte maneira:

```bash
ssh <publicIpAddress>
```

Para confirmar se o usuário foi adicionado para a VM e os grupos especificados, exiba o conteúdo do arquivo */etc/group* da seguinte maneira:

```bash
cat /etc/group
```

A saída de exemplo a seguir mostra que o usuário do arquivo *cloud_init_add_user.txt* foi adicionado à VM e ao grupo apropriado:

```bash
root:x:0:
<snip />
sudo:x:27:myadminuser
<snip />
myadminuser:x:1000:
```

## <a name="next-steps"></a>Próximas etapas
Para obter exemplos adicionais de alterações de configuração do cloud-init, consulte o seguinte:
 
- [Adicionar um usuário do Linux adicional a uma VM](cloudinit-add-user.md)
- [Executar um gerenciador de pacotes para atualizar os pacotes existentes na primeira inicialização](cloudinit-update-vm.md)
- [Alterar o nome do host local da VM](cloudinit-update-vm-hostname.md) 
- [Instalar um pacote de aplicativos, atualizar arquivos de configuração e injetar chaves](tutorial-automate-vm-deployment.md)