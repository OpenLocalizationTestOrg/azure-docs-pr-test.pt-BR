---
title: aaaAzure do Active Directory de perguntas frequentes de acesso condicional | Microsoft Docs
description: Obtenha respostas toofrequently perguntas frequentes sobre o acesso condicional no Active Directory do Azure.
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 14f7fc83-f4bb-41bf-b6f1-a9bb97717c34
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: d23acbb01217d7e9717d1a43de1b46a929404118
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-conditional-access-faqs"></a>Perguntas frequentes sobre o acesso condicional ao Azure Active Directory

## <a name="which-applications-work-with-conditional-access-policies"></a>Quais aplicativos funcionam com políticas de acesso condicional?

Para obter informações sobre aplicativos que funcionam com políticas de acesso condicional, consulte [Aplicativos e navegadores que usam regras de acesso condicional no Azure Active Directory](active-directory-conditional-access-supported-apps.md).

## <a name="are-conditional-access-policies-enforced-for-b2b-collaboration-and-guest-users"></a>As políticas de acesso condicional são impostas para colaboração B2B e usuários convidados?

As políticas são impostas para usuários de colaboração B2B (entre empresas). No entanto, em alguns casos, um usuário não pode ser capaz de toosatisfy requisitos da política de saudação. Por exemplo, a organização de um usuário convidado pode não oferecer suporte à autenticação multifator. 



## <a name="does-a-sharepoint-online-policy-also-apply-tooonedrive-for-business"></a>Uma política do SharePoint Online também se aplicam tooOneDrive para a empresa?

Sim. Uma política do SharePoint Online também se aplica a tooOneDrive para empresas.


## <a name="why-cant-i-set-a-policy-on-client-apps-like-word-or-outlook"></a>Por que não é possível definir uma política em aplicativos cliente, como o Word ou o Outlook?

Uma política de acesso condicional define os requisitos para acessar um serviço. Ela será aplicada quando o serviço de autenticação da toothat ocorre. política de saudação não definida diretamente em um aplicativo cliente. Em vez disso, ela será aplicada quando um cliente chamar um serviço. Por exemplo, uma política definida no SharePoint aplica tooclients chamando do SharePoint. Uma conjunto de políticas no Exchange se aplica a tooOutlook.

## <a name="does-a-conditional-access-policy-apply-tooservice-accounts"></a>Uma política de acesso condicional se aplica a contas tooservice?

Políticas de acesso condicional se aplicam a contas de usuário tooall. Isso inclui as contas de usuário usadas como contas de serviço. Geralmente, uma conta de serviço for executado autônoma não pode atender aos requisitos de saudação de uma política de acesso condicional. Por exemplo, autenticação multifator pode ser necessária. As contas de serviços podem ser excluídas de uma política ao usar configurações de gerenciamento de política de acesso condicional. 

## <a name="are-graph-apis-available-for-configuring-conditional-access-policies"></a>As APIs do Graph estão disponíveis para configurar as políticas de acesso condicional?

No momento, não. 

## <a name="what-is-hello-default-exclusion-policy-for-unsupported-device-platforms"></a>O que é política de exclusão padrão Olá para plataformas de dispositivos sem suporte?

No momento, as políticas de acesso condicional são impostas seletivamente aos usuários de dispositivos com Android e iOS. Aplicativos em outras plataformas de dispositivo, por padrão, não são afetados pela política de acesso condicional Olá para dispositivos iOS e Android. Um administrador de locatário pode escolher toooverride Olá política global toodisallow acesso toousers em plataformas que não são suportadas.


## <a name="how-do-conditional-access-policies-work-for-microsoft-teams"></a>Como as políticas de acesso condicional funcionam para o Microsoft Teams?  

O Microsoft Teams depende muito do Exchange Online e do SharePoint Online para cenários de produtividade de núcleo, como reuniões, calendários e compartilhamento de arquivos. Políticas de acesso condicional que são definidas para esses aplicativos de nuvem se aplicam a equipes tooMicrosoft quando um usuário faz logon.

O Microsoft Teams também tem suporte separadamente como um aplicativo de nuvem em políticas de acesso condicional do Azure Active Directory. Políticas de autoridade de certificado que são definidas para um aplicativo de nuvem se aplicam a equipes tooMicrosoft quando um usuário faz logon.

Os clientes de área de trabalho do Microsoft Teams para Windows e Mac oferecem suporte a autenticação moderna. Autenticação moderna traz a entrada com base em aplicativos cliente do hello Azure Active Directory autenticação Library (ADAL) tooMicrosoft Office em plataformas. 
