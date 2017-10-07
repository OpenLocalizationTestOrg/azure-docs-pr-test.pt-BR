---
title: "aaaCreate um interno carregar balanceador - clássico de CLI do Azure | Microsoft Docs"
description: "Saiba como toocreate um balanceador de carga interno usando Olá CLI do Azure no modelo de implantação clássico Olá"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: becbbbde-a118-4269-9444-d3153f00bf34
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: ef29dfda5f7a75a411bbabe8b688a31c6bf81113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-hello-azure-cli"></a>Introdução à criação de um balanceador de carga interno (clássico) usando Olá CLI do Azure

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Serviços de nuvem](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](load-balancer-get-started-ilb-arm-cli.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

## <a name="toocreate-an-internal-load-balancer-set-for-virtual-machines"></a>toocreate um balanceador de carga interno definido para máquinas virtuais

toocreate um balanceador de carga interno definido e Olá servidores que enviarão sua tooit de tráfego, você deve fazer a seguir hello:

1. Crie uma instância de interno balanceamento de carga que será o ponto de extremidade de saudação da entrada tráfego toobe o balanceamento de carga servidores Olá de um conjunto com balanceamento de carga.
2. Adicione pontos de extremidade correspondente máquinas virtuais toohello que irá receber tráfego de entrada hello.
3. Configure servidores de saudação que enviará Olá tráfego toobe com balanceamento de carga toosend seu tráfego toohello endereço IP virtual (VIP) da instância de balanceamento de carga interno de saudação.

## <a name="step-by-step-creating-an-internal-load-balancer-using-cli"></a>Passo a passo da criação de um balanceador de carga interno usando a CLI

Este guia mostra como toocreate um balanceador de carga interno com base no cenário de saudação acima.

1. Se você nunca tiver usado a CLI do Azure, consulte [instalar e configurar Olá CLI do Azure](../cli-install-nodejs.md) e siga as instruções de saudação toohello ponto em que você selecione sua conta do Azure e assinatura.
2. Executar Olá **modo de configuração do azure** tooswitch tooclassic modo de comando, conforme mostrado abaixo.

    ```azurecli
    azure config mode asm
    ```

    Saída esperada:

        info:    New mode is asm

## <a name="create-endpoint-and-load-balancer-set"></a>Criar ponto de extremidade e conjunto de balanceadores de carga

cenário de saudação pressupõe Olá máquinas de virtuais "DB1" e "DB2" em um serviço de nuvem chamado "mytestcloud". As duas máquinas virtuais estão usando uma rede virtual chamada minha "testvnet" com a sub-rede "subnet-1".

Este guia criará um conjunto de balanceadores de carga internos usando a porta 1433 como a porta pública e 1433 como a porta local.

Este é um cenário comum em que máquinas virtuais SQL Olá o back-end usando que um servidores de banco de dados de carga interno balanceador tooguarantee Olá não seja exposto diretamente usando um endereço IP público.

### <a name="step-1"></a>Etapa 1

Crie um conjunto do balanceador de carga interno usando o `azure network service internal-load-balancer add`.

```azurecli
azure service internal-load-balancer add --serviceName mytestcloud --internalLBName ilbset --subnet-name subnet-1 --static-virtualnetwork-ipaddress 192.168.2.7
```

Confira `azure service internal-load-balancer --help` para obter mais informações.

Você pode verificar as propriedades do balanceador de carga interno de saudação usando o comando Olá `azure service internal-load-balancer list` *nome do serviço de nuvem*.

A seguir, um exemplo de saída de hello:

    azure service internal-load-balancer list my-testcloud
    info:    Executing command service internal-load-balancer list
    + Getting cloud service deployment
    data:    Name    Type     SubnetName  StaticVirtualNetworkIPAddress
    data:    ------  -------  ----------  -----------------------------
    data:    ilbset  Private  subnet-1    192.168.2.7
    info:    service internal-load-balancer list command OK


### <a name="step-2"></a>Etapa 2

Configure o balanceador de carga interno Olá definida quando você adicionar o primeiro ponto de extremidade de saudação. Você associará Olá ponto de extremidade, a máquina virtual e a investigação porta toohello balanceador de carga interno definido nesta etapa.

```azurecli
azure vm endpoint create db1 1433 --local-port 1433 --protocol tcp --probe-port 1433 --probe-protocol tcp --probe-interval 300 --probe-timeout 600 --internal-load-balancer-name ilbset
```

### <a name="step-3"></a>Etapa 3

Verificar a configuração de Balanceador de carga de hello usando `azure vm show` *nome da máquina virtual*

```azurecli
azure vm show DB1
```

saída de Hello serão:

    azure vm show DB1
    info:    Executing command vm show
    + Getting virtual machines
    data:    DNSName "mytestcloud.cloudapp.net"
    data:    Location "East US 2"
    data:    VMName "DB1"
    data:    IPAddress "192.168.2.4"
    data:    InstanceStatus "ReadyRole"
    data:    InstanceSize "Standard_D1"
    data:    Image "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk hostCaching "ReadWrite"
    data:    OSDisk name "db1-DB1-0-201511120457370846"
    data:    OSDisk mediaLink "https://XXXX.blob.core.windows.net/vhd"
    data:    OSDisk sourceImageName "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-20151022-en.us-127GB.vhd"
    data:    OSDisk operatingSystem "Windows"
    data:    OSDisk iOType "Standard"
    data:    ReservedIPName ""
    data:    VirtualIPAddresses 0 address "137.116.64.107"
    data:    VirtualIPAddresses 0 name "db1ContractContract"
    data:    VirtualIPAddresses 0 isDnsProgrammed true
    data:    VirtualIPAddresses 1 address "192.168.2.7"
    data:    VirtualIPAddresses 1 name "ilbset"
    data:    Network Endpoints 0 localPort 5986
    data:    Network Endpoints 0 name "PowerShell"
    data:    Network Endpoints 0 port 5986
    data:    Network Endpoints 0 protocol "tcp"
    data:    Network Endpoints 0 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 0 enableDirectServerReturn false
    data:    Network Endpoints 1 localPort 3389
    data:    Network Endpoints 1 name "Remote Desktop"
    data:    Network Endpoints 1 port 60173
    data:    Network Endpoints 1 protocol "tcp"
    data:    Network Endpoints 1 virtualIPAddress "137.116.64.107"
    data:    Network Endpoints 1 enableDirectServerReturn false
    data:    Network Endpoints 2 localPort 1433
    data:    Network Endpoints 2 name "tcp-1433-1433"
    data:    Network Endpoints 2 port 1433
    data:    Network Endpoints 2 loadBalancerProbe port 1433
    data:    Network Endpoints 2 loadBalancerProbe protocol "tcp"
    data:    Network Endpoints 2 loadBalancerProbe intervalInSeconds 300
    data:    Network Endpoints 2 loadBalancerProbe timeoutInSeconds 600
    data:    Network Endpoints 2 protocol "tcp"
    data:    Network Endpoints 2 virtualIPAddress "192.168.2.7"
    data:    Network Endpoints 2 enableDirectServerReturn false
    data:    Network Endpoints 2 loadBalancerName "ilbset"
    info:    vm show command OK

## <a name="create-a-remote-desktop-endpoint-for-a-virtual-machine"></a>Criar um ponto de extremidade da área de trabalho remota para uma máquina virtual

Você pode criar um tráfego de rede do ponto de extremidade da área de trabalho remota tooforward de uma porta local de tooa porta pública para uma máquina virtual específica usando `azure vm endpoint create`.

```azurecli
azure vm endpoint create web1 54580 -k 3389
```

## <a name="remove-virtual-machine-from-load-balancer"></a>Remover máquina virtual do balanceador de carga

Você pode remover uma máquina virtual de um balanceador de carga interno definido, excluindo o ponto de extremidade Olá associado. Depois que o ponto de extremidade de saudação for removido, máquina virtual de saudação não pertencer balanceador de carga toohello definir mais.

Usando o exemplo hello acima, você pode remover ponto de extremidade de saudação criado para a máquina virtual "DB1" do balanceador de carga interno "ilbset" usando o comando Olá `azure vm endpoint delete`.

```azurecli
azure vm endpoint delete DB1 tcp-1433-1433
```

Confira `azure vm endpoint --help` para obter mais informações.

## <a name="next-steps"></a>Próximas etapas

[Configurar um modo de distribuição do balanceador de carga usando a afinidade de IP de origem](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)
