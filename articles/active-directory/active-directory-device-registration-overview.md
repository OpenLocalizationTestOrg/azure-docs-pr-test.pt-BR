---
title: "Visão geral do registro de dispositivo do Active Directory aaaAzure | Microsoft Docs"
description: "Registro de dispositivo do Active Directory do Azure é a base de saudação para cenários de acesso condicional com base no dispositivo. Quando um dispositivo é registrado, provisões de registro de dispositivo do Active Directory do Azure Olá dispositivo com uma identidade que é o dispositivo de saudação do tooauthenticate usado quando Olá usuário faz logon."
services: active-directory
keywords: registro de dispositivos, habilitar registro de dispositivos, registro de dispositivos e MDM
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 1e92c1a2-01b8-4225-950b-373cd601b035
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: b9846e34fe873d271ebe71cbf8e70c6b4768885b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-device-registration"></a>Introdução ao registro de dispositivos do Azure Active Directory
Registro de dispositivo do Active Directory do Azure é a base de saudação para cenários de acesso condicional com base no dispositivo. Quando um dispositivo é registrado, registro de dispositivo do Active Directory do Azure fornece dispositivo Olá com uma identidade que é o dispositivo de saudação do tooauthenticate usado quando Olá usuário faz logon. dispositivo Olá autenticado e atributos de saudação do dispositivo hello, podem ser usado tooenforce políticas de acesso condicional para aplicativos hospedados na nuvem hello e local.

Quando combinado com uma solução de management(MDM) de dispositivo móvel como Microsoft Intune, os atributos de dispositivo Olá no Active Directory do Azure são atualizados com informações adicionais sobre o dispositivo de saudação. Isso permite regras de acesso condicional toocreate que imponham acesso de dispositivos toomeet aos padrões de segurança e conformidade. Para saber mais sobre o registro de dispositivos no Microsoft Intune, veja [Registrar dispositivos para gerenciamento no Intune](https://docs.microsoft.com/intune/deploy-use/enroll-devices-in-microsoft-intune).

## <a name="scenarios-enabled-by-azure-active-directory-device-registration"></a>Cenários habilitados por registro de dispositivos do Azure Active Directory
O registro de dispositivos do Azure Active Directory inclui suporte para dispositivos iOS, Android e Windows. cenários de saudação individuais que utilizam o registro de dispositivo do AD do Azure podem ter requisitos e suporte de plataforma mais específicos. Esses cenários são os seguintes:

* **Tooapplications de acesso condicional que estão hospedados no local**: você pode usar dispositivos registrados com políticas de acesso para aplicativos que são configurados toouse do AD FS com o Windows Server 2012 R2. Para obter mais informações sobre como configurar o acesso condicional para local, consulte [Configurando o acesso condicional local usando o registro do dispositivo do Azure Active Directory](active-directory-device-registration-on-premises-setup.md).
* **Acesso condicional para aplicativos do Office 365 com o Microsoft Intune** : os administradores de TI podem provisionar o acesso condicional dispositivo políticas toosecure recursos corporativos, enquanto a saudação mesmo momento que permite aos operadores de informações em dispositivos compatíveis Serviços de saudação tooaccess. Para mais informações, consulte [Políticas de dispositivo de acesso condicional para serviços do Office 365](active-directory-conditional-access-device-policies.md).

## <a name="setting-up-azure-active-directory-device-registration"></a>Configuração do registro de dispositivos Azure Active Directory
É necessário tooenable registro do dispositivo do AD do Azure no hello Portal do Azure para que os dispositivos móveis possam descobrir serviço Olá procurando registros DNS conhecidos. Você deve configurar DNS da sua empresa para que os dispositivos Windows 10, Windows 8.1, Windows 7, Android e iOS podem descobrir e usar o serviço de saudação.
Você pode exibir e habilitar/desabilitar os dispositivos registrados usando Olá Portal do administrador no Active Directory do Azure.

> [!NOTE]
> Para obter instruções mais recentes sobre como ver tooset o registro automático do dispositivo, [como toosetup o registro automático de domínio do Windows associados a dispositivos com o Active Directory do Azure](active-directory-conditional-access-automatic-device-registration-setup.md).
> 
> 

### <a name="enable-azure-active-directory-device-registration-service"></a>Habilitar o serviço de registro de dispositivos do Azure Active Directory
1. Entre em toohello portal do Microsoft Azure como administrador.
2. No painel esquerdo do hello, selecione **do Active Directory**.
3. Em Olá **diretório** , selecione seu diretório.
4. Selecione Olá **configurar** guia.
5. Role toohello seção chamada **dispositivos**.
6. Selecione **TODOS** para **USUÁRIOS PODEM USAR DISPOSITIVOS COM INGRESSO NO LOCAL DE TRABALHO**.
7. Selecione o número máximo de saudação de dispositivos que você deseja tooauthorize por usuário.

> [!NOTE]
> O registro com o Microsoft Intune ou o gerenciamento de dispositivos móveis para o Office 365 exige ingresso no local de trabalho. Se você tiver configurado um desses serviços, todos está selecionada e Olá NONE botão está desabilitado.
> 
> 

Por padrão, a autenticação de dois fatores não está habilitada para o serviço de saudação. No entanto, a autenticação de dois fatores é recomendável ao registrar um dispositivo.

* Antes de solicitar a autenticação de dois fatores para esse serviço, você deve configurar um provedor de autenticação de dois fatores no Azure Active Directory e configurar as contas de usuário para autenticação multifator, consulte [adicionando multi-Factor TooAzure de autenticação do Active Directory](../multi-factor-authentication/multi-factor-authentication-get-started-cloud.md)
* Se estiver usando o AD FS com o Windows Server 2012 R2, configure um módulo de autenticação de dois fatores no AD FS. Veja [Usar a Autenticação Multifator com os Serviços de Federação do Active Directory](../multi-factor-authentication/multi-factor-authentication-get-started-server.md).

## <a name="configure-azure-active-directory-device-registration-discovery"></a>Configurar a descoberta de registro de dispositivos do Azure Active Directory
Dispositivos do Windows 7 e Windows 8.1 descobre o serviço de registro de dispositivo Olá combinando Olá nome de conta de usuário com um nome de servidor de registro de dispositivo conhecido.

Você deve criar um registro de DNS CNAME que aponte toohello um registro a associado com seu serviço de registro de dispositivo do Active Directory do Azure. Olá registro CNAME deve usar enterpriseregistration de um prefixo conhecido Olá seguido pelo sufixo UPN Olá usado pelas contas de usuário Olá na sua organização. Se sua organização usa vários sufixos UPN, vários registros CNAME devem ser criados no DNS.

Por exemplo, se você usa dois sufixos UPN na sua organização chamada @contoso.com e @region.contoso.com, você criará Olá registros DNS a seguir.

| Entrada | Tipo | Endereço |
| --- | --- | --- |
| enterpriseregistration.contoso.com |CNAME |enterpriseregistration.windows.net |
| enterpriseregistration.region.contoso.com |CNAME |enterpriseregistration.windows.net |

## <a name="view-and-manage-device-objects-in-azure-active-directory"></a>Exibir e gerenciar objetos de dispositivo no Active Directory do Azure
1. No portal do administrador do Azure hello, exibir, bloquear e desbloquear dispositivos. Um dispositivo que está bloqueado não terá mais acesso tooapplications que são configurados tooallow apenas dispositivos registrados.
2. Faça logon no toohello Portal do Microsoft Azure como administrador.
3. No painel esquerdo do hello, selecione **do Active Directory**.
4. Selecione seu diretório.
5. Selecione Olá **usuários** guia. Selecione um usuário tooview seus dispositivos
6. Selecione Olá **dispositivos** guia.
7. Selecione **dispositivos registrados** de saudação menu suspenso.
8. Aqui você pode ver, bloquear ou desbloquear os dispositivos registrados dos usuários hello.

## <a name="additional-topics"></a>Tópicos adicionais
Você pode registrar seus dispositivos Ingressados no Domínio do Windows 7 e do Windows 8.1 com o registro de dispositivos do Azure AD. Olá tópicos a seguir fornece mais informações sobre pré-requisitos de saudação e registro de dispositivo Olá etapas tooconfigure necessário em dispositivos Windows 7 e Windows 8.1.

* [Registro de dispositivo automático com o Active Directory do Azure para dispositivos de domínio associado do Windows](active-directory-conditional-access-automatic-device-registration.md)
* [Registro de dispositivo automático com o Azure Active Directory para dispositivos ingressados no domínio do Windows 10](active-directory-azureadjoin-devices-group-policy.md)

