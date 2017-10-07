---
title: maneiras de aaaDifferent toocreate uma VM do Linux no Azure | Microsoft Azure
description: "Saiba mais maneiras diferentes de saudação toocreate uma máquina virtual do Linux no Azure, incluindo links tootools e tutoriais para cada método."
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: f38f8a44-6c88-4490-a84a-46388212d24c
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 250e92c063c87a8c1279097dc2264777d95478d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="different-ways-toocreate-a-linux-vm"></a>Diferentes maneiras toocreate uma VM do Linux
Você tem Olá flexibilidade no Azure toocreate uma máquina virtual Linux (VM) usando ferramentas e fluxos de trabalho tooyou confortável. Este artigo resume essas diferenças e exemplos para criar suas VMs do Linux, incluindo Olá 2.0 do CLI do Azure. Você também pode exibir as opções de criação, incluindo Olá [Azure CLI 1.0](creation-choices-nodejs.md).

Olá [2.0 do CLI do Azure](/cli/azure/install-az-cli2) está disponível em plataformas por meio de um pacote de npm, pacotes de distribuição fornecido ou contêiner do Docker. Instalar o build de hello mais apropriado para seu ambiente e de log em tooan conta do Azure usando [logon az](/cli/azure/#login)

* [Criar uma VM do Linux com hello 2.0 do CLI do Azure](quick-create-cli.md)
  
  * Crie um grupo de recursos com [az group create](/cli/azure/group#create) chamado *myResourceGroup*: 
   
    ```azurecli
    az group create --name myResourceGroup --location eastus
    ```
    
  * Criar uma VM com [criar vm az](/cli/azure/vm#create) chamado *myVM* usando hello mais recente *UbuntuLTS* imagem e gerar as chaves de SSH se eles ainda não existir no *~/.ssh*:

    ```azurecli
    az vm create \
        --resource-group myResourceGroup \
        --name myVM \
        --image UbuntuLTS \
        --generate-ssh-keys
    ```

* [Criar uma VM do Linux com um modelo do Azure](create-ssh-secured-vm-from-template.md)
  
  * Olá exemplo a seguir usa [criar implantação de grupo az](/cli/azure/group/deployment#create) toocreate uma máquina virtual de um modelo armazenado no GitHub:
    
    ```azurecli
    az group deployment create --resource-group myResourceGroup \ 
      --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
      --parameters @myparameters.json
    ```
* [Criar uma VM do Linux e personalizá-la com cloud-init](tutorial-automate-vm-deployment.md)

* [Criar um aplicativo de alta disponibilidade e com balanceamento de carga em várias VMs Linux](tutorial-load-balancer.md)


## <a name="azure-portal"></a>Portal do Azure
Olá [portal do Azure](https://portal.azure.com) permite que você tooquickly criar uma máquina virtual porque não há nada tooinstall em seu sistema. Use Olá toocreate portal do Azure Olá VM:

* [Criar uma VM do Linux usando Olá portal do Azure](quick-create-portal.md) 


## <a name="operating-system-and-image-choices"></a>Sistema operacional e opções de imagem
Ao criar uma máquina virtual, você pode escolher uma imagem com base em Olá deseja toorun do sistema operacional. A Azure e seus parceiros oferecem muitas imagens, algumas delas incluem aplicativos e ferramentas pré-instalados. Ou, carregar uma de suas próprias imagens (consulte [Olá seguinte seção](#use-your-own-image)).

### <a name="azure-images"></a>Imagens do Azure
Saudação de uso [a imagem da vm az](/cli/azure/vm/image) comandos toosee que está disponível, publisher, versão de distribuição e compilações.

Liste os editores disponíveis:

```azurecli
az vm image list-publishers --location eastus
```

Listar produtos (ofertas) disponíveis para determinado editor:

```azurecli
az vm image list-offers --publisher Canonical --location eastus
```

Listar SKUs disponíveis (versões de distribuição) de determinada oferta:

```azurecli
az vm image list-skus --publisher Canonical --offer UbuntuServer --location eastus
```

Liste todas as imagens disponíveis para determinada versão:

```azurecli
az vm image list --publisher Canonical --offer UbuntuServer --sku 16.04.0-LTS --location eastus
```

Para obter mais exemplos de navegação e usar imagens disponíveis, consulte [navegue e selecione as imagens de máquina virtual do Azure com hello CLI do Azure](cli-ps-findimage.md).

Olá [criar vm az](/cli/azure/vm#create) comando tem aliases que você pode usar o acesso de tooquickly Olá distribuições mais comuns e suas versões mais recentes. Usando aliases geralmente é mais rápido do que especificar publicador hello, oferta, SKU e versão cada vez que você cria uma máquina virtual:

| Alias | Editor | Oferta | SKU | Versão |
|:--- |:--- |:--- |:--- |:--- |
| CentOS |OpenLogic |Centos |7,2 |mais recente |
| CoreOS |CoreOS |CoreOS |Estável |mais recente |
| Debian |credativ |Debian |8 |mais recente |
| openSUSE |SUSE |openSUSE |13.2 |mais recente |
| RHEL |Redhat |RHEL |7,2 |mais recente |
| SLES |SLES |SLES |12-SP1 |mais recente |
| UbuntuLTS |Canônico |UbuntuServer |14.04.4-LTS |mais recente |

### <a name="use-your-own-image"></a>Usar sua própria imagem
Se você precisar de personalizações específicas, poderá usar uma imagem com base em uma VM existente do Azure capturando essa VM. Você também pode carregar uma imagem criada no local. Para obter mais informações sobre as distribuições com suporte e como toouse suas próprias imagens, consulte Olá seguintes artigos:

* [Distribuições endossadas pelo Azure](endorsed-distros.md)
* [Informações para distribuições não endossadas](create-upload-generic.md)
* [Como uma imagem de uma VM do Azure existente de toocreate](tutorial-custom-images.md).
  
  * Exemplo de início rápido comandos toocreate uma imagem de uma VM do Azure existente:
    
    ```azurecli
    az vm deallocate --resource-group myResourceGroup --name myVM
    az vm generalize --resource-group myResourceGroup --name myVM
    az vm image create --resource-group myResourceGroup --source myVM --name myImage
    ```

## <a name="next-steps"></a>Próximas etapas
* Criar uma VM do Linux com hello [CLI](quick-create-cli.md), da saudação [portal](quick-create-portal.md), ou usando um [modelo do Azure Resource Manager](../windows/cli-deploy-templates.md).
* Depois de criar uma VM do Linux, [saiba mais sobre discos e armazenamento do Azure](tutorial-manage-disks.md).
* Rápida etapas muito[redefinir uma senha ou as chaves de SSH e gerenciar usuários](using-vmaccess-extension.md).
