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
# <a name="use-azure-key-vault-from-a-web-application"></a>Usar cofre da chave do Azure em um aplicativo Web
## <a name="introduction"></a>Introdução
Use este toohelp tutorial você aprenderá como toouse chave do Azure Cofre de um aplicativo web no Azure. Orienta você pelo processo de saudação de acessar um segredo de um cofre de chaves do Azure para que ele pode ser usado em seu aplicativo web.

**Estimado tempo toocomplete:** 15 minutos

Para obter informações gerais sobre o Cofre da Chave do Azure, consulte [O que é o Cofre da Chave do Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Pré-requisitos
toocomplete neste tutorial, você deve ter Olá a seguir:

* Um segredo de tooa URI em um cofre de chaves do Azure
* Uma ID de cliente e um segredo do cliente para um aplicativo web registrado com o Active Directory do Azure que tenha acesso tooyour Cofre de chaves
* Um aplicativo Web. Estamos será mostrando etapas Olá para um aplicativo ASP.NET MVC implantado no Azure como um aplicativo Web.

> [!NOTE]
> É essencial que você tenha concluído as etapas de saudação listadas na [Introdução ao Azure Key Vault](key-vault-get-started.md) para este tutorial para que você tenha hello segredo do URI tooa e hello ID do cliente e segredo do cliente para um aplicativo web.
> 
> 

aplicativo web Hello que acessarão Olá Cofre de chaves é hello um que é registrado no Active Directory do Azure e tem acesso tooyour Cofre de chaves. Se não for o caso de Olá, volte tooRegister um aplicativo no tutorial de Introdução hello e repita a saudação etapas listadas.

Este tutorial é projetado para desenvolvedores da web que entenda Olá fundamentos de criação de aplicativos web no Azure. Para obter mais informações sobre aplicativos Web do Azure, consulte [Visão geral de aplicativos Web](../app-service-web/app-service-web-overview.md).

## <a id="packages"></a>Adicionar pacotes NuGet
Existem dois pacotes que seu aplicativo web precisa toohave instalado.

* Biblioteca de autenticação do Active Directory - contém métodos para interagir com o Active Directory do Azure e gerenciar a identidade do usuário
* Biblioteca de cofre da chave do Azure - contém métodos para interagir com o cofre da chave do Azure

Esses pacotes podem ser instalados usando Olá Package Manager Console usando o comando Olá Install-Package.

    // this is currently hello latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <a id="webconfig"></a>Modificar o Web.config
Há três configurações de aplicativo que precisa toobe toohello adicionado. config da seguinte maneira.

    <!-- ClientId and ClientSecret refer toohello web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is hello URI for hello secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


Se você não for toohost seu aplicativo como um aplicativo Web do Azure, você deve adicionar Olá real ClientId, o segredo do cliente e o segredo do URI valores toohello Web. config. Caso contrário, deixe esses valores fictícios porque estaremos adicionando os valores reais Olá no hello Portal do Azure para um nível adicional de segurança.

## <a id="gettoken"></a>Adicione o método tooGet um Token de acesso
Saudação de toouse ordem API Cofre de chaves é necessário um token de acesso. Olá chave cofre cliente controla chamadas toohello API Cofre de chaves, mas você precisa toosupply-lo com uma função que obtém o token de acesso de saudação.  

A seguir está Olá código tooget um token de acesso do Active Directory do Azure. Esse código pode ir em qualquer lugar do aplicativo. Gosto tooadd um utilitários ou classe EncryptionHelper.  

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
> Usando uma ID de cliente e o segredo do cliente é tooauthenticate de maneira mais fácil de saudação um aplicativo do AD do Azure. E usá-lo em seu aplicativo Web permite uma separação de funções e mais controle sobre o gerenciamento de chaves. Mas ele depender colocar Olá segredo do cliente em suas definições de configuração que podem ser arriscadas como como colocar o segredo de saudação que você deseja tooprotect em suas definições de configuração para alguns. Consulte abaixo para obter mais informações sobre como toouse uma ID de cliente e certificado em vez de ID do cliente e o segredo do cliente tooauthenticate Olá aplicativo AD do Azure.
> 
> 

## <a id="appstart"></a>Recuperar o segredo de saudação no início do aplicativo
Agora precisamos código toocall Olá API Cofre de chaves e recuperar o segredo de saudação. Olá código a seguir pode ser colocado em qualquer lugar desde que ele é chamado antes de precisar toouse-lo. Posso ter colocar esse código no evento de início do aplicativo hello em Olá global. asax para que ele é executado uma vez no início e torna Olá segredo disponível para o aplicativo hello.

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class toohold hello secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <a id="portalsettings"></a>Adicionar configurações de aplicativo hello Portal do Azure (opcional)
Se você tiver um aplicativo Web do Azure agora você pode adicionar valores reais Olá Olá AppSettings no hello Portal do Azure. Ao fazer isso, valores reais de saudação não estarão no Web. config de saudação mas protegida pelo Olá Portal onde você tem recursos de controle de acesso separado. Esses valores são substituídos para valores de saudação que você inseriu no Web. config. Certifique-se de que nomes de saudação são Olá mesmo.

![Configurações do aplicativo exibidas no Portal do Azure][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a>Autenticar com um Certificado em vez de um Segredo do Cliente
É outra maneira tooauthenticate um aplicativo do AD do Azure usando uma ID de cliente e um certificado em vez de uma ID de cliente e o segredo do cliente. A seguir são Olá etapas toouse um certificado em um aplicativo Web do Azure:

1. Obter ou Criar um Certificado
2. Associar Olá certificado com um aplicativo do AD do Azure
3. Adicionar Olá de toouse de aplicativo Web do código tooyour certificado
4. Adicionar um aplicativo Web de tooyour de certificado

**Obter ou Criar um Certificado** Para os nossos objetivos, definiremos um certificado de teste. Aqui estão alguns comandos que você pode usar em um Prompt de comando do desenvolvedor toocreate um certificado. Alterar diretório toowhere que Olá arquivos de certificado criado.  Além disso, para saudação inicial e final a data do certificado hello, use Olá data atual mais 1 ano.

    makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r
    pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123

Anote a data de término hello e a senha hello. pfx de saudação (neste exemplo: 31/07/2016 e test123). Você precisará delas mais tarde.

Para saber mais sobre a criação de um certificado de teste, confira [Como criar seu próprio certificado de teste](https://msdn.microsoft.com/library/ff699202.aspx)

**Olá associar certificado com um aplicativo do Azure AD** agora que você tem um certificado, você precisa tooassociate-lo com um aplicativo do AD do Azure. Atualmente, Olá Portal do Azure não oferece suporte para esse fluxo de trabalho; Isso pode ser feito por meio do PowerShell. Execute Olá certificado de saudação tooassoicate comandos com o aplicativo hello AD do Azure a seguir:

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

Depois de executar esses comandos, você pode ver o aplicativo hello no AD do Azure. Ao pesquisar, certifique-se que você selecionar "Minha empresa possui aplicativos" em vez de "Aplicativos minha empresa usa" na caixa de diálogo de pesquisa de saudação.

toolearn mais informações sobre objetos de aplicativo do Azure AD e ServicePrincipal, consulte [objetos Application e entidade de serviço](../active-directory/active-directory-application-objects.md)

**Adicionar Olá de toouse de aplicativo Web do código tooyour certificado** agora vamos adicionar código tooyour aplicativo Web tooaccess Olá cert e usá-lo para autenticação.

Primeiro, há cert de saudação do código tooaccess.

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


Observe que Olá StoreLocation é CurrentUser em vez de LocalMachine. E se nós está fornecendo toohello 'false' encontrar o método porque estamos usando um certificado de teste.

Next é o código que usa Olá CertificateHelper e cria um ClientAssertionCertificate que é necessário para autenticação.

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


Aqui está a saudação novo código tooget Olá token de acesso. Isso substitui o método GetToken da saudação acima. Eu dei a ele um nome diferente por conveniência.

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

Coloquei todo esse código na classe Utils do projeto do Aplicativo Web para facilidade de uso.

última alteração de código Hello está em Olá método Application_Start. Primeiro, precisamos toocall Olá Olá tooload de método GetCert() ClientAssertionCertificate. E, em seguida, podemos alterar o método de retorno de chamada de saudação que fornecemos ao criar um novo KeyVaultClient. Observe que isso substitui o código de saudação que usamos acima.

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


**Adicionar um tooyour certificado aplicativo Web por meio de hello Azure Portal** adicionar um aplicativo Web de tooyour do certificado é um processo de duas etapas simples. Primeiro, vá toohello Portal do Azure e navegue tooyour aplicativo Web. Na folha de configurações de saudação para seu aplicativo Web, clique na entrada de saudação para "domínios personalizados e SSL". Em Olá folha que abre você estarão Olá tooupload capaz de certificado que você criou anteriormente, KVWebApp.pfx, certifique-se de que você se lembrar senha Olá Olá pfx.

![Adicionar um aplicativo Web de tooa do certificado em Olá Portal do Azure][2]

Olá, última coisa que você precisa de toodo é tooadd tooyour uma configuração de aplicativo Web App com hello nome site\_carga\_certificados e um valor de *. Isso garantirá que todos os Certificados sejam carregados. Se você quisesse Olá somente tooload certificados que você carregou, em seguida, você pode inserir uma lista separada por vírgulas de suas impressões digitais.

toolearn mais sobre como adicionar um certificado tooa aplicativo Web, consulte [usando certificados em aplicativos de sites do Azure](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)

**Adicionar um certificado tooKey cofre como um segredo** em vez de carregar seu toohello de certificado do serviço de aplicativo Web diretamente, você pode armazená-lo no cofre de chaves como um segredo e implantá-lo de lá. Esse é um processo de duas etapas é descrito em Olá postagem de blog a seguir [implantação de certificado do Azure do aplicativo Web por meio de Cofre de chaves](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)

## <a id="next"></a>Próximas etapas
Para referências de programação, consulte [Referência de API do cliente C# do cofre da chave do Azure](https://msdn.microsoft.com/library/azure/dn903628.aspx).

<!--Image references-->
[1]: ./media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: ./media/key-vault-use-from-web-application/PortalAddCertificate.png
