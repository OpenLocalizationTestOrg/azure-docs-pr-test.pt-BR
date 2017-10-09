---
title: aaaSilent instalar o conector de Proxy de aplicativo do Azure AD | Microsoft Docs
description: "Aborda como tooperform uma instalação autônoma do conector de Proxy de aplicativo do AD do Azure tooprovide acesso remoto seguro tooyour local aplicativos."
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3aa1c7f2-fb2a-4693-abd5-95bb53700cbb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: ce796ff45a65ba7d5f0f63c02085bdc6af494548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a>Instalar silenciosamente Olá conector de Proxy de aplicativo do AD do Azure
Você deseja toobe toosend capaz de uma instalação de script toomultiple Windows servers ou tooWindows servidores que não têm a interface do usuário habilitado. Este tópico ajuda você a criar um script do Windows PowerShell que permite a instalação autônoma e registro para o Conector de Proxy de Aplicativo do Azure AD.

Esse recurso é útil quando você deseja:

* Instale o conector de saudação em máquinas com nenhuma camada de interface do usuário ou computador de toohello RDP não é possível.
* Instalar e registrar vários conectores ao mesmo tempo.
* Integração de instalação do conector hello e registro como parte de outro procedimento.
* Crie uma imagem de servidor padrão que contém Olá conector bits, mas não está registrada.

Proxy de aplicativo funciona, instalando um serviço do Windows Server slim chamado hello conector dentro de sua rede. Para toowork do conector de Proxy de aplicativo hello, ele tem toobe registrado com seu diretório do AD do Azure usando um administrador global e uma senha. Normalmente, essa informação é inserida durante a instalação do Conector em uma caixa de diálogo pop-up. No entanto, você pode usar o Windows PowerShell toocreate um tooenter de objeto de credencial suas informações de registro. Ou você pode criar seu próprio token e usá-lo tooenter suas informações de registro.

## <a name="install-hello-connector"></a>Instalar o conector Olá
Instale Olá conector MSIs sem registrar o conector de saudação da seguinte maneira:

1. Abra um prompt de comando.
2. Executar Olá na qual Olá /q significa instalação silenciosa do comando a seguir - Olá instalação não solicita Olá tooaccept contrato de licença de usuário final.
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a>Registrar o conector de saudação com o Azure AD
Há dois métodos que você pode usar o conector de saudação tooregister:

* Registrar o conector hello usando um objeto de credencial do Windows PowerShell
* Registrar o conector hello usando um token criado offline

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a>Registrar o conector hello usando um objeto de credencial do Windows PowerShell
1. Crie objeto de credenciais do Windows PowerShell Olá executando este comando. Substituir  *\<username\>*  e  *\<senha\>*  com hello nome de usuário e senha para seu diretório:
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. Vá muito**conector de Proxy de aplicativo C:\Program Files\Microsoft AAD** e executar script hello usando Olá PowerShell credenciais objeto criado por você. Substituir *$cred* com nome Olá Olá PowerShell credenciais objeto criado:
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a>Registrar o conector hello usando um token criado offline
1. Crie um token offline usando Olá AuthenticationContext classe usando valores hello no trecho de código hello:

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// hello AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// hello application ID of hello connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// hello reply address of hello connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// hello AppIdUri of hello registration service in AAD
        /// </summary>
        static readonly Uri RegistrationServiceAppIdUri = new Uri("https://proxy.cloudwebappproxy.net/registerapp");

        #endregion

        #region private members
        private string token;
        private string tenantID;
        #endregion

        public void GetAuthenticationToken()
        {
            AuthenticationContext authContext = new AuthenticationContext(AadAuthenticationEndpoint.AbsoluteUri);

            AuthenticationResult authResult = authContext.AcquireToken(RegistrationServiceAppIdUri.AbsoluteUri,
                ConnectorAppId,
                ConnectorRedirectAddress,
                PromptBehavior.Always);

            if (authResult == null || string.IsNullOrEmpty(authResult.AccessToken) || string.IsNullOrEmpty(authResult.TenantId))
            {
                Trace.TraceError("Authentication result, token or tenant id returned are null");
                throw new InvalidOperationException("Authentication result, token or tenant id returned are null");
            }

            token = authResult.AccessToken;
            tenantID = authResult.TenantId;
        }


2. Uma vez que o token Olá, crie uma SecureString usando Olá token:

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. Olá executar comando do Windows PowerShell a seguir, substituindo \<GUID de locatário\> com sua ID de diretório:

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a>Próximas etapas 
* [Publicar aplicativos usando seu próprio nome de domínio](active-directory-application-proxy-custom-domains.md)
* [Habilitar o logon único](active-directory-application-proxy-sso-using-kcd.md)
* [Solucionar problemas que surgirem com o Proxy de Aplicativo](active-directory-application-proxy-troubleshoot.md)


