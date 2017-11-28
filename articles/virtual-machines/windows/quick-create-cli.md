---
title: "Início Rápido do Azure – Criar CLI de VM do Windows | Microsoft Docs"
description: "Aprenda rapidamente criar máquinas virtuais Windows com a CLI do Azure."
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
ms.openlocfilehash: fcb2f1389b3434d0d2e3145217e54ceb2326b969
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-windows-virtual-machine-with-the-azure-cli"></a><span data-ttu-id="4c214-103">Criar uma máquina virtual do Windows com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4c214-103">Create a Windows virtual machine with the Azure CLI</span></span>

<span data-ttu-id="4c214-104">A CLI do Azure é usada para criar e gerenciar recursos do Azure da linha de comando ou em scripts.</span><span class="sxs-lookup"><span data-stu-id="4c214-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="4c214-105">Este guia detalha o uso da CLI do Azure para implantar uma máquina virtual executando o Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="4c214-105">This guide details using the Azure CLI to deploy a virtual machine running Windows Server 2016.</span></span> <span data-ttu-id="4c214-106">Depois que a implantação for concluída, nos conectamos ao servidor e instalamos o IIS.</span><span class="sxs-lookup"><span data-stu-id="4c214-106">Once deployment is complete, we connect to the server and install IIS.</span></span>

<span data-ttu-id="4c214-107">Se você não tiver uma assinatura do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="4c214-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4c214-108">Se você optar por instalar e usar a CLI localmente, este guia de início rápido exigirá a execução da CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="4c214-108">If you choose to install and use the CLI locally, this quickstart requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="4c214-109">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="4c214-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="4c214-110">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="4c214-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="4c214-111">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="4c214-111">Create a resource group</span></span>

<span data-ttu-id="4c214-112">Crie um grupo de recursos com [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="4c214-112">Create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="4c214-113">Um grupo de recursos do Azure é um contêiner lógico no qual os recursos do Azure são implantados e gerenciados.</span><span class="sxs-lookup"><span data-stu-id="4c214-113">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> 

<span data-ttu-id="4c214-114">O exemplo a seguir cria um grupo de recursos chamado *myResourceGroup* no local *eastus*.</span><span class="sxs-lookup"><span data-stu-id="4c214-114">The following example creates a resource group named *myResourceGroup* in the *eastus* location.</span></span>

```azurecli-interactive 
az group create --name myResourceGroup --location eastus
```

## <a name="create-virtual-machine"></a><span data-ttu-id="4c214-115">Criar máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4c214-115">Create virtual machine</span></span>

<span data-ttu-id="4c214-116">Crie uma VM com [az vm create](/cli/azure/vm#create).</span><span class="sxs-lookup"><span data-stu-id="4c214-116">Create a VM with [az vm create](/cli/azure/vm#create).</span></span> 

<span data-ttu-id="4c214-117">O exemplo a seguir cria uma VM chamada *myVM*.</span><span class="sxs-lookup"><span data-stu-id="4c214-117">The following example creates a VM named *myVM*.</span></span> <span data-ttu-id="4c214-118">Este exemplo usa o *azureuser* para um nome de usuário administrativo e *myPassword12* como a senha.</span><span class="sxs-lookup"><span data-stu-id="4c214-118">This example uses *azureuser* for an administrative user name and *myPassword12* as the password.</span></span> <span data-ttu-id="4c214-119">Atualize esses valores para algo apropriado para seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="4c214-119">Update these values to something appropriate to your environment.</span></span> <span data-ttu-id="4c214-120">Esses valores são necessários durante a criação de uma conexão com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4c214-120">These values are needed when creating a connection with the virtual machine.</span></span>

```azurecli-interactive 
az vm create --resource-group myResourceGroup --name myVM --image win2016datacenter --admin-username azureuser --admin-password myPassword12
```

<span data-ttu-id="4c214-121">Quando a VM tiver sido criada, a CLI do Azure mostra informações semelhantes ao exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="4c214-121">When the VM has been created, the Azure CLI shows information similar to the following example.</span></span> <span data-ttu-id="4c214-122">Anote `publicIpAaddress`.</span><span class="sxs-lookup"><span data-stu-id="4c214-122">Take note of the `publicIpAaddress`.</span></span> <span data-ttu-id="4c214-123">Esse endereço é usado para acessar a VM.</span><span class="sxs-lookup"><span data-stu-id="4c214-123">This address is used to access the VM.</span></span>

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

## <a name="open-port-80-for-web-traffic"></a><span data-ttu-id="4c214-124">Abra a porta 80 para tráfego da Web</span><span class="sxs-lookup"><span data-stu-id="4c214-124">Open port 80 for web traffic</span></span> 

<span data-ttu-id="4c214-125">Por padrão, somente as conexões de RDP são permitidas em máquinas virtuais Windows implantadas no Azure.</span><span class="sxs-lookup"><span data-stu-id="4c214-125">By default only RDP connections are allowed in to Windows virtual machines deployed in Azure.</span></span> <span data-ttu-id="4c214-126">Se essa VM for se transformar em um servidor Web, você precisará abrir a porta 80 na Internet.</span><span class="sxs-lookup"><span data-stu-id="4c214-126">If this VM is going to be a webserver, you need to open port 80 from the Internet.</span></span> <span data-ttu-id="4c214-127">Use o comando [az vm open-port](/cli/azure/vm#open-port) para abrir a porta desejada.</span><span class="sxs-lookup"><span data-stu-id="4c214-127">Use the [az vm open-port](/cli/azure/vm#open-port) command to open the desired port.</span></span>  
 
 ```azurecli-interactive  
az vm open-port --port 80 --resource-group myResourceGroup --name myVM
```


## <a name="connect-to-virtual-machine"></a><span data-ttu-id="4c214-128">Conectar-se à máquina virtual</span><span class="sxs-lookup"><span data-stu-id="4c214-128">Connect to virtual machine</span></span>

<span data-ttu-id="4c214-129">Use o seguinte comando para criar uma sessão de área de trabalho remota com a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4c214-129">Use the following command to create a remote desktop session with the virtual machine.</span></span> <span data-ttu-id="4c214-130">Substitua o endereço IP pelo endereço IP público de sua máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4c214-130">Replace the IP address with the public IP address of your virtual machine.</span></span> <span data-ttu-id="4c214-131">Quando solicitado, insira as credenciais usadas ao criar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4c214-131">When prompted, enter the credentials used when creating the virtual machine.</span></span>

```bash 
mstsc /v:<Public IP Address>
```

## <a name="install-iis-using-powershell"></a><span data-ttu-id="4c214-132">Instalar o IIS usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c214-132">Install IIS using PowerShell</span></span>

<span data-ttu-id="4c214-133">Agora que você fez logon na VM do Azure, pode usar uma única linha do PowerShell para instalar o IIS e habilitar a regra de firewall local para permitir o tráfego da Web.</span><span class="sxs-lookup"><span data-stu-id="4c214-133">Now that you have logged in to the Azure VM, you can use a single line of PowerShell to install IIS and enable the local firewall rule to allow web traffic.</span></span> <span data-ttu-id="4c214-134">Abra um promt do PowerShell e execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4c214-134">Open a PowerShell prompt and run the following command:</span></span>

```powershell
Install-WindowsFeature -name Web-Server -IncludeManagementTools
```

## <a name="view-the-iis-welcome-page"></a><span data-ttu-id="4c214-135">Exibir a página de boas-vindas do IIS</span><span class="sxs-lookup"><span data-stu-id="4c214-135">View the IIS welcome page</span></span>

<span data-ttu-id="4c214-136">Com o IIS instalado e a porta 80 que agora está aberta na sua VM da Internet, você pode usar um navegador da Web de sua escolha para exibir a página de boas-vindas do IIS padrão.</span><span class="sxs-lookup"><span data-stu-id="4c214-136">With IIS installed and port 80 now open on your VM from the Internet, you can use a web browser of your choice to view the default IIS welcome page.</span></span> <span data-ttu-id="4c214-137">Certifique-se de usar o endereço IP público que você documentou acima para visitar a página padrão.</span><span class="sxs-lookup"><span data-stu-id="4c214-137">Be sure to use the public IP address you documented above to visit the default page.</span></span> 

![Site do IIS padrão](./media/quick-create-powershell/default-iis-website.png) 

## <a name="clean-up-resources"></a><span data-ttu-id="4c214-139">Limpar recursos</span><span class="sxs-lookup"><span data-stu-id="4c214-139">Clean up resources</span></span>

<span data-ttu-id="4c214-140">Quando não for mais necessário, você pode usar o comando [az group delete](/cli/azure/group#delete) para remover o grupo de recursos, a VM e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="4c214-140">When no longer needed, you can use the [az group delete](/cli/azure/group#delete) command to remove the resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="4c214-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4c214-141">Next steps</span></span>

<span data-ttu-id="4c214-142">Neste início rápido, você implantou uma máquina virtual simples, uma regra de grupo de segurança de rede e instalou um servidor Web.</span><span class="sxs-lookup"><span data-stu-id="4c214-142">In this quick start, you’ve deployed a simple virtual machine, a network security group rule, and installed a web server.</span></span> <span data-ttu-id="4c214-143">Para saber mais sobre máquinas virtuais do Azure, continue o tutorial para VMs do Windows.</span><span class="sxs-lookup"><span data-stu-id="4c214-143">To learn more about Azure virtual machines, continue to the tutorial for Windows VMs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4c214-144">Tutoriais de máquina virtual do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="4c214-144">Azure Windows virtual machine tutorials</span></span>](./tutorial-manage-vm.md)
