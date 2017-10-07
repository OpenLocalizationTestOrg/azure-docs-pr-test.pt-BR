---
title: "aaaCreate interno do Azure PowerShell clássico de Balanceador - carregar | Microsoft Docs"
description: "Saiba como o toocreate um interno balanceador usando o PowerShell no modelo de implantação clássico Olá de carga"
services: load-balancer
documentationcenter: na
author: kumudd
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 3be93168-3787-45a5-a194-9124fe386493
ms.service: load-balancer
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/23/2017
ms.author: kumud
ms.openlocfilehash: 382db80c42ffab09905513019b72e85a4f9dfeff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-creating-an-internal-load-balancer-classic-using-powershell"></a>Introdução à criação de um balanceador de carga interno (clássico) usando o PowerShell

> [!div class="op_single_selector"]
> * [PowerShell](../load-balancer/load-balancer-get-started-ilb-classic-ps.md)
> * [CLI do Azure](../load-balancer/load-balancer-get-started-ilb-classic-cli.md)
> * [Serviços de nuvem](../load-balancer/load-balancer-get-started-ilb-classic-cloud.md)

[!INCLUDE [load-balancer-get-started-ilb-intro-include.md](../../includes/load-balancer-get-started-ilb-intro-include.md)]

> [!IMPORTANT]
> O Azure tem dois modelos de implantação diferentes para criar e trabalhar com recursos: [Gerenciador de Recursos e clássico](../azure-resource-manager/resource-manager-deployment-model.md).  Este artigo aborda usando o modelo de implantação clássico hello. A Microsoft recomenda que mais novas implantações de usam o modelo do Gerenciador de recursos de saudação. Saiba como muito[executar essas etapas usando o modelo do Gerenciador de recursos de saudação](load-balancer-get-started-ilb-arm-ps.md).

[!INCLUDE [load-balancer-get-started-ilb-scenario-include.md](../../includes/load-balancer-get-started-ilb-scenario-include.md)]

[!INCLUDE [azure-ps-prerequisites-include.md](../../includes/azure-ps-prerequisites-include.md)]

## <a name="create-an-internal-load-balancer-set-for-virtual-machines"></a>Criar um conjunto de balanceadores de carga internos para máquinas virtuais

toocreate um balanceador de carga interno definido e Olá servidores que enviarão sua tooit de tráfego, você tem a seguir Olá toodo:

1. Crie uma instância de interno balanceamento de carga que será o ponto de extremidade de saudação da entrada tráfego toobe o balanceamento de carga servidores Olá de um conjunto com balanceamento de carga.
2. Adicione pontos de extremidade correspondente máquinas virtuais toohello que irá receber tráfego de entrada hello.
3. Configure servidores de saudação que enviará Olá tráfego toobe com balanceamento de carga toosend seu tráfego toohello endereço IP virtual (VIP) da instância de balanceamento de carga interno de saudação.

### <a name="step-1-create-an-internal-load-balancing-instance"></a>Etapa 1: criar uma instância de Balanceamento de Carga Interno

Para um serviço de nuvem existente ou um serviço de nuvem implantado em uma rede virtual regional, você pode criar uma instância de balanceamento de carga interno com hello comandos do Windows PowerShell a seguir:

```powershell
$svc="<Cloud Service Name>"
$ilb="<Name of your ILB instance>"
$subnet="<Name of hello subnet within your virtual network>"
$IP="<hello IPv4 address toouse on hello subnet-optional>"

Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb –SubnetName $subnet –StaticVNetIPAddress $IP
```

Observe que esse uso do hello [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx) Olá de parâmetros defaultprobe usa o cmdlet do Windows PowerShell. Para obter mais informações sobre conjuntos de parâmetros adicionais, consulte [Add-AzureEndpoint](https://msdn.microsoft.com/library/dn495300.aspx).

### <a name="step-2-add-endpoints-toohello-internal-load-balancing-instance"></a>Etapa 2: Adicionar a instância de balanceamento de carga interno toohello de pontos de extremidade

Aqui está um exemplo:

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
$lbsetname="lbset"
$prot="tcp"
$locport=1433
$pubport=1433
$ilb="ilbset"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -Lbset $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

### <a name="step-3-configure-your-servers-toosend-their-traffic-toohello-new-internal-load-balancing-endpoint"></a>Etapa 3: Configurar seu servidores toosend seu tráfego toohello novo balanceamento de carga interno ponto de extremidade

Muito configurados servidores Olá cujo tráfego é contínuo toobe com balanceamento de carga toouse Olá novo endereço IP (Olá VIP) do hello instância balanceamento de carga interno. Este é o endereço de saudação na qual Olá balanceamento de carga interno instância está escutando. Na maioria dos casos, você precisa toojust adicionar ou modificar um registro DNS para Olá VIP da instância de balanceamento de carga interno hello.

Se você especificou um endereço IP de saudação durante a criação de saudação da instância de balanceamento de carga interno Olá, você já tem Olá VIP. Caso contrário, você pode ver o VIP de saudação do hello comandos a seguir:

```powershell
$svc="<Cloud Service Name>"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

toouse esses comandos, preencha os valores hello e remover hello < e >. Aqui está um exemplo:

```powershell
$svc="mytestcloud"
Get-AzureService -ServiceName $svc | Get-AzureInternalLoadBalancer
```

De exibição de saudação do hello comando Get-AzureInternalLoadBalancer, observe o endereço IP hello e torne servidores do hello alterações necessárias tooyour ou tooensure de registros DNS que o tráfego seja enviado toohello VIP.

> [!NOTE]
> plataforma do Microsoft Azure Olá usa um endereço IPv4 estático, roteável publicamente para uma variedade de cenários administrativos. endereço IP de saudação é 168.63.129.16. Esse endereço IP não deve ser bloqueado por nenhum firewall porque ele pode causar um comportamento inesperado.
> Com relação tooAzure de balanceamento de carga interno, esse endereço IP é usado pelo monitoramento de testes do estado de integridade de Olá Olá carga balanceador toodetermine para máquinas virtuais em um conjunto com balanceamento de carga. Se um grupo de segurança de rede é usada toorestrict tráfego tooAzure VMs em um conjunto de balanceamento de carga internamente ou tooa aplicada sub-rede de rede Virtual, certifique-se de que uma regra de segurança de rede é adicionada tooallow tráfego de 168.63.129.16.

## <a name="example-of-internal-load-balancing"></a>Exemplo de balanceamento de carga interna

toostep você Olá final tooend processo de criação de um conjunto com balanceamento de carga para duas configurações de exemplo, consulte Olá seções a seguir.

### <a name="an-internet-facing-multi-tier-application"></a>Um aplicativo para a Internet de diversas camadas

Você deseja tooprovide um serviço de banco de dados com balanceamento de carga para um conjunto de servidores web voltados para a Internet. Os dois conjuntos de servidores são hospedados em um único serviço de nuvem do Azure. Servidor Web tráfego tooTCP porta 1433 deve ser distribuída entre duas máquinas virtuais na camada de banco de dados de saudação. A Figura 1 mostra a configuração de saudação.

![Conjunto com balanceamento de carga interno para a camada de banco de dados de saudação](./media/load-balancer-internal-getstarted/IC736321.png)

configuração de Olá consiste das seguintes hello:

* serviço de nuvem existente Olá hospedar máquinas virtuais de saudação é denominado mytestcloud.
* dois servidores de banco de dados existente Olá são nomeados DB1, DB2.
* Servidores Web na camada da web de saudação conectam toohello servidores de banco de dados na camada de banco de dados de saudação usando o endereço IP privado de saudação. Outra opção é toouse seu próprio DNS para a rede virtual hello e registrar manualmente um registro a para o conjunto de Balanceador de carga interno hello.

Olá, comandos a seguir configuram uma nova instância de balanceamento de carga interno denominada **ILBset** e adicione máquinas de virtuais toohello de pontos de extremidade correspondente toohello dois servidores de banco de dados:

```powershell
$svc="mytestcloud"
$ilb="ilbset"
Add-AzureInternalLoadBalancer -ServiceName $svc -InternalLoadBalancerName $ilb
$prot="tcp"
$locport=1433
$pubport=1433
$epname="TCP-1433-1433"
$lbsetname="lbset"
$vmname="DB1"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM

$epname="TCP-1433-1433-2"
$vmname="DB2"
Get-AzureVM –ServiceName $svc –Name $vmname | Add-AzureEndpoint -Name $epname -LbSetName $lbsetname -Protocol $prot -LocalPort $locport -PublicPort $pubport –DefaultProbe -InternalLoadBalancerName $ilb | Update-AzureVM
```

## <a name="remove-an-internal-load-balancing-configuration"></a>Remover uma configuração de Balanceamento de Carga Interno

tooremove uma máquina virtual como um ponto de extremidade de uma instância de Balanceador de carga interno, Olá use comandos a seguir:

```powershell
$svc="<Cloud service name>"
$vmname="<Name of hello VM>"
$epname="<Name of hello endpoint>"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

toouse esses comandos, preencha os valores hello, removendo hello < e >.

Aqui está um exemplo:

```powershell
$svc="mytestcloud"
$vmname="DB1"
$epname="TCP-1433-1433"
Get-AzureVM -ServiceName $svc -Name $vmname | Remove-AzureEndpoint -Name $epname | Update-AzureVM
```

tooremove uma instância do balanceador de carga interno de um serviço de nuvem, use Olá comandos a seguir:

```powershell
$svc="<Cloud service name>"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

toouse esses comandos, preencha valor hello e remova hello < e >.

Aqui está um exemplo:

```powershell
$svc="mytestcloud"
Remove-AzureInternalLoadBalancer -ServiceName $svc
```

## <a name="additional-information-about-internal-load-balancer-cmdlets"></a>Informações adicionais sobre cmdlets de balanceador de carga interno

tooobtain informações adicionais sobre os cmdlets de balanceamento de carga interna, executados Olá comandos em um prompt do Windows PowerShell a seguir:

```powershell
Get-Help New-AzureInternalLoadBalancerConfig -full
Get-Help Add-AzureInternalLoadBalancer -full
Get-Help Get-AzureInternalLoadbalancer -full
Get-Help Remove-AzureInternalLoadBalancer -full
```

## <a name="next-steps"></a>Próximas etapas

[Configurar um modo de distribuição do balanceador de carga usando a afinidade de IP de origem](load-balancer-distribution-mode.md)

[Definir configurações de tempo limite de TCP ocioso para o balanceador de carga](load-balancer-tcp-idle-timeout.md)

