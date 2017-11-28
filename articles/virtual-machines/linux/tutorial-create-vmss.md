---
title: "aaaCreate conjuntos de escala de uma máquina Virtual para Linux no Azure | Microsoft Docs"
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
ms.openlocfilehash: 00dd81043f9be46ef2dc6dfe97eefdb20944ee13
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a><span data-ttu-id="eeabc-103">Criar um conjunto de escala de máquina Virtual e implantar um aplicativo altamente disponível no Linux</span><span class="sxs-lookup"><span data-stu-id="eeabc-103">Create a Virtual Machine Scale Set and deploy a highly available app on Linux</span></span>
<span data-ttu-id="eeabc-104">Um conjunto de escala de máquina virtual permite que você toodeploy e gerenciar um conjunto de máquinas virtuais idênticos e o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="eeabc-104">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="eeabc-105">Você pode dimensionar o número de saudação de VMs no conjunto de escala de saudação manualmente ou definir tooautoscale regras com base no uso da CPU, a demanda por memória ou o tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="eeabc-105">You can scale hello number of VMs in hello scale set manually, or define rules tooautoscale based on CPU usage, memory demand, or network traffic.</span></span> <span data-ttu-id="eeabc-106">Neste tutorial, você implantará um conjunto de dimensionamento de máquinas virtuais no Azure.</span><span class="sxs-lookup"><span data-stu-id="eeabc-106">In this tutorial, you deploy a virtual machine scale set in Azure.</span></span> <span data-ttu-id="eeabc-107">Você aprenderá como:</span><span class="sxs-lookup"><span data-stu-id="eeabc-107">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eeabc-108">Use a nuvem init toocreate tooscale um aplicativo</span><span class="sxs-lookup"><span data-stu-id="eeabc-108">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="eeabc-109">Criar um conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="eeabc-109">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="eeabc-110">Aumentar ou diminuir o número de saudação de instâncias em um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="eeabc-110">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="eeabc-111">Exibir informações de conexão para instâncias do conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="eeabc-111">View connection info for scale set instances</span></span>
> * <span data-ttu-id="eeabc-112">Usar discos de dados com conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="eeabc-112">Use data disks in a scale set</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="eeabc-113">Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="eeabc-113">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="eeabc-114">Executar `az --version` toofind versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="eeabc-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="eeabc-115">Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="eeabc-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="scale-set-overview"></a><span data-ttu-id="eeabc-116">Visão geral do conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="eeabc-116">Scale Set overview</span></span>
<span data-ttu-id="eeabc-117">Um conjunto de escala de máquina virtual permite que você toodeploy e gerenciar um conjunto de máquinas virtuais idênticos e o dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="eeabc-117">A virtual machine scale set allows you toodeploy and manage a set of identical, auto-scaling virtual machines.</span></span> <span data-ttu-id="eeabc-118">Escala define use Olá mesmos componentes conforme você aprendeu no tutorial anterior Olá muito[criar VMs altamente disponíveis](tutorial-availability-sets.md).</span><span class="sxs-lookup"><span data-stu-id="eeabc-118">Scale sets use hello same components as you learned about in hello previous tutorial too[Create highly available VMs](tutorial-availability-sets.md).</span></span> <span data-ttu-id="eeabc-119">As VMs em um conjunto de escala são criadas em um conjunto e distribuídas entre domínios de falha e atualização de lógica de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="eeabc-119">VMs in a scale set are created in an availability set and distributed across logic fault and update domains.</span></span>

<span data-ttu-id="eeabc-120">VMs são criadas conforme necessário em um conjunto de escala.</span><span class="sxs-lookup"><span data-stu-id="eeabc-120">VMs are created as needed in a scale set.</span></span> <span data-ttu-id="eeabc-121">Definir toocontrol de regras de dimensionamento automático como e quando as VMs são adicionadas ou removidas do conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="eeabc-121">You define autoscale rules toocontrol how and when VMs are added or removed from hello scale set.</span></span> <span data-ttu-id="eeabc-122">Essas regras podem ser disparados com base em métricas como carga de CPU, utilização de memória ou tráfego de rede.</span><span class="sxs-lookup"><span data-stu-id="eeabc-122">These rules can trigger based on metrics such as CPU load, memory usage, or network traffic.</span></span>

<span data-ttu-id="eeabc-123">Escala define o suporte de too1, 000 VMs quando você usar uma imagem da plataforma Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="eeabc-123">Scale sets support up too1,000 VMs when you use an Azure platform image.</span></span> <span data-ttu-id="eeabc-124">Para cargas de trabalho de produção, você poderá muito[criar uma imagem VM personalizada](tutorial-custom-images.md).</span><span class="sxs-lookup"><span data-stu-id="eeabc-124">For production workloads, you may wish too[Create a custom VM image](tutorial-custom-images.md).</span></span> <span data-ttu-id="eeabc-125">Você pode criar máquinas virtuais de too100 em uma escala definida ao usar uma imagem personalizada.</span><span class="sxs-lookup"><span data-stu-id="eeabc-125">You can create up too100 VMs in a scale set when using a custom image.</span></span>


## <a name="create-an-app-tooscale"></a><span data-ttu-id="eeabc-126">Criar um aplicativo tooscale</span><span class="sxs-lookup"><span data-stu-id="eeabc-126">Create an app tooscale</span></span>
<span data-ttu-id="eeabc-127">Para uso em produção, você poderá muito[criar uma imagem VM personalizada](tutorial-custom-images.md) que inclui o aplicativo instalado e configurado.</span><span class="sxs-lookup"><span data-stu-id="eeabc-127">For production use, you may wish too[Create a custom VM image](tutorial-custom-images.md) that includes your application installed and configured.</span></span> <span data-ttu-id="eeabc-128">Para este tutorial, permite personalizar Olá que VMs na primeira tooquickly de inicialização Consulte uma escala definida em ação.</span><span class="sxs-lookup"><span data-stu-id="eeabc-128">For this tutorial, lets customize hello VMs on first boot tooquickly see a scale set in action.</span></span>

<span data-ttu-id="eeabc-129">Um tutorial anterior, você aprendeu [como toocustomize uma máquina virtual do Linux na primeira inicialização](tutorial-automate-vm-deployment.md) com init de nuvem.</span><span class="sxs-lookup"><span data-stu-id="eeabc-129">In a previous tutorial, you learned [How toocustomize a Linux virtual machine on first boot](tutorial-automate-vm-deployment.md) with cloud-init.</span></span> <span data-ttu-id="eeabc-130">Você pode usar Olá tooinstall de arquivo de configuração de nuvem init mesmo NGINX e executar um aplicativo simples do 'Hello World' Node. js.</span><span class="sxs-lookup"><span data-stu-id="eeabc-130">You can use hello same cloud-init configuration file tooinstall NGINX and run a simple 'Hello World' Node.js app.</span></span> 

<span data-ttu-id="eeabc-131">No shell atual, crie um arquivo chamado *init.txt nuvem* e colar Olá seguinte configuração.</span><span class="sxs-lookup"><span data-stu-id="eeabc-131">In your current shell, create a file named *cloud-init.txt* and paste hello following configuration.</span></span> <span data-ttu-id="eeabc-132">Por exemplo, crie o arquivo de saudação no hello nuvem Shell não está no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="eeabc-132">For example, create hello file in hello Cloud Shell not on your local machine.</span></span> <span data-ttu-id="eeabc-133">Digite `sensible-editor cloud-init.txt` toocreate Olá arquivo e ver uma lista de editores disponíveis.</span><span class="sxs-lookup"><span data-stu-id="eeabc-133">Enter `sensible-editor cloud-init.txt` toocreate hello file and see a list of available editors.</span></span> <span data-ttu-id="eeabc-134">Verifique se que esse arquivo de inicialização de nuvem inteiro Olá foi copiado corretamente, Olá especialmente a primeira linha:</span><span class="sxs-lookup"><span data-stu-id="eeabc-134">Make sure that hello whole cloud-init file is copied correctly, especially hello first line:</span></span>

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


## <a name="create-a-scale-set"></a><span data-ttu-id="eeabc-135">Criar um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="eeabc-135">Create a scale set</span></span>
<span data-ttu-id="eeabc-136">Antes de criar uma máquina virtual, crie um grupo de recursos com o [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="eeabc-136">Before you can create a scale set, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="eeabc-137">Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupScaleSet* em Olá *eastus* local:</span><span class="sxs-lookup"><span data-stu-id="eeabc-137">hello following example creates a resource group named *myResourceGroupScaleSet* in hello *eastus* location:</span></span>

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

<span data-ttu-id="eeabc-138">Crie um conjunto de dimensionamento de máquinas virtuais com [az vmss create](/cli/azure/vmss#create).</span><span class="sxs-lookup"><span data-stu-id="eeabc-138">Now create a virtual machine scale set with [az vmss create](/cli/azure/vmss#create).</span></span> <span data-ttu-id="eeabc-139">Olá, exemplo a seguir cria uma conjunto nomeada de escalas *myScaleSet*usa Olá nuvem init arquivo toocustomize Olá VM e gera chaves SSH se não existirem:</span><span class="sxs-lookup"><span data-stu-id="eeabc-139">hello following example creates a scale set named *myScaleSet*, uses hello cloud-init file toocustomize hello VM, and generates SSH keys if they do not exist:</span></span>

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

<span data-ttu-id="eeabc-140">Ele usa toocreate de alguns minutos e configurar todos os recursos de conjunto de escala hello e máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="eeabc-140">It takes a few minutes toocreate and configure all hello scale set resources and VMs.</span></span> <span data-ttu-id="eeabc-141">Há tarefas em segundo plano que continuam toorun depois Olá CLI do Azure retorna toohello prompt.</span><span class="sxs-lookup"><span data-stu-id="eeabc-141">There are background tasks that continue toorun after hello Azure CLI returns you toohello prompt.</span></span> <span data-ttu-id="eeabc-142">Pode ser outro alguns minutos antes de poder acessar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="eeabc-142">It may be another couple of minutes before you can access hello app.</span></span>


## <a name="allow-web-traffic"></a><span data-ttu-id="eeabc-143">Permitir o tráfego da web</span><span class="sxs-lookup"><span data-stu-id="eeabc-143">Allow web traffic</span></span>
<span data-ttu-id="eeabc-144">Um balanceador de carga foi criado automaticamente como parte do conjunto de escalas da máquina virtual hello.</span><span class="sxs-lookup"><span data-stu-id="eeabc-144">A load balancer was created automatically as part of hello virtual machine scale set.</span></span> <span data-ttu-id="eeabc-145">o balanceador de carga Olá distribui o tráfego entre um conjunto de VMs definidos usando regras de Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="eeabc-145">hello load balancer distributes traffic across a set of defined VMs using load balancer rules.</span></span> <span data-ttu-id="eeabc-146">Você pode aprender mais sobre conceitos de Balanceador de carga e a configuração no tutorial de Avançar hello, [como tooload equilibrar as máquinas virtuais no Azure](tutorial-load-balancer.md).</span><span class="sxs-lookup"><span data-stu-id="eeabc-146">You can learn more about load balancer concepts and configuration in hello next tutorial, [How tooload balance virtual machines in Azure](tutorial-load-balancer.md).</span></span>

<span data-ttu-id="eeabc-147">tooallow tráfego tooreach Olá web app, crie uma regra com [criar regra de balanceamento de carga de rede az](/cli/azure/network/lb/rule#create).</span><span class="sxs-lookup"><span data-stu-id="eeabc-147">tooallow traffic tooreach hello web app, create a rule with [az network lb rule create](/cli/azure/network/lb/rule#create).</span></span> <span data-ttu-id="eeabc-148">Olá, exemplo a seguir cria uma regra denominada *myLoadBalancerRuleWeb*:</span><span class="sxs-lookup"><span data-stu-id="eeabc-148">hello following example creates a rule named *myLoadBalancerRuleWeb*:</span></span>

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

## <a name="test-your-app"></a><span data-ttu-id="eeabc-149">Testar seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="eeabc-149">Test your app</span></span>
<span data-ttu-id="eeabc-150">toosee seu aplicativo Node. js na web hello, obter o endereço IP público de saudação do balanceador de carga com [az rede ip público exibir](/cli/azure/network/public-ip#show).</span><span class="sxs-lookup"><span data-stu-id="eeabc-150">toosee your Node.js app on hello web, obtain hello public IP address of your load balancer with [az network public-ip show](/cli/azure/network/public-ip#show).</span></span> <span data-ttu-id="eeabc-151">Olá, exemplo a seguir obtém endereço IP hello *myScaleSetLBPublicIP* criado como parte do conjunto de escala hello:</span><span class="sxs-lookup"><span data-stu-id="eeabc-151">hello following example obtains hello IP address for *myScaleSetLBPublicIP* created as part of hello scale set:</span></span>

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

<span data-ttu-id="eeabc-152">Insira o endereço IP público de saudação no navegador da web de tooa.</span><span class="sxs-lookup"><span data-stu-id="eeabc-152">Enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="eeabc-153">aplicativo Hello é exibido, incluindo o nome de host de saudação do hello VM que Olá a carga do tráfego do balanceador distribuída para:</span><span class="sxs-lookup"><span data-stu-id="eeabc-153">hello app is displayed, including hello hostname of hello VM that hello load balancer distributed traffic to:</span></span>

![Executar o aplicativo Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

<span data-ttu-id="eeabc-155">a escala de saudação toosee definida em ação, você pode forçar atualização sua carga de saudação do toosee de navegador da web balanceador distribuir o tráfego entre todas as VMs Olá executando o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eeabc-155">toosee hello scale set in action, you can force-refresh your web browser toosee hello load balancer distribute traffic across all hello VMs running your app.</span></span>


## <a name="management-tasks"></a><span data-ttu-id="eeabc-156">Tarefas de gerenciamento</span><span class="sxs-lookup"><span data-stu-id="eeabc-156">Management tasks</span></span>
<span data-ttu-id="eeabc-157">Ciclo de vida de saudação do conjunto de escala hello, talvez seja necessário toorun uma ou mais tarefas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="eeabc-157">Throughout hello lifecycle of hello scale set, you may need toorun one or more management tasks.</span></span> <span data-ttu-id="eeabc-158">Além disso, talvez você queira toocreate scripts que automatizam várias tarefas de ciclo de vida.</span><span class="sxs-lookup"><span data-stu-id="eeabc-158">Additionally, you may want toocreate scripts that automate various lifecycle-tasks.</span></span> <span data-ttu-id="eeabc-159">Olá 2.0 do CLI do Azure fornece uma maneira rápida de toodo essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="eeabc-159">hello Azure CLI 2.0 provides a quick way toodo those tasks.</span></span> <span data-ttu-id="eeabc-160">Estas são algumas tarefas comuns.</span><span class="sxs-lookup"><span data-stu-id="eeabc-160">Here are a few common tasks.</span></span>

### <a name="view-vms-in-a-scale-set"></a><span data-ttu-id="eeabc-161">Exibição de VMs em um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="eeabc-161">View VMs in a scale set</span></span>
<span data-ttu-id="eeabc-162">uma lista de VMs em execução em escala de seu conjunto de tooview, use [instâncias de lista az vmss](/cli/azure/vmss#list-instances) da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="eeabc-162">tooview a list of VMs running in your scale set, use [az vmss list-instances](/cli/azure/vmss#list-instances) as follows:</span></span>

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

<span data-ttu-id="eeabc-163">saudação de saída é similar toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="eeabc-163">hello output is similar toohello following example:</span></span>

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a><span data-ttu-id="eeabc-164">Aumentar ou diminuir as instâncias de VM</span><span class="sxs-lookup"><span data-stu-id="eeabc-164">Increase or decrease VM instances</span></span>
<span data-ttu-id="eeabc-165">toosee Olá número de instâncias atualmente têm em uma escala de definido, use [Mostrar de vmss az](/cli/azure/vmss#show) e consultar *sku.capacity*:</span><span class="sxs-lookup"><span data-stu-id="eeabc-165">toosee hello number of instances you currently have in a scale set, use [az vmss show](/cli/azure/vmss#show) and query on *sku.capacity*:</span></span>

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

<span data-ttu-id="eeabc-166">Você pode, em seguida, manualmente aumentar ou diminuir Olá número de máquinas virtuais em escala Olá com [escala de vmss az](/cli/azure/vmss#scale).</span><span class="sxs-lookup"><span data-stu-id="eeabc-166">You can then manually increase or decrease hello number of virtual machines in hello scale set with [az vmss scale](/cli/azure/vmss#scale).</span></span> <span data-ttu-id="eeabc-167">Olá exemplo a seguir define Olá número de VMs em sua escala definida muito*5*:</span><span class="sxs-lookup"><span data-stu-id="eeabc-167">hello following example sets hello number of VMs in your scale set too*5*:</span></span>

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

<span data-ttu-id="eeabc-168">Regras de dimensionamento automático permitem que você defina como tooscale para cima ou para baixo número de saudação de VMs em sua escala é definida na resposta toodemand como tráfego de rede ou o uso da CPU.</span><span class="sxs-lookup"><span data-stu-id="eeabc-168">Autoscale rules let you define how tooscale up or down hello number of VMs in your scale set in response toodemand such as network traffic or CPU usage.</span></span> <span data-ttu-id="eeabc-169">Atualmente, essas regras não podem ser definidas na CLI 2.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="eeabc-169">Currently, these rules cannot be set in Azure CLI 2.0.</span></span> <span data-ttu-id="eeabc-170">Saudação de uso [portal do Azure](https://portal.azure.com) tooconfigure AutoEscala.</span><span class="sxs-lookup"><span data-stu-id="eeabc-170">Use hello [Azure portal](https://portal.azure.com) tooconfigure autoscale.</span></span>

### <a name="get-connection-info"></a><span data-ttu-id="eeabc-171">Obter informações de conexão</span><span class="sxs-lookup"><span data-stu-id="eeabc-171">Get connection info</span></span>
<span data-ttu-id="eeabc-172">informações de conexão tooobtain sobre Olá VMs em seus conjuntos de escala, use [az vmss lista--conexão-informações da instância](/cli/azure/vmss#list-instance-connection-info).</span><span class="sxs-lookup"><span data-stu-id="eeabc-172">tooobtain connection information about hello VMs in your scale sets, use [az vmss list-instance-connection-info](/cli/azure/vmss#list-instance-connection-info).</span></span> <span data-ttu-id="eeabc-173">Este comando gera o endereço IP público de saudação e a porta para cada VM que permite que você tooconnect com SSH:</span><span class="sxs-lookup"><span data-stu-id="eeabc-173">This command outputs hello public IP address and port for each VM that allows you tooconnect with SSH:</span></span>

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a><span data-ttu-id="eeabc-174">Usar discos de dados com conjuntos de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="eeabc-174">Use data disks with scale sets</span></span>
<span data-ttu-id="eeabc-175">Você pode criar e usar discos de dados com conjuntos de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="eeabc-175">You can create and use data disks with scale sets.</span></span> <span data-ttu-id="eeabc-176">Um tutorial anterior, você aprendeu como muito[discos do Azure gerenciar](tutorial-manage-disks.md) que descreve Olá práticas recomendadas e melhorias de desempenho para a criação de aplicativos em discos de dados em vez de disco Olá sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="eeabc-176">In a previous tutorial, you learned how too[Manage Azure disks](tutorial-manage-disks.md) that outlines hello best practices and performance improvements for building apps on data disks rather than hello OS disk.</span></span>

### <a name="create-scale-set-with-data-disks"></a><span data-ttu-id="eeabc-177">Criar conjunto de dimensionamento com discos de dados</span><span class="sxs-lookup"><span data-stu-id="eeabc-177">Create scale set with data disks</span></span>
<span data-ttu-id="eeabc-178">toocreate uma escala definida e anexar discos de dados, adicionar Olá `--data-disk-sizes-gb` parâmetro toohello [vmss az criar](/cli/azure/vmss#create) comando.</span><span class="sxs-lookup"><span data-stu-id="eeabc-178">toocreate a scale set and attach data disks, add hello `--data-disk-sizes-gb` parameter toohello [az vmss create](/cli/azure/vmss#create) command.</span></span> <span data-ttu-id="eeabc-179">Olá, exemplo a seguir cria uma escala com *50*Gb discos de dados anexado tooeach instância:</span><span class="sxs-lookup"><span data-stu-id="eeabc-179">hello following example creates a scale set with *50*Gb data disks attached tooeach instance:</span></span>

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

<span data-ttu-id="eeabc-180">Quando as instâncias são removidas de um conjunto de dimensionamento, todos os discos de dados anexados também são removidos.</span><span class="sxs-lookup"><span data-stu-id="eeabc-180">When instances are removed from a scale set, any attached data disks are also removed.</span></span>

### <a name="add-data-disks"></a><span data-ttu-id="eeabc-181">Adicionar discos de dados</span><span class="sxs-lookup"><span data-stu-id="eeabc-181">Add data disks</span></span>
<span data-ttu-id="eeabc-182">tooadd um tooinstances de disco de dados em sua escala definida, use [anexar disco de vmss az](/cli/azure/vmss/disk#attach).</span><span class="sxs-lookup"><span data-stu-id="eeabc-182">tooadd a data disk tooinstances in your scale set, use [az vmss disk attach](/cli/azure/vmss/disk#attach).</span></span> <span data-ttu-id="eeabc-183">Olá exemplo a seguir adiciona uma *50*instância de tooeach disco Gb:</span><span class="sxs-lookup"><span data-stu-id="eeabc-183">hello following example adds a *50*Gb disk tooeach instance:</span></span>

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a><span data-ttu-id="eeabc-184">Desanexar discos de dados</span><span class="sxs-lookup"><span data-stu-id="eeabc-184">Detach data disks</span></span>
<span data-ttu-id="eeabc-185">tooremove um tooinstances de disco de dados em sua escala definida, use [desanexar disco de vmss az](/cli/azure/vmss/disk#detach).</span><span class="sxs-lookup"><span data-stu-id="eeabc-185">tooremove a data disk tooinstances in your scale set, use [az vmss disk detach](/cli/azure/vmss/disk#detach).</span></span> <span data-ttu-id="eeabc-186">Olá, exemplo a seguir remove Olá disco de dados no LUN *2* de cada instância de:</span><span class="sxs-lookup"><span data-stu-id="eeabc-186">hello following example removes hello data disk at LUN *2* from each instance:</span></span>

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a><span data-ttu-id="eeabc-187">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="eeabc-187">Next steps</span></span>
<span data-ttu-id="eeabc-188">Neste tutorial, você criou um conjunto de dimensionamento de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="eeabc-188">In this tutorial, you created a virtual machine scale set.</span></span> <span data-ttu-id="eeabc-189">Você aprendeu como:</span><span class="sxs-lookup"><span data-stu-id="eeabc-189">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eeabc-190">Use a nuvem init toocreate tooscale um aplicativo</span><span class="sxs-lookup"><span data-stu-id="eeabc-190">Use cloud-init toocreate an app tooscale</span></span>
> * <span data-ttu-id="eeabc-191">Criar um conjunto de dimensionamento de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="eeabc-191">Create a virtual machine scale set</span></span>
> * <span data-ttu-id="eeabc-192">Aumentar ou diminuir o número de saudação de instâncias em um conjunto de escala</span><span class="sxs-lookup"><span data-stu-id="eeabc-192">Increase or decrease hello number of instances in a scale set</span></span>
> * <span data-ttu-id="eeabc-193">Exibir informações de conexão para instâncias do conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="eeabc-193">View connection info for scale set instances</span></span>
> * <span data-ttu-id="eeabc-194">Usar discos de dados com conjunto de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="eeabc-194">Use data disks in a scale set</span></span>

<span data-ttu-id="eeabc-195">Toohello toolearn de tutorial Avançar adiantar mais sobre conceitos para máquinas virtuais de balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="eeabc-195">Advance toohello next tutorial toolearn more about load balancing concepts for virtual machines.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="eeabc-196">Balancear carga de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="eeabc-196">Load balance virtual machines</span></span>](tutorial-load-balancer.md)