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
# <a name="create-a-virtual-machine-scale-set-and-deploy-a-highly-available-app-on-linux"></a>Criar um conjunto de escala de máquina Virtual e implantar um aplicativo altamente disponível no Linux
Um conjunto de escala de máquina virtual permite que você toodeploy e gerenciar um conjunto de máquinas virtuais idênticos e o dimensionamento automático. Você pode dimensionar o número de saudação de VMs no conjunto de escala de saudação manualmente ou definir tooautoscale regras com base no uso da CPU, a demanda por memória ou o tráfego de rede. Neste tutorial, você implantará um conjunto de dimensionamento de máquinas virtuais no Azure. Você aprenderá como:

> [!div class="checklist"]
> * Use a nuvem init toocreate tooscale um aplicativo
> * Criar um conjunto de dimensionamento de máquinas virtuais
> * Aumentar ou diminuir o número de saudação de instâncias em um conjunto de escala
> * Exibir informações de conexão para instâncias do conjunto de dimensionamento
> * Usar discos de dados com conjunto de dimensionamento


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="scale-set-overview"></a>Visão geral do conjunto de escala
Um conjunto de escala de máquina virtual permite que você toodeploy e gerenciar um conjunto de máquinas virtuais idênticos e o dimensionamento automático. Escala define use Olá mesmos componentes conforme você aprendeu no tutorial anterior Olá muito[criar VMs altamente disponíveis](tutorial-availability-sets.md). As VMs em um conjunto de escala são criadas em um conjunto e distribuídas entre domínios de falha e atualização de lógica de disponibilidade.

VMs são criadas conforme necessário em um conjunto de escala. Definir toocontrol de regras de dimensionamento automático como e quando as VMs são adicionadas ou removidas do conjunto de escala de saudação. Essas regras podem ser disparados com base em métricas como carga de CPU, utilização de memória ou tráfego de rede.

Escala define o suporte de too1, 000 VMs quando você usar uma imagem da plataforma Windows Azure. Para cargas de trabalho de produção, você poderá muito[criar uma imagem VM personalizada](tutorial-custom-images.md). Você pode criar máquinas virtuais de too100 em uma escala definida ao usar uma imagem personalizada.


## <a name="create-an-app-tooscale"></a>Criar um aplicativo tooscale
Para uso em produção, você poderá muito[criar uma imagem VM personalizada](tutorial-custom-images.md) que inclui o aplicativo instalado e configurado. Para este tutorial, permite personalizar Olá que VMs na primeira tooquickly de inicialização Consulte uma escala definida em ação.

Um tutorial anterior, você aprendeu [como toocustomize uma máquina virtual do Linux na primeira inicialização](tutorial-automate-vm-deployment.md) com init de nuvem. Você pode usar Olá tooinstall de arquivo de configuração de nuvem init mesmo NGINX e executar um aplicativo simples do 'Hello World' Node. js. 

No shell atual, crie um arquivo chamado *init.txt nuvem* e colar Olá seguinte configuração. Por exemplo, crie o arquivo de saudação no hello nuvem Shell não está no seu computador local. Digite `sensible-editor cloud-init.txt` toocreate Olá arquivo e ver uma lista de editores disponíveis. Verifique se que esse arquivo de inicialização de nuvem inteiro Olá foi copiado corretamente, Olá especialmente a primeira linha:

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


## <a name="create-a-scale-set"></a>Criar um conjunto de escala
Antes de criar uma máquina virtual, crie um grupo de recursos com o [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupScaleSet* em Olá *eastus* local:

```azurecli-interactive 
az group create --name myResourceGroupScaleSet --location eastus
```

Crie um conjunto de dimensionamento de máquinas virtuais com [az vmss create](/cli/azure/vmss#create). Olá, exemplo a seguir cria uma conjunto nomeada de escalas *myScaleSet*usa Olá nuvem init arquivo toocustomize Olá VM e gera chaves SSH se não existirem:

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

Ele usa toocreate de alguns minutos e configurar todos os recursos de conjunto de escala hello e máquinas virtuais. Há tarefas em segundo plano que continuam toorun depois Olá CLI do Azure retorna toohello prompt. Pode ser outro alguns minutos antes de poder acessar o aplicativo hello.


## <a name="allow-web-traffic"></a>Permitir o tráfego da web
Um balanceador de carga foi criado automaticamente como parte do conjunto de escalas da máquina virtual hello. o balanceador de carga Olá distribui o tráfego entre um conjunto de VMs definidos usando regras de Balanceador de carga. Você pode aprender mais sobre conceitos de Balanceador de carga e a configuração no tutorial de Avançar hello, [como tooload equilibrar as máquinas virtuais no Azure](tutorial-load-balancer.md).

tooallow tráfego tooreach Olá web app, crie uma regra com [criar regra de balanceamento de carga de rede az](/cli/azure/network/lb/rule#create). Olá, exemplo a seguir cria uma regra denominada *myLoadBalancerRuleWeb*:

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

## <a name="test-your-app"></a>Testar seu aplicativo
toosee seu aplicativo Node. js na web hello, obter o endereço IP público de saudação do balanceador de carga com [az rede ip público exibir](/cli/azure/network/public-ip#show). Olá, exemplo a seguir obtém endereço IP hello *myScaleSetLBPublicIP* criado como parte do conjunto de escala hello:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSetLBPublicIP \
    --query [ipAddress] \
    --output tsv
```

Insira o endereço IP público de saudação no navegador da web de tooa. aplicativo Hello é exibido, incluindo o nome de host de saudação do hello VM que Olá a carga do tráfego do balanceador distribuída para:

![Executar o aplicativo Node.js](./media/tutorial-create-vmss/running-nodejs-app.png)

a escala de saudação toosee definida em ação, você pode forçar atualização sua carga de saudação do toosee de navegador da web balanceador distribuir o tráfego entre todas as VMs Olá executando o aplicativo.


## <a name="management-tasks"></a>Tarefas de gerenciamento
Ciclo de vida de saudação do conjunto de escala hello, talvez seja necessário toorun uma ou mais tarefas de gerenciamento. Além disso, talvez você queira toocreate scripts que automatizam várias tarefas de ciclo de vida. Olá 2.0 do CLI do Azure fornece uma maneira rápida de toodo essas tarefas. Estas são algumas tarefas comuns.

### <a name="view-vms-in-a-scale-set"></a>Exibição de VMs em um conjunto de escala
uma lista de VMs em execução em escala de seu conjunto de tooview, use [instâncias de lista az vmss](/cli/azure/vmss#list-instances) da seguinte maneira:

```azurecli-interactive 
az vmss list-instances \
  --resource-group myResourceGroupScaleSet \
  --name myScaleSet \
  --output table
```

saudação de saída é similar toohello exemplo a seguir:

```azurecli-interactive 
  InstanceId  LatestModelApplied    Location    Name          ProvisioningState    ResourceGroup            VmId
------------  --------------------  ----------  ------------  -------------------  -----------------------  ------------------------------------
           1  True                  eastus      myScaleSet_1  Succeeded            MYRESOURCEGROUPSCALESET  c72ddc34-6c41-4a53-b89e-dd24f27b30ab
           3  True                  eastus      myScaleSet_3  Succeeded            MYRESOURCEGROUPSCALESET  44266022-65c3-49c5-92dd-88ffa64f95da
```


### <a name="increase-or-decrease-vm-instances"></a>Aumentar ou diminuir as instâncias de VM
toosee Olá número de instâncias atualmente têm em uma escala de definido, use [Mostrar de vmss az](/cli/azure/vmss#show) e consultar *sku.capacity*:

```azurecli-interactive 
az vmss show \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --query [sku.capacity] \
    --output table
```

Você pode, em seguida, manualmente aumentar ou diminuir Olá número de máquinas virtuais em escala Olá com [escala de vmss az](/cli/azure/vmss#scale). Olá exemplo a seguir define Olá número de VMs em sua escala definida muito*5*:

```azurecli-interactive 
az vmss scale \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --new-capacity 5
```

Regras de dimensionamento automático permitem que você defina como tooscale para cima ou para baixo número de saudação de VMs em sua escala é definida na resposta toodemand como tráfego de rede ou o uso da CPU. Atualmente, essas regras não podem ser definidas na CLI 2.0 do Azure. Saudação de uso [portal do Azure](https://portal.azure.com) tooconfigure AutoEscala.

### <a name="get-connection-info"></a>Obter informações de conexão
informações de conexão tooobtain sobre Olá VMs em seus conjuntos de escala, use [az vmss lista--conexão-informações da instância](/cli/azure/vmss#list-instance-connection-info). Este comando gera o endereço IP público de saudação e a porta para cada VM que permite que você tooconnect com SSH:

```azurecli-interactive 
az vmss list-instance-connection-info \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet
```


## <a name="use-data-disks-with-scale-sets"></a>Usar discos de dados com conjuntos de dimensionamento
Você pode criar e usar discos de dados com conjuntos de dimensionamento. Um tutorial anterior, você aprendeu como muito[discos do Azure gerenciar](tutorial-manage-disks.md) que descreve Olá práticas recomendadas e melhorias de desempenho para a criação de aplicativos em discos de dados em vez de disco Olá sistema operacional.

### <a name="create-scale-set-with-data-disks"></a>Criar conjunto de dimensionamento com discos de dados
toocreate uma escala definida e anexar discos de dados, adicionar Olá `--data-disk-sizes-gb` parâmetro toohello [vmss az criar](/cli/azure/vmss#create) comando. Olá, exemplo a seguir cria uma escala com *50*Gb discos de dados anexado tooeach instância:

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

Quando as instâncias são removidas de um conjunto de dimensionamento, todos os discos de dados anexados também são removidos.

### <a name="add-data-disks"></a>Adicionar discos de dados
tooadd um tooinstances de disco de dados em sua escala definida, use [anexar disco de vmss az](/cli/azure/vmss/disk#attach). Olá exemplo a seguir adiciona uma *50*instância de tooeach disco Gb:

```azurecli-interactive 
az vmss disk attach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --size-gb 50 \
    --lun 2
```

### <a name="detach-data-disks"></a>Desanexar discos de dados
tooremove um tooinstances de disco de dados em sua escala definida, use [desanexar disco de vmss az](/cli/azure/vmss/disk#detach). Olá, exemplo a seguir remove Olá disco de dados no LUN *2* de cada instância de:

```azurecli-interactive 
az vmss disk detach \
    --resource-group myResourceGroupScaleSet \
    --name myScaleSet \
    --lun 2
```


## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você criou um conjunto de dimensionamento de máquinas virtuais. Você aprendeu como:

> [!div class="checklist"]
> * Use a nuvem init toocreate tooscale um aplicativo
> * Criar um conjunto de dimensionamento de máquinas virtuais
> * Aumentar ou diminuir o número de saudação de instâncias em um conjunto de escala
> * Exibir informações de conexão para instâncias do conjunto de dimensionamento
> * Usar discos de dados com conjunto de dimensionamento

Toohello toolearn de tutorial Avançar adiantar mais sobre conceitos para máquinas virtuais de balanceamento de carga.

> [!div class="nextstepaction"]
> [Balancear carga de máquinas virtuais](tutorial-load-balancer.md)