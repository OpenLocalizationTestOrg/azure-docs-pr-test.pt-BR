---
title: "Usando o PowerShell para gerenciar o Gerenciador de Tráfego no Azure | Microsoft Docs"
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
ms.openlocfilehash: 1cd7bd7e32c96398d72c7cd3b51e2b456d60f01d
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2017
---
# <a name="using-powershell-to-manage-traffic-manager"></a>Usando o PowerShell para gerenciar o Gerenciador de Tráfego

O Azure Resource Manager é a interface de gerenciamento preferida dos serviços no Azure. Os perfis do Gerenciador de Tráfego do Azure podem ser gerenciados usando ferramentas e APIs baseadas no Azure Resource Manager.

## <a name="resource-model"></a>Modelo de recursos

O Gerenciador de Tráfego do Azure é configurado usando um conjunto de configurações chamado de perfil do Gerenciador de Tráfego. Esse perfil contém as configurações de DNS, as configurações de roteamento de tráfego, as configurações de monitoramento de ponto de extremidade e uma lista de pontos de extremidade de serviço para os quais o tráfego é roteado.

Cada perfil do Gerenciador de Tráfego é representado por um recurso do tipo "TrafficManagerProfiles". No nível da API REST, o URI para cada perfil é:

    https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.Network/trafficManagerProfiles/{profile-name}?api-version={api-version}

## <a name="setting-up-azure-powershell"></a>Configurando o PowerShell do Azure

Essas instruções usam o Microsoft Azure PowerShell. O artigo a seguir explica como instalar e configurar o Azure PowerShell.

* [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview)

Os exemplos neste artigo presumem que você tenha um grupo de recursos existente. Você pode criar um grupo de recursos usando o seguinte comando:

```powershell
New-AzureRmResourceGroup -Name MyRG -Location "West US"
```

> [!NOTE]
> O Azure Resource Manager requer que todos os grupos de recursos tenham um local. Esse local é usado como o padrão para os recursos criados no grupo de recursos em questão. No entanto, como os recursos de perfil do Gerenciador de Tráfego são globais, não regionais, a escolha do local do grupo de recursos não afeta o Gerenciador de Tráfego do Azure.

## <a name="create-a-traffic-manager-profile"></a>Criar um perfil do Gerenciador de Tráfego

Para criar um perfil do Gerenciador de Tráfego, use o cmdlet `New-AzureRmTrafficManagerProfile`:

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName contoso -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
```

A tabela a seguir lista os parâmetros:

| Parâmetro | Descrição |
| --- | --- |
| Nome |O nome do recurso para o recurso do perfil do Gerenciador de Tráfego. Perfis no mesmo grupo de recursos devem ter nomes exclusivos. Esse nome é diferente do nome DNS usado para consultas de DNS. |
| ResourceGroupName |O nome do grupo de recursos que contém o recurso do perfil. |
| TrafficRoutingMethod |Especifica o método de roteamento de tráfego usado para determinar qual ponto de extremidade é retornado na resposta a consulta DNS. Os valores possíveis são “Desempenho”, “Ponderado” ou “Prioridade”. |
| RelativeDnsName |Especifica a parte do nome de host do nome DNS fornecido por esse perfil do Gerenciador de Tráfego. Esse valor é combinado ao nome de domínio DNS usado pelo Gerenciador de Tráfego do Azure para formar o nome de domínio totalmente qualificado (FQDN) do perfil. Por exemplo, definindo o valor de “contoso” se torna “contoso.trafficmanager.net.” |
| TTL |Especifica a vida útil (TTL) do DNS em segundos. Essa TTL informa aos resolvedores DNS locais e aos clientes DNS o tempo necessário para armazenar em cache as respostas DNS desse perfil do Gerenciador de Tráfego. |
| MonitorProtocol |Especifica o protocolo a ser usado para monitorar a integridade do ponto de extremidade. Os valores possíveis são “HTTP” e “HTTPS”. |
| MonitorPort |Especifica a porta TCP usada para monitorar a integridade do ponto de extremidade. |
| MonitorPath |Especifica o caminho relativo ao nome de domínio de ponto de extremidade usado para testar a integridade do ponto de extremidade. |

O cmdlet cria um perfil do Gerenciador de Tráfego no Azure e retorna um objeto de perfil correspondente ao PowerShell. Nesse momento, o perfil não contém pontos de extremidade. Para obter mais informações sobre como adicionar pontos de extremidade a um perfil do Gerenciador de Tráfego, consulte [Adicionando pontos de extremidade do Gerenciador de Tráfego](#adding-traffic-manager-endpoints).

## <a name="get-a-traffic-manager-profile"></a>Obter um perfil do Gerenciador de Tráfego

Para recuperar um objeto existente de perfil do Gerenciador de Tráfego, use o cmdlet `Get-AzureRmTrafficManagerProfle`:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
```

Esse cmdlet retorna um objeto de perfil do Gerenciador de Tráfego.

## <a name="update-a-traffic-manager-profile"></a>Atualizar um perfil do Gerenciador de Tráfego

A modificação de perfis do Gerenciador de Tráfego segue um processo de 3 etapas:

1. Recuperar o perfil usando `Get-AzureRmTrafficManagerProfile` ou usar o perfil retornado por `New-AzureRmTrafficManagerProfile`.
2. Modificar o perfil. Você pode adicionar e remover pontos de extremidade ou alterar ponto de extremidade ou parâmetros do perfil. Essas alterações são operações offline. Você está alterando apenas o objeto local na memória que representa o perfil.
3. Confirme as alterações usando o cmdlet `Set-AzureRmTrafficManagerProfile`.

Todas as propriedades de perfil podem ser alteradas, exceto RelativeDnsName do perfil. Para alterar o RelativeDnsName, você deve excluir o perfil e um novo perfil com um novo nome.

O exemplo a seguir demonstra como alterar a TTL do perfil:

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG
$profile.Ttl = 300
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Há três tipos de pontos de extremidade do Gerenciador de Tráfego:

1. Os **pontos de extremidade do Azure** são serviços hospedados no Azure
2. Os **pontos de extremidade externos** são serviços hospedados fora do Azure
3. Os **pontos de extremidade aninhados** são usados para construir hierarquias aninhadas de perfis do Gerenciador de Tráfego. Os pontos de extremidade aninhados habilitam configurações avançadas de roteamento de tráfego para aplicativos complexos.

Em todos os três casos, os pontos de extremidade podem ser adicionados de duas maneiras:

1. Usando um processo de 3 etapas descrito anteriormente. A vantagem desse método é que diversas alterações do ponto de extremidade podem ser feitas em uma única atualização.
2. Usando o cmdlet New-AzureRmTrafficManagerEndpoint. Esse cmdlet adiciona um ponto de extremidade a um perfil existente do Gerenciador de Tráfego em uma única operação.

## <a name="adding-azure-endpoints"></a>Adicionando pontos de extremidade do Azure

Os pontos de extremidade do Azure fazem referência a serviços hospedados no Azure. Há suporte para dois tipos de pontos de extremidade do Azure:

1. Aplicativos Web do Azure 
2. Recursos PublicIpAddress do Azure (que podem ser anexados ao balanceador de carga ou a uma NIC de máquina virtual). O PublicIpAddress deve ter um nome DNS atribuído para poder ser usado no Gerenciador de Tráfego.

Em cada caso:

* O serviço é especificado usando o parâmetro 'targetResourceId' de `Add-AzureRmTrafficManagerEndpointConfig` ou `New-AzureRmTrafficManagerEndpoint`.
* O “Target” e “EndpointLocation” são deduzidos pelo TargetResourceId.
* A especificação de “Weight” é opcional. Os pesos só serão usados se o perfil for configurado para usar o método de roteamento de tráfego “Weighted”. Caso contrário, eles serão ignorados. Se especificado, o valor deve ser um número entre 1 e 1000. O valor padrão é '1'.
* A especificação de “Priority” é opcional. As prioridades só serão usadas se o perfil for configurado para usar o método de roteamento de tráfego “Priority”. Caso contrário, eles serão ignorados. Os valores válidos são de 1 a 1000; valores mais baixos indicam uma prioridade mais alta. Se especificados para um ponto de extremidade, deverão ser especificados para todos os pontos de extremidade. Se omitidos, os valores padrão começando por 1 serão aplicados na ordem em que os pontos de extremidade forem listados.

### <a name="example-1-adding-web-app-endpoints-using-add-azurermtrafficmanagerendpointconfig"></a>Exemplo 1: adicionar pontos de extremidade do aplicativo Web usando `Add-AzureRmTrafficManagerEndpointConfig`

Neste exemplo, podemos criar um perfil do Gerenciador de Tráfego e adicionar dois pontos de extremidade do aplicativo Web usando o cmdlet `Add-AzureRmTrafficManagerEndpointConfig`.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$webapp1 = Get-AzureRMWebApp -Name webapp1
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp1ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp1.Id -EndpointStatus Enabled
$webapp2 = Get-AzureRMWebApp -Name webapp2
Add-AzureRmTrafficManagerEndpointConfig -EndpointName webapp2ep -TrafficManagerProfile $profile -Type AzureEndpoints -TargetResourceId $webapp2.Id -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```
### <a name="example-2-adding-a-publicipaddress-endpoint-using-new-azurermtrafficmanagerendpoint"></a>Exemplo 2: Adicionar um ponto de extremidade publicIpAddress usando `New-AzureRmTrafficManagerEndpoint`

Neste exemplo, um recurso de endereço IP público é adicionado ao perfil do Gerenciador de Tráfego. O endereço IP público deve ter um nome DNS configurado e pode ser vinculado à NIC de uma VM ou a um balanceador de carga.

```powershell
$ip = Get-AzureRmPublicIpAddress -Name MyPublicIP -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name MyIpEndpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type AzureEndpoints -TargetResourceId $ip.Id -EndpointStatus Enabled
```

## <a name="adding-external-endpoints"></a>Adicionando pontos de extremidade externos

O Gerenciador de Tráfego usa pontos de extremidade externos para direcionar o tráfego para serviços hospedados fora do Azure. Como com pontos de extremidade do Azure, pontos de extremidade externos podem ser adicionados usando `Add-AzureRmTrafficManagerEndpointConfig` seguido por `Set-AzureRmTrafficManagerProfile` ou `New-AzureRMTrafficManagerEndpoint`.

Ao especificar pontos de extremidade externos:

* O nome de domínio do ponto de extremidade deve ser especificado usando o parâmetro ‘Target’
* Se o método de roteamento de tráfego “Desempenho” for usado, o 'EndpointLocation' será necessário. Caso contrário, será opcional. O valor deve ser um [nome válido da região do Azure](https://azure.microsoft.com/regions/).
* “Weight” e “Priority” são opcionais.

### <a name="example-1-adding-external-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Exemplo 1: adicionar pontos de extremidade externos usando `Add-AzureRmTrafficManagerEndpointConfig` e `Set-AzureRmTrafficManagerProfile`

Neste exemplo, podemos criar um perfil do Gerenciador de Tráfego, adicionar dois pontos de extremidade externos e confirmar as alterações.

```powershell
$profile = New-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName myapp -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName eu-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointLocation "North Europe" -EndpointStatus Enabled
Add-AzureRmTrafficManagerEndpointConfig -EndpointName us-endpoint -TrafficManagerProfile $profile -Type ExternalEndpoints -Target app-us.contoso.com -EndpointLocation "Central US" -EndpointStatus Enabled
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-adding-external-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Exemplo 2: adicionar pontos de extremidade externos usando `New-AzureRmTrafficManagerEndpoint`

Neste exemplo, adicionamos um ponto de extremidade externo a um perfil existente. O perfil é especificado usando os nomes de grupo de recursos e perfil.

```powershell
New-AzureRmTrafficManagerEndpoint -Name eu-endpoint -ProfileName MyProfile -ResourceGroupName MyRG -Type ExternalEndpoints -Target app-eu.contoso.com -EndpointStatus Enabled
```

## <a name="adding-nested-endpoints"></a>Adicionando pontos de extremidade ‘aninhados’

Cada perfil do Gerenciador de Tráfego especifica um único método de roteamento de tráfego. No entanto, há cenários que exigem um roteamento de tráfego mais sofisticado do que o roteamento fornecido por um único perfil do Gerenciador de Tráfego. Aninhe perfis do Gerenciador de Tráfego para combinar os benefícios de mais de um método de roteamento de tráfego. Perfis aninhados permitem que você substitua o comportamento do Gerenciador de Tráfego padrão para fornecer suporte a implantações de aplicativos maiores e mais complexas. Para obter mais exemplos, consulte [Perfis aninhados do Gerenciador de Tráfego](traffic-manager-nested-profiles.md).

Os pontos de extremidade aninhados são configurados no perfil pai, usando um tipo de ponto de extremidade específico, o ‘NestedEndpoints’. Ao especificar pontos de extremidade aninhados:

* O ponto de extremidade deve ser especificado usando o parâmetro 'targetResourceId'
* Se o método de roteamento de tráfego “Desempenho” for usado, o 'EndpointLocation' será necessário. Caso contrário, será opcional. O valor deve ser um [nome válido da região do Azure](http://azure.microsoft.com/regions/).
* 'Weight' e 'Priority' são opcionais, como os Pontos de Extremidade do Azure.
* O parâmetro “MinChildEndpoints” é opcional. O valor padrão é '1'. Caso o número de pontos de extremidade disponíveis esteja abaixo desse limite, o perfil pai considerará o perfil filho como “prejudicado” e desviará o tráfego para os outros pontos de extremidade do perfil pai.

### <a name="example-1-adding-nested-endpoints-using-add-azurermtrafficmanagerendpointconfig-and-set-azurermtrafficmanagerprofile"></a>Exemplo 1: adicionar pontos de extremidade aninhados usando `Add-AzureRmTrafficManagerEndpointConfig` e `Set-AzureRmTrafficManagerProfile`

Neste exemplo, podemos criar novos perfis pai e filho do Gerenciador de Tráfego, adicionar o filho como um ponto de extremidade aninhado no pai e confirmar as alterações.

```powershell
$child = New-AzureRmTrafficManagerProfile -Name child -ResourceGroupName MyRG -TrafficRoutingMethod Priority -RelativeDnsName child -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
$parent = New-AzureRmTrafficManagerProfile -Name parent -ResourceGroupName MyRG -TrafficRoutingMethod Performance -RelativeDnsName parent -Ttl 30 -MonitorProtocol HTTP -MonitorPort 80 -MonitorPath "/"
Add-AzureRmTrafficManagerEndpointConfig -EndpointName child-endpoint -TrafficManagerProfile $parent -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

Para não demorarmos neste exemplo, não adicionamos outros pontos de extremidade aos perfis filho ou pai.

### <a name="example-2-adding-nested-endpoints-using-new-azurermtrafficmanagerendpoint"></a>Exemplo 2: adicionar pontos de extremidade aninhados usando `New-AzureRmTrafficManagerEndpoint`

Neste exemplo, adicionamos um perfil filho existente como um ponto de extremidade aninhado a um perfil pai existente. O perfil é especificado usando os nomes de grupo de recursos e perfil.

```powershell
$child = Get-AzureRmTrafficManagerEndpoint -Name child -ResourceGroupName MyRG
New-AzureRmTrafficManagerEndpoint -Name child-endpoint -ProfileName parent -ResourceGroupName MyRG -Type NestedEndpoints -TargetResourceId $child.Id -EndpointStatus Enabled -EndpointLocation "North Europe" -MinChildEndpoints 2
```

## <a name="update-a-traffic-manager-endpoint"></a>Atualizar um Ponto de Extremidade do Gerenciador de Tráfego

Há duas maneiras de atualizar um ponto de extremidade existente do Gerenciador de Tráfego:

1. Obtenha o perfil do Gerenciador de Tráfego usando `Get-AzureRmTrafficManagerProfile`, atualize as propriedades do ponto de extremidade no perfil e confirme as alterações usando `Set-AzureRmTrafficManagerProfile`. Esse método apresenta a vantagem de poder atualizar mais de um ponto de extremidade em uma única operação.
2. Obtenha o ponto de extremidade do Gerenciador de Tráfego usando `Get-AzureRmTrafficManagerEndpoint`, atualize as propriedades do ponto de extremidade e confirme as alterações usando `Set-AzureRmTrafficManagerEndpoint`. Esse método é mais simples, pois não exige a indexação na matriz dos Pontos de Extremidade no perfil.

### <a name="example-1-updating-endpoints-using-get-azurermtrafficmanagerprofile-and-set-azurermtrafficmanagerprofile"></a>Exemplo 1: atualizar pontos de extremidade usando `Get-AzureRmTrafficManagerProfile` e `Set-AzureRmTrafficManagerProfile`

Neste exemplo, modificamos a prioridade em dois pontos de extremidade em um perfil existente.

```powershell
$profile = Get-AzureRmTrafficManagerProfile -Name myprofile -ResourceGroupName MyRG
$profile.Endpoints[0].Priority = 2
$profile.Endpoints[1].Priority = 1
Set-AzureRmTrafficManagerProfile -TrafficManagerProfile $profile
```

### <a name="example-2-updating-an-endpoint-using-get-azurermtrafficmanagerendpoint-and-set-azurermtrafficmanagerendpoint"></a>Exemplo 2: atualizar um ponto de extremidade usando `Get-AzureRmTrafficManagerEndpoint` e `Set-AzureRmTrafficManagerEndpoint`

Neste exemplo, modificamos o peso de um ponto de extremidade simples em um perfil existente.

```powershell
$endpoint = Get-AzureRmTrafficManagerEndpoint -Name myendpoint -ProfileName myprofile -ResourceGroupName MyRG -Type ExternalEndpoints
$endpoint.Weight = 20
Set-AzureRmTrafficManagerEndpoint -TrafficManagerEndpoint $endpoint
```

## <a name="enabling-and-disabling-endpoints-and-profiles"></a>Habilitando e desabilitando pontos de extremidade e perfis

O Gerenciador de Tráfego permite que os pontos de extremidade individuais sejam habilitados e desabilitados, além de permitir a habilitação e a desabilitação de perfis inteiros.
Faça essas alterações ao obter/atualizar/definir os recursos de ponto de extremidade ou de perfil. Para simplificar essas operações comuns, eles também têm suporte por meio de cmdlets dedicados.

### <a name="example-1-enabling-and-disabling-a-traffic-manager-profile"></a>Exemplo 1: Habilitando e desabilitando um perfil do Gerenciador de Tráfego

Para habilitar um perfil do Gerenciador de Tráfego, use `Enable-AzureRmTrafficManagerProfile`. O perfil pode ser especificado usando um objeto de perfil. O objeto de perfil pode ser passado por meio do pipeline ou usando o parâmetro '-TrafficManagerProfile'. Neste exemplo, podemos especificar o perfil pelo nome do grupo de recursos e perfil.

```powershell
Enable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

Para desabilitar um perfil do Gerenciador de Tráfego:

```powershell
Disable-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyResourceGroup
```

O cmdlet Disable-AzureRmTrafficManagerProfile solicita confirmação. Esse aviso pode ser suprimido usando o parâmetro '-Force'.

### <a name="example-2-enabling-and-disabling-a-traffic-manager-endpoint"></a>Exemplo 2: Habilitando e desabilitando um ponto de extremidade do Gerenciador de Tráfego

Para habilitar um ponto de extremidade do Gerenciador de Tráfego, use `Enable-AzureRmTrafficManagerEndpoint`. Há duas maneiras de especificar o ponto de extremidade

1. Usando um objeto TrafficManagerEndpoint passado pelo pipeline ou usando o parâmetro '-TrafficManagerEndpoint'
2. Usando o nome do ponto de extremidade, o tipo de ponto de extremidade, o nome do perfil e o nome do grupo de recursos:

```powershell
Enable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Da mesma forma, para desabilitar um ponto de extremidade do Gerenciador de Tráfego:

```powershell
Disable-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG -Force
```

Assim como acontece com `Disable-AzureRmTrafficManagerProfile`, o cmdlet `Disable-AzureRmTrafficManagerEndpoint` solicita confirmação. Esse aviso pode ser suprimido usando o parâmetro '-Force'.

## <a name="delete-a-traffic-manager-endpoint"></a>Excluir um Ponto de Extremidade do Gerenciador de Tráfego

Para remover pontos de extremidade individuais, use o cmdlet `Remove-AzureRmTrafficManagerEndpoint`:

```powershell
Remove-AzureRmTrafficManagerEndpoint -Name MyEndpoint -Type AzureEndpoints -ProfileName MyProfile -ResourceGroupName MyRG
```

Esse cmdlet solicita confirmação. Esse aviso pode ser suprimido usando o parâmetro '-Force'.

## <a name="delete-a-traffic-manager-profile"></a>Excluir um perfil do Gerenciador de Tráfego

Para excluir um perfil do Gerenciador de Tráfego, use o cmdlet `Remove-AzureRmTrafficManagerProfile`, especificando os nomes de grupo de recursos e de perfil:

```powershell
Remove-AzureRmTrafficManagerProfile -Name MyProfile -ResourceGroupName MyRG [-Force]
```

Esse cmdlet solicita confirmação. Esse aviso pode ser suprimido usando o parâmetro '-Force'.

O perfil a ser excluído também pode ser especificado usando um objeto de perfil:

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
