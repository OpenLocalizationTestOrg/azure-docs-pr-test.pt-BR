---
title: aaaIntegrate registros de recursos do Azure nos seus sistemas SIEM | Microsoft Docs
description: "Saiba mais sobre a integração de log do Azure, seus principais recursos e como ela funciona."
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TerryLanfear
ms.assetid: 9c1346e1-baf8-4975-b2f2-42ae05b2dc0a
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/10/2017
ms.author: TomSh
ms.custom: azlog
ms.openlocfilehash: 4a59ce625702e5266a7c8eb020473cfeaf6b1964
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toomicrosoft-azure-log-integration"></a>Introdução tooMicrosoft integração de log do Azure
Saiba mais sobre a integração de log do Azure, seus principais recursos e como ela funciona.

## <a name="overview"></a>Visão geral

Integração do log do Azure é uma solução gratuita que permite que você toointegrate de logs bruto de recursos do Azure em sistemas de gerenciamento de eventos (SIEM) e informações de segurança local tooyour.

A Integração do Log do Azure coleta eventos do Windows de logs do Visualizador de Eventos do Windows, [Logs de Atividades do Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md), [Alertas da Central de Segurança do Azure](../security-center/security-center-intro.md) e [Logs de Diagnóstico do Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) de recursos do Azure. Essa integração ajuda a sua solução SIEM fornecem um painel unificado para todos os seus ativos, local ou na nuvem hello, para que você pode agregar, correlacionar, analisar e alertas para eventos de segurança.

>[!NOTE]
Neste momento, nuvens Olá só tem suportada são comercial do Azure e do Azure governamental. Não há suporte para outras nuvens.

![Integração de log do Azure][1]

## <a name="what-logs-can-i-integrate"></a>Quais logs posso integrar?
O Azure produz um log abrangente para cada um de seus serviço. Esses logs representam três tipos de logs:

* **Logs de gerenciamento do controle** dar visibilidade a saudação [do Azure Resource Manager](../azure-resource-manager/resource-group-overview.md) operações CREATE, UPDATE e DELETE. Os Logs de Atividades do Azure são um exemplo desse tipo de log.
* **Logs de plano de dados** dar visibilidade a eventos de saudação gerados como parte do uso de saudação de um recurso do Azure. Um exemplo desse tipo de log é do Visualizador de eventos do Windows hello **sistema**, **segurança**, e **aplicativo** canais em uma máquina virtual do Windows. Outro exemplo é o Log de Diagnóstico configurado por meio do Azure Monitor
* **Eventos processados** fornecem informações de eventos e alertas processados em seu nome. Um exemplo desse tipo de evento é Azure Center alertas de segurança, em que a Central de segurança do Azure tem processados e analisados sua postura de segurança atual de tooyour relevantes do assinatura tooprovide alertas.

A integração de Log do Azure dá suporte a ArcSight, QRadar e Splunk. Em todas as circunstâncias, entre em contato com seu tooassess de fornecedores SIEM se eles têm um conector nativo. Em alguns casos, você não precisará toouse integração do Azure Log quando nativo conectores estão disponíveis. Para obter informações adicionais no log com suporte, visite tipos Olá perguntas Frequentes.

>[!NOTE]
Enquanto a integração de Log do Azure é uma solução gratuita, há custos de armazenamento do Azure resultantes do armazenamento de informações do arquivo de log de saudação.

Ajuda da comunidade está disponível por meio de saudação [Fórum do MSDN de integração do Azure Log](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration). Fórum de saudação fornece Olá AzLog comunidade Olá capacidade toosupport uns aos outros com perguntas, respostas, dicas e truques sobre como tooget hello mais fora da integração de Log do Azure. Além disso, a equipe de integração do Azure Log Olá monitora este fórum e ajudará sempre que possível.

Você também pode abrir uma [solicitação de suporte](../azure-supportability/how-to-create-azure-support-request.md). toodo, selecione **Log integração** como serviço Olá para o qual você está solicitando suporte.

## <a name="next-steps"></a>Próximas etapas
Neste documento, você foram introduzidas tooAzure integração de log. toolearn mais sobre o Azure log integração e tipos de saudação de logs com suporte, consulte o seguinte hello:

* [Integração do Log do Microsoft Azure](https://www.microsoft.com/download/details.aspx?id=53324) – Visite o Centro de Download para obter os detalhes, os requisitos de sistema e as instruções de instalação da integração do Log do Azure.
* [Introdução à integração do log do Azure](security-azure-log-integration-get-started.md) — este tutorial explica as etapas de instalação da integração do log do Azure, bem como a integração de logs do armazenamento WAD do Azure, Logs de Atividades do Azure, alertas da Central de Segurança do Azure e logs de auditoria do Azure Active Directory.
* [Etapas de configuração de parceiro](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – esta postagem de blog mostra como tooconfigure Azure log toowork integração com soluções de parceiros Splunk, HP ArcSight e IBM QRadar. Este blog representa a atual posição sobre como configurar soluções de parceiros de saudação. Em todos os casos, consulte a documentação de solução de toopartner primeiro.
* [Alertas de atividade e ASC acima syslog tooQRadar](https://blogs.msdn.microsoft.com/azuresecurity/2016/09/24/integrate-azure-logs-to-qradar/) – esta postagem de blog fornece as etapas de saudação toosend alertas de atividade e o Centro de segurança do Azure sobre tooQRadar de syslog
* [Perguntas frequentes sobre o log de integração do Azure](security-azure-log-integration-faq.md) – encontre as respostas para as perguntas frequentes sobre a integração de log do Azure.
* [Integração Central de segurança do log de alertas com o Azure Integration](../security-center/security-center-integrating-alerts-with-log-integration.md) – este documento mostra como a Central de segurança do Azure toosync alertas com integração de Log do Azure.

<!--Image references-->
[1]: ./media/security-azure-log-integration-overview/azure-log-integration.png
