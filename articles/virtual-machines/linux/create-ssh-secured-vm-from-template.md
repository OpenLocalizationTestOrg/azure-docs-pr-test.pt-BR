---
title: aaaCreate uma VM do Linux no Azure de um modelo | Microsoft Docs
description: Como toouse hello Azure CLI 2.0 toocreate uma VM do Linux de um modelo do Gerenciador de recursos
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 721b8378-9e47-411e-842c-ec3276d3256a
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 05/12/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f4b8c4103cccbae13c679ff2a2cac928a0e8e809
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-virtual-machine-with-azure-resource-manager-templates"></a>Como toocreate uma máquina virtual de Linux com modelos do Gerenciador de recursos do Azure
Este artigo mostra como tooquickly implantar uma máquina virtual do Linux (VM) com modelos do Gerenciador de recursos do Azure e hello 2.0 do CLI do Azure. Você também pode executar essas etapas com hello [Azure CLI 1.0](create-ssh-secured-vm-from-template-nodejs.md).


## <a name="templates-overview"></a>Visão geral de modelos
Modelos do Gerenciador de recursos do Azure são arquivos JSON que definem a infraestrutura de saudação e a configuração de sua solução do Azure. Usando um modelo, você pode implantar a solução repetidamente em todo seu ciclo de vida e com a confiança de que seus recursos serão implantados em um estado consistente. toolearn mais sobre o formato de saudação do modelo de saudação e de como você cria, consulte [criar seu primeiro modelo do Azure Resource Manager](../../azure-resource-manager/resource-manager-create-first-template.md). Olá tooview sintaxe JSON para tipos de recursos, consulte [definir recursos em modelos do Azure Resource Manager](/azure/templates/).


## <a name="create-resource-group"></a>Criar grupo de recursos
Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. Você deve criar um grupo de recursos antes de criar uma máquina virtual. Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupVM* em Olá *eastus* região:

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Criar máquina virtual
Olá, exemplo a seguir cria uma VM do [este modelo do Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json) com [criar implantação de grupo az](/cli/azure/group/deployment#create). Fornecer o valor de saudação do sua própria chave pública SSH, como conteúdo de saudação do *~/.ssh/id_rsa.pub*. Se você precisar toocreate um par de chave SSH, consulte [como toocreate e use um SSH par de chaves para VMs do Linux no Azure](mac-create-ssh-keys.md).

```azurecli
az group deployment create --resource-group myResourceGroup \
  --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json \
  --parameters '{"sshKeyData": {"value": "ssh-rsa AAAAB3N{snip}B9eIgoZ"}}'
```

Neste exemplo, você especificou um modelo armazenado no GitHub. Você também pode baixar ou criar um modelo e especificar o caminho de local de saudação com hello mesmo `--template-file` parâmetro.

tooSSH tooyour VM, obter o endereço IP público de saudação com [az rede ip público exibir](/cli/azure/network/public-ip#show):

```azurecli
az network public-ip show \
    --resource-group myResourceGroup \
    --name sshPublicIP \
    --query [ipAddress] \
    --output tsv
```

Você pode, em seguida, SSH tooyour VM como normal:

```bash
ssh azureuser@<ipAddress>
```

## <a name="next-steps"></a>Próximas etapas
Neste exemplo, você criou uma VM básica do Linux. Mais modelos de Gerenciador de recursos que incluem estruturas de aplicativo ou criar um ambiente mais complexo, procurar Olá [Galeria de modelos de início rápido do Azure](https://azure.microsoft.com/documentation/templates/).
