---
title: "Como salvar com segurança as configurações de aplicativo secretas para um aplicativo Web | Microsoft Docs"
description: "Como salvar com segurança salvar as configurações de aplicativo secretas, como credenciais do Azure ou chaves de API de terceiros usando o Provedor do Key Vault do ASP.NET Core, o segredo do usuário ou os construtores de configuração do .NET 4.7.1"
services: visualstudio
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 
ms.service: 
ms.workload: web, azure
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 11/09/2017
ms.author: cawa
ms.openlocfilehash: 612b8d2c36e9b46e99452e78d1b30fda03474151
ms.sourcegitcommit: b07d06ea51a20e32fdc61980667e801cb5db7333
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/08/2017
---
# <a name="securely-save-secret-application-settings-for-a-web-application"></a>Salvar com segurança as configurações de aplicativo secretas para um aplicativo Web

## <a name="overview"></a>Visão geral
Este artigo descreve como salvar com segurança os parâmetros secretos de configuração de aplicativos para aplicativos do Azure.

Tradicionalmente, todas as configurações de aplicativos Web são salvas em arquivos de configuração como Web.config. Essa prática leva a fazer check-in em configurações secretas, como credenciais de nuvem para sistemas públicos de controle do código-fonte como Github. Enquanto isso, pode ser difícil seguir a melhor prática de segurança devido à sobrecarga necessária para mudar o código-fonte e redefinir as configurações de desenvolvimento.

Para verificar se o processo de desenvolvimento é seguro, bibliotecas de ferramentas e de estruturas são criadas para salvar as configurações de aplicativo secretas com segurança com pouca ou nenhuma alteração de código-fonte.

## <a name="aspnet-and-net-core-applications"></a>Aplicativos ASP.NET e .NET Core

### <a name="save-secret-settings-in-user-secret-store-that-is-outside-of-source-control-folder"></a>Salvar configurações secretas no repositório de segredo do usuário que está fora da pasta de controle do código-fonte
Se você estiver fazendo um protótipo rápido ou não tiver acesso à Internet, comece a mover suas configurações secretas da pasta de controle do código-fonte para o repositório de segredo do usuário. O repositório de segredo do usuário é um arquivo salvo na pasta do criador de perfil de usuário, para que segredos não sejam verificados no controle do código-fonte. O diagrama a seguir demonstra como funciona o [segredo do usuário](https://docs.microsoft.com/aspnet/core/security/app-secrets?tabs=visual-studio#SecretManager).

![O segredo do usuário mantém as configurações secretas fora do controle do código-fonte](./media/vs-secure-secret-appsettings/aspnetcore-usersecret.PNG)

Se você estiver executando um aplicativo de console .NET Core, use o Key Vault para salvar seu segredo com segurança.

### <a name="save-secret-settings-in-azure-key-vault"></a>Salvar configurações secretas no Azure Key Vault
Se você estiver desenvolvendo um projeto de equipe e precisar compartilhar com segurança o código-fonte, use o [Azure Key Vault](https://azure.microsoft.com/services/key-vault/).

1. Crie um Key Vault na assinatura do Azure. Preencha todos os campos obrigatórios na interface do usuário e clique em *Criar* na parte inferior da folha

    ![Criar Azure Key Vault](./media/vs-secure-secret-appsettings/create-keyvault.PNG)

2. Conceder acesso a você e aos membros da equipe para o Key Vault. Se você tiver uma equipe grande, crie um [grupo do Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-groups-create-azure-portal) e adicione a esse grupo de segurança acesso ao Key Vault. No menu suspenso *Permissões do Segredo*, marque *Obter* e *Listar* em *Operações de Gerenciamento de Segredos*.

    ![Adicionar Política de acesso ao Key Vault](./media/vs-secure-secret-appsettings/add-keyvault-access-policy.png)

3. Adicione o segredo para o Key Vault no portal do Azure. Para definições de configuração aninhadas, substitua ':' por '-' para que o nome de segredo do Key Vault seja válido. ':' não pode ser usado no nome de um segredo do Key Vault.

    ![Adicionar segredo do Key Vault](./media/vs-secure-secret-appsettings/add-keyvault-secret.png)

4. Instale a extensão de [Autenticação de Serviços do Azure para o Visual Studio](https://go.microsoft.com/fwlink/?linkid=862354). Com essa extensão, o aplicativo pode acessar o Key Vault usando a identidade de conexão do Visual Studio.

5. Adicione os seguintes pacotes NuGet ao seu projeto:

    ```
    Microsoft.Azure.Services.AppAuthentication
    ```
6. Adicione o seguinte código ao arquivo Program.cs:

    ```csharp
    public static IWebHost BuildWebHost(string[] args) =>
        WebHost.CreateDefaultBuilder(args)
            .ConfigureAppConfiguration((ctx, builder) =>
            {
                var keyVaultEndpoint = GetKeyVaultEndpoint();
                if (!string.IsNullOrEmpty(keyVaultEndpoint))
                {
                    var azureServiceTokenProvider = new AzureServiceTokenProvider();
                    var keyVaultClient = new KeyVaultClient(
                        new KeyVaultClient.AuthenticationCallback(
                            azureServiceTokenProvider.KeyVaultTokenCallback));
                            builder.AddAzureKeyVault(
                            keyVaultEndpoint, keyVaultClient, new DefaultKeyVaultSecretManager());
                        }
                    })
                    .UseStartup<Startup>()
                    .Build();

        private static string GetKeyVaultEndpoint() => Environment.GetEnvironmentVariable("KEYVAULT_ENDPOINT");
    ```
7. Adicione a URL do Key Vault ao arquivo launchsettings.json. O nome da variável de ambiente *KEYVAULT_ENDPOINT* é definido no código que você adicionou na etapa 6.

    ![Adicionar URL do Key Vault como uma variável de ambiente do projeto](./media/vs-secure-secret-appsettings/add-keyvault-url.png)

8. Comece a depuração do projeto. Ele deve ser executado com êxito.

## <a name="aspnet-and-net-applications"></a>Aplicativos do ASP.NET e .NET

O .NET 4.7.1 é compatível com construtores de configuração de segredo e do Key Vault, que garante que os segredos podem ser movidos fora da pasta de controle do código-fonte sem alterações de código.
Para continuar, [baixe o .NET 4.7.1](https://www.microsoft.com/download/details.aspx?id=56115) e migre o seu aplicativo se ele estiver usando uma versão mais antiga do .NET Framework.

### <a name="save-secret-settings-in-a-secret-file-that-is-outside-of-source-control-folder"></a>Salvar configurações secretas no arquivo de segredo que está fora da pasta de controle do código-fonte
Se você estiver escrevendo um protótipo rápido e não quiser provisionar recursos do Azure, use esta opção.

1. Instale o pacote NuGet a seguir no seu projeto.
    ```
    Microsoft.Configuration.ConfigurationBuilders.Basic.1.0.0-alpha1.nupkg
    ```

2. Crie um arquivo semelhante ao seguinte. Salve-o em um local fora da sua pasta de projeto.

    ```xml

       <root>
              <secrets ver="1.0">
                     <secret name="secret1" value="foo_one" />
                        <secret name="secret2" value="foo_two" />
                       </secrets>
      </root>
      ```

3. Defina o arquivo secreto para ser um construtor de configuração no arquivo Web.config. Coloque esta seção antes da seção *appSettings*.

    ```xml
    <configBuilders>
        <builders>
            <add name="Secrets"
                 secretsFile="C:\Users\AppData\MyWebApplication1\secret.xml" type="Microsoft.Configuration.ConfigurationBuilders.UserSecretsConfigBuilder,
                    Microsoft.Configuration.ConfigurationBuilders, Version=1.0.0.0, Culture=neutral" />
        </builders>
    </configBuilders>
    ```

4. Especifique se a seção appSettings está usando o construtor de configuração secreta. Verifique se que há alguma entrada para a configuração secreta com valor fictício.

    ```xml
        <appSettings configBuilders="Secrets">
            <add key="webpages:Version" value="3.0.0.0" />
            <add key="webpages:Enabled" value="false" />
            <add key="ClientValidationEnabled" value="true" />
            <add key="UnobtrusiveJavaScriptEnabled" value="true" />
            <add key="secret" value="" />
        </appSettings>
    ```

5. Depure o aplicativo. Ele deve ser executado com êxito.

### <a name="save-secret-settings-in-an-azure-key-vault"></a>Salvar configurações secretas em um Azure Key Vault
Siga as instruções da seção do ASP.NET Core para configurar um Key Vault para o seu projeto.

1. Instale o pacote NuGet a seguir no seu projeto.
```
Microsoft.Configuration.ConfigurationBuilders.Azure.1.0.0-alpha1.nupkg
```

2. Defina o construtor de configuração do Key Vault em Web.config. Coloque esta seção antes da seção *appSettings*. Substitua *vaultName* para ser o nome do Key Vault se o Key Vault no Azure público ou URI completo se você estiver usando a nuvem soberana.

    ```xml
    <configSections>
        <section name="configBuilders" type="System.Configuration.ConfigurationBuildersSection, System.Configuration, Version=4.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a" restartOnExternalChanges="false" requirePermission="false" />
    </configSections>
    <configBuilders>
        <builders>
            <add name="KeyVault" vaultName="Test911" type="Microsoft.Configuration.ConfigurationBuilders.AzureKeyVaultConfigBuilder, ConfigurationBuilders, Version=1.0.0.0, Culture=neutral" />
        </builders>
    </configBuilders>
    ```
3.  Especifique se a seção appSettings está usando o construtor de configuração do Key Vault. Verifique se que há alguma entrada para a configuração secreta com valor fictício.

    ```xml
    <appSettings configBuilders="AzureKeyVault">
        <add key="webpages:Version" value="3.0.0.0" />
        <add key="webpages:Enabled" value="false" />
        <add key="ClientValidationEnabled" value="true" />
        <add key="UnobtrusiveJavaScriptEnabled" value="true" />
        <add key="secret" value="" />
    </appSettings>
    ```

4. Comece a depuração do projeto. Ele deve ser executado com êxito.
