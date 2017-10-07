---
title: aaaVulnerabilities detectados pelo Azure Active Directory Identity Protection | Microsoft Docs
description: "Visão geral de vulnerabilidades Olá detectados pelo Azure Active Directory Identity Protection."
services: active-directory
keywords: "azure active directory identity protection, cloud app discovery, gerenciamento de aplicativos, segurança, risco, nível de risco, vulnerabilidade, política de segurança"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92233a5b-cb34-4d28-88cc-d5d29c0f3256
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: 5e1cb401f8b566a180eb46e3420a090bcfc66767
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="vulnerabilities-detected-by-azure-active-directory-identity-protection"></a>Vulnerabilidades detectadas pelo Azure Active Directory Identity Protection
Vulnerabilidades são pontos fracos no seu ambiente que podem ser explorados por um invasor. É recomendável que você resolver essas vulnerabilidades tooimprove Olá a postura de segurança da sua organização e impedir que invasores explorando-los.


![vulnerabilidades](./media/active-directory-identityprotection-vulnerabilities/101.png "vulnerabilidades")



Olá seções a seguir fornecem uma visão geral das vulnerabilidades Olá relatado pela proteção de identidade.

## <a name="multi-factor-authentication-registration-not-configured"></a>Registro de autenticação multifator não configurado
Essa vulnerabilidade ajuda a controlar a implantação de saudação do Azure multi-Factor Authentication na sua organização. 

Autenticação multifator do Azure fornece uma segunda camada toouser de autenticação de segurança. Ele ajuda a proteger acesso toodata e aplicativos atendendo a demanda do usuário para um processo de logon simple. Ele fornece autenticação forte por meio de uma variedade de opções de fácil verificação — chamada telefônica, mensagem de texto, notificação de aplicativo móvel ou verificação de código e tokens OATH de terceiros.

Recomendamos exigir o Azure Multi-Factor Authentication para entradas de usuário. A autenticação multifator desempenha um papel fundamental nas políticas de acesso condicional baseadas em risco disponíveis por meio do Identity Protection.

Para obter mais detalhes, veja [O que é o Azure Multi-Factor Authentication?](../multi-factor-authentication/multi-factor-authentication.md)

## <a name="unmanaged-cloud-apps"></a>Aplicativos de nuvem não gerenciados
Essa vulnerabilidade ajuda a identificar aplicativos de nuvem não gerenciados na sua organização.

Os departamentos de TI nas empresas modernas, geralmente são não sabe nada sobre todos os aplicativos de nuvem Olá que os usuários em sua organização estiver usando toodo seu trabalho. É fácil toosee por que os administradores terão preocupações sobre dados de toocorporate de acesso não autorizado, perda de dados e outros riscos de segurança. 

É recomendável que sua organização implantar aplicativos em nuvem Cloud App Discovery toodiscover não gerenciado e toomanage esses aplicativos usando o Active Directory do Azure.

Para obter mais detalhes, veja [Encontrando aplicativos de nuvem não gerenciados com o Cloud App Discovery](active-directory-cloudappdiscovery-whatis.md).

## <a name="security-alerts-from-privileged-identity-management"></a>Alertas de Segurança do Privileged Identity Management
Essa vulnerabilidade ajuda você a descobrir e resolver alertas sobre identidades com privilégios na sua organização.  

toocarry de usuários tooenable operações privilegiadas, as organizações precisam toogrant usuários privilegiados temporários ou permanentes de acesso no AD do Azure, os recursos do Azure ou Office 365 ou outros aplicativos SaaS. Cada um desses usuários privilegiados aumenta Olá de superfície de ataque da sua organização. Essa vulnerabilidade ajuda a identificar os usuários com acesso privilegiado desnecessário e tomar a ação apropriada tooreduce ou eliminar o risco de saudação que representam. 

É recomendável que sua organização usa o Azure AD Privileged Identity Management toomanage, controle e identidades com privilégios de monitor e seus tooresources de acesso no AD do Azure, bem como outros Microsoft online services como Office 365 ou Microsoft Intune.

Para obter mais detalhes, veja [Azure AD Privileged Identity Management](active-directory-privileged-identity-management-configure.md). 

## <a name="see-also"></a>Confira também
* [Azure Active Directory Identity Protection](active-directory-identityprotection.md)

