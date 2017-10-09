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
# <a name="create-a-windows-virtual-machine-with-hello-azure-cli"></a><span data-ttu-id="01ac6-103">Criar uma máquina virtual do Windows com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="01ac6-103">Create a Windows virtual machine with hello Azure CLI</span></span>

<span data-ttu-id="01ac6-104">Olá CLI do Azure é usado toocreate e gerenciar recursos do Azure Olá linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="01ac6-104">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="01ac6-105">Esses detalhes de guia usando Olá CLI do Azure toodeploy uma máquina virtual executando o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="01ac6-105">This guide details using hello Azure CLI toodeploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="01ac6-106">Depois que a implantação for concluída, vamos conectar toohello servidor e instale o IIS.</span><span class="sxs-lookup"><span data-stu-id="01ac6-106">Once deployment is complete, we connect toohello server and install IIS.</span></span>

<span data-ttu-id="01ac6-107">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="01ac6-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="01ac6-108">Se você escolher tooinstall e usa o hello CLI localmente, este guia de início rápido requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="01ac6-108">If you choose tooinstall and use hello CLI locally, this quickstart requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="01ac6-109">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="01ac6-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="01ac6-110">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="01ac6-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="01ac6-111">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="01ac6-111">Create a resource group</span></span>

<span data-ttu-id="01ac6-112">Crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="01ac6-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="01ac6-113">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="01ac6-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="01ac6-114">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroup* em Olá *eastus* local.</span><span class="sxs-lookup"><span data-stu-id="01ac6-114">hello following example creates a resource group named *myResourceGroup* in hello *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="01ac6-115">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="01ac6-115">Create virtual machine</span></span>

<span data-ttu-id="01ac6-116">Crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="01ac6-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="01ac6-117">Olá, exemplo a seguir cria uma VM denominada *myVM*.</span><span class="sxs-lookup"><span data-stu-id="01ac6-117">hello following example creates a VM named *myVM*.</span></span> <span data-ttu-id="01ac6-118">Este exemplo usa *azureuser* para um nome de usuário administrativo e *myPassword12* senha hello.</span><span class="sxs-lookup"><span data-stu-id="01ac6-118">This example uses *azureuser* for an administrative user name and *myPassword12* as hello password.</span></span> <span data-ttu-id="01ac6-119">Atualize ambiente de tooyour apropriado de toosomething esses valores.</span><span class="sxs-lookup"><span data-stu-id="01ac6-119">Update these values toosomething appropriate tooyour environment.</span></span> <span data-ttu-id="01ac6-120">Esses valores são necessários para criar uma conexão com máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="01ac6-120">These values are needed when creating a connection with hello virtual machine.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="01ac6-121">Quando Olá VM tiver sido criado, Olá CLI do Azure mostra informações toohello semelhante exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="01ac6-121">When hello VM has been created, hello Azure CLI shows information similar toohello following example.</span></span> <span data-ttu-id="01ac6-122">Anote Olá `publicIpAaddress`.</span><span class="sxs-lookup"><span data-stu-id="01ac6-122">Take note of hello `publicIpAaddress`.</span></span> <span data-ttu-id="01ac6-123">Esse endereço é usado tooaccess Olá VM.</span><span class="sxs-lookup"><span data-stu-id="01ac6-123">This address is used tooaccess hello VM.</span></span>

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

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="01ac6-124">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="01ac6-124">Open port 80 for web traffic</span></span> 

<span data-ttu-id="01ac6-125">Por padrão, apenas as conexões RDP são permitidas em máquinas virtuais de tooWindows implantadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="01ac6-125">By default only RDP connections are allowed in tooWindows virtual machines deployed in Azure.</span></span> <span data-ttu-id="01ac6-126">Se essa VM for toobe um servidor Web, você precisa tooopen porta 80 de saudação à Internet.</span><span class="sxs-lookup"><span data-stu-id="01ac6-126">If this VM is going toobe a webserver, you need tooopen port 80 from hello Internet.</span></span> <span data-ttu-id="01ac6-127">Saudação de uso [az vm abrir portas](/cli/azure/vm#open-port) saudação do comando tooopen desejado de porta.</span><span class="sxs-lookup"><span data-stu-id="01ac6-127">Use hello [az vm open-port](/cli/azure/vm#open-port) command tooopen hello desired port.</span></span>  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-toovirtual-machine"></a><span data-ttu-id="01ac6-128">Conectar máquina toovirtual</span><span class="sxs-lookup"><span data-stu-id="01ac6-128">Connect toovirtual machine</span></span>

<span data-ttu-id="01ac6-129">A seguir Olá Use o comando toocreate uma sessão de área de trabalho remota com a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="01ac6-129">Use hello following command toocreate a remote desktop session with hello virtual machine.</span></span> <span data-ttu-id="01ac6-130">Substitua o endereço IP de saudação pelo endereço IP público de saudação de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="01ac6-130">Replace hello IP address with hello public IP address of your virtual machine.</span></span> <span data-ttu-id="01ac6-131">Quando solicitado, insira as credenciais de saudação usadas ao criar a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="01ac6-131">When prompted, enter hello credentials used when creating hello virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="01ac6-132">Instalar o IIS usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="01ac6-132">Install IIS using PowerShell</span></span>

<span data-ttu-id="01ac6-133">Agora que você fez no toohello VM do Azure, você pode usar uma única linha do PowerShell tooinstall IIS e permitir o tráfego da web do hello firewall local regra tooallow.</span><span class="sxs-lookup"><span data-stu-id="01ac6-133">Now that you have logged in toohello Azure VM, you can use a single line of PowerShell tooinstall IIS and enable hello local firewall rule tooallow web traffic.</span></span> <span data-ttu-id="01ac6-134">Abra um prompt do PowerShell e execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="01ac6-134">Open a PowerShell prompt and run hello following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-hello-iis-welcome-page"></a><span data-ttu-id="01ac6-135">Olá exibir página de boas-vindas do IIS</span><span class="sxs-lookup"><span data-stu-id="01ac6-135">View hello IIS welcome page</span></span>

<span data-ttu-id="01ac6-136">Com o IIS instalado e a porta 80 agora aberta na sua VM de saudação à Internet, você pode usar um navegador da web da sua página Bem-vindo do tooview choice saudação padrão IIS.</span><span class="sxs-lookup"><span data-stu-id="01ac6-136">With IIS installed and port 80 now open on your VM from hello Internet, you can use a web browser of your choice tooview hello default IIS welcome page.</span></span> <span data-ttu-id="01ac6-137">Ser se toouse Olá endereço IP público documentado acima da página do toovisit saudação padrão.</span><span class="sxs-lookup"><span data-stu-id="01ac6-137">Be sure toouse hello public IP address you documented above toovisit hello default page.</span></span> 

![Site do IIS padrão](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="01ac6-139">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="01ac6-139">Clean up resources</span></span>

<span data-ttu-id="01ac6-140">Quando não é mais necessário, você pode usar o hello [excluir grupo de az](/cli/azure/group#delete) tooremove grupo de recursos de saudação, a VM e relacionados com todos os recursos de comando.</span><span class="sxs-lookup"><span data-stu-id="01ac6-140">When no longer needed, you can use hello [az group delete](/cli/azure/group#delete) command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="01ac6-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="01ac6-141">Next steps</span></span>

<span data-ttu-id="01ac6-142">Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web.</span><span class="sxs-lookup"><span data-stu-id="01ac6-142">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="01ac6-143">toolearn mais sobre máquinas virtuais do Azure, continuar toohello tutorial para VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="01ac6-143">toolearn more about Azure virtual machines, continue toohello tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="01ac6-144">Tutoriais de máquina virtual do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="01ac6-144">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
