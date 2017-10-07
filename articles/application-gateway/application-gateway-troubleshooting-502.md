---
title: erros de Gateway incorreto de Gateway de aplicativo do Azure (502) aaaTroubleshoot | Microsoft Docs
description: Saiba como erros tootroubleshoot 502 de Gateway do aplicativo
services: application-gateway
documentationcenter: na
author: amitsriva
manager: rossort
editor: 
tags: azure-resource-manager
ms.assetid: 1d431ead-d318-47d8-b3ad-9c69f7e08813
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/09/2017
ms.author: amsriva
ms.openlocfilehash: a50f736ac157256a53f6fbe3a208f0c11dd58f4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-bad-gateway-errors-in-application-gateway"></a>Solução de problemas de erros de gateway incorreto no Application Gateway

Saiba como erros (502) de gateway incorreto tootroubleshoot recebeu ao usar o gateway do aplicativo.

## <a name="overview"></a>Visão geral

Depois de configurar um gateway de aplicativo, um dos erros de saudação que os usuários podem encontrar é "Erro de servidor: 502 - o servidor Web recebeu uma resposta inválida enquanto agia como um gateway ou servidor proxy". Este erro pode ocorrer devido a seguir toohello motivos principais:

* O [pool de back-end do Gateway de Aplicativo do Azure não está configurado ou está vazio](#empty-backendaddresspool).
* Nenhum dos Olá VMs ou instâncias em [conjunto de escala de VM estão íntegros](#unhealthy-instances-in-backendaddresspool).
* Máquinas virtuais ou instâncias do conjunto de escala de VM back-end são [não está respondendo investigação de integridade padrão toohello](#problems-with-default-health-probe.md).
* Configuração inválida ou incorreta [de investigações de integridade personalizadas](#problems-with-custom-health-probe.md).
* [Tempo limite de solicitação ou problemas de conectividade](#request-time-out) com solicitações de usuário.

## <a name="empty-backendaddresspool"></a>BackendAddressPool vazio

### <a name="cause"></a>Causa

Se Olá Application Gateway não tem nenhuma VM ou conjunto de escala configurado no pool de endereços de back-end do hello, ele não pode rotear qualquer solicitação de cliente e gerará um erro de gateway incorreto.

### <a name="solution"></a>Solução

Certifique-se de que o pool de endereços de back-end de saudação não está vazio. Isso pode ser feito por meio do PowerShell, da CLI ou do portal.

```powershell
Get-AzureRmApplicationGateway -Name "SampleGateway" -ResourceGroupName "ExampleResourceGroup"
```

saída Olá Olá precede o cmdlet deve conter o pool de endereços de back-end não vazio. A seguir há um exemplo em que são retornados dois pools que estão configurados com endereços FQDN ou IP para VMs de back-end. Olá, estado de provisionamento da saudação BackendAddressPool deve ser 'êxito'.

BackendAddressPoolsText:

```json
[{
    "BackendAddresses": [{
        "ipAddress": "10.0.0.10",
        "ipAddress": "10.0.0.11"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool01",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool01"
}, {
    "BackendAddresses": [{
        "Fqdn": "xyx.cloudapp.net",
        "Fqdn": "abc.cloudapp.net"
    }],
    "BackendIpConfigurations": [],
    "ProvisioningState": "Succeeded",
    "Name": "Pool02",
    "Etag": "W/\"00000000-0000-0000-0000-000000000000\"",
    "Id": "/subscriptions/<subscription id>/resourceGroups/<resource group name>/providers/Microsoft.Network/applicationGateways/<application gateway name>/backendAddressPools/pool02"
}]
```

## <a name="unhealthy-instances-in-backendaddresspool"></a>Instâncias não íntegras em BackendAddressPool

### <a name="cause"></a>Causa

Se todas as instâncias de saudação do BackendAddressPool estiverem não íntegros, Application Gateway não teria qualquer solicitação de usuário tooroute de back-end. Isso também pode ser o caso de Olá quando instâncias de back-end estão íntegros, mas não tem o aplicativo hello necessário implantado.

### <a name="solution"></a>Solução

Certifique-se de que as instâncias de saudação estejam íntegros e aplicativo hello está configurado corretamente. Verifique se capaz de toorespond tooa ping de outra VM em instâncias de back-end de saudação Olá mesma rede virtual. Se configurado com um ponto de extremidade público, certifique-se de que um aplicativo da web do navegador solicitação toohello está operacional.

## <a name="problems-with-default-health-probe"></a>Problemas com a investigação de integridade padrão

### <a name="cause"></a>Causa

502 erros também podem ser frequentes indicadores que Olá investigação de integridade padrão é não é possível tooreach VMs de back-end. Quando uma instância do Application Gateway é provisionada, ele automaticamente configura uma tooeach de investigação de integridade padrão BackendAddressPool usando as propriedades do hello BackendHttpSetting. Nenhum usuário de entrada é necessária tooset essa investigação. Especificamente, quando uma regra de balanceamento de carga é configurada, é feita uma associação entre BackendHttpSetting e BackendAddressPool. Uma investigação de padrão é configurada para cada uma dessas associações e inicia uma instância de tooeach integridade periódicas verificação de conexão no hello BackendAddressPool Olá porta especificada no elemento de BackendHttpSetting Olá a Application Gateway. Tabela a seguir lista os valores de saudação associados a investigação de integridade saudação padrão.

| Propriedades da investigação | Valor | Descrição |
| --- | --- | --- |
| URL de investigação |http://127.0.0.1/ |Caminho da URL |
| Intervalo |30 |Intervalo da investigação em segundos |
| Tempo limite |30 |Tempo limite da investigação em segundos |
| Limite não íntegro |3 |Contagem de repetições da investigação. servidor de back-end Hello está marcado para baixo depois contagem de falhas de investigação consecutivas Olá atinge o limite não íntegro hello. |

### <a name="solution"></a>Solução

* Verifique se um site padrão está configurado e está escutando em 127.0.0.1.
* Se BackendHttpSetting Especifica uma porta diferente de 80, o site padrão de saudação deve ser toolisten configurado na porta.
* Olá toohttp://127.0.0.1:port de chamada deve retornar um código de resultado HTTP de 200. Isso deve ser retornado dentro do período de tempo limite de 30 segundos hello.
* Certifique-se de que a porta configurada está aberta e que não existem regras de firewall ou grupos de segurança de rede do Azure, que bloquear o tráfego de entrada ou de saída na porta de saudação configurado.
* Se as VMs clássicas do Azure ou serviço de nuvem é usado com o FQDN ou IP público, certifique-se de que Olá correspondente [ponto de extremidade](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fapplication-gateway%2ftoc.json) é aberto.
* Se Olá VM é configurada por meio do Gerenciador de recursos do Azure e está fora da saudação redes em que o Gateway de aplicativo é implantado, [grupo de segurança de rede](../virtual-network/virtual-networks-nsg.md) deve ser configurado tooallow acesso Olá desejado de porta.

## <a name="problems-with-custom-health-probe"></a>Problemas com a investigação de integridade personalizada

### <a name="cause"></a>Causa

Investigações de integridade personalizados permitem que o padrão de toohello flexibilidade adicional investigando o comportamento. Ao usar testes personalizados, os usuários podem configurar o intervalo de sondagem hello, Olá URL e tootest de caminho e quantos tooaccept de respostas com falha antes de marcar a instância de pool de back-end hello como não íntegro. Olá propriedades adicionais a seguir é adicionado.

| Propriedades da investigação | Descrição |
| --- | --- |
| Nome |Nome do teste de saudação. Esse nome é usado toorefer toohello investigação em configurações de HTTP de back-end. |
| Protocolo |Protocolo usado toosend investigação de saudação. investigação de saudação usa o protocolo de saudação definido nas configurações de HTTP de back-end de saudação |
| Host |Investigação de saudação do toosend do nome de host. Aplicável somente quando vários sites são configurados no Application Gateway. Isso é diferente do nome de host de VM. |
| Caminho |Caminho relativo da investigação de saudação. caminho válido Olá começa com '/'. teste de saudação é enviado muito\<protocolo\>://\<host\>:\<porta\>\<caminho\> |
| Intervalo |Intervalo de investigação em segundos. Este é o intervalo de tempo de saudação entre duas investigações consecutivos. |
| Tempo limite |Tempo limite da investigação em segundos. Se uma resposta válida não for recebida dentro desse período de tempo limite, investigação hello está marcada como falha. |
| Limite não íntegro |Contagem de repetições da investigação. servidor de back-end Hello está marcado para baixo depois contagem de falhas de investigação consecutivas Olá atinge o limite não íntegro hello. |

### <a name="solution"></a>Solução

Valide que Olá que investigação de integridade personalizado está configurado corretamente como Olá anterior da tabela. Além disso toohello anterior etapas, solução de problemas também Certifique-se de seguir hello:

* Certifique-se de que esse teste hello está especificado corretamente de acordo com a saudação [guia](application-gateway-create-probe-ps.md).
* Se o Gateway do aplicativo está configurado para um único site, por saudação padrão Host nome deve ser especificado como '127.0.0.1', a menos que o contrário configurada na investigação personalizada.
* Certifique-se de que uma chamada toohttp: / /\<host\>:\<porta\>\<caminho\> retorna um código de resultado HTTP de 200.
* Certifique-se de que o intervalo de tempo limite e UnhealtyThreshold estão dentro dos intervalos aceitáveis hello.
* Se usar um HTTPS investigação, certifique-se de que servidor de back-end Olá não requer SNI Configurando um certificado de fallback no próprio servidor de back-end Olá. 
* Certifique-se de que o intervalo de tempo limite e UnhealtyThreshold estão dentro dos intervalos aceitáveis hello.

## <a name="request-time-out"></a>Tempo limite de solicitação

### <a name="cause"></a>Causa

Quando uma solicitação de usuário é recebida, o Application Gateway aplica Olá configurado regras toohello solicitação e encaminha tooa instância de pool de back-end. Ele espera um intervalo configurável de tempo para uma resposta da instância de back-end de saudação. Por padrão, o intervalo é de **30 segundos**. Se o Gateway de Aplicativo não receber uma resposta do aplicativo de back-end nesse intervalo, a solicitação de usuário obterá um erro 502.

### <a name="solution"></a>Solução

Application Gateway permite que usuários tooconfigure essa definição via BackendHttpSetting, que pode ser então aplicadas toodifferent pools. Os pools de back-end diferentes podem ter BackendHttpSetting diferentes e, assim, um tempo limite de solicitação diferente configurado.

```powershell
    New-AzureRmApplicationGatewayBackendHttpSettings -Name 'Setting01' -Port 80 -Protocol Http -CookieBasedAffinity Enabled -RequestTimeout 60
```

## <a name="next-steps"></a>Próximas etapas

Se hello etapas anteriores não resolverem o problema de saudação, abra um [tíquete de suporte](https://azure.microsoft.com/support/options/).

