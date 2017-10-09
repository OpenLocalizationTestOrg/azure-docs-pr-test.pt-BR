---
title: conectividade do aaaDiagnose local por meio do gateway VPN com o observador de rede do Azure | Microsoft Docs
description: "Este artigo descreve como toodiagnose local conectividade por meio do gateway VPN com a solução de problemas de recurso do observador de rede do Azure."
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: aeffbf3d-fd19-4d61-831d-a7114f7534f9
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 9941c5d1b49bec29062210684dae8653cbdb84b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="diagnose-on-premises-connectivity-via-vpn-gateways"></a>Diagnosticar a conectividade local por meio do Gateway de VPN

Gateway de VPN do Azure permite que você solução híbrida toocreate que atendem a necessidade de saudação para uma conexão segura entre sua rede local e sua rede virtual do Azure. Como seus requisitos são exclusivos, portanto é escolha de saudação do dispositivo VPN local. O Azure atualmente suporta [vários dispositivos VPN](../vpn-gateway/vpn-gateway-about-vpn-devices.md#devicetable) que constantemente são validadas em parceria com fornecedores de dispositivos de saudação. Revisar definições de configuração específicas de dispositivo de saudação antes de configurar seu dispositivo VPN local. Da mesma forma, o Gateway de VPN do Azure está configurado com um conjunto de [parâmetros IPsec suportados](../vpn-gateway/vpn-gateway-about-vpn-devices.md#ipsec) que são usados para estabelecer conexões. Atualmente não há nenhuma maneira de toospecify ou selecione uma combinação específica de parâmetros IPsec da saudação Gateway de VPN do Azure. Para estabelecer uma conexão bem-sucedida entre local e o Azure, Olá local configurações do dispositivo VPN devem estar em conformidade com os parâmetros de IPsec Olá indicados pelo Gateway de VPN do Azure. Se hello configurações estão corretas, se uma perda de conectividade e até agora como solucionar esses problemas não trivial e geralmente levou horas tooidentify e correção de problema de saudação.

Com hello observador de rede do Azure solucionar problemas de recurso, são toodiagnose capaz de quaisquer problemas com o Gateway e conexões e dentro de minutos tem suficiente toomake informações um problema de saudação do toorectify de decisão.

## <a name="scenario"></a>Cenário

Você deseja conexão tooconfigure uma site a site entre o Azure e no local usando FortiGate como Olá Gateway VPN local. tooachieve esse cenário, você pode exigir Olá após a instalação:

1. Gateway de rede virtual - Olá Gateway de VPN no Azure
1. Gateway de rede local - Olá [Gateway de VPN (FortiGate) local](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#LocalNetworkGateway) representação na nuvem do Azure
1. Conexão site a site (diretiva com base em) - [Conexão entre Olá Gateway de VPN e hello roteador local](https://docs.microsoft.com/en-us/azure/vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md#createconnection)
1. [Configuração do FortiGate](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/Site-to-Site_VPN_using_FortiGate.md)

Orientações passo a passo detalhadas para definir uma configuração de Site a Site podem ser encontradas visitando: [criar uma rede virtual com uma conexão Site a Site usando o portal do Azure de saudação](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).

Uma das etapas de configuração crítica Olá é a configuração de parâmetros de comunicação de IPsec hello, qualquer erro de configuração leva tooloss de conectividade entre a rede de local de saudação e do Azure. Atualmente, Gateways de VPN do Azure são Olá toosupport configurado IPsec parâmetros a seguir para a fase 1. Conforme mencionado anteriormente, observe que essas configurações não podem ser modificadas.  Como você pode ver na tabela de saudação abaixo, os algoritmos de criptografia Olá suportados pelo Gateway de VPN do Azure são AES256 e AES128 3DES.

### <a name="ike-phase-1-setup"></a>Fase 1 da configuração IKE

| **Propriedade** | **PolicyBased** | **Gateway de VPN RouteBased e Standard ou de Alto Desempenho** |
| --- | --- | --- |
| Versão IKE |IKEv1 |IKEv2 |
| Grupo Diffie-Hellman |Grupo 2 (1024 bits) |Grupo 2 (1024 bits) |
| Método de autenticação |Chave Pré-Compartilhada |Chave Pré-Compartilhada |
| Algoritmos de criptografia |AES256 AES128 3DES |AES256 3DES |
| Algoritmo de hash |SHA1(SHA128) |SHA1(SHA128), SHA2(SHA256) |
| Tempo de vida (tempo) da SA (associação de segurança) da fase 1 |28.800 segundos |10.800 segundos |

Como um usuário, será necessário tooconfigure seu FortiGate, uma configuração de exemplo pode ser encontrada em [GitHub](https://github.com/Azure/Azure-vpn-config-samples/blob/master/Fortinet/Current/fortigate_show%20full-configuration.txt). Inadvertidamente você configurou seu toouse FortiGate SHA-512 como algoritmo de hash de saudação. Como esse algoritmo não é um algoritmo com suporte para conexões baseadas em política, a conexão VPN funcionará.

Esses problemas são tootroubleshoot disco rígido e causas são geralmente não intuitivos. Nesse caso, você pode abrir suporte tíquete tooget ajuda sobre como resolver o problema de saudação. Mas, com a API de solução de problemas do Observador de Rede do Azure, é possível identificar esses problemas sozinho.

## <a name="troubleshooting-using-azure-network-watcher"></a>Solução de problemas usando o Observador de Rede do Azure

toodiagnose sua conexão, conecte-se tooAzure PowerShell e iniciar Olá `Start-AzureRmNetworkWatcherResourceTroubleshooting` cmdlet. Você pode encontrar hello detalhes sobre como usar este cmdlet na [conexões - PowerShell e solucionar problemas de Gateway de rede Virtual](network-watcher-troubleshoot-manage-powershell.md). Esse cmdlet pode levar toofew toocomplete de minutos.

Após a conclusão do cmdlet hello, você pode navegar toohello local de armazenamento especificado no cmdlet Olá tooget obter informações em sobre o problema de saudação e logs. Observador de rede do Azure cria uma pasta zip que contém Olá arquivos de log a seguir:

![1][1]

Arquivo hello aberto chamado IKEErrors.txt e exibe o seguinte Olá erro, indicando um problema com uma configuração incorreta de configuração de IKE local.

```
Error: On-premises device rejected Quick Mode settings. Check values.
     based on log : Peer sent NO_PROPOSAL_CHOSEN notify
```

Você pode obter informações detalhadas de Olá Scrubbed wfpdiag.txt sobre o erro hello, como nesse caso ela menciona que houve `ERROR_IPSEC_IKE_POLICY_MATCH` que tooconnection lead não está funcionando corretamente.

Outro erro de configuração comum é hello especificando chaves compartilhadas incorretas. Em caso de Olá anterior exemplo especificadas diferentes chaves compartilhadas, Olá IKEErrors.txt mostra Olá erro a seguir: `Error: Authentication failed. Check shared key`.

Recurso de solução de problemas de observador de rede do Azure permite que você toodiagnose e solucionar problemas de seu Gateway de VPN e Conexão com a facilidade de saudação de um simple cmdlet do PowerShell. Atualmente, suporte Olá diagnosticar condições a seguir e está trabalhando para adicionar mais de condição.

### <a name="gateway"></a>Gateway

| Tipo de Falha | Motivo | Registro|
|---|---|---|
| NoFault | Quando nenhum erro é detectado. |Sim|
| GatewayNotFound | Não é possível localizar o Gateway ou o Gateway não está provisionado. |Não|
| PlannedMaintenance |  A instância do gateway está em manutenção.  |Não|
| UserDrivenUpdate | Uma atualização de um usuário está em andamento. Isso pode ser uma operação de redimensionamento. | Não |
| VipUnResponsive | É possível acessar a instância primária de saudação do hello Gateway. Isso acontece quando ocorre falha na investigação de integridade de saudação. | Não |
| PlatformInActive | Há um problema com a plataforma de saudação. | Não|
| ServiceNotRunning | serviço subjacente Olá não está em execução. | Não|
| NoConnectionsFoundForGateway | Nenhuma conexão existe no gateway hello. Isso é apenas um aviso.| Não|
| ConnectionsNotConnected | Nenhuma das conexões Olá estão conectadas. Isso é apenas um aviso.| Sim|
| GatewayCPUUsageExceeded | o uso de Gateway atual Olá uso da CPU é > 95%. | Sim |

### <a name="connection"></a>Conexão

| Tipo de Falha | Motivo | Registro|
|---|---|---|
| NoFault | Quando nenhum erro é detectado. |Sim|
| GatewayNotFound | Não é possível localizar o Gateway ou o Gateway não está provisionado. |Não|
| PlannedMaintenance | A instância do gateway está em manutenção.  |Não|
| UserDrivenUpdate | Uma atualização de um usuário está em andamento. Isso pode ser uma operação de redimensionamento.  | Não |
| VipUnResponsive | É possível acessar a instância primária de saudação do hello Gateway. Isso acontece quando ocorre falha na investigação de integridade de saudação. | Não |
| ConnectionEntityNotFound | A configuração da Conexão está ausente. | Não |
| ConnectionIsMarkedDisconnected | Olá Conexão está marcado como "desconectado". |Não|
| ConnectionNotConfiguredOnGateway | serviço subjacente Olá não tem Olá que Conexão configurada. | Sim |
| ConnectionMarkedStandy | Olá serviço subjacente é marcado como em espera.| Sim|
| Autenticação | Incompatibilidade de chave pré-compartilhada. | Sim|
| PeerReachability | gateway do Hello correspondente não está acessível. | Sim|
| IkePolicyMismatch | gateway de par de saudação tem políticas de IKE que não são suportadas pelo Azure. | Sim|
| Erro WfpParse | Erro ao analisar logs WFP hello. |Sim|

## <a name="next-steps"></a>Próximas etapas

Saiba mais toocheck conectividade de Gateway de VPN com o PowerShell e a automação do Azure visitando [gateways de VPN de Monitor de solução de problemas do observador de rede do Azure](network-watcher-monitor-with-azure-automation.md)

[1]: ./media/network-watcher-diagnose-on-premises-connectivity/figure1.png
