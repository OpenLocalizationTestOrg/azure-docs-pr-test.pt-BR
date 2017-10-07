---
title: "políticas de dispositivo de acesso condicional aaaAzure do Active Directory para serviços do Office 365 | Microsoft Docs"
description: "Saiba mais sobre como tooprovision toohelp de políticas de dispositivo de acesso condicional proteger recursos corporativos melhor, mantendo tooservices de conformidade e acesso do usuário."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 8664c0bb-bba1-4012-b321-e9c8363080a0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: 38229a8d9766efbf0e6b17875b3018011c6b4ea3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="active-directory-conditional-access-device-policies-for-office-365-services"></a>Políticas de dispositivo de acesso condicional do Active Directory para serviços do Office 365

Acesso condicional requer toowork de várias partes. Ele envolve um usuário autenticado com multifator, um dispositivo autenticado e um dispositivo em conformidade, entre outros fatores. Neste artigo, nosso foco principalmente nas condições com base no dispositivo que sua organização pode usar toohelp controlar acesso tooOffice 365 services. 

Usuários corporativos querem serviços tooaccess Office 365 como o Exchange e SharePoint Online no trabalho ou escola em seus dispositivos pessoais. Você deseja Olá acesso toobe segura. Você pode provisionar acesso condicional dispositivo políticas toohelp Verifique recursos corporativos mais seguros, durante a concessão de acesso tooservices para usuários que estão usando dispositivos compatíveis. Você pode definir políticas de acesso condicional tooOffice 365 no portal de acesso condicional do Microsoft Intune hello.

Azure Active Directory (AD do Azure) impõe o acesso condicional políticas toohelp acesso seguro tooOffice 365 os serviços. É possível criar uma política de acesso condicional que impede um usuário que usa um dispositivo fora de conformidade de acessar um serviço do Office 365. usuário Olá deve estar de acordo com políticas de dispositivo da empresa toohello antes que seja concedido acesso toohello serviço. Como alternativa, você pode criar uma política que exige que os usuários tooenroll tooan de acesso de toogain seus dispositivos serviço Office 365. As políticas podem ser aplicadas tooall usuários em uma organização ou limitada tooa alguns grupos de destino. Você pode adicionar mais políticas de tooa de grupos de destino ao longo do tempo.

Um pré-requisito para aplicação de políticas de dispositivo é que os usuários devem registrar seus dispositivos com o serviço de registro de dispositivo de saudação do AD do Azure. Você pode optar por tooturn na autenticação multifator para dispositivos que se registrar com hello o serviço de registro de dispositivo do AD do Azure. A autenticação multifator é recomendada para Olá serviço de registro de dispositivo do Active Directory do Azure. Quando a autenticação multifator é ativada, os usuários que registrem seus dispositivos com hello o serviço de registro de dispositivo do AD do Azure são desafiados para autenticação de dois fatores.

## <a name="how-does-a-conditional-access-policy-work"></a>Como funciona uma política de acesso condicional?

Quando um usuário solicita acesso tooan serviço Office 365 de uma plataforma de dispositivo com suporte, o Azure AD autentica o usuário hello e dispositivo hello. Serviço do Azure AD concede acesso toohello somente se o usuário hello está de acordo com política de toohello definida para o serviço de saudação. Os usuários em dispositivos que não estão registrados recebe instruções sobre como tooenroll e se tornem compatíveis tooaccess serviços corporativos do Office 365. Os usuários em dispositivos Android e iOS é necessário tooenroll seus dispositivos usando o aplicativo de Portal da empresa Intune hello. Quando um usuário registra um dispositivo, Olá dispositivo está registrado com o AD do Azure e ele é registrado para conformidade e gerenciamento de dispositivo. Você deve usar o serviço de registro de dispositivo Olá AD do Azure com Microsoft Intune para gerenciamento de dispositivos móveis para serviços do Office 365. Registro de dispositivo é necessário para os usuários tooaccess serviços do Office 365 quando as políticas de dispositivo são impostas.

Quando um usuário registra com êxito um dispositivo, o dispositivo de saudação se torna confiável. AD do Azure fornece aplicativos de toocompany de acesso de logon único de usuário Olá autenticado. O AD do Azure impõe um serviço acesso condicional política toogrant acesso tooa não apenas Olá Olá usuário solicita acesso, mas cada usuário em tempo de saudação renova uma solicitação de acesso. usuário Olá é negado acesso tooservices quando as credenciais de logon forem alteradas, dispositivo Olá for perdido ou roubado ou saudação da política de saudação não condições em tempo de saudação da solicitação de renovação.

## <a name="deployment-considerations"></a>Considerações de implantação

Você deve usar dispositivos de tooregister do serviço de registro do hello AD do Azure dispositivo.

Quando os usuários locais são sobre toobe autenticado, os serviços de Federação do Active Directory (AD FS) (versão 1.0 e posterior) é necessário. Autenticação multifator para ingresso falha quando o provedor de identidade Olá não é capaz de autenticação multifator. Por exemplo, não é possível usar a autenticação multifator com o AD FS 2.0. Certifique-se de que Olá local do AD FS funciona com autenticação multifator, e um método de autenticação multifator válido está em vigor antes de ativar a autenticação multifator para serviço de registro de dispositivo Olá AD do Azure. Por exemplo, o AD FS no Windows Server 2012 R2 tem funcionalidades de autenticação multifator. Você também deve definir um método de autenticação adicional válido (autenticação multifator) no servidor de saudação do AD FS antes de ativar a autenticação multifator para serviço de registro de dispositivo de saudação do AD do Azure. Para obter mais informações sobre os métodos de autenticação multifator com suporte no AD FS, consulte [Configurar métodos de autenticação adicionais do AD FS](/windows-server/identity/ad-fs/operations/configure-additional-authentication-methods-for-ad-fs).

## <a name="next-steps"></a>Próximas etapas

*   Para respostas toocommon perguntas, consulte [acesso condicional do Active Directory do Azure perguntas frequentes](active-directory-conditional-faqs.md).
