---
title: aaaCreate uma VM do Linux usando um modelo do Azure com o Azure CLI 1.0 | Microsoft Docs
description: Crie uma VM do Linux no Azure usando hello 1.0 da CLI do Azure e um modelo do Gerenciador de recursos do Azure.
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
ms.date: 05/12/2017
ms.author: v-livech
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b694cc8247a8431b7ef4b24cc7dc2b4cdb9660ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-linux-vm-using-hello-azure-cli-10-an-azure-resource-manager-template"></a>Como toocreate uma VM do Linux usando Olá CLI do Azure 1.0 um modelo do Gerenciador de recursos do Azure
Este artigo mostra como tooquickly implantar uma máquina Virtual do Linux usando hello 1.0 da CLI do Azure e um modelo do Gerenciador de recursos do Azure. artigo Olá requer:

* uma conta do Azure ([obtenha uma avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/)).
* Olá [Azure CLI 1.0](../../cli-install-nodejs.md) conectado `azure login`.
* Olá CLI do Azure *devem estar no* modo do Azure Resource Manager `azure config mode arm`.

Você pode implantar rapidamente um modelo de VM do Linux usando Olá [portal do Azure](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#quick-command-summary) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](create-ssh-secured-vm-from-template.md) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação

## <a name="quick-command-summary"></a>Resumo rápido do comando
```azurecli
azure group create \
    -n myResourceGroup \
    -l westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

## <a name="detailed-walkthrough"></a>Passo a passo detalhado
Modelos permitem toocreate VMs no Azure com as configurações que você deseja toocustomize durante a inicialização de hello, configurações, como nomes de usuário e nomes de host. Neste artigo, estamos iniciando um modelo do Azure utilizando uma VM do Ubuntu junto com um grupo de segurança de rede (NSG) com a porta 22 aberta para o SSH.

Os modelos do Azure Resource Manager são arquivos JSON que podem ser usados para tarefas únicas simples, como iniciar uma VM Ubuntu, como feito neste artigo.  Modelos do Azure também podem ser usado tooconstruct as configurações do Azure complexas de ambientes inteiros como uma pilha de implantação de produção, desenvolvimento ou teste.

## <a name="create-hello-linux-vm"></a>Criar hello VM do Linux
Olá mostra exemplo de código a seguir como toocall `azure group create` toocreate um recurso de grupo e implantar uma VM do Linux protegidos SSH no hello mesmo tempo usando [este modelo do Azure Resource Manager](https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json). Lembre-se de que o exemplo é necessário toouse nomes de ambiente tooyour exclusivo. Este exemplo usa *myResourceGroup* como nome do grupo de recursos hello e *myVM* como nome da VM hello.

```azurecli
azure group create \
    --name myResourceGroup \
    --location westus \
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-vm-sshkey/azuredeploy.json
```

saída de Hello deve ter aparência Olá bloco de saída a seguir:

```azurecli
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
info:    Supply values for hello following parameters
sshKeyData: ssh-rsa AAAAB3Nza<..ssh public key text..>VQgwjNjQ== myAdminUser@myVM
+ Initializing template configurations and parameters
+ Creating a deployment
info:    Created template deployment "azuredeploy"
data:    Id:                  /subscriptions/<..subid text..>/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westus
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

Esse exemplo implantado uma VM usando Olá `--template-uri` parâmetro.  Você também pode baixar ou criar um modelo localmente e passar o modelo de saudação usando Olá `--template-file` parâmetro com um arquivo de modelo do caminho toohello como um argumento. Olá CLI do Azure solicita parâmetros Olá exigidos pelo modelo de saudação.

## <a name="next-steps"></a>Próximas etapas
Saudação de pesquisa [Galeria de modelos](https://azure.microsoft.com/documentation/templates/) toodiscover que toodeploy de estruturas de aplicativo Avançar.

