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
# <a name="silently-install-hello-azure-ad-application-proxy-connector"></a><span data-ttu-id="bc33e-103">Instalar silenciosamente Olá conector de Proxy de aplicativo do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="bc33e-103">Silently install hello Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="bc33e-104">Você deseja toobe toosend capaz de uma instalação de script toomultiple Windows servers ou tooWindows servidores que não têm a interface do usuário habilitado.</span><span class="sxs-lookup"><span data-stu-id="bc33e-104">You want toobe able toosend an installation script toomultiple Windows servers or tooWindows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="bc33e-105">Este tópico ajuda você a criar um script do Windows PowerShell que permite a instalação autônoma e registro para o Conector de Proxy de Aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc33e-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="bc33e-106">Esse recurso é útil quando você deseja:</span><span class="sxs-lookup"><span data-stu-id="bc33e-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="bc33e-107">Instale o conector de saudação em máquinas com nenhuma camada de interface do usuário ou computador de toohello RDP não é possível.</span><span class="sxs-lookup"><span data-stu-id="bc33e-107">Install hello connector on machines with no UI layer or when you cannot RDP toohello machine.</span></span>
* <span data-ttu-id="bc33e-108">Instalar e registrar vários conectores ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="bc33e-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="bc33e-109">Integração de instalação do conector hello e registro como parte de outro procedimento.</span><span class="sxs-lookup"><span data-stu-id="bc33e-109">Integrate hello connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="bc33e-110">Crie uma imagem de servidor padrão que contém Olá conector bits, mas não está registrada.</span><span class="sxs-lookup"><span data-stu-id="bc33e-110">Create a standard server image that contains hello connector bits but is not registered.</span></span>

<span data-ttu-id="bc33e-111">Proxy de aplicativo funciona, instalando um serviço do Windows Server slim chamado hello conector dentro de sua rede.</span><span class="sxs-lookup"><span data-stu-id="bc33e-111">Application Proxy works by installing a slim Windows Server service called hello Connector inside your network.</span></span> <span data-ttu-id="bc33e-112">Para toowork do conector de Proxy de aplicativo hello, ele tem toobe registrado com seu diretório do AD do Azure usando um administrador global e uma senha.</span><span class="sxs-lookup"><span data-stu-id="bc33e-112">For hello Application Proxy Connector toowork it has toobe registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="bc33e-113">Normalmente, essa informação é inserida durante a instalação do Conector em uma caixa de diálogo pop-up.</span><span class="sxs-lookup"><span data-stu-id="bc33e-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="bc33e-114">No entanto, você pode usar o Windows PowerShell toocreate um tooenter de objeto de credencial suas informações de registro.</span><span class="sxs-lookup"><span data-stu-id="bc33e-114">However, you can use Windows PowerShell toocreate a credential object tooenter your registration information.</span></span> <span data-ttu-id="bc33e-115">Ou você pode criar seu próprio token e usá-lo tooenter suas informações de registro.</span><span class="sxs-lookup"><span data-stu-id="bc33e-115">Or you can create your own token and use it tooenter your registration information.</span></span>

## <a name="install-hello-connector"></a><span data-ttu-id="bc33e-116">Instalar o conector Olá</span><span class="sxs-lookup"><span data-stu-id="bc33e-116">Install hello connector</span></span>
<span data-ttu-id="bc33e-117">Instale Olá conector MSIs sem registrar o conector de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="bc33e-117">Install hello Connector MSIs without registering hello Connector as follows:</span></span>

1. <span data-ttu-id="bc33e-118">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="bc33e-118">Open a command prompt.</span></span>
2. <span data-ttu-id="bc33e-119">Executar Olá na qual Olá /q significa instalação silenciosa do comando a seguir - Olá instalação não solicita Olá tooaccept contrato de licença de usuário final.</span><span class="sxs-lookup"><span data-stu-id="bc33e-119">Run hello following command in which hello /q means quiet installation - hello installation doesn't prompt you tooaccept hello End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-hello-connector-with-azure-ad"></a><span data-ttu-id="bc33e-120">Registrar o conector de saudação com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="bc33e-120">Register hello connector with Azure AD</span></span>
<span data-ttu-id="bc33e-121">Há dois métodos que você pode usar o conector de saudação tooregister:</span><span class="sxs-lookup"><span data-stu-id="bc33e-121">There are two methods you can use tooregister hello connector:</span></span>

* <span data-ttu-id="bc33e-122">Registrar o conector hello usando um objeto de credencial do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc33e-122">Register hello connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="bc33e-123">Registrar o conector hello usando um token criado offline</span><span class="sxs-lookup"><span data-stu-id="bc33e-123">Register hello connector using a token created offline</span></span>

### <a name="register-hello-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="bc33e-124">Registrar o conector hello usando um objeto de credencial do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc33e-124">Register hello connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="bc33e-125">Crie objeto de credenciais do Windows PowerShell Olá executando este comando.</span><span class="sxs-lookup"><span data-stu-id="bc33e-125">Create hello Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="bc33e-126">Substituir  *\<username\>*  e  *\<senha\>*  com hello nome de usuário e senha para seu diretório:</span><span class="sxs-lookup"><span data-stu-id="bc33e-126">Replace *\<username\>* and *\<password\>* with hello username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="bc33e-127">Vá muito**conector de Proxy de aplicativo C:\Program Files\Microsoft AAD** e executar script hello usando Olá PowerShell credenciais objeto criado por você.</span><span class="sxs-lookup"><span data-stu-id="bc33e-127">Go too**C:\Program Files\Microsoft AAD App Proxy Connector** and run hello script using hello PowerShell credentials object you created.</span></span> <span data-ttu-id="bc33e-128">Substituir *$cred* com nome Olá Olá PowerShell credenciais objeto criado:</span><span class="sxs-lookup"><span data-stu-id="bc33e-128">Replace *$cred* with hello name of hello PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-hello-connector-using-a-token-created-offline"></a><span data-ttu-id="bc33e-129">Registrar o conector hello usando um token criado offline</span><span class="sxs-lookup"><span data-stu-id="bc33e-129">Register hello connector using a token created offline</span></span>
1. <span data-ttu-id="bc33e-130">Crie um token offline usando Olá AuthenticationContext classe usando valores hello no trecho de código hello:</span><span class="sxs-lookup"><span data-stu-id="bc33e-130">Create an offline token using hello AuthenticationContext class using hello values in hello code snippet:</span></span>

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


2. <span data-ttu-id="bc33e-131">Uma vez que o token Olá, crie uma SecureString usando Olá token:</span><span class="sxs-lookup"><span data-stu-id="bc33e-131">Once you have hello token, create a SecureString using hello token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="bc33e-132">Olá executar comando do Windows PowerShell a seguir, substituindo \<GUID de locatário\> com sua ID de diretório:</span><span class="sxs-lookup"><span data-stu-id="bc33e-132">Run hello following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="bc33e-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bc33e-133">Next steps</span></span> 
* [<span data-ttu-id="bc33e-134">Publicar aplicativos usando seu próprio nome de domínio</span><span class="sxs-lookup"><span data-stu-id="bc33e-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="bc33e-135">Habilitar o logon único</span><span class="sxs-lookup"><span data-stu-id="bc33e-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="bc33e-136">Solucionar problemas que surgirem com o Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="bc33e-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


