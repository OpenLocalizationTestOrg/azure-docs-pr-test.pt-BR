---
title: "aaaOperations segurança do pacote de gerenciamento e segurança de dados de solução de auditoria | Microsoft Docs"
description: "Este documento explica como os dados são gerenciados e protegidos na Solução de Segurança e Auditoria do Operations Management Suite."
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: 9cdf7deb-2a30-4672-b89f-71179ee8326a
ms.service: operations-management-suite
ms.custom: oms-security
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 9c4181b3b491e4f7f0c57d7252eca78a819722d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="operations-management-suite-security-and-audit-solution-data-security"></a>Segurança de dados da solução de Segurança e Auditoria do Operations Management Suite
impedir que clientes toohelp, detectar e responder toothreats, [Operations Management Suite (OMS) solução de segurança e auditoria](operations-management-suite-overview.md) coleta e processa os dados sobre seus recursos, que inclui:

* Log de eventos de segurança
* Eventos de ETW (Rastreamento de Eventos para Windows)
* Eventos de auditoria do AppLocker
* Log do Firewall do Windows
* Eventos de Análise de Ameaças Avançadas
* Resultados da avaliação de linha de base
* Resultados da avaliação antimalware
* Resultados da avaliação de atualização/patch
* Fluxos de syslogs explicitamente habilitados no agente Olá

Oferecemos a privacidade de saudação do investimento forte tooprotect e a segurança dos dados. A Microsoft obedece toostrict diretrizes de conformidade e segurança — da codificação toooperating um serviço.
Este artigo explica como os dados são gerenciados e protegidos na Solução de Segurança e Auditoria do OMS.

## <a name="data-sources"></a>Fontes de dados
OMS solução de segurança e auditoria analisam dados de suas máquinas virtuais e computadores físicos onde Olá agente do OMS está instalado. A Solução de Segurança e Auditoria do OMS pode coletar informações de configuração sobre eventos de segurança, como eventos do Windows, logs de auditoria, logs do IIS e mensagens de syslog. Exemplos desses dados são: tipo e versão de sistema operacional, processos em execução, nome do computador, endereços IP, usuário conectado e ID de locatário.  

## <a name="data-protection"></a>Proteção de dados
**Diferenciação de dados**: dados são mantidos separados logicamente em cada componente serviço hello. Todos os dados são marcados por organização. Essa marcação persiste em todo o ciclo de vida de dados de saudação e é imposta em cada camada de serviço hello. 

**Acesso a dados**: tooprovide recomendações de segurança e investigar potenciais ameaças de segurança, os funcionários da Microsoft podem acessar informações coletadas ou analisados pelos serviços. Cumprimento toohello [termos do Microsoft Online Services](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) e [privacidade](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx), que de estado que o Microsoft não usam dados do cliente ou derivar informações dele para qualquer anúncio ou semelhante fins comerciais. recomendações de segurança tooprovide e investigar potenciais ameaças de segurança, os funcionários da Microsoft podem acessar informações coletadas ou analisados pelos serviços. Somente usamos os dados do cliente como necessário tooprovide você com o Azure de serviços, incluindo fins compatível com o fornecimento desses serviços. Você manter todos os direitos tooyour próprios dados.

**Use dados**: a Microsoft usa os padrões e inteligência de ameaça Vista em vários locatários tooenhance nossos recursos de detecção e prevenção; fazemos acordo com os compromissos de privacidade de saudação descritos em nosso [privacidade Instrução](https://www.microsoft.com/privacystatement/en-us/OnlineServices/Default.aspx).

> [!NOTE]
> Local de dados é configurado no nível de espaço de trabalho do OMS hello, durante a criação de espaço de trabalho hello, que faz parte da saudação inicial OMS segurança e auditoria processo de configuração.
> 
> 

## <a name="see-also"></a>Consulte também
Neste documento, você aprendeu como os dados são gerenciados e protegidos no OMS. toolearn mais sobre o OMS solução de segurança e auditoria, consulte:

* [Operations Management Suite (OMS) overview](operations-management-suite-overview.md)
* [Monitorando e respondendo tooSecurity alertas no Operations Management Suite solução de segurança e auditoria](oms-security-responding-alerts.md)
* [Monitorando recursos na solução de Segurança e Auditoria do Operations Management Suite](oms-security-monitoring-resources.md)

