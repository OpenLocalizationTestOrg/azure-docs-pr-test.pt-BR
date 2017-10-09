---
title: "Visão geral de redefinição de senha de autoatendimento aaaAzure AD | Microsoft Docs"
description: "O que a redefinição de senha de autoatendimento no Azure AD faz para sua organização?"
services: active-directory
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.reviewer: gahug
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: joflore
ms.custom: it-pro
ms.openlocfilehash: 0efc291b1eeec0b7ae33ff5a7d9ed38e70c8be6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-self-service-password-reset-for-hello-it-professional"></a>Redefinição de senha de autoatendimento do Azure AD para Olá profissional de TI

"Autoatendimento" é uma palavra de efeito lançada em torno de dentro de vários departamentos de TI através de hello world com significados diferentes. mercado de saudação é inundado com produtos que permitem que você crie grupos de locais de toomanage, senhas ou perfis de usuário de nuvem hello ou local.

A SSPR (Redefinição de senha de autoatendimento) do Azure AD (Azure Active Directory) tem a vantagem da facilidade de uso e implantação. A redefinição de senha de autoatendimento do Azure AD combina um conjunto de recursos que:

* Permitir que seus usuários toomanage suas próprias senhas
  * De qualquer dispositivo
  * Em qualquer local
  * A qualquer momento
* Manter a conformidade com políticas definidas por você, como administrador

Se você estiver pronto, comece com o Azure AD SSPR usando nosso [guia de início rápido](active-directory-passwords-getting-started.md) e faça com que seus usuários redefinam rapidamente suas próprias senhas.

## <a name="what-is-possible"></a>O que é possível

* **Alteração de senha de autoatendimento** permite que os usuários finais ou administradores toochange suas senhas sem assistência do administrador
* **Desbloqueio de conta de autoatendimento** permite toounlock de usuários finais suas próprias contas sem assistência do administrador
* **Redefinição de senha de autoatendimento** permite que os usuários finais ou administradores tooreset suas senhas automaticamente sem a assistência do administrador. A redefinição de senha por autoatendimento exige o Azure AD Premium ou Básico - [Edições do Azure Active Directory](active-directory-editions.md).
* **Redefinição de senha iniciada pelo administrador** permite que um administrador tooreset senha do usuário final ou outro administrador de dentro do hello [portal do Azure](https://docs.microsoft.com/azure/azure-portal-overview)
* **Relatórios de atividade de gerenciamento de senha** fornecem aos administradores percepções sobre as atividades de registro e de redefinição de senha que ocorrem em suas organizações - [Relatórios de gerenciamento](active-directory-passwords-reporting.md)
* **Write-back de senha** permite o gerenciamento de senhas locais da nuvem Olá para todos os precedentes Olá cenários podem ser executados por, ou em nome de hello, federadas ou sincronizadas usuários. O Write-back de Senha exige o [Azure AD Premium](active-directory-get-started-premium.md).

## <a name="why-choose-azure-ad-self-service-password-reset"></a>Por que escolher a redefinição da senha por autoatendimento do Azure AD

* **Reduzir os custos**, pois a redefinição de senha com auxílio do suporte ou da assistência técnica representa normalmente 20% dos gastos da organização de TI
* **Aprimorar as experiências do usuário final** e **reduzir o volume de suporte técnico** fornecendo final usuários Olá power tooresolve seus próprios problemas de senha uma vez sem chamar um suporte técnico ou abrir uma solicitação de suporte.
* **Gerar mobilidade**, pois os usuários podem redefinir suas senhas onde quer que estejam.

## <a name="azure-ad-self-service-password-reset-availability"></a>Disponibilidade da redefinição da senha por autoatendimento do Azure AD

A redefinição de senha por autoatendimento do Azure AD está disponível em três camadas, dependendo de sua assinatura.

* **Azure AD Gratuito**: os administradores somente de nuvem podem redefinir suas próprias senhas
* **Azure AD Básico** ou qualquer **assinatura paga do O365**: usuários somente de nuvem e administradores somente de nuvem podem redefinir suas próprias senhas
* **Azure AD Premium**: qualquer usuário ou administrador, incluindo somente nuvem, federado ou usuários com sincronização de senha, pode redefinir sua própria senha. Senhas locais exigem toobe de write-back de senha habilitada.

## <a name="azure-ad-self-service-password-reset-a-sum-of-hello-parts"></a>Redefinição de senha de autoatendimento do Azure AD, uma soma de partes de saudação

Autoatendimento redefinição de senha no AD do Azure é composta de saudação componentes a seguir:

* **Portal de configuração de gerenciamento de senha** onde você pode controlar as opções de como as senhas são gerenciadas no seu locatário pelo Olá portal do Azure
* **Portal de registro de redefinição de senha**, onde os usuários podem se autorregistrar para a redefinição de senha
* **Portal de redefinição de senha** onde os usuários podem redefinir suas senhas usando desafios Olá definidos pelo administrador hello e Olá respostas usuários forneceu
* **Portal de alteração de senha do usuário**, onde os usuários podem alterar suas próprias senhas inserindo a senha antiga e escolhendo uma nova
* **Relatórios de gerenciamento de senha** onde os administradores podem exibir e analisar a atividade de senha de relatórios para seus locatários em Olá portal do Azure
* **Write-back de senha tooon-local usando o Azure AD Connect** permite que você tooenable gerenciamento de local, federado, ou os usuários da nuvem Olá sincronizadas

## <a name="azure-ad-pricing-sla-updates-and-roadmap"></a>Preços do Azure AD, SLA, atualizações e roteiro

Mais detalhes sobre esses tópicos podem ser encontradas no hello páginas a seguir

* [**Detalhes de preços do Azure AD**](https://azure.microsoft.com/pricing/details/active-directory/)
* [**Preços do Office 365**](https://products.office.com/compare-all-microsoft-office-products?tab=2)
* [**Contratos de Nível de Serviço do Azure**](https://azure.microsoft.com/support/legal/sla/)
* [**Contrato de Nível de Serviço do Microsoft Online Services**](http://go.microsoft.com/fwlink/?LinkID=272026&clcid=0x409)
* [**Atualizações do Azure**](https://azure.microsoft.com/updates/)
* [**Roteiro do Azure**](https://www.microsoft.com/cloud-platform/roadmap-recently-available)

## <a name="next-steps"></a>Próximas etapas

Olá links a seguir fornece informações adicionais sobre a redefinição de senha usando o AD do Azure

* [**Início Rápido**](active-directory-passwords-getting-started.md): comece agora mesmo a usar o gerenciamento de autoatendimento de senhas do Azure AD 
* [**Licenciamento** ](active-directory-passwords-licensing.md) - Configuração do licenciamento do Azure AD
* [**Dados** ](active-directory-passwords-data.md) - entender dados Olá necessários e como ele é usado para gerenciamento de senha
* [**Distribuição** ](active-directory-passwords-best-practices.md) -planejar e implantar os usuários de tooyour SSPR usando Olá diretrizes encontradas aqui
* [**Personalizar** ](active-directory-passwords-customize.md) -personalizar Olá aparência de saudação SSPR experiência para sua empresa.
* [**Relatórios**](active-directory-passwords-reporting.md): descubra se, quando e onde os usuários estão acessando a funcionalidade SSPR
* [**Mergulho profundo técnica** ](active-directory-passwords-how-it-works.md) -vá atrás Olá cortina toounderstand como ele funciona
* [**Perguntas frequentes**](active-directory-passwords-faq.md): como? Por quê? O quê? Onde? Quem? Quando? -Respostas tooquestions você sempre quis tooask
* [**Solucionar problemas de** ](active-directory-passwords-troubleshoot.md) -Saiba como problemas comuns de tooresolve que vemos com SSPR

