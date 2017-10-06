---
title: aaaCreate um interno carregar balanceador - CLI do Azure | Microsoft Docs
description: "Saiba como toocreate um balanceador de carga interno usando Olá CLI do Azure no Gerenciador de recursos"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
ms.assetid: c7a24e92-b4da-43c0-90f2-841c1b7ce489
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 3aea6fdb07600f0d661ec6b8ffc784b03380a127
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internal-load-balancer-by-using-hello-azure-cli"></a>Criar um balanceador de carga interno usando Olá CLI do Azure

> [!div class="op_single_selector"]
> * [Portal do Azure](../load-balancer/load-balancer-get-started-ilb-arm-portal.md)
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-arm-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-ilb-arm-cli.md)
> * [Modelo](../load-balancer/load-balancer-get-started-ilb-arm-template.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!NOTE]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação do hello Gerenciador de recursos, a Microsoft recomenda para a maioria das novas implantações em vez da saudação [modelo de implantação clássico](load-balancer-get-started-ilb-classic-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="deploy-hello-solution-by-using-hello-azure-cli"></a>Implantar solução hello usando Olá CLI do Azure

Olá, as etapas a seguir mostra como toocreate um voltados para Internet balanceador de carga usando o Gerenciador de recursos do Azure com CLI. No Gerenciador de recursos do Azure, cada recurso é criado e configurado individualmente e juntar toocreate um recurso.

Você precisa toocreate e configurar Olá objetos toodeploy um balanceador de carga a seguir:

* **Configuração de IP de front-end**: contém endereços IP públicos para o tráfego de rede de entrada
* **Pool de endereços de back-end**: contém as interfaces de rede (NICs) que permitam o tráfego de rede de tooreceive Olá máquinas virtuais do balanceador de carga Olá
* **Regras de balanceamento de carga**: contém regras que mapeiam uma porta pública Olá tooport de Balanceador de carga no pool de endereços de back-end de saudação
* **Regras NAT de entrada**: contém regras que mapeiam uma porta pública na porta tooa do balanceador de carga Olá para uma máquina virtual no pool de endereços de back-end de saudação
* **Testes**: contém investigações de integridade que são usadas toocheck Olá disponibilidade das instâncias de máquinas virtuais no pool de endereços de back-end de saudação

Para saber mais, confira [Suporte do Azure Resource Manager para Balanceador de Carga](load-balancer-arm.md).

## <a name="set-up-cli-toouse-resource-manager"></a>Configurar CLI toouse Gerenciador de recursos

1. Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md). Siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.
2. Executar Olá **modo de configuração do azure** comando tooswitch tooResource Manager modo, da seguinte maneira:

    ```azurecli
    azure config mode arm
    ```

    Saída esperada:

        info:    New mode is arm

## <a name="create-an-internal-load-balancer-step-by-step"></a>Criar um balanceador de carga interno, passo a passo

1. Entrar tooAzure.

    ```azurecli
    azure login
    ```

    Inserir as credenciais do Azure, quando for solicitado.

2. Alterar o modo de Gerenciador de recursos do hello comando ferramentas tooAzure.

    ```azurecli
    azure config mode arm
    ```

## <a name="create-a-resource-group"></a>Criar um grupo de recursos

Todos os recursos no Azure Resource Manager estão associados a um grupo de recursos. Se você ainda não fez isso, crie um grupo de recursos.

```azurecli
azure group create <resource group name> <location>
```

## <a name="create-an-internal-load-balancer-set"></a>Criar um conjunto do balanceador de carga interno

1. Criar um balanceador de carga interno

    Em Olá cenário a seguir, um grupo de recursos chamado nrprg é criado na região Leste dos EUA.

    ```azurecli
    azure network lb create --name nrprg --location eastus
    ```

   > [!NOTE]
   > Todos os recursos de um balanceador de carga interno, como redes virtuais e sub-redes da rede virtual, devem ser no hello mesmo grupo de recursos e no hello mesma região.

2. Crie um endereço IP de front-end para o balanceador de carga interno hello.

    endereço IP de saudação que você usa deve ser dentro do intervalo de sub-rede de saudação da sua rede virtual.

    ```azurecli
    azure network lb frontend-ip create --resource-group nrprg --lb-name ilbset --name feilb --private-ip-address 10.0.0.7 --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet
    ```

3. Crie pool de endereços de back-end de saudação.

    ```azurecli
    azure network lb address-pool create --resource-group nrprg --lb-name ilbset --name beilb
    ```

    Depois de definir um endereço IP de front-end e um pool de endereços de back-end, você poderá criar regras de balanceador de carga, regras NAT de entrada e investigações de integridade personalizadas.

4. Crie uma regra de Balanceador de carga para o balanceador de carga interno hello.

    Quando você segue etapas anteriores Olá, o comando Olá cria uma regra de Balanceador de carga para escuta tooport 1433 no pool de front-end do hello e envio com balanceamento de carga de rede tráfego toohello back-end pool de endereços, usando a porta 1433.

    ```azurecli
    azure network lb rule create --resource-group nrprg --lb-name ilbset --name ilbrule --protocol tcp --frontend-port 1433 --backend-port 1433 --frontend-ip-name feilb --backend-address-pool-name beilb
    ```

5. Crie regras NAT de entrada.

    Regras de NAT de entrada são usados toocreate pontos de extremidade em um balanceador de carga que vão tooa instância de máquina virtual específica. etapas anteriores Olá criadas duas regras NAT para a área de trabalho remota.

    ```azurecli
    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule1 --protocol TCP --frontend-port 5432 --backend-port 3389

    azure network lb inbound-nat-rule create --resource-group nrprg --lb-name ilbset --name NATrule2 --protocol TCP --frontend-port 5433 --backend-port 3389
    ```

6. Crie testes de integridade Olá balanceador de carga.

    Um teste de integridade verifica todos os toomake de instâncias de máquina virtual-se de que eles podem enviar o tráfego de rede. instância de máquina virtual de saudação com verificações de investigação com falha será removida do balanceador de carga Olá até que ele ficar online novamente e uma verificação de teste determina que ele esteja íntegro.

    ```azurecli
    azure network lb probe create --resource-group nrprg --lb-name ilbset --name ilbprobe --protocol tcp --interval 300 --count 4
    ```

    > [!NOTE]
    > plataforma do Microsoft Azure Olá usa um endereço IPv4 estático, roteável publicamente para uma variedade de cenários administrativos. endereço IP de saudação é 168.63.129.16. Esse endereço IP não deve ser bloqueado por nenhum firewall porque ele pode causar um comportamento inesperado.
    > Com relação tooAzure balanceamento de carga interno, esse endereço IP é usado pelo monitoramento de testes do estado de integridade de Olá Olá carga balanceador toodetermine para máquinas virtuais em um conjunto com balanceamento de carga. Se um grupo de segurança de rede é usada toorestrict tráfego tooAzure VMs em um conjunto de balanceamento de carga internamente ou sub-rede da rede virtual tooa aplicada, certifique-se de que uma regra de segurança de rede é adicionada tooallow tráfego de 168.63.129.16.

## <a name="create-nics"></a>Criar NICs

Você precisa toocreate NICs (ou modificar as existentes) e associá-los tooNAT regras, regras de Balanceador de carga e testes.

1. Criar uma NIC denominado *lb-nic1 ser*e, em seguida, associe-Olá *rdp1* NAT regra e hello *beilb* pool de endereços de back-end.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic1-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp1" --location eastus
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

2. Criar uma NIC denominado *lb-nic2 ser*e, em seguida, associe-Olá *rdp2* NAT regra e hello *beilb* pool de endereços de back-end.

    ```azurecli
    azure network nic create --resource-group nrprg --name lb-nic2-be --subnet-name nrpvnetsubnet --subnet-vnet-name nrpvnet --lb-address-pool-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/backendAddressPools/beilb" --lb-inbound-nat-rule-ids "/subscriptions/####################################/resourceGroups/nrprg/providers/Microsoft.Network/loadBalancers/nrplb/inboundNatRules/rdp2" --location eastus
    ```

3. Criar uma máquina virtual denominada *DB1*e, em seguida, associe-Olá NIC denominado *lb-nic1 ser*. Uma conta de armazenamento chamado *web1nrp* é criado antes de saudação execuções de comando a seguir:

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB1 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic1-be --availset-name nrp-avset --storage-account-name web1nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```
    > [!IMPORTANT]
    > Máquinas virtuais em um toobe de necessidade de Balanceador de carga no hello mesmo conjunto de disponibilidade. Use `azure availset create` toocreate um conjunto de disponibilidade.

4. Criar uma máquina virtual (VM) denominada *DB2*e, em seguida, associe-Olá NIC denominado *lb-nic2 ser*. Uma conta de armazenamento chamado *web1nrp* foi criado antes de executar o comando a seguir de saudação.

    ```azurecli
    azure vm create --resource--resource-grouproup nrprg --name DB2 --location eastus --vnet-name nrpvnet --vnet-subnet-name nrpvnetsubnet --nic-name lb-nic2-be --availset-name nrp-avset --storage-account-name web2nrp --os-type Windows --image-urn MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:4.0.20150825
    ```

## <a name="delete-a-load-balancer"></a>Excluir um balanceador de carga

tooremove um balanceador de carga, use Olá comando a seguir:

```azurecli
azure network lb delete --resource-group nrprg --name ilbset
```

## <a name="next-steps"></a>Próximas etapas

[Configurar um modo de distribuição do balanceador de carga usando a afinidade de IP de origem](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)

