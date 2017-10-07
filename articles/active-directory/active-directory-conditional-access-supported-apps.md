---
title: aaaApplications e navegadores que usam regras de acesso condicional no Active Directory do Azure | Microsoft Docs
description: "Com controle de acesso condicional, Active Directory do Azure verifica condições específicas quando ele autentica o usuário hello e tooallow acesso ao aplicativo."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 62349fba-3cc0-4ab5-babe-372b3389eff6
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/22/2017
ms.author: markvi
ms.reviewer: calebb
ms.openlocfilehash: ca20853bb9f4b22d0b88ddd2f051d658e0d88cf3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="applications-and-browsers-that-use-conditional-access-rules-in-azure-active-directory"></a>Aplicativos e navegadores que usam regras de acesso condicional no Azure Active Directory

As regras de acesso condicional têm suporte em aplicativos conectados do Azure Active Directory, (Azure AD) aplicativos SaaS (software como serviço) federados pré-integrados, aplicativos que usam senha de logon único (SSO), aplicativos de linha de negócios e aplicativos que usam o Proxy de Aplicativo Azure AD. Para obter uma lista detalhada dos aplicativos para os quais você pode habilitar o acesso condicional, veja [Serviços habilitados com acesso condicional](active-directory-conditional-access-technical-reference.md). O acesso condicional funciona com os aplicativos móveis e da área de trabalho que usam autenticação moderna. Neste artigo, abordaremos o funcionamento do acesso condicional em aplicativos móveis e de área de trabalho.

Você pode usar páginas de entrada do Azure AD em aplicativos que usam autenticação moderna. Com uma página de logon, a autenticação multifator é solicitada de um usuário. É mostrada uma mensagem se o acesso de saudação do usuário será bloqueado. Autenticação moderna é necessária para Olá tooauthenticate de dispositivo com o AD do Azure, para que as políticas de acesso condicional baseado em dispositivo são avaliadas.

É importante tooknow quais aplicativos podem usar regras de acesso condicional e Olá etapas que talvez você precise tootake toosecure outros pontos de entrada do aplicativo.

## <a name="applications-that-use-modern-authentication"></a>Aplicativos que usam a autenticação moderna
> [!NOTE]
> Se você tiver uma política de acesso condicional no Azure AD com um equivalente no Office 365, configure duas políticas de acesso condicional. Isso seria aplicada, por exemplo, tooconditional as políticas de acesso para o Exchange Online ou SharePoint Online.
>
>

Olá seguintes aplicativos dão suporte ao acesso condicional para o Office 365 e outros aplicativos de serviço conectado de AD do Azure:


| Serviço de Destino| Plataforma| Aplicativo |
| --- | --- | --- |
| Qualquer serviço de aplicativo de Meus Aplicativos| Android e iOS| Política de localização e MFA para aplicativos. Políticas baseadas em dispositivos não têm suporte.|
| Serviço de Aplicativo Remoto do Azure| Windows 10, Windows 8.1, Windows 7, iOS, Android e Mac OS X| Aplicativo Remoto do Azure|
| Dynamics CRM| Windows 10, Windows 8.1, Windows 7, iOS e Android| Aplicativo Dynamics CRM|
| Equipes da Microsoft| Windows 10, Windows 8.1, Windows 7, iOS/Android e MAC OSX| Microsoft Team Services – controla todos os serviços que dão suporte ao Microsoft Teams e todos os seus aplicativos cliente – Windows Desktop, MAC OS X, iOS, Android, WP e cliente da Web|
| Office 365 Exchange Online| Windows 10| Aplicativo de Calendário/Email/Pessoas, Outlook 2016, Outlook 2013 (com autenticação moderna), Skype for Business (com autenticação moderna)|
| Office 365 Exchange Online| Windows 8.1, Windows 7| Outlook 2016, Outlook 2013 (com autenticação moderna), Skype for Business (com autenticação moderna)|
| Office 365 Exchange Online| iOS| Aplicativo móvel do Outlook|
| Office 365 Exchange Online| Mac OS X| Outlook 2016 (Office para macOS)|
| Office 365 SharePoint Online| Windows 10| Aplicativos do Office 2016, Office Universal de aplicativos, Office 2013 (com autenticação moderna), o cliente de sincronização OneDrive (consulte [notas](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)), suporte de grupos do Office planejado para Olá futuras, suporte de aplicativo do SharePoint planejado para Olá futuras|
| Office 365 SharePoint Online| Windows 8.1, Windows 7| Aplicativos do Office 2016, Office 2013 (com autenticação moderna), cliente de sincronização do OneDrive (veja as [observações](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))|
| Office 365 SharePoint Online| iOS, Android| Aplicativos móveis do Office|
| Office 365 SharePoint Online| Mac OS X| Office 2016 para macOS (somente Word, Excel, PowerPoint, OneNote). OneDrive para suporte de negócios planejada para Olá futuras|
| Office 365 Yammer| Windows 10, iOS, Android| Aplicativo Office Yammer|
| Serviço PowerBI| Windows 10, Windows 8.1, Windows 7 e iOS| Aplicativo PowerBI. Olá aplicativo do Power BI para Android no momento não oferece suporte para acesso condicional com base no dispositivo.|
| Visual Studio Team Services| Windows 10, Windows 8.1, Windows 7, iOS e Android| Aplicativo Visual Studio Team Services|








## <a name="applications-that-do-not-use-modern-authentication"></a>Aplicativos que não usam autenticação moderna
No momento, você deve usar outros tooapps acesso tooblock de métodos que não usam autenticação moderna. As regras de acesso para aplicativos que não usam a autenticação moderna não são impostas por acesso condicional. Isso é basicamente uma consideração para acesso ao Exchange e ao SharePoint. A maioria das versões anteriores de aplicativos usar protocolos antigos de controle de acesso.

### <a name="control-access-in-office-365-sharepoint-online"></a>Controlar o acesso no Office 365 SharePoint Online
Você pode desabilitar protocolos herdados para acesso ao SharePoint usando o cmdlet Olá SPOTenant conjunto. Use este clientes do Office tooprevent cmdlet que usam protocolos de autenticação não moderna acessem recursos do SharePoint Online.

**Exemplo de comando**: `Set-SPOTenant -LegacyAuthProtocolsEnabled $false`

### <a name="control-access-in-office-365-exchange-online"></a>Controlar o acesso no Office 365 Exchange Online
O Exchange oferece duas categorias principais de protocolos. Examine Olá as opções a seguir e selecione política Olá adequada para sua organização.

* **Exchange ActiveSync**. Por padrão, as políticas de acesso condicional para a autenticação multifator e local não são impostas para o Exchange ActiveSync. Você precisar tooprotect acesso toothese serviços por meio da configuração de política do Exchange ActiveSync diretamente ou pelo bloqueio do Exchange ActiveSync usando regras de serviços de Federação do Active Directory (AD FS).
* **Protocolos herdados**. Você pode bloquear os protocolos herdados com o AD FS. Isso impede que clientes do Office access tooolder, como o Office 2013 sem autenticação moderna habilitado e versões anteriores do Office.

### <a name="use-ad-fs-tooblock-legacy-protocol"></a>Usar protocolo herdado do AD FS tooblock
Você pode usar o hello exemplo emissão autorização regras tooblock protocolo herdado, o acesso no nível de saudação do AD FS a seguir. Escolha entre duas configurações comuns.

#### <a name="option-1-allow-exchange-activesync-and-allow-legacy-apps-but-only-on-hello-intranet"></a>Opção 1: Permitir que o Exchange ActiveSync e permitir que os aplicativos herdados, mas somente na intranet Olá
Aplicando Olá três toohello de regras a seguir de terceira parte confiável do AD FS confiança para a plataforma de identidade do Microsoft Office 365, o tráfego do Exchange ActiveSync, e navegador e o tráfego de autenticação moderna têm acesso. Aplicativos herdados são impedidos de saudação extranet.

##### <a name="rule-1"></a>Regra 1
    @RuleName = "Allow all intranet traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-2"></a>Regra 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

##### <a name="rule-3"></a>Regra 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");

#### <a name="option-2-allow-exchange-activesync-and-block-legacy-apps"></a>Opção 2: Permitir o Exchange ActiveSync e bloquear aplicativos herdados
Aplicando Olá três toohello de regras a seguir de terceira parte confiável do AD FS confiança para a plataforma de identidade do Microsoft Office 365, o tráfego do Exchange ActiveSync, e navegador e o tráfego de autenticação moderna têm acesso. Aplicativos herdados são bloqueados de qualquer localização.

##### <a name="rule-1"></a>Regra 1
    @RuleName = "Allow all intranet traffic only for browser and modern authentication clients"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "true"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-2"></a>Regra 2
    @RuleName = "Allow Exchange ActiveSync"
    c1:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-client-application", Value == "Microsoft.Exchange.ActiveSync"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


##### <a name="rule-3"></a>Regra 3
    @RuleName = "Allow extranet browser and browser dialog traffic"
    c1:[Type == "http://schemas.microsoft.com/ws/2012/01/insidecorporatenetwork", Value == "false"] &&
    c2:[Type == "http://schemas.microsoft.com/2012/01/requestcontext/claims/x-ms-endpoint-absolute-path", Value =~ "(/adfs/ls)|(/adfs/oauth2)"]
    => issue(Type = "http://schemas.microsoft.com/authorization/claims/permit", Value = "true");


## <a name="supported-browsers-for-device-based-policies"></a>Navegadores com suporte para políticas baseadas em dispositivo 

Você só pode obter acesso para políticas de dispositivo com base em verificar para ingresso no domínio e de conformidade do dispositivo ao AD do Azure pode identificar e autenticar o dispositivo de saudação. Enquanto a maioria das verificações, como o local e o trabalho MFA na maioria dos dispositivos e navegadores, políticas de dispositivo requerem da versão de hello sistemas operacionais e navegadores listados abaixo. Acesso será bloqueado para os usuários em navegadores sem suporte ou sistemas operacionais de saudação quando uma política de dispositivo está em vigor. 

| SO                     | Navegadores                 | Suporte     |
| :--                    | :--                      | :-:         |
| Win 10                 | IE, Edge                 | ![Verificação][1] |
| Win 10                 | Chrome                   | Visualização     |
| Win 8 / 8.1            | IE, Chrome               | ![Verificação][1] |
| Win 7                  | IE, Chrome               | ![Verificação][1] |
| iOS                    | Safari                   | ![Verificação][1] |
| Android                | Chrome                   | ![Verificação][1] |
| Windows Phone          | IE, Edge                 | ![Verificação][1] |
| Windows Server 2016    | IE, Edge                 | ![Verificação][1] |
| Windows Server 2016    | Chrome                   | Em breve |
| Windows Server 2012 R2 | IE, Chrome               | ![Verificação][1] |
| Windows Server 2008 R2 | IE, Chrome               | ![Verificação][1] |
| Mac OS                 | Safari                   | ![Verificação][1] |
| Mac OS                 | Chrome                   | Em breve |

> [!NOTE]
> Para obter suporte Chrome, você deve estar usando criadores de atualização do Windows 10 e instalar extensão do hello encontrada [aqui](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji).
>
>

## <a name="next-steps"></a>Próximas etapas

Para obter mais detalhes, confira [Acesso condicional no Azure Active Directory](active-directory-conditional-access.md)




<!--Image references-->
[1]: ./media/active-directory-conditional-access-supported-apps/ic195031.png


