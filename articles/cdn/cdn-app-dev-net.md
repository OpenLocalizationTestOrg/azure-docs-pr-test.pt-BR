---
title: "Introdução à biblioteca do Azure CDN para .NET | Microsoft Docs"
description: Aprenda a gravar aplicativos .NET para gerenciar o Azure CDN usando o Visual Studio.
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
ms.openlocfilehash: 5379586355ece98af6295236d6cbd09cb31c742b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="cf389-103">Introdução ao desenvolvimento de CDN do Azure</span><span class="sxs-lookup"><span data-stu-id="cf389-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cf389-104">Node.js</span><span class="sxs-lookup"><span data-stu-id="cf389-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="cf389-105">.NET</span><span class="sxs-lookup"><span data-stu-id="cf389-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="cf389-106">Você pode usar a [Biblioteca do Azure CDN para .NET](https://msdn.microsoft.com/library/mt657769.aspx) para automatizar a criação e o gerenciamento de perfis CDN e de pontos de extremidade.</span><span class="sxs-lookup"><span data-stu-id="cf389-106">You can use the [Azure CDN Library for .NET](https://msdn.microsoft.com/library/mt657769.aspx) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="cf389-107">Este tutorial o orientará na criação de um aplicativo de console simples do .NET, que demonstra várias operações disponíveis.</span><span class="sxs-lookup"><span data-stu-id="cf389-107">This tutorial walks through the creation of a simple .NET console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="cf389-108">Este tutorial não pretende descrever todos os aspectos da biblioteca do Azure CDN para o .NET em detalhes.</span><span class="sxs-lookup"><span data-stu-id="cf389-108">This tutorial is not intended to describe all aspects of the Azure CDN Library for .NET in detail.</span></span>

<span data-ttu-id="cf389-109">Você precisa do Visual Studio 2015 para concluir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="cf389-109">You need Visual Studio 2015 to complete this tutorial.</span></span>  <span data-ttu-id="cf389-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) está disponível gratuitamente para download.</span><span class="sxs-lookup"><span data-stu-id="cf389-110">[Visual Studio Community 2015](https://www.visualstudio.com/products/visual-studio-community-vs.aspx) is freely available for download.</span></span>

> [!TIP]
> <span data-ttu-id="cf389-111">O [projeto concluído deste tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) está disponível para download no MSDN.</span><span class="sxs-lookup"><span data-stu-id="cf389-111">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-nuget-packages"></a><span data-ttu-id="cf389-112">Crie seu projeto e adicione pacotes NuGet</span><span class="sxs-lookup"><span data-stu-id="cf389-112">Create your project and add Nuget packages</span></span>
<span data-ttu-id="cf389-113">Agora que criamos um grupo de recursos para nossos perfis CDN e demos permissão para o nosso aplicativo Azure AD gerenciar os perfis CDN e os pontos de extremidade neste grupo, podemos começar a criação do nosso aplicativo.</span><span class="sxs-lookup"><span data-stu-id="cf389-113">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="cf389-114">No Visual Studio 2015, clique em **Arquivo**, **Novo**, **Projeto...** para abrir a caixa de diálogo do novo projeto.</span><span class="sxs-lookup"><span data-stu-id="cf389-114">From within Visual Studio 2015, click **File**, **New**, **Project...** to open the new project dialog.</span></span>  <span data-ttu-id="cf389-115">Expanda **Visual C#** e, em seguida, selecione **Windows** no painel à esquerda.</span><span class="sxs-lookup"><span data-stu-id="cf389-115">Expand **Visual C#**, then select **Windows** in the pane on the left.</span></span>  <span data-ttu-id="cf389-116">Clique em **Aplicativo de Console** no painel central.</span><span class="sxs-lookup"><span data-stu-id="cf389-116">Click **Console Application** in the center pane.</span></span>  <span data-ttu-id="cf389-117">Nomeie o projeto e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cf389-117">Name your project, then click **OK**.</span></span>  

![Novo Projeto](./media/cdn-app-dev-net/cdn-new-project.png)

<span data-ttu-id="cf389-119">Nosso projeto usará algumas bibliotecas do Azure contidas em pacotes NuGet.</span><span class="sxs-lookup"><span data-stu-id="cf389-119">Our project is going to use some Azure libraries contained in Nuget packages.</span></span>  <span data-ttu-id="cf389-120">Vamos adicioná-las ao projeto.</span><span class="sxs-lookup"><span data-stu-id="cf389-120">Let's add those to the project.</span></span>

1. <span data-ttu-id="cf389-121">Clique no menu **Ferramentas**, **Gerenciador de Pacotes Nuget** e, em seguida, **Console do Gerenciador de Pacotes**.</span><span class="sxs-lookup"><span data-stu-id="cf389-121">Click the **Tools** menu, **Nuget Package Manager**, then **Package Manager Console**.</span></span>
   
    ![Gerenciar pacotes NuGet](./media/cdn-app-dev-net/cdn-manage-nuget.png)
2. <span data-ttu-id="cf389-123">No Console do Gerenciador de Pacotes, execute o seguinte comando para instalar a **ADAL (Biblioteca de Autenticação do Active Directory)**:</span><span class="sxs-lookup"><span data-stu-id="cf389-123">In the Package Manager Console, execute the following command to install the **Active Directory Authentication Library (ADAL)**:</span></span>
   
    `Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory`
3. <span data-ttu-id="cf389-124">Execute o seguinte para instalar a **biblioteca de gerenciamento do Azure CDN**:</span><span class="sxs-lookup"><span data-stu-id="cf389-124">Execute the following to install the **Azure CDN Management Library**:</span></span>
   
    `Install-Package Microsoft.Azure.Management.Cdn`

## <a name="directives-constants-main-method-and-helper-methods"></a><span data-ttu-id="cf389-125">Diretivas, constantes, método principal e métodos auxiliares</span><span class="sxs-lookup"><span data-stu-id="cf389-125">Directives, constants, main method, and helper methods</span></span>
<span data-ttu-id="cf389-126">Vejamos a estrutura básica do nosso programa gravado.</span><span class="sxs-lookup"><span data-stu-id="cf389-126">Let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="cf389-127">De volta à guia Program.cs, substitua as diretivas `using` na parte superior com o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cf389-127">Back in the Program.cs tab, replace the `using` directives at the top with the following:</span></span>
   
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
2. <span data-ttu-id="cf389-128">Precisamos definir algumas constantes que serão usadas nos nossos métodos.</span><span class="sxs-lookup"><span data-stu-id="cf389-128">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="cf389-129">Na classe `Program`, mas antes do método `Main`, adicione o seguinte.</span><span class="sxs-lookup"><span data-stu-id="cf389-129">In the `Program` class, but before the `Main` method, add the following.</span></span>  <span data-ttu-id="cf389-130">Certifique-se de substituir os espaços reservados, inclusive os **&lt;colchetes angulares&gt;**, por seus próprios valores, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="cf389-130">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="cf389-131">Também no nível de classe, defina essas duas variáveis.</span><span class="sxs-lookup"><span data-stu-id="cf389-131">Also at the class level, define these two variables.</span></span>  <span data-ttu-id="cf389-132">Nós as usaremos posteriormente para determinar se o perfil e o ponto de extremidade já existem.</span><span class="sxs-lookup"><span data-stu-id="cf389-132">We'll use these later to determine if our profile and endpoint already exist.</span></span>
   
    ```csharp
    static bool profileAlreadyExists = false;
    static bool endpointAlreadyExists = false;
    ```
4. <span data-ttu-id="cf389-133">Substitua o método `Main` da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="cf389-133">Replace the `Main` method as follows:</span></span>
   
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
   
       Console.WriteLine("Press Enter to end program.");
       Console.ReadLine();
   }
   ```
5. <span data-ttu-id="cf389-134">Alguns dos nossos outros métodos solicitarão que o usuário responda perguntas do tipo "Sim/Não".</span><span class="sxs-lookup"><span data-stu-id="cf389-134">Some of our other methods are going to prompt the user with "Yes/No" questions.</span></span>  <span data-ttu-id="cf389-135">Adicione o seguinte método para tornar esse processo um pouco mais fácil:</span><span class="sxs-lookup"><span data-stu-id="cf389-135">Add the following method to make that a little easier:</span></span>
   
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

<span data-ttu-id="cf389-136">Agora que a estrutura básica do nosso programa está gravada, devemos criar métodos chamados pelo método `Main` .</span><span class="sxs-lookup"><span data-stu-id="cf389-136">Now that the basic structure of our program is written, we should create the methods called by the `Main` method.</span></span>

## <a name="authentication"></a><span data-ttu-id="cf389-137">Autenticação</span><span class="sxs-lookup"><span data-stu-id="cf389-137">Authentication</span></span>
<span data-ttu-id="cf389-138">Para que possamos usar a biblioteca de gerenciamento do Azure CDN, é necessário autenticar nossa entidade de serviço e obter um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="cf389-138">Before we can use the Azure CDN Management Library, we need to authenticate our service principal and obtain an authentication token.</span></span>  <span data-ttu-id="cf389-139">Esse método usa a ADAL para recuperar o token.</span><span class="sxs-lookup"><span data-stu-id="cf389-139">This method uses ADAL to retrieve the token.</span></span>

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

<span data-ttu-id="cf389-140">Se você estiver usando a autenticação de usuário individual, o método `GetAccessToken` terá uma aparência ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="cf389-140">If you are using individual user authentication, the `GetAccessToken` method will look slightly different.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cf389-141">Use este exemplo de código somente se optar pela autenticação de usuário individual, em vez de uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="cf389-141">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>
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

<span data-ttu-id="cf389-142">Certifique-se de substituir `<redirect URI>` com o URI de redirecionamento que você inseriu quando registrou o aplicativo no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="cf389-142">Be sure to replace `<redirect URI>` with the redirect URI you entered when you registered the application in Azure AD.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="cf389-143">Relacione os perfis CDN e os pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="cf389-143">List CDN profiles and endpoints</span></span>
<span data-ttu-id="cf389-144">Agora estamos prontos para executar as operações de CDN.</span><span class="sxs-lookup"><span data-stu-id="cf389-144">Now we're ready to perform CDN operations.</span></span>  <span data-ttu-id="cf389-145">A primeira tarefa que nosso método faz é relacionar todos os perfis e pontos de extremidade em nosso grupo de recursos e, se ele encontrar uma correspondência para os nomes de perfis e de pontos de extremidade especificados em nossas constantes, ele fará uma observação a respeito posteriormente. Portanto, não tentaremos criar duplicatas.</span><span class="sxs-lookup"><span data-stu-id="cf389-145">The first thing our method does is list all the profiles and endpoints in our resource group, and if it finds a match for the profile and endpoint names specified in our constants, makes a note of that for later so we don't try to create duplicates.</span></span>

```csharp
private static void ListProfilesAndEndpoints(CdnManagementClient cdn)
{
    // List all the CDN profiles in this resource group
    var profileList = cdn.Profiles.ListByResourceGroup(resourceGroupName);
    foreach (Profile p in profileList)
    {
        Console.WriteLine("CDN profile {0}", p.Name);
        if (p.Name.Equals(profileName, StringComparison.OrdinalIgnoreCase))
        {
            // Hey, that's the name of the CDN profile we want to create!
            profileAlreadyExists = true;
        }

        //List all the CDN endpoints on this CDN profile
        Console.WriteLine("Endpoints:");
        var endpointList = cdn.Endpoints.ListByProfile(p.Name, resourceGroupName);
        foreach (Endpoint e in endpointList)
        {
            Console.WriteLine("-{0} ({1})", e.Name, e.HostName);
            if (e.Name.Equals(endpointName, StringComparison.OrdinalIgnoreCase))
            {
                // The unique endpoint name already exists.
                endpointAlreadyExists = true;
            }
        }
        Console.WriteLine();
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="cf389-146">Criar perfis CDN e pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="cf389-146">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="cf389-147">Em seguida, criaremos um perfil.</span><span class="sxs-lookup"><span data-stu-id="cf389-147">Next, we'll create a profile.</span></span>

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

<span data-ttu-id="cf389-148">Depois que o perfil for criado, criaremos um ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="cf389-148">Once the profile is created, we'll create an endpoint.</span></span>

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
> <span data-ttu-id="cf389-149">O exemplo acima atribui ao ponto de extremidade uma origem denominada *Contoso*, com um nome de host `www.contoso.com`.</span><span class="sxs-lookup"><span data-stu-id="cf389-149">The example above assigns the endpoint an origin named *Contoso* with a hostname `www.contoso.com`.</span></span>  <span data-ttu-id="cf389-150">Você deve alterá-la para apontar para o nome de host de sua própria origem.</span><span class="sxs-lookup"><span data-stu-id="cf389-150">You should change this to point to your own origin's hostname.</span></span>
> 
> 

## <a name="purge-an-endpoint"></a><span data-ttu-id="cf389-151">Limpar um ponto de extremidade</span><span class="sxs-lookup"><span data-stu-id="cf389-151">Purge an endpoint</span></span>
<span data-ttu-id="cf389-152">Supondo que o ponto de extremidade tenha sido criado, uma tarefa comum que talvez desejemos executar em nosso programa está limpando o conteúdo no ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="cf389-152">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging the content in our endpoint.</span></span>

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
> <span data-ttu-id="cf389-153">No exemplo acima, a cadeia de caracteres `/*` indica que eu quero limpar tudo na raiz do caminho do ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="cf389-153">In the example above, the string `/*` denotes that I want to purge everything in the root of the endpoint path.</span></span>  <span data-ttu-id="cf389-154">Isso é equivalente a marcar **Limpar Tudo** na caixa de diálogo "limpeza" do portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="cf389-154">This is equivalent to checking **Purge All** in the Azure portal's "purge" dialog.</span></span> <span data-ttu-id="cf389-155">No método `CreateCdnProfile`, criei nosso perfil como perfil **Azure CDN da Verizon** usando o código `Sku = new Sku(SkuName.StandardVerizon)`; assim, ele será bem-sucedido.</span><span class="sxs-lookup"><span data-stu-id="cf389-155">In the `CreateCdnProfile` method, I created our profile as an **Azure CDN from Verizon** profile using the code `Sku = new Sku(SkuName.StandardVerizon)`, so this will be successful.</span></span>  <span data-ttu-id="cf389-156">No entanto, os perfis **Azure CDN do Akamai** não dá suporte para a ação **Limpar Tudo**. Portanto, se eu estivesse usando um perfil do Akamai neste tutorial, eu precisaria incluir caminhos específicos para limpar.</span><span class="sxs-lookup"><span data-stu-id="cf389-156">However, **Azure CDN from Akamai** profiles do not support **Purge All**, so if I was using an Akamai profile for this tutorial, I would need to include specific paths to purge.</span></span>
> 
> 

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="cf389-157">Excluir perfis CDN e pontos de extremidade</span><span class="sxs-lookup"><span data-stu-id="cf389-157">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="cf389-158">Os últimos métodos excluirão nosso ponto de extremidade e perfil.</span><span class="sxs-lookup"><span data-stu-id="cf389-158">The last methods will delete our endpoint and profile.</span></span>

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

## <a name="running-the-program"></a><span data-ttu-id="cf389-159">Executando o programa</span><span class="sxs-lookup"><span data-stu-id="cf389-159">Running the program</span></span>
<span data-ttu-id="cf389-160">Agora podemos compilar e executar o programa clicando no botão **Iniciar** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cf389-160">We can now compile and run the program by clicking the **Start** button in Visual Studio.</span></span>

![Programa em execução](./media/cdn-app-dev-net/cdn-program-running-1.png)

<span data-ttu-id="cf389-162">Quando o programa atingir o prompt acima, você poderá retornar a seu grupo de recursos no portal do Azure e ver que o perfil foi criado.</span><span class="sxs-lookup"><span data-stu-id="cf389-162">When the program reaches the above prompt, you should be able to return to your resource group in the Azure portal and see that the profile has been created.</span></span>

![Sucesso!](./media/cdn-app-dev-net/cdn-success.png)

<span data-ttu-id="cf389-164">Em seguida, podemos confirmar as solicitações para executar o restante do programa.</span><span class="sxs-lookup"><span data-stu-id="cf389-164">We can then confirm the prompts to run the rest of the program.</span></span>

![Programa em conclusão](./media/cdn-app-dev-net/cdn-program-running-2.png)

## <a name="next-steps"></a><span data-ttu-id="cf389-166">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cf389-166">Next Steps</span></span>
<span data-ttu-id="cf389-167">Para ver o projeto concluído desse passo a passo, [baixe o exemplo](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span><span class="sxs-lookup"><span data-stu-id="cf389-167">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-Management-1f2fba2c).</span></span>

<span data-ttu-id="cf389-168">Para localizar documentação adicional sobre a biblioteca de gerenciamento do Azure CDN para .NET, confira a [referência no MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span><span class="sxs-lookup"><span data-stu-id="cf389-168">To find additional documentation on the Azure CDN Management Library for .NET, view the [reference on MSDN](https://msdn.microsoft.com/library/mt657769.aspx).</span></span>

<span data-ttu-id="cf389-169">Gerencie seus recursos CDN com o [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="cf389-169">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

