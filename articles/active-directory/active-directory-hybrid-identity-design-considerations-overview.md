---
title: "aaaAzure considerações de design do Active Directory híbrida identidade - visão geral | Microsoft Docs"
description: "Visão geral e mapa de conteúdo do guia de considerações de design de identidade híbrida"
documentationcenter: 
services: active-directory
author: billmath
manager: femila
editor: 
ms.assetid: 100509c4-0b83-4207-90c8-549ba8372cf7
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 10aacb04c90abd100eb56d7c44d590946b052f18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-hybrid-identity-design-considerations"></a>Considerações do design de identidade híbrida do Active Directory do Azure
Dispositivos com base no consumidor são proliferação Olá, mundo corporativo e baseado em nuvem aplicativos do software como serviço (SaaS) são tooadopt fácil. Assim, a manutenção do controle de acesso de aplicativo dos usuários em plataformas de data centers e nuvem internas é um desafio.  

Soluções de identidade da Microsoft abrangem locais e recursos baseados em nuvem, criando uma identidade de usuário único para autenticação e autorização tooall recursos, independentemente do local. Chamamos isso de Identidade Híbrida. Há diferente opções de design e configuração de identidade híbrida usando soluções da Microsoft e, em alguns casos, talvez seja difícil toodetermine qual combinação melhor atende as necessidades de saudação da sua organização. 

Este guia de considerações de Design de identidade híbrida ajuda toounderstand como toodesign uma solução de identidade híbrida que melhor se adapta a tecnologia e negócios Olá necessidades de sua organização.  Este guia detalha uma série de etapas e tarefas que você pode seguir toohelp projetar uma solução de identidade híbrida que atende às necessidades exclusivas de sua organização. Durante saudação etapas e tarefas, guia Olá apresentará tecnologias relevantes hello e recurso opções disponíveis tooorganizations toomeet funciona e qualidade de serviço (como disponibilidade, escalabilidade, desempenho, capacidade de gerenciamento e segurança) requisitos de nível. 

Especificamente, metas guia considerações de design do hello híbrida identidade são Olá tooanswer perguntas a seguir: 

* O que fazem perguntas necessárias tooask e responder toodrive um design híbrido específicas da identidade para um domínio de tecnologia ou problema que melhor atende aos meus requisitos?
* Quais sequência de atividades deve concl toodesign uma solução de identidade para o domínio de tecnologia ou problema Olá? 
* Quais opções de tecnologia e configuração de identidade híbrida são disponível toohelp me atender aos meus requisitos? Quais são as compensações Olá entre essas opções para que eu possa escolher a melhor opção de saudação para minha empresa?

## <a name="who-is-this-guide-intended-for"></a>A quem este guia se destina?
 CIO, CITO, arquitetos de identidade principais, arquitetos corporativos e arquitetos de TI responsáveis pela criação de uma solução de identidade híbrida para organizações de médio ou grande porte.

## <a name="how-can-this-guide-help-you"></a>Como este guia pode ajudá-lo?
Você pode usar este guia toounderstand como toodesign uma solução de identidade híbrida que é capaz de toointegrate uma nuvem com base em sistema de gerenciamento de identidade com a atual identidade solução local. 

Olá gráfico a seguir mostra um exemplo de uma solução de identidade híbrida que permite que os administradores de TI toomanage toointegrate seus atual do Active Directory do Windows Server solução localizada local com o Microsoft Azure Active Directory tooenable usuários toouse único Sign-On (SSO) em aplicativos localizados na nuvem hello e local.

![](./media/hybrid-id-design-considerations/hybridID-example.png)

Olá acima ilustração é um exemplo de uma solução de identidade híbrida que usa a nuvem e serviços de toointegrate com recursos locais na ordem tooprovide uma experiência de único processo de autenticação de usuário final de toohello toofacilitate IT Gerenciando Esses recursos. Embora isso possa ser um cenário bastante comum, o design de identidade híbrida cada organização é provavelmente toobe diferente do exemplo hello ilustrado na Figura 1 devido a requisitos de toodifferent. 

Este guia fornece uma série de etapas e tarefas que você pode seguir toodesign uma solução de identidade híbrida que atende às necessidades exclusivas de sua organização. Durante a saudação seguintes etapas e tarefas, tecnologias relevantes do Olá Olá guia apresenta e recurso opções disponíveis tooyou toomeet funcionais e qualidade de serviço requisitos de nível para sua organização.

**Suposições**: você tem alguma experiência com o Windows Server, com os Serviços de Domínio do Active Directory e com o Active Directory do Azure. Neste documento, presumimos que você quer saber como essas soluções podem atender às suas necessidades comerciais por conta própria ou em uma solução integrada.

## <a name="design-considerations-overview"></a>Visão geral sobre as considerações de design
Este documento fornece um conjunto de etapas e tarefas que você pode seguir toodesign uma solução de identidade híbrida que melhor atenda às suas necessidades. Olá etapas são apresentadas em uma sequência ordenada. Considerações de design, que você aprenderá nas próximas etapas podem exigir toochange decisões feitas nas etapas anteriores, no entanto, devido a escolhas de design tooconflicting. Cada tentativa tooalert você toopotential conflitos de design em todo o documento de saudação. 

Você chegará no design de saudação que melhor atenda às suas necessidades somente após percorrer as etapas de saudação quantas vezes forem necessária tooincorporate todas as considerações de saudação no documento de saudação. 

| Fase de identidade híbrida | Lista de tópicos |
| --- | --- |
| Determinar requisitos de identidade |[Determinar as necessidades de negócios](active-directory-hybrid-identity-design-considerations-business-needs.md)<br> [Determinar os requisitos de sincronização de diretório](active-directory-hybrid-identity-design-considerations-directory-sync-requirements.md)<br> [Determinar os requisitos de autenticação multifator](active-directory-hybrid-identity-design-considerations-multifactor-auth-requirements.md)<br> [Definir uma estratégia de adoção de identidade híbrida](active-directory-hybrid-identity-design-considerations-identity-adoption-strategy.md) |
| Planejar para aumentar a segurança de dados usando solução de identidade forte |[Determinar os requisitos para proteção de dados](active-directory-hybrid-identity-design-considerations-dataprotection-requirements.md) <br> [Determinar requisitos de gerenciamento de conteúdo](active-directory-hybrid-identity-design-considerations-contentmgt-requirements.md)<br> [Determinar requisitos de controle de acesso](active-directory-hybrid-identity-design-considerations-accesscontrol-requirements.md)<br> [Determinar requisitos de resposta a incidentes](active-directory-hybrid-identity-design-considerations-incident-response-requirements.md) <br> [Definir a estratégia de proteção de dados](active-directory-hybrid-identity-design-considerations-data-protection-strategy.md) |
| Plano para o ciclo de vida de identidade híbrida |[Determinar tarefas de gerenciamento de identidade híbrida](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md) <br> [Gerenciamento da Sincronização](active-directory-hybrid-identity-design-considerations-hybrid-id-management-tasks.md)<br> [Determinar a estratégia de adoção do gerenciamento de identidade híbrida](active-directory-hybrid-identity-design-considerations-lifecycle-adoption-strategy.md) |

## <a name="download-this-guide"></a>Baixar este guia
Você pode baixar uma versão em pdf do guia de considerações de Design de identidade híbrida de saudação do hello [Galeria do Technet](https://gallery.technet.microsoft.com/Azure-Hybrid-Identity-b06c8288). 

