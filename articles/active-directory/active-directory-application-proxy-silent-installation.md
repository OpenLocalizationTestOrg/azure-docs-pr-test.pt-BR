---
title: "Instalação silenciosa do conector de Proxy do Aplicativo Azure AD | Microsoft Docs"
description: "Aborda como realizar a instalação autônoma do Conector de roxy de Aplicativo do Azure AD para fornecer acesso remoto seguro aos seus aplicativos locais."
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
ms.openlocfilehash: 9e28c89d8f64f0ae3d4150017ca544e606075c45
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="silently-install-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="e741d-103">Faça uma instalação silenciosa do Conector de Proxy de Aplicativo do Azure AD</span><span class="sxs-lookup"><span data-stu-id="e741d-103">Silently install the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="e741d-104">Você deseja conseguir enviar um script de instalação para vários servidores do Windows ou para os servidores do Windows que não têm uma interface de usuário ativada.</span><span class="sxs-lookup"><span data-stu-id="e741d-104">You want to be able to send an installation script to multiple Windows servers or to Windows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="e741d-105">Este tópico ajuda você a criar um script do Windows PowerShell que permite a instalação autônoma e registro para o Conector de Proxy de Aplicativo do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="e741d-105">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="e741d-106">Esse recurso é útil quando você deseja:</span><span class="sxs-lookup"><span data-stu-id="e741d-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="e741d-107">Instale o conector em máquinas que não possuam camada de interface do usuário ou quando você não puder realizar o RDP na máquina.</span><span class="sxs-lookup"><span data-stu-id="e741d-107">Install the connector on machines with no UI layer or when you cannot RDP to the machine.</span></span>
* <span data-ttu-id="e741d-108">Instalar e registrar vários conectores ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="e741d-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="e741d-109">Integrar a instalação e o registro do conector como parte de outro procedimento.</span><span class="sxs-lookup"><span data-stu-id="e741d-109">Integrate the connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="e741d-110">Criar uma imagem de servidor padrão que contém bits do conector, mas que não está registrada.</span><span class="sxs-lookup"><span data-stu-id="e741d-110">Create a standard server image that contains the connector bits but is not registered.</span></span>

<span data-ttu-id="e741d-111">O Proxy de Aplicativo funciona por meio da instalação de um serviço leve do Windows Server chamado Conector dentro de sua rede.</span><span class="sxs-lookup"><span data-stu-id="e741d-111">Application Proxy works by installing a slim Windows Server service called the Connector inside your network.</span></span> <span data-ttu-id="e741d-112">Para o Conector do proxy de aplicativo funcionar, ele deve ser registrado com o diretório do Azure AD usando uma senha e um administrador global.</span><span class="sxs-lookup"><span data-stu-id="e741d-112">For the Application Proxy Connector to work it has to be registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="e741d-113">Normalmente, essa informação é inserida durante a instalação do Conector em uma caixa de diálogo pop-up.</span><span class="sxs-lookup"><span data-stu-id="e741d-113">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="e741d-114">No entanto, você pode usar o Windows PowerShell para criar um objeto de credencial para inserir suas informações de registro.</span><span class="sxs-lookup"><span data-stu-id="e741d-114">However, you can use Windows PowerShell to create a credential object to enter your registration information.</span></span> <span data-ttu-id="e741d-115">Ou você pode criar seu próprio token e usá-lo para inserir suas informações de registro.</span><span class="sxs-lookup"><span data-stu-id="e741d-115">Or you can create your own token and use it to enter your registration information.</span></span>

## <a name="install-the-connector"></a><span data-ttu-id="e741d-116">Instalar o conector</span><span class="sxs-lookup"><span data-stu-id="e741d-116">Install the connector</span></span>
<span data-ttu-id="e741d-117">Instale o MSIs do Conector sem registrar o Conector, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="e741d-117">Install the Connector MSIs without registering the Connector as follows:</span></span>

1. <span data-ttu-id="e741d-118">Abra um prompt de comando.</span><span class="sxs-lookup"><span data-stu-id="e741d-118">Open a command prompt.</span></span>
2. <span data-ttu-id="e741d-119">Execute o seguinte comando no qual /q significa instalação silenciosa – a instalação não solicita que você aceite os termos de licença.</span><span class="sxs-lookup"><span data-stu-id="e741d-119">Run the following command in which the /q means quiet installation - the installation doesn't prompt you to accept the End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-the-connector-with-azure-ad"></a><span data-ttu-id="e741d-120">Registrar o conector com o Azure AD</span><span class="sxs-lookup"><span data-stu-id="e741d-120">Register the connector with Azure AD</span></span>
<span data-ttu-id="e741d-121">Há dois métodos que você pode usar para registrar o conector:</span><span class="sxs-lookup"><span data-stu-id="e741d-121">There are two methods you can use to register the connector:</span></span>

* <span data-ttu-id="e741d-122">Registrar o conector usando um objeto de credencial do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e741d-122">Register the connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="e741d-123">Registrar o conector usando um token criado offline</span><span class="sxs-lookup"><span data-stu-id="e741d-123">Register the connector using a token created offline</span></span>

### <a name="register-the-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="e741d-124">Registrar o conector usando um objeto de credencial do Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="e741d-124">Register the connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="e741d-125">Crie o objeto de Credenciais do Windows PowerShell executando este comando.</span><span class="sxs-lookup"><span data-stu-id="e741d-125">Create the Windows PowerShell Credentials object by running this command.</span></span> <span data-ttu-id="e741d-126">Substitua *\<nome de usuário\>* e *\<senha\>* pelo nome de usuário e a senha para seu diretório:</span><span class="sxs-lookup"><span data-stu-id="e741d-126">Replace *\<username\>* and *\<password\>* with the username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="e741d-127">Vá para **C:\Program Files\Microsoft AAD App Proxy Connector** e execute o script usando o objeto de credenciais do PowerShell criado.</span><span class="sxs-lookup"><span data-stu-id="e741d-127">Go to **C:\Program Files\Microsoft AAD App Proxy Connector** and run the script using the PowerShell credentials object you created.</span></span> <span data-ttu-id="e741d-128">Substitua *$cred* pelo nome do objeto de credenciais do PowerShell criado:</span><span class="sxs-lookup"><span data-stu-id="e741d-128">Replace *$cred* with the name of the PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-the-connector-using-a-token-created-offline"></a><span data-ttu-id="e741d-129">Registrar o conector usando um token criado offline</span><span class="sxs-lookup"><span data-stu-id="e741d-129">Register the connector using a token created offline</span></span>
1. <span data-ttu-id="e741d-130">Crie um token offline usando a classe AuthenticationContext, com os valores no trecho de código:</span><span class="sxs-lookup"><span data-stu-id="e741d-130">Create an offline token using the AuthenticationContext class using the values in the code snippet:</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// The AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// The application ID of the connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// The reply address of the connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// The AppIdUri of the registration service in AAD
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


2. <span data-ttu-id="e741d-131">Quando tiver o token, crie uma SecureString usando o token:</span><span class="sxs-lookup"><span data-stu-id="e741d-131">Once you have the token, create a SecureString using the token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="e741d-132">Execute o seguinte comando do Windows PowerShell, substituindo \<GUID de locatário\> com sua ID de diretório:</span><span class="sxs-lookup"><span data-stu-id="e741d-132">Run the following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="e741d-133">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e741d-133">Next steps</span></span> 
* [<span data-ttu-id="e741d-134">Publicar aplicativos usando seu próprio nome de domínio</span><span class="sxs-lookup"><span data-stu-id="e741d-134">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="e741d-135">Habilitar o logon único</span><span class="sxs-lookup"><span data-stu-id="e741d-135">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="e741d-136">Solucionar problemas que surgirem com o Proxy de Aplicativo</span><span class="sxs-lookup"><span data-stu-id="e741d-136">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


