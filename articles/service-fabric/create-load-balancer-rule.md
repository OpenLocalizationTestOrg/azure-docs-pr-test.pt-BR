---
title: aaaCreate uma regra de Balanceador de carga do Azure para um cluster
description: Configure as portas de tooopen um balanceador de carga do Azure para o cluster do Azure Service Fabric.
services: service-fabric
documentationcenter: na
author: thraka
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/22/2017
ms.author: adegeo
ms.openlocfilehash: 4a40f62422bd895d782be8cbaace5f4e1af81db3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="open-ports-for-a-service-fabric-cluster"></a>Abrir portas para um cluster do Service Fabric

Balanceador de carga Olá implantado com o cluster do Service Fabric do Azure direciona o tráfego tooyour aplicativo em execução em um nó. Se você alterar sua toouse aplicativo uma porta diferente, você deve expor essa porta (ou rotear uma porta diferente) em Olá balanceador de carga do Azure.

Quando você implantou seu tooAzure de cluster de malha do serviço, um balanceador de carga foi criado automaticamente para você. Caso não tenha um balanceador de carga, confira [Configurar um balanceador de carga voltado para Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).

## <a name="configure-service-fabric"></a>Configurar o Service Fabric

Seu aplicativo do Service Fabric **ServiceManifest.xml** arquivo de configuração define pontos de extremidade de saudação toouse espera que seu aplicativo. Depois que o arquivo de configuração Olá foi atualizada toodefine um ponto de extremidade, o balanceador de carga Olá deve ser atualizada tooexpose que (ou um diferente) porta. Para obter mais informações sobre como toocreate Olá ponto de extremidade de malha de serviço, consulte [um ponto de extremidade de instalação](service-fabric-service-manifest-resources.md).

## <a name="create-a-load-balancer-rule"></a>Criar uma regra de balanceador de carga

Uma regra de Balanceador de carga abre uma porta para a internet e encaminha a porta do nó interno toohello tráfego usada pelo seu aplicativo. Caso não tenha um balanceador de carga, confira [Configurar um balanceador de carga voltado para Internet](..\load-balancer\load-balancer-get-started-internet-portal.md).

regra de toocreate um balanceador de carga, você precisa Olá toocollect informações a seguir:

- Nome do balanceador de carga.
- Grupo de recursos Olá balanceador de carga e cluster do service fabric.
- Porta externa.
- Porta interna.

## <a name="azure-cli"></a>CLI do Azure
>[!NOTE]
>Se você precisar de nome de saudação toodetermine saudação do balanceador de carga, use get de tooquickly esse comando uma lista de todos os balanceadores de carga e grupos de recursos de saudação associado.
>
>`az network lb list --query "[].{ResourceGroup: resourceGroup, Name: name}"`
>

Leva apenas um único comando toocreate uma regra de Balanceador de carga com hello **CLI do Azure**. Basta tooknow ambos os nome de saudação do hello carga balanceador e o recurso grupo toocreate uma nova regra.

```azurecli
az network lb rule create --backend-port 40000 --frontend-port 39999 --protocol Tcp --lb-name LB-svcfab3 -g svcfab_cli -n my-app-rule
```

Olá comando CLI do Azure tem alguns parâmetros que são descritos em Olá a tabela a seguir:

| Parâmetro | Descrição |
| --------- | ----------- |
| `--backend-port`  | o aplicativo de malha do Hello porta Olá serviço está escutando. |
| `--frontend-port` | saudação de porta Olá carregar balanceador expõe para conexões externas. |
| `-lb-name` | nome Hello de saudação toochange do balanceador de carga. |
| `-g`       | grupo de recursos de saudação que tem o balanceador de carga hello e o cluster do service fabric. |
| `-n`       | Olá escolhida o nome da regra de saudação. |


>[!NOTE]
>Para obter mais informações sobre como toocreate um balanceador de carga com hello CLI do Azure, consulte [criar um balanceador de carga com hello CLI do Azure](..\load-balancer\load-balancer-get-started-internet-arm-cli.md).

## <a name="powershell"></a>PowerShell

>[!NOTE]
>Se você precisar de nome de saudação toodetermine saudação do balanceador de carga, use get de tooquickly esse comando uma lista de todos os balanceadores de carga e grupos de recursos associado.
>
>`Get-AzureRmLoadBalancer | Select Name, ResourceGroupName`

PowerShell é um pouco mais complicado do que Olá CLI do Azure. Conceitualmente, faça uma regra Olá toocreate as etapas a seguir.

1. Obter o balanceador de carga de saudação do Azure.
2. Criar uma regra.
3. Adicione o balanceador de carga Olá regra toohello.
4. Atualize balanceador de carga de saudação.

```powershell
# Get hello load balancer
$lb = Get-AzureRmLoadBalancer -Name LB-svcfab3 -ResourceGroupName svcfab_cli

# Create hello rule based on information from hello load balancer.
$lbrule = New-AzureRmLoadBalancerRuleConfig -Name my-app-rule7 -Protocol Tcp -FrontendPort 39990 -BackendPort 40009 `
                                            -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
                                            -BackendAddressPool  $lb.BackendAddressPools[0] `
                                            -Probe $lb.Probes[0]

# Add hello rule toohello load balancer
$lb.LoadBalancingRules.Add($lbrule)

# Update hello load balancer on Azure
$lb | Set-AzureRmLoadBalancer
```

Sobre Olá `New-AzureRmLoadBalancerRuleConfig` comando hello `-FrontendPort` balanceador de carga representa Olá porta Olá expõe para conexões externas e hello `-BackendPort` aplicativo de malha representa Olá porta saudação do serviço está escutando.

>[!NOTE]
>Para obter mais informações sobre como toocreate um balanceador de carga com o PowerShell, consulte [criar um balanceador de carga com o PowerShell](..\load-balancer\load-balancer-get-started-internet-arm-ps.md).

