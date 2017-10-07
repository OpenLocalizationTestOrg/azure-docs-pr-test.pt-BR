---
title: aaaCreate um ambiente completo de Linux com hello 1.0 da CLI do Azure | Microsoft Docs
description: "Crie armazenamento, uma VM do Linux, uma rede virtual e sub-rede, um balanceador de carga, uma NIC, um IP público e um grupo de segurança de rede, tudo a partir de saudação Terra usando Olá 1.0 da CLI do Azure."
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ba4060b-ce95-4747-a735-1d7c68597a1a
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 7fe00e138704fe9c9a1c9b87a7dd1afd6174e527
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-complete-linux-environment-with-hello-azure-cli-10"></a>Criar um ambiente completo do Linux com hello 1.0 da CLI do Azure
Neste artigo, vamos criar uma rede simples com um balanceador de carga e com um par de VMs úteis para desenvolvimento e computação simples. Percorremos o processo de saudação pelo comando, até que você tiver dois ativa, seguro toowhich de VMs do Linux, que você pode se conectar de em qualquer lugar em Olá da Internet. Em seguida, você pode mover em ambientes e redes complexas toomore.

Caminho hello, você aprenderá sobre hierarquia de dependência de saudação que modelo de implantação do Gerenciador de recursos de saudação lhe e sobre quanta energia fornece. Depois de ver como o sistema de saudação é criado, você poderá recriá-lo muito mais rapidamente usando [modelos do Azure Resource Manager](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Além disso, depois que você saiba como partes de saudação do seu ambiente se encaixam, criando modelos tooautomate-los se torna mais fácil.

Olá ambiente contém:

* Duas VMs dentro de um conjunto de disponibilidade.
* Um balanceador de carga com uma regra de balanceamento de carga na porta 80.
* O grupo de segurança de rede (NSG) regras tooprotect sua VM de tráfego não desejado.

toocreate nesse ambiente personalizado, você precisa hello mais recente [Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) no modo do Gerenciador de recursos (`azure config mode arm`). Você também precisará de uma ferramenta de análise de JSON. Este exemplo usa [jq](https://stedolan.github.io/jq/).


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefa de saudação do CLI versões toocomplete
Você pode concluir a tarefa hello usando uma saudação versões da CLI a seguir:

- [1.0 de CLI do Azure](#quick-commands) – nosso CLI para Olá clássico e o recurso de gerenciamento modelos de implantação (Este artigo)
- [2.0 do CLI do Azure](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) -nossa próxima geração CLI para o modelo de implantação do gerenciamento de recursos de saudação


## <a name="quick-commands"></a>Comandos rápidos
Se você precisar tooquickly realizar tarefa hello, Olá Olá de detalhes da seção a seguir base tooupload comandos tooAzure uma VM. Obter mais informações e o contexto para cada etapa pode ser encontrada no restante de saudação do documento hello, iniciando [aqui](#detailed-walkthrough).

Certifique-se de que você tenha [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) conectado e usando o modo do Gerenciador de recursos:

```azurecli
azure config mode arm
```

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem `myResourceGroup`, `mystorageaccount` e `myVM`.

Crie grupo de recursos de saudação. Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westeurope` local:

```azurecli
azure group create -n myResourceGroup -l westeurope
```

Verifique se o grupo de recursos hello usando o analisador JSON hello:

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Crie conta de armazenamento de saudação. Olá, exemplo a seguir cria uma conta de armazenamento denominada `mystorageaccount`. (o nome de conta de armazenamento Olá deve ser exclusivo, portanto, fornecer seu próprio nome exclusivo.)

```azurecli
azure storage account create -g myResourceGroup -l westeurope \
  --kind Storage --sku-name GRS mystorageaccount
```

Verifique se a conta de armazenamento de saudação usando o analisador JSON de saudação:

```azurecli
azure storage account show -g myResourceGroup mystorageaccount --json | jq '.'
```

Crie rede virtual hello. Olá, exemplo a seguir cria uma rede virtual denominada `myVnet`:

```azurecli
azure network vnet create -g myResourceGroup -l westeurope\
  -n myVnet -a 192.168.0.0/16
```

Crie uma sub-rede. Olá, exemplo a seguir cria uma sub-rede denominada `mySubnet`:

```azurecli
azure network vnet subnet create -g myResourceGroup \
  -e myVnet -n mySubnet -a 192.168.1.0/24
```

Verificar Olá uma rede virtual e sub-rede usando o analisador JSON hello:

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Crie um IP público. Olá, exemplo a seguir cria um IP público denominado `myPublicIP` com nome DNS de saudação do `mypublicdns`. (o nome DNS Olá deve ser exclusivo, para fornecer seu próprio nome exclusivo.)

```azurecli
azure network public-ip create -g myResourceGroup -l westeurope \
  -n myPublicIP  -d mypublicdns -a static -i 4
```

Crie o balanceador de carga de saudação. Olá, exemplo a seguir cria um balanceador de carga chamado `myLoadBalancer`:

```azurecli
azure network lb create -g myResourceGroup -l westeurope -n myLoadBalancer
```

Criar um pool IP de front-end para o balanceador de carga hello e associar IP público hello. Olá, exemplo a seguir cria um pool IP de front-end denominado `mySubnetPool`:

```azurecli
azure network lb frontend-ip create -g myResourceGroup -l myLoadBalancer \
  -i myPublicIP -n myFrontEndPool
```

Crie pool IP de back-end Olá Olá balanceador de carga. Olá, exemplo a seguir cria um pool IP de back-end denominado `myBackEndPool`:

```azurecli
azure network lb address-pool create -g myResourceGroup -l myLoadBalancer \
  -n myBackEndPool
```

Crie regras NAT (conversão) de endereço Olá balanceador de carga de rede de entrada do SSH. Olá, exemplo a seguir cria duas regras de Balanceador de carga, `myLoadBalancerRuleSSH1` e `myLoadBalancerRuleSSH2`:

```azurecli
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH1 -p tcp -f 4222 -b 22
azure network lb inbound-nat-rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleSSH2 -p tcp -f 4223 -b 22
```

Olá web de criar regras de NAT de entrada para Olá balanceador de carga. Olá, exemplo a seguir cria uma regra de Balanceador de carga denominada `myLoadBalancerRuleWeb`:

```azurecli
azure network lb rule create -g myResourceGroup -l myLoadBalancer \
  -n myLoadBalancerRuleWeb -p tcp -f 80 -b 80 \
  -t myFrontEndPool -o myBackEndPool
```

Crie hello investigação de integridade do balanceador de carga. Olá, exemplo a seguir cria um teste TCP chamado `myHealthProbe`:

```azurecli
azure network lb probe create -g myResourceGroup -l myLoadBalancer \
  -n myHealthProbe -p "tcp" -i 15 -c 4
```

Verifique o balanceador de carga hello, pools de IP e as regras de NAT usando o analisador JSON de saudação:

```azurecli
azure network lb show -g myResourceGroup -n myLoadBalancer --json | jq '.'
```

Crie hello primeira placa de rede (NIC). Substituir saudação `#####-###-###` seções com sua ID de assinatura do Azure. Sua assinatura ID é observado na saída de saudação do **jq** quando você examinar recursos Olá que você está criando. Você também pode exibir sua ID de assinatura com `azure account list`.

Olá, exemplo a seguir cria uma NIC chamada `myNic1`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic1 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
```

Criar o segundo NIC de saudação. Olá, exemplo a seguir cria uma NIC chamada `myNic2`:

```azurecli
azure network nic create -g myResourceGroup -l westeurope \
  -n myNic2 -m myVnet -k mySubnet \
  -d "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool" \
  -e "/subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
```

Verificar Olá duas NICs usando o analisador JSON hello:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
azure network nic show myResourceGroup myNic2 --json | jq '.'
```

Crie grupo de segurança de rede de saudação. Olá, exemplo a seguir cria um grupo de segurança de rede denominado `myNetworkSecurityGroup`:

```azurecli
azure network nsg create -g myResourceGroup -l westeurope \
  -n myNetworkSecurityGroup
```

Adicione duas regras de entrada para o grupo de segurança de rede hello. Olá, exemplo a seguir cria duas regras, `myNetworkSecurityGroupRuleSSH` e `myNetworkSecurityGroupRuleHTTP`:

```azurecli
azure network nsg rule create -p tcp -r inbound -y 1000 -u 22 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleSSH
azure network nsg rule create -p tcp -r inbound -y 1001 -u 80 -c allow \
  -g myResourceGroup -a myNetworkSecurityGroup -n myNetworkSecurityGroupRuleHTTP
```

Verifique se o grupo de segurança de rede hello e as regras de entrada usando o analisador JSON hello:

```azurecli
azure network nsg show -g myResourceGroup -n myNetworkSecurityGroup --json | jq '.'
```

Associação de segurança de rede Olá toohello duas NICs de grupo:

```azurecli
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic1
azure network nic set -g myResourceGroup -o myNetworkSecurityGroup -n myNic2
```

Crie conjunto de disponibilidade de saudação. Olá, exemplo a seguir cria um conjunto nomeada de disponibilidade `myAvailabilitySet`:

```azurecli
azure availset create -g myResourceGroup -l westeurope -n myAvailabilitySet
```

Criar hello primeira VM do Linux. Olá, exemplo a seguir cria uma VM denominada `myVM1`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM1 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic1 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Criar hello segundo VM do Linux. Olá, exemplo a seguir cria uma VM denominada `myVM2`:

```azurecli
azure vm create \
    --resource-group myResourceGroup \
    --name myVM2 \
    --location westeurope \
    --os-type linux \
    --availset-name myAvailabilitySet \
    --nic-name myNic2 \
    --vnet-name myVnet \
    --vnet-subnet-name mySubnet \
    --storage-account-name mystorageaccount \
    --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --admin-username azureuser
```

Use Olá JSON analisador tooverify tudo que foi criado:

```azurecli
azure vm show -g myResourceGroup -n myVM1 --json | jq '.'
azure vm show -g myResourceGroup -n myVM2 --json | jq '.'
```

Exporte seu novo ambiente tooa tooquickly recriar novas instâncias do modelo:

```azurecli
azure group export myResourceGroup
```

## <a name="detailed-walkthrough"></a>Passo a passo detalhado
Olá etapas detalhadas que sigam explicam o que cada comando é fazer à medida que seu ambiente. Esses conceitos são úteis durante a criação de seus próprios ambientes personalizados para desenvolvimento ou produção.

Certifique-se de que você tenha [hello Azure CLI 1.0](../../cli-install-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) conectado e usando o modo do Gerenciador de recursos:

```azurecli
azure config mode arm
```

Em Olá exemplos a seguir, substitua os nomes de parâmetro de exemplo com seus próprios valores. Os nomes de parâmetro de exemplo incluem `myResourceGroup`, `mystorageaccount` e `myVM`.

## <a name="create-resource-groups-and-choose-deployment-locations"></a>Criar grupos de recursos e escolher locais de implantação
Grupos de recursos do Azure são entidades de lógica de implantação que contêm informações e metadados tooenable Olá lógico gerenciamento de configuração de implantações de recursos. Olá, exemplo a seguir cria um grupo de recursos denominado `myResourceGroup` em Olá `westeurope` local:

```azurecli
azure group create --name myResourceGroup --location westeurope
```

Saída:

```azurecli                        
info:    Executing command group create
+ Getting resource group myResourceGroup
+ Creating resource group myResourceGroup
info:    Created resource group myResourceGroup
data:    Id:                  /subscriptions/guid/resourceGroups/myResourceGroup
data:    Name:                myResourceGroup
data:    Location:            westeurope
data:    Provisioning State:  Succeeded
data:    Tags: null
data:
info:    group create command OK
```

## <a name="create-a-storage-account"></a>Criar uma conta de armazenamento
É necessário contas de armazenamento para os discos VM e para os discos de dados adicionais que você deseja tooadd. Você cria contas de armazenamento quase que imediatamente depois de criar grupos de recursos.

Aqui usamos Olá `azure storage account create` comando, passando local Olá da conta hello, grupo de recursos de saudação que controla a ele e o tipo de saudação de suporte de armazenamento que você deseja. Olá, exemplo a seguir cria uma conta de armazenamento denominada `mystorageaccount`:

```azurecli
azure storage account create \  
  --location westeurope \
  --resource-group myResourceGroup \
  --kind Storage --sku-name GRS \
  mystorageaccount
```

Saída:

```azurecli
info:    Executing command storage account create
+ Creating storage account
info:    storage account create command OK
```

tooexamine nosso recurso de grupo usando Olá `azure group show` command, vamos usar Olá [jq](https://stedolan.github.io/jq/) ferramenta juntamente com hello `--json` opção CLI do Azure. (Você pode usar **jsawk** ou qualquer biblioteca de idioma que você preferir tooparse Olá JSON.)

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Saída:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

conta de armazenamento tooinvestigate hello usando Olá CLI, é necessário primeiro chaves e nomes de conta tooset hello. Substitua o nome de saudação da conta de armazenamento Olá Olá exemplo com um nome que você escolher a seguir:

```bash
export AZURE_STORAGE_CONNECTION_STRING="$(azure storage account connectionstring show mystorageaccount --resource-group myResourceGroup --json | jq -r '.string')"
```

Em seguida, você poderá exibir as informações de armazenamento facilmente:

```azurecli
azure storage container list
```

Saída:

```azurecli
info:    Executing command storage container list
+ Getting storage containers
data:    Name  Public-Access  Last-Modified
data:    ----  -------------  -----------------------------
data:    vhds  Off            Sun, 27 Sep 2015 19:03:54 GMT
info:    storage container list command OK
```

## <a name="create-a-virtual-network-and-subnet"></a>Criar a rede virtual e a sub-rede
Em seguida você vai tooneed toocreate uma rede virtual em execução no Azure e uma sub-rede na qual você pode criar suas VMs. Olá, exemplo a seguir cria uma rede virtual denominada `myVnet` com hello `192.168.0.0/16` prefixo de endereço:

```azurecli
azure network vnet create --resource-group myResourceGroup --location westeurope \
  --name myVnet --address-prefixes 192.168.0.0/16
```

Saída:

```azurecli
info:    Executing command network vnet create
+ Looking up virtual network "myVnet"
+ Creating virtual network "myVnet"
+ Loading virtual network state
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet
data:    Name                            : myVnet
data:    Type                            : Microsoft.Network/virtualNetworks
data:    Location                        : westeurope
data:    ProvisioningState               : Succeeded
data:    Address prefixes:
data:      192.168.0.0/16
info:    network vnet create command OK
```

Novamente, vamos usar a opção – json Olá `azure group show` e `jq` toosee como estamos criando nossos recursos. Agora, temos um recurso `storageAccounts` e um recurso `virtualNetworks`.  

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Saída:

```json
{
  "tags": {},
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup",
  "name": "myResourceGroup",
  "provisioningState": "Succeeded",
  "location": "westeurope",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "resources": [
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
      "name": "myVnet",
      "type": "virtualNetworks",
      "location": "westeurope",
      "tags": null
    },
    {
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
      "name": "mystorageaccount",
      "type": "storageAccounts",
      "location": "westeurope",
      "tags": null
    }
  ],
  "permissions": [
    {
      "actions": [
        "*"
      ],
      "notActions": []
    }
  ]
}
```

Agora vamos criar uma sub-rede em Olá `myVnet` rede virtual no qual Olá VMs são implantadas. Usamos Olá `azure network vnet subnet create` comando, junto com os recursos de saudação já criamos: Olá `myResourceGroup` grupo de recursos e hello `myVnet` rede virtual. Saudação de exemplo a seguir, adicionamos sub-rede Olá denominada `mySubnet` com prefixo de endereço da sub-rede Olá `192.168.1.0/24`:

```azurecli
azure network vnet subnet create --resource-group myResourceGroup \
  --vnet-name myVnet --name mySubnet --address-prefix 192.168.1.0/24
```

Saída:

```azurecli
info:    Executing command network vnet subnet create
+ Looking up hello subnet "mySubnet"
+ Creating subnet "mySubnet"
+ Looking up hello subnet "mySubnet"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:    Type                            : Microsoft.Network/virtualNetworks/subnets
data:    ProvisioningState               : Succeeded
data:    Name                            : mySubnet
data:    Address prefix                  : 192.168.1.0/24
data:
info:    network vnet subnet create command OK
```

Como sub-rede Olá é logicamente dentro da rede virtual hello, procuramos informações de sub-rede Olá com um comando ligeiramente diferente. comando Olá usamos é `azure network vnet show`, mas continuar a saída JSON de saudação tooexamine usando `jq`.

```azurecli
azure network vnet show myResourceGroup myVnet --json | jq '.'
```

Saída:

```json
{
  "subnets": [
    {
      "ipConfigurations": [],
      "addressPrefix": "192.168.1.0/24",
      "provisioningState": "Succeeded",
      "name": "mySubnet",
      "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
    }
  ],
  "tags": {},
  "addressSpace": {
    "addressPrefixes": [
      "192.168.0.0/16"
    ]
  },
  "dhcpOptions": {
    "dnsServers": []
  },
  "provisioningState": "Succeeded",
  "etag": "W/\"974f3e2c-028e-4b35-832b-a4b16ad25eb6\"",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
  "name": "myVnet",
  "location": "westeurope"
}
```

## <a name="create-a-public-ip-address"></a>Criar um endereço IP público
Agora vamos criar o endereço IP público hello (PIP) que podemos atribuir tooyour balanceador de carga. Ele permite tooconnect tooyour VMs de saudação à Internet usando Olá `azure network public-ip create` comando. Como o endereço de saudação padrão é dinâmico, criamos uma entrada DNS denominada Olá **cloudapp.azure.com** domínio usando Olá `--domain-name-label` opção. Olá, exemplo a seguir cria um IP público denominado `myPublicIP` com nome DNS de saudação do `mypublicdns`. Como o nome de DNS Olá deve ser exclusivo, você pode fornecer seu próprio nome DNS exclusivo:

```azurecli
azure network public-ip create --resource-group myResourceGroup \
  --location westeurope --name myPublicIP --domain-name-label mypublicdns
```

Saída:

```azurecli
info:    Executing command network public-ip create
+ Looking up hello public ip "myPublicIP"
+ Creating public ip address "myPublicIP"
+ Looking up hello public ip "myPublicIP"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
data:    Name                            : myPublicIP
data:    Type                            : Microsoft.Network/publicIPAddresses
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Allocation method               : Dynamic
data:    Idle timeout                    : 4
data:    Domain name label               : mypublicdns
data:    FQDN                            : mypublicdns.westeurope.cloudapp.azure.com
info:    network public-ip create command OK
```

Olá endereço IP público é também um recurso de nível superior, para que você possa ver com `azure group show`.

```azurecli
azure group show myResourceGroup --json | jq '.'
```

Saída:

```json
{
"tags": {},
"id": "/subscriptions/guid/resourceGroups/myResourceGroup",
"name": "myResourceGroup",
"provisioningState": "Succeeded",
"location": "westeurope",
"properties": {
    "provisioningState": "Succeeded"
},
"resources": [
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
    "name": "myPublicIP",
    "type": "publicIPAddresses",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet",
    "name": "myVnet",
    "type": "virtualNetworks",
    "location": "westeurope",
    "tags": null
    },
    {
    "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Storage/storageAccounts/mystorageaccount",
    "name": "mystorageaccount",
    "type": "storageAccounts",
    "location": "westeurope",
    "tags": null
    }
],
"permissions": [
    {
    "actions": [
        "*"
    ],
    "notActions": []
    }
]
}
```

Você pode investigar mais detalhes de recursos, incluindo o nome de domínio totalmente qualificado (FQDN) saudação do subdomínio de saudação usando Olá completa `azure network public-ip show` comando. recurso de endereço IP público Olá foi alocado logicamente, mas um endereço específico ainda não foi atribuído. tooobtain um endereço IP, você vai tooneed um balanceador de carga, ainda não tiver criado.

```azurecli
azure network public-ip show myResourceGroup myPublicIP --json | jq '.'
```

Saída:

```json
{
"tags": {},
"publicIpAllocationMethod": "Dynamic",
"dnsSettings": {
    "domainNameLabel": "mypublicdns",
    "fqdn": "mypublicdns.westeurope.cloudapp.azure.com"
},
"idleTimeoutInMinutes": 4,
"provisioningState": "Succeeded",
"etag": "W/\"c63154b3-1130-49b9-a887-877d74d5ebc5\"",
"id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP",
"name": "myPublicIP",
"location": "westeurope"
}
```

## <a name="create-a-load-balancer-and-ip-pools"></a>Criar um balanceador de carga e pools de IPs
Quando você cria um balanceador de carga, ele permite que você toodistribute tráfego em várias VMs. Ele também fornece aplicativos de tooyour redundância executando várias VMs que respondem a solicitações de toouser no evento de saudação de manutenção ou pesadas. Olá, exemplo a seguir cria um balanceador de carga chamado `myLoadBalancer`:

```azurecli
azure network lb create --resource-group myResourceGroup --location westeurope \
  --name myLoadBalancer
```

Saída:

```azurecli
info:    Executing command network lb create
+ Looking up hello load balancer "myLoadBalancer"
+ Creating load balancer "myLoadBalancer"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer
data:    Name                            : myLoadBalancer
data:    Type                            : Microsoft.Network/loadBalancers
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
info:    network lb create command OK
```

Nosso balanceador de carga está bem vazio, então vamos criar alguns pools de IPs. Queremos toocreate dois pools de IP para nosso balanceador de carga, um para o front-end hello e outro para o back-end hello. pool de IP de front-end de saudação é visível publicamente. Também é Olá local toowhich que nós atribuímos Olá PIP que criamos anteriormente. Em seguida, usamos pool de back-end Olá como um local de nossa tooconnect VMs para. Dessa forma, o tráfego de saudação pode fluir pelo toohello balanceador de carga Olá VMs.

Primeiro, vamos criar nosso pool de IPs de front-end. Olá, exemplo a seguir cria um pool de front-end denominado `myFrontEndPool`:

```azurecli
azure network lb frontend-ip create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --public-ip-name myPublicIP \
  --name myFrontEndPool
```

Saída:

```azurecli
info:    Executing command network lb frontend-ip create
+ Looking up hello load balancer "myLoadBalancer"
+ Looking up hello public ip "myPublicIP"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myFrontEndPool
data:    Provisioning state              : Succeeded
data:    Private IP allocation method    : Dynamic
data:    Public IP address id            : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP
info:    network lb mySubnet-ip create command OK
```

Observe como usamos Olá `--public-ip-name` toopass de inserção Olá `myPublicIP` que criamos anteriormente. Atribuição de IP público Olá balanceador de carga do endereço toohello permite que você tooreach suas VMs em Olá da Internet.

Em seguida, vamos criar nosso segundo pool de IPs, desta vez, para o tráfego de back-end. Olá, exemplo a seguir cria um pool de back-end denominado `myBackEndPool`:

```azurecli
azure network lb address-pool create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myBackEndPool
```

Saída:

```azurecli
info:    Executing command network lb address-pool create
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myBackEndPool
data:    Provisioning state              : Succeeded
info:    network lb address-pool create command OK
```

Podemos ver como nosso balanceador de carga está procurando com `azure network lb show` e examinar a saída JSON hello:

```azurecli
azure network lb show myResourceGroup myLoadBalancer --json | jq '.'
```

Saída:

```json
{
  "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"29c38649-77d6-43ff-ab8f-977536b0047c\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [],
  "probes": []
}
```

## <a name="create-load-balancer-nat-rules"></a>Criar regras NAT do balanceador de carga
tráfego tooget que passam por nossos balanceador de carga, precisamos de regras NAT (conversão) de endereços de rede de toocreate que especificam as ações de entrada ou saídas. Você pode especificar Olá protocolo toouse e mapear portas externas toointernal portas conforme desejado. Em nosso ambiente, vamos criar algumas regras que permitem SSH por meio de nosso tooour de Balanceador de carga de máquinas virtuais. Fizemos porta do TCP portas 4222 e 4223 toodirect tooTCP 22 em nosso VMs (que criamos mais tarde). Olá, exemplo a seguir cria uma regra denominada `myLoadBalancerRuleSSH1` toomap TCP porta 4222 tooport 22:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH1 \
  --protocol tcp --frontend-port 4222 --backend-port 22
```

Saída:

```azurecli
info:    Executing command network lb inbound-nat-rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default enable floating ip: false
warn:    Using default idle timeout: 4
warn:    Using default mySubnet IP configuration "myFrontEndPool"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleSSH1
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 4222
data:    Backend port                    : 22
data:    Enable floating IP              : false
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
info:    network lb inbound-nat-rule create command OK
```

Repita o procedimento de saudação da segunda regra NAT para o SSH. Olá, exemplo a seguir cria uma regra denominada `myLoadBalancerRuleSSH2` toomap TCP porta 4223 tooport 22:

```azurecli
azure network lb inbound-nat-rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleSSH2 --protocol tcp \
  --frontend-port 4223 --backend-port 22
```

Vamos também vá em frente e crie uma regra NAT para a porta TCP 80 para tráfego da web, gancho regra Olá tooour pools de IP. Se nós ligar Olá regra tooan pool IP, em vez de gancho Olá regra tooour VMs individualmente, podemos pode adicionar ou remover o VMs saudação do pool de IP. Balanceador de carga Olá ajusta automaticamente o fluxo de saudação do tráfego. Olá, exemplo a seguir cria uma regra denominada `myLoadBalancerRuleWeb` toomap TCP porta 80 tooport 80:

```azurecli
azure network lb rule create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myLoadBalancerRuleWeb --protocol tcp \
  --frontend-port 80 --backend-port 80 --frontend-ip-name myFrontEndPool \
  --backend-address-pool-name myBackEndPool
```

Saída:

```azurecli
info:    Executing command network lb rule create
+ Looking up hello load balancer "myLoadBalancer"
warn:    Using default idle timeout: 4
warn:    Using default enable floating ip: false
warn:    Using default load distribution: Default
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myLoadBalancerRuleWeb
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    mySubnet port                   : 80
data:    Backend port                    : 80
data:    Enable floating IP              : false
data:    Load distribution               : Default
data:    Idle timeout in minutes         : 4
data:    mySubnet IP configuration id    : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool
data:    Backend address pool id         : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
info:    network lb rule create command OK
```

## <a name="create-a-load-balancer-health-probe"></a>Criar uma investigação de integridade do balanceador de carga
Uma integridade de teste periodicamente verificações Olá VMs que estão por trás de nossa toomake de Balanceador de carga se eles está operacional e respondendo toorequests conforme definido. Se não forem removidos da operação tooensure que os usuários não estão sendo direcionado toothem. Você pode definir a verificações personalizadas para a investigação de integridade hello, juntamente com os intervalos e valores de tempo limite. Para obter mais informações sobre investigações de integridade, consulte [Investigações do Balanceador de Carga](../../load-balancer/load-balancer-custom-probe-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Olá, exemplo a seguir cria um TCP integridade investigado nomeado `myHealthProbe`:

```azurecli
azure network lb probe create --resource-group myResourceGroup \
  --lb-name myLoadBalancer --name myHealthProbe --protocol "tcp" \
  --interval 15 --count 4
```

Saída:

```azurecli
info:    Executing command network lb probe create
warn:    Using default probe port: 80
+ Looking up hello load balancer "myLoadBalancer"
+ Updating load balancer "myLoadBalancer"
data:    Name                            : myHealthProbe
data:    Provisioning state              : Succeeded
data:    Protocol                        : Tcp
data:    Port                            : 80
data:    Interval in seconds             : 15
data:    Number of probes                : 4
info:    network lb probe create command OK
```

Aqui, especificamos um intervalo de 15 segundos para nossas verificações de integridade. Podemos pode perder a um máximo de quatro testes (um minuto) antes de Balanceador de carga Olá considera que hospedam Olá não está mais funcionando.

## <a name="verify-hello-load-balancer"></a>Verifique se o balanceador de carga Olá
Agora a configuração de Balanceador de carga de saudação é feita. Aqui estão as etapas hello:

1. Você criou um balanceador de carga.
2. Você criou um pool IP de front-end e atribuído um tooit IP público.
3. Você criou um pool de IPs de back-end ao qual as VMs podem se conectar.
4. Você criou regras NAT que permitem SSH toohello VMs para gerenciamento, juntamente com uma regra que permite que a porta TCP 80 para o nosso aplicativo web.
5. Você adicionou uma saudação de seleção de tooperiodically de investigação de integridade VMs. Essa investigação de integridade garante que os usuários não tentam tooaccess uma máquina virtual que não está funcionando ou que serve o conteúdo.

Vamos ver como seu balanceador de carga está agora:

```azurecli
azure network lb show --resource-group myResourceGroup \
  --name myLoadBalancer --json | jq '.'
```

Saída:

```json
{
  "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
  "provisioningState": "Succeeded",
  "resourceGuid": "f1446acb-09ba-44d9-b8b6-849d9983dc09",
  "outboundNatRules": [],
  "inboundNatPools": [],
  "inboundNatRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH1",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4222,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    },
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleSSH2",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "protocol": "Tcp",
      "mySubnetPort": 4223,
      "backendPort": 22,
      "idleTimeoutInMinutes": 4,
      "enableFloatingIP": false,
      "provisioningState": "Succeeded"
    }
  ],
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer",
  "name": "myLoadBalancer",
  "type": "Microsoft.Network/loadBalancers",
  "location": "westeurope",
  "mySubnetIPConfigurations": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myFrontEndPool",
      "provisioningState": "Succeeded",
      "publicIPAddress": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/publicIPAddresses/myPublicIP"
      },
      "privateIPAllocationMethod": "Dynamic",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "inboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        },
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
    }
  ],
  "backendAddressPools": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myBackEndPool",
      "provisioningState": "Succeeded",
      "loadBalancingRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb"
        }
      ],
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
    }
  ],
  "loadBalancingRules": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myLoadBalancerRuleWeb",
      "provisioningState": "Succeeded",
      "enableFloatingIP": false,
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/loadBalancingRules/myLoadBalancerRuleWeb",
      "mySubnetIPConfiguration": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/mySubnetIPConfigurations/myFrontEndPool"
      },
      "backendAddressPool": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
      },
      "protocol": "Tcp",
      "loadDistribution": "Default",
      "mySubnetPort": 80,
      "backendPort": 80,
      "idleTimeoutInMinutes": 4
    }
  ],
  "probes": [
    {
      "etag": "W/\"62a7c8e7-859c-48d3-8e76-5e078c5e4a02\"",
      "name": "myHealthProbe",
      "provisioningState": "Succeeded",
      "numberOfProbes": 4,
      "intervalInSeconds": 15,
      "port": 80,
      "protocol": "Tcp",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/probes/myHealthProbe"
    }
  ]
}
```

## <a name="create-an-nic-toouse-with-hello-linux-vm"></a>Criar uma NIC toouse com hello VM do Linux
As NICs estão disponíveis por meio de programação porque você pode aplicar regras tootheir uso. Você também pode ter mais de uma. Seguir Olá `azure network nic create` de comando, ligar o pool IP hello NIC toohello carga back-end e associá-lo a saudação tráfego de SSH de toopermit de regra de NAT.

Substituir saudação `#####-###-###` seções com sua ID de assinatura do Azure. Sua assinatura ID é observado na saída de saudação do `jq` ao examinar recursos Olá que você está criando. Você também pode exibir sua ID de assinatura com `azure account list`.

Olá, exemplo a seguir cria uma NIC chamada `myNic1`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic1 \
  --lb-address-pool-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
```

Saída:

```azurecli
info:    Executing command network nic create
+ Looking up hello subnet "mySubnet"
+ Looking up hello network interface "myNic1"
+ Creating network interface "myNic1"
data:    Id                              : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1
data:    Name                            : myNic1
data:    Type                            : Microsoft.Network/networkInterfaces
data:    Location                        : westeurope
data:    Provisioning state              : Succeeded
data:    Enable IP forwarding            : false
data:    IP configurations:
data:      Name                          : Nic-IP-config
data:      Provisioning state            : Succeeded
data:      Private IP address            : 192.168.1.4
data:      Private IP allocation method  : Dynamic
data:      Subnet                        : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet
data:      Load balancer backend address pools:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool
data:      Load balancer inbound NAT rules:
data:        Id                          : /subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1
data:
info:    network nic create command OK
```

Você pode ver detalhes Olá examinando os recursos de saudação diretamente. Examinar o recurso hello usando Olá `azure network nic show` comando:

```azurecli
azure network nic show myResourceGroup myNic1 --json | jq '.'
```

Saída:

```json
{
  "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
  "provisioningState": "Succeeded",
  "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1",
  "name": "myNic1",
  "type": "Microsoft.Network/networkInterfaces",
  "location": "westeurope",
  "ipConfigurations": [
    {
      "etag": "W/\"fc1eaaa1-ee55-45bd-b847-5a08c7f4264a\"",
      "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/networkInterfaces/myNic1/ipConfigurations/Nic-IP-config",
      "loadBalancerBackendAddressPools": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool"
        }
      ],
      "loadBalancerInboundNatRules": [
        {
          "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH1"
        }
      ],
      "privateIPAddress": "192.168.1.4",
      "privateIPAllocationMethod": "Dynamic",
      "subnet": {
        "id": "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet"
      },
      "provisioningState": "Succeeded",
      "name": "Nic-IP-config"
    }
  ],
  "dnsSettings": {
    "appliedDnsServers": [],
    "dnsServers": []
  },
  "enableIPForwarding": false,
  "resourceGuid": "a20258b8-6361-45f6-b1b4-27ffed28798c"
}
```

Agora podemos criar hello segundo NIC, capturando no pool IP de back-end tooour novamente. Esta regra NAT tempo Olá segundo permite o tráfego SSH. Olá, exemplo a seguir cria uma NIC chamada `myNic2`:

```azurecli
azure network nic create --resource-group myResourceGroup --location westeurope \
  --subnet-vnet-name myVnet --subnet-name mySubnet --name myNic2 \
  --lb-address-pool-ids  /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/backendAddressPools/myBackEndPool \
  --lb-inbound-nat-rule-ids /subscriptions/########-####-####-####-############/resourceGroups/myResourceGroup/providers/Microsoft.Network/loadBalancers/myLoadBalancer/inboundNatRules/myLoadBalancerRuleSSH2
```

## <a name="create-a-network-security-group-and-rules"></a>Criar um grupo de segurança de rede e suas regras
Agora podemos criar um grupo de segurança de rede e Olá regras de entrada que controlam acesso NIC toohello. Um grupo de segurança de rede pode ser aplicado tooa NIC ou sub-rede. Definir o fluxo de saudação toocontrol regras de tráfego dentro e fora de suas VMs. Olá, exemplo a seguir cria um grupo de segurança de rede denominado `myNetworkSecurityGroup`:

```azurecli
azure network nsg create --resource-group myResourceGroup --location westeurope \
  --name myNetworkSecurityGroup
```

Vamos adicionar regra de entrada hello para Olá NSG tooallow conexões na porta 22 (toosupport SSH) de entrada. Olá, exemplo a seguir cria uma regra denominada `myNetworkSecurityGroupRuleSSH` tooallow TCP na porta 22:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1000 --destination-port-range 22 --access allow \
  --name myNetworkSecurityGroupRuleSSH
```

Agora vamos adicionar regra de entrada hello para Olá NSG tooallow conexões na porta 80 (toosupport o tráfego da web) de entrada. Olá, exemplo a seguir cria uma regra denominada `myNetworkSecurityGroupRuleHTTP` tooallow TCP na porta 80:

```azurecli
azure network nsg rule create --resource-group myResourceGroup \
  --nsg-name myNetworkSecurityGroup --protocol tcp --direction inbound \
  --priority 1001 --destination-port-range 80 --access allow \
  --name myNetworkSecurityGroupRuleHTTP
```

> [!NOTE]
> regra de entrada Hello é um filtro para conexões de rede de entrada. Neste exemplo, podemos associar Olá NSG toohello NIC virtual VMs, que significa que qualquer solicitação tooport 22 é transmitido toohello NIC em nosso VM. Essa regra de entrada é sobre uma conexão de rede e não sobre um ponto de extremidade, que seria o caso em implantações clássicas. tooopen uma porta, você deve deixar Olá `--source-port-range` definido muito '\*' tooaccept (valor padrão de saudação) solicitações de entrada **qualquer** solicitando a porta. Normalmente, as portas são dinâmicas.
>
>

## <a name="bind-toohello-nic"></a>Associar toohello NIC
Associe Olá NSG toohello NICs. É preciso tooconnect nosso NICs com nosso grupo de segurança de rede. Execute os dois comandos, toohook backup dos nossos NICs:

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic1 \
  --network-security-group-name myNetworkSecurityGroup
```

```azurecli
azure network nic set --resource-group myResourceGroup --name myNic2 \
  --network-security-group-name myNetworkSecurityGroup
```

## <a name="create-an-availability-set"></a>Criar um conjunto de disponibilidade
Conjuntos de disponibilidade ajudam a difundir suas VMs em domínios de falha e domínios de atualização. Vamos criar um conjunto de disponibilidade para suas VMs. Olá, exemplo a seguir cria um conjunto nomeada de disponibilidade `myAvailabilitySet`:

```azurecli
azure availset create --resource-group myResourceGroup --location westeurope
  --name myAvailabilitySet
```

Os domínios de falha definem um agrupamento de máquinas virtuais que compartilham uma mesma fonte de alimentação e um mesmo comutador de rede. Por padrão, máquinas virtuais Olá configuradas em seu conjunto de disponibilidade são separadas em domínios de falha de toothree. ideia Olá é um problema de hardware em um desses domínios de falha não afeta todas as VMs que estão executando o aplicativo. Azure distribui automaticamente as VMs em domínios de falha de saudação quando colocando-os em um conjunto de disponibilidade.

Domínios de atualização indicam grupos de máquinas virtuais e o hardware físico subjacente que pode ser reinicializado no hello simultaneamente. ordem de saudação na qual os domínios de atualização são reiniciados pode não ser sequencial durante a manutenção planejada, mas é reinicializada somente uma atualização de cada vez. Mais uma vez, o Azure distribui automaticamente as VMs entre os domínios de atualização ao colocá-las em um site de disponibilidade.

Leia mais sobre [gerenciar a disponibilidade de saudação de VMs](manage-availability.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="create-hello-linux-vms"></a>Criar VMs do Linux Olá
Você criou os recursos de armazenamento e rede Olá VMs toosupport acessível pela Internet. Agora, vamos criar essas VMs e protegê-las com uma chave SSH que não tem senha. Nesse caso, vamos toocreate uma VM Ubuntu com base em Olá LTS mais recente. Localizaremos as informações dessa imagem usando `azure vm image list`, conforme descrito em [localização de imagens de VM do Azure](../windows/cli-ps-findimage.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Selecionamos uma imagem usando o comando Olá `azure vm image list westeurope canonical | grep LTS`. Neste caso, usamos `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`. Para o último campo de hello, passamos `latest` para que no futuro Olá sempre obtemos compilação mais recente do hello. (cadeia de caracteres de saudação usamos é `canonical:UbuntuServer:16.04.0-LTS:16.04.201608150`).

A próxima etapa é tooanyone familiar que já tenha criado um ssh chaves pública e privada do rsa emparelhar no Linux ou Mac usando **ssh-keygen - t rsa -b 2048**. Se não tiver pares de chave de certificado no seu diretório `~/.ssh` , você poderá criá-los:

* Automaticamente, usando Olá `azure vm create --generate-ssh-keys` opção.
* Manualmente, usando [Olá instruções toocreate-las por conta própria](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Como alternativa, você pode usar o hello `--admin-password` método tooauthenticate suas conexões SSH após Olá VM é criada. Esse método normalmente é menos seguro.

Criamos Olá VM fazendo com que todos os nossos recursos e informações junto com hello `azure vm create` comando:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM1 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic1 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

Saída:

```azurecli
info:    Executing command vm create
+ Looking up hello VM "myVM1"
info:    Verifying hello public key SSH file: /home/ahmet/.ssh/id_rsa.pub
info:    Using hello VM Size "Standard_DS1"
info:    hello [OS, Data] Disk or image configuration requires storage account
+ Looking up hello storage account mystorageaccount
+ Looking up hello availability set "myAvailabilitySet"
info:    Found an Availability set "myAvailabilitySet"
+ Looking up hello NIC "myNic1"
info:    Found an existing NIC "myNic1"
info:    Found an IP configuration with virtual network subnet id "/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myVnet/subnets/mySubnet" in hello NIC "myNic1"
info:    This is an NIC without publicIP configured
info:    hello storage URI 'https://mystorageaccount.blob.core.windows.net/' will be used for boot diagnostics settings, and it can be overwritten by hello parameter input of '--boot-diagnostics-storage-uri'.
info:    vm create command OK
```

Você pode conectar tooyour VM imediatamente usando suas chaves SSH padrão. Certifique-se de que você especifique a porta apropriada Olá já que estamos passando por meio do balanceador de carga de saudação. (Para nossa primeira VM, configuramos porta Olá NAT regra tooforward 4222 tooour VM.)

```bash
ssh ops@mypublicdns.westeurope.cloudapp.azure.com -p 4222
```

Saída:

```bash
hello authenticity of host '[mypublicdns.westeurope.cloudapp.azure.com]:4222 ([xx.xx.xx.xx]:4222)' can't be established.
ECDSA key fingerprint is 94:2d:d0:ce:6b:fb:7f:ad:5b:3c:78:93:75:82:12:f9.
Are you sure you want toocontinue connecting (yes/no)? yes
Warning: Permanently added '[mypublicdns.westeurope.cloudapp.azure.com]:4222,[xx.xx.xx.xx]:4222' (ECDSA) toohello list of known hosts.
Welcome tooUbuntu 16.04.1 LTS (GNU/Linux 4.4.0-34-generic x86_64)

 * Documentation:  https://help.ubuntu.com
 * Management:     https://landscape.canonical.com
 * Support:        https://ubuntu.com/advantage

  Get cloud support with Ubuntu Advantage Cloud Guest:
    http://www.ubuntu.com/business/services/cloud

0 packages can be updated.
0 updates are security updates.

ops@myVM1:~$
```

Vá em frente e crie sua segunda VM em Olá mesma maneira:

```azurecli
azure vm create \
  --resource-group myResourceGroup \
  --name myVM2 \
  --location westeurope \
  --os-type linux \
  --availset-name myAvailabilitySet \
  --nic-name myNic2 \
  --vnet-name myVnet \
  --vnet-subnet-name mySubnet \
  --storage-account-name mystorageaccount \
  --image-urn canonical:UbuntuServer:16.04.0-LTS:latest \
  --ssh-publickey-file ~/.ssh/id_rsa.pub \
  --admin-username azureuser
```

E agora você pode usar o hello `azure vm show myResourceGroup myVM1` tooexamine de comando que você criou. Neste ponto, você está executando suas VMs Ubuntu atrás de um balanceador de carga no Azure, em que só pode fazer logon com seu par de chaves SSH (porque as senhas estão desabilitadas). Instalar nginx ou httpd, implantar um aplicativo web e ver o tráfego de saudação fluxo por meio de tooboth de Balanceador de carga Olá de VMs de saudação.

```azurecli
azure vm show --resource-group myResourceGroup --name myVM1
```

Saída:

```azurecli
info:    Executing command vm show
+ Looking up hello VM "TestVM1"
+ Looking up hello NIC "myNic1"
data:    Id                              :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM1
data:    ProvisioningState               :Succeeded
data:    Name                            :myVM1
data:    Location                        :westeurope
data:    Type                            :Microsoft.Compute/virtualMachines
data:
data:    Hardware Profile:
data:      Size                          :Standard_DS1
data:
data:    Storage Profile:
data:      Image reference:
data:        Publisher                   :canonical
data:        Offer                       :UbuntuServer
data:        Sku                         :16.04.0-LTS
data:        Version                     :latest
data:
data:      OS Disk:
data:        OSType                      :Linux
data:        Name                        :clib45a8b650f4428a1-os-1471973896525
data:        Caching                     :ReadWrite
data:        CreateOption                :FromImage
data:        Vhd:
data:          Uri                       :https://mystorageaccount.blob.core.windows.net/vhds/clib45a8b650f4428a1-os-1471973896525.vhd
data:
data:    OS Profile:
data:      Computer Name                 :myVM1
data:      User Name                     :ops
data:      Linux Configuration:
data:        Disable Password Auth       :true
data:
data:    Network Profile:
data:      Network Interfaces:
data:        Network Interface #1:
data:          Primary                   :true
data:          MAC Address               :00-0D-3A-24-D4-AA
data:          Provisioning State        :Succeeded
data:          Name                      :LmyNic1
data:          Location                  :westeurope
data:
data:    AvailabilitySet:
data:      Id                            :/subscriptions/guid/resourceGroups/myResourceGroup/providers/Microsoft.Compute/availabilitySets/myAvailabilitySet
data:
data:    Diagnostics Profile:
data:      BootDiagnostics Enabled       :true
data:      BootDiagnostics StorageUri    :https://mystorageaccount.blob.core.windows.net/
data:
data:      Diagnostics Instance View:
info:    vm show command OK

```


## <a name="export-hello-environment-as-a-template"></a>Ambiente de saudação de exportação como um modelo
Agora que você criou esse ambiente, e se você quiser toocreate um ambiente de desenvolvimento adicional com hello os mesmos parâmetros, ou em um ambiente de produção que faz a correspondência? Gerenciador de recursos usa modelos JSON que define todos os parâmetros de saudação para seu ambiente. Crie ambientes inteiros fazendo referência a esse modelo JSON. Você pode [criar modelos JSON manualmente](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) ou exportar um modelo existente do ambiente toocreate Olá JSON para você:

```azurecli
azure group export --name myResourceGroup
```

Este comando cria Olá `myResourceGroup.json` arquivo no diretório de trabalho atual. Quando você cria um ambiente com base neste modelo, você será solicitado para todos os nomes de recurso hello, incluindo nomes de saudação para o balanceador de carga hello, interfaces de rede ou VMs. Você pode preencher esses nomes em seu arquivo de modelo adicionando Olá `-p` ou `--includeParameterDefaultValue` toohello parâmetro `azure group export` comando que foi mostrado anteriormente. Editar os nomes de recurso do JSON modelo toospecify hello, ou [criar um arquivo parameters.json](../../resource-group-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) que especifica os nomes de recursos de saudação.

toocreate um ambiente de seu modelo:

```azurecli
azure group deployment create --resource-group myNewResourceGroup \
  --template-file myResourceGroup.json
```

Talvez você queira tooread [mais informações sobre como toodeploy modelos](../../resource-group-template-deploy-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Saiba mais sobre como tooincrementally ambientes de atualização, use o arquivo de parâmetros de saudação e acessar os modelos de um único local de armazenamento.

## <a name="next-steps"></a>Próximas etapas
Agora você está pronto toobegin trabalhando com vários componentes de rede e máquinas virtuais. Você pode usar este toobuild do ambiente de exemplo do aplicativo usando os componentes principais do hello introduzidos aqui.
