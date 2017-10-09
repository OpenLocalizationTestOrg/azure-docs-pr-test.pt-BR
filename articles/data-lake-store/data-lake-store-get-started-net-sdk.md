---
title: "aplicativos de toodevelop de SDK .NET aaaUse Olá no repositório Azure Data Lake | Microsoft Docs"
description: "Use o SDK .NET do Azure Data Lake repositório toocreate uma conta do repositório Data Lake e executar operações básicas em Olá repositório Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ea57d5a9-2929-4473-9d30-08227912aba7
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/09/2017
ms.author: nitinme
ms.openlocfilehash: cb3a1dfb2f6379f728069d66b0ee77ce0f838fe7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a><span data-ttu-id="56a58-103">Introdução ao Repositório Azure Data Lake usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="56a58-103">Get started with Azure Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="56a58-104">Portal</span><span class="sxs-lookup"><span data-stu-id="56a58-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="56a58-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="56a58-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="56a58-106">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="56a58-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="56a58-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="56a58-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="56a58-108">API REST</span><span class="sxs-lookup"><span data-stu-id="56a58-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="56a58-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="56a58-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="56a58-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="56a58-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="56a58-111">Python</span><span class="sxs-lookup"><span data-stu-id="56a58-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="56a58-112">Saiba como Olá toouse [repositório .NET SDK do Azure Data Lake](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform de operações básicas, como criar pastas, carregar e baixar arquivos de dados, etc. Para obter mais informações sobre o Data Lake, veja [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="56a58-112">Learn how toouse hello [Azure Data Lake Store .NET SDK](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="56a58-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="56a58-113">Prerequisites</span></span>
* <span data-ttu-id="56a58-114">**Visual Studio 2013, 2015 ou 2017**.</span><span class="sxs-lookup"><span data-stu-id="56a58-114">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="56a58-115">instruções de saudação abaixo usam o Visual Studio 2015 atualização 2.</span><span class="sxs-lookup"><span data-stu-id="56a58-115">hello instructions below use Visual Studio 2015 Update 2.</span></span>

* <span data-ttu-id="56a58-116">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="56a58-116">**An Azure subscription**.</span></span> <span data-ttu-id="56a58-117">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="56a58-117">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="56a58-118">**Conta do Repositório Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="56a58-118">**Azure Data Lake Store account**.</span></span> <span data-ttu-id="56a58-119">Para obter instruções sobre como toocreate uma conta, consulte [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="56a58-119">For instructions on how toocreate an account, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>

* <span data-ttu-id="56a58-120">**Criar um aplicativo do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="56a58-120">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="56a58-121">Você pode usar Olá AD do Azure tooauthenticate Olá repositório Data Lake aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56a58-121">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="56a58-122">Há diferentes abordagens tooauthenticate com o AD do Azure, que são **autenticação do usuário final** ou **autenticação de serviço a serviço**.</span><span class="sxs-lookup"><span data-stu-id="56a58-122">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="56a58-123">Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="56a58-123">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="56a58-124">Criar um aplicativo .NET</span><span class="sxs-lookup"><span data-stu-id="56a58-124">Create a .NET application</span></span>
1. <span data-ttu-id="56a58-125">Abra o Visual Studio e crie um aplicativo de console.</span><span class="sxs-lookup"><span data-stu-id="56a58-125">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="56a58-126">De saudação **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.</span><span class="sxs-lookup"><span data-stu-id="56a58-126">From hello **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="56a58-127">De **novo projeto**, digite ou selecione Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="56a58-127">From **New Project**, type or select hello following values:</span></span>

   | <span data-ttu-id="56a58-128">Propriedade</span><span class="sxs-lookup"><span data-stu-id="56a58-128">Property</span></span> | <span data-ttu-id="56a58-129">Valor</span><span class="sxs-lookup"><span data-stu-id="56a58-129">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="56a58-130">Categoria</span><span class="sxs-lookup"><span data-stu-id="56a58-130">Category</span></span> |<span data-ttu-id="56a58-131">Modelos/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="56a58-131">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="56a58-132">Modelo</span><span class="sxs-lookup"><span data-stu-id="56a58-132">Template</span></span> |<span data-ttu-id="56a58-133">Aplicativo de console</span><span class="sxs-lookup"><span data-stu-id="56a58-133">Console Application</span></span> |
   | <span data-ttu-id="56a58-134">Nome</span><span class="sxs-lookup"><span data-stu-id="56a58-134">Name</span></span> |<span data-ttu-id="56a58-135">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="56a58-135">CreateADLApplication</span></span> |
4. <span data-ttu-id="56a58-136">Clique em **Okey** toocreate projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="56a58-136">Click **OK** toocreate hello project.</span></span>
5. <span data-ttu-id="56a58-137">Adicione projeto de tooyour de pacotes de Nuget hello.</span><span class="sxs-lookup"><span data-stu-id="56a58-137">Add hello Nuget packages tooyour project.</span></span>

   1. <span data-ttu-id="56a58-138">Nome do projeto Olá no Gerenciador de soluções de saudação de mouse e clique em **gerenciar pacotes NuGet**.</span><span class="sxs-lookup"><span data-stu-id="56a58-138">Right-click hello project name in hello Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="56a58-139">Em Olá **Nuget Package Manager** guia, certifique-se de que **origem do pacote** está definido muito**nuget.org** e **incluir pré-lançamento** caixa de seleção é selecionada.</span><span class="sxs-lookup"><span data-stu-id="56a58-139">In hello **Nuget Package Manager** tab, make sure that **Package source** is set too**nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="56a58-140">Procurar e instalar Olá pacotes do NuGet a seguir:</span><span class="sxs-lookup"><span data-stu-id="56a58-140">Search for and install hello following NuGet packages:</span></span>

      * <span data-ttu-id="56a58-141">`Microsoft.Azure.Management.DataLake.Store` - este tutorial usa a versão 2.1.3-preview.</span><span class="sxs-lookup"><span data-stu-id="56a58-141">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="56a58-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - este tutorial usa a versão v2.2.12.</span><span class="sxs-lookup"><span data-stu-id="56a58-142">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="56a58-143">![Adicionar uma origem de Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Criar uma nova conta do Azure Data Lake")</span><span class="sxs-lookup"><span data-stu-id="56a58-143">![Add a Nuget source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="56a58-144">Olá fechar **Nuget Package Manager**.</span><span class="sxs-lookup"><span data-stu-id="56a58-144">Close hello **Nuget Package Manager**.</span></span>
6. <span data-ttu-id="56a58-145">Abra **Program.cs**, excluir o código existente do hello e, em seguida, inclua Olá instruções tooadd referências toonamespaces a seguir.</span><span class="sxs-lookup"><span data-stu-id="56a58-145">Open **Program.cs**, delete hello existing code, and then include hello following statements tooadd references toonamespaces.</span></span>

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. <span data-ttu-id="56a58-146">Declare variáveis Olá conforme mostrado abaixo e forneça valores de saudação para o nome do repositório Data Lake e nome do grupo de recursos de saudação já existe.</span><span class="sxs-lookup"><span data-stu-id="56a58-146">Declare hello variables as shown below, and provide hello values for Data Lake Store name and hello resource group name that already exist.</span></span> <span data-ttu-id="56a58-147">Além disso, certifique-se de saudação local caminho e nome de arquivo fornecidas aqui deverá existir no computador de saudação.</span><span class="sxs-lookup"><span data-stu-id="56a58-147">Also, make sure hello local path and file name you provide here must exist on hello computer.</span></span> <span data-ttu-id="56a58-148">Adicione Olá trecho de código a seguir depois de declarações de namespace hello.</span><span class="sxs-lookup"><span data-stu-id="56a58-148">Add hello following code snippet after hello namespace declarations.</span></span>

        namespace SdkSample
        {
            class Program
            {
                private static DataLakeStoreAccountManagementClient _adlsClient;
                private static DataLakeStoreFileSystemManagementClient _adlsFileSystemClient;

                private static string _adlsAccountName;
                private static string _resourceGroupName;
                private static string _location;
                private static string _subId;

                private static void Main(string[] args)
                {
                    _adlsAccountName = "<DATA-LAKE-STORE-NAME>"; // TODO: Replace this value with hello name of your existing Data Lake Store account.
                    _resourceGroupName = "<RESOURCE-GROUP-NAME>"; // TODO: Replace this value with hello name of hello resource group containing your Data Lake Store account.
                    _location = "East US 2";
                    _subId = "<SUBSCRIPTION-ID>";

                    string localFolderPath = @"C:\local_path\"; // TODO: Make sure this exists and can be overwritten.
                    string localFilePath = Path.Combine(localFolderPath, "file.txt"); // TODO: Make sure this exists and can be overwritten.
                    string remoteFolderPath = "/data_lake_path/";
                    string remoteFilePath = Path.Combine(remoteFolderPath, "file.txt");
                }
            }
        }

<span data-ttu-id="56a58-149">Olá restantes seções Olá artigo, você pode ver como toouse Olá disponível .NET métodos tooperform as operações, como autenticação, o carregamento do arquivo, etc.</span><span class="sxs-lookup"><span data-stu-id="56a58-149">In hello remaining sections of hello article, you can see how toouse hello available .NET methods tooperform operations such as authentication, file upload, etc.</span></span>

## <a name="authentication"></a><span data-ttu-id="56a58-150">Autenticação</span><span class="sxs-lookup"><span data-stu-id="56a58-150">Authentication</span></span>

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a><span data-ttu-id="56a58-151">Se você estiver usando autenticação de usuário final (recomendada para este tutorial)</span><span class="sxs-lookup"><span data-stu-id="56a58-151">If you are using end-user authentication (recommended for this tutorial)</span></span>

<span data-ttu-id="56a58-152">Use com um tooauthenticate de aplicativo nativo existente do AD do Azure seu aplicativo **interativamente**, que significa que você será solicitado tooenter suas credenciais do Azure.</span><span class="sxs-lookup"><span data-stu-id="56a58-152">Use this with an existing Azure AD native application tooauthenticate your application **interactively**, which means you will be prompted tooenter your Azure credentials.</span></span>

<span data-ttu-id="56a58-153">Para facilidade de uso, Olá trecho abaixo usa valores padrão para a ID de cliente e redirecione o URI que funcionará com nenhuma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="56a58-153">For ease of use, hello snippet below uses default values for client ID and redirect URI that will work with any Azure subscription.</span></span> <span data-ttu-id="56a58-154">toohelp você concluir este tutorial mais rapidamente, é recomendável que usar essa abordagem.</span><span class="sxs-lookup"><span data-stu-id="56a58-154">toohelp you complete this tutorial faster, we recommend you use this approach.</span></span> <span data-ttu-id="56a58-155">No trecho Olá abaixo, forneça apenas o valor de saudação para sua ID de locatário.</span><span class="sxs-lookup"><span data-stu-id="56a58-155">In hello snippet below, just provide hello value for your tenant ID.</span></span> <span data-ttu-id="56a58-156">Você pode recuperar usando instruções Olá fornecidas em [criar um aplicativo do Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="56a58-156">You can retrieve it using hello instructions provided at [Create an Active Directory Application](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

<span data-ttu-id="56a58-157">Algumas coisas tooknow sobre este trecho de código acima:</span><span class="sxs-lookup"><span data-stu-id="56a58-157">A couple of things tooknow about this snippet above:</span></span>

* <span data-ttu-id="56a58-158">toohelp concluir o tutorial hello mais rápido, este trecho de código usa um AD do Azure ID de cliente e de domínio que está disponível por padrão para todas as assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="56a58-158">toohelp you complete hello tutorial faster, this snippet uses an an Azure AD domain and client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="56a58-159">Portanto, você pode **usar o trecho de código como está em seu aplicativo**.</span><span class="sxs-lookup"><span data-stu-id="56a58-159">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="56a58-160">No entanto, se você quiser toouse seu próprio domínio de AD do Azure e ID de cliente do aplicativo, você deve criar um aplicativo nativo do AD do Azure e, em seguida, use Olá AD do Azure locatário ID, ID de cliente e URI de redirecionamento para o aplicativo hello criado.</span><span class="sxs-lookup"><span data-stu-id="56a58-160">However, if you do want toouse your own Azure AD domain and application client ID, you must create an Azure AD native application and then use hello Azure AD tenant ID, client ID, and redirect URI for hello application you created.</span></span> <span data-ttu-id="56a58-161">Veja [Criar um aplicativo do Active Directory para autenticação do usuário final no Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="56a58-161">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a><span data-ttu-id="56a58-162">Se você está usando autenticação serviço a serviço com o segredo do cliente</span><span class="sxs-lookup"><span data-stu-id="56a58-162">If you are using service-to-service authentication with client secret</span></span>
<span data-ttu-id="56a58-163">Olá trecho de código a seguir pode ser usado tooauthenticate seu aplicativo **não interativamente**, usando o segredo do cliente Olá / chave para uma entidade de segurança do aplicativo / serviço.</span><span class="sxs-lookup"><span data-stu-id="56a58-163">hello following snippet can be used tooauthenticate your application **non-interactively**, using hello client secret / key for an application / service principal.</span></span> <span data-ttu-id="56a58-164">Use-o com um ”aplicativo Web” do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="56a58-164">Use this with an existing Azure AD "Web App" Application.</span></span> <span data-ttu-id="56a58-165">Para obter instruções sobre como o aplicativo de web toocreate Olá AD do Azure e como tooretrieve Olá ID do cliente e o segredo do cliente necessários no trecho de saudação abaixo, consulte [criar um aplicativo do Active Directory para autenticação de serviço a serviço com dados Repositório Lake](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="56a58-165">For instructions on how toocreate hello Azure AD web application and how tooretrieve hello client ID and client secret required in hello snippet below, see [Create an Active Directory Application for service-to-service authentication with Data Lake Store](data-lake-store-authenticate-using-active-directory.md).</span></span>

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a><span data-ttu-id="56a58-166">Se você está usando a autenticação serviço a serviço com certificado</span><span class="sxs-lookup"><span data-stu-id="56a58-166">If you are using service-to-service authentication with certificate</span></span>

<span data-ttu-id="56a58-167">Como uma terceira opção, hello trecho de código a seguir pode ser usado tooauthenticate seu aplicativo **não interativamente**, usando o certificado de saudação para um aplicativo do Active Directory do Azure / serviço principal.</span><span class="sxs-lookup"><span data-stu-id="56a58-167">As a third option, hello following snippet can be used tooauthenticate your application **non-interactively**, using hello certificate for an Azure Active Directory application / service principal.</span></span> <span data-ttu-id="56a58-168">Use-a com um [aplicativo do Azure AD com certificados](../azure-resource-manager/resource-group-authenticate-service-principal.md) existente.</span><span class="sxs-lookup"><span data-stu-id="56a58-168">Use this with an existing [Azure AD Application with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md).</span></span>

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a><span data-ttu-id="56a58-169">Criar objetos de cliente</span><span class="sxs-lookup"><span data-stu-id="56a58-169">Create client objects</span></span>
<span data-ttu-id="56a58-170">Olá trecho a seguir cria sistema de arquivos e a conta do repositório Data Lake Olá objetos de cliente, que são usados tooissue solicitações toohello do serviço.</span><span class="sxs-lookup"><span data-stu-id="56a58-170">hello following snippet creates hello Data Lake Store account and filesystem client objects, which are used tooissue requests toohello service.</span></span>

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a><span data-ttu-id="56a58-171">Listar todas as contas do Data Lake Store em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="56a58-171">List all Data Lake Store accounts within a subscription</span></span>
<span data-ttu-id="56a58-172">Olá trecho a seguir lista todas as contas do repositório Data Lake dentro de uma determinada assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="56a58-172">hello following snippet lists all Data Lake Store accounts within a given Azure subscription.</span></span>

    // List all ADLS accounts within hello subscription
    public static async Task<List<DataLakeStoreAccount>> ListAdlStoreAccounts()
    {
        var response = await _adlsClient.Account.ListAsync();
        var accounts = new List<DataLakeStoreAccount>(response);

        while (response.NextPageLink != null)
        {
            response = _adlsClient.Account.ListNext(response.NextPageLink);
            accounts.AddRange(response);
        }

        return accounts;
    }

## <a name="create-a-directory"></a><span data-ttu-id="56a58-173">Criar um diretório</span><span class="sxs-lookup"><span data-stu-id="56a58-173">Create a directory</span></span>
<span data-ttu-id="56a58-174">Olá trecho a seguir mostra um `CreateDirectory` método que você pode usar toocreate um diretório dentro de uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="56a58-174">hello following snippet shows a `CreateDirectory` method that you can use toocreate a directory within a Data Lake Store account.</span></span>

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a><span data-ttu-id="56a58-175">Carregar um arquivo</span><span class="sxs-lookup"><span data-stu-id="56a58-175">Upload a file</span></span>
<span data-ttu-id="56a58-176">Olá trecho a seguir mostra um `UploadFile` método que você pode usar tooupload arquivos tooa conta de repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="56a58-176">hello following snippet shows an `UploadFile` method that you can use tooupload files tooa Data Lake Store account.</span></span>

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

<span data-ttu-id="56a58-177">Olá SDK dá suporte a recursiva upload e download entre um caminho de arquivo local e um caminho de arquivo do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="56a58-177">hello SDK supports recursive upload and download between a local file path and a Data Lake Store file path.</span></span>    

## <a name="get-file-or-directory-info"></a><span data-ttu-id="56a58-178">Obter informações do arquivo ou diretório</span><span class="sxs-lookup"><span data-stu-id="56a58-178">Get file or directory info</span></span>
<span data-ttu-id="56a58-179">Olá trecho a seguir mostra um `GetItemInfo` método que você pode usar tooretrieve informações sobre um arquivo ou diretório disponível no repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="56a58-179">hello following snippet shows a `GetItemInfo` method that you can use tooretrieve information about a file or directory available in Data Lake Store.</span></span>

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a><span data-ttu-id="56a58-180">Listar arquivos ou diretórios</span><span class="sxs-lookup"><span data-stu-id="56a58-180">List file or directories</span></span>
<span data-ttu-id="56a58-181">Olá trecho a seguir mostra um `ListItem` método que pode usar toolist Olá arquivos e diretórios em uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="56a58-181">hello following snippet shows a `ListItem` method that can use toolist hello file and directories in a Data Lake Store account.</span></span>

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a><span data-ttu-id="56a58-182">Concatenar arquivos</span><span class="sxs-lookup"><span data-stu-id="56a58-182">Concatenate files</span></span>
<span data-ttu-id="56a58-183">Olá trecho a seguir mostra um `ConcatenateFiles` método que você usa arquivos de tooconcatenate.</span><span class="sxs-lookup"><span data-stu-id="56a58-183">hello following snippet shows a `ConcatenateFiles` method that you use tooconcatenate files.</span></span>

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a><span data-ttu-id="56a58-184">Anexar o arquivo tooa</span><span class="sxs-lookup"><span data-stu-id="56a58-184">Append tooa file</span></span>
<span data-ttu-id="56a58-185">Olá trecho a seguir mostra um `AppendToFile` método que você usar anexar o arquivo de tooa de dados já armazenado em uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="56a58-185">hello following snippet shows a `AppendToFile` method that you use append data tooa file already stored in a Data Lake Store account.</span></span>

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a><span data-ttu-id="56a58-186">Baixar um arquivo</span><span class="sxs-lookup"><span data-stu-id="56a58-186">Download a file</span></span>
<span data-ttu-id="56a58-187">Olá trecho a seguir mostra um `DownloadFile` método que você use toodownload um arquivo de uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="56a58-187">hello following snippet shows a `DownloadFile` method that you use toodownload a file from a Data Lake Store account.</span></span>

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a><span data-ttu-id="56a58-188">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="56a58-188">Next steps</span></span>
* [<span data-ttu-id="56a58-189">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="56a58-189">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="56a58-190">Usar a Análise Data Lake do Azure com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="56a58-190">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="56a58-191">Usar o Azure HDInsight com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="56a58-191">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="56a58-192">Referência do SDK do .NET do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="56a58-192">Data Lake Store .NET SDK Reference</span></span>](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [<span data-ttu-id="56a58-193">Referência do REST do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="56a58-193">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
