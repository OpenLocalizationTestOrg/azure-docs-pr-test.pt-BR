---
title: Aplicativos e navegadores que usam regras de acesso condicional no Azure Active Directory | Microsoft Docs
description: "Com o controle de acesso condicional, o Azure Active Directory verifica as condições específicas quando autentica o usuário e para permitir o acesso do aplicativo."
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
ms.openlocfilehash: 8614660f7c98af7b4e6d50348775495c67ae1cc8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="applications-and-browsers-that-use-conditional-access-rules-in-azure-active-directory"></a>Aplicativos e navegadores que usam regras de acesso condicional no Azure Active Directory

As regras de acesso condicional têm suporte em aplicativos conectados do Azure Active Directory, (Azure AD) aplicativos SaaS (software como serviço) federados pré-integrados, aplicativos que usam senha de logon único (SSO), aplicativos de linha de negócios e aplicativos que usam o Proxy de Aplicativo Azure AD. Para obter uma lista detalhada dos aplicativos para os quais você pode habilitar o acesso condicional, veja [Serviços habilitados com acesso condicional](active-directory-conditional-access-technical-reference.md). O acesso condicional funciona com os aplicativos móveis e da área de trabalho que usam autenticação moderna. Neste artigo, abordaremos o funcionamento do acesso condicional em aplicativos móveis e de área de trabalho.

Você pode usar páginas de entrada do Azure AD em aplicativos que usam autenticação moderna. Com uma página de logon, a autenticação multifator é solicitada de um usuário. Se o acesso do usuário estiver bloqueado, será mostrada uma mensagem. A autenticação moderna é necessária para que o dispositivo se autentique no Azure AD para que políticas de acesso condicional com base no dispositivo sejam avaliadas.

É importante saber quais aplicativos podem usar as regras de acesso condicional e as etapas que talvez você precise executar para proteger outros pontos de entrada do aplicativo.

## <a name="applications-that-use-modern-authentication"></a>Aplicativos que usam a autenticação moderna
> [!NOTE]
> Se você tiver uma política de acesso condicional no Azure AD com um equivalente no Office 365, configure duas políticas de acesso condicional. Isso se aplica, por exemplo, a políticas de acesso condicional para o Exchange Online ou o SharePoint Online.
>
>

Os aplicativos a seguir oferecem suporte ao acesso condicional para o Office 365 e outros aplicativos de serviço conectados ao Azure AD:


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
| Office 365 SharePoint Online| Windows 10| Aplicativos do Office 2016, aplicativos universais do Office, Office 2013 (com autenticação moderna), cliente de sincronização do OneDrive (veja as [observações](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e)), suporte aos Grupos do Office planejado para o futuro, suporte aos aplicativos do SharePoint planejado para o futuro|
| Office 365 SharePoint Online| Windows 8.1, Windows 7| Aplicativos do Office 2016, Office 2013 (com autenticação moderna), cliente de sincronização do OneDrive (veja as [observações](https://support.office.com/en-US/article/Azure-Active-Directory-conditional-access-with-the-OneDrive-sync-client-on-Windows-028d73d7-4b86-4ee0-8fb7-9a209434b04e))|
| Office 365 SharePoint Online| iOS, Android| Aplicativos móveis do Office|
| Office 365 SharePoint Online| Mac OS X| Office 2016 para macOS (somente Word, Excel, PowerPoint, OneNote). Suporte para OneDrive for Business planejado para o futuro|
| Office 365 Yammer| Windows 10, iOS, Android| Aplicativo Office Yammer|
| Serviço PowerBI| Windows 10, Windows 8.1, Windows 7 e iOS| Aplicativo PowerBI. Atualmente, o aplicativo Power BI para Android não dá suporte ao acesso condicional baseado no dispositivo.|
| Visual Studio Team Services| Windows 10, Windows 8.1, Windows 7, iOS e Android| Aplicativo Visual Studio Team Services|








## <a name="applications-that-do-not-use-modern-authentication"></a>Aplicativos que não usam autenticação moderna
Atualmente, você deve usar outros métodos para bloquear o acesso a aplicativos que não usam autenticação moderna. As regras de acesso para aplicativos que não usam a autenticação moderna não são impostas por acesso condicional. Isso é basicamente uma consideração para acesso ao Exchange e ao SharePoint. A maioria das versões anteriores de aplicativos usar protocolos antigos de controle de acesso.

### <a name="control-access-in-office-365-sharepoint-online"></a>Controlar o acesso no Office 365 SharePoint Online
Você pode desabilitar os protocolos herdados para o acesso ao SharePoint usando o cmdlet Set-SPOTenant. Use este cmdlet para impedir que os clientes do Office que usam os protocolos de autenticação não moderna acessem recursos do SharePoint Online.

**Exemplo de comando**: `Set-SPOTenant -LegacyAuthProtocolsEnabled $false`

### <a name="control-access-in-office-365-exchange-online"></a>Controlar o acesso no Office 365 Exchange Online
O Exchange oferece duas categorias principais de protocolos. Examine as opções a seguir e selecione a política ideal para sua organização.

* **Exchange ActiveSync**. Por padrão, as políticas de acesso condicional para a autenticação multifator e local não são impostas para o Exchange ActiveSync. Você precisa proteger o acesso a esses serviços, configurando a política do Exchange ActiveSync diretamente ou bloqueando o Exchange ActiveSync usando regras de Serviços de Federação do Active Directory (AD FS).
* **Protocolos herdados**. Você pode bloquear os protocolos herdados com o AD FS. Isso bloqueia o acesso para clientes mais antigos do Office, como o Office 2013 sem autenticação moderna habilitada e versões anteriores do Office.

### <a name="use-ad-fs-to-block-legacy-protocol"></a>Usar o AD FS para bloquear o protocolo legado
Você pode usar as regras de autorização de emissão de exemplo a seguir para bloquear o acesso de protocolo herdado no nível do AD FS. Escolha entre duas configurações comuns.

#### <a name="option-1-allow-exchange-activesync-and-allow-legacy-apps-but-only-on-the-intranet"></a>Opção 1: permitir o Exchange ActiveSync e só permitir aplicativos herdados, mas somente na intranet
Ao aplicar as três regras a seguir ao Objeto de Confiança de Terceira Parte Confiável do AD FS para a Plataforma de Identidade do Microsoft Office 365, o tráfego do Exchange ActiveSync e o tráfego de autenticação moderno e de navegador, têm acesso. Aplicativos herdados são bloqueados da extranet.

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
Ao aplicar as três regras a seguir ao Objeto de Confiança de Terceira Parte Confiável do AD FS para a Plataforma de Identidade do Microsoft Office 365, o tráfego do Exchange ActiveSync e o tráfego de autenticação moderno e de navegador, têm acesso. Aplicativos herdados são bloqueados de qualquer localização.

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

Você só pode obter acesso para políticas baseadas em dispositivo que verificam a conformidade do dispositivo e o ingresso no domínio quando o Azure AD puder identificar e autenticar o dispositivo. Enquanto a maioria das verificações, como de localização e MFA, funcionam na maioria dos dispositivos e navegadores, as políticas de dispositivo requerem a versão do sistema operacional e os navegadores listados abaixo. O acesso será bloqueado para usuários em navegadores ou sistemas operacionais sem suporte quando uma política de dispositivo estiver em vigor. 

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
> Para obter suporte do Chrome, você precisa estar usando a Atualização do Windows 10 para Criadores e instalar a extensão encontrada [aqui](https://chrome.google.com/webstore/detail/windows-10-accounts/ppnbnpeolgkicgegkbkbjmhlideopiji).
>
>

## <a name="next-steps"></a>Próximas etapas

Para obter mais detalhes, confira [Acesso condicional no Azure Active Directory](active-directory-conditional-access.md)




<!--Image references-->
[1]: ./media/active-directory-conditional-access-supported-apps/ic195031.png


