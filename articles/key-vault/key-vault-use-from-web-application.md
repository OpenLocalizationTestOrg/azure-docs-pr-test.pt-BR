---
title: Cofre de chaves do Azure de um aplicativo Web de aaaUse | Microsoft Docs
description: "Use este toohelp tutorial você aprenderá como toouse chave do Azure Cofre de um aplicativo web."
services: key-vault
documentationcenter: 
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: d5e2299e60b379c4e234d5cd6be03411c5a5c958
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="c9e55-103">Usar cofre da chave do Azure em um aplicativo Web</span><span class="sxs-lookup"><span data-stu-id="c9e55-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="c9e55-104">Introdução</span><span class="sxs-lookup"><span data-stu-id="c9e55-104">Introduction</span></span>
<span data-ttu-id="c9e55-105">Use este toohelp tutorial você aprenderá como toouse chave do Azure Cofre de um aplicativo web no Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e55-105">Use this tutorial toohelp you learn how toouse Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="c9e55-106">Orienta você pelo processo de saudação de acessar um segredo de um cofre de chaves do Azure para que ele pode ser usado em seu aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="c9e55-106">It walks you through hello process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="c9e55-107">**Estimado tempo toocomplete:** 15 minutos</span><span class="sxs-lookup"><span data-stu-id="c9e55-107">**Estimated time toocomplete:** 15 minutes</span></span>

<span data-ttu-id="c9e55-108">Para obter informações gerais sobre o Cofre da Chave do Azure, consulte [O que é o Cofre da Chave do Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="c9e55-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c9e55-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c9e55-109">Prerequisites</span></span>
<span data-ttu-id="c9e55-110">toocomplete neste tutorial, você deve ter Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9e55-110">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="c9e55-111">Um segredo de tooa URI em um cofre de chaves do Azure</span><span class="sxs-lookup"><span data-stu-id="c9e55-111">A URI tooa secret in an Azure Key Vault</span></span>
* <span data-ttu-id="c9e55-112">Uma ID de cliente e um segredo do cliente para um aplicativo web registrado com o Active Directory do Azure que tenha acesso tooyour Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="c9e55-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access tooyour Key Vault</span></span>
* <span data-ttu-id="c9e55-113">Um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="c9e55-113">A web application.</span></span> <span data-ttu-id="c9e55-114">Estamos será mostrando etapas Olá para um aplicativo ASP.NET MVC implantado no Azure como um aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="c9e55-114">We will be showing hello steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="c9e55-115">É essencial que você tenha concluído as etapas de saudação listadas na [Introdução ao Azure Key Vault](key-vault-get-started.md) para este tutorial para que você tenha hello segredo do URI tooa e hello ID do cliente e segredo do cliente para um aplicativo web.</span><span class="sxs-lookup"><span data-stu-id="c9e55-115">It is essential that you have completed hello steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have hello URI tooa secret and hello Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="c9e55-116">aplicativo web Hello que acessarão Olá Cofre de chaves é hello um que é registrado no Active Directory do Azure e tem acesso tooyour Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c9e55-116">hello web application that will be accessing hello Key Vault is hello one that is registered in Azure Active Directory and has been given access tooyour Key Vault.</span></span> <span data-ttu-id="c9e55-117">Se não for o caso de Olá, volte tooRegister um aplicativo no tutorial de Introdução hello e repita a saudação etapas listadas.</span><span class="sxs-lookup"><span data-stu-id="c9e55-117">If this is not hello case, go back tooRegister an Application in hello Get Started tutorial and repeat hello steps listed.</span></span>

<span data-ttu-id="c9e55-118">Este tutorial é projetado para desenvolvedores da web que entenda Olá fundamentos de criação de aplicativos web no Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e55-118">This tutorial is designed for web developers that understand hello basics of creating web applications on Azure.</span></span> <span data-ttu-id="c9e55-119">Para obter mais informações sobre aplicativos Web do Azure, consulte [Visão geral de aplicativos Web](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c9e55-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <span data-ttu-id="c9e55-120"><a id="packages"></a>Adicionar pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="c9e55-120"><a id="packages"></a>Add Nuget Packages</span></span>
<span data-ttu-id="c9e55-121">Existem dois pacotes que seu aplicativo web precisa toohave instalado.</span><span class="sxs-lookup"><span data-stu-id="c9e55-121">There are two packages that your web application needs toohave installed.</span></span>

* <span data-ttu-id="c9e55-122">Biblioteca de autenticação do Active Directory - contém métodos para interagir com o Active Directory do Azure e gerenciar a identidade do usuário</span><span class="sxs-lookup"><span data-stu-id="c9e55-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="c9e55-123">Biblioteca de cofre da chave do Azure - contém métodos para interagir com o cofre da chave do Azure</span><span class="sxs-lookup"><span data-stu-id="c9e55-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="c9e55-124">Esses pacotes podem ser instalados usando Olá Package Manager Console usando o comando Olá Install-Package.</span><span class="sxs-lookup"><span data-stu-id="c9e55-124">Both of these packages can be installed using hello Package Manager Console using hello Install-Package command.</span></span>

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <span data-ttu-id="c9e55-125"><a id="webconfig"></a>Modificar o Web.config</span><span class="sxs-lookup"><span data-stu-id="c9e55-125"><a id="webconfig"></a>Modify Web.Config</span></span>
<span data-ttu-id="c9e55-126">Há três configurações de aplicativo que precisa toobe toohello adicionado. config da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="c9e55-126">There are three application settings that need toobe added toohello web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="c9e55-127">Se você não for toohost seu aplicativo como um aplicativo Web do Azure, você deve adicionar Olá real ClientId, o segredo do cliente e o segredo do URI valores toohello Web. config. Caso contrário, deixe esses valores fictícios porque estaremos adicionando os valores reais Olá no hello Portal do Azure para um nível adicional de segurança.</span><span class="sxs-lookup"><span data-stu-id="c9e55-127">If you are not going toohost your application as an Azure Web App, then you should add hello actual ClientId, Client Secret, and Secret URI values toohello web.config. Otherwise leave these dummy values because we will be adding hello actual values in hello Azure Portal for an additional level of security.</span></span>

## <span data-ttu-id="c9e55-128"><a id="gettoken"></a>Adicione o método tooGet um Token de acesso</span><span class="sxs-lookup"><span data-stu-id="c9e55-128"><a id="gettoken"></a>Add Method tooGet an Access Token</span></span>
<span data-ttu-id="c9e55-129">Saudação de toouse ordem API Cofre de chaves é necessário um token de acesso.</span><span class="sxs-lookup"><span data-stu-id="c9e55-129">In order toouse hello Key Vault API you need an access token.</span></span> <span data-ttu-id="c9e55-130">Olá chave cofre cliente controla chamadas toohello API Cofre de chaves, mas você precisa toosupply-lo com uma função que obtém o token de acesso de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9e55-130">hello Key Vault Client handles calls toohello Key Vault API but you need toosupply it with a function that gets hello access token.</span></span>  

<span data-ttu-id="c9e55-131">A seguir está Olá código tooget um token de acesso do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e55-131">Following is hello code tooget an access token from Azure Active Directory.</span></span> <span data-ttu-id="c9e55-132">Esse código pode ir em qualquer lugar do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c9e55-132">This code can go anywhere in your application.</span></span> <span data-ttu-id="c9e55-133">Gosto tooadd um utilitários ou classe EncryptionHelper.</span><span class="sxs-lookup"><span data-stu-id="c9e55-133">I like tooadd a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property toohold hello secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //hello method that will be provided toohello KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed tooobtain hello JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="c9e55-134">Usando uma ID de cliente e o segredo do cliente é tooauthenticate de maneira mais fácil de saudação um aplicativo do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e55-134">Using a Client ID and Client Secret is hello easiest way tooauthenticate an Azure AD application.</span></span> <span data-ttu-id="c9e55-135">E usá-lo em seu aplicativo Web permite uma separação de funções e mais controle sobre o gerenciamento de chaves.</span><span class="sxs-lookup"><span data-stu-id="c9e55-135">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="c9e55-136">Mas ele depender colocar Olá segredo do cliente em suas definições de configuração que podem ser arriscadas como como colocar o segredo de saudação que você deseja tooprotect em suas definições de configuração para alguns.</span><span class="sxs-lookup"><span data-stu-id="c9e55-136">But it does rely on putting hello Client Secret in your configuration settings which for some can be as risky as putting hello secret that you want tooprotect in your configuration settings.</span></span> <span data-ttu-id="c9e55-137">Consulte abaixo para obter mais informações sobre como toouse uma ID de cliente e certificado em vez de ID do cliente e o segredo do cliente tooauthenticate Olá aplicativo AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e55-137">See below for a discussion on how toouse a Client ID and Certificate instead of Client ID and Client Secret tooauthenticate hello Azure AD application.</span></span>
> 
> 

## <span data-ttu-id="c9e55-138"><a id="appstart"></a>Recuperar o segredo de saudação no início do aplicativo</span><span class="sxs-lookup"><span data-stu-id="c9e55-138"><a id="appstart"></a>Retrieve hello secret on Application Start</span></span>
<span data-ttu-id="c9e55-139">Agora precisamos código toocall Olá API Cofre de chaves e recuperar o segredo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9e55-139">Now we need code toocall hello Key Vault API and retrieve hello secret.</span></span> <span data-ttu-id="c9e55-140">Olá código a seguir pode ser colocado em qualquer lugar desde que ele é chamado antes de precisar toouse-lo.</span><span class="sxs-lookup"><span data-stu-id="c9e55-140">hello following code can be put anywhere as long as it is called before you need toouse it.</span></span> <span data-ttu-id="c9e55-141">Posso ter colocar esse código no evento de início do aplicativo hello em Olá global. asax para que ele é executado uma vez no início e torna Olá segredo disponível para o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="c9e55-141">I have put this code in hello Application Start event in hello Global.asax so that it runs once on start and makes hello secret available for hello application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <span data-ttu-id="c9e55-142"><a id="portalsettings"></a>Adicionar configurações de aplicativo hello Portal do Azure (opcional)</span><span class="sxs-lookup"><span data-stu-id="c9e55-142"><a id="portalsettings"></a>Add App Settings in hello Azure Portal (optional)</span></span>
<span data-ttu-id="c9e55-143">Se você tiver um aplicativo Web do Azure agora você pode adicionar valores reais Olá Olá AppSettings no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e55-143">If you have an Azure Web App you can now add hello actual values for hello AppSettings in hello Azure Portal.</span></span> <span data-ttu-id="c9e55-144">Ao fazer isso, valores reais de saudação não estarão no Web. config de saudação mas protegida pelo Olá Portal onde você tem recursos de controle de acesso separado.</span><span class="sxs-lookup"><span data-stu-id="c9e55-144">By doing this, hello actual values will not be in hello web.config but protected via hello Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="c9e55-145">Esses valores são substituídos para valores de saudação que você inseriu no Web. config. Certifique-se de que nomes de saudação são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="c9e55-145">These values will be substituted for hello values that you entered in your web.config. Make sure that hello names are hello same.</span></span>

![Configurações do aplicativo exibidas no Portal do Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="c9e55-147">Autenticar com um Certificado em vez de um Segredo do Cliente</span><span class="sxs-lookup"><span data-stu-id="c9e55-147">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="c9e55-148">É outra maneira tooauthenticate um aplicativo do AD do Azure usando uma ID de cliente e um certificado em vez de uma ID de cliente e o segredo do cliente.</span><span class="sxs-lookup"><span data-stu-id="c9e55-148">Another way tooauthenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="c9e55-149">A seguir são Olá etapas toouse um certificado em um aplicativo Web do Azure:</span><span class="sxs-lookup"><span data-stu-id="c9e55-149">Following are hello steps toouse a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="c9e55-150">Obter ou Criar um Certificado</span><span class="sxs-lookup"><span data-stu-id="c9e55-150">Get or Create a Certificate</span></span>
2. <span data-ttu-id="c9e55-151">Associar Olá certificado com um aplicativo do AD do Azure</span><span class="sxs-lookup"><span data-stu-id="c9e55-151">Associate hello Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="c9e55-152">Adicionar Olá de toouse de aplicativo Web do código tooyour certificado</span><span class="sxs-lookup"><span data-stu-id="c9e55-152">Add code tooyour Web App toouse hello Certificate</span></span>
4. <span data-ttu-id="c9e55-153">Adicionar um aplicativo Web de tooyour de certificado</span><span class="sxs-lookup"><span data-stu-id="c9e55-153">Add a Certificate tooyour Web App</span></span>

<span data-ttu-id="c9e55-154">**Obter ou Criar um Certificado** Para os nossos objetivos, definiremos um certificado de teste.</span><span class="sxs-lookup"><span data-stu-id="c9e55-154">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="c9e55-155">Aqui estão alguns comandos que você pode usar em um Prompt de comando do desenvolvedor toocreate um certificado.</span><span class="sxs-lookup"><span data-stu-id="c9e55-155">Here are a couple of commands that you can use in a Developer Command Prompt toocreate a certificate.</span></span> <span data-ttu-id="c9e55-156">Alterar diretório toowhere que Olá arquivos de certificado criado.</span><span class="sxs-lookup"><span data-stu-id="c9e55-156">Change directory toowhere you want hello cert files created.</span></span>  <span data-ttu-id="c9e55-157">Além disso, para saudação inicial e final a data do certificado hello, use Olá data atual mais 1 ano.</span><span class="sxs-lookup"><span data-stu-id="c9e55-157">Also, for hello beginning and ending date of hello certificate, use hello current date plus 1 year.</span></span>

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

<span data-ttu-id="c9e55-158">Anote a data de término hello e a senha hello. pfx de saudação (neste exemplo: 31/07/2016 e test123).</span><span class="sxs-lookup"><span data-stu-id="c9e55-158">Make note of hello end date and hello password for hello .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="c9e55-159">Você precisará delas mais tarde.</span><span class="sxs-lookup"><span data-stu-id="c9e55-159">You will need them below.</span></span>

<span data-ttu-id="c9e55-160">Para saber mais sobre a criação de um certificado de teste, confira [Como criar seu próprio certificado de teste](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="c9e55-160">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="c9e55-161">**Olá associar certificado com um aplicativo do Azure AD** agora que você tem um certificado, você precisa tooassociate-lo com um aplicativo do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e55-161">**Associate hello Certificate with an Azure AD application** Now that you have a certificate, you need tooassociate it with an Azure AD application.</span></span> <span data-ttu-id="c9e55-162">Atualmente, Olá Portal do Azure não oferece suporte para esse fluxo de trabalho; Isso pode ser feito por meio do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c9e55-162">Presently, hello Azure Portal does not support this workflow; this can be completed through PowerShell.</span></span> <span data-ttu-id="c9e55-163">Execute Olá certificado de saudação tooassoicate comandos com o aplicativo hello AD do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="c9e55-163">Run hello following commands tooassoicate hello certificate with hello Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get hello thumbprint toouse in your app settings
    $x509.Thumbprint

<span data-ttu-id="c9e55-164">Depois de executar esses comandos, você pode ver o aplicativo hello no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="c9e55-164">After you have run these commands, you can see hello application in Azure AD.</span></span> <span data-ttu-id="c9e55-165">Ao pesquisar, certifique-se que você selecionar "Minha empresa possui aplicativos" em vez de "Aplicativos minha empresa usa" na caixa de diálogo de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="c9e55-165">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in hello search dialog.</span></span>

<span data-ttu-id="c9e55-166">toolearn mais informações sobre objetos de aplicativo do Azure AD e ServicePrincipal, consulte [objetos Application e entidade de serviço](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="c9e55-166">toolearn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="c9e55-167">**Adicionar Olá de toouse de aplicativo Web do código tooyour certificado** agora vamos adicionar código tooyour aplicativo Web tooaccess Olá cert e usá-lo para autenticação.</span><span class="sxs-lookup"><span data-stu-id="c9e55-167">**Add code tooyour Web App toouse hello Certificate** Now we will add code tooyour Web App tooaccess hello cert and use it for authentication.</span></span>

<span data-ttu-id="c9e55-168">Primeiro, há cert de saudação do código tooaccess.</span><span class="sxs-lookup"><span data-stu-id="c9e55-168">First there is code tooaccess hello cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since hello test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


<span data-ttu-id="c9e55-169">Observe que Olá StoreLocation é CurrentUser em vez de LocalMachine.</span><span class="sxs-lookup"><span data-stu-id="c9e55-169">Note that hello StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="c9e55-170">E se nós está fornecendo toohello 'false' encontrar o método porque estamos usando um certificado de teste.</span><span class="sxs-lookup"><span data-stu-id="c9e55-170">And that we are supplying 'false' toohello Find method because we are using a test cert.</span></span>

<span data-ttu-id="c9e55-171">Next é o código que usa Olá CertificateHelper e cria um ClientAssertionCertificate que é necessário para autenticação.</span><span class="sxs-lookup"><span data-stu-id="c9e55-171">Next is code that uses hello CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="c9e55-172">Aqui está a saudação novo código tooget Olá token de acesso.</span><span class="sxs-lookup"><span data-stu-id="c9e55-172">Here is hello new code tooget hello access token.</span></span> <span data-ttu-id="c9e55-173">Isso substitui o método GetToken da saudação acima.</span><span class="sxs-lookup"><span data-stu-id="c9e55-173">This replaces hello GetToken method above.</span></span> <span data-ttu-id="c9e55-174">Eu dei a ele um nome diferente por conveniência.</span><span class="sxs-lookup"><span data-stu-id="c9e55-174">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="c9e55-175">Coloquei todo esse código na classe Utils do projeto do Aplicativo Web para facilidade de uso.</span><span class="sxs-lookup"><span data-stu-id="c9e55-175">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="c9e55-176">última alteração de código Hello está em Olá método Application_Start.</span><span class="sxs-lookup"><span data-stu-id="c9e55-176">hello last code change is in hello Application_Start method.</span></span> <span data-ttu-id="c9e55-177">Primeiro, precisamos toocall Olá Olá tooload de método GetCert() ClientAssertionCertificate.</span><span class="sxs-lookup"><span data-stu-id="c9e55-177">First we need toocall hello GetCert() method tooload hello ClientAssertionCertificate.</span></span> <span data-ttu-id="c9e55-178">E, em seguida, podemos alterar o método de retorno de chamada de saudação que fornecemos ao criar um novo KeyVaultClient.</span><span class="sxs-lookup"><span data-stu-id="c9e55-178">And then we change hello callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="c9e55-179">Observe que isso substitui o código de saudação que usamos acima.</span><span class="sxs-lookup"><span data-stu-id="c9e55-179">Note that this replaces hello code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="c9e55-180">**Adicionar um tooyour certificado aplicativo Web por meio de hello Azure Portal** adicionar um aplicativo Web de tooyour do certificado é um processo de duas etapas simples.</span><span class="sxs-lookup"><span data-stu-id="c9e55-180">**Add a Certificate tooyour Web App through hello Azure Portal** Adding a Certificate tooyour Web App is a simple two-step process.</span></span> <span data-ttu-id="c9e55-181">Primeiro, vá toohello Portal do Azure e navegue tooyour aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="c9e55-181">First, go toohello Azure Portal and navigate tooyour Web App.</span></span> <span data-ttu-id="c9e55-182">Na folha de configurações de saudação para seu aplicativo Web, clique na entrada de saudação para "domínios personalizados e SSL".</span><span class="sxs-lookup"><span data-stu-id="c9e55-182">On hello Settings blade for your Web App, click on hello entry for "Custom domains and SSL".</span></span> <span data-ttu-id="c9e55-183">Em Olá folha que abre você estarão Olá tooupload capaz de certificado que você criou anteriormente, KVWebApp.pfx, certifique-se de que você se lembrar senha Olá Olá pfx.</span><span class="sxs-lookup"><span data-stu-id="c9e55-183">On hello blade that opens you will be able tooupload hello Certificate that you created above, KVWebApp.pfx, make sure that you remember hello password for hello pfx.</span></span>

![Adicionar um aplicativo Web de tooa do certificado em Olá Portal do Azure][2]

<span data-ttu-id="c9e55-185">Olá, última coisa que você precisa de toodo é tooadd tooyour uma configuração de aplicativo Web App com hello nome site\_carga\_certificados e um valor de *.</span><span class="sxs-lookup"><span data-stu-id="c9e55-185">hello last thing that you need toodo is tooadd an Application Setting tooyour Web App that has hello name WEBSITE\_LOAD\_CERTIFICATES and a value of *.</span></span> <span data-ttu-id="c9e55-186">Isso garantirá que todos os Certificados sejam carregados.</span><span class="sxs-lookup"><span data-stu-id="c9e55-186">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="c9e55-187">Se você quisesse Olá somente tooload certificados que você carregou, em seguida, você pode inserir uma lista separada por vírgulas de suas impressões digitais.</span><span class="sxs-lookup"><span data-stu-id="c9e55-187">If you wanted tooload only hello Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="c9e55-188">toolearn mais sobre como adicionar um certificado tooa aplicativo Web, consulte [usando certificados em aplicativos de sites do Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="c9e55-188">toolearn more about adding a Certificate tooa Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="c9e55-189">**Adicionar um certificado tooKey cofre como um segredo** em vez de carregar seu toohello de certificado do serviço de aplicativo Web diretamente, você pode armazená-lo no cofre de chaves como um segredo e implantá-lo de lá.</span><span class="sxs-lookup"><span data-stu-id="c9e55-189">**Add a Certificate tooKey Vault as a secret** Instead of uploading your certificate toohello Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="c9e55-190">Esse é um processo de duas etapas é descrito em Olá postagem de blog a seguir [implantação de certificado do Azure do aplicativo Web por meio de Cofre de chaves](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="c9e55-190">This is a two-step process that is outlined in hello following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <span data-ttu-id="c9e55-191"><a id="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c9e55-191"><a id="next"></a>Next steps</span></span>
<span data-ttu-id="c9e55-192">Para referências de programação, consulte [Referência de API do cliente C# do cofre da chave do Azure](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="c9e55-192">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
