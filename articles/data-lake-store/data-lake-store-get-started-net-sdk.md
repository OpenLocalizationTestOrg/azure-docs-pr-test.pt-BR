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
# <a name="get-started-with-azure-data-lake-store-using-net-sdk"></a>Introdução ao Repositório Azure Data Lake usando o SDK do .NET
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [SDK .NET](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [CLI 2.0 do Azure](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Saiba como Olá toouse [repositório .NET SDK do Azure Data Lake](https://docs.microsoft.com/dotnet/api/overview/azure/data-lake-store?view=azure-dotnet) tooperform de operações básicas, como criar pastas, carregar e baixar arquivos de dados, etc. Para obter mais informações sobre o Data Lake, veja [Azure Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Pré-requisitos
* **Visual Studio 2013, 2015 ou 2017**. instruções de saudação abaixo usam o Visual Studio 2015 atualização 2.

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Conta do Repositório Azure Data Lake**. Para obter instruções sobre como toocreate uma conta, consulte [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)

* **Criar um aplicativo do Azure Active Directory**. Você pode usar Olá AD do Azure tooauthenticate Olá repositório Data Lake aplicativo com o Azure AD. Há diferentes abordagens tooauthenticate com o AD do Azure, que são **autenticação do usuário final** ou **autenticação de serviço a serviço**. Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).

## <a name="create-a-net-application"></a>Criar um aplicativo .NET
1. Abra o Visual Studio e crie um aplicativo de console.
2. De saudação **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.
3. De **novo projeto**, digite ou selecione Olá valores a seguir:

   | Propriedade | Valor |
   | --- | --- |
   | Categoria |Modelos/Visual C#/Windows |
   | Modelo |Aplicativo de console |
   | Nome |CreateADLApplication |
4. Clique em **Okey** toocreate projeto de saudação.
5. Adicione projeto de tooyour de pacotes de Nuget hello.

   1. Nome do projeto Olá no Gerenciador de soluções de saudação de mouse e clique em **gerenciar pacotes NuGet**.
   2. Em Olá **Nuget Package Manager** guia, certifique-se de que **origem do pacote** está definido muito**nuget.org** e **incluir pré-lançamento** caixa de seleção é selecionada.
   3. Procurar e instalar Olá pacotes do NuGet a seguir:

      * `Microsoft.Azure.Management.DataLake.Store` - este tutorial usa a versão 2.1.3-preview.
      * `Microsoft.Rest.ClientRuntime.Azure.Authentication` - este tutorial usa a versão v2.2.12.

        ![Adicionar uma origem de Nuget](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Criar uma nova conta do Azure Data Lake")
   4. Olá fechar **Nuget Package Manager**.
6. Abra **Program.cs**, excluir o código existente do hello e, em seguida, inclua Olá instruções tooadd referências toonamespaces a seguir.

        using System;
        using System.IO;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
        using System.Threading;

        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;
        using Microsoft.Rest.Azure.Authentication;

7. Declare variáveis Olá conforme mostrado abaixo e forneça valores de saudação para o nome do repositório Data Lake e nome do grupo de recursos de saudação já existe. Além disso, certifique-se de saudação local caminho e nome de arquivo fornecidas aqui deverá existir no computador de saudação. Adicione Olá trecho de código a seguir depois de declarações de namespace hello.

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

Olá restantes seções Olá artigo, você pode ver como toouse Olá disponível .NET métodos tooperform as operações, como autenticação, o carregamento do arquivo, etc.

## <a name="authentication"></a>Autenticação

### <a name="if-you-are-using-end-user-authentication-recommended-for-this-tutorial"></a>Se você estiver usando autenticação de usuário final (recomendada para este tutorial)

Use com um tooauthenticate de aplicativo nativo existente do AD do Azure seu aplicativo **interativamente**, que significa que você será solicitado tooenter suas credenciais do Azure.

Para facilidade de uso, Olá trecho abaixo usa valores padrão para a ID de cliente e redirecione o URI que funcionará com nenhuma assinatura do Azure. toohelp você concluir este tutorial mais rapidamente, é recomendável que usar essa abordagem. No trecho Olá abaixo, forneça apenas o valor de saudação para sua ID de locatário. Você pode recuperar usando instruções Olá fornecidas em [criar um aplicativo do Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).

    // User login via interactive popup
    // Use hello client ID of an existing AAD Web application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());
    var tenant_id = "<AAD_tenant_id>"; // Replace this string with hello user's Azure Active Directory tenant ID
    var nativeClientApp_clientId = "1950a258-227b-4e31-a9cf-717495945fc2";
    var activeDirectoryClientSettings = ActiveDirectoryClientSettings.UsePromptOnly(nativeClientApp_clientId, new Uri("urn:ietf:wg:oauth:2.0:oob"));
    var creds = UserTokenProvider.LoginWithPromptAsync(tenant_id, activeDirectoryClientSettings).Result;

Algumas coisas tooknow sobre este trecho de código acima:

* toohelp concluir o tutorial hello mais rápido, este trecho de código usa um AD do Azure ID de cliente e de domínio que está disponível por padrão para todas as assinaturas do Azure. Portanto, você pode **usar o trecho de código como está em seu aplicativo**.
* No entanto, se você quiser toouse seu próprio domínio de AD do Azure e ID de cliente do aplicativo, você deve criar um aplicativo nativo do AD do Azure e, em seguida, use Olá AD do Azure locatário ID, ID de cliente e URI de redirecionamento para o aplicativo hello criado. Veja [Criar um aplicativo do Active Directory para autenticação do usuário final no Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) para obter instruções.

### <a name="if-you-are-using-service-to-service-authentication-with-client-secret"></a>Se você está usando autenticação serviço a serviço com o segredo do cliente
Olá trecho de código a seguir pode ser usado tooauthenticate seu aplicativo **não interativamente**, usando o segredo do cliente Olá / chave para uma entidade de segurança do aplicativo / serviço. Use-o com um ”aplicativo Web” do Azure AD. Para obter instruções sobre como o aplicativo de web toocreate Olá AD do Azure e como tooretrieve Olá ID do cliente e o segredo do cliente necessários no trecho de saudação abaixo, consulte [criar um aplicativo do Active Directory para autenticação de serviço a serviço com dados Repositório Lake](data-lake-store-authenticate-using-active-directory.md).

    // Service principal / appplication authentication with client secret / key
    // Use hello client ID of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientSecret = "<AAD-application-client-secret>";
    var clientCredential = new ClientCredential(webApp_clientId, clientSecret);
    var creds = await ApplicationTokenProvider.LoginSilentAsync(domain, clientCredential);

### <a name="if-you-are-using-service-to-service-authentication-with-certificate"></a>Se você está usando a autenticação serviço a serviço com certificado

Como uma terceira opção, hello trecho de código a seguir pode ser usado tooauthenticate seu aplicativo **não interativamente**, usando o certificado de saudação para um aplicativo do Active Directory do Azure / serviço principal. Use-a com um [aplicativo do Azure AD com certificados](../azure-resource-manager/resource-group-authenticate-service-principal.md) existente.

    // Service principal / application authentication with certificate
    // Use hello client ID and certificate of an existing AAD "Web App" application.
    SynchronizationContext.SetSynchronizationContext(new SynchronizationContext());

    var domain = "<AAD-directory-domain>";
    var webApp_clientId = "<AAD-application-clientid>";
    var clientCert = <AAD-application-client-certificate>
    var clientAssertionCertificate = new ClientAssertionCertificate(webApp_clientId, clientCert);
    var creds = await ApplicationTokenProvider.LoginSilentWithCertificateAsync(domain, clientAssertionCertificate);

## <a name="create-client-objects"></a>Criar objetos de cliente
Olá trecho a seguir cria sistema de arquivos e a conta do repositório Data Lake Olá objetos de cliente, que são usados tooissue solicitações toohello do serviço.

    // Create client objects and set hello subscription ID
    _adlsClient = new DataLakeStoreAccountManagementClient(creds) { SubscriptionId = _subId };
    _adlsFileSystemClient = new DataLakeStoreFileSystemManagementClient(creds);

## <a name="list-all-data-lake-store-accounts-within-a-subscription"></a>Listar todas as contas do Data Lake Store em uma assinatura
Olá trecho a seguir lista todas as contas do repositório Data Lake dentro de uma determinada assinatura do Azure.

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

## <a name="create-a-directory"></a>Criar um diretório
Olá trecho a seguir mostra um `CreateDirectory` método que você pode usar toocreate um diretório dentro de uma conta do repositório Data Lake.

    // Create a directory
    public static async Task CreateDirectory(string path)
    {
        await _adlsFileSystemClient.FileSystem.MkdirsAsync(_adlsAccountName, path);
    }

## <a name="upload-a-file"></a>Carregar um arquivo
Olá trecho a seguir mostra um `UploadFile` método que você pode usar tooupload arquivos tooa conta de repositório Data Lake.

    // Upload a file
    public static void UploadFile(string srcFilePath, string destFilePath, bool force = true)
    {
        _adlsFileSystemClient.FileSystem.UploadFile(_adlsAccountName, srcFilePath, destFilePath, overwrite:force);
    }

Olá SDK dá suporte a recursiva upload e download entre um caminho de arquivo local e um caminho de arquivo do repositório Data Lake.    

## <a name="get-file-or-directory-info"></a>Obter informações do arquivo ou diretório
Olá trecho a seguir mostra um `GetItemInfo` método que você pode usar tooretrieve informações sobre um arquivo ou diretório disponível no repositório Data Lake.

    // Get file or directory info
    public static async Task<FileStatusProperties> GetItemInfo(string path)
    {
        return await _adlsFileSystemClient.FileSystem.GetFileStatusAsync(_adlsAccountName, path).FileStatus;
    }

## <a name="list-file-or-directories"></a>Listar arquivos ou diretórios
Olá trecho a seguir mostra um `ListItem` método que pode usar toolist Olá arquivos e diretórios em uma conta do repositório Data Lake.

    // List files and directories
    public static List<FileStatusProperties> ListItems(string directoryPath)
    {
        return _adlsFileSystemClient.FileSystem.ListFileStatus(_adlsAccountName, directoryPath).FileStatuses.FileStatus.ToList();
    }

## <a name="concatenate-files"></a>Concatenar arquivos
Olá trecho a seguir mostra um `ConcatenateFiles` método que você usa arquivos de tooconcatenate.

    // Concatenate files
    public static Task ConcatenateFiles(string[] srcFilePaths, string destFilePath)
    {
        await _adlsFileSystemClient.FileSystem.ConcatAsync(_adlsAccountName, destFilePath, srcFilePaths);
    }

## <a name="append-tooa-file"></a>Anexar o arquivo tooa
Olá trecho a seguir mostra um `AppendToFile` método que você usar anexar o arquivo de tooa de dados já armazenado em uma conta do repositório Data Lake.

    // Append toofile
    public static async Task AppendToFile(string path, string content)
    {
        using (var stream = new MemoryStream(Encoding.UTF8.GetBytes(content)))
        {
            await _adlsFileSystemClient.FileSystem.AppendAsync(_adlsAccountName, path, stream);
        }
    }

## <a name="download-a-file"></a>Baixar um arquivo
Olá trecho a seguir mostra um `DownloadFile` método que você use toodownload um arquivo de uma conta do repositório Data Lake.

    // Download file
    public static void DownloadFile(string srcFilePath, string destFilePath)
    {
         _adlsFileSystemClient.FileSystem.DownloadFile(_adlsAccountName, srcFilePath, destFilePath);
    }

## <a name="next-steps"></a>Próximas etapas
* [Proteger dados no Repositório Data Lake](data-lake-store-secure-data.md)
* [Usar a Análise Data Lake do Azure com o Repositório Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usar o Azure HDInsight com o Repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Referência do SDK do .NET do Azure Data Lake Store](https://docs.microsoft.com/dotnet/api/?view=azuremgmtdatalakestore-2.1.0-preview&term=DataLake.Store)
* [Referência do REST do Azure Data Lake Store](https://msdn.microsoft.com/library/mt693424.aspx)
