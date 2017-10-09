---
title: "Aplicativos, permissões e consentimento no Azure Active Directory. | Microsoft Docs"
description: "O Azure AD Connect integrará seus diretórios locais com o Azure Active Directory.  Isso permite que você tooprovide uma identidade comum para aplicativos do Office 365, Azure e SaaS integrada ao AD do Azure."
keywords: "Introdução tooAzure AD, aplicativos, o que é o Azure AD Connect, instalar o active directory"
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: 
ms.assetid: 25897cc4-7687-49b6-b0d5-71f51302b6b1
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/31/2017
ms.author: billmath
ms.reviewer: jesakowi
ms.custom: oldportal;it-pro;
ms.openlocfilehash: af0c2669199736fdb41e85876a7e3a7064e80770
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="apps-permissions-and-consent-in-azure-active-directory"></a>Aplicativos, permissões e consentimento no Azure Active Directory
No Active Directory do Azure, você pode adicionar o diretório tooyour de aplicativos.  aplicativos de saudação podem variar dependendo do tipo de saudação do aplicativo.  aplicativos tooview no portal clássico do hello, selecione um diretório e escolher aplicativos.

![](media/active-directory-apps-permissions-consent/apps1.png)

> [!IMPORTANT]
> A Microsoft recomenda que você gerencie o AD do Azure usando Olá [Centro de administração do AD do Azure](https://aad.portal.azure.com) em Olá portal do Azure em vez de usar Olá portal clássico do Azure mencionado neste artigo.

## <a name="types-of-apps"></a>Tipos de aplicativos

1. **Aplicativos de locatário único** </br>
    - **Aplicativos de único locatário** -conhecida tooas aplicativos de linha de negócios (LOB). Esse é Olá caso em que alguém de sua organização desenvolve seu próprio aplicativo e gostaria que os usuários na organização Olá toosign capaz de toobe no aplicativo toohello.
    ![](media/active-directory-apps-permissions-consent/apps2.png)
    - **Aplicativos de Proxy de aplicativo** - quando você expõe um aplicativo local com o Proxy de aplicativo do AD do Azure, um aplicativo de único locatário é registrado no seu locatário (em adição toohello serviço de Proxy de aplicativo). Este aplicativo é o que representa seu aplicativo local para todas as interações de nuvem (por exemplo, autenticação). (O proxy de aplicativo requer o Azure AD Básico ou superior.)


2. **Aplicativos multilocatário**
    - **Aplicativos de vários locatários que outras pessoas possam consentir** - semelhante muito "aplicativos de único locatário que desenvolve sua organização". a principal diferença Hello (além de lógica de saudação no próprio aplicativo hello) é que os usuários de outros locatários também podem dar consentimento tooand toohello aplicativo de entrada.</br>
    ![](media/active-directory-apps-permissions-consent/apps4.png)
    - **Aplicativos multilocatário desenvolvidos por outros, para os quais a Contoso pode dar consentimento**. (Ou "aplicativos com consentimento" de forma abreviada). Isso é Olá outro lado de "aplicativos multilocatários que sua organização desenvolve". Quando outra organização desenvolve um aplicativo multilocatário, os usuários da sua organização podem consentir toohello aplicativo e entrar tooit.
    - **Aplicativos próprios da Microsoft** – aplicativos que representam os serviços da Microsoft. Autorização é orientada por fatos Olá que você se inscrever para o serviço de saudação. Às vezes, há especial UX e lógica para determinados aplicativos de terceiros que é frequentemente usada ao estabelecer políticas de acesso toohello aplicativo.</br>
    ![](media/active-directory-apps-permissions-consent/apps3.png)
    - **Aplicativos pré-integrados** -aplicativos disponíveis no hello Galeria de aplicativo do Azure AD, você pode adicionar tooyour directory tooprovide single sign-on (e, em alguns casos, o provisionamento) toopopular aplicativos de SaaS.
    - **Logon único do Azure AD**: SSO "Real", para aplicativos que podem ser integrados ao Azure AD por meio de um protocolo de entrada com suporte como SAML 2.0 ou OpenID Connect. Olá assistente o guiará através de configurá-la.
    - **Logon único senha**: AD do Azure armazena com segurança as credenciais do usuário Olá para o aplicativo hello e credenciais Olá são "injetadas" formulário de entrada hello por Olá extensão de navegador de acesso do aplicativo do Azure AD. Também conhecido como "cofre para senhas".

## <a name="permissions"></a>Permissões

Quando um aplicativo é registrado, o usuário de saudação realizar o registro do aplicativo hello (ou seja, o desenvolvedor de saudação) define qual aplicativo de saudação permissões precisa acessar e quais recursos. (recursos de saudação são, por conta própria, definido como outros aplicativos). Por exemplo, alguém criar um aplicativo de leitor de email, seria estado que seu aplicativo requer a permissão de "Caixas de correio acesso como usuário conectado hello" hello em hello "Office 365 Exchange Online" recurso:
    
![](media/active-directory-apps-permissions-consent/apps6.png)

Em ordem para toorequest (cliente de saudação) de um aplicativo determinada permissão de outro aplicativo (recurso de saudação), desenvolvedor de saudação do aplicativo de recurso Olá define permissões de saudação que existem. Em nosso exemplo, a Microsoft, o proprietário de saudação do aplicativo de recurso "Office 365 Exchange Online" Olá, definiu uma permissão denominada "Caixas de correio acesso como usuário conectado Olá".

Ao definir permissões, o desenvolvedor do aplicativo hello deve definir se Olá permissão pode ser consentida, ou se ele requer o consentimento do administrador. Isso permite que desenvolvedores tooallow tooconsent de usuários em seus próprios tooapps solicitando somente permissões de baixa confidencialidade, mas requer administradores tooconsent toomore confidenciais permissões. Por exemplo, Olá "Active Directory do Azure" aplicativo de recurso, tiver sido definida, para que os usuários podem dar consentimento tooapps, solicitando permissões somente leitura limitadas.  No entanto, o consentimento do administrador é necessário para permissões de leitura completas e todas as permissões de gravação.

Como clientes nativos não são autenticados, um aplicativo definido como um aplicativo cliente nativo somente pode solicitar permissões delegadas. Isso significa que sempre deve haver um usuário real envolvido ao obter um token. Aplicativos Web e APIs Web (clientes confidenciais) devem sempre ser autenticados com o Azure AD ao obter um token de acesso. Que significa que eles também têm a possibilidade de saudação do solicitando permissões somente de aplicativo. Por exemplo, se o serviço de back-end do tooauthenticate tooanother precisa de um serviço de back-end. Aplicativos solicitando permissões somente do aplicativo sempre exigem o consentimento do administrador.

Resumindo:



- Um aplicativo (cliente) informa Olá permissões para outros aplicativos (recursos).
- Um aplicativo (recurso) informa quais permissões são expostos tooother aplicativos (clientes).
- Uma permissão pode ser uma permissão somente de aplicativo ou uma permissão delegada.
- Uma permissão delegada pode ser marcada como "permite o consentimento do usuário" ou "requer o consentimento do administrador".
- Um aplicativo pode se comportar como um cliente (declarando que precisa de recursos de tooa permissões), como um recurso (declarando quais permissões expõe), ou ambos.

## <a name="controls"></a>Controles

a seguir Olá é uma lista de controles de administrador diferentes Olá disponíveis para todos os esse comportamento. Olá administrador controles podem ser acessados no portal clássico do hello de configurar no diretório de saudação.

![](media/active-directory-apps-permissions-consent/apps7.png)

Em hello Azure portal em **gerenciar**, **as configurações de usuário**.

![](media/active-directory-apps-permissions-consent/apps11.png)



- Você pode controlar se os usuários podem dar consentimento tooapps:

No portal clássico do hello, selecione **usuários podem resultar em aplicativos permissões tooaccess seus dados.**
![](media/active-directory-apps-permissions-consent/apps8.png)

No portal do Azure de Olá, selecione **usuários podem permitir que aplicativos tooaccess seus dados**.
![](media/active-directory-apps-permissions-consent/apps12.png)



- Você pode controlar se os usuários podem registrar seus próprios aplicativos de LOB único locatário: em select portal clássico do hello **os usuários podem adicionar aplicativos integrados.**
![](media/active-directory-apps-permissions-consent/apps9.png)

No portal do Azure de Olá, selecione **usuários podem permitir que aplicativos tooaccess seus dados**.
![](media/active-directory-apps-permissions-consent/apps13.png)

>[!NOTE]
>Mesmo se você permitir aos usuários aplicativos LOB tooregister único locatário, há limites toowhat pode ser registrado.  
>Por exemplo, os desenvolvedores que não são administradores de diretório.
>
>- Os usuários não podem transformar um aplicativo de locatário único em um aplicativo multilocatário.
>- Ao registrar os aplicativos LOB único locatário, os usuários não podem solicitar permissões somente de aplicativo tooother aplicativos.
>- Ao registrar os aplicativos LOB único locatário, os usuários não podem solicitar permissões delegadas tooother aplicativos se essas permissões exigem consentimento do administrador.
>- Os usuários não podem fazer tooapps alterações que não são proprietários do.



- Você pode controlar se os usuários podem ou não adicionar por conta própria aplicativos pré-integrados que usam o SSO de senha (também conhecido como "cofre para senhas") ![](media/active-directory-apps-permissions-consent/apps10.png)



- Você pode controlar as condições sob as quais aplicativos podem ser acessados (ou seja, acesso condicional). Lembre-se de que isso se aplica a toohello aplicativo de cliente e o aplicativo de recurso toohello. Portanto, digamos que você definir uma política de acesso condicional que afirma que o aplicativo hello "Office 365 Exchange Online" só pode ser acessado de computadores, que são compatíveis.  Essa política também será iniciada quando um usuário tenta toouse um aplicativo cliente que solicita permissões tooExchange on-line.



- Você tem visibilidade no qual aplicativos foram consentido tooand quais estão sendo usados.

1.  Quando um usuário consente tooan aplicativo um objeto ServicePrincipal é criado no locatário hello. Criação de ServicePrincipal é incluída no relatório de auditoria de saudação.
2.  Relatórios de atividade de entrada do usuário dizer qual usuário do aplicativo hello está tentando entrar. 

## <a name="example"></a>Exemplo

Por exemplo, vamos hello "FabrikamMail para o Office 365" aplicativo, que você tenha percebido usuários em seu locatário estão tentando entrar. "FabrikamMail" é um aplicativo de leitor de email para o Android, publicado pela "Fabrikam, Inc.". Isso se encaixa hello "aplicativos multilocatários outros desenvolver, que a Contoso pode consentir".

Se os usuários têm permissão tooconsent, recebem uma saudação de prompt de consentimento primeira vez que entrar no:![](media/active-directory-apps-permissions-consent/apps14.png)

"Acessar suas caixas de correio" é a cadeia de caracteres do hello voltado ao usuário autorização para permissão de "Acesso as caixas de correio como usuário conectado hello" hello exposto por "Office 365 Exchange Online" (ou seja, Exchange).

Você pode ver permissões Olá procurando objeto ServicePrincipal de saudação do Exchange (recurso de saudação), que foi adicionado ao se inscrever para o Office 365. Você pode pensar no objeto ServicePrincipal de saudação de uma "instância" do aplicativo hello em seu locatário, que é usado para gravar as configurações e opções diferentes.  Você pode ver isso usando Olá `Get-AzureADServicePrincipal` no PowerShell.

    PS C:\> Get-AzureADServicePrincipal -ObjectId 383f7b97-6754-4d3d-9474-3908ebcba1c6 | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : Office 365 Exchange Online
    AppId                     : 00000002-0000-0ff1-ce00-000000000000
    AppOwnerTenantId          : 
    AppRoleAssignmentRequired : False
    AppRoles                  : {...}
    DisplayName               : Microsoft.Exchange
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {...
                                , class OAuth2Permission {
                                  AdminConsentDescription : Allows hello app toohave hello same access toomailboxes as hello signed-in user via Exchange Web Services.
                                  AdminConsentDisplayName : Access mailboxes as hello signed-in user via Exchange Web Services
                                  Id                      : 3b5f3d61-589b-4a3c-a359-5dd4b5ee5bd5
                                  IsEnabled               : True
                                  Type                    : User
                                  UserConsentDescription  : Allows hello app full access tooyour mailboxes on your behalf.
                                  UserConsentDisplayName  : Access your mailboxes
                                  Value                   : full_access_as_user
                                },
                                ...}
    PasswordCredentials       : {}
    PublisherName             : 
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {00000002-0000-0ff1-ce00-000000000000/outlook.office365.com, 00000002-0000-0ff1-ce00-000000000000/mail.office365.com, 00000002-0000-0ff1-ce00-000000000000/outlook.com, 
                                00000002-0000-0ff1-ce00-000000000000/*.outlook.com...}
    Tags                      : {}

Consentimento é iniciado quando o usuário Olá clicar em "Aceitar". Primeiro, um objeto ServicePrincipal para "FabrikamMail para o Office 365" é criado no locatário hello. Olá ServicePrincipal parecida com esta:

    PS C:\> Get-AzureADServicePrincipal -SearchString "FabrikamMail for Office 365" | fl *
    
    DeletionTimeStamp         : 
    ObjectId                  : a8b16333-851d-42e8-acd2-eac155849b37
    ObjectType                : ServicePrincipal
    AccountEnabled            : True
    AppDisplayName            : FabrikamMail for Office 365
    AppId                     : aba7c072-2267-4031-8960-e7a2db6e0590
    AppOwnerTenantId          : 4a4076e0-a70f-41c6-b819-6f9c4a86df89
    AppRoleAssignmentRequired : False
    AppRoles                  : {}
    DisplayName               : FabrikamMail for Office 365
    ErrorUrl                  : 
    Homepage                  : 
    KeyCredentials            : {}
    LogoutUrl                 : 
    Oauth2Permissions         : {}
    PasswordCredentials       : {}
    PublisherName             : Fabrikam, Inc.
    ReplyUrl                  : 
    SamlMetadataUrl           : 
    ServicePrincipalNames     : {aba7c072-2267-4031-8960-e7a2db6e0590}
    Tags                      : {WindowsAzureActiveDirectoryIntegratedApp}

Consentimento tooan aplicativo cria um link de Oauth2PermissionGrant entre seguinte hello:
  
- objeto de usuário Olá
- aplicativos de cliente Olá ServicePrincipalName (SPN)
- aplicativos de recurso Olá ServicePrincipalName (SPN)
- permissões no aplicativo de recurso de saudação.  

No caso de saudação de FabrikamMail, parece que algo assim:

    PS C:\> Get-AzureADUserOAuth2PermissionGrant -ObjectId ddiggle@aadpremiumlab.onmicrosoft.com | fl *
    
    ClientId    : a8b16333-851d-42e8-acd2-eac155849b37
    ConsentType : Principal
    ExpiryTime  : 05/15/2017 07:02:39 AM
    ObjectId    : M2OxqB2F6EKs0urBVYSbN5d7PzhUZz1NlH25COvLocbJjoxkUFfRQauryBKwBWet
    PrincipalId : 648c8ec9-5750-41d1-abab-c812b00567ad
    ResourceId  : 383f7b97-6754-4d3d-9474-3908ebcba1c6
    Scope       : full_access_as_user
    StartTime   : 01/01/0001 12:00:00 AM

(**ClientId** é a ID de objeto principal de serviço do FabrikamMail (Olá que foi criada apenas), **PrincipalId** é a ID de objeto de usuário hello (saudação do usuário do que consentimento), **ResourceId**é o serviço do Exchange ID de objeto principal, o escopo é a permissão de saudação do Exchange foi consentimento).

Se os usuários não são permitidos tooconsent, eles verão uma tela que diz que essa permissão é necessária.

