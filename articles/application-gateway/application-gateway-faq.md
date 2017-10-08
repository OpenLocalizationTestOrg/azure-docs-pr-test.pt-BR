---
title: aaaFrequently perguntado para o Gateway de aplicativo do Azure | Microsoft Docs
description: "Esta página fornece respostas toofrequently perguntas frequentes sobre o Gateway de aplicativo do Azure"
documentationcenter: na
services: application-gateway
author: georgewallace
manager: timlt
editor: tysonn
ms.assetid: d54ee7ec-4d6b-4db7-8a17-6513fda7e392
ms.service: application-gateway
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/19/2017
ms.author: gwallace
ms.openlocfilehash: b2df3a82a71a3264d3d34d317d08e4b4f72c6e3e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-application-gateway"></a>Perguntas frequentes sobre o Gateway de Aplicativo

## <a name="general"></a>Geral

**P. O que é o Gateway de Aplicativo?**

O Gateway de Aplicativo do Azure é um ADC (Controlador de Entrega de Aplicativos) como um serviço, oferecendo vários recursos de balanceamento de carga de camada 7 para seus aplicativos. Ele oferece um serviço altamente disponível e escalonável e totalmente gerenciado pelo Azure.

**P. Quais recursos recebem suporte do Gateway de Aplicativo?**

Application Gateway oferece suporte a SSL tooend final e de descarregamento de SSL, Firewall do aplicativo Web, a afinidade de sessão baseada em cookie, url baseadas em caminhos roteamento, várias hospedagem de site e outros. Para obter uma lista completa de recursos com suporte, visite [tooApplication Introdução Gateway](application-gateway-introduction.md)

**P. Qual é a diferença Olá entre o balanceador de carga do Azure e o Application Gateway?**

O Gateway de Aplicativo é um balanceador de carga de camada 7, o que significa que ele funciona com apenas tráfego da Web (HTTP/HTTPS/WebSocket). Ele oferece suporte a recursos como terminação SSL, a afinidade de sessão baseada em cookie e round robin para tráfego de balanceamento de carga. Balanceador de carga, equilibra a carga do tráfego na camada 4 (TCP/UDP).

**P. Quais protocolos recebem suporte do Gateway de Aplicativo?**

O Gateway de Aplicativo oferece suporte a WebSocket, HTTP e HTTPS.

**P. Quais recursos têm suporte atualmente como parte do pool de back-end?**

Pools de back-end podem ser formados por NICs, conjuntos de dimensionamento de máquinas virtuais, IPs públicos, IPs internos, FQDN (nomes de domínio totalmente qualificados) e back-ends multilocatário como Aplicativos Web do Azure . Application Gateway membros do pool de back-end não são ligadas tooan conjunto de disponibilidade. Os membros de pools de back-end podem existir entre clusters, data centers ou fora do Azure, desde que tenham conectividade IP.

**P. Quais regiões Olá serviço está disponível em?**

O Gateway de Aplicativo está disponível em todas as regiões do Azure global. Ele também está disponível no [Azure China](https://www.azure.cn/) e no [Azure Governamental](https://azure.microsoft.com/en-us/overview/clouds/government/)

**P. Ele é uma implantação dedicada à minha assinatura ou é compartilhado entre os clientes?**

O Gateway de Aplicativo é uma implementação dedicada em sua rede virtual.

**P. O redirecionamento HTTP-> HTTPS tem suporte?**

Há suporte para redirecionamento. Visite [visão geral de redirecionamento do Application Gateway](application-gateway-redirect-overview.md) toolearn mais.

**P. Em que ordem os ouvintes são processados?**

Ouvintes são processados na ordem de saudação que são mostradas. Por esse motivo, se um ouvinte básico corresponder a uma solicitação de entrada, ele a processará primeiro.  Ouvintes de vários locais devem ser configurados antes que o tráfego de tooensure um ouvinte básico é roteado toohello correto back-end.

**P. Onde posso encontrar o IP e o DNS do Gateway de Aplicativo?**

Ao usar um endereço IP público como um ponto de extremidade, essas informações podem ser encontradas no recurso de endereço IP público hello, ou na página de visão geral de saudação para Olá Application Gateway no portal de saudação. Para os endereços IP internos, isso pode ser encontrado na página de visão geral de saudação.

**P. Hello IP ou DNS muda com o tempo de vida de saudação do hello Application Gateway?**

Olá VIP pode alterar se gateway Olá é interrompido e iniciado pelo cliente hello. Olá DNS associado com o Application Gateway não altera ciclo de vida de saudação do gateway de saudação. Por esse motivo, é recomendável toouse um alias CNAME e aponte-endereço DNS de toohello de saudação Application Gateway.

**P. O Gateway de Aplicativo oferece suporte a IP estático?**

Não, o Gateway de Aplicativo não oferece suporte a endereços IP públicos estáticos, mas oferece suporte a IPs estáticos internos.

**P. Application Gateway dá suporte a vários IPs públicos no gateway Olá?**

Há suporte a apenas um endereço IP público em um Gateway de Aplicativo.

**P. O Gateway de Aplicativo oferece suporte a cabeçalhos x-forwarded-for?**

Sim, Application Gateway insere x-encaminhado-para, proto encaminhados x e cabeçalhos de porta encaminhados x em solicitação Olá encaminhados toohello back-end. formato de saudação do cabeçalho x-encaminhado-para é uma lista separada por vírgulas de IP: porta. os valores válidos para proto encaminhados x Olá são http ou https. Porta encaminhados X Especifica a porta de saudação no qual solicitação Olá atingida em Olá Application Gateway.

**P. Quanto tempo leva toodeploy um Application Gateway? O meu Gateway de Aplicativo ainda funciona quando está sendo atualizado?**

Novas implantações do Application Gateway podem demorar até too20 tooprovision de minutos. Alterações tooinstance tamanho/contagem não precisam de interrupções e gateway Olá permanece ativa durante esse tempo.

## <a name="configuration"></a>Configuração

**P. O Gateway de Aplicativo é sempre implantado em uma rede virtual?**

Sim, o Gateway de Aplicativo é sempre implantado em uma sub-rede de rede virtual. Essa sub-rede só pode conter Gateways de Aplicativos.

**P. Application Gateway pode falar tooinstances fora de sua rede virtual?**

Gateway de aplicativo pode se comunicar tooinstances fora da rede virtual de saudação que está em como não há conectividade IP. Se você estiver planejando toouse IPs internos como membros do pool de back-end, ele requer [emparelhamento VNET](../virtual-network/virtual-network-peering-overview.md) ou [Gateway VPN](../vpn-gateway/vpn-gateway-about-vpngateways.md).

**P. Posso implantar tudo na sub-rede do Application Gateway Olá?**

Não, mas você pode implantar outros application gateways na sub-rede hello.

**P. Há suporte para grupos de segurança de rede na sub-rede de Gateway do aplicativo hello?**

Grupos de segurança de rede têm suporte na sub-rede de Gateway do aplicativo hello com hello restrições a seguir:

* Exceções devem ser colocadas tráfego de entrada nas portas 65534 65503 para toowork de integridade de back-end corretamente.

* A conectividade de internet de saída não pode ser bloqueada.

* Tráfego de saudação marca AzureLoadBalancer deve ser permitido.

**P. Quais são os limites de saudação no Application Gateway? Posso aumentar esses limites?**

Visite [limites de Gateway do aplicativo](../azure-subscription-service-limits.md#application-gateway-limits) tooview Olá limites.

**P. Posso usar o Gateway de Aplicativo para tráfego interno e externo ao mesmo tempo?**

Sim, o Gateway de Aplicativo oferece suporte a um endereço IP interno e um IP externo por Gateway de Aplicativo.

**P. Há suporte para o emparelhamento VNet?**

Sim, o emparelhamento VNet tem suporte e é útil para o balanceamento de carga de tráfego em outras redes virtuais.

**P. Posso falar servidores locais tooon quando eles estão conectados por túneis de rota expressa ou VPN?**

Sim, contanto que o tráfego seja permitido.

**P. Posso ter um pool de back-end que atende a muitos aplicativos em portas diferentes?**

Há suporte para arquitetura de microsserviço. Você precisaria de vários tooprobe de configurações de http em portas diferentes.

**P. Investigações personalizadas têm suporte para curingas/regex nos dados de resposta?**

As investigações personalizadas não têm suporte para curingas/regex nos dados de resposta. 

**P. Como as regras são processadas?**

Regras são processadas na ordem Olá que estão configurados. É recomendável que as regras de vários locais são configuradas antes chance de saudação de tooreduce regras básicas que o tráfego é roteada back-end do toohello inadequado como regra básica Olá corresponderia tráfego com base em regra de multissite toohello anterior de porta que está sendo avaliada.

**P. Como as regras são processadas?**

Regras são processadas na ordem de saudação que são criados. É recomendável que as regras multissite sejam configuradas antes das regras básicas. Ao configurar primeiro ouvintes de vários locais, essa configuração reduz a chance de saudação que o tráfego é back-end do toohello roteados inadequados. Esse problema de roteamento pode ocorrer enquanto a regra básica Olá corresponderia tráfego com base em regra de multissite toohello anterior de porta que está sendo avaliada.

**P. O que o campo do Host Olá para testes personalizados significam?**

O campo do host Especifica Olá nome toosend Olá a investigação. Aplicável somente quando vários sites são configurados no Gateway de Aplicativo; do contrário, use '127.0.0.1'. Esse valor é diferente do nome de host da VM e está no formato \<protocolo\>://\<host\>:\<porta\>\<caminho\>.

**P. É possível lista branca Application Gateway acesso tooa alguns IPs de origem?**

Esse cenário pode ser feito usando os NSGs na sub-rede de Gateway de Aplicativo. Olá restrições a seguir deve ser colocado na sub-rede Olá Olá listado ordem de prioridade:

* Permitir tráfego de entrada de intervalo de IP/IP de origem.

* Permitir solicitações de entrada de todas as fontes tooports 65534 65503 para [comunicação de integridade de back-end](application-gateway-diagnostics.md).

* Permitir entradas investigações do balanceador de carga do Azure (marca AzureLoadBalancer) e tráfego de rede virtual (marca VirtualNetwork) em Olá [NSG](../virtual-network/virtual-networks-nsg.md).

* Bloquear todo o outro tráfego de entrada com um Negar todas as regras.

* Permitir tráfego de saída toohello internet para todos os destinos.

## <a name="performance"></a>Desempenho

**P. Como o Gateway de Aplicativo oferece suporte a alta disponibilidade e escalabilidade?**

O Gateway de Aplicativo dará suporte a cenários de alta disponibilidade quando você tiver duas ou mais instâncias implantadas. Azure distribui essas instâncias por atualização e falha tooensure domínios que todas as instâncias não falham em Olá simultaneamente. Application Gateway oferece suporte à escalabilidade adicionando várias instâncias do hello mesma carga de saudação tooshare de gateway.

**P. Como posso obter o cenário de recuperação de desastres em data centers com o Gateway de Aplicativo?**

Os clientes podem usar o Traffic Manager toodistribute tráfego entre vários Gateways de aplicativo em diferentes data centers.

**P. Há suporte para o dimensionamento automático?**

Não, mas Application Gateway tem uma métrica de taxa de transferência que pode ser usado tooalert quando um limite for atingido. Manualmente adicionando instâncias ou alterando o tamanho não reinicie o gateway de saudação e não afeta o tráfego existente.

**P. A escala/redução vertical causa tempo de inatividade?**

Não há tempo de inatividade, as instâncias são distribuídas entre domínios de atualização e domínios de falha.

**P. Pode alterar o tamanho da instância de médio toolarge sem interrupção?**

Sim, o Azure distribui instâncias por atualização e falha tooensure domínios que todas as instâncias não falham em Olá simultaneamente. Aplicativo Gateway oferece suporte ao dimensionamento adicionando várias instâncias do hello mesmo gateway tooshare Olá de carga.

## <a name="ssl-configuration"></a>Configuração de SSL

**P. Quais certificados têm suporte no Gateway de Aplicativo?**

Certificados autoassinados, certificados de autoridade de certificação e certificados curinga têm suporte. Não há suporte para certificados EV.

**P. Quais são os conjuntos de codificação atual Olá suportados pelo Gateway de aplicativo?**

Olá seguem Olá atual codificação que recebe suportada pelo gateway do aplicativo. Visite: [configurar SSL versões de política e conjuntos de codificação no Application Gateway](application-gateway-configure-ssl-policy-powershell.md) toolearn como toocustomize opções de SSL.

- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_RSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA
- TLS_DHE_RSA_WITH_AES_256_GCM_SHA384
- TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
- TLS_DHE_RSA_WITH_AES_256_CBC_SHA
- TLS_DHE_RSA_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_AES_256_GCM_SHA384
- TLS_RSA_WITH_AES_128_GCM_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA256
- TLS_RSA_WITH_AES_128_CBC_SHA256
- TLS_RSA_WITH_AES_256_CBC_SHA
- TLS_RSA_WITH_AES_128_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_256_GCM_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_GCM_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA384
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA256
- TLS_ECDHE_ECDSA_WITH_AES_256_CBC_SHA
- TLS_ECDHE_ECDSA_WITH_AES_128_CBC_SHA
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA256
- TLS_DHE_DSS_WITH_AES_256_CBC_SHA
- TLS_DHE_DSS_WITH_AES_128_CBC_SHA
- TLS_RSA_WITH_3DES_EDE_CBC_SHA
- TLS_DHE_DSS_WITH_3DES_EDE_CBC_SHA

**P. Application Gateway também suporta o back-end toohello de tráfego criptografado?**

Sim, descarregamento SSL do Application Gateway oferece suporte e final tooend SSL, que criptografa novamente back-end toohello de tráfego hello.

**P. Pode configurar versões de protocolo SSL do SSL política toocontrol?**

Sim, você pode configurar o Application Gateway toodeny TLS 1.0 por, 1.1 e TLS 1.2. SSL 2.0 e 3.0 já estão desabilitados por padrão e não são configuráveis.

**P. Posso configurar conjuntos de codificação e a ordem de política?**

Sim, há suporte para [configuração de conjuntos de criptografia](application-gateway-ssl-policy-overview.md). Ao definir uma política personalizada, pelo menos uma das Olá conjuntos de codificação a seguir deve ser habilitada. Gateway de aplicativo usa o gerenciamento de back-end de toofor SHA256.

* TLS_ECDHE_RSA_WITH_AES_128_GCM_SHA256 
* TLS_ECDHE_RSA_WITH_AES_128_CBC_SHA256
* TLS_DHE_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_128_GCM_SHA256
* TLS_RSA_WITH_AES_256_CBC_SHA256
* TLS_RSA_WITH_AES_128_CBC_SHA256

**P. Há suporte para quantos certificados SSL?**

O SSL too20 certificados têm suporte.

**P. Quantos certificados de autenticação para nova criptografia de back-end têm suporte?**

Backup too10 certificados de autenticação são compatíveis com um padrão de 5.

**P. O Gateway de Aplicativo é integrado ao Azure Key Vault de forma nativa?**

Não, ele não é integrado ao Azure Key Vault.

## <a name="web-application-firewall-waf-configuration"></a>Configuração de WAF (Firewall de Aplicativo Web)

**P. Olá SKU WAF oferece todos os recursos de saudação disponíveis com hello SKU padrão?**

Sim, WAF dá suporte a todos os recursos de saudação em Olá SKU padrão.

**P. Qual é versão CRS Olá que Application Gateway oferece suporte?**

O Gateway de Aplicativo dá suporte a CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) e a CRS [3.0](application-gateway-crs-rulegroups-rules.md#owasp30).

**P. Como monitorar o WAF?**

O WAF é monitorado por meio do log de diagnóstico. Encontre mais informações sobre o log de diagnóstico em [Log de diagnósticos e métricas para o Gateway de Aplicativo](application-gateway-diagnostics.md)

**P. O modo de detecção bloqueia o tráfego?**

Não, o modo de detecção apenas registra o tráfego em log, o que dispara uma regra WAF.

**P. Como posso personalizar regras WAF?**

Sim, regras de WAF são personalizáveis, para obter mais informações sobre como toocustomize-los visite [WAF personalizar regras e grupos de regras](application-gateway-customize-waf-rules-portal.md)

**P. Quais regras estão disponíveis no momento?**

WAF atualmente suporta CRS [2.2.9](application-gateway-crs-rulegroups-rules.md#owasp229) e [3.0](application-gateway-crs-rulegroups-rules.md#owasp30), que fornecem segurança de linha de base em relação a maioria das Olá vulnerabilidades de 10 principais identificadas pelo Olá abra Web aplicativo segurança projeto (OWASP) encontrada aqui [OWASP top 10 vulnerabilidades](https://www.owasp.org/index.php/Top10#OWASP_Top_10_for_2013)

* Proteção contra injeção de SQL

* Proteção contra scripts entre sites

* Proteção Contra Ataques Comuns da Web, como a injeção de comandos, as solicitações HTTP indesejadas, a divisão de resposta HTTP e o ataque de inclusão de arquivo remoto

* Proteção contra violações de protocolo HTTP

* Proteção contra anomalias de protocolo HTTP, como ausência de host de agente do usuário e de cabeçalhos de aceitação

* Prevenção contra bots, rastreadores e scanners

* Detecção de problemas de configuração de aplicativo comuns (ou seja, Apache, IIS etc.)

**P. O WAF também oferece suporte à prevenção de DDoS?**

Não, o WAF não oferece prevenção de DDoS.

## <a name="diagnostics-and-logging"></a>Diagnóstico e registro em log

**P. Quais tipos de logs estão disponíveis com o Gateway de Aplicativo?**

Há três logs disponíveis para o Gateway de Aplicativo. Para saber mais sobre esses logs e outros recursos de diagnóstico, visite [Integridade de back-end, logs de diagnóstico e métricas para o Gateway de Aplicativo](application-gateway-diagnostics.md).

- **ApplicationGatewayAccessLog** -log de acesso Olá contém cada solicitação enviada toohello Application Gateway front-end. dados de saudação incluem IP do chamador Olá, URL solicitada, latência de resposta, retornam o código, bytes de entrada e saída. O log de acesso é coletado a cada 300 segundos. Esse log contém um registro por instância do Gateway de Aplicativo.
- **ApplicationGatewayPerformanceLog** -log de desempenho Olá captura informações de desempenho de base por instância incluindo solicitação total atendida, a taxa de transferência em bytes, o total de solicitações atendidas, contagem de solicitação com falha, com e sem integridade Contagem de instâncias de back-end.
- **ApplicationGatewayFirewallLog** -log de firewall Olá contém solicitações que são registradas por meio do modo de detecção ou prevenção de um gateway de aplicativo que é configurado com o firewall do aplicativo web.

**P. Como saber se os membros de meu pool de back-end estão íntegros?**

Você pode usar o cmdlet do PowerShell Olá `Get-AzureRmApplicationGatewayBackendHealth` ou verificar a integridade por meio do portal Olá visitando [diagnóstico de Gateway do aplicativo](application-gateway-diagnostics.md)

**P. O que é a política de retenção Olá Olá logs de diagnóstico?**

Conta de armazenamento do fluxo toohello clientes de logs de diagnóstico e os clientes podem definir a política de retenção de saudação com base em suas preferências. Logs de diagnóstico também podem ser enviados tooan Hub de eventos ou análise de Log. Visite [Diagnósticos do Gateway de Aplicativo](application-gateway-diagnostics.md) para obter mais detalhes.

**P. Como posso obter logs de auditoria para o Gateway de Aplicativo?**

Os logs de auditoria estão disponíveis para o Gateway de Aplicativo. No portal de saudação, clique em **Log de atividades** na folha de menu de saudação de um log de auditoria do Application Gateway tooaccess hello. 

**P. Posso configurar alertas com o Gateway de Aplicativo?**

Sim, o Gateway de Aplicativo oferece suporte a alertas, e os alertas são configurados com base em métricas.  Application Gateway tem uma métrica de "taxa de transferência de", que pode ser tooalert configurado no momento. toolearn mais sobre alertas, visite [receber notificações de alerta](../monitoring-and-diagnostics/insights-receive-alert-notifications.md).

**P. A integridade do back-end retorna um status desconhecido, o que pode estar causando esse status?**

motivo mais comum de saudação é back-end toohello de acesso está sendo bloqueado por um NSG ou DNS personalizado. Visite [back-end integridade, o log de diagnóstico e métricas para o Application Gateway](application-gateway-diagnostics.md) toolearn mais.

## <a name="next-steps"></a>Próximas etapas

toolearn mais sobre o Application Gateway visite [tooApplication Introdução Gateway](application-gateway-introduction.md).
