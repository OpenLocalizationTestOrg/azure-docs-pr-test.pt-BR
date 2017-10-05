---
title: 'Azure Active Directory B2C: usar a API do Graph | Microsoft Docs'
description: "Como chamar a API do Graph para um locatário B2C usando uma identidade de aplicativo para automatizar o processo."
services: active-directory-b2c
documentationcenter: .net
author: parakhj
manager: krassk
editor: parakhj
ms.assetid: f9904516-d9f7-43b1-ae4f-e4d9eb1c67a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/07/2017
ms.author: parakhj
ms.openlocfilehash: c838fcad21875c4f813159ad78d4c87129a40a86
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-ad-b2c-use-the-graph-api"></a><span data-ttu-id="f2daf-103">Azure AD B2C: usar a API do Graph</span><span class="sxs-lookup"><span data-stu-id="f2daf-103">Azure AD B2C: Use the Graph API</span></span>
<span data-ttu-id="f2daf-104">Os locatários do Azure Active Directory (Azure AD) B2C tendem a ser muito grandes.</span><span class="sxs-lookup"><span data-stu-id="f2daf-104">Azure Active Directory (Azure AD) B2C tenants tend to be very large.</span></span> <span data-ttu-id="f2daf-105">Isso significa que muitas tarefas comuns de gerenciamento de locatário devem ser executadas programaticamente.</span><span class="sxs-lookup"><span data-stu-id="f2daf-105">This means that many common tenant management tasks need to be performed programmatically.</span></span> <span data-ttu-id="f2daf-106">O principal exemplo é o gerenciamento de usuário.</span><span class="sxs-lookup"><span data-stu-id="f2daf-106">A primary example is user management.</span></span> <span data-ttu-id="f2daf-107">Talvez seja necessário migrar o repositório de usuário existente para um locatário B2C.</span><span class="sxs-lookup"><span data-stu-id="f2daf-107">You might need to migrate an existing user store to a B2C tenant.</span></span> <span data-ttu-id="f2daf-108">Talvez seja melhor hospedar o registro de usuário em sua própria página e criar contas de usuário no seu diretório do Azure AD B2C nos bastidores.</span><span class="sxs-lookup"><span data-stu-id="f2daf-108">You may want to host user registration on your own page and create user accounts in your Azure AD B2C directory behind the scenes.</span></span> <span data-ttu-id="f2daf-109">Esses tipos de tarefas exigem a capacidade de criar, ler, atualizar e excluir contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="f2daf-109">These types of tasks require the ability to create, read, update, and delete user accounts.</span></span> <span data-ttu-id="f2daf-110">Você pode realizar essas tarefas usando a API do Graph do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2daf-110">You can do these tasks by using the Azure AD Graph API.</span></span>

<span data-ttu-id="f2daf-111">Para locatários B2C, existem basicamente dois modos de se comunicar com a API do Graph.</span><span class="sxs-lookup"><span data-stu-id="f2daf-111">For B2C tenants, there are two primary modes of communicating with the Graph API.</span></span>

* <span data-ttu-id="f2daf-112">Para tarefas de execução única, interativas, você deverá agir como uma conta de administrador no locatário B2C quando executar as tarefas.</span><span class="sxs-lookup"><span data-stu-id="f2daf-112">For interactive, run-once tasks, you should act as an administrator account in the B2C tenant when you perform the tasks.</span></span> <span data-ttu-id="f2daf-113">Esse modo requer que um administrador entre com credenciais antes de poder executar todas as chamadas à API do Graph.</span><span class="sxs-lookup"><span data-stu-id="f2daf-113">This mode requires an administrator to sign in with credentials before that admin can perform any calls to the Graph API.</span></span>
* <span data-ttu-id="f2daf-114">Para tarefas automatizadas, contínuas, você deve usar algum tipo de conta de serviço fornecida com os privilégios necessários para executar tarefas de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="f2daf-114">For automated, continuous tasks, you should use some type of service account that you provide with the necessary privileges to perform management tasks.</span></span> <span data-ttu-id="f2daf-115">No Azure AD, você pode fazer isso registrando um aplicativo e autenticando no Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2daf-115">In Azure AD, you can do this by registering an application and authenticating to Azure AD.</span></span> <span data-ttu-id="f2daf-116">Isso é feito usando uma **ID de aplicativo** que usa a [concessão de credenciais do cliente OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="f2daf-116">This is done by using an **Application ID** that uses the [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="f2daf-117">Nesse caso, o aplicativo atua em nome próprio, e não como usuário, para chamar a API do Graph.</span><span class="sxs-lookup"><span data-stu-id="f2daf-117">In this case, the application acts as itself, not as a user, to call the Graph API.</span></span>

<span data-ttu-id="f2daf-118">Neste artigo, discutiremos como executar o caso de uso automatizado.</span><span class="sxs-lookup"><span data-stu-id="f2daf-118">In this article, we'll discuss how to perform the automated-use case.</span></span> <span data-ttu-id="f2daf-119">Para demonstrar isso, vamos criar um .NET 4.5 `B2CGraphClient` que executa as operações CRUD (criar, ler, atualizar e excluir) do usuário.</span><span class="sxs-lookup"><span data-stu-id="f2daf-119">To demonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="f2daf-120">O cliente terá uma CLI (interface de linha de comando) do Windows que permite que você chame vários métodos.</span><span class="sxs-lookup"><span data-stu-id="f2daf-120">The client will have a Windows command-line interface (CLI) that allows you to invoke various methods.</span></span> <span data-ttu-id="f2daf-121">No entanto, o código é gravado para se comportar de forma não interativa e automatizada.</span><span class="sxs-lookup"><span data-stu-id="f2daf-121">However, the code is written to behave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="f2daf-122">Obter um locatário do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="f2daf-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="f2daf-123">Antes de criar o aplicativo ou os usuários ou interagir com o Azure AD, você precisará de um locatário habilitado para B2C e uma conta de administrador global no locatário.</span><span class="sxs-lookup"><span data-stu-id="f2daf-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in the tenant.</span></span> <span data-ttu-id="f2daf-124">Se você ainda não tiver um locatário, confira a [introdução ao Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="f2daf-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="f2daf-125">Registrar seu aplicativo em seu locatário</span><span class="sxs-lookup"><span data-stu-id="f2daf-125">Register your application in your tenant</span></span>
<span data-ttu-id="f2daf-126">Quando você tiver um locatário B2C, será necessário registrar seu aplicativo por meio do [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f2daf-126">After you have a B2C tenant, you need to register your application via the [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2daf-127">Para usar a API do Graph com seu locatário B2C, você precisará registrar um aplicativo dedicado usando a folha genérica *Registros de Aplicativo* no Portal do Azure, **NÃO** a folha *Aplicativos* do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f2daf-127">To use the Graph API with your B2C tenant, you will need to register a dedicated application by using the generic *App Registrations* blade in the Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="f2daf-128">Você não pode reutilizar seus aplicativos B2C já existentes registrados na folha *Aplicativos* do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="f2daf-128">You can't reuse the already-existing B2C applications that you registered in the Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="f2daf-129">Entre no [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f2daf-129">Sign in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="f2daf-130">Escolha seu locatário do Azure AD B2C selecionando sua conta no canto superior direito da página.</span><span class="sxs-lookup"><span data-stu-id="f2daf-130">Choose your Azure AD B2C tenant by selecting your account in the top right corner of the page.</span></span>
3. <span data-ttu-id="f2daf-131">No painel de navegação à esquerda, escolha **Mais Serviços**, clique em **Registros de Aplicativo** e clique em **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="f2daf-131">In the left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="f2daf-132">Siga os avisos e crie um novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f2daf-132">Follow the prompts and create a new application.</span></span> 
    1. <span data-ttu-id="f2daf-133">Selecione **Aplicativo Web/API** como o Tipo de Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f2daf-133">Select **Web App / API** as the Application Type.</span></span>    
    2. <span data-ttu-id="f2daf-134">Forneça **qualquer URI de redirecionamento** (por exemplo, https://B2CGraphAPI), pois isso não é relevante para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="f2daf-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="f2daf-135">Agora, o aplicativo aparecerá na lista de aplicativos. Clique nele para obter a **ID do Aplicativo** (também conhecida como ID do Cliente).</span><span class="sxs-lookup"><span data-stu-id="f2daf-135">The application will now show up in the list of applications, click on it to obtain the **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="f2daf-136">Copie-a, pois precisará dela em uma seção posterior.</span><span class="sxs-lookup"><span data-stu-id="f2daf-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="f2daf-137">Na folha Configurações, clique em **Chaves** e adicione uma nova chave (também conhecida como o segredo do cliente).</span><span class="sxs-lookup"><span data-stu-id="f2daf-137">In the Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="f2daf-138">Copie-a também para uso em uma seção posterior.</span><span class="sxs-lookup"><span data-stu-id="f2daf-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="f2daf-139">Configurar as permissões de criação, leitura e atualização para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="f2daf-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="f2daf-140">Agora você precisa configurar seu aplicativo para obter todas as permissões necessárias para criar, ler, atualizar e excluir usuários.</span><span class="sxs-lookup"><span data-stu-id="f2daf-140">Now you need to configure your application to get all the required permissions to create, read, update and delete users.</span></span>

1. <span data-ttu-id="f2daf-141">Ainda na folha Registros de Aplicativo do Portal do Azure, selecione seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f2daf-141">Continuing in the Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="f2daf-142">Na folha Configurações, clique em **Permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="f2daf-142">In the Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="f2daf-143">Na folha Permissões necessárias, clique em **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="f2daf-143">In the Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="f2daf-144">Na folha Habilitar Acesso, selecione a permissão **Ler e gravar dados de diretório** em **Permissões de Aplicativo** e clique em **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="f2daf-144">In the Enable Access  blade, select the **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="f2daf-145">Por fim, na folha Permissões necessárias, clique no botão **Conceder Permissões**.</span><span class="sxs-lookup"><span data-stu-id="f2daf-145">Finally, back in the Required permissions blade, click on the **Grant Permissions** button.</span></span>

<span data-ttu-id="f2daf-146">Agora, você tem um aplicativo que tem permissão para criar, ler e atualizar usuários de seu locatário B2C.</span><span class="sxs-lookup"><span data-stu-id="f2daf-146">You now have an application that has permission to create, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="f2daf-147">Configurar permissões de exclusão para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="f2daf-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="f2daf-148">Atualmente, a permissão *Ler e gravar dados de diretório* **NÃO** inclui a capacidade de fazer qualquer exclusão, como excluir usuários.</span><span class="sxs-lookup"><span data-stu-id="f2daf-148">Currently, the *Read and write directory data* permission does **NOT** include the ability to do any deletions such as deleting users.</span></span> <span data-ttu-id="f2daf-149">Se você quiser fornecer ao seu aplicativo a capacidade de excluir os usuários, será necessário executar estas etapas adicionais envolvendo o PowerShell, caso contrário, pule para a próxima seção.</span><span class="sxs-lookup"><span data-stu-id="f2daf-149">If you want to give your application the ability to delete users, you'll need to do these extra steps that involve PowerShell, otherwise, you can skip to the next section.</span></span>

<span data-ttu-id="f2daf-150">Primeiro, baixe e instale o [Assistente de Conexão do Microsoft Online Services](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="f2daf-150">First, download and install the [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="f2daf-151">Em seguida, baixe e instale o [Módulo do Azure Active Directory de 64 bits para Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="f2daf-151">Then download and install the [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="f2daf-152">Depois de instalar o módulo do PowerShell, abra o PowerShell e conecte-se ao locatário B2C.</span><span class="sxs-lookup"><span data-stu-id="f2daf-152">After you install the PowerShell module, open PowerShell and connect to your B2C tenant.</span></span> <span data-ttu-id="f2daf-153">Depois de executar o `Get-Credential`, você será solicitado a fornecer um nome de usuário e uma senha. Insira o nome de usuário e a senha de sua conta de administrador do locatário B2C.</span><span class="sxs-lookup"><span data-stu-id="f2daf-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter the user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2daf-154">Você precisa usar uma conta de administrador de locatário B2C que seja **local** para o locatário B2C.</span><span class="sxs-lookup"><span data-stu-id="f2daf-154">You need to use a B2C tenant administrator account that is **local** to the B2C tenant.</span></span> <span data-ttu-id="f2daf-155">Essas contas têm esta aparência: myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="f2daf-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="f2daf-156">Agora, usaremos a **ID do Aplicativo** no script a seguir para atribuir ao aplicativo a função de administrador de conta de usuário, o que permitirá a exclusão de usuários.</span><span class="sxs-lookup"><span data-stu-id="f2daf-156">Now we'll use the **Application ID** in the script below to assign the application the user account administrator role which will allow it to delete users.</span></span> <span data-ttu-id="f2daf-157">Essas funções têm identificadores bem conhecidos, então tudo o que você precisa fazer é inserir sua **ID de Aplicativo** no script a seguir.</span><span class="sxs-lookup"><span data-stu-id="f2daf-157">These roles have well-known identifiers, so all you need to do is input your **Application ID** in the script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="f2daf-158">Agora, seu aplicativo também tem permissões para excluir usuários de seu locatário B2C.</span><span class="sxs-lookup"><span data-stu-id="f2daf-158">Your application now also has permissions to delete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-the-sample-code"></a><span data-ttu-id="f2daf-159">Baixar, configurar e compilar o código de exemplo</span><span class="sxs-lookup"><span data-stu-id="f2daf-159">Download, configure, and build the sample code</span></span>
<span data-ttu-id="f2daf-160">Primeiro, baixe o código de exemplo e execute-o.</span><span class="sxs-lookup"><span data-stu-id="f2daf-160">First, download the sample code and get it running.</span></span> <span data-ttu-id="f2daf-161">Em seguida, faremos uma análise mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="f2daf-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="f2daf-162">Você pode [baixar o código de exemplo como um arquivo .zip](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="f2daf-162">You can [download the sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="f2daf-163">Você também pode cloná-lo em um diretório de sua escolha:</span><span class="sxs-lookup"><span data-stu-id="f2daf-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="f2daf-164">Abra a solução do Visual Studio `B2CGraphClient\B2CGraphClient.sln` no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f2daf-164">Open the `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="f2daf-165">No `B2CGraphClient` de projeto, abra o arquivo `App.config`.</span><span class="sxs-lookup"><span data-stu-id="f2daf-165">In the `B2CGraphClient` project, open the file `App.config`.</span></span> <span data-ttu-id="f2daf-166">Substitua as três configurações do aplicativo por seus próprios valores:</span><span class="sxs-lookup"><span data-stu-id="f2daf-166">Replace the three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{The ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{The Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="f2daf-167">Agora, clique com o botão direito do mouse na solução `B2CGraphClient` e compile novamente o exemplo.</span><span class="sxs-lookup"><span data-stu-id="f2daf-167">Next, right-click on the `B2CGraphClient` solution and rebuild the sample.</span></span> <span data-ttu-id="f2daf-168">Se tiver êxito, agora deverá você ter um arquivo executável `B2C.exe` localizado em `B2CGraphClient\bin\Debug`.</span><span class="sxs-lookup"><span data-stu-id="f2daf-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-the-graph-api"></a><span data-ttu-id="f2daf-169">Criar operações CRUD do usuário usando a API do Graph</span><span class="sxs-lookup"><span data-stu-id="f2daf-169">Build user CRUD operations by using the Graph API</span></span>
<span data-ttu-id="f2daf-170">Para usar o B2CGraphClient, abra um prompt de comando `cmd` do Windows e altere o diretório para o diretório `Debug`.</span><span class="sxs-lookup"><span data-stu-id="f2daf-170">To use the B2CGraphClient, open a `cmd` Windows command prompt and change your directory to the `Debug` directory.</span></span> <span data-ttu-id="f2daf-171">Em seguida, execute o `B2C Help` comando.</span><span class="sxs-lookup"><span data-stu-id="f2daf-171">Then run the `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="f2daf-172">Isso exibirá uma breve descrição de cada comando.</span><span class="sxs-lookup"><span data-stu-id="f2daf-172">This will display a brief description of each command.</span></span> <span data-ttu-id="f2daf-173">Sempre que você invoca um desses comandos, o `B2CGraphClient` faz uma solicitação para a API do Graph do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2daf-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request to the Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="f2daf-174">Obter um token de acesso</span><span class="sxs-lookup"><span data-stu-id="f2daf-174">Get an access token</span></span>
<span data-ttu-id="f2daf-175">Qualquer solicitação para a API do Graph requer um token de acesso para autenticação.</span><span class="sxs-lookup"><span data-stu-id="f2daf-175">Any request to the Graph API requires an access token for authentication.</span></span> <span data-ttu-id="f2daf-176">`B2CGraphClient` usa a ADAL (Biblioteca de Autenticação do Active Directory) de software livre para ajudar a obter tokens de acesso.</span><span class="sxs-lookup"><span data-stu-id="f2daf-176">`B2CGraphClient` uses the open-source Active Directory Authentication Library (ADAL) to help acquire access tokens.</span></span> <span data-ttu-id="f2daf-177">A ADAL facilita a aquisição de tokens, fornecendo uma API simples e cuidando de alguns detalhes importantes, como armazenar em cache os tokens de acesso.</span><span class="sxs-lookup"><span data-stu-id="f2daf-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="f2daf-178">No entanto, você não precisa usar a ADAL para obter tokens.</span><span class="sxs-lookup"><span data-stu-id="f2daf-178">You don't have to use ADAL to get tokens, though.</span></span> <span data-ttu-id="f2daf-179">Você também pode obter tokens ao criar solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="f2daf-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="f2daf-180">Este exemplo de código usa o ADAL v2 para se comunicar com a API do Graph.</span><span class="sxs-lookup"><span data-stu-id="f2daf-180">This code sample uses ADAL v2 in order to communicate with the Graph API.</span></span>  <span data-ttu-id="f2daf-181">Você deve usar o ADAL v2 ou v3 para obter tokens de acesso que podem ser usados com a API do Graph do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2daf-181">You must use ADAL v2 or v3 in order to get access tokens which can be used with the Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="f2daf-182">Quando `B2CGraphClient` é executado, o código cria uma instância da classe `B2CGraphClient`.</span><span class="sxs-lookup"><span data-stu-id="f2daf-182">When `B2CGraphClient` runs, it creates an instance of the `B2CGraphClient` class.</span></span> <span data-ttu-id="f2daf-183">O construtor para essa classe configura a estrutura de autenticação da ADAL:</span><span class="sxs-lookup"><span data-stu-id="f2daf-183">The constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // The client_id, client_secret, and tenant are provided in Program.cs, which pulls the values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // The AuthenticationContext is ADAL's primary class, in which you indicate the tenant to use.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // The ClientCredential is where you pass in your client_id and client_secret, which are
    // provided to Azure AD in order to receive an access_token by using the app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="f2daf-184">Vamos usar o comando `B2C Get-User` como um exemplo.</span><span class="sxs-lookup"><span data-stu-id="f2daf-184">We'll use the `B2C Get-User` command as an example.</span></span> <span data-ttu-id="f2daf-185">Quando `B2C Get-User` é invocado sem quaisquer entradas adicionais, o CLI chama o `B2CGraphClient.GetAllUsers(...)` método.</span><span class="sxs-lookup"><span data-stu-id="f2daf-185">When `B2C Get-User` is invoked without any additional inputs, the CLI calls the `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="f2daf-186">Este método chama `B2CGraphClient.SendGraphGetRequest(...)`, que envia uma solicitação HTTP GET para a Graph API.</span><span class="sxs-lookup"><span data-stu-id="f2daf-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request to the Graph API.</span></span> <span data-ttu-id="f2daf-187">Antes de `B2CGraphClient.SendGraphGetRequest(...)` enviar a solicitação GET, ele obtém primeiro um token de acesso usando a ADAL:</span><span class="sxs-lookup"><span data-stu-id="f2daf-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends the GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL to acquire a token by using the app's identity (the credential)
    // The first parameter is the resource we want an access_token for; in this case, the Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="f2daf-188">Você pode obter um token de acesso para a API do Graph chamando o método ADAL `AuthenticationContext.AcquireToken(...)` .</span><span class="sxs-lookup"><span data-stu-id="f2daf-188">You can get an access token for the Graph API by calling the ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="f2daf-189">Em seguida, a ADAL retorna um `access_token` que representa a identidade do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f2daf-189">ADAL then returns an `access_token` that represents the application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="f2daf-190">Ler usuários</span><span class="sxs-lookup"><span data-stu-id="f2daf-190">Read users</span></span>
<span data-ttu-id="f2daf-191">Quando quiser obter uma lista de usuários ou obter um usuário específico da API do Graph, você poderá enviar uma solicitação HTTP `GET` para o ponto de extremidade `/users`.</span><span class="sxs-lookup"><span data-stu-id="f2daf-191">When you want to get a list of users or get a particular user from the Graph API, you can send an HTTP `GET` request to the `/users` endpoint.</span></span> <span data-ttu-id="f2daf-192">Uma solicitação para todos os usuários em um locatário tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="f2daf-192">A request for all of the users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="f2daf-193">Para ver essa solicitação, execute:</span><span class="sxs-lookup"><span data-stu-id="f2daf-193">To see this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="f2daf-194">Há dois aspectos importantes a serem observados:</span><span class="sxs-lookup"><span data-stu-id="f2daf-194">There are two important things to note:</span></span>

* <span data-ttu-id="f2daf-195">O token de acesso adquirido pela ADAL foi adicionado ao cabeçalho `Authorization` usando o esquema `Bearer`.</span><span class="sxs-lookup"><span data-stu-id="f2daf-195">The access token acquired via ADAL is added to the `Authorization` header by using the `Bearer` scheme.</span></span>
* <span data-ttu-id="f2daf-196">Para locatários B2C, você deve usar o parâmetro de consulta `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="f2daf-196">For B2C tenants, you must use the query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="f2daf-197">Ambos esses detalhes são tratados no `B2CGraphClient.SendGraphGetRequest(...)` método:</span><span class="sxs-lookup"><span data-stu-id="f2daf-197">Both of these details are handled in the `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure to use the 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append the access token for the Graph API to the Authorization header of the request by using the Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="f2daf-198">Criar contas de usuário consumidor</span><span class="sxs-lookup"><span data-stu-id="f2daf-198">Create consumer user accounts</span></span>
<span data-ttu-id="f2daf-199">Ao criar contas de usuário no locatário B2C, você pode enviar uma solicitação HTTP `POST` para o ponto de extremidade `/users`:</span><span class="sxs-lookup"><span data-stu-id="f2daf-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request to the `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required to create consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier the user uses to sign in to the account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set to 'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying to the end user
    "mailNickname": "joec",                        // an email alias for the user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set to false
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="f2daf-200">A maioria das propriedades nesta solicitação é necessária para criar usuários consumidores.</span><span class="sxs-lookup"><span data-stu-id="f2daf-200">Most of these properties in this request are required to create consumer users.</span></span> <span data-ttu-id="f2daf-201">Para saber mais, clique [aqui](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="f2daf-201">To learn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="f2daf-202">Observe que os comentários `//` foram incluídos para fins de ilustração.</span><span class="sxs-lookup"><span data-stu-id="f2daf-202">Note that the `//` comments have been included for illustration.</span></span> <span data-ttu-id="f2daf-203">Não os inclua em uma solicitação real.</span><span class="sxs-lookup"><span data-stu-id="f2daf-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="f2daf-204">Para ver a solicitação, execute um dos seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="f2daf-204">To see the request, run one of the following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="f2daf-205">O comando `Create-User` usa um arquivo .json como parâmetro de entrada.</span><span class="sxs-lookup"><span data-stu-id="f2daf-205">The `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="f2daf-206">Ele contém uma representação JSON de um objeto de usuário.</span><span class="sxs-lookup"><span data-stu-id="f2daf-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="f2daf-207">Existem dois arquivos .json de exemplo no código de exemplo: `usertemplate-email.json` e `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="f2daf-207">There are two sample .json files in the sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="f2daf-208">Você pode modificar esses arquivos para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="f2daf-208">You can modify these files to suit your needs.</span></span> <span data-ttu-id="f2daf-209">Além dos campos necessários acima, há vários campos opcionais incluídos nesses arquivos que você pode usar.</span><span class="sxs-lookup"><span data-stu-id="f2daf-209">In addition to the required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="f2daf-210">Detalhes sobre os campos opcionais podem ser encontrados na [Referência de entidade da API do Graph do Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="f2daf-210">Details on the optional fields can be found in the [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="f2daf-211">Você pode ver como a solicitação POST é construída em `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="f2daf-211">You can see how the POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="f2daf-212">Ela anexa um token de acesso ao cabeçalho `Authorization` da solicitação.</span><span class="sxs-lookup"><span data-stu-id="f2daf-212">It attaches an access token to the `Authorization` header of the request.</span></span>
* <span data-ttu-id="f2daf-213">Ela define `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="f2daf-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="f2daf-214">Ela inclui o objeto de usuário JSON no corpo da solicitação.</span><span class="sxs-lookup"><span data-stu-id="f2daf-214">It includes the JSON user object in the body of the request.</span></span>

> [!NOTE]
> <span data-ttu-id="f2daf-215">Se as contas que deseja migrar de um repositório do usuário existente tiverem um nível de segurança de senha menor do que o [nível de segurança de senha forte imposto pelo Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), você poderá desabilitar o requisito de senha forte usando o valor `DisableStrongPassword` na propriedade `passwordPolicies`.</span><span class="sxs-lookup"><span data-stu-id="f2daf-215">If the accounts that you want to migrate from an existing user store has lower password strength than the [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable the strong password requirement using the `DisableStrongPassword` value in the `passwordPolicies` property.</span></span> <span data-ttu-id="f2daf-216">Por exemplo, você pode modificar a solicitação de criação de usuário fornecida acima da seguinte maneira: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="f2daf-216">For instance, you can modify the create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="f2daf-217">Atualizar contas de usuário consumidor</span><span class="sxs-lookup"><span data-stu-id="f2daf-217">Update consumer user accounts</span></span>
<span data-ttu-id="f2daf-218">Quando você atualiza os objetos de usuário, o processo é semelhante àquele usado para criar objetos de usuário.</span><span class="sxs-lookup"><span data-stu-id="f2daf-218">When you update user objects, the process is similar to the one you use to create user objects.</span></span> <span data-ttu-id="f2daf-219">Mas esse processo usa o método HTTP `PATCH` :</span><span class="sxs-lookup"><span data-stu-id="f2daf-219">But this process uses the HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only the user's displayName
}
```

<span data-ttu-id="f2daf-220">Tente atualizar um usuário atualizando os arquivos JSON com novos dados.</span><span class="sxs-lookup"><span data-stu-id="f2daf-220">Try to update a user by updating your JSON files with new data.</span></span> <span data-ttu-id="f2daf-221">Você pode usar o `B2CGraphClient` para executar um destes comandos:</span><span class="sxs-lookup"><span data-stu-id="f2daf-221">You can then use `B2CGraphClient` to run one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="f2daf-222">Inspecione o `B2CGraphClient.SendGraphPatchRequest(...)` método para obter detalhes sobre como enviar esta solicitação.</span><span class="sxs-lookup"><span data-stu-id="f2daf-222">Inspect the `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how to send this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="f2daf-223">Pesquisar usuários</span><span class="sxs-lookup"><span data-stu-id="f2daf-223">Search users</span></span>
<span data-ttu-id="f2daf-224">É possível pesquisar usuários em seu locatário B2C de duas maneiras.</span><span class="sxs-lookup"><span data-stu-id="f2daf-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="f2daf-225">Uma delas é usar a ID de objeto do usuário. A segunda opção é usar o identificador de entrada do usuário (ou seja, a propriedade `signInNames`).</span><span class="sxs-lookup"><span data-stu-id="f2daf-225">One, using the user's object ID or two, using the user's sign-in identifer (i.e., the `signInNames` property).</span></span>

<span data-ttu-id="f2daf-226">Execute um dos seguintes comandos para pesquisar um usuário específico:</span><span class="sxs-lookup"><span data-stu-id="f2daf-226">Run one of the following commands to search for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="f2daf-227">Aqui estão alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="f2daf-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="f2daf-228">Excluir usuários</span><span class="sxs-lookup"><span data-stu-id="f2daf-228">Delete users</span></span>
<span data-ttu-id="f2daf-229">O processo de exclusão de um usuário é simples.</span><span class="sxs-lookup"><span data-stu-id="f2daf-229">The process for deleting a user is straightforward.</span></span> <span data-ttu-id="f2daf-230">Use o método HTTP `DELETE` e construa a URL com a ID de objeto correta:</span><span class="sxs-lookup"><span data-stu-id="f2daf-230">Use the HTTP `DELETE` method and construct the URL with the correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="f2daf-231">Para ver um exemplo, insira esse comando e exiba a solicitação Delete exclusão resultante que é mostrada no console:</span><span class="sxs-lookup"><span data-stu-id="f2daf-231">To see an example, enter this command and view the delete request that is printed to the console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="f2daf-232">Inspecione o `B2CGraphClient.SendGraphDeleteRequest(...)` método para obter detalhes sobre como enviar esta solicitação.</span><span class="sxs-lookup"><span data-stu-id="f2daf-232">Inspect the `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how to send this request.</span></span>

<span data-ttu-id="f2daf-233">Você pode executar outras ações com a API do Graph do Azure AD além do gerenciamento de usuários.</span><span class="sxs-lookup"><span data-stu-id="f2daf-233">You can perform many other actions with the Azure AD Graph API in addition to user management.</span></span> <span data-ttu-id="f2daf-234">A [Referência da API do Graph do Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) fornece detalhes de cada ação, bem como solicitações de exemplo.</span><span class="sxs-lookup"><span data-stu-id="f2daf-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="f2daf-235">Usar atributos personalizados</span><span class="sxs-lookup"><span data-stu-id="f2daf-235">Use custom attributes</span></span>
<span data-ttu-id="f2daf-236">Quase todos os aplicativos consumidores precisam armazenar algum tipo de informação de perfil de usuário personalizada.</span><span class="sxs-lookup"><span data-stu-id="f2daf-236">Most consumer applications need to store some type of custom user profile information.</span></span> <span data-ttu-id="f2daf-237">Uma maneira de fazer isso é definir um atributo personalizado em seu locatário B2C.</span><span class="sxs-lookup"><span data-stu-id="f2daf-237">One way you can do this is to define a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="f2daf-238">Em seguida, você pode tratar esse atributo da mesma maneira que trata qualquer outra propriedade em um objeto de usuário.</span><span class="sxs-lookup"><span data-stu-id="f2daf-238">You can then treat that attribute the same way you treat any other property on a user object.</span></span> <span data-ttu-id="f2daf-239">Você pode atualizar, excluir ou consultar o atributo, enviá-lo como uma declaração de entrada em tokens e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="f2daf-239">You can update the attribute, delete the attribute, query by the attribute, send the attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="f2daf-240">Para definir um atributo personalizado no locatário B2C, veja a [Referência de atributo personalizado do B2C](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="f2daf-240">To define a custom attribute in your B2C tenant, see the [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="f2daf-241">Você pode exibir os atributos personalizados definidos no locatário B2C usando `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="f2daf-241">You can view the custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="f2daf-242">A saída dessas funções revela os detalhes de cada atributo personalizado, como:</span><span class="sxs-lookup"><span data-stu-id="f2daf-242">The output of these functions reveals the details of each custom attribute, such as:</span></span>

```JSON
{
      "odata.type": "Microsoft.DirectoryServices.ExtensionProperty",
      "objectType": "ExtensionProperty",
      "objectId": "cec6391b-204d-42fe-8f7c-89c2b1964fca",
      "deletionTimestamp": null,
      "appDisplayName": "",
      "name": "extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number",
      "dataType": "Integer",
      "isSyncedFromOnPremises": false,
      "targetObjects": [
        "User"
      ]
}
```

<span data-ttu-id="f2daf-243">Você pode usar o nome completo, como `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, como uma propriedade nos objetos de usuário.</span><span class="sxs-lookup"><span data-stu-id="f2daf-243">You can use the full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="f2daf-244">Atualize seu arquivo .json com a nova propriedade e um valor para a propriedade e execute:</span><span class="sxs-lookup"><span data-stu-id="f2daf-244">Update your .json file with the new property and a value for the property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="f2daf-245">Usando `B2CGraphClient`, você terá um aplicativo de serviço que pode gerenciar os usuários de locatário B2C de forma programática.</span><span class="sxs-lookup"><span data-stu-id="f2daf-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="f2daf-246">`B2CGraphClient` usa sua própria identidade de aplicativo para se autenticar na API do Graph do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f2daf-246">`B2CGraphClient` uses its own application identity to authenticate to the Azure AD Graph API.</span></span> <span data-ttu-id="f2daf-247">Ele também adquire tokens usando um segredo do cliente.</span><span class="sxs-lookup"><span data-stu-id="f2daf-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="f2daf-248">Ao incorporar essa funcionalidade a seu aplicativo, lembre-se de alguns pontos importantes para aplicativos B2C:</span><span class="sxs-lookup"><span data-stu-id="f2daf-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="f2daf-249">Você precisa conceder ao aplicativo as permissões apropriadas no locatário.</span><span class="sxs-lookup"><span data-stu-id="f2daf-249">You need to grant the application the proper permissions in the tenant.</span></span>
* <span data-ttu-id="f2daf-250">Por enquanto, você precisa usar ADAL (não MSAL) para obter tokens de acesso.</span><span class="sxs-lookup"><span data-stu-id="f2daf-250">For now, you need to use ADAL (not MSAL) to get access tokens.</span></span> <span data-ttu-id="f2daf-251">(Você também pode enviar mensagens de protocolo diretamente, sem usar uma biblioteca.)</span><span class="sxs-lookup"><span data-stu-id="f2daf-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="f2daf-252">Ao chamar a API do Graph, use `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="f2daf-252">When you call the Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="f2daf-253">Quando você cria e atualiza usuários consumidores, algumas propriedades são obrigatórias, conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="f2daf-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="f2daf-254">Se você tiver perguntas ou solicitações de ações que deseja executar usando a API do Graph em seu locatário B2C, deixe um comentário sobre este artigo ou apresente um problema no repositório de código de exemplo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="f2daf-254">If you have any questions or requests for actions you would like to perform by using the Graph API on your B2C tenant, leave a comment on this article or file an issue in the GitHub code sample repository.</span></span>

