---
title: Balanceador de carga aaaCreate um com a Internet com o IPv6 - CLI do Azure | Microsoft Docs
description: "Saiba como toocreate um Internet oposto balanceador de carga com o IPv6 no Gerenciador de recursos do Azure usando Olá CLI do Azure"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
tags: azure-resource-manager
keywords: "ipv6, azure load balancer, pilha dual, ip público, ipv6 nativo, móvel, iot"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 7ff75ac90d74a74e3d0c27672b36fbd955a086a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-internet-facing-load-balancer-with-ipv6-in-azure-resource-manager-using-hello-azure-cli"></a>Criar uma balanceador de carga com o IPv6 no Azure Resource Manager usando Olá CLI do Azure da Internet

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [CLI do Azure](load-balancer-ipv6-internet-cli.md)
> * [Modelo](load-balancer-ipv6-internet-template.md)

Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP). o balanceador de carga Olá fornece alta disponibilidade através da distribuição de tráfego de entrada entre instâncias do serviço de integridade em serviços de nuvem ou máquinas virtuais em um conjunto de Balanceador de carga. O Azure Load Balancer também pode apresentar esses serviços em várias portas, vários endereços IP ou ambos.

## <a name="example-deployment-scenario"></a>Exemplo de cenário de implantação

Olá, diagrama a seguir ilustra Olá solução balanceamento de carga que está sendo implantado usando o modelo de exemplo hello descrito neste artigo.

![Cenário com o balanceador de carga](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

Nesse cenário, você criará hello Azure recursos a seguir:

* duas VMs (máquinas virtuais)
* uma interface de rede virtual para cada VM com endereços IPv4 e IPv6 atribuídos
* um balanceador de carga voltado para a Internet com um IPv4 e um endereço IP público IPv6
* um conjunto de disponibilidade toothat contém Olá duas VMs
* dois carregar balanceamento regras toomap Olá VIPs toohello privados pontos de extremidade públicos

## <a name="deploying-hello-solution-using-hello-azure-cli"></a>Implantar solução hello usando Olá CLI do Azure

Olá etapas a seguir mostra como toocreate um voltados à Internet carregar balanceador usando o Gerenciador de recursos do Azure com CLI. No Gerenciador de recursos do Azure, cada recurso é criado e configurado individualmente e juntar toocreate um recurso.

toodeploy um balanceador de carga, que você crie e configure Olá seguintes objetos:

* Configuração de IP de front-end – contém endereços IP públicos para o tráfego de rede de entrada.
* Pool de endereços de back-end - contém interfaces de rede (NICs) para tráfego de rede de tooreceive Olá máquinas virtuais do balanceador de carga de saudação.
* Regras de balanceamento de carga - contém regras de mapeamento de uma porta pública em Olá tooport de Balanceador de carga no pool de endereços de back-end de saudação.
* Regras NAT de entrada - contém regras de mapeamento de uma porta pública na porta tooa do balanceador de carga Olá para uma máquina virtual no pool de endereços de back-end de saudação.
* Testes - contém integridade investigações usadas toocheck disponibilidade das instâncias de máquinas virtuais no pool de endereços de back-end de saudação.

Para saber mais, confira [Suporte do Azure Resource Manager para Balanceador de Carga](load-balancer-arm.md).

## <a name="set-up-your-cli-environment-toouse-azure-resource-manager"></a>Configurar seu ambiente de CLI toouse Gerenciador de recursos do Azure

Neste exemplo, estamos executando ferramentas CLI de saudação em uma janela de comando do PowerShell. Não estamos usando cmdlets do PowerShell do Azure Olá mas usamos a legibilidade de tooimprove de recursos e reutilização de script do PowerShell.

1. Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.
2. Executar Olá **modo de configuração do azure** modo do comando tooswitch tooResource Gerenciador.

    ```azurecli
    azure config mode arm
    ```

    Saída esperada:

        info:    New mode is arm

3. Entre no tooAzure e obter uma lista de assinaturas.

    ```azurecli
    azure login
    ```

    Inserir as credenciais do Azure quando solicitado.

    ```azurecli
    azure account list
    ```

    Escolha a assinatura Olá que deseja toouse. Anote a Id de assinatura de saudação para a próxima etapa de saudação.

4. Configure variáveis do PowerShell para uso com os comandos CLI hello.

    ```powershell
    $subscriptionid = "########-####-####-####-############"  # enter subscription id
    $location = "southcentralus"
    $rgName = "pscontosorg1southctrlus09152016"
    $vnetName = "contosoIPv4Vnet"
    $vnetPrefix = "10.0.0.0/16"
    $subnet1Name = "clicontosoIPv4Subnet1"
    $subnet1Prefix = "10.0.0.0/24"
    $subnet2Name = "clicontosoIPv4Subnet2"
    $subnet2Prefix = "10.0.1.0/24"
    $dnsLabel = "contoso09152016"
    $lbName = "myIPv4IPv6Lb"
    ```

## <a name="create-a-resource-group-a-load-balancer-a-virtual-network-and-subnets"></a>Crie um grupo de recursos, um balanceador de carga, uma rede virtual e sub-redes

1. Criar um grupos de recursos

    ```azurecli
    azure group create $rgName $location
    ```

2. Criar um balanceador de carga

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. Criar uma rede virtual (VNet).

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

    Criar duas sub-redes nessa VNet.

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-hello-front-end-pool"></a>Crie endereços IP públicos para o pool de front-end Olá

1. Definir variáveis do PowerShell Olá

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. Crie um público Olá front-end IP pool de endereços IP.

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > Balanceador de carga Olá usa o rótulo de domínio de saudação do IP público Olá como seu FQDN. Esta uma alteração de implantação clássica, que usa o nome do serviço de nuvem Olá Olá FQDN do balanceador de carga.
    > Neste exemplo, hello FQDN é *contoso09152016.southcentralus.cloudapp.azure.com*.

## <a name="create-front-end-and-back-end-pools"></a>Criar pools de front-end e back-end

Este exemplo cria um pool IP de front-end Olá que recebe o tráfego de rede entrada hello no balanceador de carga hello e pool IP de back-end Olá onde o pool de front-end Olá envia tráfego de rede com balanceamento de carga de saudação.

1. Definir variáveis do PowerShell Olá

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. Crie um pool IP de front-end associando Olá IP público criado na etapa anterior hello e balanceador de carga de saudação.

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-hello-probe-nat-rules-and-lb-rules"></a>Criar regras de balanceamento de carga, regras NAT e investigação Olá

Este exemplo cria Olá itens a seguir:

* um toocheck de regra de teste para a porta 80 do tooTCP de conectividade
* um NAT regra tootranslate todo o tráfego de entrada na porta 3389 tooport 3389 para RDP<sup>1</sup>
* um NAT regra tootranslate todo o tráfego de entrada na porta 3391 tooport 3389 para RDP<sup>1</sup>
* um toobalance de regra de Balanceador de carga todo o tráfego de entrada na porta 80 tooport 80 em Olá endereços no pool de back-end de saudação.

<sup>1</sup> regras NAT são tooa associado instância de máquina virtual por trás do balanceador de carga de saudação. tráfego de rede de saudação que chegam na porta 3389 é enviado toohello específico de máquina virtual e a porta associada à regra NAT hello. Você deve especificar um protocolo (UDP ou TCP) para uma regra NAT. Os dois protocolos não podem ser atribuído toohello a mesma porta.

1. Definir variáveis do PowerShell Olá

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. Criar a investigação de saudação

    Olá exemplo a seguir cria uma investigação TCP verifica para conectividade tooback-end a porta TCP 80 a cada 15 segundos. Ele marcará recursos de back-end Olá indisponível após duas falhas consecutivas.

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. Criar regras de NAT de entrada que permitem conexões RDP toohello recursos de back-end

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. Criar regras que enviam tráfego de portas de back-end toodifferent dependendo de qual solicitação de saudação do front-end recebida de um balanceador de carga

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. Verifique suas configurações

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    Saída esperada:

        info:    Executing command network lb show
        info:    Looking up hello load balancer "myIPv4IPv6Lb"
        data:    Id                              : /subscriptions/########-####-####-####-############/resourceGroups/pscontosorg1southctrlus09152016/providers/Microsoft.Network/loadBalancers/myIPv4IPv6Lb
        data:    Name                            : myIPv4IPv6Lb
        data:    Type                            : Microsoft.Network/loadBalancers
        data:    Location                        : southcentralus
        data:    Provisioning state              : Succeeded
        data:
        data:    Frontend IP configurations:
        data:    Name             Provisioning state  Private IP allocation  Private IP   Subnet  Public IP
        data:    ---------------  ------------------  ---------------------  -----------  ------  ---------
        data:    FrontendVipIPv4  Succeeded           Dynamic                                     myIPv4Vip
        data:    FrontendVipIPv6  Succeeded           Dynamic                                     myIPv6Vip
        data:
        data:    Probes:
        data:    Name                 Provisioning state  Protocol  Port  Path  Interval  Count
        data:    -------------------  ------------------  --------  ----  ----  --------  -----
        data:    ProbeForIPv4AndIPv6  Succeeded           Tcp       80          15        2
        data:
        data:    Backend Address Pools:
        data:    Name             Provisioning state
        data:    ---------------  ------------------
        data:    BackendPoolIPv4  Succeeded
        data:    BackendPoolIPv6  Succeeded
        data:
        data:    Load Balancing Rules:
        data:    Name                  Provisioning state  Load distribution  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    --------------------  ------------------  -----------------  --------  -------------  ------------  ------------------  -----------------------
        data:    LBRuleForIPv4-Port80  Succeeded           Default            Tcp       80             80            false               4
        data:    LBRuleForIPv6-Port80  Succeeded           Default            Tcp       80             8080          false               4
        data:
        data:    Inbound NAT Rules:
        data:    Name                 Provisioning state  Protocol  Frontend port  Backend port  Enable floating IP  Idle timeout in minutes
        data:    -------------------  ------------------  --------  -------------  ------------  ------------------  -----------------------
        data:    NatRule-For-Rdp-VM1  Succeeded           Tcp       3389           3389          false               4
        data:    NatRule-For-Rdp-VM2  Succeeded           Tcp       3391           3389          false               4
        info:    network lb show

## <a name="create-nics"></a>Criar NICs

Criar NICs e associá-los tooNAT regras, regras de Balanceador de carga e testes.

1. Definir variáveis do PowerShell Olá

    ```powershell
    $nic1Name = "myIPv4IPv6Nic1"
    $nic2Name = "myIPv4IPv6Nic2"
    $subnet1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet1Name"
    $subnet2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgName/providers/Microsoft.Network/VirtualNetworks/$vnetName/subnets/$subnet2Name"
    $backendAddressPoolV4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV4Name"
    $backendAddressPoolV6Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/backendAddressPools/$backendAddressPoolV6Name"
    $natRule1V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule1V4Name"
    $natRule2V4Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/loadbalancers/$lbName/inboundNatRules/$natRule2V4Name"
    ```

2. Crie um NIC para cada back-end e adicione uma configuração de IPv6.

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-hello-back-end-vm-resources-and-attach-each-nic"></a>Criar recursos de back-end de saudação VM e conecte cada NIC

toocreate VMs, você deve ter uma conta de armazenamento. Balanceamento de carga, Olá VMs necessário toobe membros de um conjunto de disponibilidade. Para saber mais sobre a criação de VMs, consulte [Criar uma VM do Azure usando o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json)

1. Definir variáveis do PowerShell Olá

    ```powershell
    $storageAccountName = "ps08092016v6sa0"
    $availabilitySetName = "myIPv4IPv6AvailabilitySet"
    $vm1Name = "myIPv4IPv6VM1"
    $vm2Name = "myIPv4IPv6VM2"
    $nic1Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic1Name"
    $nic2Id = "/subscriptions/$subscriptionid/resourceGroups/$rgname/providers/Microsoft.Network/networkInterfaces/$nic2Name"
    $disk1Name = "WindowsVMosDisk1"
    $disk2Name = "WindowsVMosDisk2"
    $osDisk1Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk1Name.vhd"
    $osDisk2Uri = "https://$storageAccountName.blob.core.windows.net/vhds/$disk2Name.vhd"
    $imageurn "MicrosoftWindowsServer:WindowsServer:2012-R2-Datacenter:latest"
    $vmUserName = "vmUser"
    $mySecurePassword = "PlainTextPassword*1"
    ```

    > [!WARNING]
    > Este exemplo usa Olá username e password para VMs Olá em texto não criptografado. Apropriado deve ter cuidado ao usando as credenciais em Olá claro. Para um método mais seguro de tratamento de credenciais no PowerShell, consulte Olá [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.

2. Criar conjunto de disponibilidade e a conta de armazenamento Olá

    Quando você cria Olá VMs, você pode usar uma conta de armazenamento existente. saudação de comando a seguir cria uma nova conta de armazenamento.

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

    Em seguida, crie o conjunto de disponibilidade de saudação.

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

3. Criar máquinas virtuais de saudação com NICs Olá associado

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a>Próximas etapas

[Introdução à configuração de um balanceador de carga interno](load-balancer-get-started-ilb-arm-cli.md)

[Configurar um modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
