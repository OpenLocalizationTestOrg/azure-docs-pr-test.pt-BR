---
title: "integração de aaaPartner na Central de segurança do Azure | Microsoft Docs"
description: "Saiba mais sobre como a Central de segurança do Azure se integra com parceiros tooenhance geral de segurança de seus recursos do Azure."
services: security-center
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 6af354da-f27a-467a-8b7e-6cbcf70fdbcb
ms.service: security-center
ms.topic: hero-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2017
ms.author: yurid
ms.openlocfilehash: 3621335730a076721cb3c23788a47be50aa8fc73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="partner-integration-in-azure-security-center"></a>Integração com Parceiros na Central de Segurança do Azure

Neste artigo, descreveremos como o Centro de segurança do Azure se integra ao parceiros toohelp é melhorar a segurança geral. Central de segurança oferece uma experiência integrada no Azure e aproveita hello Azure Marketplace para o parceiro de certificação e cobrança.

> [!NOTE] 
> A partir de junho de 2017, Central de segurança usa dados de toocollect e repositório de Microsoft Monitoring Agent de saudação. Para saber mais, veja [Migração de plataforma da Central de Segurança do Azure](security-center-platform-migration.md). informações Olá neste artigo representam a funcionalidade da Central de segurança após a transição toohello Microsoft Monitoring Agent.
>

## <a name="why-deploy-partner-solutions-from-security-center"></a>Por que implantar soluções de parceiro da Central de Segurança

Integração com quatro principais razões tooleverage parceiros na Central de segurança são:

- **Facilidade de implantação**. Implantando uma solução de parceiro pelo seguinte Olá recomendação da Central de segurança é muito mais fácil. o processo de implantação Olá pode ser completamente automatizado por meio de uma topologia de rede e de instalação padrão. Como alternativa, os clientes podem escolher uma opção semiautomatizada para obter mais flexibilidade e personalização.
- **Detecções integradas**. Os eventos de segurança das soluções de parceiro são automaticamente coletados, agregados e exibidos como parte dos incidentes e alertas da Central de Segurança. Esses eventos também são combinados com as detecções de outros tooprovide fontes avançado de recursos de detecção de ameaças.
- **Monitoramento e gerenciamento de integridade unificados**. Os clientes podem usar toomonitor de eventos de integridade integrado todas as soluções de parceiros em um relance. Gerenciamento básico está disponível, com a instalação usando a solução de parceiro Olá tooadvanced fácil acesso.
- **Exportar tooSIEM**. Os clientes podem exportar todos os Central de segurança e parceiro em comum alertas sistemas de gerenciamento de eventos (SIEM) e informações de segurança local tooon formato de evento (CEF) usando a integração de log do Azure (visualização).


## <a name="partners-that-integrate-with-security-center"></a>Parceiros que se integram à Central de Segurança

No momento, a Central de Segurança se integra a estas soluções:

- Proteção de ponto de extremidade ([Trend Micro](https://help.deepsecurity.trendmicro.com/azure-marketplace-getting-started-with-deep-security.html), Symantec e [Antimalware da Microsoft para Serviços de Nuvem e Máquinas Virtuais do Azure](https://docs.microsoft.com/azure/security/azure-security-antimalware)) 
- Firewall de aplicativo Web ([Barracuda](https://www.barracuda.com/products/webapplicationfirewall), [F5](https://support.f5.com/kb/en-us/products/big-ip_asm/manuals/product/bigip-ve-web-application-firewall-microsoft-azure-12-0-0.html), [Imperva](https://www.imperva.com/Products/WebApplicationFirewall-WAF), [Fortinet](https://www.fortinet.com/resources.html?limit=10&search=&document-type=data-sheets), [Gateway de Aplicativo do Azure](https://azure.microsoft.com/blog/azure-web-application-firewall-waf-generally-available/)) 
- Firewall de próxima geração ([Check Point](https://www.checkpoint.com/products/vsec-microsoft-azure/), [Barracuda](https://campus.barracuda.com/product/nextgenfirewallf/article/NGF/AzureDeployment/), [Fortinet](http://docs.fortinet.com/d/fortigate-fortios-handbook-the-complete-guide-to-fortios-5.2) e [Cisco](http://www.cisco.com/c/en/us/td/docs/security/firepower/quick_start/azure/ftdv-azure-qsg.html)) 
- Avaliação de vulnerabilidades ([Qualys](https://www.qualys.com/public-clouds/microsoft-azure/))  

Ao longo do tempo, a Central de segurança expandir Olá número de parceiros dentro dessas categorias e adicionar novas categorias. 

## <a name="deploy-a-partner-solution"></a>Implantar uma solução de parceiro

Com base na configuração de saudação do ambiente do Azure e política de segurança Olá definida, a Central de segurança poder recomendar que você implanta uma solução de parceiro. Olá recomendação da Central de segurança o guiará pelo processo de saudação de selecionar e instalar uma solução de parceiro. Olá experiência de implantação geral poderão variar, dependendo tipo hello da solução e o parceiro que você usa. Para obter mais informações, consulte Olá artigos a seguir:

- [Instalar o Endpoint Protection](security-center-install-endpoint-protection.md)
- [Adicione um firewall do aplicativo Web](security-center-add-web-application-firewall.md)
- [Adicionar um firewall de próxima geração](security-center-add-next-generation-firewall.md)
- [Avaliação de vulnerabilidade não instalada](security-center-vulnerability-assessment-recommendations.md)

## <a name="manage-partner-solutions"></a>Gerenciar soluções de parceiros

Após a implantação, tooview informações sobre Olá integridade da solução Olá os e executar tarefas de gerenciamento básico, Olá **Central de segurança** folha, selecione Olá **soluções de parceiros** opção. Para saber mais sobre o gerenciamento de soluções de parceiros na Central de Segurança, veja [Monitorar soluções de parceiro com a Central de Segurança do Azure](security-center-partner-solutions.md).

![Integração de parceiros](./media/security-center-partner-integration/security-center-partner-integration-fig1-new2.png)

> [!NOTE]
> Suporte à proteção de ponto de extremidade Symantec é toodiscovery limitado. Nenhum alerta de integridade disponível.
>

## <a name="see-also"></a>Consulte também

Neste artigo, você aprendeu como toointegrate parceiro soluções na Central de segurança do Azure. toolearn mais sobre o Centro de segurança, consulte Olá artigos a seguir:

* [Guia de planejamento e operações da Central de Segurança](security-center-planning-and-operations-guide.md)
* [Gerenciar e responder a alertas toosecurity na Central de segurança](security-center-managing-and-responding-alerts.md)
* [Alertas de segurança por tipo na Central de Segurança](security-center-alerts-type.md)
* [Monitoramento da integridade de segurança na Central de Segurança](security-center-monitoring.md). Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Monitoramento das soluções de parceiros na Central de Segurança](security-center-partner-solutions.md). Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
* [Perguntas frequentes sobre a Central de Segurança do Azure](security-center-faq.md). Obtenha respostas toofrequently perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de Segurança do Azure](http://blogs.msdn.com/b/azuresecurity/). Encontre postagens no blog sobre a conformidade e segurança do Azure.
