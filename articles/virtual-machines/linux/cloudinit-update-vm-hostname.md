---
title: Usar cloud-init para definir o nome do host para uma VM Linux no Azure | Microsoft Docs
description: "Como usar cloud-init para personalizar uma VM Linux durante a criação com a CLI do Azure 2.0"
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
ms.openlocfilehash: 7455748b2e08104dadfed8cfe41581a400539d4f
ms.sourcegitcommit: b854df4fc66c73ba1dd141740a2b348de3e1e028
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/04/2017
---
# <a name="use-cloud-init-to-set-hostname-for-a-linux-vm-in-azure"></a>Usar cloud-init para definir o nome do host para uma VM Linux no Azure
Este artigo mostra como usar [cloud-init](https://cloudinit.readthedocs.io) para configurar um nome do host específico em uma VM (máquina virtual) ou em um VMSS (conjuntos de dimensionamento de máquinas virtuais) no momento do provisionamento no Azure. Esses scripts cloud-init são executados na primeira inicialização depois que os recursos são provisionados pelo Azure. Para obter mais informações de como o cloud-init funciona nativamente no Azure e as distribuições do Linux compatíveis, consulte [Visão geral de cloud-init](using-cloud-init.md)

## <a name="set-the-hostname-with-cloud-init"></a>Defina o nome do host com a inicialização de nuvem
Por padrão, o nome do host é o mesmo que o nome da VM quando você cria uma nova máquina virtual no Azure.  Para executar um script cloud-init para alterar esse nome do host padrão ao criar uma VM no Azure com [az vm create](/cli/azure/vm#create), especifique o arquivo cloud-init com a opção `--custom-data`.  

Para ver o processo de atualização em ação, crie um arquivo no shell atual denominado *cloud_init_hostname.txt* e cole a seguinte configuração. Para este exemplo, crie o arquivo no Cloud Shell, não no computador local. Você pode usar qualquer editor que queira. Insira `sensible-editor cloud_init_hostname.txt` para criar o arquivo e ver uma lista de editores disponíveis. Escolha #1 para usar o editor **nano**. Verifique se o arquivo cloud-init inteiro foi copiado corretamente, principalmente a primeira linha.  

```yaml
#cloud-config
hostname: myhostname
```

Antes de implantar essa imagem, você precisa criar um grupo de recursos com o comando [az group create](/cli/azure/group#create). Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* no local *eastus*.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

Agora, crie uma VM com [az vm create](/cli/azure/vm#create) e especifique o arquivo de inicialização de nuvem com `--custom-data cloud_init_hostname.txt` da seguinte maneira:

```azurecli-interactive 
az vm create \
  --resource-group myResourceGroup \
  --name centos74 \
  --image OpenLogic:CentOS:7-CI:latest \
  --custom-data cloud_init_hostname.txt \
  --generate-ssh-keys 
```

Depois de criado, a CLI do Azure mostra informações sobre a VM. Use o `publicIpAddress` para conectar por SSH à VM. Insira seu próprio endereço da seguinte maneira:

```bash
ssh <publicIpAddress>
```

Para ver o nome da VM, use o comando `hostname` da seguinte maneira:

```bash
hostname
```

A VM deve relatar o nome de host como esse valor definido no arquivo de inicialização de nuvem, conforme mostrado no exemplo de saída a seguir:

```bash
myhostname
```

## <a name="next-steps"></a>Próximas etapas
Para obter exemplos adicionais de alterações de configuração do cloud-init, consulte o seguinte:
 
- [Adicionar um usuário do Linux adicional a uma VM](cloudinit-add-user.md)
- [Executar um gerenciador de pacotes para atualizar os pacotes existentes na primeira inicialização](cloudinit-update-vm.md)
- [Alterar o nome do host local da VM](cloudinit-update-vm-hostname.md) 
- [Instalar um pacote de aplicativos, atualizar arquivos de configuração e injetar chaves](tutorial-automate-vm-deployment.md)