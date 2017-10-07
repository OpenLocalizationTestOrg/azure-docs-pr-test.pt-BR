---
title: "aaaHow tooload equilibrar as máquinas virtuais Linux no Azure | Microsoft Docs"
description: "Saiba como toouse hello Azure carregar balanceador toocreate um aplicativo altamente disponível e seguro entre três VMs do Linux"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: f01752c3caec3489ee13e63000775769f3236e11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-linux-virtual-machines-in-azure-toocreate-a-highly-available-application"></a>Como o tooload equilibrar a máquinas virtuais Linux no Azure toocreate um aplicativo altamente disponível
O balanceamento de carga fornece um nível mais alto de disponibilidade, distribuindo as solicitações de entrada em várias máquinas virtuais. Neste tutorial, você aprenderá sobre Olá diferentes componentes do balanceador de carga do Azure Olá que distribuir o tráfego e fornecem alta disponibilidade. Você aprenderá como:

> [!div class="checklist"]
> * Criar um balanceador de carga do Azure
> * Criar uma investigação de integridade do balanceador de carga
> * Criar regras de tráfego para o balanceador de carga
> * Use a nuvem init toocreate um aplicativo básico do Node. js
> * Criar máquinas virtuais e anexar tooa balanceador de carga
> * Exibir um balanceador de carga em ação
> * Adicionar e remover as VMs de um balanceador de carga


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se você escolher tooinstall e usa o hello CLI localmente, este tutorial requer que você está executando a versão de CLI do Azure Olá 2.0.4 ou posterior. Executar `az --version` toofind versão de saudação. Se você precisar tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="azure-load-balancer-overview"></a>Visão geral do Balanceador de Carga do Azure
Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP) que fornece alta disponibilidade distribuindo o tráfego de entrada entre VMs íntegros. Um teste de integridade do balanceador de carga monitora uma determinada porta em cada VM e só distribui o tráfego tooan operacional VM.

Você define uma configuração de IP de front-end que contém um ou mais endereços IP públicos. Essa configuração de IP de front-end permite que seu toobe de aplicativos e o balanceador de carga acessível pela Internet da saudação. 

Máquinas virtuais conectar-se usando sua placa de interface de rede virtual (NIC) de Balanceador de carga tooa. tráfego de toodistribute toohello VMs, um pool de endereços de back-end contém endereços IP Olá Olá virtual (NICs) toohello conectados do balanceador de carga.

fluxo de saudação toocontrol de tráfego, você definir regras de Balanceador de carga para portas e protocolos que mapeiam tooyour VMs específicos.

Se você seguiu o tutorial anterior Olá muito[criar um conjunto de escala de máquinas virtuais](tutorial-create-vmss.md), um balanceador de carga foi criado para você. Todos esses componentes foram configurados para você como parte do conjunto de escala de saudação.


## <a name="create-azure-load-balancer"></a>Criar o balanceador de carga do Azure
Esta seção fornece detalhes sobre como você pode criar e configurar cada componente de saudação do balanceador de carga. Antes de criar seu balanceador de carga, crie um grupo de recursos com o [az group create](/cli/azure/group#create). Olá, exemplo a seguir cria um grupo de recursos denominado *myResourceGroupLoadBalancer* em Olá *eastus* local:

```azurecli-interactive 
az group create --name myResourceGroupLoadBalancer --location eastus
```

### <a name="create-a-public-ip-address"></a>Criar um endereço IP público
tooaccess Olá de seu aplicativo na Internet, é necessário um endereço IP público Olá balanceador de carga. Crie um endereço IP público com [az network public-ip create](/cli/azure/network/public-ip#create). Olá, exemplo a seguir cria um endereço IP público denominado *myPublicIP* em Olá *myResourceGroupLoadBalancer* grupo de recursos:

```azurecli-interactive 
az network public-ip create \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP
```

### <a name="create-a-load-balancer"></a>Criar um balanceador de carga
Crie um balanceador de carga com [az network lb create](/cli/azure/network/lb#create). Olá, exemplo a seguir cria um balanceador de carga denominado *myLoadBalancer* e atribui hello *myPublicIP* configuração de IP de front-end do endereço toohello:

```azurecli-interactive 
az network lb create \
    --resource-group myResourceGroupLoadBalancer \
    --name myLoadBalancer \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --public-ip-address myPublicIP
```

### <a name="create-a-health-probe"></a>Criar uma investigação de integridade
tooallow Olá balanceador toomonitor Olá status de carga do seu aplicativo, você usar uma investigação de integridade. investigação de integridade Olá dinamicamente adiciona ou remove as VMs de rotação do balanceador de carga de saudação com base em suas verificações de toohealth de resposta. Por padrão, uma máquina virtual é removida da distribuição de Balanceador de carga Olá após duas falhas consecutivas em intervalos de 15 segundos. Crie uma investigação de integridade com base em um protocolo ou página de verificação de integridade específica ao seu aplicativo. 

saudação de exemplo a seguir cria uma investigação TCP. Você também pode criar investigações de HTTP personalizadas para obter verificações de integridade mais refinadas. Ao usar uma investigação personalizada de HTTP, você deve criar página de verificação de integridade hello, tais como *healthcheck.js*. investigação de saudação deve retornar um **HTTP 200 Okey** resposta para Olá carga balanceador tookeep Olá host rotação.

toocreate uma investigação de integridade TCP, use [criar investigação de balanceamento de carga de rede az](/cli/azure/network/lb/probe#create). Olá, exemplo a seguir cria um teste de integridade chamado *myHealthProbe*:

```azurecli-interactive 
az network lb probe create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myHealthProbe \
    --protocol tcp \
    --port 80
```

### <a name="create-a-load-balancer-rule"></a>Criar uma regra de balanceador de carga
Uma regra de Balanceador de carga é toodefine usado como o tráfego é distribuído toohello VMs. Você definir a configuração de IP front-end Olá para o tráfego de entrada hello e Olá back-end pool tooreceive Olá tráfego IP, juntamente com a origem de saudação necessários e porta de destino. toomake-se de que apenas as VMs íntegras receberem tráfego, você também definir Olá toouse de investigação de integridade.

Crie uma regra de balanceador de carga com [az network lb rule create](/cli/azure/network/lb/rule#create). Olá, exemplo a seguir cria uma regra denominada *myLoadBalancerRule*, Olá usa *myHealthProbe* investigação de integridade e o tráfego na porta saldos *80*:

```azurecli-interactive 
az network lb rule create \
    --resource-group myResourceGroupLoadBalancer \
    --lb-name myLoadBalancer \
    --name myLoadBalancerRule \
    --protocol tcp \
    --frontend-port 80 \
    --backend-port 80 \
    --frontend-ip-name myFrontEndPool \
    --backend-pool-name myBackEndPool \
    --probe-name myHealthProbe
```


## <a name="configure-virtual-network"></a>Configurar rede virtual
Antes de implantar algumas máquinas virtuais e testar seu balanceador, crie hello dando suporte a recursos de rede virtual. Para obter mais informações sobre redes virtuais, consulte Olá [gerenciar redes virtuais do Azure](tutorial-virtual-network.md) tutorial.

### <a name="create-network-resources"></a>Criar recursos da rede
Crie a rede virtual com [az network vnet create](/cli/azure/network/vnet#create). Olá, exemplo a seguir cria uma rede virtual denominada *myVnet* com uma sub-rede denominada *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupLoadBalancer \
    --name myVnet \
    --subnet-name mySubnet
```

tooadd um grupo de segurança de rede, use [criar az rede nsg](/cli/azure/network/nsg#create). Olá, exemplo a seguir cria um grupo de segurança de rede denominado *myNetworkSecurityGroup*:

```azurecli-interactive 
az network nsg create \
    --resource-group myResourceGroupLoadBalancer \
    --name myNetworkSecurityGroup
```

Crie uma regra de grupo de segurança de rede com [az network nsg create](/cli/azure/network/nsg/rule#create). Olá, exemplo a seguir cria uma regra de grupo de segurança de rede denominada *myNetworkSecurityGroupRule*:

```azurecli-interactive 
az network nsg rule create \
    --resource-group myResourceGroupLoadBalancer \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --priority 1001 \
    --protocol tcp \
    --destination-port-range 80
```

NICs virtuais são criadas com [az network nic create](/cli/azure/network/nic#create). Olá, exemplo a seguir cria três NICs virtuais. (Uma NIC virtual para cada VM que você criou para seu aplicativo no hello seguindo as etapas.) Você pode criar VMs e NICs virtuais adicionais a qualquer momento e adicioná-los toohello balanceador de carga:

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupLoadBalancer \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --network-security-group myNetworkSecurityGroup \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-virtual-machines"></a>Criar máquinas virtuais

### <a name="create-cloud-init-config"></a>Criar configuração de inicialização de nuvem
Um tutorial anterior em [como toocustomize uma máquina virtual do Linux na primeira inicialização](tutorial-automate-vm-deployment.md), você aprendeu como tooautomate personalização de VM com a nuvem init. Você pode usar Olá tooinstall de arquivo de configuração de nuvem init mesmo NGINX e executar um aplicativo simples do 'Hello World' Node. js.

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

### <a name="create-virtual-machines"></a>Criar máquinas virtuais
tooimprove Olá alta disponibilidade do seu aplicativo, colocar suas VMs em um conjunto de disponibilidade. Para obter mais informações sobre conjuntos de disponibilidade, consulte Olá anterior [como máquinas virtuais altamente disponíveis de toocreate](tutorial-availability-sets.md) tutorial.

Crie um conjunto de disponibilidade com [az vm availability-set create](/cli/azure/vm/availability-set#create). Olá, exemplo a seguir cria um conjunto nomeada de disponibilidade *myAvailabilitySet*:

```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupLoadBalancer \
    --name myAvailabilitySet
```

Agora você pode criar VMs Olá com [criar vm az](/cli/azure/vm#create). Olá exemplo a seguir cria três VMs e gera as chaves de SSH se eles ainda não existir:

```bash
for i in `seq 1 3`; do
    az vm create \
        --resource-group myResourceGroupLoadBalancer \
        --name myVM$i \
        --availability-set myAvailabilitySet \
        --nics myNic$i \
        --image UbuntuLTS \
        --admin-username azureuser \
        --generate-ssh-keys \
        --custom-data cloud-init.txt \
        --no-wait
done
```

Há tarefas em segundo plano que continuam toorun depois Olá CLI do Azure retorna toohello prompt. Olá `--no-wait` parâmetro não espera para todos os Olá toocomplete de tarefas. Pode ser outro alguns minutos antes de poder acessar o aplicativo hello. Olá investigação de integridade do balanceador de carga detecta automaticamente quando o aplicativo hello está em execução em cada VM. Depois que o aplicativo hello está em execução, regra de Balanceador de carga Olá inicia toodistribute tráfego.


## <a name="test-load-balancer"></a>Testar o balanceador de carga
Obter o endereço IP público de saudação do balanceador de carga com [az rede ip público exibir](/cli/azure/network/public-ip#show). Olá, exemplo a seguir obtém endereço IP hello *myPublicIP* criado anteriormente:

```azurecli-interactive 
az network public-ip show \
    --resource-group myResourceGroupLoadBalancer \
    --name myPublicIP \
    --query [ipAddress] \
    --output tsv
```

Você pode inserir o endereço IP público de saudação no navegador da web de tooa. Lembre-se: demora alguns minutos Olá Olá VMs toobe pronto antes do início de Balanceador de carga Olá toodistribute toothem de tráfego. Olá aplicativo é exibido, incluindo o nome de host de saudação do hello VM balanceador de carga que Olá distribuído tooas de tráfego em Olá exemplo a seguir:

![Executar o aplicativo Node.js](./media/tutorial-load-balancer/running-nodejs-app.png)

Balanceador de carga toosee Olá distribuir tráfego entre todas as três VMs executando o aplicativo, você pode forçar atualização de seu navegador da web.


## <a name="add-and-remove-vms"></a>Adicionar e remover as VMs
Talvez seja necessário tooperform manutenção Olá VMs que executam seu aplicativo, como ao instalar atualizações do sistema operacional. toodeal com o aumento no tráfego tooyour aplicativo, talvez seja necessário tooadd VMs adicionais. Esta seção mostra como tooremove ou adicionar uma VM do balanceador de carga de saudação.

### <a name="remove-a-vm-from-hello-load-balancer"></a>Remover uma máquina virtual do balanceador de carga Olá
Você pode remover uma máquina virtual do pool de endereços de back-end Olá com [remover az rede nic ip-config-pool de endereços](/cli/azure/network/nic/ip-config/address-pool#remove). Olá remove de exemplo a seguir Olá NIC virtual para **myVM2** de *myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool remove \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool 
```

Balanceador de carga toosee Olá distribuir o tráfego entre Olá restantes duas VMs que executam seu aplicativo você pode forçar atualização de seu navegador da web. Agora você pode realizar uma manutenção em Olá VM, como instalar atualizações do sistema operacional ou executar uma reinicialização da VM.

### <a name="add-a-vm-toohello-load-balancer"></a>Adicionar um balanceador de carga de toohello VM
Depois de executar a manutenção VM, ou se você precisar de capacidade de tooexpand, você pode adicionar um pool de endereços de back-end do VM toohello com [adicionar az rede nic ip-config-pool de endereços](/cli/azure/network/nic/ip-config/address-pool#add). Olá, exemplo a seguir adiciona Olá NIC virtual para **myVM2** muito*myLoadBalancer*:

```azurecli-interactive 
az network nic ip-config address-pool add \
    --resource-group myResourceGroupLoadBalancer \
    --nic-name myNic2 \
    --ip-config-name ipConfig1 \
    --lb-name myLoadBalancer \
    --address-pool myBackEndPool
```


## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você criou um balanceador de carga e anexado VMs tooit. Você aprendeu como:

> [!div class="checklist"]
> * Criar um balanceador de carga do Azure
> * Criar uma investigação de integridade do balanceador de carga
> * Criar regras de tráfego para o balanceador de carga
> * Use a nuvem init toocreate um aplicativo básico do Node. js
> * Criar máquinas virtuais e anexar tooa balanceador de carga
> * Exibir um balanceador de carga em ação
> * Adicionar e remover as VMs de um balanceador de carga

Toohello toolearn de tutorial Avançar adiantar mais sobre os componentes de rede virtual do Azure.

> [!div class="nextstepaction"]
> [Gerencie VMs e redes virtuais](tutorial-virtual-network.md)
