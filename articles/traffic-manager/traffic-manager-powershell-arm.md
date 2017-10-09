---
title: aaaUsing PowerShell toomanage Traffic Manager no Azure | Microsoft Docs
description: "Usando o PowerShell para o Gerenciador de Tráfego com o Azure Resource Manager"
services: traffic-manager
documentationcenter: na
author: kumudd
manager: timlt
ms.assetid: bc247448-1d2e-4104-ac03-42b59ebde065
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: 018c37db63beb82fdad54cfd7e13ab3cb645723a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-powershell-toomanage-traffic-manager"></a>Usando o PowerShell toomanage Traffic Manager

Gerenciador de recursos do Azure é a interface de gerenciamento preferencial de saudação para serviços no Azure. Os perfis do Gerenciador de Tráfego do Azure podem ser gerenciados usando ferramentas e APIs baseadas no Azure Resource Manager.

## <a name="resource-model"></a>Modelo de recursos

O Gerenciador de Tráfego do Azure é configurado usando um conjunto de configurações chamado de perfil do Gerenciador de Tráfego. Este perfil contém as configurações de DNS, configurações de roteamento de tráfego, configurações de monitoramento do ponto de extremidade e uma lista de tráfego de toowhich de pontos de extremidade do serviço é roteada.

Cada perfil do Gerenciador de Tráfego é representado por um recurso do tipo "TrafficManagerProfiles". Em Olá nível da API REST, Olá URI para cada perfil é o seguinte:

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a>Configurando o PowerShell do Azure

Essas instruções usam o Microsoft Azure PowerShell. Olá seguinte artigo explica como tooinstall e configurar o Azure PowerShell.

* [Como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview)

exemplos de saudação neste artigo presumem que você tenha um grupo de recursos existente. Você pode criar um grupo de recursos usando o comando a seguir de saudação:

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> O Azure Resource Manager requer que todos os grupos de recursos tenham um local. Esse local é usado como saudação padrão para recursos criados nesse grupo de recursos. No entanto, como os recursos de perfil do Traffic Manager são globais, não regional, escolha de saudação do local do grupo de recursos não tem impacto sobre o Azure Traffic Manager.

## <a name="create-a-traffic-manager-profile"></a>Criar um perfil do Gerenciador de Tráfego

toocreate um perfil do Gerenciador de tráfego, use Olá `New-AzureRmTrafficManagerProfile` cmdlet:

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

Olá, a tabela a seguir descreve os parâmetros de saudação:

| Parâmetro | Descrição |
| --- | --- |
| Nome |nome de recurso de saudação de saudação recurso de perfil do Gerenciador de tráfego. Perfis do hello mesmo grupo de recursos deve ter nomes exclusivos. Esse nome é separado do nome DNS Olá usado para consultas DNS. |
| ResourceGroupName |nome de Olá do recurso de perfil do hello recurso grupo contentor hello. |
| TrafficRoutingMethod |Especifica o roteamento de tráfego da saudação método usado toodetermine qual ponto de extremidade é retornado na resposta de uma consulta DNS. Os valores possíveis são “Desempenho”, “Ponderado” ou “Prioridade”. |
| RelativeDnsName |Especifica a porção hostname de Olá Olá do nome de DNS fornecido por esse perfil do Gerenciador de tráfego. Esse valor é combinado com o nome de domínio DNS Olá usado pelo Gerenciador de tráfego do Azure tooform Olá nome totalmente qualificado (FQDN) do perfil de saudação. Por exemplo, definir o valor Olá 'contoso' torna-se 'contoso.trafficmanager.net'. |
| TTL |Especifica a saudação DNS Time-to-Live (TTL), em segundos. Este TTL informa os resolvedores de DNS Local hello e os clientes DNS quanto tempo toocache respostas DNS a esse perfil do Gerenciador de tráfego. |
| MonitorProtocol |Especifica a integridade do ponto de extremidade do hello protocolo toouse toomonitor. Os valores possíveis são “HTTP” e “HTTPS”. |
| MonitorPort |Especifica a saudação a porta TCP usada toomonitor integridade do ponto de extremidade. |
| MonitorPath |Especifica o nome de domínio de ponto de extremidade do hello caminho relativo toohello usado tooprobe para integridade do ponto de extremidade. |

Olá cmdlet cria um perfil do Traffic Manager no Azure e retorna um tooPowerShell de objeto correspondente do perfil. Neste ponto, o perfil de saudação não contém nenhum ponto de extremidade. Para obter mais informações sobre como adicionar o perfil do Gerenciador de tráfego de tooa de pontos de extremidade, consulte [adicionar pontos de extremidade do Traffic Manager](#adding-traffic-manager-endpoints).

## <a name="get-a-traffic-manager-profile"></a>Obter um perfil do Gerenciador de Tráfego

tooretrieve um objeto de perfil do Gerenciador de tráfego existente, use Olá `Get-AzureRmTrafficManagerProfle` cmdlet:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

Esse cmdlet retorna um objeto de perfil do Gerenciador de Tráfego.

## <a name="update-a-traffic-manager-profile"></a>Atualizar um perfil do Gerenciador de Tráfego

A modificação de perfis do Gerenciador de Tráfego segue um processo de 3 etapas:

1. Recuperar Olá perfil usando `Get-AzureRmTrafficManagerProfile` ou usar perfil Olá retornado por `New-AzureRmTrafficManagerProfile`.
2. Modificar o perfil de saudação. Você pode adicionar e remover pontos de extremidade ou alterar ponto de extremidade ou parâmetros do perfil. Essas alterações são operações offline. Somente você está alterando o objeto de saudação local na memória que representa o perfil de saudação.
3. Confirmar as alterações usando Olá `Set-AzureRmTrafficManagerProfile` cmdlet.

Todas as propriedades de perfil podem ser alteradas com exceção RelativeDnsName do perfil Olá. toochange Olá RelativeDnsName, você deve excluir o perfil e um novo perfil com um novo nome.

saudação de exemplo a seguir demonstra como toochange Olá TTL do perfil:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Há três tipos de pontos de extremidade do Gerenciador de Tráfego:

1. Os **pontos de extremidade do Azure** são serviços hospedados no Azure
2. Os **pontos de extremidade externos** são serviços hospedados fora do Azure
3. **Aninhados pontos de extremidade** são hierarquias usadas tooconstruct aninhado de perfis de Gerenciador de tráfego. Os pontos de extremidade aninhados habilitam configurações avançadas de roteamento de tráfego para aplicativos complexos.

Em todos os três casos, os pontos de extremidade podem ser adicionados de duas maneiras:

1. Usando um processo de 3 etapas descrito anteriormente. vantagem Olá desse método é que várias alterações de ponto de extremidade podem ser feitas em uma única atualização.
2. Usando Olá AzureRmTrafficManagerEndpoint novo cmdlet. Esse cmdlet adiciona um perfil de Gerenciador de tráfego existente do ponto de extremidade tooan em uma única operação.

## <a name="adding-azure-endpoints"></a>Adicionando pontos de extremidade do Azure

Os pontos de extremidade do Azure fazem referência a serviços hospedados no Azure. Há suporte para dois tipos de pontos de extremidade do Azure:

1. Aplicativos Web do Azure 
2. Recursos PublicIpAddress do Azure (que podem ser anexado tooa balanceador de carga ou uma NIC de máquina virtual). Olá PublicIpAddress deve ter um nome DNS atribuído toobe usado no Gerenciador de tráfego.

Em cada caso:

* o serviço de saudação é especificado usando o parâmetro 'targetResourceId' hello `Add-AzureRmTrafficManagerEndpointConfig` ou `New-AzureRmTrafficManagerEndpoint`.
* Olá 'Target' e 'EndpointLocation' são implicado Olá TargetResourceId.
* A especificação de saudação 'Peso' é opcional. Os pesos são usados somente se o perfil de saudação for método de roteamento de tráfego do toouse configurado hello 'Ponderado'. Caso contrário, eles serão ignorados. Se especificado, o valor de saudação deve ser um número entre 1 e 1000. valor padrão de saudação é '1'.
* Olá especificando 'Priority' é opcional. As prioridades são usadas somente se o perfil de Olá é o método de roteamento de tráfego do toouse configurado hello 'Priority'. Caso contrário, eles serão ignorados. Os valores válidos são de 1 too1000 com valores menores que indica uma prioridade mais alta. Se especificados para um ponto de extremidade, deverão ser especificados para todos os pontos de extremidade. Se omitido, os valores padrão a partir de '1' são aplicados na ordem de saudação que pontos de extremidade de saudação são listados.

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a>Exemplo 1: adicionar pontos de extremidade do aplicativo Web usando `Add-AzureRmTrafficManagerEndpointConfig`

Neste exemplo, podemos criar um perfil do Gerenciador de tráfego e adicionar dois pontos de extremidade do aplicativo Web usando Olá `Add-AzureRmTrafficManagerEndpointConfig` cmdlet.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a>Exemplo 2: Adicionar um ponto de extremidade publicIpAddress usando `New-AzureRmTrafficManagerEndpoint`

Neste exemplo, um recurso de endereço IP público é adicionado toohello perfil do Gerenciador de tráfego. endereço IP público de saudação deve ter um nome DNS configurado e pode ser vinculado ou toohello NIC um VM ou tooa do balanceador de carga.

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a>Adicionando pontos de extremidade externos

Traffic Manager usa pontos de extremidade externos toodirect tráfego tooservices hospedado fora do Azure. Como com pontos de extremidade do Azure, pontos de extremidade externos podem ser adicionados usando `Add-AzureRmTrafficManagerEndpointConfig` seguido por `Set-AzureRmTrafficManagerProfile` ou `New-AzureRMTrafficManagerEndpoint`.

Ao especificar pontos de extremidade externos:

* nome de domínio do ponto de extremidade Olá deve ser especificado usando o parâmetro de 'Target' hello
* Se Olá método de roteamento de tráfego 'Desempenho' for usado, Olá 'EndpointLocation' é necessário. Caso contrário, será opcional. Olá valor deve ser um [nome da região do Azure válida](https://azure.microsoft.com/regions/).
* Olá 'Peso' e 'Priority' é opcional.

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Exemplo 1: adicionar pontos de extremidade externos usando `Add-AzureRmTrafficManagerEndpointConfig` e `Set-AzureRmTrafficManagerProfile`

Neste exemplo, podemos criar um perfil do Gerenciador de tráfego, adicionar dois pontos de extremidade externos e confirmar as alterações de saudação.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Exemplo 2: adicionar pontos de extremidade externos usando `New-AzureRmTrafficManagerEndpoint`

Neste exemplo, vamos adicionar um perfil existente do ponto de extremidade externo tooan. perfil de saudação é especificado usando os nomes de grupo de perfil e recursos de saudação.

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a>Adicionando pontos de extremidade ‘aninhados’

Cada perfil do Gerenciador de Tráfego especifica um único método de roteamento de tráfego. No entanto, há cenários que exigem mais sofisticadas roteamento de tráfego de roteamento Olá fornecido por um único perfil do Gerenciador de tráfego. Você pode aninhar os benefícios de saudação do Gerenciador de tráfego perfis toocombine de mais de um método de roteamento de tráfego. Perfis aninhados permitem que você toooverride saudação padrão do Traffic Manager comportamento toosupport maior e mais complexas implantações de aplicativos. Para obter mais exemplos, consulte [Perfis aninhados do Gerenciador de Tráfego](traffic-manager-nested-profiles.md).

Pontos de extremidade aninhados são configurados no perfil de pai hello, usando um tipo de ponto de extremidade específico, 'NestedEndpoints'. Ao especificar pontos de extremidade aninhados:

* ponto de extremidade Olá deve ser especificado usando o parâmetro de 'targetResourceId' hello
* Se Olá método de roteamento de tráfego 'Desempenho' for usado, Olá 'EndpointLocation' é necessário. Caso contrário, será opcional. Olá valor deve ser um [nome da região do Azure válida](http://azure.microsoft.com/regions/).
* Olá 'Peso' e 'Priority' é opcional, como pontos de extremidade do Azure.
* Olá 'MinChildEndpoints' parâmetro é opcional. valor padrão de saudação é '1'. Se o número de saudação de pontos de extremidade disponíveis cair abaixo desse limite, perfil pai de saudação considera o perfil filho Olá 'degradado' e desvia tráfego toohello outros pontos de extremidade no perfil do hello pai.

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Exemplo 1: adicionar pontos de extremidade aninhados usando `Add-AzureRmTrafficManagerEndpointConfig` e `Set-AzureRmTrafficManagerProfile`

Neste exemplo, podemos criar pai e filho do novo Gerenciador de tráfego perfis, Adicionar filho hello como um pai do ponto de extremidade aninhada toohello e confirmar as alterações de saudação.

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Para resumir, neste exemplo, não adicionamos quaisquer outros pontos de extremidade toohello filho ou pai perfis.

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Exemplo 2: adicionar pontos de extremidade aninhados usando `New-AzureRmTrafficManagerEndpoint`

Neste exemplo, adicionamos um perfil filho existente como um perfil de pai existente do ponto de extremidade aninhada tooan. perfil de saudação é especificado usando os nomes de grupo de perfil e recursos de saudação.

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a>Atualizar um Ponto de Extremidade do Gerenciador de Tráfego

Há tooupdate de duas maneiras de um ponto de extremidade do Gerenciador de tráfego existente:

1. Obter o perfil do Gerenciador de tráfego de saudação usando `Get-AzureRmTrafficManagerProfile`, atualizar as propriedades de ponto de extremidade Olá no perfil de saudação e confirmar as alterações de saudação usando `Set-AzureRmTrafficManagerProfile`. Esse método tem a vantagem de saudação de ser capaz de tooupdate mais de um ponto de extremidade em uma única operação.
2. Obter usando o ponto de extremidade do Traffic Manager Olá `Get-AzureRmTrafficManagerEndpoint`, atualizar as propriedades de ponto de extremidade hello e confirmar alterações hello usando `Set-AzureRmTrafficManagerEndpoint`. Esse método é mais simples, já que não exige a indexação em uma matriz de pontos de extremidade Olá no perfil de saudação.

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a>Exemplo 1: atualizar pontos de extremidade usando `Get-AzureRmTrafficManagerProfile` e `Set-AzureRmTrafficManagerProfile`

Neste exemplo, vamos modificar prioridade da saudação de dois pontos de extremidade em um perfil existente.

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a>Exemplo 2: atualizar um ponto de extremidade usando `Get-AzureRmTrafficManagerEndpoint` e `Set-AzureRmTrafficManagerEndpoint`

Neste exemplo, vamos modificar peso de saudação de um ponto de extremidade em um perfil existente.

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a>Habilitando e desabilitando pontos de extremidade e perfis

O Traffic Manager permite toobe de pontos de extremidade individuais habilitados e desabilitados, além de permitir a habilitação e desabilitação de perfis de inteiros.
Essas alterações podem ser feitas pelos recursos de ponto de extremidade ou perfil Olá obtendo/Atualizar/configuração. toostreamline essas operações comuns, eles também têm suporte por meio de cmdlets dedicados.

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a>Exemplo 1: Habilitando e desabilitando um perfil do Gerenciador de Tráfego

tooenable um perfil do Gerenciador de tráfego, use `Enable-AzureRmTrafficManagerProfile`. perfil de saudação pode ser especificado usando um objeto de perfil. Olá objeto de perfil pode ser passado por meio do pipeline de saudação ou usando Olá '-TrafficManagerProfile' parâmetro. Neste exemplo, podemos especificar perfil Olá pelo nome do grupo de recursos e perfil hello.

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

toodisable um perfil do Gerenciador de tráfego:

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

Olá Disable-AzureRmTrafficManagerProfile cmdlet solicita confirmação. Esse aviso pode ser suprimido Olá '-Force' parâmetro.

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a>Exemplo 2: Habilitando e desabilitando um ponto de extremidade do Gerenciador de Tráfego

tooenable um ponto de extremidade do Traffic Manager, use `Enable-AzureRmTrafficManagerEndpoint`. Não há ponto de extremidade Olá toospecify de duas maneiras

1. Usando um objeto TrafficManagerEndpoint passado por meio do pipeline de saudação ou Olá '-TrafficManagerEndpoint' parâmetro
2. Usando o nome do ponto de extremidade hello, tipo de ponto de extremidade, nome do perfil e nome do grupo de recursos:

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Da mesma forma, toodisable um ponto de extremidade do Gerenciador de tráfego:

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

Assim como acontece com `Disable-AzureRmTrafficManagerProfile`, Olá `Disable-AzureRmTrafficManagerEndpoint` cmdlet solicita confirmação. Esse aviso pode ser suprimido Olá '-Force' parâmetro.

## <a name="delete-a-traffic-manager-endpoint"></a>Excluir um Ponto de Extremidade do Gerenciador de Tráfego

tooremove pontos de extremidade individuais, use Olá `Remove-AzureRmTrafficManagerEndpoint` cmdlet:

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Esse cmdlet solicita confirmação. Esse aviso pode ser suprimido Olá '-Force' parâmetro.

## <a name="delete-a-traffic-manager-profile"></a>Excluir um perfil do Gerenciador de Tráfego

toodelete um perfil do Gerenciador de tráfego, use Olá `Remove-AzureRmTrafficManagerProfile` cmdlet, especificando nomes de grupo de recursos e perfil hello:

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

Esse cmdlet solicita confirmação. Esse aviso pode ser suprimido Olá '-Force' parâmetro.

Olá toobe de perfil excluída também pode ser especificada usando um objeto de perfil:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
Remove-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile [-Force]
```

Essa sequência também pode ser transferida:

```powershell
Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG | Remove-AzureRmTrafficManagerProfile [-Force]
```

## <a name="next-steps"></a>Próximas etapas

[Monitoramento do Gerenciador de Tráfego](traffic-manager-monitoring.md)

[Considerações sobre desempenho do Gerenciador de Tráfego](traffic-manager-performance-considerations.md)
