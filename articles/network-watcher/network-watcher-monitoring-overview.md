---
title: aaaIntroduction tooAzure observador de rede | Microsoft Docs
description: "Esta página fornece uma visão geral da saudação serviço observador de rede para monitorar e visualizar rede conectada recursos no Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 14bc2266-99e3-42a2-8d19-bd7257fec35e
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/11/2017
ms.author: gwallace
ms.openlocfilehash: 283b3fa6add05d9bad6d5dbdae1524344d1bfc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-network-monitoring-overview"></a>Visão geral do monitoramento da rede do Azure

Os clientes criam uma rede de ponta a ponta no Azure administrando e compondo vários recursos de rede individuais, como VNet, ExpressRoute, Gateway de Aplicativo, Balanceadores de carga e mais. Monitoramento está disponível em cada um dos recursos de rede hello. Nós nos referimos toothis monitoramento como o monitoramento de nível de recursos.

rede de tooend Olá end pode ter configurações complexas e as interações entre os recursos, criar cenários complexos que precisam baseada em cenário de monitoramento por meio do observador de rede.

Este artigo aborda o cenário e o monitoramento no nível do recurso. O monitoramento de rede no Azure é completo e abrange duas grandes categorias:

* [**Inspetor de rede** ](#network-watcher) -baseada em cenário de monitoramento é fornecido com recursos de saudação do observador de rede. Esse serviço inclui a captura de pacotes, próximo salto, verificação do fluxo de IP, exibição do grupo de segurança e logs de fluxo de NSG. Monitoramento do nível do cenário fornece uma exibição de tooend final dos recursos de rede no monitoramento de recursos de rede do contraste tooindividual.
* [**Monitoramento de recursos**](#network-resource-level-monitoring) - o monitoramento no nível do recurso é composto de quatro recursos, logs de diagnóstico, métricas, solução de problemas e integridade dos recursos. Todos esses recursos são criados no nível de recursos de rede hello.

## <a name="network-watcher"></a>Observador de Rede

Observador de rede é um serviço regional que permite que você toomonitor e diagnosticar as condições em uma rede cenário nível, para e do Azure. Diagnóstico de rede e as ferramentas de visualização disponíveis com o observador de rede ajudarão-lo a entender, diagnosticar e obter a rede de tooyour insights no Azure.

Observador de rede atualmente tem Olá recursos a seguir:

* **[Topologia](network-watcher-topology-overview.md)**  -fornece uma saudação de mostrando de exibição de nível de rede vários interconexões e associações entre recursos de rede em um grupo de recursos.
* **[Captura de pacotes variável](network-watcher-packet-capture-overview.md)** - captura os dados do pacote dentro e fora de uma máquina virtual. Avançado ajustados controles como sendo tooset capaz de tempo e opções de filtragem e limitações de tamanho fornecem versatilidade. dados de pacote de saudação podem ser armazenados em um repositório de blob ou no disco local do hello no formato. cap.
* **[Verificação do fluxo de IP](network-watcher-ip-flow-verify-overview.md)** - verifica se um pacote é permitido ou negado com base nos parâmetros do pacote com cinco tuplas das informações do fluxo (IP de Destino, IP de Origem, Porta de Destino, Porta de Origem e Protocolo). Se o pacote de saudação é negado por um grupo de segurança, hello regra e o grupo negado de pacote de saudação é retornado.
* **[Próximo salto](network-watcher-next-hop-overview.md)**  -determina o próximo salto Olá para pacotes que está sendo direcionado no hello malha de rede do Azure, permitindo que você rotas toodiagnose qualquer configuradas incorretamente definido pelo usuário.
* **[Exibição de grupo de segurança](network-watcher-security-group-view-overview.md)**  -obtém Olá segurança efetiva e aplicadas regras que são aplicadas em uma máquina virtual.
* **[Log de fluxo de NSG](network-watcher-nsg-flow-logging-overview.md)**  -fluxo de logs para grupos de segurança de rede permitem que você toocapture logs tootraffic relacionados que são permitidas ou negadas pelas regras de segurança de saudação no grupo de saudação. Olá fluxo é definido pelas informações de uma tupla 5 – IP de origem, IP de destino, porta de origem, protocolo e porta de destino.
* **[Gateway de rede virtual e solução de problemas de Conexão](network-watcher-troubleshoot-manage-rest.md)**  -fornece Olá capacidade tootroubleshoot Gateways de rede Virtual e conexões.
* **[Limites de assinatura de rede](#network-subscription-limits)**  -permite o uso de recursos de rede tooview em limites de.
* **[Configurando o Log de diagnóstico](#diagnostic-logs)**  – fornece um único painel tooenable ou desabilitar logs de diagnóstico para recursos de rede em um grupo de recursos.
* **[Conectividade (visualização)](network-watcher-connectivity-overview.md)**  -verifica a possibilidade de saudação do estabelecimento de uma conexão TCP direto de tooa uma máquina virtual que recebe o ponto de extremidade.

### <a name="role-based-access-control-rbac-in-network-watcher"></a>Controle de Acesso baseado em Funções (RBAC) no Observador de Rede

Observador de rede usa Olá [modelo o acesso RBAC (controle)](../active-directory/role-based-access-control-what-is.md). Olá, as seguintes permissões é necessárias pelo Olá observador de rede. É importante toomake se essa função hello usada para iniciar as APIs do Gerenciador da rede ou usando o observador de rede do portal de saudação tem acesso de saudação necessário.

|Recurso| Permissão|
|---|---| 
|Microsoft.Storage/ |Ler|
|Microsoft.Authorization/| Ler| 
|Microsoft.Resources/subscriptions/resourceGroups/| Ler|
|Microsoft.Storage/storageAccounts/listServiceSas/ | Ação|
|Microsoft.Storage/storageAccounts/listAccountSas/ |Ação|
|Microsoft.Storage/storageAccounts/listKeys/ | Ação|
|Microsoft.Compute/virtualMachines/ |Ler|
|Microsoft.Compute/virtualMachines/ |Gravar|
|Microsoft.Compute/virtualMachineScaleSets/ |Ler|
|Microsoft.Compute/virtualMachineScaleSets/ |Gravar|
|Microsoft.Network/networkWatchers/packetCaptures/ |Ler|
|Microsoft.Network/networkWatchers/packetCaptures/| Gravar|
|Microsoft.Network/networkWatchers/packetCaptures/| Excluir|
|Microsoft.Network/networkWatchers/ |Gravar |
|Microsoft.Network/networkWatchers/| Ler |
|Microsoft.Insights/alertRules/ |*|
|Microsoft.Support/ | *|

### <a name="network-subscription-limits"></a>Limites de assinatura da rede

Limites de assinatura de rede fornecem detalhes de uso de saudação de cada um dos recursos de rede de saudação em uma assinatura em uma região com o número máximo de saudação de recursos disponíveis.

![limite de assinatura da rede][nsl]

## <a name="network-resource-level-monitoring"></a>Monitoramento no nível do recurso da rede

Olá recursos a seguir está disponível para o monitoramento de nível de recursos:

### <a name="audit-log"></a>Log de auditoria

Operações executadas como parte da configuração de saudação de redes são registradas. Esses logs podem ser exibidos no portal do Azure de saudação ou recuperados por meio de ferramentas da Microsoft, como o Power BI ou ferramentas de terceiros. Logs de auditoria estão disponíveis por meio do portal hello, PowerShell, CLI e API de Rest. Para obter mais informações sobre os Logs de auditoria, consulte [Operações de auditoria com o Gerenciador de Recursos](../resource-group-audit.md)

Os logs de auditoria estão disponíveis para as operações realizadas em todos os recursos da rede.

### <a name="metrics"></a>Métricas

As métricas são medidas de desempenho e contadores coletados em um período de tempo. As métricas estão disponíveis atualmente para o Gateway de Aplicativo. As métricas podem ser usados tootrigger alertas com base no limite. Consulte [Application Gateway Diagnostics](../application-gateway/application-gateway-diagnostics.md) tooview como métricas podem ser usados toocreate alertas.

![exibição de métricas][metrics]

### <a name="diagnostic-logs"></a>Logs de diagnóstico

Eventos periódicos e espontâneas são criados pelos recursos de rede e registrados em contas de armazenamento, enviadas tooan Hub de eventos ou análise de Log. Esses logs fornecem informações sobre a integridade de saudação de um recurso. Esses logs podem ser visualizados em ferramentas como o Power BI e o Log Analytics. toolearn como logs de diagnóstico tooview, visite [análise de Log](../log-analytics/log-analytics-azure-networking-analytics.md).

Os logs de diagnóstico estão disponíveis para o [Balanceador de Carga](../load-balancer/load-balancer-monitor-log.md), [Grupos de Segurança da Rede](../virtual-network/virtual-network-nsg-manage-log.md), Rotas e [Gateway de Aplicativo](../application-gateway/application-gateway-diagnostics.md).

O Observador de Rede fornece uma exibição dos logs de diagnóstico. Essa exibição contém todos os recursos de rede que oferecem suporte ao log de diagnóstico. Nessa exibição, você pode habilitar e desabilitar os recursos de rede de modo rápido e prático.

![logs][logs]

### <a name="troubleshooting"></a>Solucionar problemas

Olá folha, uma experiência no portal de saudação de solução de problemas é fornecida em recursos de rede atualmente toodiagnose problemas comuns associados a um recurso individual. Essa experiência está disponível para Olá recursos - rota expressa, Gateway de VPN, Application Gateway, os Logs de segurança de rede, rotas, DNS, balanceador de carga e Gerenciador de tráfego de rede a seguir. toolearn mais sobre o recurso nível de solução de problemas, visite [diagnosticar e resolver problemas com a solução de problemas do Azure](https://azure.microsoft.com/blog/azure-troubleshoot-diagonse-resolve-issues/)

![informações da solução de problemas][TS]

### <a name="resource-health"></a>Integridade de recursos

integridade de saudação de um recurso de rede é fornecida em uma base periódica. Tais recursos incluem o Gateway de VPN e o túnel de VPN. Integridade do recurso é acessível em Olá portal do Azure. toolearn mais sobre a integridade de recursos, visite [visão geral de integridade do recurso](../resource-health/resource-health-overview.md)

## <a name="next-steps"></a>Próximas etapas

Depois de conhecer o Observador de Rede, você pode aprender a:

Fazer uma captura de pacote na sua VM visitando [captura de variável de pacote no hello portal do Azure](network-watcher-packet-capture-manage-portal.md)

executar o monitoramento proativo e diagnóstico usando a [captura de pacotes disparada por alertas](network-watcher-alert-triggered-packet-capture.md).

detectar as vulnerabilidades da segurança com [Analisar a captura de pacotes com o Wireshark](network-watcher-deep-packet-inspection.md), usando ferramentas de código-fonte aberto.

Saiba mais sobre alguns dos Olá outra chave [recursos de rede](../networking/networking-overview.md) do Azure.

<!--Image references-->
[TS]: ./media/network-watcher-monitoring-overview/troubleshooting.png
[logs]: ./media/network-watcher-monitoring-overview/logs.png
[metrics]: ./media/network-watcher-monitoring-overview/metrics.png
[nsl]: ./media/network-watcher-monitoring-overview/nsl.png











