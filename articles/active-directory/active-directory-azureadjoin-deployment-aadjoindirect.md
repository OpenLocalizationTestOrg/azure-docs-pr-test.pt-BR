---
title: "aaaUsage cenários e considerações de implantação para a junção do Azure AD | Microsoft Docs"
description: "Explica como os administradores podem configurar a Junção do AD do Azure para seus usuários finais (funcionários, estudantes, outros usuários). Ele também aborda diferentes cenários do mundo real Olá para o uso de junção do Azure AD."
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: 81d4461e-21c8-4fdd-9076-0e4991979f62
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 7e57971481aa312ebf8a69999d194f9dcc3d4708
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="usage-scenarios-and-deployment-considerations-for-azure-ad-join"></a>Cenários de uso e considerações de implantação para a Junção do Azure AD
## <a name="usage-scenarios-for-azure-ad-join"></a>Cenários de uso da Junção do Azure AD
### <a name="scenario-1-businesses-largely-in-hello-cloud"></a>Cenário 1: Empresas em grande parte na nuvem de saudação
Azure junção do Active Directory (junção do Azure AD) pode aproveitar a se você atualmente operar e gerenciar identidades para a sua empresa na nuvem hello ou estiver movendo nuvem toohello em breve. Você pode usar uma conta que você criou no AD do Azure toosign em tooWindows 10. Por meio de [Olá executado pela primeira vez o processo de experiência (FRX)](active-directory-azureadjoin-user-frx.md), ou ingressando AD Azure do [menu de configurações de saudação](active-directory-azureadjoin-user-upgrade.md), os usuários podem ingressar seu tooAzure máquinas AD.  Os usuários também podem aproveitar logon único (SSO) acesso muito recursos como o Office 365, em seus navegadores ou aplicativos do Office de nuvem.

### <a name="scenario-2-educational-institutions"></a>Cenário 2: instituições de ensino
Instituições de ensino normalmente têm dois tipos de usuário: professores e alunos. Os membros são considerados membros de longo prazo da organização hello. É recomendável criar contas locais para eles. Mas os alunos são shorter-term membros da organização hello e podem ser gerenciadas suas contas no AD do Azure. Isso significa que a escala de diretório pode ser enviada nuvem toohello em vez de ser armazenada localmente. Isso também significa que os alunos serão capaz de toosign em tooWindows com suas contas do AD do Azure e obter acesso a 365 recursos tooOffice em aplicativos do Office.

### <a name="scenario-3-retail-businesses"></a>Cenário 3: empresas de varejo
Lojas varejistas geralmente têm funcionários temporários e de longo prazo. Geralmente criamos contas locais e computadores unidos ao domínio para funcionários em tempo integral de longo prazo. Mas sazonais trabalhadores são shorter-term membros da organização hello e é desejável toomanage suas contas onde licenças de usuário podem ser movidas mais facilmente ao redor. Quando você cria suas contas de usuário na nuvem Olá com licenças do Office 365, esses usuários obtém benefícios de saudação da assinatura tooWindows e aplicativos do Office com uma conta do AD do Azure, enquanto você manter mais flexibilidade com suas licenças depois de sair.

### <a name="scenario-4-additional-scenarios"></a>Cenário 4: outros cenários
Juntamente com os benefícios de saudação discutidos anteriormente, você se beneficiar de seus usuários ingressar seu dispositivos tooAzure AD devido a uma experiência simplificada de junção, gerenciamento de dispositivo eficiente, registro de gerenciamento automático do dispositivo móvel e tooAzure de logon único AD e recursos locais.  

## <a name="deployment-considerations-for-azure-ad-join"></a>Considerações de implantação para a Junção do Azure AD
### <a name="enable-your-users-toojoin-a-company-owned-device-directly-tooazure-ad"></a>Habilitar o toojoin usuários um dispositivo da empresa diretamente tooAzure AD
As empresas podem fornecer organizações e empresas de toopartner contas somente em nuvem. Esses parceiros podem acessar facilmente os aplicativos da empresa e os recursos com o logon único. Esse cenário é aplicável toousers que acessam recursos principalmente na nuvem hello, como o Office 365 ou SaaS aplicativos que dependem do AD do Azure para autenticação.

### <a name="prerequisites"></a>Pré-requisitos
**No nível de empresa hello (administrador)**

* Assinatura do Azure com o Azure Active Directory  

**No nível de usuário Olá**

* Windows 10 (Professional e Enterprise Editions)

### <a name="administrator-tasks"></a>Tarefas do administrador
* [Configure o registro de dispositivos](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Tarefas do usuário
* [Configurar um novo dispositivo Windows 10 com o Azure AD durante a instalação](active-directory-azureadjoin-user-frx.md)
* [Configurar um dispositivo Windows 10 com o Azure AD no menu de configurações de saudação](active-directory-azureadjoin-user-upgrade.md)
* [Ingressar em uma organização de tooyour de dispositivo pessoal do Windows 10](active-directory-azureadjoin-personal-device.md)

## <a name="enable-byod-in-your-organization-for-windows-10"></a>Habilitar o BYOD na sua organização para o Windows 10
Você pode configurar seu funcionários e usuários toouse seus recursos e aplicativos da empresa do Windows dispositivos (BYOD) tooaccess pessoal. Os usuários podem adicionar seu AD do Azure contas (contas corporativas ou de estudante) tooa pessoal Windows dispositivo tooaccess recursos de forma segura e compatível.

### <a name="prerequisites"></a>Pré-requisitos
**No nível de empresa hello (administrador)**

* Assinatura do Azure AD

**No nível de usuário Olá**

* Windows 10 (Professional e Enterprise Editions)

### <a name="administrator-tasks"></a>Tarefas do administrador
* [Configure o registro de dispositivos](active-directory-azureadjoin-setup.md)

### <a name="user-tasks"></a>Tarefas do usuário
* [Ingressar em uma organização de tooyour de dispositivo pessoal do Windows 10](active-directory-azureadjoin-personal-device.md)

## <a name="additional-information"></a>Informações adicionais
* [Windows 10 para a empresa Olá: dispositivos de toouse maneiras de trabalho](active-directory-azureadjoin-windows10-devices-overview.md)
* [Estendendo nuvem dispositivos de tooWindows 10 de recursos por meio de junção do Active Directory do Azure](active-directory-azureadjoin-user-upgrade.md)
* [Autenticando identidades sem senhas com o Microsoft Passport](active-directory-azureadjoin-passport.md)
* [Saiba mais sobre cenários de uso da Junção do Azure AD](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [Conecte-se a dispositivos que ingressaram no domínio tooAzure AD para experiências do Windows 10](active-directory-azureadjoin-devices-group-policy.md)
* [Configurar a Junção do Azure AD](active-directory-azureadjoin-setup.md)

