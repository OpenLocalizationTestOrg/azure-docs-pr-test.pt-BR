---
title: "Conectar com segurança a um cluster do Azure Service Fabric | Microsoft Docs"
description: "Descreve como autenticar o acesso do cliente a um cluster do Service Fabric e como proteger a comunicação entre clientes e um cluster."
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
ms.openlocfilehash: d6a13ceb8ccd9207ecacc166247535d496d5dec7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-to-a-secure-cluster"></a><span data-ttu-id="ca782-103">Conectar a um cluster seguro</span><span class="sxs-lookup"><span data-stu-id="ca782-103">Connect to a secure cluster</span></span>

<span data-ttu-id="ca782-104">Quando um cliente se conecta a um nó de cluster do Service Fabric, ele pode ser autenticado e uma comunicação segura pode ser estabelecida com a segurança de certificado ou o AAD (Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="ca782-104">When a client connects to a Service Fabric cluster node, the client can be authenticated and secure communication established using certificate security or Azure Active Directory (AAD).</span></span> <span data-ttu-id="ca782-105">Essa autenticação garante que somente usuários autorizados possam acessar o cluster e os aplicativos implantados e executar tarefas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="ca782-105">This authentication ensures that only authorized users can access the cluster and deployed applications and perform management tasks.</span></span>  <span data-ttu-id="ca782-106">A segurança de certificado ou do AAD deve ter sido previamente habilitada no cluster quando o cluster foi criado.</span><span class="sxs-lookup"><span data-stu-id="ca782-106">Certificate or AAD security must have been previously enabled on the cluster when the cluster was created.</span></span>  <span data-ttu-id="ca782-107">Para obter mais informações sobre cenários de segurança de cluster, consulte [Segurança de cluster](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="ca782-107">For more information on cluster security scenarios, see [Cluster security](service-fabric-cluster-security.md).</span></span> <span data-ttu-id="ca782-108">Se você estiver se conectando a um cluster protegido com certificados, [configure o certificado do cliente](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) no computador que se conecta ao cluster.</span><span class="sxs-lookup"><span data-stu-id="ca782-108">If you are connecting to a cluster secured with certificates, [set up the client certificate](service-fabric-connect-to-secure-cluster.md#connectsecureclustersetupclientcert) on the computer that connects to the cluster.</span></span> 

<a id="connectsecureclustercli"></a> 

## <a name="connect-to-a-secure-cluster-using-azure-service-fabric-cli-sfctl"></a><span data-ttu-id="ca782-109">Conectar-se a um cluster seguro usando a CLI do Azure Service Fabric (sfctl)</span><span class="sxs-lookup"><span data-stu-id="ca782-109">Connect to a secure cluster using Azure Service Fabric CLI (sfctl)</span></span>

<span data-ttu-id="ca782-110">Há algumas maneiras diferentes de se conectar a um cluster seguro usando a CLI do Service Fabric (sfctl).</span><span class="sxs-lookup"><span data-stu-id="ca782-110">There are a few different ways to connect to a secure cluster using the Service Fabric CLI (sfctl).</span></span> <span data-ttu-id="ca782-111">Ao usar um certificado do cliente para autenticação, os detalhes do certificado devem corresponder a um certificado implantado para os nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="ca782-111">When using a client certificate for authentication, the certificate details must match a certificate deployed to the cluster nodes.</span></span> <span data-ttu-id="ca782-112">Se o certificado tiver Autoridades de Certificação (CAs), você precisa especificar as Autoridades de Certificação confiáveis.</span><span class="sxs-lookup"><span data-stu-id="ca782-112">If your certificate has Certificate Authorities (CAs), you need to additionally specify the trusted CAs.</span></span>

<span data-ttu-id="ca782-113">Você pode se conectar a um cluster usando o comando `sfctl cluster select`.</span><span class="sxs-lookup"><span data-stu-id="ca782-113">You can connect to a cluster using the `sfctl cluster select` command.</span></span>

<span data-ttu-id="ca782-114">Certificados de cliente podem ser especificados em dois modos diferentes, como um par de certificados e chaves ou como um arquivo pem individual.</span><span class="sxs-lookup"><span data-stu-id="ca782-114">Client certificates can be specified in two different fashions, either as a cert and key pair, or as a single pem file.</span></span> <span data-ttu-id="ca782-115">Para arquivos `pem` protegidos por senha, você será solicitado automaticamente para inserir a senha.</span><span class="sxs-lookup"><span data-stu-id="ca782-115">For password protected `pem` files, you will be prompted automatically to enter the password.</span></span>

<span data-ttu-id="ca782-116">Para especificar o certificado do cliente como um arquivo pem, especifique o caminho do arquivo no argumento `--pem`.</span><span class="sxs-lookup"><span data-stu-id="ca782-116">To specify the client certificate as a pem file, specify the file path in the `--pem` argument.</span></span> <span data-ttu-id="ca782-117">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ca782-117">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem
```

<span data-ttu-id="ca782-118">Arquivos pem protegidos por senha solicitarão a senha antes da execução de qualquer comando.</span><span class="sxs-lookup"><span data-stu-id="ca782-118">Password protected pem files will prompt for password prior to running any command.</span></span>

<span data-ttu-id="ca782-119">Para especificar um certificado, o par de chaves usa os argumentos `--cert` e `--key` para especificar os caminhos de arquivo para cada arquivo respectivo.</span><span class="sxs-lookup"><span data-stu-id="ca782-119">To specify a cert, key pair use the `--cert` and `--key` arguments to specify the file paths to each respective file.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --cert ./client.crt --key ./keyfile.key
```

<span data-ttu-id="ca782-120">Às vezes, os certificados usados para proteger clusters de teste ou de desenvolvimento falham na validação do certificado.</span><span class="sxs-lookup"><span data-stu-id="ca782-120">Sometimes certificates used to secure test or dev clusters fail certificate validation.</span></span> <span data-ttu-id="ca782-121">Para ignorar a verificação do certificado, especifique a opção `--no-verify`.</span><span class="sxs-lookup"><span data-stu-id="ca782-121">To bypass certificate verification, specify the `--no-verify` option.</span></span> <span data-ttu-id="ca782-122">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ca782-122">For example:</span></span>

> [!WARNING]
> <span data-ttu-id="ca782-123">Não use a opção `no-verify` ao se conectar aos clusters de produção do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ca782-123">Do not use the `no-verify` option when connecting to production Service Fabric clusters.</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --no-verify
```

<span data-ttu-id="ca782-124">Além disso, você pode especificar caminhos para diretórios de certificados de CA confiáveis ou certificados individuais.</span><span class="sxs-lookup"><span data-stu-id="ca782-124">In addition, you can specify paths to directories of trusted CA certs, or individual certs.</span></span> <span data-ttu-id="ca782-125">Para especificar esses caminhos, use o argumento `--ca`.</span><span class="sxs-lookup"><span data-stu-id="ca782-125">To specify these paths, use the `--ca` argument.</span></span> <span data-ttu-id="ca782-126">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ca782-126">For example:</span></span>

```azurecli
sfctl cluster select --endpoint https://testsecurecluster.com:19080 --pem ./client.pem --ca ./trusted_ca
```

<span data-ttu-id="ca782-127">Depois de se conectar, você poderá [executar outros comandos sfctl](service-fabric-cli.md) para interagir com o cluster.</span><span class="sxs-lookup"><span data-stu-id="ca782-127">After you connect, you should be able to [run other sfctl commands](service-fabric-cli.md) to interact with the cluster.</span></span>

<a id="connectsecurecluster"></a>

## <a name="connect-to-a-cluster-using-powershell"></a><span data-ttu-id="ca782-128">Conectar a um cluster usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ca782-128">Connect to a cluster using PowerShell</span></span>
<span data-ttu-id="ca782-129">Antes de executar operações em um cluster por meio do PowerShell, primeiro estabeleça uma conexão com o cluster.</span><span class="sxs-lookup"><span data-stu-id="ca782-129">Before you perform operations on a cluster through PowerShell, first establish a connection to the cluster.</span></span> <span data-ttu-id="ca782-130">A conexão do cluster é usada para todos os comandos posteriores na sessão do PowerShell específica.</span><span class="sxs-lookup"><span data-stu-id="ca782-130">The cluster connection is used for all subsequent commands in the given PowerShell session.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="ca782-131">Conectar a um cluster não seguro</span><span class="sxs-lookup"><span data-stu-id="ca782-131">Connect to an unsecure cluster</span></span>

<span data-ttu-id="ca782-132">Para se conectar a um cluster não seguro, forneça o endereço do ponto de extremidade do cluster ao comando **Connect-ServiceFabricCluster**:</span><span class="sxs-lookup"><span data-stu-id="ca782-132">To connect to an unsecure cluster, provide the cluster endpoint address to the **Connect-ServiceFabricCluster** command:</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 
```

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="ca782-133">Conectar-se a um cluster seguro usando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca782-133">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="ca782-134">Para se conectar a um cluster seguro que usa o Azure Active Directory para autorizar o acesso de administrador de cluster, forneça a impressão digital do certificado do cluster e use o sinalizador *AzureActiveDirectory*.</span><span class="sxs-lookup"><span data-stu-id="ca782-134">To connect to a secure cluster that uses Azure Active Directory to authorize cluster administrator access, provide the cluster certificate thumbprint and use the *AzureActiveDirectory* flag.</span></span>  

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
-ServerCertThumbprint <Server Certificate Thumbprint> `
-AzureActiveDirectory
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="ca782-135">Conectar-se a um cluster seguro usando um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="ca782-135">Connect to a secure cluster using a client certificate</span></span>
<span data-ttu-id="ca782-136">Execute o comando do PowerShell a seguir para se conectar a um cluster seguro que usa certificados de cliente para autorizar o acesso do administrador.</span><span class="sxs-lookup"><span data-stu-id="ca782-136">Run the following PowerShell command to connect to a secure cluster that uses client certificates to authorize administrator access.</span></span> <span data-ttu-id="ca782-137">Forneça a impressão digital do certificado do cluster, bem como a impressão digital do certificado de cliente que recebeu permissões para o gerenciamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="ca782-137">Provide the cluster certificate thumbprint and the thumbprint of the client certificate that has been granted permissions for cluster management.</span></span> <span data-ttu-id="ca782-138">Os detalhes do certificado devem corresponder a um certificado em nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="ca782-138">The certificate details must match a certificate on the cluster nodes.</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="ca782-139">*ServerCertThumbprint* é a impressão digital do certificado do servidor instalado nos nós do cluster.</span><span class="sxs-lookup"><span data-stu-id="ca782-139">*ServerCertThumbprint* is the thumbprint of the server certificate installed on the cluster nodes.</span></span> <span data-ttu-id="ca782-140">*FindValue* é a impressão digital do certificado de cliente do administrador.</span><span class="sxs-lookup"><span data-stu-id="ca782-140">*FindValue* is the thumbprint of the admin client certificate.</span></span>
<span data-ttu-id="ca782-141">Quando os parâmetros são preenchidos, o comando se parece com o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca782-141">When the parameters are filled in, the command looks like the following example:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint clustername.westus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint A8136758F4AB8962AF2BF3F27921BE1DF67F4326 `
          -FindType FindByThumbprint -FindValue 71DE04467C9ED0544D021098BCD44C71E183414E `
          -StoreLocation CurrentUser -StoreName My
```

### <a name="connect-to-a-secure-cluster-using-windows-active-directory"></a><span data-ttu-id="ca782-142">Conectar-se a um cluster seguro usando o Windows Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca782-142">Connect to a secure cluster using Windows Active Directory</span></span>
<span data-ttu-id="ca782-143">Se o cluster autônomo for implantado usando a segurança do AD, conecte-se ao cluster adicionando a opção "WindowsCredential".</span><span class="sxs-lookup"><span data-stu-id="ca782-143">If your standalone cluster is deployed using AD security, connect to the cluster by appending the switch "WindowsCredential".</span></span>

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -WindowsCredential
```

<a id="connectsecureclusterfabricclient"></a>

## <a name="connect-to-a-cluster-using-the-fabricclient-apis"></a><span data-ttu-id="ca782-144">Conectar-se a um cluster usando as APIs de FabricClient</span><span class="sxs-lookup"><span data-stu-id="ca782-144">Connect to a cluster using the FabricClient APIs</span></span>
<span data-ttu-id="ca782-145">O SDK do Service Fabric fornece a classe [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) para o gerenciamento de cluster.</span><span class="sxs-lookup"><span data-stu-id="ca782-145">The Service Fabric SDK provides the [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) class for cluster management.</span></span> <span data-ttu-id="ca782-146">Para usar as APIs FabricClient, obtenha o pacote do Microsoft.ServiceFabric NuGet.</span><span class="sxs-lookup"><span data-stu-id="ca782-146">To use the FabricClient APIs, get the Microsoft.ServiceFabric NuGet package.</span></span>

### <a name="connect-to-an-unsecure-cluster"></a><span data-ttu-id="ca782-147">Conectar a um cluster não seguro</span><span class="sxs-lookup"><span data-stu-id="ca782-147">Connect to an unsecure cluster</span></span>

<span data-ttu-id="ca782-148">Para se conectar a um cluster não seguro remoto, crie uma instância de FabricClient e forneça o endereço do cluster:</span><span class="sxs-lookup"><span data-stu-id="ca782-148">To connect to a remote unsecured cluster, create a FabricClient instance and provide the cluster address:</span></span>

```csharp
FabricClient fabricClient = new FabricClient("clustername.westus.cloudapp.azure.com:19000");
```

<span data-ttu-id="ca782-149">Para o código executado por meio de um cluster, por exemplo, em um Serviço Confiável, crie um FabricClient *sem* especificar o endereço do cluster.</span><span class="sxs-lookup"><span data-stu-id="ca782-149">For code that is running from within a cluster, for example, in a Reliable Service, create a FabricClient *without* specifying the cluster address.</span></span> <span data-ttu-id="ca782-150">FabricClient conecta-se ao gateway de gerenciamento local no nó em que o código está sendo executado, evitando um salto extra na rede.</span><span class="sxs-lookup"><span data-stu-id="ca782-150">FabricClient connects to the local management gateway on the node the code is currently running on, avoiding an extra network hop.</span></span>

```csharp
FabricClient fabricClient = new FabricClient();
```

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="ca782-151">Conectar-se a um cluster seguro usando um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="ca782-151">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="ca782-152">Os nós no cluster devem ter certificados válidos cujo nome comum ou nome DNS no SAN aparece na [propriedade RemoteCommonNames](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) definida em [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="ca782-152">The nodes in the cluster must have valid certificates whose common name or DNS name in SAN appears in the [RemoteCommonNames property](https://docs.microsoft.com/dotnet/api/system.fabric.x509credentials#System_Fabric_X509Credentials_RemoteCommonNames) set on [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient).</span></span> <span data-ttu-id="ca782-153">Seguir esse processo habilita a autenticação mútua entre o cliente e o nó de cluster.</span><span class="sxs-lookup"><span data-stu-id="ca782-153">Following this process enables mutual authentication between the client and the cluster nodes.</span></span>

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

### <a name="connect-to-a-secure-cluster-interactively-using-azure-active-directory"></a><span data-ttu-id="ca782-154">Conectar-se a um cluster seguro de forma interativa usando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca782-154">Connect to a secure cluster interactively using Azure Active Directory</span></span>

<span data-ttu-id="ca782-155">O exemplo e a seguir usa o Azure Active Directory para a identidade do cliente e o certificado do servidor para a identidade do servidor.</span><span class="sxs-lookup"><span data-stu-id="ca782-155">The following example uses Azure Active Directory for client identity and server certificate for server identity.</span></span>

<span data-ttu-id="ca782-156">Uma janela de diálogo aparece automaticamente para entrada interativa após a conexão com o cluster.</span><span class="sxs-lookup"><span data-stu-id="ca782-156">A dialog window automatically pops up for interactive sign-in upon connecting to the cluster.</span></span>

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

### <a name="connect-to-a-secure-cluster-non-interactively-using-azure-active-directory"></a><span data-ttu-id="ca782-157">Conectar-se a um cluster seguro de forma não interativa usando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca782-157">Connect to a secure cluster non-interactively using Azure Active Directory</span></span>

<span data-ttu-id="ca782-158">O exemplo a seguir tem base no Microsoft.IdentityModel.Clients.ActiveDirectory, Versão: 2.19.208020213.</span><span class="sxs-lookup"><span data-stu-id="ca782-158">The following example relies on Microsoft.IdentityModel.Clients.ActiveDirectory, Version: 2.19.208020213.</span></span>

<span data-ttu-id="ca782-159">Para saber mais sobre aquisição de token do AAD, consulte [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span><span class="sxs-lookup"><span data-stu-id="ca782-159">For more information on AAD token acquisition, see [Microsoft.IdentityModel.Clients.ActiveDirectory](https://msdn.microsoft.com/library/microsoft.identitymodel.clients.activedirectory.aspx).</span></span>

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

### <a name="connect-to-a-secure-cluster-without-prior-metadata-knowledge-using-azure-active-directory"></a><span data-ttu-id="ca782-160">Conectar-se a um cluster seguro sem conhecimento prévio de metadados usando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca782-160">Connect to a secure cluster without prior metadata knowledge using Azure Active Directory</span></span>

<span data-ttu-id="ca782-161">O exemplo a seguir usa a aquisição de token não interativa, mas a mesma abordagem pode ser usada para criar uma experiência de aquisição de token interativa personalizada.</span><span class="sxs-lookup"><span data-stu-id="ca782-161">The following example uses non-interactive token acquisition, but the same approach can be used to build a custom interactive token acquisition experience.</span></span> <span data-ttu-id="ca782-162">Os metadados necessários do Azure Active Directory para a aquisição de token são lidos na configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="ca782-162">The Azure Active Directory metadata needed for token acquisition is read from cluster configuration.</span></span>

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

## <a name="connect-to-a-secure-cluster-using-service-fabric-explorer"></a><span data-ttu-id="ca782-163">Conectar-se a um cluster seguro usando o Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="ca782-163">Connect to a secure cluster using Service Fabric Explorer</span></span>
<span data-ttu-id="ca782-164">Para alcançar o [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) para determinado cluster, aponte o navegador para:</span><span class="sxs-lookup"><span data-stu-id="ca782-164">To reach [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) for a given cluster, point your browser to:</span></span>

`http://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="ca782-165">A URL completa também está disponível no painel essencial do cluster do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca782-165">The full URL is also available in the cluster essentials pane of the Azure portal.</span></span>

### <a name="connect-to-a-secure-cluster-using-azure-active-directory"></a><span data-ttu-id="ca782-166">Conectar-se a um cluster seguro usando o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ca782-166">Connect to a secure cluster using Azure Active Directory</span></span>

<span data-ttu-id="ca782-167">Para se conectar a um cluster protegido com o AAD, aponte seu navegador para:</span><span class="sxs-lookup"><span data-stu-id="ca782-167">To connect to a cluster that is secured with AAD, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="ca782-168">Você deverá automaticamente fazer logon no AAD.</span><span class="sxs-lookup"><span data-stu-id="ca782-168">You are automatically be prompted to log in with AAD.</span></span>

### <a name="connect-to-a-secure-cluster-using-a-client-certificate"></a><span data-ttu-id="ca782-169">Conectar-se a um cluster seguro usando um certificado de cliente</span><span class="sxs-lookup"><span data-stu-id="ca782-169">Connect to a secure cluster using a client certificate</span></span>

<span data-ttu-id="ca782-170">Para conectar-se a um cluster protegido com certificados, aponte seu navegador para:</span><span class="sxs-lookup"><span data-stu-id="ca782-170">To connect to a cluster that is secured with certificates, point your browser to:</span></span>

`https://<your-cluster-endpoint>:19080/Explorer`

<span data-ttu-id="ca782-171">Você deverá automaticamente selecionar um certificado do cliente.</span><span class="sxs-lookup"><span data-stu-id="ca782-171">You are automatically be prompted to select a client certificate.</span></span>

<a id="connectsecureclustersetupclientcert"></a>
## <a name="set-up-a-client-certificate-on-the-remote-computer"></a><span data-ttu-id="ca782-172">Configurar um certificado de cliente no computador remoto</span><span class="sxs-lookup"><span data-stu-id="ca782-172">Set up a client certificate on the remote computer</span></span>
<span data-ttu-id="ca782-173">Pelo menos dois certificados devem ser usados para proteger o cluster, um para o cluster e certificado do servidor e outro para acesso para cliente.</span><span class="sxs-lookup"><span data-stu-id="ca782-173">At least two certificates should be used for securing the cluster, one for the cluster and server certificate and another for client access.</span></span>  <span data-ttu-id="ca782-174">É recomendável que você também use certificados secundários e certificados de acesso para cliente adicionais.</span><span class="sxs-lookup"><span data-stu-id="ca782-174">We recommend that you also use additional secondary certificates and client access certificates.</span></span>  <span data-ttu-id="ca782-175">Para proteger a comunicação entre um cliente e um nó de cluster usando a segurança de certificado, você precisa primeiro obter e instalar o certificado do cliente.</span><span class="sxs-lookup"><span data-stu-id="ca782-175">To secure the communication between a client and a cluster node using certificate security, you first need to obtain and install the client certificate.</span></span> <span data-ttu-id="ca782-176">O certificado pode ser instalado no repositório Pessoal (Meu) do computador local ou o usuário atual.</span><span class="sxs-lookup"><span data-stu-id="ca782-176">The certificate can be installed into the Personal (My) store of the local computer or the current user.</span></span>  <span data-ttu-id="ca782-177">Você também precisa da impressão digital do certificado do servidor para que o cliente possa autenticar o cluster.</span><span class="sxs-lookup"><span data-stu-id="ca782-177">You also need the thumbprint of the server certificate so that the client can authenticate the cluster.</span></span>

<span data-ttu-id="ca782-178">Execute o cmdlet do PowerShell a seguir para configurar o certificado do cliente no computador do qual você acessa o cluster.</span><span class="sxs-lookup"><span data-stu-id="ca782-178">Run the following PowerShell cmdlet to set up the client certificate on the computer from which you access the cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
        -Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

<span data-ttu-id="ca782-179">Se o certificado for autoassinado, você precisará importá-lo para o repositório de "pessoas confiáveis" do computador antes de poder usá-lo para se conectar a um cluster seguro.</span><span class="sxs-lookup"><span data-stu-id="ca782-179">If it is a self-signed certificate, you need to import it to your machine's "trusted people" store before you can use this certificate to connect to a secure cluster.</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\TrustedPeople `
-FilePath C:\docDemo\certs\DocDemoClusterCert.pfx `
-Password (ConvertTo-SecureString -String test -AsPlainText -Force)
```

## <a name="next-steps"></a><span data-ttu-id="ca782-180">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ca782-180">Next steps</span></span>

* [<span data-ttu-id="ca782-181">Processo de atualização de Cluster de Malha do Serviço e as suas expectativas</span><span class="sxs-lookup"><span data-stu-id="ca782-181">Service Fabric Cluster upgrade process and expectations from you</span></span>](service-fabric-cluster-upgrade.md)
* [<span data-ttu-id="ca782-182">Gerenciando aplicativos da Malha do Serviço no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ca782-182">Managing your Service Fabric applications in Visual Studio</span></span>](service-fabric-manage-application-in-visual-studio.md)
* [<span data-ttu-id="ca782-183">Introdução ao modelo de Integridade da Malha de Serviço</span><span class="sxs-lookup"><span data-stu-id="ca782-183">Service Fabric Health model introduction</span></span>](service-fabric-health-introduction.md)
* [<span data-ttu-id="ca782-184">Segurança do aplicativo e RunAs</span><span class="sxs-lookup"><span data-stu-id="ca782-184">Application Security and RunAs</span></span>](service-fabric-application-runas-security.md)
* [<span data-ttu-id="ca782-185">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ca782-185">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
