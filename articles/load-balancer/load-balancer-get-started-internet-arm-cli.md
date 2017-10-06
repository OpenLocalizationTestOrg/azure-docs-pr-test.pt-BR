---
title: aaaCreate um voltados para Internet carregar balanceador - CLI do Azure | Microsoft Docs
description: "Saiba como um balanceador de carga voltado para Internet usando o Gerenciador de recursos de toocreate Olá CLI do Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: a8bcdd88-f94c-4537-8143-c710eaa86818
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: cadb5edb3b4a4e2f0813109d027eaafdc7ef7303
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-internet-load-balancer-using-hello-azure-cli"></a>Criando um balanceador de carga de internet usando Olá CLI do Azure

> [!div class="op_single_selector"]
> * [Portal](../load-balancer/load-balancer-get-started-internet-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-internet-arm-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-internet-arm-cli.md)
> * [Modelo](../load-balancer/load-balancer-get-started-internet-arm-template.md)

[!INCLUDE [load-balancer-get-started-internet-intro-include.md](../../includes/load-balancer-get-started-internet-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

Este artigo aborda o modelo de implantação do Gerenciador de recursos de saudação. Você também pode [Saiba como toocreate um voltados à Internet carregar balanceador de implantação clássico](load-balancer-get-started-internet-classic-portal.md)

[!INCLUDE [load-balancer-get-started-internet-scenario-include.md](../../includes/load-balancer-get-started-internet-scenario-include.md)]

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Implantar solução hello usando Olá CLI do Azure

Olá etapas a seguir mostra como toocreate um voltados à Internet carregar balanceador usando o Gerenciador de recursos do Azure com CLI. Com o Azure Resource Manager cada recurso é criado e configurado individualmente, em seguida, juntar toocreate um recurso.

Você deve criar e configurar Olá objetos toodeploy um balanceador de carga a seguir:

* Configuração de IP de front-end – contém endereços IP públicos para o tráfego de rede de entrada.
* Pool de endereços de back-end - contém interfaces de rede (NICs) para tráfego de rede de tooreceive Olá máquinas virtuais do balanceador de carga de saudação.
* Regras de balanceamento de carga - contém regras de mapeamento de uma porta pública em Olá tooport de Balanceador de carga no pool de endereços de back-end de saudação.
* Regras NAT de entrada - contém regras de mapeamento de uma porta pública na porta tooa do balanceador de carga Olá para uma máquina virtual no pool de endereços de back-end de saudação.
* Testes - contém integridade investigações usadas toocheck disponibilidade das instâncias de máquinas virtuais no pool de endereços de back-end de saudação.

Para obter mais informações, confira [Suporte do Azure Resource Manager para balanceador de carga](load-balancer-arm.md).

## <a name="set-up-cli-toouse-resource-manager"></a>Configurar CLI toouse Gerenciador de recursos

1. Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.
2. Executar Olá **modo de configuração do azure** modo do Gerenciador de tooResource do comando tooswitch, conforme mostrado abaixo.

    ```azurecli
        azure config mode arm
    ```

    Saída esperada:

        info:    New mode is arm

## <a name="create-a-virtual-network-and-a-public-ip-address-for-hello-front-end-ip-pool"></a>Criar uma rede virtual e um endereço IP público para o pool de IP de front-end de saudação

1. Criar uma rede virtual (VNet) denominada *NRPVnet* no local do Leste dos EUA hello usando um grupo de recursos denominado *NRPRG*.

    ```azurecli
        azure network vnet create NRPRG NRPVnet eastUS -a 10.0.0.0/16
    ```

    Crie uma sub-rede denominada *NRPVnetSubnet* com um bloco CIDR de 10.0.0.0/24 na *NRPVnet*.

    ```azurecli
        azure network vnet subnet create NRPRG NRPVnet NRPVnetSubnet -a 10.0.0.0/24
    ```

2. Criar um endereço IP público denominado *NRPPublicIP* toobe usado por um pool IP de front-end com o nome DNS *loadbalancernrp.eastus.cloudapp.azure.com*. comando de saudação abaixo usa o tipo de alocação estática hello e tempo limite de ociosidade de 4 minutos.

    ```azurecli
        azure network public-ip create -g NRPRG -n NRPPublicIP -l eastus -d loadbalancernrp -a static -i 4
    ```

   > [!IMPORTANT]
   > Balanceador de carga Olá usará o rótulo de domínio de saudação do IP público hello como seu FQDN. Esta uma alteração de implantação clássica, que usa o serviço de nuvem Olá Olá totalmente o nome de domínio qualificado (FQDN) do balanceador de carga.
   > Neste exemplo, hello FQDN é *loadbalancernrp.eastus.cloudapp.azure.com*.

## <a name="create-a-load-balancer"></a>Criar um balanceador de carga

Olá, comando a seguir cria um balanceador de carga denominado *NRPlb* em Olá *NRPRG* grupo de recursos em Olá *Leste dos EUA* local do Azure.

    ```azurecli
    azure network lb create NRPRG NRPlb eastus
    ```

## <a name="create-a-front-end-ip-pool-and-a-backend-address-pool"></a>Criar um pool de IPs de front-end e um pool de endereços de back-end
Este exemplo demonstra como toocreate Olá pool IP front-end que recebe o tráfego de rede entrada hello em hello balanceador de carga e Olá pool IP de back-end em que o pool de front-end Olá envia Olá tráfego de rede de balanceamento de carga.

1. Crie um pool IP de front-end associando Olá IP público criado na etapa anterior hello e balanceador de carga de saudação.

    ```azurecli
        azure network lb frontend-ip create nrpRG NRPlb NRPfrontendpool -i nrppublicip
    ```

2. Configurar um pool de endereços de back-end usado tooreceive o tráfego de entrada hello front-end do pool de IP.

    ```azurecli
        azure network lb address-pool create NRPRG NRPlb NRPbackendpool
    ```

## <a name="create-lb-rules-nat-rules-and-probe"></a>Criar regras de balanceamento de carga, regras NAT e investigação

Este exemplo cria Olá itens a seguir.

* regra de NAT tootranslate todo o tráfego de entrada na porta 21 tooport 22<sup>1</sup>
* regra de NAT tootranslate todo o tráfego de entrada na porta 23 tooport 22
* um toobalance de regra de Balanceador de carga todo o tráfego de entrada na porta 80 tooport 80 em Olá endereços no pool de back-end de saudação.
* um status de integridade de saudação do teste regra toocheck em uma página chamada *HealthProbe.aspx*.

<sup>1</sup> regras NAT são tooa associado instância de máquina virtual por trás do balanceador de carga de saudação. tráfego de rede de saudação que chegam a porta 21 é enviado tooa específico de máquina virtual na porta 22 associado a esta regra NAT. Você deve especificar um protocolo (UDP ou TCP) para uma regra NAT. Os dois protocolos não podem ser atribuído toohello a mesma porta.

1. Crie regras NAT de saudação.

    ```azurecli
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh1 --protocol tcp --frontend-port 21 --backend-port 22
        azure network lb inbound-nat-rule create --resource-group nrprg --lb-name nrplb --name ssh2 --protocol tcp --frontend-port 23 --backend-port 22
    ```

2. Crie uma regra de balanceador de carga.

    ```azurecli
        azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule --protocol tcp --frontend-port 80 --backend-port 80 --frontend-ip-name NRPfrontendpool --backend-address-pool-name NRPbackendpool
    ```

3. Crie um teste de integridade.

    ```azurecli
        azure network lb probe create --resource-group nrprg --lb-name nrplb --name healthprobe --protocol "http" --port 80 --path healthprobe.aspx --interval 15 --count 4
    ```

4. Verifique suas configurações.

    ```azurecli
        azure network lb show nrprg nrplb
    ```

    Saída esperada:

        info:    Executing command network lb show
        + Looking up hello load balancer "nrplb"
        + Looking up hello public ip "NRPPublicIP"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb
        data:    Name                            : nrplb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : eastus
        data:    Provisioning State              : Succeeded
        data:    Frontend IP configurations:
        data:      Name                          : NRPfrontendpool
        data:      Provisioning state            : Succeeded
        data:      Public IP address id          : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/publicIPAddresses/NRPPublicIP
        data:      Public IP allocation method   : Static
        data:      Public IP address             : 40.114.13.145
        data:
        data:    Backend address pools:
        data:      Name                          : NRPbackendpool
        data:      Provisioning state            : Succeeded
        data:
        data:    Load balancing rules:
        data:      Name                          : HTTP
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 80
        data:      Backend port                  : 80
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:      Backend address pool          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:
        data:    Inbound NAT rules:
        data:      Name                          : ssh1
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 21
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:      Name                          : ssh2
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Tcp
        data:      Frontend port                 : 23
        data:      Backend port                  : 22
        data:      Enable floating IP            : false
        data:      Idle timeout in minutes       : 4
        data:      Frontend IP configuration     : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/frontendIPConfigurations/NRPfrontendpool
        data:
        data:    Probes:
        data:      Name                          : healthprobe
        data:      Provisioning state            : Succeeded
        data:      Protocol                      : Http
        data:      Port                          : 80
        data:      Interval in seconds           : 15
        data:      Number of probes              : 4
        data:
        info:    network lb show command OK

## <a name="create-nics"></a>Criar NICs

Você precisa toocreate NICs (ou modificar as existentes) e associá-los tooNAT regras, regras de Balanceador de carga e testes.

1. Criar uma NIC denominada *lb-nic1 ser*e associá-lo a saudação *rdp1* NAT regra e hello *NRPbackendpool* pool de endereços de back-end.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" eastus
    ```

    Saída esperada:

        info:    Executing command network nic create
        + Looking up hello network interface "lb-nic1-be"
        + Looking up hello subnet "nrpvnetsubnet"
        + Creating network interface "lb-nic1-be"
        + Looking up hello network interface "lb-nic1-be"
        data:    Id                              : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/networkInterfaces/lb-nic1-be
        data:    Name                            : lb-nic1-be
        data:    Type                            : Microsoft.Network/networkInterfaces
        data:    Location                        : eastus
        data:    Provisioning state              : Succeeded
        data:    Enable IP forwarding            : false
        data:    IP configurations:
        data:      Name                          : NIC-config
        data:      Provisioning state            : Succeeded
        data:      Private IP address            : 10.0.0.4
        data:      Private IP Allocation Method  : Dynamic
        data:      Subnet                        : /subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet
        data:      Load balancer backend address pools
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool
        data:      Load balancer inbound NAT rules:
        data:        Id                          : /subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1
        data:
        info:    network nic create command OK

2. Criar uma NIC denominada *lb-nic2 ser*e associá-lo a saudação *rdp2* NAT regra e hello *NRPbackendpool* pool de endereços de back-end.

    ```azurecli
        azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/NRPbackendpool" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" eastus
    ```

3. Criar uma máquina virtual (VM) denominada *web1*e associá-lo a saudação NIC denominado *lb-nic1 ser*. Uma conta de armazenamento chamado *web1nrp* foi criado antes de executar o comando de saudação abaixo.

    ```azurecli
        azure vm create --resource-group nrprg --name web1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

    > [!IMPORTANT]
    > Máquinas virtuais em um toobe de necessidade de Balanceador de carga no hello mesmo conjunto de disponibilidade. Use `azure availset create` toocreate um conjunto de disponibilidade.

    saída de Hello deve ser a seguir toohello semelhante:

        info:    Executing command vm create
        + Looking up hello VM "web1"
        Enter username: azureuser
        Enter password for azureuser: *********
        Confirm password: *********
        info:    Using hello VM Size "Standard_A1"
        info:    hello [OS, Data] Disk or image configuration requires storage account
        + Looking up hello storage account web1nrp
        + Looking up hello availability set "nrp-avset"
        info:    Found an Availability set "nrp-avset"
        + Looking up hello NIC "lb-nic1-be"
        info:    Found an existing NIC "lb-nic1-be"
        info:    Found an IP configuration with virtual network subnet id "/subscriptions/####################################/resourceGroups/NRPRG/providers/Microsoft.Network/virtualNetworks/NRPVnet/subnets/NRPVnetSubnet" in hello NIC "lb-nic1-be"
        info:    This is a NIC without publicIP configured
        + Creating VM "web1"
        info:    vm create command OK

    > [!NOTE]
    > mensagem informativa Olá **isso é uma NIC sem publicIP configurado** é esperado porque hello NIC criada Olá balanceador de carga conectando tooInternet usando Olá pública IP balanceador de carga.

    Desde Olá *lb-nic1 ser* NIC está associada à saudação *rdp1* regra de NAT, você pode conectar-se muito*web1* usando o RDP pela porta 3441 no balanceador de carga de saudação.

4. Criar uma máquina virtual (VM) denominada *web2*e associá-lo a saudação NIC denominado *lb-nic2 ser*. Uma conta de armazenamento chamado *web1nrp* foi criado antes de executar o comando de saudação abaixo.

    ```azurecli
        azure vm create --resource-group nrprg --name web2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="update-an-existing-load-balancer"></a>Atualizar um balanceador de carga existente
Você pode adicionar regras ao fazer referência a um balanceador de carga existente. No exemplo a seguir hello, uma nova regra de Balanceador de carga é adicionada balanceador de carga existente tooan **NRPlb**

```azurecli
azure network lb rule create --resource-group nrprg --lb-name nrplb --name lbrule2 --protocol tcp --frontend-port 8080 --backend-port 8051 --frontend-ip-name frontendnrppool --backend-address-pool-name NRPbackendpool
```

## <a name="delete-a-load-balancer"></a>Excluir um balanceador de carga
Use Olá comando tooremove um balanceador de carga a seguir:

```azurecli
azure network lb delete --resource-group nrprg --name nrplb
```

## <a name="next-steps"></a>Próximas etapas
[Introdução à configuração de um balanceador de carga interno](load-balancer-get-started-ilb-arm-cli.md)

[Configurar um modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
