---
title: "aaaIntroduction tooAzure Central de segurança | Microsoft Docs"
description: "Saiba mais sobre a Central de Segurança do Azure, seus principais recursos e como ela funciona."
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 45b9756b-6449-49ec-950b-5ed1e7c56daa
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 287dbaaa7e2004c522f103595bc316261daf05b4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-security-center"></a>Introdução tooAzure Central de segurança
Saiba mais sobre a Central de Segurança do Azure, seus principais recursos e como ela funciona.

> [!NOTE]
> A partir do início de junho de 2017, Central de segurança usará Olá Microsoft Monitoring Agent toocollect e armazenar dados. Consulte [migração da plataforma Azure Security Center](security-center-platform-migration.md) toolearn mais. informações Olá neste artigo representam a funcionalidade da Central de segurança após a transição toohello Microsoft Monitoring Agent.
>
>

## <a name="what-is-azure-security-center"></a>O que é a Central de Segurança do Azure?
 Central de segurança ajuda a evitar, detectar e reagir toothreats com maior visibilidade e controle sobre a segurança de saudação de seus recursos do Azure. Ela permite o gerenciamento de políticas e o monitoramento da segurança integrada entre suas assinaturas do Azure, ajuda a detectar ameaças que poderiam passar despercebidas e funciona com uma enorme variedade de soluções de segurança.

## <a name="key-capabilities"></a>Principais recursos
 Central de segurança oferece recursos de prevenção, detecção e resposta que são criados no tooAzure de ameaça eficiente e fácil de usar. Os principais recursos são:

| Estágio | Recurso |
| --- | --- |
| Evitar |Monitores Olá estado de segurança de seus recursos do Azure |
| Evitar | Define políticas para suas assinaturas do Azure com base nos requisitos de segurança da sua empresa, tipos de saudação de aplicativos que você use e Olá confidencialidade dos seus dados |
| Evitar | Proprietários de serviços usa orientado por política segurança recomendações tooguide pelo processo de saudação da implementação necessário controles |
| Evitar | Implanta rapidamente aplicativos da Microsoft e de parceiros e serviços de segurança |
| Detectar |Coleta e analisa dados de segurança de seus recursos do Azure, rede hello e soluções de parceiros, como firewalls e programas antimalware automaticamente |
| Detectar | Usa global de ameaças intelligence da Microsoft hello produtos e serviços, Olá Microsoft Digital Crimes unidade (DCU), Microsoft Security Response Center (MSRC) e feeds externos |
| Detectar | Aplica a análise avançada, incluindo aprendizado de máquina e análise comportamental |
| Responder |Fornece alertas/incidentes de segurança priorizados |
| Responder | Oferece ideias sobre a origem de saudação do ataque hello e recursos afetados |
| Responder | Sugere maneiras toostop Olá ataque atual e ajudar a evitar ataques futuros |

## <a name="introductory-walkthrough"></a>Passo a passo introdutório

> [!NOTE]
> Este documento apresenta serviço hello usando um exemplo de implantação. Este documento não é um guia passo a passo.
>
>

 Acessar a Central de segurança do hello [portal do Azure](https://azure.microsoft.com/features/azure-portal/). [Entrar no portal de toohello](https://portal.azure.com). No menu do portal principal hello, role toohello **Central de segurança** opção ou selecione Olá **Central de segurança** bloco que você fixou anteriormente toohello painel do portal.

![Bloco de segurança no portal do Azure][1]

Na Central de Segurança, defina as políticas de segurança, monitore as configurações de segurança e exiba alertas de segurança.

### <a name="security-policies"></a>Diretivas de segurança
Você pode definir políticas para seus requisitos de segurança da empresa tooyour de acordo com as assinaturas do Azure. Você também pode adaptá-los toohello tipos de aplicativos que você está usando ou toohello confidencialidade de dados de saudação em cada assinatura. Por exemplo, os recursos usados para desenvolvimento ou teste podem ter requisitos de segurança diferentes daqueles usados para aplicativos de produção. Da mesma forma, os aplicativos com dados regulamentados, como PII, podem exigir um nível mais alto de segurança.

> [!NOTE]
> toomodify uma política de segurança, você deve ser de um administrador de segurança ou Olá uma assinatura proprietário ou colaborador. toolearn mais informações sobre funções e ações permitidas na Central de segurança, consulte [permissões na Central de segurança do Azure](security-center-permissions.md).
>
>

Em Olá **Central de segurança** folha, selecione Olá **política** lado a lado para obter uma lista de suas assinaturas e os grupos de recursos.   

![Folha da Central de segurança][2]

Em Olá **política de segurança** folha, selecione os detalhes da política de uma assinatura tooview hello.

**Coleta de dados** habilita a coleta de dados para uma política de segurança. A habilitação fornece:

* Verificação diária de todas as máquinas virtuais com suporte para monitoramento de segurança e recomendações.
* Coleção de eventos de segurança para a análise e detecção de ameaças.

> [!NOTE]
> Coleta de dados é configurada no nível de assinatura de saudação.
>
>

Selecione **política de prevenção de** tooopen Olá **política de prevenção de** folha. **Mostrar as recomendações para** permite que você escolher Olá os controles de segurança que você deseja toomonitor e hello recomendações que você deseja toosee com base nas necessidades de segurança de saudação de recursos de saudação na assinatura hello.

### <a name="security-recommendations"></a>Recomendações de segurança
 Central de segurança analisa o estado de segurança Olá seus recursos do Azure tooidentify possíveis vulnerabilidades de segurança. Uma lista de recomendações orienta você pelo processo de saudação de configuração de controles necessários. Os exemplos incluem:

* Provisionamento antimalware toohelp identificar e remover softwares mal-intencionados
* Configurando a rede segurança e grupos de regras toocontrol tráfego tooVMs
* Provisionamento de firewalls de aplicativo web toohelp se proteger contra ataques que seus aplicativos web de destino
* Como implantar atualizações de sistema ausentes
* Configurações de sistema operacional que não correspondem a saudação de endereçamento recomendado linhas de base

Clique em Olá **recomendações** lado a lado para obter uma lista de recomendações. Clique em cada recomendação tooview obter informações adicionais ou problema de saudação do tootake ação tooresolve.

![Recomendações de segurança na Central de Segurança do Azure][5]

### <a name="security-state-of-azure-resources"></a>Estado da segurança dos recursos do Azure
Olá **prevenção** seção de saudação painel mostra Olá postura de segurança geral do ambiente de saudação por tipo de recurso, incluindo as VMs, aplicativos web e outros recursos.   

Selecione um tipo de recurso em **prevenção** tooview obter mais informações, incluindo uma lista de qualquer possíveis vulnerabilidades de segurança que foram identificados. (**De computação** está selecionado no exemplo hello abaixo.)

![Bloco de integridade de recursos][6]

### <a name="security-alerts"></a>Alertas de segurança
 Central de segurança automaticamente coleta, analisa e integra dados de log de seus recursos do Azure, rede hello e soluções de parceiros, como programas de antimalware e firewalls. Quando forem detectadas ameaças, é criado um alerta de segurança. Os exemplos abrangem a detecção de:

* As máquinas virtuais comprometidas se comunicam com os endereços IP mal-intencionados conhecidos
* Malware avançado detectado usando o relatório de erros do Windows
* Ataques por força bruta contra máquinas virtuais
* Alertas de segurança dos firewalls e programas antimalware integrados

Olá clicando em **alertas de segurança** bloco exibe uma lista de alertas de prioridade.

![Alertas de segurança][7]

Selecionar um alerta mostra mais informações sobre ataques de saudação e sugestões sobre como tooremediate-lo.

![Detalhes do alerta de segurança][8]

### <a name="partner-solutions"></a>Soluções de parceiros
Olá **soluções de parceiros** lado a lado permite monitorar em um estado de segurança Olá rapidamente suas soluções de parceiros integrados com sua assinatura do Azure. Central de segurança exibe alertas de soluções de saudação.

Selecione Olá **soluções de parceiros** lado a lado. Uma folha será aberta exibindo uma lista de todas as soluções de parceiro conectadas.

![Soluções de parceiros][9]

## <a name="get-started"></a>Introdução
tooget iniciado com a Central de segurança, é necessário um tooMicrosoft de assinatura do Azure. A Central de segurança é habilitada com sua assinatura do Azure. Se você não tiver uma assinatura, você pode se inscrever em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).

 Acessar a Central de segurança do hello [portal do Azure](https://azure.microsoft.com/features/azure-portal/). Consulte Olá [portal documentação](https://azure.microsoft.com/documentation/services/azure-portal/) toolearn mais.

[Introdução ao centro de segurança do Azure](security-center-get-started.md) rapidamente orienta você através de componentes de monitoramento de segurança e gerenciamento de política de saudação da Central de segurança.

## <a name="next-steps"></a>Próximas etapas
Neste documento, você foram introduzidas Center de tooSecurity, seus principais recursos e como tooget iniciada. toolearn mais, consulte Olá recursos a seguir:

* [Definir políticas de segurança na Central de segurança do Azure](security-center-policies.md) — Saiba como tooconfigure as políticas de segurança para sua assinatura do Azure e grupos de recursos.
* [Gerenciando as recomendações de segurança na Central de Segurança do Azure](security-center-recommendations.md) : saiba como as recomendações ajudam a proteger os recursos do Azure.
* [Monitoramento de integridade de segurança na Central de segurança do Azure](security-center-monitoring.md) — Saiba como toomonitor Olá a integridade de seus recursos do Azure.
* [Gerenciando e respondendo toosecurity alertas na Central de segurança do Azure](security-center-managing-and-responding-alerts.md) — Saiba como alertas de toosecurity toomanage e responder.
* [Soluções de parceiro com a Central de segurança do Azure de monitoramento](security-center-partner-solutions.md) — Saiba como toomonitor Olá status de integridade de suas soluções de parceiro.
- [Segurança de dados da Central de Segurança do Azure](security-center-data-security.md) – saiba como os dados são gerenciados e protegidos na Central de Segurança do Azure.
* [Perguntas frequentes sobre o Centro de segurança do Azure](security-center-faq.md) — localizar perguntas frequentes sobre como usar o serviço de saudação.
* [Blog de segurança do Azure](http://blogs.msdn.com/b/azuresecurity/) — Obtenha notícias mais recentes de segurança do Azure hello e informações.

<!--Image references-->
[1]: ./media/security-center-intro/security-tile.png
[2]: ./media/security-center-intro/security-center.png
[3]: ./media/security-center-intro/security-policy.png
[4]: ./media/security-center-intro/security-policy-blade.png
[5]: ./media/security-center-intro/recommendations.png
[6]: ./media/security-center-intro/resources-health.png
[7]: ./media/security-center-intro/security-alert.png
[8]: ./media/security-center-intro/security-alert-detail.png
[9]: ./media/security-center-intro/partner-solutions.png
