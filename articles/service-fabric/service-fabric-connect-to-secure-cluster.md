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
# <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="9b140-103">Conecte-se o cluster seguro tooa</span><span class="sxs-lookup"><span data-stu-id="9b140-103">Connect tooa secure cluster</span></span>

<span data-ttu-id="9b140-104">Quando um cliente se conecta o nó de cluster do Service Fabric tooa, o cliente de saudação pode ser estabelecida usando a segurança de certificado ou Azure Active Directory (AAD) uma comunicação segura e autenticada.</span><span class="sxs-lookup"><span data-stu-id="9b140-104">When a client connects tooa Service Fabric cluster node, hello client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="9b140-105">Essa autenticação garante que apenas usuários autorizados podem acessar o cluster hello e aplicativos implantados e executam tarefas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="9b140-105">This authentication ensures that only authorized users can access hello cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="9b140-106">Certificado ou segurança do AAD deve ter sido previamente habilitada no cluster hello quando Olá cluster foi criado.</span><span class="sxs-lookup"><span data-stu-id="9b140-106">Certificate or AAD security must have been previously enabled on hello cluster when hello cluster was created.</span></span>  <span data-ttu-id="9b140-107">Para obter mais informações sobre cenários de segurança de cluster, consulte [Segurança de cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="9b140-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="9b140-108">Se você estiver se conectando tooa cluster protegido com certificados, [configurar certificados de cliente Olá](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) no computador de saudação que conecta toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="9b140-108">If you are connecting tooa cluster secured with certificates, [set up hello client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on hello computer that connects toohello cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-tooa-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="9b140-109">Conecte-se tooa cluster seguro usando o Azure Service Fabric CLI (sfctl)</span><span class="sxs-lookup"><span data-stu-id="9b140-109">Connect tooa secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="9b140-110">Há algumas maneiras diferentes tooconnect tooa segura cluster usando Olá CLI de malha do serviço (sfctl).</span><span class="sxs-lookup"><span data-stu-id="9b140-110">There are a few different ways tooconnect tooa secure cluster using hello Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="9b140-111">Ao usar um certificado de cliente para autenticação, o certificado de saudação detalhes devem corresponder a um certificado implantado toohello nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="9b140-111">When using a client certificate for authentication, hello certificate details must match a certificate deployed toohello cluster nodes.</span></span> <span data-ttu-id="9b140-112">Se o certificado tiver autoridades de certificação (CAs), será necessário tooadditionally especificar Olá confiável autoridades de certificação.</span><span class="sxs-lookup"><span data-stu-id="9b140-112">If your certificate has Certificate Authorities (CAs), you need tooadditionally specify hello trusted CAs.</span></span>

<span data-ttu-id="9b140-113">Você pode se conectar a cluster tooa usando Olá `sfctl cluster select` comando.</span><span class="sxs-lookup"><span data-stu-id="9b140-113">You can connect tooa cluster using hello `sfctl cluster select` command.</span></span>

<span data-ttu-id="9b140-114">Certificados de cliente podem ser especificados em dois modos diferentes, como um par de certificados e chaves ou como um arquivo pem individual.</span><span class="sxs-lookup"><span data-stu-id="9b140-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="9b140-115">Senha protegida `pem` arquivos, você será solicitado automaticamente a senha de saudação tooenter.</span><span class="sxs-lookup"><span data-stu-id="9b140-115">For password protected `pem` files, you will be prompted automatically tooenter hello password.</span></span>

<span data-ttu-id="9b140-116">certificado de cliente Olá toospecify como um arquivo pem, especifique o caminho do arquivo de saudação em Olá `--pem` argumento.</span><span class="sxs-lookup"><span data-stu-id="9b140-116">toospecify hello client certificate as a pem file, specify hello file path in hello `--pem` argument.</span></span> <span data-ttu-id="9b140-117">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9b140-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="9b140-118">Protegido por senha pem arquivos solicitará toorunning anterior senha qualquer comando.</span><span class="sxs-lookup"><span data-stu-id="9b140-118">Password protected pem files will prompt for password prior toorunning any command.</span></span>

<span data-ttu-id="9b140-119">toospecify um certificado, o par de chaves usa Olá `--cert` e `--key` toospecify Olá caminhos tooeach respectivo arquivo de argumentos.</span><span class="sxs-lookup"><span data-stu-id="9b140-119">toospecify a cert, key pair use hello `--cert` and `--key` arguments toospecify hello file paths tooeach respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="9b140-120">Às vezes, os certificados usados toosecure teste ou desenvolvimento clusters falharem na validação do certificado.</span><span class="sxs-lookup"><span data-stu-id="9b140-120">Sometimes certificates used toosecure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="9b140-121">verificação de certificado toobypass especificar Olá `--no-verify` opção.</span><span class="sxs-lookup"><span data-stu-id="9b140-121">toobypass certificate verification, specify hello `--no-verify` option.</span></span> <span data-ttu-id="9b140-122">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9b140-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="9b140-123">Não use Olá `no-verify` opção ao conectar-se a clusters de malha do serviço tooproduction.</span><span class="sxs-lookup"><span data-stu-id="9b140-123">Do not use hello `no-verify` option when connecting tooproduction Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="9b140-124">Além disso, você pode especificar caminhos toodirectories de certificados de autoridade de certificação confiáveis ou certificados individuais.</span><span class="sxs-lookup"><span data-stu-id="9b140-124">In addition, you can specify paths toodirectories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="9b140-125">toospecify esses caminhos, use Olá `--ca` argumento.</span><span class="sxs-lookup"><span data-stu-id="9b140-125">toospecify these paths, use hello `--ca` argument.</span></span> <span data-ttu-id="9b140-126">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="9b140-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="9b140-127">Depois de se conectar, você deve poder muito[executar outros comandos sfctl](service-fabric-cli.md) toointeract com cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9b140-127">After you connect, you should be able too[run other sfctl commands](service-fabric-cli.md) toointeract with hello cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-tooa-cluster-using-powershell"></a><span data-ttu-id="9b140-128">Conecte-se o cluster tooa usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b140-128">Connect tooa cluster using PowerShell</span></span>
<span data-ttu-id="9b140-129">Antes de executar operações em um cluster por meio do PowerShell, primeiro estabelecer um cluster de toohello de conexão.</span><span class="sxs-lookup"><span data-stu-id="9b140-129">Before you perform operations on a cluster through PowerShell, first establish a connection toohello cluster.</span></span> <span data-ttu-id="9b140-130">conexão de cluster Olá é usado para todos os comandos subsequentes Olá considerando a sessão do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9b140-130">hello cluster connection is used for all subsequent commands in hello given PowerShell session.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="9b140-131">Conecte-se o cluster não segura tooan</span><span class="sxs-lookup"><span data-stu-id="9b140-131">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="9b140-132">tooconnect tooan não segura de cluster, forneça Olá toohello de endereço de ponto de extremidade de cluster **Connect-ServiceFabricCluster** comando:</span><span class="sxs-lookup"><span data-stu-id="9b140-132">tooconnect tooan unsecure cluster, provide hello cluster endpoint address toohello **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="9b140-133">Conecte-se tooa cluster seguro usando o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9b140-133">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="9b140-134">tooconnect tooa cluster seguro que usa o acesso de administrador de cluster do Active Directory do Azure tooauthorize, forneça a impressão digital do certificado de cluster hello e usar Olá *AzureActiveDirectory* sinalizador.</span><span class="sxs-lookup"><span data-stu-id="9b140-134">tooconnect tooa secure cluster that uses Azure Active Directory tooauthorize cluster administrator access, provide hello cluster certificate thumbprint and use hello *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="9b140-135">Conecte-se tooa cluster segura usando um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="9b140-135">Connect tooa secure cluster using a client certificate</span></span>
<span data-ttu-id="9b140-136">Saudação de execução a seguir de comando do PowerShell tooconnect tooa segura de cluster que usa o acesso de administrador do tooauthorize de certificados de cliente.</span><span class="sxs-lookup"><span data-stu-id="9b140-136">Run hello following PowerShell command tooconnect tooa secure cluster that uses client certificates tooauthorize administrator access.</span></span> <span data-ttu-id="9b140-137">Forneça a impressão digital do certificado de cluster hello e a impressão digital de saudação do certificado de cliente Olá que concedeu permissões para gerenciamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="9b140-137">Provide hello cluster certificate thumbprint and hello thumbprint of hello client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="9b140-138">detalhes do certificado Olá devem corresponder a um certificado em nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b140-138">hello certificate details must match a certificate on hello cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="9b140-139">*ServerCertThumbprint* é a impressão digital de saudação do certificado do servidor de saudação instalado em nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b140-139">*ServerCertThumbprint* is hello thumbprint of hello server certificate installed on hello cluster nodes.</span></span> <span data-ttu-id="9b140-140">*FindValue* é a impressão digital de saudação do certificado de cliente Olá administrador.</span><span class="sxs-lookup"><span data-stu-id="9b140-140">*FindValue* is hello thumbprint of hello admin client certificate.</span></span>
<span data-ttu-id="9b140-141">Quando os parâmetros de saudação são preenchidos, comando Olá aparência Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="9b140-141">When hello parameters are filled in, hello command looks like hello following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-tooa-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="9b140-142">Conecte-se tooa cluster seguro usando o Active Directory do Windows</span><span class="sxs-lookup"><span data-stu-id="9b140-142">Connect tooa secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="9b140-143">Se o cluster autônomo é implantado usando a segurança do AD, conecte-se toohello cluster acrescentando comutador hello "WindowsCredential".</span><span class="sxs-lookup"><span data-stu-id="9b140-143">If your standalone cluster is deployed using AD security, connect toohello cluster by appending hello switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-tooa-cluster-using-hello-fabricclient-apis"></a><span data-ttu-id="9b140-144">Conecte-se o cluster tooa usando Olá FabricClient APIs</span><span class="sxs-lookup"><span data-stu-id="9b140-144">Connect tooa cluster using hello FabricClient APIs</span></span>
<span data-ttu-id="9b140-145">Olá SDK do Service Fabric fornece Olá [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) classe para gerenciamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="9b140-145">hello Service Fabric SDK provides hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="9b140-146">Olá toouse FabricClient APIs, obter Olá pacote Microsoft.ServiceFabric NuGet.</span><span class="sxs-lookup"><span data-stu-id="9b140-146">toouse hello FabricClient APIs, get hello Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-tooan-unsecure-cluster"></a><span data-ttu-id="9b140-147">Conecte-se o cluster não segura tooan</span><span class="sxs-lookup"><span data-stu-id="9b140-147">Connect tooan unsecure cluster</span></span>

<span data-ttu-id="9b140-148">tooconnect tooa segura cluster remoto, crie uma instância de FabricClient e forneça o endereço de cluster hello:</span><span class="sxs-lookup"><span data-stu-id="9b140-148">tooconnect tooa remote unsecured cluster, create a FabricClient instance and provide hello cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="9b140-149">Para o código que é executado a partir de um cluster, por exemplo, em um serviço confiável, crie um FabricClient *sem* especificando o endereço de cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9b140-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying hello cluster address.</span></span> <span data-ttu-id="9b140-150">FabricClient conecta-se gerenciamento local toohello gateway no código de saudação do nó hello está sendo executado, evitando um salto extra na rede.</span><span class="sxs-lookup"><span data-stu-id="9b140-150">FabricClient connects toohello local management gateway on hello node hello code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="9b140-151">Conecte-se tooa cluster segura usando um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="9b140-151">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="9b140-152">Olá nós cluster Olá devem ter certificados válidos cujo nome comum ou nome DNS na rede SAN é exibido no hello [RemoteCommonNames propriedade](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) definida em [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="9b140-152">hello nodes in hello cluster must have valid certificates whose common name or DNS name in SAN appears in hello [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="9b140-153">Esse processo a seguir habilita a autenticação mútua entre o cliente hello e nós de cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="9b140-153">Following this process enables mutual authentication between hello client and hello cluster nodes.</span></span>

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

### <a name="connect-tooa-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="9b140-154">Conecte-se tooa cluster seguro usando o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9b140-154">Connect tooa secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="9b140-155">Olá seguindo o exemplo usa o Active Directory do Azure para certificado de cliente de identidade e servidor para a identidade do servidor.</span><span class="sxs-lookup"><span data-stu-id="9b140-155">hello following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="9b140-156">Uma janela de caixa de diálogo aparece automaticamente para entrada interativa ao conectar o cluster toohello.</span><span class="sxs-lookup"><span data-stu-id="9b140-156">A dialog window automatically pops up for interactive sign-in upon connecting toohello cluster.</span></span>

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

### <a name="connect-tooa-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="9b140-157">Conecte-se tooa cluster seguro não interativamente usando o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9b140-157">Connect tooa secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="9b140-158">Olá exemplo a seguir se baseia no ActiveDirectory, versão: 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="9b140-158">hello following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="9b140-159">Para saber mais sobre aquisição de token do AAD, consulte [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="9b140-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

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

### <a name="connect-tooa-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="9b140-160">Conecte-se o cluster seguro tooa sem conhecimento prévio de metadados usando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b140-160">Connect tooa secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="9b140-161">Olá, exemplo a seguir usa a aquisição de token não interativo, mas hello mesma abordagem pode ser usado toobuild uma experiência de aquisição de token interativo personalizado.</span><span class="sxs-lookup"><span data-stu-id="9b140-161">hello following example uses non-interactive token acquisition, but hello same approach can be used toobuild a custom interactive token acquisition experience.</span></span> <span data-ttu-id="9b140-162">Olá Active Directory do Azure metadados necessários para aquisição de token é lido de configuração de cluster.</span><span class="sxs-lookup"><span data-stu-id="9b140-162">hello Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

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

## <a name="connect-tooa-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="9b140-163">Conecte-se tooa cluster seguro usando o Gerenciador do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9b140-163">Connect tooa secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="9b140-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) para um determinado cluster, aponte seu navegador para:</span><span class="sxs-lookup"><span data-stu-id="9b140-164">tooreach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="9b140-165">a URL completa Olá também está disponível no painel de essentials de cluster Olá de saudação portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="9b140-165">hello full URL is also available in hello cluster essentials pane of hello Azure portal.</span></span>

### <a name="connect-tooa-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="9b140-166">Conecte-se tooa cluster seguro usando o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="9b140-166">Connect tooa secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="9b140-167">tooconnect tooa cluster protegido por AAD, aponte seu navegador para:</span><span class="sxs-lookup"><span data-stu-id="9b140-167">tooconnect tooa cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="9b140-168">Você automaticamente ser solicitado toolog com AAD.</span><span class="sxs-lookup"><span data-stu-id="9b140-168">You are automatically be prompted toolog in with AAD.</span></span>

### <a name="connect-tooa-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="9b140-169">Conecte-se tooa cluster segura usando um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="9b140-169">Connect tooa secure cluster using a client certificate</span></span>

<span data-ttu-id="9b140-170">tooconnect tooa cluster protegido com certificados, aponte seu navegador para:</span><span class="sxs-lookup"><span data-stu-id="9b140-170">tooconnect tooa cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="9b140-171">Você automaticamente ser solicitado tooselect um certificado de cliente.</span><span class="sxs-lookup"><span data-stu-id="9b140-171">You are automatically be prompted tooselect a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-hello-remote-computer"></a><span data-ttu-id="9b140-172">Configurar um certificado de cliente no computador remoto Olá</span><span class="sxs-lookup"><span data-stu-id="9b140-172">Set up a client certificate on hello remote computer</span></span>
<span data-ttu-id="9b140-173">Pelo menos dois certificados devem ser usados para proteger o cluster hello, um certificado de cluster e servidor de saudação e outro para acesso para cliente.</span><span class="sxs-lookup"><span data-stu-id="9b140-173">At least two certificates should be used for securing hello cluster, one for hello cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="9b140-174">É recomendável que você também use certificados secundários e certificados de acesso para cliente adicionais.</span><span class="sxs-lookup"><span data-stu-id="9b140-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="9b140-175">a comunicação entre um cliente e um nó de cluster usando Olá toosecure segurança de certificado, você primeiro precisa tooobtain e instale o certificado de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="9b140-175">toosecure hello communication between a client and a cluster node using certificate security, you first need tooobtain and install hello client certificate.</span></span> <span data-ttu-id="9b140-176">certificado Olá pode ser instalado em hello (Meu) repositório pessoal do computador local hello ou do usuário atual do hello.</span><span class="sxs-lookup"><span data-stu-id="9b140-176">hello certificate can be installed into hello Personal (My) store of hello local computer or hello current user.</span></span>  <span data-ttu-id="9b140-177">Impressão digital de saudação do certificado do servidor de saudação também é necessário para que hello cliente pode autenticar cluster hello.</span><span class="sxs-lookup"><span data-stu-id="9b140-177">You also need hello thumbprint of hello server certificate so that hello client can authenticate hello cluster.</span></span>

<span data-ttu-id="9b140-178">Execute Olá tooset de cmdlet do PowerShell backup do certificado de cliente Olá no computador de saudação do qual você acessar o cluster Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="9b140-178">Run hello following PowerShell cmdlet tooset up hello client certificate on hello computer from which you access hello cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="9b140-179">Se for um certificado autoassinado, você precisa tooimport-lo "pessoas confiáveis" da máquina tooyour armazenar antes de usar este cluster do certificado tooconnect tooa segura.</span><span class="sxs-lookup"><span data-stu-id="9b140-179">If it is a self-signed certificate, you need tooimport it tooyour machine's "trusted people" store before you can use this certificate tooconnect tooa secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="9b140-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9b140-180">Next steps</span></span>

* [<span data-ttu-id="9b140-181">Processo de atualização de Cluster de Malha do Serviço e as suas expectativas</span><span class="sxs-lookup"><span data-stu-id="9b140-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="9b140-182">Gerenciando aplicativos da Malha do Serviço no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9b140-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="9b140-183">Introdução ao modelo de Integridade da Malha de Serviço</span><span class="sxs-lookup"><span data-stu-id="9b140-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="9b140-184">Segurança do aplicativo e RunAs</span><span class="sxs-lookup"><span data-stu-id="9b140-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="9b140-185">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="9b140-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
