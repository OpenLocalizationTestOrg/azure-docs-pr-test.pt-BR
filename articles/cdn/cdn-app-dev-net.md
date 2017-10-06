---
title: aaaGet iniciado com hello Azure CDN biblioteca para .NET | Microsoft Docs
description: Saiba como toowrite .NET aplicativos toomanage CDN do Azure usando o Visual Studio.
services: cdn
documentationcenter: .net
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 63cf4101-92e7-49dd-a155-a90e54a792ca
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 9753e48c7469072cef6b2ac728e18c78121c97f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a>Introdução ao desenvolvimento de CDN do Azure
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

Você pode usar o hello [biblioteca de CDN do Azure para .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate criação e gerenciamento de perfis CDN e os pontos de extremidade.  Este tutorial orienta a criação de um aplicativo de console simples do .NET que demonstra várias operações disponíveis Olá Olá.  Este tutorial é toodescribe não se destina todos os aspectos da saudação biblioteca de CDN do Azure para .NET em detalhes.

É necessário toocomplete do Visual Studio 2015 neste tutorial.  [Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) está disponível gratuitamente para download.

> [!TIP]
> Olá [projeto concluído deste tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) está disponível para download no MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a>Crie seu projeto e adicione pacotes NuGet
Agora que podemos criar um grupo de recursos para os perfis CDN e considerando nossa perfis de CDN do Azure AD aplicativos permissão toomanage e pontos de extremidade dentro desse grupo, podemos começar criando o nosso aplicativo.

Em Visual Studio 2015, clique **arquivo**, **novo**, **projeto...**  tooopen Olá novo diálogo do projeto.  Expanda **Visual C#**, em seguida, selecione **Windows** no painel Olá Olá esquerda.  Clique em **aplicativo de Console** no painel central de saudação.  Nomeie o projeto e clique em **OK**.  

![Novo Projeto](./media/cdn-app-dev-net/cdn-new-project.png)

Nosso projeto vai toouse algumas bibliotecas do Azure contidas em pacotes do Nuget.  Vamos adicionar esses projeto toohello.

1. Clique em Olá **ferramentas** menu **Nuget Package Manager**, em seguida, **Package Manager Console**.
   
    ![Gerenciar pacotes NuGet](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. No hello Package Manager Console, execute Olá Olá de tooinstall de comando a seguir **biblioteca de autenticação do Active Directory (ADAL)**:
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. Executar Olá Olá tooinstall a seguir **biblioteca de gerenciamento do Azure CDN**:
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a>Diretivas, constantes, método principal e métodos auxiliares
Vamos estrutura básica de saudação de nosso programa gravado.

1. No guia de Program.cs hello, substitua Olá `using` diretivas na parte superior da saudação com os seguintes hello:
   
    ```csharp
    using System;
    using System.Collections.Generic;
    using Microsoft.Azure.Management.Cdn;
    using Microsoft.Azure.Management.Cdn.Models;
    using Microsoft.Azure.Management.Resources;
    using Microsoft.Azure.Management.Resources.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.Rest;
    ```
2. Precisamos toodefine algumas constantes que nossos métodos usará.  Em hello `Program` classe, mas antes do hello `Main` método, adicione o seguinte de saudação.  Ser tooreplace se espaços reservados hello, incluindo Olá  **&lt;colchetes angulares&gt;**, com seus próprios valores conforme necessário.
   
    ```csharp
    //Tenant app constants
    private const string clientID = "<YOUR CLIENT ID>";
    private const string clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    private const string authority = "https://login.microsoftonline.com/<YOUR TENANT ID>/<YOUR TENANT DOMAIN NAME>";
   
    //Application constants
    private const string subscriptionId = "<YOUR SUBSCRIPTION ID>";
    private const string profileName = "CdnConsoleApp";
    private const string endpointName = "<A UNIQUE NAME FOR YOUR CDN ENDPOINT>";
    private const string resourceGroupName = "CdnConsoleTutorial";
    private const string resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. Também no nível de classe hello, defina essas duas variáveis.  Vamos usar essas toodetermine posterior se nosso perfil e o ponto de extremidade já existem.
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. Substituir saudação `Main` método da seguinte maneira:
   
   ```csharp
   static void Main(string[] args)
   {
       //Get a token
       AuthenticationResult authResult = GetAccessToken();
   
       // Create CDN client
       CdnManagementClient cdn = new CdnManagementClient(new TokenCredentials(authResult.AccessToken))
           { SubscriptionId = subscriptionId };
   
       ListProfilesAndEndpoints(cdn);
   
       // Create CDN Profile
       CreateCdnProfile(cdn);
   
       // Create CDN Endpoint
       CreateCdnEndpoint(cdn);
   
       Console.WriteLine();
   
       // Purge CDN Endpoint
       PromptPurgeCdnEndpoint(cdn);
   
       // Delete CDN Endpoint
       PromptDeleteCdnEndpoint(cdn);
   
       // Delete CDN Profile
       PromptDeleteCdnProfile(cdn);
   
       Console.WriteLine("Press Enter tooend program.");
       Console.ReadLine();
   }
   ```
5. Alguns dos nossos outros métodos for usuário de saudação tooprompt com perguntas de "Sim/não".  Adicionar Olá toomake do método a seguir que um pouco mais fácil:
   
    ```csharp
    private static bool PromptUser(string Question)
    {
        Console.Write(Question + " (Y/N): ");
        var response = Console.ReadKey();
        Console.WriteLine();
        if (response.Key == ConsoleKey.Y)
        {
            return true;
        }
        else if (response.Key == ConsoleKey.N)
        {
            return false;
        }
        else
        {
            // They pressed something other than Y or N.  Let's ask them again.
            return PromptUser(Question);
        }
    }
    ```

Agora que a estrutura básica de saudação do programa é gravada, que deve ser criado métodos Olá chamados pelo Olá `Main` método.

## <a name="authentication"></a>Autenticação
Antes que possamos Olá biblioteca de gerenciamento do Azure CDN, precisamos tooauthenticate nosso serviço principal e obter um token de autenticação.  Esse método usa o token de saudação tooretrieve ADAL.

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority); 
    ClientCredential credential = new ClientCredential(clientID, clientSecret);
    AuthenticationResult authResult = 
        authContext.AcquireTokenAsync("https://management.core.windows.net/", credential).Result;

    return authResult;
}
```

Se você estiver usando a autenticação de usuário individual, Olá `GetAccessToken` método parecerá um pouco diferente.

> [!IMPORTANT]
> Somente use esse exemplo de código se você está escolhendo toohave autenticação de usuário individual em vez de uma entidade de serviço.
> 
> 

```csharp
private static AuthenticationResult GetAccessToken()
{
    AuthenticationContext authContext = new AuthenticationContext(authority);
    AuthenticationResult authResult = authContext.AcquireTokenAsync("https://management.core.windows.net/",
        clientID, new Uri("http://<redirect URI>"), new PlatformParameters(PromptBehavior.RefreshSession)).Result;

    return authResult;
}
```

Ser tooreplace se `<redirect URI>` com hello redirecione o URI que você inseriu quando registrou o aplicativo hello no AD do Azure.

## <a name="list-cdn-profiles-and-endpoints"></a>Relacione os perfis CDN e os pontos de extremidade
Agora estamos prontos tooperform operações de CDN.  Olá primeira coisa que nosso método faz é lista todos os perfis de saudação e pontos de extremidade em nosso grupo de recursos e se ele encontrar uma correspondência para nomes de perfil e o ponto de extremidade de saudação especificado em nossas constantes, torna Observe que para mais tarde então não tentaremos toocreate duplicatas.

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all hello CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's hello name of hello CDN profile we want toocreate!
            profileAlreadyExists = true;
        }

        //List all hello CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // hello unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a>Criar perfis CDN e pontos de extremidade
Em seguida, criaremos um perfil.

```csharp
private static void CreateCdnProfile(CdnManagementClient cdn)
{
    if (profileAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating profile {0}.", profileName);
        ProfileCreateParameters profileParms =
            new ProfileCreateParameters() { Location = resourceLocation, Sku = new Sku(SkuName.StandardVerizon) };
        cdn.Profiles.Create(profileName, profileParms, resourceGroupName);
    }
}
```

Após a criação de perfil Olá, vamos criar um ponto de extremidade.

```csharp
private static void CreateCdnEndpoint(CdnManagementClient cdn)
{
    if (endpointAlreadyExists)
    {
        Console.WriteLine("Profile {0} already exists.", profileName);
    }
    else
    {
        Console.WriteLine("Creating endpoint {0} on profile {1}.", endpointName, profileName);
        EndpointCreateParameters endpointParms =
            new EndpointCreateParameters()
            {
                Origins = new List<DeepCreatedOrigin>() { new DeepCreatedOrigin("Contoso", "www.contoso.com") },
                IsHttpAllowed = true,
                IsHttpsAllowed = true,
                Location = resourceLocation
            };
        cdn.Endpoints.Create(endpointName, endpointParms, profileName, resourceGroupName);
    }
}
```

> [!NOTE]
> exemplo Hello acima atribui o ponto de extremidade de saudação uma origem denominada *Contoso* com um nome de host `www.contoso.com`.  Você deve alterar o nome de host deste toopoint tooyour próprio da origem.
> 
> 

## <a name="purge-an-endpoint"></a>Limpar um ponto de extremidade
Supondo que o ponto de extremidade de saudação foi criado, uma tarefa comum que que talvez desejemos tooperform em nosso programa está limpando conteúdo Olá no ponto de extremidade.

```csharp
private static void PromptPurgeCdnEndpoint(CdnManagementClient cdn)
{
    if (PromptUser(String.Format("Purge CDN endpoint {0}?", endpointName)))
    {
        Console.WriteLine("Purging endpoint. Please wait...");
        cdn.Endpoints.PurgeContent(endpointName, profileName, resourceGroupName, new List<string>() { "/*" });
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

> [!NOTE]
> O exemplo hello acima, Olá cadeia de caracteres `/*` indica que desejo toopurge tudo na raiz de saudação do caminho do ponto de extremidade de saudação.  Este é o equivalente toochecking **limpar todos os** de saudação portal do Azure "Limpar" caixa de diálogo. Em Olá `CreateCdnProfile` método, criei nosso perfil como um **CDN do Azure da Verizon** perfil usando código Olá `Sku = new Sku(SkuName.StandardVerizon)`, isso será bem-sucedida.  No entanto, **Azure CDN do Akamai** não dão suporte a perfis **limpar todos os**, portanto, se eu estava usando um perfil do Akamai para este tutorial, será preciso tooinclude toopurge de caminhos específicos.
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a>Excluir perfis CDN e pontos de extremidade
métodos de última Olá excluirá nosso ponto de extremidade e o perfil.

```csharp
private static void PromptDeleteCdnEndpoint(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN endpoint {0} on profile {1}?", endpointName, profileName)))
    {
        Console.WriteLine("Deleting endpoint. Please wait...");
        cdn.Endpoints.DeleteIfExists(endpointName, profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}

private static void PromptDeleteCdnProfile(CdnManagementClient cdn)
{
    if(PromptUser(String.Format("Delete CDN profile {0}?", profileName)))
    {
        Console.WriteLine("Deleting profile. Please wait...");
        cdn.Profiles.DeleteIfExists(profileName, resourceGroupName);
        Console.WriteLine("Done.");
        Console.WriteLine();
    }
}
```

## <a name="running-hello-program"></a>Programa de saudação em execução
Agora podemos pode compilar e executar o programa de saudação clicando Olá **iniciar** botão no Visual Studio.

![Programa em execução](./media/cdn-app-dev-net/cdn-program-running-1.png)

Quando o programa de saudação atingir Olá acima prompt, você deve ser capaz de tooreturn tooyour grupo de recursos Olá portal do Azure e ver que o perfil de saudação foi criada.

![Sucesso!](./media/cdn-app-dev-net/cdn-success.png)

Podemos afirmar Olá prompts toorun Olá rest do programa hello.

![Programa em conclusão](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a>Próximas etapas
projeto de saudação concluída toosee deste passo a passo, [baixar exemplo hello](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).

toofind obter documentação adicional sobre Olá biblioteca de gerenciamento de CDN do Azure para .NET, Olá exibição [referência no MSDN](https://msdn.microsoft.com/library/mt657769.aspx).

Gerencie seus recursos CDN com o [PowerShell](cdn-manage-powershell.md).

