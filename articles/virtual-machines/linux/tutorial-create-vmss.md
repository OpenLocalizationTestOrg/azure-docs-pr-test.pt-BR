---
title: "Criar um conjunto de escala de máquina Virtual para Linux no Azure | Documentos do Microsoft"
description: "Criar e implantar um aplicativo em VMs do Linux usando um conjunto de escala de máquina virtual altamente disponível"
services: virtual-machine-scale-sets
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
tags: 
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 08/11/2017
ms.author: iainfou
ms.openlocfilehash: 2b8d519e11f70eda164bd8f6e131a3989f242ab0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="8d3d0-103">Criar um conjunto de escala de máquina Virtual e implantar um aplicativo altamente disponível no Linux</span><span class="sxs-lookup"><span data-stu-id="8d3d0-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="8d3d0-104">Um conjunto de dimensionamento de máquinas virtuais permite implantar e gerenciar um conjunto de máquinas virtuais idênticas de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-104">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="8d3d0-105">Você pode dimensionar o número de VMs no conjunto de escala manualmente ou definir regras para dimensionamento automático com base no uso da CPU, a demanda por memória ou tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-105">You can scale the number of VMs in the scale set manually, or define rules to autoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="8d3d0-106">Neste tutorial, você implantará um conjunto de dimensionamento de máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="8d3d0-107">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8d3d0-108">Usar cloud-init para criar um aplicativo para escala</span><span class="sxs-lookup"><span data-stu-id="8d3d0-108">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="8d3d0-109">Criar um conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="8d3d0-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="8d3d0-110">Aumentar ou diminuir o número de instâncias em um conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="8d3d0-110">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="8d3d0-111">Exibir informações de conexão para instâncias do conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="8d3d0-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="8d3d0-112">Usar discos de dados com conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="8d3d0-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8d3d0-113">Se você optar por instalar e usar a CLI localmente, este tutorial exigirá que você execute a CLI do Azure versão 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-113">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8d3d0-114">Execute `az --version` para encontrar a versão.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="8d3d0-115">Se você precisa instalar ou atualizar, consulte [Instalar a CLI 2.0 do Azure]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8d3d0-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="8d3d0-116">Visão geral do conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="8d3d0-116">Scale Set overview</span></span>
<span data-ttu-id="8d3d0-117">Um conjunto de dimensionamento de máquinas virtuais permite implantar e gerenciar um conjunto de máquinas virtuais idênticas de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-117">A virtual machine scale set allows you to deploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="8d3d0-118">Conjuntos de escala usam os mesmos componentes que você aprendeu no tutorial anterior para [criar máquinas virtuais altamente disponíveis](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="8d3d0-118">Scale sets use the same components as you learned about in the previous tutorial to [Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="8d3d0-119">As VMs em um conjunto de escala são criadas em um conjunto e distribuídas entre domínios de falha e atualização de lógica de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="8d3d0-120">VMs são criadas conforme necessário em um conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="8d3d0-121">Você define regras de dimensionamento automático para controlar como e quando as VMs são adicionadas ou removidas do conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-121">You define autoscale rules to control how and when VMs are added or removed from the scale set.</span></span> <span data-ttu-id="8d3d0-122">Essas regras podem ser disparados com base em métricas como carga de CPU, utilização de memória ou tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="8d3d0-123">Escala define suporte até 1.000 VMs quando você usar uma imagem da plataforma Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-123">Scale sets support up to 1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="8d3d0-124">Para cargas de trabalho de produção, convém [criar uma imagem VM personalizada](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="8d3d0-124">For production workloads, you may wish to [Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="8d3d0-125">Você pode criar até 100 VMs em uma escala definida ao usar uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-125">You can create up to 100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-to-scale"></a><span data-ttu-id="8d3d0-126">Criar um aplicativo para escala</span><span class="sxs-lookup"><span data-stu-id="8d3d0-126">Create an app to scale</span></span>
<span data-ttu-id="8d3d0-127">Para uso em produção, você poderá [criar uma imagem VM personalizada](tutorial-custom-images.md) que inclui o aplicativo instalado e configurado.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-127">For production use, you may wish to [Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="8d3d0-128">Para este tutorial, permite personalizar as VMs na primeira inicialização para ver rapidamente uma escala definida em ação.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-128">For this tutorial, lets customize the VMs on first boot to quickly see a scale set in action.</span></span>

<span data-ttu-id="8d3d0-129">Um tutorial anterior, você aprendeu [como personalizar uma máquina virtual de Linux na primeira inicialização](tutorial-automate-vm-deployment.md) com cloud-init.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-129">In a previous tutorial, you learned [How to customize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="8d3d0-130">Você pode utilizar o mesmo arquivo de configuração de inicialização de nuvem para instalar o NGINX e executar um aplicativo simples do Node. js 'Hello, World'.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-130">You can use the same cloud-init configuration file to install NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="8d3d0-131">No shell atual, crie um arquivo chamado *cloud-init.txt* e cole a configuração a seguir.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-131">In your current shell, create a file named *cloud-init.txt* and paste the following configuration.</span></span> <span data-ttu-id="8d3d0-132">Por exemplo, crie o arquivo no Cloud Shell e não em seu computador local.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-132">For example, create the file in the Cloud Shell not on your local machine.</span></span> <span data-ttu-id="8d3d0-133">Insira `sensible-editor cloud-init.txt` para criar o arquivo e ver uma lista de editores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-133">Enter `sensible-editor cloud-init.txt` to create the file and see a list of available editors.</span></span> <span data-ttu-id="8d3d0-134">Certifique-se de que o arquivo de inicialização de nuvem inteiro seja copiado corretamente, especialmente a primeira linha:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-134">Make sure that the whole cloud-init file is copied correctly, especially the first line:</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
  - nodejs
  - npm
write_files:
  - owner: www-data:www-data
  - path: /etc/nginx/sites-available/default
    content: |
      server {
        listen 80;
        location / {
          proxy_pass http://localhost:3000;
          proxy_http_version 1.1;
          proxy_set_header Upgrade $http_upgrade;
          proxy_set_header Connection keep-alive;
          proxy_set_header Host $host;
          proxy_cache_bypass $http_upgrade;
        }
      }
  - owner: azureuser:azureuser
  - path: /home/azureuser/myapp/index.js
    content: |
      var express = require('express')
      var app = express()
      var os = require('os');
      app.get('/', function (req, res) {
        res.send('Hello World from host ' + os.hostname() + '!')
      })
      app.listen(3000, function () {
        console.log('Hello world app listening on port 3000!')
      })
runcmd:
  - service nginx restart
  - cd "/home/azureuser/myapp"
  - npm init
  - npm install express -y
  - nodejs index.js
```


## <a name="create-a-scale-set"></a><span data-ttu-id="8d3d0-135">Criar um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="8d3d0-135">Create a scale set</span></span>
<span data-ttu-id="8d3d0-136">Antes de criar uma máquina virtual, crie um grupo de recursos com o [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8d3d0-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8d3d0-137">O seguinte exemplo cria um grupo de recursos chamado *myResourceGroupScaleSet* no local *eastus*:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-137">The following example creates a resource group named *myResourceGroupScaleSet* in the *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="8d3d0-138">Crie um conjunto de dimensionamento de máquinas virtuais com [az vmss create](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="8d3d0-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="8d3d0-139">O exemplo a seguir cria uma conjunto nomeada de escala *myScaleSet*, usa o arquivo de nuvem-int para personalizar a VM e gera chaves SSH, se não existirem:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-139">The following example creates a scale set named *myScaleSet*, uses the cloud-init file to customize the VM, and generates SSH keys if they do not exist:</span></span>

```azurecli-interactive 
az vmss create \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --image UbuntuLTS \
  --upgrade-policy-mode automatic \
  --custom-data cloud-init.txt \
  --admin-username azureuser \
  --generate-ssh-keys      
```

<span data-ttu-id="8d3d0-140">Leva alguns minutos para criar e configurar todos os recursos e as VMs do conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-140">It takes a few minutes to create and configure all the scale set resources and VMs.</span></span> <span data-ttu-id="8d3d0-141">Há tarefas em segundo plano que continuarão em execução depois que a CLI do Azure faz você voltar para o prompt.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-141">There are background tasks that continue to run after the Azure CLI returns you to the prompt.</span></span> <span data-ttu-id="8d3d0-142">Pode demorar mais alguns minutos antes que você possa acessar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-142">It may be another couple of minutes before you can access the app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="8d3d0-143">Permitir o tráfego da web</span><span class="sxs-lookup"><span data-stu-id="8d3d0-143">Allow web traffic</span></span>
<span data-ttu-id="8d3d0-144">Um balanceador de carga foi criado automaticamente como parte do conjunto de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-144">A load balancer was created automatically as part of the virtual machine scale set.</span></span> <span data-ttu-id="8d3d0-145">O balanceador de carga distribui o tráfego entre um conjunto de VMs definidas usando regras do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-145">The load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="8d3d0-146">Você pode aprender mais sobre conceitos de Balanceador de carga e a configuração no próximo tutorial, [como carga de máquinas virtuais de saldo no Azure](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="8d3d0-146">You can learn more about load balancer concepts and configuration in the next tutorial, [How to load balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="8d3d0-147">Para permitir o tráfego acessar o aplicativo web, crie uma regra com [criar regra de balanceamento de carga de rede az](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="8d3d0-147">To allow traffic to reach the web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="8d3d0-148">O exemplo a seguir cria uma regra chamada *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-148">The following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

```azurecli-interactive 
az network lb rule create \
  --resource-group myResourceGroupScaleSet \
  --name myLoadBalancerRuleWeb \
  --lb-name myScaleSetLB \
  --backend-pool-name myScaleSetLBBEPool \
  --backend-port 80 \
  --frontend-ip-name loadBalancerFrontEnd \
  --frontend-port 80 \
  --protocol tcp
```

## <a name="test-your-app"></a><span data-ttu-id="8d3d0-149">Testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="8d3d0-149">Test your app</span></span>
<span data-ttu-id="8d3d0-150">Para ver seu aplicativo Node. js na web, obter o endereço IP público de sua balanceador de carga com [az rede ip público exibir](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="8d3d0-150">To see your Node.js app on the web, obtain the public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="8d3d0-151">O seguinte exemplo obtém o endereço IP de *myScaleSetLBPublicIP*, criado como parte do conjunto de dimensionamento:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-151">The following example obtains the IP address for *myScaleSetLBPublicIP* created as part of the scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="8d3d0-152">Insira o endereço IP público em um navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-152">Enter the public IP address in to a web browser.</span></span> <span data-ttu-id="8d3d0-153">O aplicativo é exibido, incluindo o nome do host da VM para a qual o balanceador de carga distribui o tráfego:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-153">The app is displayed, including the hostname of the VM that the load balancer distributed traffic to:</span></span>

![Executar o aplicativo Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="8d3d0-155">Para ver a escala definida em ação, você pode forçar atualização seu navegador da web para ver o balanceador de carga distribuir tráfego entre todas as VMs que executam seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-155">To see the scale set in action, you can force-refresh your web browser to see the load balancer distribute traffic across all the VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="8d3d0-156">Tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="8d3d0-156">Management tasks</span></span>
<span data-ttu-id="8d3d0-157">Durante todo o ciclo de vida do conjunto de dimensionamento, você poderá precisar executar uma ou mais tarefas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-157">Throughout the lifecycle of the scale set, you may need to run one or more management tasks.</span></span> <span data-ttu-id="8d3d0-158">Além disso, talvez você deseje criar scripts que automatizam várias tarefas do ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-158">Additionally, you may want to create scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="8d3d0-159">A CLI 2.0 do Azure fornece uma maneira rápida de realizar essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-159">The Azure CLI 2.0 provides a quick way to do those tasks.</span></span> <span data-ttu-id="8d3d0-160">Estas são algumas tarefas comuns.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="8d3d0-161">Exibição de VMs em um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="8d3d0-161">View VMs in a scale set</span></span>
<span data-ttu-id="8d3d0-162">Para exibir uma lista de VMs em execução no seu conjunto de escala, use [instâncias de lista az vmss](/cli/azure/vmss#list-instances) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-162">To view a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="8d3d0-163">A saída deverá ser semelhante ao seguinte exemplo:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-163">The output is similar to the following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="8d3d0-164">Aumentar ou diminuir as instâncias de VM</span><span class="sxs-lookup"><span data-stu-id="8d3d0-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="8d3d0-165">Para ver o número de instâncias que você fez em um conjunto de escala, use [az vmss show](/cli/azure/vmss#show) e consulte *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-165">To see the number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="8d3d0-166">Manualmente, é possível aumentar ou diminuir o número de máquinas virtuais no conjunto de dimensionamento com [az vmss scale](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="8d3d0-166">You can then manually increase or decrease the number of virtual machines in the scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="8d3d0-167">O seguinte exemplo aumenta o número de VMs no conjunto de dimensionamento para *5*:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-167">The following example sets the number of VMs in your scale set to *5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="8d3d0-168">As regras de dimensionamento automático permitem definir como escalar e reduzir verticalmente o número de VMs no conjunto de dimensionamento em resposta à demanda, como tráfego de rede ou uso da CPU.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-168">Autoscale rules let you define how to scale up or down the number of VMs in your scale set in response to demand such as network traffic or CPU usage.</span></span> <span data-ttu-id="8d3d0-169">Atualmente, essas regras não podem ser definidas na CLI 2.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="8d3d0-170">Use o [portal do Azure](https://portal.azure.com) para configurar o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-170">Use the [Azure portal](https://portal.azure.com) to configure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="8d3d0-171">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="8d3d0-171">Get connection info</span></span>
<span data-ttu-id="8d3d0-172">Para obter informações de conexão sobre as VMs nos conjuntos de dimensionamento, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="8d3d0-172">To obtain connection information about the VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="8d3d0-173">Esse comando gera o endereço IP público e as portas para cada VM que permite a conexão com o SSH:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-173">This command outputs the public IP address and port for each VM that allows you to connect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="8d3d0-174">Usar discos de dados com conjuntos de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="8d3d0-174">Use data disks with scale sets</span></span>
<span data-ttu-id="8d3d0-175">Você pode criar e usar discos de dados com conjuntos de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="8d3d0-176">Em um tutorial anterior, você aprendeu como [Gerenciar discos do Azure](tutorial-manage-disks.md) que descreve as práticas recomendadas e as melhorias de desempenho para a criação de aplicativos em discos de dados, em vez do disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-176">In a previous tutorial, you learned how to [Manage Azure disks](tutorial-manage-disks.md) that outlines the best practices and performance improvements for building apps on data disks rather than the OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="8d3d0-177">Criar conjunto de dimensionamento com discos de dados</span><span class="sxs-lookup"><span data-stu-id="8d3d0-177">Create scale set with data disks</span></span>
<span data-ttu-id="8d3d0-178">Para criar um conjunto de dimensionamento e anexar discos de dados, adicione o parâmetro `--data-disk-sizes-gb` ao comando [az vmss create](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="8d3d0-178">To create a scale set and attach data disks, add the `--data-disk-sizes-gb` parameter to the [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="8d3d0-179">O exemplo a seguir cria um conjunto de dimensionamento com discos de dados de *50*Gb anexados a cada instância:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-179">The following example creates a scale set with *50*Gb data disks attached to each instance:</span></span>

```azurecli-interactive 
az vmss create \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetDisks \
    --image UbuntuLTS \
    --upgrade-policy-mode automatic \
    --custom-data cloud-init.txt \
    --admin-username azureuser \
    --generate-ssh-keys \
    --data-disk-sizes-gb 50
```

<span data-ttu-id="8d3d0-180">Quando as instâncias são removidas de um conjunto de dimensionamento, todos os discos de dados anexados também são removidos.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="8d3d0-181">Adicionar discos de dados</span><span class="sxs-lookup"><span data-stu-id="8d3d0-181">Add data disks</span></span>
<span data-ttu-id="8d3d0-182">Para adicionar um disco de dados a instâncias no conjunto de dimensionamento, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="8d3d0-182">To add a data disk to instances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="8d3d0-183">O exemplo a seguir adiciona um disco de *50*Gb a cada instância:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-183">The following example adds a *50*Gb disk to each instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="8d3d0-184">Desanexar discos de dados</span><span class="sxs-lookup"><span data-stu-id="8d3d0-184">Detach data disks</span></span>
<span data-ttu-id="8d3d0-185">Para remover um disco de dados para instâncias no conjunto de dimensionamento, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="8d3d0-185">To remove a data disk to instances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="8d3d0-186">O exemplo a seguir remove o disco de dados no LUN *2* de cada instância:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-186">The following example removes the data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="8d3d0-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8d3d0-187">Next steps</span></span>
<span data-ttu-id="8d3d0-188">Neste tutorial, você criou um conjunto de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="8d3d0-189">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="8d3d0-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8d3d0-190">Usar cloud-init para criar um aplicativo para escala</span><span class="sxs-lookup"><span data-stu-id="8d3d0-190">Use cloud-init to create an app to scale</span></span>
> * <span data-ttu-id="8d3d0-191">Criar um conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="8d3d0-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="8d3d0-192">Aumentar ou diminuir o número de instâncias em um conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="8d3d0-192">Increase or decrease the number of instances in a scale set</span></span>
> * <span data-ttu-id="8d3d0-193">Exibir informações de conexão para instâncias do conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="8d3d0-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="8d3d0-194">Usar discos de dados com conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="8d3d0-194">Use data disks in a scale set</span></span>

<span data-ttu-id="8d3d0-195">Avança para o próximo tutorial para saber mais sobre conceitos de máquinas virtuais de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="8d3d0-195">Advance to the next tutorial to learn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8d3d0-196">Balancear carga de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="8d3d0-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)