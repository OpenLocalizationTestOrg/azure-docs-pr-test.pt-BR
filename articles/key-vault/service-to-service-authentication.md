---
title: "Autenticação serviço a serviço no Azure Key Vault usando o .NET"
description: Use a biblioteca Microsoft.Azure.Services.AppAuthentication para se autenticar no Azure Key Vault usando o .NET.
keywords: "credenciais de local de autenticação do Azure Key Vault"
author: lleonard-msft
manager: mbaldwin
services: key-vault
ms.author: alleonar
ms.date: 11/15/2017
ms.topic: article
ms.prod: 
ms.service: microsoft-keyvault
ms.technology: 
ms.assetid: 4be434c4-0c99-4800-b775-c9713c973ee9
ms.openlocfilehash: bff4b15ca2f1c985c4b4e27d159adaa5fd039553
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="service-to-service-authentication-to-azure-key-vault-using-net"></a>Autenticação serviço a serviço no Azure Key Vault usando o .NET

Para se autenticar no Azure Key Vault, você precisa de uma credencial do Azure AD (Active Directory), seja ele um segredo compartilhado ou um certificado. O gerenciamento de credenciais como essas pode ser difícil e é tentador agrupar as credenciais em um aplicativo incluindo-os nos arquivos de configuração ou de origem.

O `Microsoft.Azure.Services.AppAuthentication` para a biblioteca .NET simplifica esse problema. Ele usa as credenciais do desenvolvedor para autenticação durante o desenvolvimento local. Quando a solução é implantada posteriormente no Azure, a biblioteca alterna automaticamente para as credenciais do aplicativo.  

O uso das credenciais do desenvolvedor durante o desenvolvimento local é mais seguro, porque você não precisa criar credenciais do Azure AD nem compartilhar credenciais entre desenvolvedores.

A biblioteca `Microsoft.Azure.Services.AppAuthentication` gerencia a autenticação automaticamente, que, por sua vez, permite que você se concentre em sua solução, em vez de nas credenciais.

A biblioteca `Microsoft.Azure.Services.AppAuthentication` dá suporte ao desenvolvimento local com o Microsoft Visual Studio, a CLI do Azure ou a Autenticação Integrada do Azure AD. Quando implantada nos Serviços de Aplicativos do Azure ou em uma VM (Máquina Virtual) do Azure, a biblioteca usa automaticamente o [MSI](/azure/active-directory/msi-overview) (Managed Service Identity). Nenhuma alteração de configuração ou de código é necessária. A biblioteca também dá suporte ao uso direto das [credenciais do cliente](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-authenticate-service-principal) do Azure AD quando o MSI não está disponível ou quando o contexto de segurança do desenvolvedor não pode ser determinado durante o desenvolvimento local.

<a name="asal"></a>
## <a name="using-the-library"></a>Usando a biblioteca

Para aplicativos .NET, a maneira mais simples de trabalhar com um MSI (Managed Service Identity) é por meio do pacote `Microsoft.Azure.Services.AppAuthentication`. Estas são algumas dicas para começar:

1. Adicione uma referência ao pacote NuGet [Microsoft.Azure.Services.AppAuthentication](https://www.nuget.org/packages/Microsoft.Azure.Services.AppAuthentication) no aplicativo.

2. Adicione os códigos a seguir:

    ``` csharp
    using Microsoft.Azure.Services.AppAuthentication;
    using Microsoft.Azure.KeyVault;

    // ...

    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(
    azureServiceTokenProvider.KeyVaultTokenCallback));

    // or

    var azureServiceTokenProvider = new AzureServiceTokenProvider();
    string accessToken = await azureServiceTokenProvider.GetAccessTokenAsync(
       "https://management.azure.com/").ConfigureAwait(false);
    ```

A classe `AzureServiceTokenProvider` armazena em cache o token na memória e recupera-o do Azure AD logo antes da expiração. Consequentemente, você não precisa mais verificar a expiração antes de chamar o método `GetAccessTokenAsync`. Basta chamar o método quando desejar usar o token. 

O método `GetAccessTokenAsync` exige um identificador de recurso. Para saber mais, consulte [Quais serviços do Azure dão suporte ao Managed Service Identity](https://docs.microsoft.com/azure/active-directory/msi-overview#which-azure-services-support-managed-service-identity).


<a name="samples"></a>
## <a name="samples"></a>Exemplos

As seguintes amostras mostram a biblioteca `Microsoft.Azure.Services.AppAuthentication` em ação:

1. [Usar um MSI (Managed Service Identity) para recuperar um segredo do Azure Key Vault em tempo de execução](https://github.com/Azure-Samples/app-service-msi-keyvault-dotnet)

2. [Implantar de forma programática um modelo do Azure Resource Manager de uma VM do Azure com um MSI](https://github.com/Azure-Samples/windowsvm-msi-arm-dotnet).

3. [Usar uma amostra do .NET Core e o MSI para chamar os serviços do Azure de uma VM Linux do Azure](https://github.com/Azure-Samples/linuxvm-msi-keyvault-arm-dotnet/).


<a name="local"></a>
## <a name="local-development-authentication"></a>Autenticação de desenvolvimento local

Para o desenvolvimento local, há dois cenários de autenticação principais:

- [Autenticação nos serviços do Azure](#authenticating-to-azure-services)
- [Autenticação em serviços personalizados](#authenticating-to-custom-services)

Aqui, você conhecerá os requisitos para cada cenário e as ferramentas com suporte.


### <a name="authenticating-to-azure-services"></a>Autenticação nos serviços do Azure

Os computadores locais não dão suporte ao MSI (Managed Service Identity).  Como resultado, a biblioteca `Microsoft.Azure.Services.AppAuthentication` usa suas credenciais de desenvolvedor para ser executada no ambiente de desenvolvimento local. Quando a solução é implantada no Azure, a biblioteca usa o MSI para alternar para um fluxo de concessão de credenciais do cliente do OAuth 2.0.  Isso significa que você pode testar o mesmo código local e remotamente sem se preocupar.

Para o desenvolvimento local, o `AzureServiceTokenProvider` busca tokens usando o **Visual Studio**, a **CLI (interface de linha de comando) do Azure** ou a **Autenticação Integrada do Azure AD**. Cada opção é tentada na sequência e a biblioteca usa a primeira opção bem-sucedida. Se nenhuma opção funcionar, uma exceção `AzureServiceTokenProviderException` será gerada com informações detalhadas.

### <a name="authenticating-with-visual-studio"></a>Autenticando com o Visual Studio

Para usar o Virtual Studio, verifique se:

1. Você instalou o [Visual Studio 2017 v15.5](https://blogs.msdn.microsoft.com/visualstudio/2017/10/11/visual-studio-2017-version-15-5-preview/) ou posterior.

2. A [extensão de Autenticação do Aplicativo para o Visual Studio](https://go.microsoft.com/fwlink/?linkid=862354) está instalada.
 
3. Você se conectou ao Visual Studio e selecionou uma conta a ser usada para desenvolvimento local. Use **Ferramentas**&nbsp;>&nbsp;**Opções**&nbsp;>&nbsp;**Autenticação de Serviço do Azure** para escolher uma conta de desenvolvimento local. 

Caso tenha problemas com o Visual Studio, como erros referentes ao arquivo do provedor de token, leia estas etapas com atenção. 

Também pode ser necessário autenticar novamente o token de desenvolvedor.  Para fazer isso, acesse **Ferramentas**&nbsp;>&nbsp;**Opções**>**Azure&nbsp;Serviço&nbsp;Autenticação** e procure um link **Autenticar novamente** na conta selecionada.  Selecione-o para autenticar. 

### <a name="authenticating-with-azure-cli"></a>Autenticando com a CLI do Azure

Para usar a CLI do Azure para o desenvolvimento local:

1. Instale a [CLI v2.0.12 do Azure](/cli/azure/install-azure-cli) ou posterior. Atualize as versões anteriores. 

2. Use **az login** para entrar no Azure.

Use `az account get-access-token` para verificar o acesso.  Caso receba um erro, verifique se a Etapa 1 foi concluída com êxito. 

Se a CLI do Azure não estiver instalada no diretório padrão, você poderá receber um erro relatando que o `AzureServiceTokenProvider` não pode localizar o caminho para a CLI do Azure.  Use a variável de ambiente **AzureCLIPath** para definir a pasta de instalação da CLI do Azure. `AzureServiceTokenProvider` adiciona o diretório especificado na variável de ambiente **AzureCLIPath** à variável de ambiente **Path**, quando necessário.

Caso esteja conectado à CLI do Azure com várias contas ou caso sua conta tenha acesso a várias assinaturas, você precisará especificar a assinatura específica a ser usada.  Para fazer isso, use:

```
az account set --subscription <subscription-id>
```

Esse comando gera a saída apenas em caso de falha.  Para verificar as configurações de conta atuais, use:

```
az account list
```

### <a name="authenticating-with-azure-ad-integrate-authentication"></a>Autenticando com a autenticação integrada do Azure AD

Para usar a autenticação do Azure AD, verifique se:

- O Active Directory local [é sincronizado com o Azure AD](/azure/active-directory/connect/active-directory-aadconnect).

- O código está sendo executado em um computador ingressado no domínio.


### <a name="authenticating-to-custom-services"></a>Autenticação em serviços personalizados

Quando um serviço chama os serviços do Azure, as etapas anteriores funcionam porque os serviços do Azure permitem o acesso a usuários e aplicativos.  

Ao criar um serviço que chama um serviço personalizado, use as credenciais do cliente do Azure AD para autenticação de desenvolvimento local.  Há duas opções: 

1.  Use uma entidade de serviço para entrar no Azure:

    1.  [Crie uma entidade de serviço](/cli/azure/create-an-azure-service-principal-azure-cli).

    2.  Use a CLI do Azure para entrar:

        ```
        az login --service-principal -u <principal-id> --password <password>
           --tenant <tenant-id> --allow-no-subscriptions
        ```

        Como a entidade de serviço pode não ter acesso a uma assinatura, use o argumento `--allow-no-subscriptions`.

2.  Use variáveis de ambiente para especificar detalhes da entidade de serviço.  Para obter detalhes, consulte [Executando o aplicativo usando uma entidade de serviço](#running-the-application-using-a-service-principal).

Depois de entrar no Azure, o `AzureServiceTokenProvider` usa a entidade de serviço para recuperar um token para o desenvolvimento local.

Isso se aplica apenas ao desenvolvimento local. Quando a solução é implantada no Azure, a biblioteca alterna para a autenticação do MSI.

<a name="msi"></a>
## <a name="running-the-application-using-a-managed-service-identity"></a>Executando o aplicativo usando um Managed Service Identity 

Quando você executa o código em um Serviço de Aplicativo do Azure ou em uma VM do Azure com o MSI habilitado, a biblioteca usa automaticamente o Managed Service Identity. Nenhuma alteração de código é necessária. 


<a name="sp"></a>
## <a name="running-the-application-using-a-service-principal"></a>Executando o aplicativo usando uma Entidade de Serviço 

Pode ser necessário criar uma credencial do Cliente do Azure AD para autenticar. Exemplos comuns incluem:

1. O código é executado em um ambiente de desenvolvimento local, mas não na identidade do desenvolvedor.  O Service Fabric, por exemplo, usa a [conta NetworkService](/azure/service-fabric/service-fabric-application-secret-management) para o desenvolvimento local.
 
2. O código é executado em um ambiente de desenvolvimento local e você se autentica em um serviço personalizado e, portanto, não pode usar sua identidade de desenvolvedor. 
 
3. O código é executado em um recurso de computação do Azure que ainda não dá suporte ao Managed Service Identity, como o Lote do Azure.

Para usar um certificado para entrar no Azure AD:

1. Crie um [certificado de entidade de serviço](/azure/azure-resource-manager/resource-group-authenticate-service-principal). 

2. Implante o certificado no repositório _LocalMachine_ ou _CurrentUser_. 

3. Defina uma variável de ambiente chamada **AzureServicesAuthConnectionString** como:

    ```
    RunAs=App;AppId={AppId};TenantId={TenantId};CertificateThumbprint={Thumbprint};
          CertificateStoreLocation={LocalMachine or CurrentUser}.
    ```
 
    Substitua _{AppId}_, _{TenantId}_ e _{Thumbprint}_ pelos valores gerados na Etapa 1.

    **CertificateStoreLocation** deve ser _CurrentUser_ ou _LocalMachine_, com base no plano de implantação.

4. Execute o aplicativo. 

Para entrar usando uma credencial de segredo compartilhado do Azure AD:

1. Crie uma [entidade de serviço com uma senha](/azure/azure-resource-manager/resource-group-authenticate-service-principal) e conceda acesso a ela ao Key Vault. 

2. Defina uma variável de ambiente chamada **AzureServicesAuthConnectionString** como:

    ```
    RunAs=App;AppId={AppId};TenantId={TenantId};AppKey={ClientSecret}. 
    ```

    Substitua _{AppId}_, _{TenantId}_ e _{ClientSecret}_ pelos valores gerados na Etapa 1.

3. Execute o aplicativo. 

Depois que tudo estiver configurado corretamente, nenhuma alteração de código adicional será necessária.  O `AzureServiceTokenProvider` usa a variável de ambiente e o certificado para se autenticar no Azure AD. 

<a name="connectionstrings"></a>
## <a name="connection-string-support"></a>Suporte à cadeia de conexão

Por padrão, o `AzureServiceTokenProvider` usa vários métodos para recuperar um token. 

Para controlar o processo, use uma cadeia de conexão passada para o construtor `AzureServiceTokenProvider` ou especificada na variável de ambiente *AzureServicesAuthConnectionString*. 

Há suporte para as seguintes opções:

| Opção de&nbsp;cadeia de&nbsp;conexão | Cenário | Comentários|
|:--------------------------------|:------------------------|:----------------------------|
| `RunAs=Developer; DeveloperTool=AzureCli` | Desenvolvimento local | O AzureServiceTokenProvider usa a AzureCli para obter um token. |
| `RunAs=Developer; DeveloperTool=VisualStudio` | Desenvolvimento local | O AzureServiceTokenProvider usa o Visual Studio para obter um token. |
| `RunAs=CurrentUser;` | Desenvolvimento local | O AzureServiceTokenProvider usa a Autenticação Integrada do Azure AD para obter um token. |
| `RunAs=App;` | Managed Service Identity | O AzureServiceTokenProvider usa o Managed Service Identity para obter um token. |
| `RunAs=App;AppId={AppId};TenantId={TenantId};CertificateThumbprint`<br>`   ={Thumbprint};CertificateStoreLocation={LocalMachine or CurrentUser}`  | Entidade de serviço | O `AzureServiceTokenProvider` usa um certificado para obter um token do Azure AD. |
| `RunAs=App;AppId={AppId};TenantId={TenantId};`<br>`   CertificateSubjectName={Subject};CertificateStoreLocation=`<br>`   {LocalMachine or CurrentUser}` | Entidade de serviço | O `AzureServiceTokenProvider` usa um certificado para obter um token do Azure AD|
| `RunAs=App;AppId={AppId};TenantId={TenantId};AppKey={ClientSecret}` | Entidade de serviço |O `AzureServiceTokenProvider` usa um segredo para obter um token do Azure AD. |


## <a name="next-steps"></a>Próximas etapas

- Saiba mais sobre o [Managed Service Identity](/azure/app-service/app-service-managed-service-identity).

- Saiba mais sobre maneiras diferentes de [autenticar e autorizar aplicativos](/azure/app-service/app-service-authentication-overview).

- Saiba mais sobre os [cenários de autenticação](/azure/active-directory/develop/active-directory-authentication-scenarios#web-browser-to-web-application) do Azure AD.