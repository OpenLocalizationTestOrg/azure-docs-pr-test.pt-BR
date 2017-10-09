---
title: "aaaAzure início rápido - criar VM CLI | Microsoft Docs"
description: "Aprenda rapidamente máquinas virtuais de toocreate com hello CLI do Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: hero-article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 0d9c686e2f4c7339b29b8c43cd1dd9ee56d7dc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-linux-virtual-machine-with-hello-azure-cli"></a>Criar uma máquina virtual Linux com hello CLI do Azure

Olá CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts. Esses detalhes de guia usando Olá CLI do Azure toodeploy uma máquina virtual com o servidor do Ubuntu. Depois que o servidor de saudação for implantado, é criada uma conexão SSH e um servidor de Web NGINX está instalado.

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Criar um grupo de recursos com hello [criar grupo az](/cli/azure/group#create) comando. Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. 

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Criar máquina virtual

Criar uma VM com hello [criar vm az](/cli/azure/vm#create) comando. 

Olá, exemplo a seguir cria uma VM denominada *myVM* e cria as chaves de SSH se eles ainda não existir em um local de chave padrão. toouse um conjunto específico de chaves, use Olá `--ssh-key-value` opção.  

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image UbuntuLTS --generate-ssh-keys
```

Quando Olá VM tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir. Anote Olá `publicIpAddress`. Esse endereço é usado tooaccess Olá VM.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.68.254.142",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Abra a porta 80 para tráfego da Web 

Por padrão, somente as conexões de SSH são permitidas em máquinas virtuais Linux implantadas no Azure. Se essa VM for toobe um servidor Web, você precisa tooopen porta 80 de saudação à Internet. Saudação de uso [az vm abrir portas](/cli/azure/vm#open-port) saudação do comando tooopen desejado de porta.  
 
 ```azurecli-interactive 
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```

## <a name="ssh-into-your-vm"></a>SSH em sua VM

A seguir Olá Use o comando toocreate uma sessão SSH com a máquina virtual de saudação. Certifique-se de que tooreplace  *<publicIpAddress>*  com hello corrija o endereço IP público de sua máquina virtual.  Em nosso exemplo acima, nosso endereço IP era *40.68.254.142*.

```bash 
ssh <publicIpAddress>
```

## <a name="install-nginx"></a>Instalar o NGINX

Use a seguir de saudação bash origens do pacote do script tooupdate e instala pacote NGINX mais recente de saudação. 

```bash 
#!/bin/bash

# update package source
apt-get -y update

# install NGINX
apt-get -y install nginx
```

## <a name="view-hello-nginx-welcome-page"></a>Página de boas-vindas do modo de exibição Olá NGINX

Com NGINX instalado e a porta 80 agora aberta na sua VM do hello Internet - você pode usar um navegador da web da sua página Bem-vindo escolha tooview saudação padrão NGINX. Ser Olá-se de toouse *publicIpAddress* documentado acima da página do toovisit saudação padrão. 

![Site padrão NGINX](./media/quick-create-cli/nginx.png) 


## <a name="clean-up-resources"></a>Limpar recursos

Quando não é mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) tooremove grupo de recursos de saudação, a VM e relacionados com todos os recursos de comando.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web. toolearn mais sobre máquinas virtuais do Azure, continuar toohello tutorial para VMs do Linux.


> [!div class="nextstepaction"]
> [Tutoriais de máquina virtual do Linux Azure](./tutorial-manage-vm.md)
