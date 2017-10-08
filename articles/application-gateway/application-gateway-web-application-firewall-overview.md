---
title: firewall do aplicativo aaaIntroduction tooweb (WAF) para o Gateway de aplicativo do Azure | Microsoft Docs
description: "Esta página fornece uma visão geral do WAF (Firewall do aplicativo Web) do Gateway de Aplicativo"
documentationcenter: na
services: application-gateway
author: amsriva
manager: rossort
editor: amsriva
ms.assetid: 04b362bc-6653-4765-86f6-55ee8ec2a0ff
ms.service: application-gateway
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/03/2017
ms.author: amsriva
ms.openlocfilehash: 5a42ce0fb2bd12a391844099e2de8fa2571195e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="web-application-firewall-waf"></a>Firewall do aplicativo Web (WAF)

O Firewall do aplicativo Web (WAF) é um recurso do Gateway de Aplicativo que fornece proteção centralizada de seus aplicativos Web de vulnerabilidades e explorações comuns. 

Firewall do aplicativo Web é baseada em regras de saudação [conjuntos de regras de núcleo OWASP](https://www.owasp.org/index.php/Category:OWASP_ModSecurity_Core_Rule_Set_Project) 3.0 ou 2.2.9. Os aplicativos Web cada vez mais são alvos de ataques mal-intencionados que exploram vulnerabilidades conhecidas comuns. São comuns entre essas explorações ataques de injeção SQL, script entre sites ataques tooname alguns. Evitar tais ataques no código do aplicativo pode ser desafiadora e pode exigir a manutenção rigorosa, aplicação de patch e monitoramento em vários níveis de topologia de aplicativo hello. Um firewall do aplicativo web centralizado ajuda a simplificar o gerenciamento de segurança muito mais simples e oferece aos administradores de tooapplication contra ameaças ou invasões de garantia melhor. Uma solução WAF também possa reagir de ameaça à segurança tooa mais rápida por uma vulnerabilidade conhecida em um local central em vez de proteção de cada um dos aplicativos web individuais de aplicação de patch. Os gateways de aplicativos existentes podem ser facilmente convertido tooa web aplicativo firewall habilitado application gateway.

![imageURLroute](./media/application-gateway-web-application-firewall-overview/WAF1.png)

Application Gateway funciona como uma terminação SSL do aplicativo entrega controlador e ofertas, afinidade de sessão baseada em cookie, distribuição de carga de round robin, roteamento baseado em conteúdo, capacidade toohost vários aprimoramentos de segurança e sites. Aprimoramentos de segurança oferecidos pelo Gateway de aplicativo incluem gerenciamento de política SSL, tooend final suporte para SSL. Segurança do aplicativo agora é reforçada pelo WAF (firewall do aplicativo web) está sendo integrado diretamente ao oferta Olá ADC. Isso fornece um toomanage de local central tooconfigure fácil e proteger seus aplicativos web contra vulnerabilidades de web comuns.

## <a name="benefits"></a>Benefícios

Olá seguem principais benefícios Olá fornecidas pelo firewall do aplicativo web e o Application Gateway:

### <a name="protection"></a>Proteção

* Proteger seu aplicativo da web contra ataques sem código de toobackend de modificação e vulnerabilidades de web.

* Proteger web vários aplicativos em Olá a mesma hora atrás de um application gateway. Gateway de aplicativo oferece suporte à hospedagem de sites too20 atrás de um único gateway que pode ser protegido contra ataques de web WAF.

### <a name="monitoring"></a>Monitoramento

* Monitore seu aplicativo Web contra ataques usando um log de WAF em tempo real. Esse log é integrado com [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md) tootrack WAF alertas e os logs e monitorar facilmente as tendências.

* O WAF será integrado com a Central de Segurança do Azure em breve. Central de segurança do Azure permite que uma exibição central do estado de segurança de saudação de todos os recursos do Azure.

### <a name="customization"></a>Personalização

* regras de WAF Olá capacidade toocustomize e regra agrupa toosuit seus requisitos de aplicativo e eliminar falsos positivos.

## <a name="features"></a>Recursos

Firewall do aplicativo Web vem pré-configurada com CRS 3.0 por padrão, ou você pode escolher toouse 2.2.9. O CRS 3.0 oferece menos falsos positivos do que o 2.2.9. Olá capacidade muito[personalizar regras toosuit suas necessidades](application-gateway-customize-waf-rules-portal.md) é fornecido. Algumas das vulnerabilidades web comuns Olá quais firewall do aplicativo web protege contra inclui:

* Proteção contra injeção de SQL
* Proteção contra scripts entre sites
* Proteção Contra Ataques Comuns da Web, como a injeção de comandos, as solicitações HTTP indesejadas, a divisão de resposta HTTP e o ataque de inclusão de arquivo remoto
* Proteção contra violações de protocolo HTTP
* Proteção contra anomalias de protocolo HTTP, como ausência de host de agente do usuário e de cabeçalhos de aceitação
* Prevenção contra bots, rastreadores e scanners
* Detecção de problemas de configuração de aplicativo comuns (por exemplo, Apache, IIS etc.)

Para uma lista mais detalhada das regras e suas proteções consulte seguinte Olá [principais conjuntos de regras](#core-rule-sets).

### <a name="core-rule-sets"></a>Conjuntos de regras principais

O Gateway de Aplicativo dá suporte a dois conjuntos de regras, CRS 3.0 e CRS 2.2.9. Esses conjuntos de regras principais são coleções de regras que protegem seus aplicativos Web contra atividades mal-intencionadas.

#### <a name="owasp30"></a>OWASP_3.0

conjunto de regras de núcleo Olá 3.0 fornecido tem 13 grupos de regras, conforme mostrado na Olá a tabela a seguir. Cada um desses grupos de regra contém várias regras, que podem ser desabilitadas.

|RuleGroup|Descrição|
|---|---|
|**[REQUEST-910-IP-REPUTATION](application-gateway-crs-rulegroups-rules.md#crs910)**|Contém regras tooprotect contra spam conhecidos ou atividades mal-intencionadas.|
|**[REQUEST-911-METHOD-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs911)**|Contém regras toolock para baixo métodos (PUT, PATCH <...)|
|**[REQUEST-912-DOS-PROTECTION](application-gateway-crs-rulegroups-rules.md#crs912)**| Contém regras tooprotect contra ataques dos (negação de serviço).|
|**[REQUEST-913-SCANNER-DETECTION](application-gateway-crs-rulegroups-rules.md#crs913)**| Contém regras tooprotect contra scanners de porta e o ambiente.|
|**[REQUEST-920-PROTOCOL-ENFORCEMENT](application-gateway-crs-rulegroups-rules.md#crs920)**|Contém tooprotect de regras em relação a problemas de codificação e protocolo.|
|**[REQUEST-921-PROTOCOL-ATTACK](application-gateway-crs-rulegroups-rules.md#crs921)**|Contém regras tooprotect contra injeção de cabeçalho, solicitações indesejadas e de divisão de resposta|
|**[REQUEST-930-APPLICATION-ATTACK-LFI](application-gateway-crs-rulegroups-rules.md#crs930)**|Contém regras tooprotect contra ataques de arquivo e caminho.|
|**[REQUEST-931-APPLICATION-ATTACK-RFI](application-gateway-crs-rulegroups-rules.md#crs931)**|Contém regras tooprotect em relação a inclusão de arquivos remotos (RFI)|
|**[REQUEST-932-APPLICATION-ATTACK-RCE](application-gateway-crs-rulegroups-rules.md#crs932)**|Contém regras tooprotect novamente a execução remota de código.|
|**[REQUEST-933-APPLICATION-ATTACK-PHP](application-gateway-crs-rulegroups-rules.md#crs933)**|Contém regras tooprotect contra ataques de injeção de PHP.|
|**[REQUEST-941-APPLICATION-ATTACK-XSS](application-gateway-crs-rulegroups-rules.md#crs941)**|Contém regras para proteção contra scripts entre site.|
|**[REQUEST-942-APPLICATION-ATTACK-SQLI](application-gateway-crs-rulegroups-rules.md#crs942)**|Contém as regras para proteção contra ataques de injeção de SQL.|
|**[REQUEST-943-APPLICATION-ATTACK-SESSION-FIXATION](application-gateway-crs-rulegroups-rules.md#crs943)**|Contém regras tooprotect contra ataques de Fixation de sessão.|

#### <a name="owasp229"></a>OWASP_2.2.9

conjunto de regras de núcleo Olá 2.2.9 fornecido tem 10 grupos de regras, conforme mostrado na Olá a tabela a seguir. Cada um desses grupos de regra contém várias regras, que podem ser desabilitadas.

|RuleGroup|Descrição|
|---|---|
|**[crs_20_protocol_violations](application-gateway-crs-rulegroups-rules.md#crs20)**|Contém regras tooprotect contra violações de protocolo (caracteres inválidos, GET com um corpo de solicitação, etc.)|
|**[crs_21_protocol_anomalies](application-gateway-crs-rulegroups-rules.md#crs21)**|Contém regras tooprotect com informações de cabeçalho incorreto.|
|**[crs_23_request_limits](application-gateway-crs-rulegroups-rules.md#crs23)**|Contém regras tooprotect contra argumentos ou arquivos que excedem limitações.|
|**[crs_30_http_policy](application-gateway-crs-rulegroups-rules.md#crs30)**|Contém regras tooprotect em métodos restritos, cabeçalhos e tipos de arquivo. |
|**[crs_35_bad_robots](application-gateway-crs-rulegroups-rules.md#crs35)**|Contém regras tooprotect contra rastreadores da web e scanners.|
|**[crs_40_generic_attacks](application-gateway-crs-rulegroups-rules.md#crs40)**|Contém regras tooprotect contra ataques genéricos (fixation de sessão, inclusão de arquivos remoto, injeção de PHP, etc.)|
|**[crs_41_sql_injection_attacks](application-gateway-crs-rulegroups-rules.md#crs41sql)**|Contém regras tooprotect contra ataques de injeção de SQL|
|**[crs_41_xss_attacks](application-gateway-crs-rulegroups-rules.md#crs41xss)**|Contém tooprotect regras contra entre scripts do site.|
|**[crs_42_tight_security](application-gateway-crs-rulegroups-rules.md#crs42)**|Contém um tooprotect regra contra ataques de passagem de caminho|
|**[crs_45_trojans](application-gateway-crs-rulegroups-rules.md#crs45)**|Contém regras tooprotect contra cavalos de Troia backdoor.|

### <a name="waf-modes"></a>Modos de WAF

Application Gateway WAF pode ser configurado toorun em Olá dois modos a seguir:

* **Modo de detecção** – quando toorun configurado no modo de detecção do aplicativo Gateway WAF monitora e registra todos os alertas de ameaças no arquivo de log tooa. Log de diagnóstico para o Application Gateway deve ser ativado usando Olá **diagnóstico** seção. Você também precisa tooensure que Olá WAF log está selecionado e ativado. Ao ser executado no firewall do aplicativo Web no modo de detecção não bloqueia solicitações de entrada.
* **Modo de prevenção** – quando toorun configurado no modo de prevenção, Application Gateway ativamente bloqueia invasões e ataques detectados por suas regras. invasor Olá recebe uma exceção de acesso não autorizado 403 e conexão Olá é encerrada. Modo de prevenção continua toolog tais ataques Olá WAF logs.

### <a name="application-gateway-waf-reports"></a>Monitoramento de WAF

É importante monitorar a integridade de saudação do seu gateway de aplicativo. Monitorando a integridade de saudação do seu aplicativo firewall e hello aplicativos web que ele protege são fornecidos por meio de registro em log e integração com o Monitor do Azure, Central de segurança do Azure (em breve) e a análise de Log.

![diagnóstico](./media/application-gateway-web-application-firewall-overview/diagnostics.png)

#### <a name="azure-monitor"></a>Azure Monitor

Cada log de gateway de aplicativo é integrado ao [Azure Monitor](../monitoring-and-diagnostics/monitoring-overview.md).  Isso permite que informações de diagnóstico tootrack, incluindo logs e alertas de WAF.  Essa funcionalidade é fornecida em Olá recurso do Application Gateway no portal de saudação em Olá **diagnóstico** guia ou por meio de hello Azure Monitor de serviço diretamente. toolearn mais sobre como habilitar os logs de diagnóstico para o application gateway visite [diagnóstico Application Gateway](application-gateway-diagnostics.md)

#### <a name="azure-security-center"></a>Central de Segurança do Azure

[Central de segurança do Azure](../security-center/security-center-intro.md) Olá de ajuda a evitar, detectar e responder toothreats maior visibilidade e controle sobre a segurança de seus recursos do Azure. Agora, o gateway de aplicativo [integra a Central de Segurança do Azure](application-gateway-integration-security-center.md). Central de segurança do Azure verifica seus aplicativos de web do ambiente toodetect desprotegido. Agora ele pode recomendar application gateway WAF tooprotect esses recursos vulneráveis. Você pode criar WAF de gateway do aplicativo diretamente da saudação Central de segurança do Azure.  Essas instâncias WAF são integradas ao centro de segurança do Azure e envia alertas e informações de integridade volta tooAzure Central de segurança para relatórios.

![figura 1](./media/application-gateway-web-application-firewall-overview/figure1.png)

#### <a name="logging"></a>Registro em log

O WAF do Gateway de Aplicativo fornece relatórios detalhados sobre cada ameaça detectada. O registro em log é integrado aos Logs de diagnóstico do Azure e os alertas são registrados em um formato json. Esses logs podem ser integrados ao [Log Analytics](../log-analytics/log-analytics-azure-networking-analytics.md).

![imageURLroute](./media/application-gateway-web-application-firewall-overview/waf2.png)

```json
{
  "resourceId": "/SUBSCRIPTIONS/{subscriptionId}/RESOURCEGROUPS/{resourceGroupId}/PROVIDERS/MICROSOFT.NETWORK/APPLICATIONGATEWAYS/{appGatewayName}",
  "operationName": "ApplicationGatewayFirewall",
  "time": "2017-03-20T15:52:09.1494499Z",
  "category": "ApplicationGatewayFirewallLog",
  "properties": {
    "instanceId": "ApplicationGatewayRole_IN_0",
    "clientIp": "104.210.252.3",
    "clientPort": "4835",
    "requestUri": "/?a=%3Cscript%3Ealert(%22Hello%22);%3C/script%3E",
    "ruleSetType": "OWASP",
    "ruleSetVersion": "3.0",
    "ruleId": "941320",
    "message": "Possible XSS Attack Detected - HTML Tag Handler",
    "action": "Blocked",
    "site": "Global",
    "details": {
      "message": "Warning. Pattern match \"<(a|abbr|acronym|address|applet|area|audioscope|b|base|basefront|bdo|bgsound|big|blackface|blink|blockquote|body|bq|br|button|caption|center|cite|code|col|colgroup|comment|dd|del|dfn|dir|div|dl|dt|em|embed|fieldset|fn|font|form|frame|frameset|h1|head|h ...\" at ARGS:a.",
      "data": "Matched Data: <script> found within ARGS:a: <script>alert(\\x22hello\\x22);</script>",
      "file": "rules/REQUEST-941-APPLICATION-ATTACK-XSS.conf",
      "line": "865"
    }
  }
} 

```

## <a name="application-gateway-waf-sku-pricing"></a>Preços da SKU do WAF do Gateway de Aplicativo

O firewall de aplicativo Web está disponível em um novo um SKU do WAF. Este SKU está disponível apenas no modelo de provisionamento do Azure Resource Manager e não no modelo de implantação clássico de saudação. Além disso, o SKU do WAF vem apenas em instâncias de gateway de aplicativo médias e grandes. Todos os limites de saudação para o application gateway também se aplicam a toohello WAF SKU. Preço tem base nos encargos por hora da instância do gateway e nos encargos de processamento de dados. O preços do gateway por hora para o SKU do WAF é diferente dos encargos pelo SKU Standard e podem ser encontrados em [Detalhes de preços do Gateway de Aplicativo](https://azure.microsoft.com/pricing/details/application-gateway/). Processamento de dados permaneçam encargos Olá mesmo. Não há cobrança por regra ou grupo de regras. Você pode proteger vários aplicativos web por trás Olá mesmo web firewall do aplicativo e não há nenhuma cobrança adicional para dar suporte a vários aplicativos. 

A cobrança para WAF começa efetivamente 5/5/2017, até que, em seguida, Olá gateways SKU WAF continua toobe cobrado em taxas padrão.

## <a name="next-steps"></a>Próximas etapas

Depois de aprender mais sobre os recursos de saudação do WAF, visite [como tooconfigure web firewall do aplicativo no Application Gateway](application-gateway-web-application-firewall-portal.md).

