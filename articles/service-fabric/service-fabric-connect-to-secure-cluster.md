---
title: "aaaConnect cluster do Azure Service Fabric de tooan com segurança | Microsoft Docs"
description: "Descreve como tooauthenticate cliente acessar o cluster do Service Fabric tooa e toosecure comunicação entre clientes e um cluster."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 759a539e-e5e6-4055-bff5-d38804656e10
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 1b6a87a1fefaddce2043c604ca53751157232170
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-secure-cluster"></a>Conecte-se o cluster seguro tooa

Quando um cliente se conecta o nó de cluster do Service Fabric tooa, o cliente de saudação pode ser estabelecida usando a segurança de certificado ou Azure Active Directory (AAD) uma comunicação segura e autenticada. Essa autenticação garante que apenas usuários autorizados podem acessar o cluster hello e aplicativos implantados e executam tarefas de gerenciamento.  Certificado ou segurança do AAD deve ter sido previamente habilitada no cluster hello quando Olá cluster foi criado.  Para obter mais informações sobre cenários de segurança de cluster, consulte [Segurança de cluster](service-fabric-cluster-security.md). Se você estiver se conectando tooa cluster protegido com certificados, [configurar certificados de cliente Olá](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) no computador de saudação que conecta toohello cluster. 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a>Conecte-se tooa cluster seguro usando o Azure Service Fabric CLI (sfctl)

Há algumas maneiras diferentes tooconnect tooa segura cluster usando Olá CLI de malha do serviço (sfctl). Ao usar um certificado de cliente para autenticação, o certificado de saudação detalhes devem corresponder a um certificado implantado toohello nós de cluster. Se o certificado tiver autoridades de certificação (CAs), será necessário tooadditionally especificar Olá confiável autoridades de certificação.

Você pode se conectar a cluster tooa usando Olá `sfctl cluster select` comando.

Certificados de cliente podem ser especificados em dois modos diferentes, como um par de certificados e chaves ou como um arquivo pem individual. Senha protegida `pem` arquivos, você será solicitado automaticamente a senha de saudação tooenter.

certificado de cliente Olá toospecify como um arquivo pem, especifique o caminho do arquivo de saudação em Olá `--pem` argumento. Por exemplo:

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

Protegido por senha pem arquivos solicitará toorunning anterior senha qualquer comando.

toospecify um certificado, o par de chaves usa Olá `--cert` e `--key` toospecify Olá caminhos tooeach respectivo arquivo de argumentos.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

Às vezes, os certificados usados toosecure teste ou desenvolvimento clusters falharem na validação do certificado. verificação de certificado toobypass especificar Olá `--no-verify` opção. Por exemplo:

> [!WARNING]
> Não use Olá `no-verify` opção ao conectar-se a clusters de malha do serviço tooproduction.

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

Além disso, você pode especificar caminhos toodirectories de certificados de autoridade de certificação confiáveis ou certificados individuais. toospecify esses caminhos, use Olá `--ca` argumento. Por exemplo:

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

Depois de se conectar, você deve poder muito[executar outros comandos sfctl](service-fabric-cli.md) toointeract com cluster hello.

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a>Conecte-se o cluster tooa usando o PowerShell
Antes de executar operações em um cluster por meio do PowerShell, primeiro estabelecer um cluster de toohello de conexão. conexão de cluster Olá é usado para todos os comandos subsequentes Olá considerando a sessão do PowerShell.

### <a name="connect-tooan-unsecure-cluster"></a>Conecte-se o cluster não segura tooan

tooconnect tooan não segura de cluster, forneça Olá toohello de endereço de ponto de extremidade de cluster **Connect-ServiceFabricCluster** comando:

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Conecte-se tooa cluster seguro usando o Active Directory do Azure

tooconnect tooa cluster seguro que usa o acesso de administrador de cluster do Active Directory do Azure tooauthorize, forneça a impressão digital do certificado de cluster hello e usar Olá *AzureActiveDirectory* sinalizador.  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Conecte-se tooa cluster segura usando um certificado de cliente
Saudação de execução a seguir de comando do PowerShell tooconnect tooa segura de cluster que usa o acesso de administrador do tooauthorize de certificados de cliente. Forneça a impressão digital do certificado de cluster hello e a impressão digital de saudação do certificado de cliente Olá que concedeu permissões para gerenciamento de cluster. detalhes do certificado Olá devem corresponder a um certificado em nós de cluster de saudação.

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

*ServerCertThumbprint* é a impressão digital de saudação do certificado do servidor de saudação instalado em nós de cluster de saudação. *FindValue* é a impressão digital de saudação do certificado de cliente Olá administrador.
Quando os parâmetros de saudação são preenchidos, comando Olá aparência Olá exemplo a seguir: 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a>Conecte-se tooa cluster seguro usando o Active Directory do Windows
Se o cluster autônomo é implantado usando a segurança do AD, conecte-se toohello cluster acrescentando comutador hello "WindowsCredential".

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a>Conecte-se o cluster tooa usando Olá FabricClient APIs
Olá SDK do Service Fabric fornece Olá [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) classe para gerenciamento de cluster. Olá toouse FabricClient APIs, obter Olá pacote Microsoft.ServiceFabric NuGet.

### <a name="connect-tooan-unsecure-cluster"></a>Conecte-se o cluster não segura tooan

tooconnect tooa segura cluster remoto, crie uma instância de FabricClient e forneça o endereço de cluster hello:

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

Para o código que é executado a partir de um cluster, por exemplo, em um serviço confiável, crie um FabricClient *sem* especificando o endereço de cluster hello. FabricClient conecta-se gerenciamento local toohello gateway no código de saudação do nó hello está sendo executado, evitando um salto extra na rede.

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Conecte-se tooa cluster segura usando um certificado de cliente

Olá nós cluster Olá devem ter certificados válidos cujo nome comum ou nome DNS na rede SAN é exibido no hello [RemoteCommonNames propriedade](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) definida em [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient). Esse processo a seguir habilita a autenticação mútua entre o cliente hello e nós de cluster de saudação.

```csharp
using System.Fabric;
using System.Security.Cryptography.X509Certificates;

string clientCertThumb = "71DE04467C9ED0544D021098BCD44C71E183414E";
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string CommonName = "www.clustername.westus.azure.com";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var xc = GetCredentials(clientCertThumb, serverCertThumb, CommonName);
var fc = new FabricClient(xc, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

static X509Credentials GetCredentials(string clientCertThumb, string serverCertThumb, string name)
{
    X509Credentials xc = new X509Credentials();
    xc.StoreLocation = StoreLocation.CurrentUser;
    xc.StoreName = "My";
    xc.FindType = X509FindType.FindByThumbprint;
    xc.FindValue = clientCertThumb;
    xc.RemoteCommonNames.Add(name);
    xc.RemoteCertThumbprints.Add(serverCertThumb);
    xc.ProtectionLevel = ProtectionLevel.EncryptAndSign;
    return xc;
}
```

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a>Conecte-se tooa cluster seguro usando o Active Directory do Azure

Olá seguindo o exemplo usa o Active Directory do Azure para certificado de cliente de identidade e servidor para a identidade do servidor.

Uma janela de caixa de diálogo aparece automaticamente para entrada interativa ao conectar o cluster toohello.

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}
```

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a>Conecte-se tooa cluster seguro não interativamente usando o Active Directory do Azure

Olá exemplo a seguir se baseia no ActiveDirectory, versão: 2.19.208020213.

Para saber mais sobre aquisição de token do AAD, consulte [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).

```csharp
string tenantId = "C15CFCEA-02C1-40DC-8466-FBD0EE0B05D2";
string clientApplicationId = "118473C2-7619-46E3-A8E4-6DA8D5F56E12";
string webApplicationId = "53E6948C-0897-4DA6-B26A-EE2A38A690B4";

string token = GetAccessToken(
    tenantId,
    webApplicationId,
    clientApplicationId,
    "urn:ietf:wg:oauth:2.0:oob");

string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);
claimsCredentials.LocalClaims = token;

var fc = new FabricClient(claimsCredentials, connection);

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(
    string tenantId,
    string resource,
    string clientId,
    string redirectUri)
{
    string authorityFormat = @"https://login.microsoftonline.com/{0}";
    string authority = string.Format(CultureInfo.InvariantCulture, authorityFormat, tenantId);
    var authContext = new AuthenticationContext(authority);

    var authResult = authContext.AcquireToken(
        resource,
        clientId,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a>Conecte-se o cluster seguro tooa sem conhecimento prévio de metadados usando o Azure Active Directory

Olá, exemplo a seguir usa a aquisição de token não interativo, mas hello mesma abordagem pode ser usado toobuild uma experiência de aquisição de token interativo personalizado. Olá Active Directory do Azure metadados necessários para aquisição de token é lido de configuração de cluster.

```csharp
string serverCertThumb = "A8136758F4AB8962AF2BF3F27921BE1DF67F4326";
string connection = "clustername.westus.cloudapp.azure.com:19000";

var claimsCredentials = new ClaimsCredentials();
claimsCredentials.ServerThumbprints.Add(serverCertThumb);

var fc = new FabricClient(claimsCredentials, connection);

fc.ClaimsRetrieval += (o, e) =>
{
    return GetAccessToken(e.AzureActiveDirectoryMetadata);
};

try
{
    var ret = fc.ClusterManager.GetClusterManifestAsync().Result;
    Console.WriteLine(ret.ToString());
}
catch (Exception e)
{
    Console.WriteLine("Connect failed: {0}", e.Message);
}

...

static string GetAccessToken(AzureActiveDirectoryMetadata aad)
{
    var authContext = new AuthenticationContext(aad.Authority);

    var authResult = authContext.AcquireToken(
        aad.ClusterApplication,
        aad.ClientApplication,
        new UserCredential("TestAdmin@clustenametenant.onmicrosoft.com", "TestPassword"));
    return authResult.AccessToken;
}

```

<a id="connectsecureclustersfx"></a>

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a>Conecte-se tooa cluster seguro usando o Gerenciador do Service Fabric
tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) para um determinado cluster, aponte seu navegador para:

`http://<your-cluster-endpoint>:19080/Explorer`

a URL completa Olá também está disponível no painel de essentials de cluster Olá de saudação portal do Azure.

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a>Conecte-se tooa cluster seguro usando o Active Directory do Azure

tooconnect tooa cluster protegido por AAD, aponte seu navegador para:

`https://<your-cluster-endpoint>:19080/Explorer`

Você automaticamente ser solicitado toolog com AAD.

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a>Conecte-se tooa cluster segura usando um certificado de cliente

tooconnect tooa cluster protegido com certificados, aponte seu navegador para:

`https://<your-cluster-endpoint>:19080/Explorer`

Você automaticamente ser solicitado tooselect um certificado de cliente.

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a>Configurar um certificado de cliente no computador remoto Olá
Pelo menos dois certificados devem ser usados para proteger o cluster hello, um certificado de cluster e servidor de saudação e outro para acesso para cliente.  É recomendável que você também use certificados secundários e certificados de acesso para cliente adicionais.  a comunicação entre um cliente e um nó de cluster usando Olá toosecure segurança de certificado, você primeiro precisa tooobtain e instale o certificado de cliente hello. certificado Olá pode ser instalado em hello (Meu) repositório pessoal do computador local hello ou do usuário atual do hello.  Impressão digital de saudação do certificado do servidor de saudação também é necessário para que hello cliente pode autenticar cluster hello.

Execute Olá tooset de cmdlet do PowerShell backup do certificado de cliente Olá no computador de saudação do qual você acessar o cluster Olá a seguir.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

Se for um certificado autoassinado, você precisa tooimport-lo "pessoas confiáveis" da máquina tooyour armazenar antes de usar este cluster do certificado tooconnect tooa segura.

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a>Próximas etapas

* [Processo de atualização de Cluster de Malha do Serviço e as suas expectativas](service-fabric-cluster-upgrade.md)
* [Gerenciando aplicativos da Malha do Serviço no Visual Studio](service-fabric-manage-application-in-visual-studio.md)
* [Introdução ao modelo de Integridade da Malha de Serviço](service-fabric-health-introduction.md)
* [Segurança do aplicativo e RunAs](service-fabric-application-runas-security.md)
* [Introdução à CLI do Service Fabric](service-fabric-cli.md)
