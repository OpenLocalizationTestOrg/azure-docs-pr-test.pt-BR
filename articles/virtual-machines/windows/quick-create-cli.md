---
title: "aaaAzure início rápido - criar CLI de VM do Windows | Microsoft Docs"
description: "Aprenda rapidamente toocreate um máquinas virtuais do Windows com hello CLI do Azure."
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/11/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 029bdecec219b12b80b958ceeedda214f1b13149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a>Criar uma máquina virtual do Windows com hello CLI do Azure

Olá CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts. Esses detalhes de guia usando Olá CLI do Azure toodeploy uma máquina virtual executando o Windows Server 2016. Depois que a implantação for concluída, vamos conectar toohello servidor e instale o IIS.

Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 


## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Crie um grupo de recursos com [az group create](/cli/azure/group#create). Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados. 

Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a>Criar máquina virtual

Crie uma VM com [az vm create](/cli/azure/vm#create). 

Olá, exemplo a seguir cria uma VM denominada *myVM*. Este exemplo usa *azureuser* para um nome de usuário administrativo e *myPassword12* senha hello. Atualize ambiente de tooyour apropriado de toosomething esses valores. Esses valores são necessários para criar uma conexão com máquina virtual de saudação.

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

Quando Olá VM tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir. Anote Olá `publicIpAaddress`. Esse endereço é usado tooaccess Olá VM.

```azurecli-interactive 
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

## <a name="open-port-80-for-web-traffic"></a>Abra a porta 80 para tráfego da Web 

Por padrão, apenas as conexões RDP são permitidas em máquinas virtuais de tooWindows implantadas no Azure. Se essa VM for toobe um servidor Web, você precisa tooopen porta 80 de saudação à Internet. Saudação de uso [az vm abrir portas](/cli/azure/vm#open-port) saudação do comando tooopen desejado de porta.  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a>Conectar máquina toovirtual

A seguir Olá Use o comando toocreate uma sessão de área de trabalho remota com a máquina virtual de saudação. Substitua o endereço IP de saudação pelo endereço IP público de saudação de sua máquina virtual. Quando solicitado, insira as credenciais de saudação usadas ao criar a máquina virtual de saudação.

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a>Instalar o IIS usando o PowerShell

Agora que você fez no toohello VM do Azure, você pode usar uma única linha do PowerShell tooinstall IIS e permitir o tráfego da web do hello firewall local regra tooallow. Abra um prompt do PowerShell e execute Olá comando a seguir:

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a>Olá exibir página de boas-vindas do IIS

Com o IIS instalado e a porta 80 agora aberta na sua VM de saudação à Internet, você pode usar um navegador da web da sua página Bem-vindo do tooview choice saudação padrão IIS. Ser se toouse Olá endereço IP público documentado acima da página do toovisit saudação padrão. 

![Site do IIS padrão](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a>Limpar recursos

Quando não é mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) tooremove grupo de recursos de saudação, a VM e relacionados com todos os recursos de comando.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a>Próximas etapas

Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web. toolearn mais sobre máquinas virtuais do Azure, continuar toohello tutorial para VMs do Windows.

> [!div class="nextstepaction"]
> [Tutoriais de máquina virtual do Windows Azure](./tutorial-manage-vm.md)
