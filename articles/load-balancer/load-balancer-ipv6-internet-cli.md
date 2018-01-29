---
title: "Criar um balanceador de carga público com o IPv6 – CLI do Azure | Microsoft Docs"
description: "Saiba como criar um balanceador de carga público com IPv6 no Azure Resource Manager usando a CLI do Azure."
services: load-balancer
documentationcenter: na
author: KumudD
manager: timlt
tags: azure-resource-manager
keywords: "ipv6, azure load balancer, pilha dual, ip público, ipv6 nativo, móvel, iot"
ms.assetid: a1957c9c-9c1d-423e-9d5c-d71449bc1f37
ms.service: load-balancer
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 09/25/2017
ms.author: kumud
ms.openlocfilehash: 3abd47460999f7b059469a58a59a3e297e88effb
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="create-a-public-load-balancer-with-ipv6-in-azure-resource-manager-by-using-azure-cli"></a>Criar um balanceador de carga público com IPv6 no Azure Resource Manager usando a CLI do Azure

> [!div class="op_single_selector"]
> * [PowerShell](load-balancer-ipv6-internet-ps.md)
> * [CLI do Azure](load-balancer-ipv6-internet-cli.md)
> * [Modelo](load-balancer-ipv6-internet-template.md)

[!INCLUDE [load-balancer-basic-sku-include.md](../../includes/load-balancer-basic-sku-include.md)]

Um Azure Load Balancer é um balanceador de carga de Camada 4 (TCP, UDP). Os balanceadores de carga fornecem alta disponibilidade, distribuindo o tráfego de entrada entre instâncias do serviço íntegras em serviços de nuvem ou máquinas virtuais em um conjunto de balanceadores de carga. Os balanceadores de carga também podem apresentar esses serviços em várias portas, em vários endereços IP ou em ambos.

## <a name="example-deployment-scenario"></a>Exemplo de cenário de implantação

O diagrama a seguir ilustra a solução de balanceamento de carga que está sendo implantada usando o exemplo de modelo descrito neste artigo.

![Cenário com o balanceador de carga](./media/load-balancer-ipv6-internet-cli/lb-ipv6-scenario-cli.png)

Nesse cenário, você cria os seguintes recursos do Azure:

* Duas VMs (máquinas virtuais)
* Uma interface de rede virtual para cada VM com endereços IPv4 e IPv6 atribuídos
* Um balanceador de carga público com um endereço IP público IPv4 e um IPv6
* Um conjunto de disponibilidade que contém as duas VMs
* Duas regras de balanceamento de carga para mapear os VIPs públicos para os pontos de extremidade privados

## <a name="deploy-the-solution-by-using-azure-cli"></a>Implantar a solução usando a CLI do Azure

As etapas a seguir mostram como criar um balanceador de carga público usando o Azure Resource Manager com a CLI do Azure. Com o Azure Resource Manager, todos os recursos são criados e configurados individualmente e colocados juntos para criar um recurso.

Para implantar um balanceador de carga, crie e configure os seguintes objetos:

* **Configuração de IP de front-end**: contém endereços IP públicos para o tráfego de rede de entrada.
* **Pool de endereços de back-end**: contém NICs (interfaces de rede) para que as máquinas virtuais recebam o tráfego de rede do balanceador de carga.
* **Regras de balanceamento de carga**: contém regras que mapeiam uma porta pública no balanceador de carga para uma porta no pool de endereços de back-end.
* **Regras NAT de entrada**: contém regras de NAT (tradução de endereço de rede) que mapeiam uma porta pública no balanceador de carga para uma porta de uma máquina virtual específica no pool de endereços de back-end.
* **Investigações**: contém investigações de integridade usadas para verificar a disponibilidade de instâncias de máquinas virtuais no pool de endereços de back-end.

Para saber mais, confira [Suporte do Azure Resource Manager para Balanceador de Carga](load-balancer-arm.md).

## <a name="set-up-your-azure-cli-environment-to-use-azure-resource-manager"></a>Configurar seu ambiente da CLI do Azure para usar o Azure Resource Manager

Neste exemplo, você executa as ferramentas da CLI do Azure em uma janela de comando do PowerShell. Para melhorar a legibilidade e a reutilização, use os recursos de script do PowerShell, não os cmdlets do Azure PowerShell.

1. Se você nunca usou a CLI do Azure, confira [Instalar e configurar a CLI do Azure](../cli-install-nodejs.md) e siga as instruções até o ponto em que você seleciona sua conta e assinatura do Azure.

2. Execute o comando **azure config mode** para mudar para o modo do Resource Manager:

    ```azurecli
    azure config mode arm
    ```

    Saída esperada:

        info:    New mode is arm

3. Entre no Azure e obtenha uma lista de assinaturas:

    ```azurecli
    azure login
    ```

4. Na solicitação, insira suas credenciais do Azure:

    ```azurecli
    azure account list
    ```

5. Selecione a assinatura que deseja usar e anote a ID da assinatura para ser usada na próxima etapa.

6. Configure variáveis do PowerShell para uso com os comandos da CLI do Azure:

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

1. Crie um grupo de recursos:

    ```azurecli
    azure group create $rgName $location
    ```

2. Crie um balanceador de carga:

    ```azurecli
    $lb = azure network lb create --resource-group $rgname --location $location --name $lbName
    ```

3. Criar uma rede virtual:

    ```azurecli
    $vnet = azure network vnet create  --resource-group $rgname --name $vnetName --location $location --address-prefixes $vnetPrefix
    ```

4. Nessa rede virtual, crie duas sub-redes:

    ```azurecli
    $subnet1 = azure network vnet subnet create --resource-group $rgname --name $subnet1Name --address-prefix $subnet1Prefix --vnet-name $vnetName
    $subnet2 = azure network vnet subnet create --resource-group $rgname --name $subnet2Name --address-prefix $subnet2Prefix --vnet-name $vnetName
    ```

## <a name="create-public-ip-addresses-for-the-front-end-pool"></a>Criar endereços IP públicos para o pool de front-end

1. Configure as variáveis do PowerShell:

    ```powershell
    $publicIpv4Name = "myIPv4Vip"
    $publicIpv6Name = "myIPv6Vip"
    ```

2. Crie um endereço IP público para o pool de IPs de front-end:

    ```azurecli
    $publicipV4 = azure network public-ip create --resource-group $rgname --name $publicIpv4Name --location $location --ip-version IPv4 --allocation-method Dynamic --domain-name-label $dnsLabel
    $publicipV6 = azure network public-ip create --resource-group $rgname --name $publicIpv6Name --location $location --ip-version IPv6 --allocation-method Dynamic --domain-name-label $dnsLabel
    ```

    > [!IMPORTANT]
    > O balanceador de carga usa o rótulo de domínio do IP público como FQDN (nome de domínio totalmente qualificado). Isso é uma mudança da implantação clássica, que usa o nome do serviço de nuvem como o FQDN do balanceador de carga.
    >
    > Neste exemplo, o FQDN é *contoso09152016.southcentralus.cloudapp.azure.com*.

## <a name="create-front-end-and-back-end-pools"></a>Criar pools de front-end e back-end

Nesta seção, você cria os seguintes pools de IP:
* O pool de IP de front-end que recebe o tráfego de rede de entrada no balanceador de carga.
* O pool de IP de back-end para qual o pool de front-end envia o tráfego de rede com balanceamento de carga.

1. Configure as variáveis do PowerShell:

    ```powershell
    $frontendV4Name = "FrontendVipIPv4"
    $frontendV6Name = "FrontendVipIPv6"
    $backendAddressPoolV4Name = "BackendPoolIPv4"
    $backendAddressPoolV6Name = "BackendPoolIPv6"
    ```

2. Crie um pool de IPs de front-end e associe-o ao IP público criado na etapa anterior e o balanceador de carga.

    ```azurecli
    $frontendV4 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV4Name --public-ip-name $publicIpv4Name --lb-name $lbName
    $frontendV6 = azure network lb frontend-ip create --resource-group $rgname --name $frontendV6Name --public-ip-name $publicIpv6Name --lb-name $lbName
    $backendAddressPoolV4 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV4Name --lb-name $lbName
    $backendAddressPoolV6 = azure network lb address-pool create --resource-group $rgname --name $backendAddressPoolV6Name --lb-name $lbName
    ```

## <a name="create-the-probe-nat-rules-and-load-balancer-rules"></a>Criar a investigação, regras de NAT e regras do balanceador de carga

Este exemplo cria os seguintes itens:

* Uma regra de investigação para verificar se há conectividade com a porta TCP 80.
* Uma regra NAT para converter todo o tráfego de entrada na porta 3389 para a porta 3389 para RDP.\*
* Uma regra NAT para converter todo o tráfego de entrada na porta 3391 para a porta 3389 para o protocolo RDP (desktop remoto).\*
* Uma regra do balanceador de carga para equilibrar todo o tráfego de entrada na porta 80 para a porta 80 nos endereços no pool de back-end.

\* As regras NAT são associadas a uma instância de máquina virtual específica por trás do balanceador de carga. O tráfego de rede que chega à porta 3389 é enviado a uma máquina virtual específica e à porta que está associada a essa regra NAT. Você deve especificar um protocolo (UDP ou TCP) para uma regra NAT. Você não pode atribuir os dois protocolos para a mesma porta.

1. Configure as variáveis do PowerShell:

    ```powershell
    $probeV4V6Name = "ProbeForIPv4AndIPv6"
    $natRule1V4Name = "NatRule-For-Rdp-VM1"
    $natRule2V4Name = "NatRule-For-Rdp-VM2"
    $lbRule1V4Name = "LBRuleForIPv4-Port80"
    $lbRule1V6Name = "LBRuleForIPv6-Port80"
    ```

2. Crie a investigação.

    O exemplo a seguir cria uma investigação TCP que verifica a conectividade com a porta TCP 80 back-end a cada 15 segundos. Ele marca os recursos de back-end como não disponíveis após duas falhas consecutivas.

    ```azurecli
    $probeV4V6 = azure network lb probe create --resource-group $rgname --name $probeV4V6Name --protocol tcp --port 80 --interval 15 --count 2 --lb-name $lbName
    ```

3. Criar regras NAT de entrada que permitam conexões RDP com os recursos de back-end:

    ```azurecli
    $inboundNatRuleRdp1 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule1V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3389 --backend-port 3389 --lb-name $lbName
    $inboundNatRuleRdp2 = azure network lb inbound-nat-rule create --resource-group $rgname --name $natRule2V4Name --frontend-ip-name $frontendV4Name --protocol Tcp --frontend-port 3391 --backend-port 3389 --lb-name $lbName
    ```

4. Crie regras de balanceador de carga que enviam tráfego para portas de back-end diferentes, dependendo de qual front-end recebeu a solicitação.

    ```azurecli
    $lbruleIPv4 = azure network lb rule create --resource-group $rgname --name $lbRule1V4Name --frontend-ip-name $frontendV4Name --backend-address-pool-name $backendAddressPoolV4Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 80 --lb-name $lbName
    $lbruleIPv6 = azure network lb rule create --resource-group $rgname --name $lbRule1V6Name --frontend-ip-name $frontendV6Name --backend-address-pool-name $backendAddressPoolV6Name --probe-name $probeV4V6Name --protocol Tcp --frontend-port 80 --backend-port 8080 --lb-name $lbName
    ```

5. Verifique suas configurações:

    ```azurecli
    azure network lb show --resource-group $rgName --name $lbName
    ```

    Saída esperada:

        info:    Executing command network lb show
        info:    Looking up the load balancer "myIPv4IPv6Lb"
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

Crie NICs e associe-os às regras de NAT, regras do balanceador de carga e investigações.

1. Configure as variáveis do PowerShell:

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

2. Crie um NIC para cada back-end e adicione uma configuração de IPv6:

    ```azurecli
    $nic1 = azure network nic create --name $nic1Name --resource-group $rgname --location $location --private-ip-version "IPv4" --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule1V4Id
    $nic1IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic1Name

    $nic2 = azure network nic create --name $nic2Name --resource-group $rgname --location $location --subnet-id $subnet1Id --lb-address-pool-ids $backendAddressPoolV4Id --lb-inbound-nat-rule-ids $natRule2V4Id
    $nic2IPv6 = azure network nic ip-config create --resource-group $rgname --name "IPv6IPConfig" --private-ip-version "IPv6" --lb-address-pool-ids $backendAddressPoolV6Id --nic-name $nic2Name
    ```

## <a name="create-the-back-end-vm-resources-and-attach-each-nic"></a>Crie os recursos de VM de back-end e anexe cada NIC

Para criar VMs, você deve ter uma conta de armazenamento. Para o balanceamento de carga, as VMs precisam ser membros de um conjunto de disponibilidade. Para saber mais sobre a criação de VMs, consulte [Criar uma VM do Azure usando o PowerShell](../virtual-machines/virtual-machines-windows-ps-create.md?toc=%2fazure%2fload-balancer%2ftoc.json).

1. Configure as variáveis do PowerShell:

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
    > Este exemplo usa o nome de usuário e a senha para as VMs em texto sem formatação. Tome cuidado apropriado ao usar essas credenciais em texto não criptografado. Para um método mais seguro de tratamento de credenciais no PowerShell, consulte o cmdlet [`Get-Credential`](https://technet.microsoft.com/library/hh849815.aspx).

2. Crie o conjunto de disponibilidade e a conta de armazenamento.

    Você pode usar uma conta de armazenamento existente ao criar as VMs. Crie uma nova conta de armazenamento usando o código a seguir:

    ```azurecli
    $storageAcc = azure storage account create $storageAccountName --resource-group $rgName --location $location --sku-name "LRS" --kind "Storage"
    ```

3. Criar o conjunto de disponibilidade:

    ```azurecli
    $availabilitySet = azure availset create --name $availabilitySetName --resource-group $rgName --location $location
    ```

4. Crie as máquinas virtuais com NICs associados:

    ```azurecli
    $vm1 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm1Name --nic-id $nic1Id --os-disk-vhd $osDisk1Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension

    $vm2 = azure vm create --resource-group $rgname --location $location --availset-name $availabilitySetName --name $vm2Name --nic-id $nic2Id --os-disk-vhd $osDisk2Uri --os-type "Windows" --admin-username $vmUserName --admin-password $mySecurePassword --vm-size "Standard_A1" --image-urn $imageurn --storage-account-name $storageAccountName --disable-bginfo-extension
    ```

## <a name="next-steps"></a>Próximas etapas

[Introdução à configuração de um balanceador de carga interno](load-balancer-get-started-ilb-arm-cli.md)  
[Configurar um modo de distribuição do balanceador de carga](load-balancer-distribution-mode.md)  
[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
