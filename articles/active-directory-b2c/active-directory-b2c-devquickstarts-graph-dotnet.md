---
title: "B2C de diretório ativo do Azure: Saudação de uso API do Graph | Microsoft Docs"
description: "Como toocall hello Graph API para um locatário B2C usando um processo de saudação de tooautomate de identidade de aplicativo."
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
ms.openlocfilehash: a17cdc4adf57dbf22592d99ef8ecde41652763fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-b2c-use-hello-graph-api"></a><span data-ttu-id="99b15-103">B2C do AD do Azure: Use Olá API do Graph</span><span class="sxs-lookup"><span data-stu-id="99b15-103">Azure AD B2C: Use hello Graph API</span></span>
<span data-ttu-id="99b15-104">Locatários do Active Directory (AD do Azure) B2C do Azure tendem toobe muito grande.</span><span class="sxs-lookup"><span data-stu-id="99b15-104">Azure Active Directory (Azure AD) B2C tenants tend toobe very large.</span></span> <span data-ttu-id="99b15-105">Isso significa que muitas tarefas comuns de gerenciamento de locatário necessário toobe executada de forma programática.</span><span class="sxs-lookup"><span data-stu-id="99b15-105">This means that many common tenant management tasks need toobe performed programmatically.</span></span> <span data-ttu-id="99b15-106">O principal exemplo é o gerenciamento de usuário.</span><span class="sxs-lookup"><span data-stu-id="99b15-106">A primary example is user management.</span></span> <span data-ttu-id="99b15-107">Talvez seja necessário toomigrate um locatário de B2C tooa do repositório do usuário existente.</span><span class="sxs-lookup"><span data-stu-id="99b15-107">You might need toomigrate an existing user store tooa B2C tenant.</span></span> <span data-ttu-id="99b15-108">Você pode desejar toohost registro de usuário em sua página e criar contas de usuário no diretório do Azure AD B2C em segundo plano da saudação.</span><span class="sxs-lookup"><span data-stu-id="99b15-108">You may want toohost user registration on your own page and create user accounts in your Azure AD B2C directory behind hello scenes.</span></span> <span data-ttu-id="99b15-109">Esses tipos de tarefas exigem Olá capacidade toocreate, ler, atualizar e excluir contas de usuário.</span><span class="sxs-lookup"><span data-stu-id="99b15-109">These types of tasks require hello ability toocreate, read, update, and delete user accounts.</span></span> <span data-ttu-id="99b15-110">Você pode fazer essas tarefas usando hello Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="99b15-110">You can do these tasks by using hello Azure AD Graph API.</span></span>

<span data-ttu-id="99b15-111">Para B2C locatários, há dois modos principais de se comunicar com hello API do Graph.</span><span class="sxs-lookup"><span data-stu-id="99b15-111">For B2C tenants, there are two primary modes of communicating with hello Graph API.</span></span>

* <span data-ttu-id="99b15-112">Para tarefas interativas, executar uma vez, você deve agir como uma conta de administrador no locatário de B2C hello quando você executa tarefas de saudação.</span><span class="sxs-lookup"><span data-stu-id="99b15-112">For interactive, run-once tasks, you should act as an administrator account in hello B2C tenant when you perform hello tasks.</span></span> <span data-ttu-id="99b15-113">Esse modo requer toosign um administrador com credenciais antes que o administrador pode executar qualquer toohello chamadas API do Graph.</span><span class="sxs-lookup"><span data-stu-id="99b15-113">This mode requires an administrator toosign in with credentials before that admin can perform any calls toohello Graph API.</span></span>
* <span data-ttu-id="99b15-114">Para tarefas automatizadas, contínuas, você deve usar algum tipo de conta de serviço que você fornecer com tarefas de gerenciamento de tooperform Olá os privilégios necessários.</span><span class="sxs-lookup"><span data-stu-id="99b15-114">For automated, continuous tasks, you should use some type of service account that you provide with hello necessary privileges tooperform management tasks.</span></span> <span data-ttu-id="99b15-115">No AD do Azure, você pode fazer isso por registrar um aplicativo e autenticação tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="99b15-115">In Azure AD, you can do this by registering an application and authenticating tooAzure AD.</span></span> <span data-ttu-id="99b15-116">Isso é feito usando um **ID do aplicativo** que usa Olá [as credenciais do cliente OAuth 2.0](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span><span class="sxs-lookup"><span data-stu-id="99b15-116">This is done by using an **Application ID** that uses hello [OAuth 2.0 client credentials grant](../active-directory/develop/active-directory-authentication-scenarios.md#daemon-or-server-application-to-web-api).</span></span> <span data-ttu-id="99b15-117">Nesse caso, aplicativo hello atua como em si, não como um usuário, Olá toocall API do Graph.</span><span class="sxs-lookup"><span data-stu-id="99b15-117">In this case, hello application acts as itself, not as a user, toocall hello Graph API.</span></span>

<span data-ttu-id="99b15-118">Neste artigo, discutiremos como tooperform Olá caso de uso automatizada.</span><span class="sxs-lookup"><span data-stu-id="99b15-118">In this article, we'll discuss how tooperform hello automated-use case.</span></span> <span data-ttu-id="99b15-119">toodemonstrate, criaremos um .NET 4.5 `B2CGraphClient` que executa o usuário criar, ler, atualizar e excluir operações (CRUD).</span><span class="sxs-lookup"><span data-stu-id="99b15-119">toodemonstrate, we'll build a .NET 4.5 `B2CGraphClient` that performs user create, read, update, and delete (CRUD) operations.</span></span> <span data-ttu-id="99b15-120">cliente Olá terá uma interface de linha de comando do Windows (CLI) que permite que você tooinvoke vários métodos.</span><span class="sxs-lookup"><span data-stu-id="99b15-120">hello client will have a Windows command-line interface (CLI) that allows you tooinvoke various methods.</span></span> <span data-ttu-id="99b15-121">No entanto, o código de saudação é gravado toobehave de maneira interativa, automatizada.</span><span class="sxs-lookup"><span data-stu-id="99b15-121">However, hello code is written toobehave in a noninteractive, automated fashion.</span></span>

## <a name="get-an-azure-ad-b2c-tenant"></a><span data-ttu-id="99b15-122">Obter um locatário do Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="99b15-122">Get an Azure AD B2C tenant</span></span>
<span data-ttu-id="99b15-123">Antes de criar aplicativos ou usuários, ou interagir com o Azure AD em todos os, será necessário um locatário Azure AD B2C e uma conta de administrador global no locatário hello.</span><span class="sxs-lookup"><span data-stu-id="99b15-123">Before you can create applications or users, or interact with Azure AD at all, you will need an Azure AD B2C tenant and a global administrator account in hello tenant.</span></span> <span data-ttu-id="99b15-124">Se você ainda não tiver um locatário, confira a [introdução ao Azure AD B2C](active-directory-b2c-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="99b15-124">If you don't have a tenant already, [get started with Azure AD B2C](active-directory-b2c-get-started.md).</span></span>

## <a name="register-your-application-in-your-tenant"></a><span data-ttu-id="99b15-125">Registrar seu aplicativo em seu locatário</span><span class="sxs-lookup"><span data-stu-id="99b15-125">Register your application in your tenant</span></span>
<span data-ttu-id="99b15-126">Depois que você tiver um locatário B2C, você precisa tooregister seu aplicativo por meio de saudação [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="99b15-126">After you have a B2C tenant, you need tooregister your application via hello [Azure Portal](https://portal.azure.com).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99b15-127">toouse Olá Graph API com seu locatário B2C, você precisará tooregister um aplicativo dedicado usando Olá genérico *registros do aplicativo* folha em Olá Portal do Azure, **não** do Azure AD B2C  *Aplicativos* folha.</span><span class="sxs-lookup"><span data-stu-id="99b15-127">toouse hello Graph API with your B2C tenant, you will need tooregister a dedicated application by using hello generic *App Registrations* blade in hello Azure Portal, **NOT** Azure AD B2C's *Applications* blade.</span></span> <span data-ttu-id="99b15-128">Não é possível reutilizar Olá já existente B2C aplicativos que você registrou no saudação do Azure AD B2C *aplicativos* folha.</span><span class="sxs-lookup"><span data-stu-id="99b15-128">You can't reuse hello already-existing B2C applications that you registered in hello Azure AD B2C's *Applications* blade.</span></span>

1. <span data-ttu-id="99b15-129">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="99b15-129">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="99b15-130">Escolha seu locatário do Azure AD B2C selecionando sua conta no canto superior direito de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="99b15-130">Choose your Azure AD B2C tenant by selecting your account in hello top right corner of hello page.</span></span>
3. <span data-ttu-id="99b15-131">No painel de navegação esquerdo hello, escolha **mais serviços**, clique em **registros do aplicativo**e clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="99b15-131">In hello left-hand navigation pane, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
4. <span data-ttu-id="99b15-132">Siga os prompts de saudação e criar um novo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99b15-132">Follow hello prompts and create a new application.</span></span> 
    1. <span data-ttu-id="99b15-133">Selecione **aplicativo Web / API** como Olá tipo de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99b15-133">Select **Web App / API** as hello Application Type.</span></span>    
    2. <span data-ttu-id="99b15-134">Forneça **qualquer URI de redirecionamento** (por exemplo, https://B2CGraphAPI), pois isso não é relevante para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="99b15-134">Provide **any redirect URI** (e.g. https://B2CGraphAPI) as it's not relevant for this example.</span></span>  
5. <span data-ttu-id="99b15-135">Olá aplicativo serão agora aparecem na lista de saudação de aplicativos, clique nela Olá tooobtain **ID do aplicativo** (também conhecido como ID do cliente).</span><span class="sxs-lookup"><span data-stu-id="99b15-135">hello application will now show up in hello list of applications, click on it tooobtain hello **Application ID** (also known as Client ID).</span></span> <span data-ttu-id="99b15-136">Copie-a, pois precisará dela em uma seção posterior.</span><span class="sxs-lookup"><span data-stu-id="99b15-136">Copy it as you'll need it in a later section.</span></span>
6. <span data-ttu-id="99b15-137">Na folha de configurações de saudação, clique em **chaves** e adicione uma nova chave (também conhecido como o segredo do cliente).</span><span class="sxs-lookup"><span data-stu-id="99b15-137">In hello Settings blade, click on **Keys** and add a new key (also known as client secret).</span></span> <span data-ttu-id="99b15-138">Copie-a também para uso em uma seção posterior.</span><span class="sxs-lookup"><span data-stu-id="99b15-138">Also copy it for use in a later section.</span></span>

## <a name="configure-create-read-and-update-permissions-for-your-application"></a><span data-ttu-id="99b15-139">Configurar as permissões de criação, leitura e atualização para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="99b15-139">Configure create, read and update permissions for your application</span></span>
<span data-ttu-id="99b15-140">Agora você precisa tooconfigure seu tooget aplicativo que todos Olá necessário toocreate permissões, ler, atualizar e excluir usuários.</span><span class="sxs-lookup"><span data-stu-id="99b15-140">Now you need tooconfigure your application tooget all hello required permissions toocreate, read, update and delete users.</span></span>

1. <span data-ttu-id="99b15-141">Continuar em Olá folha de registros do aplicativo do portal do Azure, selecione seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="99b15-141">Continuing in hello Azure portal's App Registrations blade, select your application.</span></span>
2. <span data-ttu-id="99b15-142">Na folha de configurações de saudação, clique em **as permissões necessárias**.</span><span class="sxs-lookup"><span data-stu-id="99b15-142">In hello Settings blade, click on **Required permissions**.</span></span>
3. <span data-ttu-id="99b15-143">Na folha de permissões necessárias de saudação, clique em **Windows Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="99b15-143">In hello Required permissions blade, click on **Windows Azure Active Directory**.</span></span>
4. <span data-ttu-id="99b15-144">Na folha de habilitar o acesso de saudação, selecione Olá **ler e gravar dados de diretório** permissão de **permissões de aplicativo** e clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="99b15-144">In hello Enable Access  blade, select hello **Read and write directory data** permission from **Application Permissions** and click **Save**.</span></span>
5. <span data-ttu-id="99b15-145">Por fim, na folha de permissões necessárias hello, clique em Olá **conceder permissões** botão.</span><span class="sxs-lookup"><span data-stu-id="99b15-145">Finally, back in hello Required permissions blade, click on hello **Grant Permissions** button.</span></span>

<span data-ttu-id="99b15-146">Agora você tem um aplicativo que tem permissão a usuários toocreate, leitura e atualização do seu locatário B2C.</span><span class="sxs-lookup"><span data-stu-id="99b15-146">You now have an application that has permission toocreate, read and update users from your B2C tenant.</span></span>

## <a name="configure-delete-permissions-for-your-application"></a><span data-ttu-id="99b15-147">Configurar permissões de exclusão para seu aplicativo</span><span class="sxs-lookup"><span data-stu-id="99b15-147">Configure delete permissions for your application</span></span>
<span data-ttu-id="99b15-148">Atualmente, Olá *ler e gravar dados de diretório* permissão **não** incluem hello capacidade toodo qualquer exclusão como excluir usuários.</span><span class="sxs-lookup"><span data-stu-id="99b15-148">Currently, hello *Read and write directory data* permission does **NOT** include hello ability toodo any deletions such as deleting users.</span></span> <span data-ttu-id="99b15-149">Se você quiser toogive os usuários do aplicativo hello capacidade toodelete, você precisará toodo estas etapas adicionais que envolvem o PowerShell, caso contrário, você pode ignorar toohello próxima seção.</span><span class="sxs-lookup"><span data-stu-id="99b15-149">If you want toogive your application hello ability toodelete users, you'll need toodo these extra steps that involve PowerShell, otherwise, you can skip toohello next section.</span></span>

<span data-ttu-id="99b15-150">Primeiro, baixe e instale Olá [assistente Microsoft Online Services entrar](http://go.microsoft.com/fwlink/?LinkID=286152).</span><span class="sxs-lookup"><span data-stu-id="99b15-150">First, download and install hello [Microsoft Online Services Sign-In Assistant](http://go.microsoft.com/fwlink/?LinkID=286152).</span></span> <span data-ttu-id="99b15-151">Baixe e instale Olá [módulo do Active Directory do Azure de 64 bits do Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span><span class="sxs-lookup"><span data-stu-id="99b15-151">Then download and install hello [64-bit Azure Active Directory module for Windows PowerShell](http://go.microsoft.com/fwlink/p/?linkid=236297).</span></span>

<span data-ttu-id="99b15-152">Depois de instalar o módulo do PowerShell hello, abra o PowerShell e conecte-se tooyour B2C locatário.</span><span class="sxs-lookup"><span data-stu-id="99b15-152">After you install hello PowerShell module, open PowerShell and connect tooyour B2C tenant.</span></span> <span data-ttu-id="99b15-153">Depois de executar `Get-Credential`, você será solicitado um nome de usuário e senha, insira Olá nome de usuário e senha da sua conta de administrador de inquilinos B2C.</span><span class="sxs-lookup"><span data-stu-id="99b15-153">After you run `Get-Credential`, you will be prompted for a user name and password, Enter hello user name and password of your B2C tenant administrator account.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="99b15-154">Você precisa de conta de administrador do locatário toouse um B2C é **local** toohello B2C locatário.</span><span class="sxs-lookup"><span data-stu-id="99b15-154">You need toouse a B2C tenant administrator account that is **local** toohello B2C tenant.</span></span> <span data-ttu-id="99b15-155">Essas contas têm esta aparência: myusername@myb2ctenant.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="99b15-155">These accounts look like this: myusername@myb2ctenant.onmicrosoft.com.</span></span>

```powershell
Connect-MsolService
```

<span data-ttu-id="99b15-156">Agora, vamos usar Olá **ID do aplicativo** no script hello abaixo tooassign Olá Olá usuário conta administrador função de aplicativo que permitirá que ele toodelete usuários.</span><span class="sxs-lookup"><span data-stu-id="99b15-156">Now we'll use hello **Application ID** in hello script below tooassign hello application hello user account administrator role which will allow it toodelete users.</span></span> <span data-ttu-id="99b15-157">Essas funções têm identificadores conhecidos, para que você só precisa toodo é de entrada seu **ID do aplicativo** no script de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="99b15-157">These roles have well-known identifiers, so all you need toodo is input your **Application ID** in hello script below.</span></span>

```powershell
$applicationId = "<YOUR_APPLICATION_ID>"
$sp = Get-MsolServicePrincipal -AppPrincipalId $applicationId
Add-MsolRoleMember -RoleObjectId fe930be7-5e62-47db-91af-98c3a49a38b1 -RoleMemberObjectId $sp.ObjectId -RoleMemberType servicePrincipal
```

<span data-ttu-id="99b15-158">Seu aplicativo agora também tem permissões toodelete os usuários do seu locatário B2C.</span><span class="sxs-lookup"><span data-stu-id="99b15-158">Your application now also has permissions toodelete users from your B2C tenant.</span></span>

## <a name="download-configure-and-build-hello-sample-code"></a><span data-ttu-id="99b15-159">Baixar, configurar e compilar o código de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="99b15-159">Download, configure, and build hello sample code</span></span>
<span data-ttu-id="99b15-160">Primeiro, baixe o código de exemplo hello e executá-lo.</span><span class="sxs-lookup"><span data-stu-id="99b15-160">First, download hello sample code and get it running.</span></span> <span data-ttu-id="99b15-161">Em seguida, faremos uma análise mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="99b15-161">Then we will take a closer look at it.</span></span>  <span data-ttu-id="99b15-162">Você pode [baixar o código de exemplo hello como um arquivo. zip](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="99b15-162">You can [download hello sample code as a .zip file](https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet/archive/master.zip).</span></span> <span data-ttu-id="99b15-163">Você também pode cloná-lo em um diretório de sua escolha:</span><span class="sxs-lookup"><span data-stu-id="99b15-163">You can also clone it into a directory of your choice:</span></span>

```
git clone https://github.com/AzureADQuickStarts/B2C-GraphAPI-DotNet.git
```

<span data-ttu-id="99b15-164">Olá abrir `B2CGraphClient\B2CGraphClient.sln` solução do Visual Studio no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="99b15-164">Open hello `B2CGraphClient\B2CGraphClient.sln` Visual Studio solution in Visual Studio.</span></span> <span data-ttu-id="99b15-165">Em Olá `B2CGraphClient` projeto, o arquivo hello abrir `App.config`.</span><span class="sxs-lookup"><span data-stu-id="99b15-165">In hello `B2CGraphClient` project, open hello file `App.config`.</span></span> <span data-ttu-id="99b15-166">Substitua três configurações de aplicativo hello com seus próprios valores:</span><span class="sxs-lookup"><span data-stu-id="99b15-166">Replace hello three app settings with your own values:</span></span>

```
<appSettings>
    <add key="b2c:Tenant" value="{Your Tenant Name}" />
    <add key="b2c:ClientId" value="{hello ApplicationID from above}" />
    <add key="b2c:ClientSecret" value="{hello Key from above}" />
</appSettings>
```

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="99b15-167">Em seguida, clique duas vezes em Olá `B2CGraphClient` exemplo hello de solução e recompilação.</span><span class="sxs-lookup"><span data-stu-id="99b15-167">Next, right-click on hello `B2CGraphClient` solution and rebuild hello sample.</span></span> <span data-ttu-id="99b15-168">Se tiver êxito, agora deverá você ter um arquivo executável `B2C.exe` localizado em `B2CGraphClient\bin\Debug`.</span><span class="sxs-lookup"><span data-stu-id="99b15-168">If you are successful, you should now have a `B2C.exe` executable file located in `B2CGraphClient\bin\Debug`.</span></span>

## <a name="build-user-crud-operations-by-using-hello-graph-api"></a><span data-ttu-id="99b15-169">Criar operações CRUD de usuário usando Olá API do Graph</span><span class="sxs-lookup"><span data-stu-id="99b15-169">Build user CRUD operations by using hello Graph API</span></span>
<span data-ttu-id="99b15-170">Olá toouse B2CGraphClient, abra um `cmd` Windows command prompt e altere seu diretório toohello `Debug` directory.</span><span class="sxs-lookup"><span data-stu-id="99b15-170">toouse hello B2CGraphClient, open a `cmd` Windows command prompt and change your directory toohello `Debug` directory.</span></span> <span data-ttu-id="99b15-171">Em seguida, execute Olá `B2C Help` comando.</span><span class="sxs-lookup"><span data-stu-id="99b15-171">Then run hello `B2C Help` command.</span></span>

```
> cd B2CGraphClient\bin\Debug
> B2C Help
```

<span data-ttu-id="99b15-172">Isso exibirá uma breve descrição de cada comando.</span><span class="sxs-lookup"><span data-stu-id="99b15-172">This will display a brief description of each command.</span></span> <span data-ttu-id="99b15-173">Cada vez que você chamar um desses comandos, `B2CGraphClient` faz uma solicitação toohello API do Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="99b15-173">Each time you invoke one of these commands, `B2CGraphClient` makes a request toohello Azure AD Graph API.</span></span>

### <a name="get-an-access-token"></a><span data-ttu-id="99b15-174">Obter um token de acesso</span><span class="sxs-lookup"><span data-stu-id="99b15-174">Get an access token</span></span>
<span data-ttu-id="99b15-175">Qualquer solicitação toohello Graph API requer um token de acesso para autenticação.</span><span class="sxs-lookup"><span data-stu-id="99b15-175">Any request toohello Graph API requires an access token for authentication.</span></span> <span data-ttu-id="99b15-176">`B2CGraphClient`usa Olá código-fonte aberto biblioteca de autenticação do Active Directory (ADAL) toohelp adquirir tokens de acesso.</span><span class="sxs-lookup"><span data-stu-id="99b15-176">`B2CGraphClient` uses hello open-source Active Directory Authentication Library (ADAL) toohelp acquire access tokens.</span></span> <span data-ttu-id="99b15-177">A ADAL facilita a aquisição de tokens, fornecendo uma API simples e cuidando de alguns detalhes importantes, como armazenar em cache os tokens de acesso.</span><span class="sxs-lookup"><span data-stu-id="99b15-177">ADAL makes token acquisition easier by providing a simple API and taking care of some important details, such as caching access tokens.</span></span> <span data-ttu-id="99b15-178">Você não tem toouse tooget ADAL tokens, embora.</span><span class="sxs-lookup"><span data-stu-id="99b15-178">You don't have toouse ADAL tooget tokens, though.</span></span> <span data-ttu-id="99b15-179">Você também pode obter tokens ao criar solicitações HTTP.</span><span class="sxs-lookup"><span data-stu-id="99b15-179">You can also get tokens by crafting HTTP requests.</span></span>

> [!NOTE]
> <span data-ttu-id="99b15-180">Este exemplo de código usa ADAL v2 na ordem toocommunicate com hello API do Graph.</span><span class="sxs-lookup"><span data-stu-id="99b15-180">This code sample uses ADAL v2 in order toocommunicate with hello Graph API.</span></span>  <span data-ttu-id="99b15-181">Você deve usar o ADAL v2 ou v3 em ordem tooget os tokens de acesso que podem ser usados com hello Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="99b15-181">You must use ADAL v2 or v3 in order tooget access tokens which can be used with hello Azure AD Graph API.</span></span>
> 
> 

<span data-ttu-id="99b15-182">Quando `B2CGraphClient` é executado, ele cria uma instância de saudação `B2CGraphClient` classe.</span><span class="sxs-lookup"><span data-stu-id="99b15-182">When `B2CGraphClient` runs, it creates an instance of hello `B2CGraphClient` class.</span></span> <span data-ttu-id="99b15-183">construtor Olá para esta classe define uma estrutura de autenticação de ADAL:</span><span class="sxs-lookup"><span data-stu-id="99b15-183">hello constructor for this class sets up an ADAL authentication scaffolding:</span></span>

```C#
public B2CGraphClient(string clientId, string clientSecret, string tenant)
{
    // hello client_id, client_secret, and tenant are provided in Program.cs, which pulls hello values from App.config
    this.clientId = clientId;
    this.clientSecret = clientSecret;
    this.tenant = tenant;

    // hello AuthenticationContext is ADAL's primary class, in which you indicate hello tenant toouse.
    this.authContext = new AuthenticationContext("https://login.microsoftonline.com/" + tenant);

    // hello ClientCredential is where you pass in your client_id and client_secret, which are
    // provided tooAzure AD in order tooreceive an access_token by using hello app's identity.
    this.credential = new ClientCredential(clientId, clientSecret);
}
```

<span data-ttu-id="99b15-184">Vamos usar Olá `B2C Get-User` comando como um exemplo.</span><span class="sxs-lookup"><span data-stu-id="99b15-184">We'll use hello `B2C Get-User` command as an example.</span></span> <span data-ttu-id="99b15-185">Quando `B2C Get-User` for chamado sem qualquer entradas adicionais, Olá CLI chamadas Olá `B2CGraphClient.GetAllUsers(...)` método.</span><span class="sxs-lookup"><span data-stu-id="99b15-185">When `B2C Get-User` is invoked without any additional inputs, hello CLI calls hello `B2CGraphClient.GetAllUsers(...)` method.</span></span> <span data-ttu-id="99b15-186">Este método chama `B2CGraphClient.SendGraphGetRequest(...)`, que envia um toohello de solicitação HTTP GET API do Graph.</span><span class="sxs-lookup"><span data-stu-id="99b15-186">This method calls `B2CGraphClient.SendGraphGetRequest(...)`, which submits an HTTP GET request toohello Graph API.</span></span> <span data-ttu-id="99b15-187">Antes de `B2CGraphClient.SendGraphGetRequest(...)` envia Olá solicitação GET, ele primeiro obtém um token de acesso usando a ADAL:</span><span class="sxs-lookup"><span data-stu-id="99b15-187">Before `B2CGraphClient.SendGraphGetRequest(...)` sends hello GET request, it first gets an access token by using ADAL:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    // First, use ADAL tooacquire a token by using hello app's identity (hello credential)
    // hello first parameter is hello resource we want an access_token for; in this case, hello Graph API.
    AuthenticationResult result = authContext.AcquireToken("https://graph.windows.net", credential);

    ...

```

<span data-ttu-id="99b15-188">Você pode obter um acesso de token para Olá API do Graph por chamada hello ADAL `AuthenticationContext.AcquireToken(...)` método.</span><span class="sxs-lookup"><span data-stu-id="99b15-188">You can get an access token for hello Graph API by calling hello ADAL `AuthenticationContext.AcquireToken(...)` method.</span></span> <span data-ttu-id="99b15-189">ADAL, em seguida, retorna um `access_token` que representa a identidade do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="99b15-189">ADAL then returns an `access_token` that represents hello application's identity.</span></span>

### <a name="read-users"></a><span data-ttu-id="99b15-190">Ler usuários</span><span class="sxs-lookup"><span data-stu-id="99b15-190">Read users</span></span>
<span data-ttu-id="99b15-191">Quando você deseja tooget uma lista de usuários ou obter um usuário específico do hello API do Graph, você pode enviar um HTTP `GET` solicitação toohello `/users` ponto de extremidade.</span><span class="sxs-lookup"><span data-stu-id="99b15-191">When you want tooget a list of users or get a particular user from hello Graph API, you can send an HTTP `GET` request toohello `/users` endpoint.</span></span> <span data-ttu-id="99b15-192">Uma solicitação para todos os usuários de saudação em um locatário tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="99b15-192">A request for all of hello users in a tenant looks like this:</span></span>

```
GET https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="99b15-193">toosee essa solicitação, execute:</span><span class="sxs-lookup"><span data-stu-id="99b15-193">toosee this request, run:</span></span>

 ```
 > B2C Get-User
 ```

<span data-ttu-id="99b15-194">Há dois toonote de coisas importantes:</span><span class="sxs-lookup"><span data-stu-id="99b15-194">There are two important things toonote:</span></span>

* <span data-ttu-id="99b15-195">Olá token de acesso adquirido por meio do ADAL é adicionado toohello `Authorization` cabeçalho usando Olá `Bearer` esquema.</span><span class="sxs-lookup"><span data-stu-id="99b15-195">hello access token acquired via ADAL is added toohello `Authorization` header by using hello `Bearer` scheme.</span></span>
* <span data-ttu-id="99b15-196">Para locatários B2C, você deve usar o parâmetro de consulta Olá `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="99b15-196">For B2C tenants, you must use hello query parameter `api-version=1.6`.</span></span>

<span data-ttu-id="99b15-197">Ambos esses detalhes são tratados no hello `B2CGraphClient.SendGraphGetRequest(...)` método:</span><span class="sxs-lookup"><span data-stu-id="99b15-197">Both of these details are handled in hello `B2CGraphClient.SendGraphGetRequest(...)` method:</span></span>

```C#
public async Task<string> SendGraphGetRequest(string api, string query)
{
    ...

    // For B2C user management, be sure toouse hello 1.6 Graph API version.
    HttpClient http = new HttpClient();
    string url = "https://graph.windows.net/" + tenant + api + "?" + "api-version=1.6";
    if (!string.IsNullOrEmpty(query))
    {
        url += "&" + query;
    }

    // Append hello access token for hello Graph API toohello Authorization header of hello request by using hello Bearer scheme.
    HttpRequestMessage request = new HttpRequestMessage(HttpMethod.Get, url);
    request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
    HttpResponseMessage response = await http.SendAsync(request);

    ...
```

### <a name="create-consumer-user-accounts"></a><span data-ttu-id="99b15-198">Criar contas de usuário consumidor</span><span class="sxs-lookup"><span data-stu-id="99b15-198">Create consumer user accounts</span></span>
<span data-ttu-id="99b15-199">Ao criar contas de usuário em seu locatário B2C, você pode enviar um HTTP `POST` solicitação toohello `/users` ponto de extremidade:</span><span class="sxs-lookup"><span data-stu-id="99b15-199">When you create user accounts in your B2C tenant, you can send an HTTP `POST` request toohello `/users` endpoint:</span></span>

```
POST https://graph.windows.net/contosob2c.onmicrosoft.com/users?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 338

{
    // All of these properties are required toocreate consumer users.

    "accountEnabled": true,
    "signInNames": [                            // controls which identifier hello user uses toosign in toohello account
        {
            "type": "emailAddress",             // can be 'emailAddress' or 'userName'
            "value": "joeconsumer@gmail.com"
        }
    ],
    "creationType": "LocalAccount",            // always set too'LocalAccount'
    "displayName": "Joe Consumer",                // a value that can be used for displaying toohello end user
    "mailNickname": "joec",                        // an email alias for hello user
    "passwordProfile": {
        "password": "P@ssword!",
        "forceChangePasswordNextLogin": false   // always set toofalse
    },
    "passwordPolicies": "DisablePasswordExpiration"
}
```

<span data-ttu-id="99b15-200">A maioria dessas propriedades nesta solicitação é usuários do consumidor toocreate necessária.</span><span class="sxs-lookup"><span data-stu-id="99b15-200">Most of these properties in this request are required toocreate consumer users.</span></span> <span data-ttu-id="99b15-201">toolearn mais, clique em [aqui](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span><span class="sxs-lookup"><span data-stu-id="99b15-201">toolearn more, click [here](https://msdn.microsoft.com/library/azure/ad/graph/api/users-operations#CreateLocalAccountUser).</span></span> <span data-ttu-id="99b15-202">Observe que Olá `//` comentários foram incluídos para fins ilustrativos.</span><span class="sxs-lookup"><span data-stu-id="99b15-202">Note that hello `//` comments have been included for illustration.</span></span> <span data-ttu-id="99b15-203">Não os inclua em uma solicitação real.</span><span class="sxs-lookup"><span data-stu-id="99b15-203">Do not include them in an actual request.</span></span>

<span data-ttu-id="99b15-204">solicitação toosee hello, execute um dos Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="99b15-204">toosee hello request, run one of hello following commands:</span></span>

```
> B2C Create-User ..\..\..\usertemplate-email.json
> B2C Create-User ..\..\..\usertemplate-username.json
```

<span data-ttu-id="99b15-205">Olá `Create-User` comando usa um arquivo. JSON como um parâmetro de entrada.</span><span class="sxs-lookup"><span data-stu-id="99b15-205">hello `Create-User` command takes a .json file as an input parameter.</span></span> <span data-ttu-id="99b15-206">Ele contém uma representação JSON de um objeto de usuário.</span><span class="sxs-lookup"><span data-stu-id="99b15-206">This contains a JSON representation of a user object.</span></span> <span data-ttu-id="99b15-207">Há dois arquivos. JSON de exemplo no código de exemplo hello: `usertemplate-email.json` e `usertemplate-username.json`.</span><span class="sxs-lookup"><span data-stu-id="99b15-207">There are two sample .json files in hello sample code: `usertemplate-email.json` and `usertemplate-username.json`.</span></span> <span data-ttu-id="99b15-208">Você pode modificar esses arquivos toosuit suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="99b15-208">You can modify these files toosuit your needs.</span></span> <span data-ttu-id="99b15-209">Além disso, toohello necessários campos acima, vários campos opcionais que você pode usar são incluídos nesses arquivos.</span><span class="sxs-lookup"><span data-stu-id="99b15-209">In addition toohello required fields above, several optional fields that you can use are included in these files.</span></span> <span data-ttu-id="99b15-210">Obter detalhes sobre os campos opcionais Olá podem ser encontrados no Olá [referência de entidade de API do Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span><span class="sxs-lookup"><span data-stu-id="99b15-210">Details on hello optional fields can be found in hello [Azure AD Graph API entity reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#user-entity).</span></span>

<span data-ttu-id="99b15-211">Você pode ver como a solicitação POST Olá é construída no `B2CGraphClient.SendGraphPostRequest(...)`.</span><span class="sxs-lookup"><span data-stu-id="99b15-211">You can see how hello POST request is constructed in `B2CGraphClient.SendGraphPostRequest(...)`.</span></span>

* <span data-ttu-id="99b15-212">Anexa um toohello de token de acesso `Authorization` cabeçalho de solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="99b15-212">It attaches an access token toohello `Authorization` header of hello request.</span></span>
* <span data-ttu-id="99b15-213">Ela define `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="99b15-213">It sets `api-version=1.6`.</span></span>
* <span data-ttu-id="99b15-214">Objeto de usuário do JSON Olá estão incluídos no corpo de saudação da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="99b15-214">It includes hello JSON user object in hello body of hello request.</span></span>

> [!NOTE]
> <span data-ttu-id="99b15-215">Se Olá contas que você deseja toomigrate de um repositório de usuário existente tem a menor força da senha de saudação [força da senha forte imposta pelo Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), você pode desabilitar o requisito de senha forte hello usando Olá `DisableStrongPassword`valor Olá `passwordPolicies` propriedade.</span><span class="sxs-lookup"><span data-stu-id="99b15-215">If hello accounts that you want toomigrate from an existing user store has lower password strength than hello [strong password strength enforced by Azure AD B2C](https://msdn.microsoft.com/library/azure/jj943764.aspx), you can disable hello strong password requirement using hello `DisableStrongPassword` value in hello `passwordPolicies` property.</span></span> <span data-ttu-id="99b15-216">Por exemplo, você pode modificar Olá criar solicitação de usuário fornecidas acima da seguinte maneira: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span><span class="sxs-lookup"><span data-stu-id="99b15-216">For instance, you can modify hello create user request provided above as follows: `"passwordPolicies": "DisablePasswordExpiration, DisableStrongPassword"`.</span></span>
> 
> 

### <a name="update-consumer-user-accounts"></a><span data-ttu-id="99b15-217">Atualizar contas de usuário consumidor</span><span class="sxs-lookup"><span data-stu-id="99b15-217">Update consumer user accounts</span></span>
<span data-ttu-id="99b15-218">Quando você atualiza os objetos de usuário, o processo de saudação é semelhante toohello utiliza objetos de usuário toocreate.</span><span class="sxs-lookup"><span data-stu-id="99b15-218">When you update user objects, hello process is similar toohello one you use toocreate user objects.</span></span> <span data-ttu-id="99b15-219">Mas esse processo usa Olá HTTP `PATCH` método:</span><span class="sxs-lookup"><span data-stu-id="99b15-219">But this process uses hello HTTP `PATCH` method:</span></span>

```
PATCH https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
Content-Type: application/json
Content-Length: 37

{
    "displayName": "Joe Consumer",                // this request updates only hello user's displayName
}
```

<span data-ttu-id="99b15-220">Tente tooupdate um usuário, atualizando os arquivos JSON com novos dados.</span><span class="sxs-lookup"><span data-stu-id="99b15-220">Try tooupdate a user by updating your JSON files with new data.</span></span> <span data-ttu-id="99b15-221">Você pode usar `B2CGraphClient` toorun um destes comandos:</span><span class="sxs-lookup"><span data-stu-id="99b15-221">You can then use `B2CGraphClient` toorun one of these commands:</span></span>

```
> B2C Update-User <user-object-id> ..\..\..\usertemplate-email.json
> B2C Update-User <user-object-id> ..\..\..\usertemplate-username.json
```

<span data-ttu-id="99b15-222">Inspecionar Olá `B2CGraphClient.SendGraphPatchRequest(...)` método para obter detalhes sobre como toosend esta solicitação.</span><span class="sxs-lookup"><span data-stu-id="99b15-222">Inspect hello `B2CGraphClient.SendGraphPatchRequest(...)` method for details on how toosend this request.</span></span>

### <a name="search-users"></a><span data-ttu-id="99b15-223">Pesquisar usuários</span><span class="sxs-lookup"><span data-stu-id="99b15-223">Search users</span></span>
<span data-ttu-id="99b15-224">É possível pesquisar usuários em seu locatário B2C de duas maneiras.</span><span class="sxs-lookup"><span data-stu-id="99b15-224">You can search for users in your B2C tenant in a couple of ways.</span></span> <span data-ttu-id="99b15-225">Um, usando a ID de objeto ou a dois, usando o identificador de entrada do usuário de saudação do usuário hello (ou seja, Olá `signInNames` propriedade).</span><span class="sxs-lookup"><span data-stu-id="99b15-225">One, using hello user's object ID or two, using hello user's sign-in identifer (i.e., hello `signInNames` property).</span></span>

<span data-ttu-id="99b15-226">Execute um dos Olá toosearch de comandos para um usuário específico a seguir:</span><span class="sxs-lookup"><span data-stu-id="99b15-226">Run one of hello following commands toosearch for a specific user:</span></span>

```
> B2C Get-User <user-object-id>
> B2C Get-User <filter-query-expression>
```

<span data-ttu-id="99b15-227">Aqui estão alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="99b15-227">Here are a couple of examples:</span></span>

```
> B2C Get-User 2bcf1067-90b6-4253-9991-7f16449c2d91
> B2C Get-User $filter=signInNames/any(x:x/value%20eq%20%27joeconsumer@gmail.com%27)
```

### <a name="delete-users"></a><span data-ttu-id="99b15-228">Excluir usuários</span><span class="sxs-lookup"><span data-stu-id="99b15-228">Delete users</span></span>
<span data-ttu-id="99b15-229">processo de saudação à exclusão de um usuário é simples.</span><span class="sxs-lookup"><span data-stu-id="99b15-229">hello process for deleting a user is straightforward.</span></span> <span data-ttu-id="99b15-230">Olá Use HTTP `DELETE` método e construir URL Olá Olá corrigir ID de objeto:</span><span class="sxs-lookup"><span data-stu-id="99b15-230">Use hello HTTP `DELETE` method and construct hello URL with hello correct object ID:</span></span>

```
DELETE https://graph.windows.net/contosob2c.onmicrosoft.com/users/<user-object-id>?api-version=1.6
Authorization: Bearer eyJhbGciOiJSUzI1NiIsIng1dCI6IjdkRC1nZWNOZ1gxWmY3R0xrT3ZwT0IyZGNWQSIsInR5cCI6IkpXVCJ9.eyJhdWQiOiJod...
```

<span data-ttu-id="99b15-231">toosee por exemplo, insira esta solicitação de exclusão Olá comando e o modo de exibição que é impressa toohello console:</span><span class="sxs-lookup"><span data-stu-id="99b15-231">toosee an example, enter this command and view hello delete request that is printed toohello console:</span></span>

```
> B2C Delete-User <object-id-of-user>
```

<span data-ttu-id="99b15-232">Inspecionar Olá `B2CGraphClient.SendGraphDeleteRequest(...)` método para obter detalhes sobre como toosend esta solicitação.</span><span class="sxs-lookup"><span data-stu-id="99b15-232">Inspect hello `B2CGraphClient.SendGraphDeleteRequest(...)` method for details on how toosend this request.</span></span>

<span data-ttu-id="99b15-233">Você pode executar muitas outras ações com hello Azure AD Graph API no gerenciamento de toouser de adição.</span><span class="sxs-lookup"><span data-stu-id="99b15-233">You can perform many other actions with hello Azure AD Graph API in addition toouser management.</span></span> <span data-ttu-id="99b15-234">A [Referência da API do Graph do Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) fornece detalhes de cada ação, bem como solicitações de exemplo.</span><span class="sxs-lookup"><span data-stu-id="99b15-234">The [Azure AD Graph API reference](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/api-catalog) provides details on each action, along with sample requests.</span></span>

## <a name="use-custom-attributes"></a><span data-ttu-id="99b15-235">Usar atributos personalizados</span><span class="sxs-lookup"><span data-stu-id="99b15-235">Use custom attributes</span></span>
<span data-ttu-id="99b15-236">A maioria dos aplicativos de consumidor necessário toostore algum tipo de informações de perfil de usuário personalizada.</span><span class="sxs-lookup"><span data-stu-id="99b15-236">Most consumer applications need toostore some type of custom user profile information.</span></span> <span data-ttu-id="99b15-237">Uma forma que você pode fazer isso é toodefine um atributo personalizado no seu locatário B2C.</span><span class="sxs-lookup"><span data-stu-id="99b15-237">One way you can do this is toodefine a custom attribute in your B2C tenant.</span></span> <span data-ttu-id="99b15-238">Em seguida, você pode tratar Olá esse atributo mesma maneira que você trate qualquer outra propriedade em um objeto de usuário.</span><span class="sxs-lookup"><span data-stu-id="99b15-238">You can then treat that attribute hello same way you treat any other property on a user object.</span></span> <span data-ttu-id="99b15-239">Você pode atualizar o atributo hello, atributo de Olá exclusão, consulta pelo atributo Olá, enviar atributo hello como uma declaração em tokens de entrada e muito mais.</span><span class="sxs-lookup"><span data-stu-id="99b15-239">You can update hello attribute, delete hello attribute, query by hello attribute, send hello attribute as a claim in sign-in tokens, and more.</span></span>

<span data-ttu-id="99b15-240">toodefine um atributo personalizado no seu locatário B2C, consulte Olá [referência de atributo personalizado B2C](active-directory-b2c-reference-custom-attr.md).</span><span class="sxs-lookup"><span data-stu-id="99b15-240">toodefine a custom attribute in your B2C tenant, see hello [B2C custom attribute reference](active-directory-b2c-reference-custom-attr.md).</span></span>

<span data-ttu-id="99b15-241">Você pode exibir hello atributos personalizados definidos no seu locatário B2C usando `B2CGraphClient`:</span><span class="sxs-lookup"><span data-stu-id="99b15-241">You can view hello custom attributes defined in your B2C tenant by using `B2CGraphClient`:</span></span>

```
> B2C Get-B2C-Application
> B2C Get-Extension-Attribute <object-id-in-the-output-of-the-above-command>
```

<span data-ttu-id="99b15-242">saída de Hello dessas funções revela detalhes de saudação de cada atributo personalizado, como:</span><span class="sxs-lookup"><span data-stu-id="99b15-242">hello output of these functions reveals hello details of each custom attribute, such as:</span></span>

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

<span data-ttu-id="99b15-243">Você pode usar o hello nome completo, como `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, como uma propriedade em seus objetos de usuário.</span><span class="sxs-lookup"><span data-stu-id="99b15-243">You can use hello full name, such as `extension_55dc0861f9a44eb999e0a8a872204adb_Jersey_Number`, as a property on your user objects.</span></span>  <span data-ttu-id="99b15-244">Atualizar o arquivo. JSON com hello nova propriedade e um valor para a propriedade hello e, em seguida, execute:</span><span class="sxs-lookup"><span data-stu-id="99b15-244">Update your .json file with hello new property and a value for hello property, and then run:</span></span>

```
> B2C Update-User <object-id-of-user> <path-to-json-file>
```

<span data-ttu-id="99b15-245">Usando `B2CGraphClient`, você terá um aplicativo de serviço que pode gerenciar os usuários de locatário B2C de forma programática.</span><span class="sxs-lookup"><span data-stu-id="99b15-245">By using `B2CGraphClient`, you have a service application that can manage your B2C tenant users programmatically.</span></span> <span data-ttu-id="99b15-246">`B2CGraphClient`usa seu próprio toohello de tooauthenticate de identidade de aplicativo do Azure AD Graph API.</span><span class="sxs-lookup"><span data-stu-id="99b15-246">`B2CGraphClient` uses its own application identity tooauthenticate toohello Azure AD Graph API.</span></span> <span data-ttu-id="99b15-247">Ele também adquire tokens usando um segredo do cliente.</span><span class="sxs-lookup"><span data-stu-id="99b15-247">It also acquires tokens by using a client secret.</span></span> <span data-ttu-id="99b15-248">Ao incorporar essa funcionalidade a seu aplicativo, lembre-se de alguns pontos importantes para aplicativos B2C:</span><span class="sxs-lookup"><span data-stu-id="99b15-248">As you incorporate this functionality into your application, remember a few key points for B2C apps:</span></span>

* <span data-ttu-id="99b15-249">É necessário toogrant Olá aplicativo hello permissões adequadas no locatário hello.</span><span class="sxs-lookup"><span data-stu-id="99b15-249">You need toogrant hello application hello proper permissions in hello tenant.</span></span>
* <span data-ttu-id="99b15-250">Por enquanto, você precisa de tokens de acesso de tooget toouse ADAL (não MSAL).</span><span class="sxs-lookup"><span data-stu-id="99b15-250">For now, you need toouse ADAL (not MSAL) tooget access tokens.</span></span> <span data-ttu-id="99b15-251">(Você também pode enviar mensagens de protocolo diretamente, sem usar uma biblioteca.)</span><span class="sxs-lookup"><span data-stu-id="99b15-251">(You can also send protocol messages directly, without using a library.)</span></span>
* <span data-ttu-id="99b15-252">Quando você chama hello Graph API, use `api-version=1.6`.</span><span class="sxs-lookup"><span data-stu-id="99b15-252">When you call hello Graph API, use `api-version=1.6`.</span></span>
* <span data-ttu-id="99b15-253">Quando você cria e atualiza usuários consumidores, algumas propriedades são obrigatórias, conforme descrito acima.</span><span class="sxs-lookup"><span data-stu-id="99b15-253">When you create and update consumer users, a few properties are required, as described above.</span></span>

<span data-ttu-id="99b15-254">Se você tiver perguntas ou solicitações de ações que você gostaria que tooperform usando Olá API do Graph em seu locatário B2C, deixe um comentário sobre este artigo ou um problema de arquivos no repositório de exemplo de código Olá GitHub.</span><span class="sxs-lookup"><span data-stu-id="99b15-254">If you have any questions or requests for actions you would like tooperform by using hello Graph API on your B2C tenant, leave a comment on this article or file an issue in hello GitHub code sample repository.</span></span>

