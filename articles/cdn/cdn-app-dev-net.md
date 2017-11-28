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
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="16651-103">Introdução ao desenvolvimento de CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="16651-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="16651-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="16651-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="16651-105">.NET</span><span class="sxs-lookup"><span data-stu-id="16651-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="16651-106">Você pode usar o hello [biblioteca de CDN do Azure para .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate criação e gerenciamento de perfis CDN e os pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="16651-106">You can use hello [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="16651-107">Este tutorial orienta a criação de um aplicativo de console simples do .NET que demonstra várias operações disponíveis Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="16651-107">This tutorial walks through hello creation of a simple .NET console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="16651-108">Este tutorial é toodescribe não se destina todos os aspectos da saudação biblioteca de CDN do Azure para .NET em detalhes.</span><span class="sxs-lookup"><span data-stu-id="16651-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="16651-109">É necessário toocomplete do Visual Studio 2015 neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="16651-109">You need Visual Studio 2015 toocomplete this tutorial.</span></span>  <span data-ttu-id="16651-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) está disponível gratuitamente para download.</span><span class="sxs-lookup"><span data-stu-id="16651-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="16651-111">Olá [projeto concluído deste tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) está disponível para download no MSDN.</span><span class="sxs-lookup"><span data-stu-id="16651-111">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="16651-112">Crie seu projeto e adicione pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="16651-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="16651-113">Agora que podemos criar um grupo de recursos para os perfis CDN e considerando nossa perfis de CDN do Azure AD aplicativos permissão toomanage e pontos de extremidade dentro desse grupo, podemos começar criando o nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="16651-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="16651-114">Em Visual Studio 2015, clique **arquivo**, **novo**, **projeto...**  tooopen Olá novo diálogo do projeto.</span><span class="sxs-lookup"><span data-stu-id="16651-114">From within Visual Studio 2015, click **File**, **New**, **Project...** tooopen hello new project dialog.</span></span>  <span data-ttu-id="16651-115">Expanda **Visual C#**, em seguida, selecione **Windows** no painel Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="16651-115">Expand **Visual C#**, then select **Windows** in hello pane on hello left.</span></span>  <span data-ttu-id="16651-116">Clique em **aplicativo de Console** no painel central de saudação.</span><span class="sxs-lookup"><span data-stu-id="16651-116">Click **Console Application** in hello center pane.</span></span>  <span data-ttu-id="16651-117">Nomeie o projeto e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="16651-117">Name your project, then click **OK**.</span></span>  

![Novo Projeto](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="16651-119">Nosso projeto vai toouse algumas bibliotecas do Azure contidas em pacotes do Nuget.</span><span class="sxs-lookup"><span data-stu-id="16651-119">Our project is going toouse some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="16651-120">Vamos adicionar esses projeto toohello.</span><span class="sxs-lookup"><span data-stu-id="16651-120">Let's add those toohello project.</span></span>

1. <span data-ttu-id="16651-121">Clique em Olá **ferramentas** menu **Nuget Package Manager**, em seguida, **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="16651-121">Click hello **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Gerenciar pacotes NuGet](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="16651-123">No hello Package Manager Console, execute Olá Olá de tooinstall de comando a seguir **biblioteca de autenticação do Active Directory (ADAL)**:</span><span class="sxs-lookup"><span data-stu-id="16651-123">In hello Package Manager Console, execute hello following command tooinstall hello **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="16651-124">Executar Olá Olá tooinstall a seguir **biblioteca de gerenciamento do Azure CDN**:</span><span class="sxs-lookup"><span data-stu-id="16651-124">Execute hello following tooinstall hello **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="16651-125">Diretivas, constantes, método principal e métodos auxiliares</span><span class="sxs-lookup"><span data-stu-id="16651-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="16651-126">Vamos estrutura básica de saudação de nosso programa gravado.</span><span class="sxs-lookup"><span data-stu-id="16651-126">Let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="16651-127">No guia de Program.cs hello, substitua Olá `using` diretivas na parte superior da saudação com os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="16651-127">Back in hello Program.cs tab, replace hello `using` directives at hello top with hello following:</span></span>
   
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
2. <span data-ttu-id="16651-128">Precisamos toodefine algumas constantes que nossos métodos usará.</span><span class="sxs-lookup"><span data-stu-id="16651-128">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="16651-129">Em hello `Program` classe, mas antes do hello `Main` método, adicione o seguinte de saudação.</span><span class="sxs-lookup"><span data-stu-id="16651-129">In hello `Program` class, but before hello `Main` method, add hello following.</span></span>  <span data-ttu-id="16651-130">Ser tooreplace se espaços reservados hello, incluindo Olá  **&lt;colchetes angulares&gt;**, com seus próprios valores conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="16651-130">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="16651-131">Também no nível de classe hello, defina essas duas variáveis.</span><span class="sxs-lookup"><span data-stu-id="16651-131">Also at hello class level, define these two variables.</span></span>  <span data-ttu-id="16651-132">Vamos usar essas toodetermine posterior se nosso perfil e o ponto de extremidade já existem.</span><span class="sxs-lookup"><span data-stu-id="16651-132">We'll use these later toodetermine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="16651-133">Substituir saudação `Main` método da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="16651-133">Replace hello `Main` method as follows:</span></span>
   
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
5. <span data-ttu-id="16651-134">Alguns dos nossos outros métodos for usuário de saudação tooprompt com perguntas de "Sim/não".</span><span class="sxs-lookup"><span data-stu-id="16651-134">Some of our other methods are going tooprompt hello user with "Yes/No" questions.</span></span>  <span data-ttu-id="16651-135">Adicionar Olá toomake do método a seguir que um pouco mais fácil:</span><span class="sxs-lookup"><span data-stu-id="16651-135">Add hello following method toomake that a little easier:</span></span>
   
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

<span data-ttu-id="16651-136">Agora que a estrutura básica de saudação do programa é gravada, que deve ser criado métodos Olá chamados pelo Olá `Main` método.</span><span class="sxs-lookup"><span data-stu-id="16651-136">Now that hello basic structure of our program is written, we should create hello methods called by hello `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="16651-137">Autenticação</span><span class="sxs-lookup"><span data-stu-id="16651-137">Authentication</span></span>
<span data-ttu-id="16651-138">Antes que possamos Olá biblioteca de gerenciamento do Azure CDN, precisamos tooauthenticate nosso serviço principal e obter um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="16651-138">Before we can use hello Azure CDN Management Library, we need tooauthenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="16651-139">Esse método usa o token de saudação tooretrieve ADAL.</span><span class="sxs-lookup"><span data-stu-id="16651-139">This method uses ADAL tooretrieve hello token.</span></span>

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

<span data-ttu-id="16651-140">Se você estiver usando a autenticação de usuário individual, Olá `GetAccessToken` método parecerá um pouco diferente.</span><span class="sxs-lookup"><span data-stu-id="16651-140">If you are using individual user authentication, hello `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="16651-141">Somente use esse exemplo de código se você está escolhendo toohave autenticação de usuário individual em vez de uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="16651-141">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>
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

<span data-ttu-id="16651-142">Ser tooreplace se `<redirect URI>` com hello redirecione o URI que você inseriu quando registrou o aplicativo hello no AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="16651-142">Be sure tooreplace `<redirect URI>` with hello redirect URI you entered when you registered hello application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="16651-143">Relacione os perfis CDN e os pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="16651-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="16651-144">Agora estamos prontos tooperform operações de CDN.</span><span class="sxs-lookup"><span data-stu-id="16651-144">Now we're ready tooperform CDN operations.</span></span>  <span data-ttu-id="16651-145">Olá primeira coisa que nosso método faz é lista todos os perfis de saudação e pontos de extremidade em nosso grupo de recursos e se ele encontrar uma correspondência para nomes de perfil e o ponto de extremidade de saudação especificado em nossas constantes, torna Observe que para mais tarde então não tentaremos toocreate duplicatas.</span><span class="sxs-lookup"><span data-stu-id="16651-145">hello first thing our method does is list all hello profiles and endpoints in our resource group, and if it finds a match for hello profile and endpoint names specified in our constants, makes a note of that for later so we don't try toocreate duplicates.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="16651-146">Criar perfis CDN e pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="16651-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="16651-147">Em seguida, criaremos um perfil.</span><span class="sxs-lookup"><span data-stu-id="16651-147">Next, we'll create a profile.</span></span>

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

<span data-ttu-id="16651-148">Após a criação de perfil Olá, vamos criar um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="16651-148">Once hello profile is created, we'll create an endpoint.</span></span>

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
> <span data-ttu-id="16651-149">exemplo Hello acima atribui o ponto de extremidade de saudação uma origem denominada *Contoso* com um nome de host `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="16651-149">hello example above assigns hello endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="16651-150">Você deve alterar o nome de host deste toopoint tooyour próprio da origem.</span><span class="sxs-lookup"><span data-stu-id="16651-150">You should change this toopoint tooyour own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="16651-151">Limpar um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="16651-151">Purge an endpoint</span></span>
<span data-ttu-id="16651-152">Supondo que o ponto de extremidade de saudação foi criado, uma tarefa comum que que talvez desejemos tooperform em nosso programa está limpando conteúdo Olá no ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="16651-152">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging hello content in our endpoint.</span></span>

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
> <span data-ttu-id="16651-153">O exemplo hello acima, Olá cadeia de caracteres `/*` indica que desejo toopurge tudo na raiz de saudação do caminho do ponto de extremidade de saudação.</span><span class="sxs-lookup"><span data-stu-id="16651-153">In hello example above, hello string `/*` denotes that I want toopurge everything in hello root of hello endpoint path.</span></span>  <span data-ttu-id="16651-154">Este é o equivalente toochecking **limpar todos os** de saudação portal do Azure "Limpar" caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="16651-154">This is equivalent toochecking **Purge All** in hello Azure portal's "purge" dialog.</span></span> <span data-ttu-id="16651-155">Em Olá `CreateCdnProfile` método, criei nosso perfil como um **CDN do Azure da Verizon** perfil usando código Olá `Sku = new Sku(SkuName.StandardVerizon)`, isso será bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="16651-155">In hello `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using hello code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="16651-156">No entanto, **Azure CDN do Akamai** não dão suporte a perfis **limpar todos os**, portanto, se eu estava usando um perfil do Akamai para este tutorial, será preciso tooinclude toopurge de caminhos específicos.</span><span class="sxs-lookup"><span data-stu-id="16651-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need tooinclude specific paths toopurge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="16651-157">Excluir perfis CDN e pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="16651-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="16651-158">métodos de última Olá excluirá nosso ponto de extremidade e o perfil.</span><span class="sxs-lookup"><span data-stu-id="16651-158">hello last methods will delete our endpoint and profile.</span></span>

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

## <a name="running-hello-program"></a><span data-ttu-id="16651-159">Programa de saudação em execução</span><span class="sxs-lookup"><span data-stu-id="16651-159">Running hello program</span></span>
<span data-ttu-id="16651-160">Agora podemos pode compilar e executar o programa de saudação clicando Olá **iniciar** botão no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="16651-160">We can now compile and run hello program by clicking hello **Start** button in Visual Studio.</span></span>

![Programa em execução](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="16651-162">Quando o programa de saudação atingir Olá acima prompt, você deve ser capaz de tooreturn tooyour grupo de recursos Olá portal do Azure e ver que o perfil de saudação foi criada.</span><span class="sxs-lookup"><span data-stu-id="16651-162">When hello program reaches hello above prompt, you should be able tooreturn tooyour resource group in hello Azure portal and see that hello profile has been created.</span></span>

![Sucesso!](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="16651-164">Podemos afirmar Olá prompts toorun Olá rest do programa hello.</span><span class="sxs-lookup"><span data-stu-id="16651-164">We can then confirm hello prompts toorun hello rest of hello program.</span></span>

![Programa em conclusão](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="16651-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16651-166">Next Steps</span></span>
<span data-ttu-id="16651-167">projeto de saudação concluída toosee deste passo a passo, [baixar exemplo hello](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="16651-167">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="16651-168">toofind obter documentação adicional sobre Olá biblioteca de gerenciamento de CDN do Azure para .NET, Olá exibição [referência no MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="16651-168">toofind additional documentation on hello Azure CDN Management Library for .NET, view hello [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="16651-169">Gerencie seus recursos CDN com o [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="16651-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

