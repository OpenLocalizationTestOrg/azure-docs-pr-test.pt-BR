---
title: "aaaLog em tooAzure de saudação CLI | Microsoft Docs"
description: Conecte-se tooyour assinatura do Azure do hello Azure Interface de linha de comando (CLI do Azure) para Windows, Linux e Mac
editor: tysonn
manager: timlt
documentationcenter: 
author: squillace
services: virtual-machines-linux,virtual-network,storage,azure-resource-manager
tags: azure-resource-manager,azure-service-management
ms.assetid: ed856527-d75e-4e16-93fb-253dafad209d
ms.service: multiple
ms.workload: multiple
ms.tgt_pltfrm: vm-multiple
ms.devlang: na
ms.topic: article
ms.date: 10/04/2016
ms.author: rasquill
"\"/": 
ms.openlocfilehash: 42682c00c8dea78b2c624e640379716d1d4d7a2d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-in-tooazure-from-hello-azure-cli"></a><span data-ttu-id="073a9-103">Faça logon no tooAzure de saudação CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="073a9-103">Log in tooAzure from hello Azure CLI</span></span>
<span data-ttu-id="073a9-104">Olá CLI do Azure é um conjunto de comandos de software livre, multiplataforma para trabalhar com recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="073a9-104">hello Azure CLI is a set of open-source, cross-platform commands for working with Azure resources.</span></span> <span data-ttu-id="073a9-105">Este artigo descreve Olá diferentes maneiras tooprovide tooyour da CLI do Azure seu Olá conta do Azure credenciais tooconnect assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="073a9-105">This article describes hello different ways tooprovide your Azure account credentials tooconnect hello Azure CLI tooyour Azure subscription:</span></span>

* <span data-ttu-id="073a9-106">Executar Olá `azure login` CLI tooauthenticate de comando por meio do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="073a9-106">Run hello `azure login` CLI command tooauthenticate through Azure Active Directory.</span></span> <span data-ttu-id="073a9-107">Isso proporciona método acessar comandos tooCLI no [comando modos](#cli-command-modes).</span><span class="sxs-lookup"><span data-stu-id="073a9-107">This method gives you access tooCLI commands in both [command modes](#cli-command-modes).</span></span> <span data-ttu-id="073a9-108">Quando você executa o comando Olá sem opções adicionais, `azure login` solicitará que você toocontinue logon interativamente por meio de um portal da web.</span><span class="sxs-lookup"><span data-stu-id="073a9-108">When you run hello command without additional options, `azure login` prompts you toocontinue logging in interactively through a web portal.</span></span> <span data-ttu-id="073a9-109">Para mais `azure login` opções de comando, consulte os cenários de saudação neste artigo ou tipo `azure login --help`.</span><span class="sxs-lookup"><span data-stu-id="073a9-109">For additional `azure login` command options, see hello scenarios in this article, or type `azure login --help`.</span></span>
* <span data-ttu-id="073a9-110">Se você precisar somente comandos da CLI toouse gerenciamento de serviços do Azure modo (não recomendados para implantações mais novas), você pode baixar e instalar um arquivo de configurações de publicação no seu computador.</span><span class="sxs-lookup"><span data-stu-id="073a9-110">If you only need toouse Azure Service Management mode CLI commands (not recommended for most new deployments), you can download and install a publish settings file on your computer.</span></span>

<span data-ttu-id="073a9-111">Se você ainda não instalou Olá CLI, consulte [instalação Olá CLI do Azure](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="073a9-111">If you haven't already installed hello CLI, see [Install hello Azure CLI](cli-install-nodejs.md).</span></span> <span data-ttu-id="073a9-112">Se você não tiver uma assinatura do Azure, poderá criar uma [conta gratuita](http://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="073a9-112">If you don't have an Azure subscription, you can create a [free account](http://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="073a9-113">Para obter informações sobre identidades de outra conta e sobre as assinaturas do Azure, confira [Como as assinaturas do Azure como são associadas ao Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="073a9-113">For background about different account identities and Azure subscriptions, see [How Azure subscriptions are associated with Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <a name="scenario-1-azure-login-with-interactive-login"></a><span data-ttu-id="073a9-114">Cenário 1: logon do azure com logon interativo</span><span class="sxs-lookup"><span data-stu-id="073a9-114">Scenario 1: azure login with interactive login</span></span>
<span data-ttu-id="073a9-115">Certas contas, Olá CLI requer toorun `azure login` e, em seguida, continuar o processo de logon de saudação com um navegador da web por meio de um portal da web, um processo chamado *logon interativo*.</span><span class="sxs-lookup"><span data-stu-id="073a9-115">With certain accounts, hello CLI requires you toorun `azure login` and then continue hello login process with a web browser through a web portal, a process called *interactive login*.</span></span> <span data-ttu-id="073a9-116">Uma razão comum é quando você tem uma conta corporativa ou escolar (também chamado de um *conta organizacional*) que é configurada toorequire a autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="073a9-116">A common reason is when you have a work or school account (also called an *organizational account*) that is set up toorequire multifactor authentication.</span></span> <span data-ttu-id="073a9-117">Use também o logon interativo com sua conta da Microsoft, quando você deseja toouse comandos de modo de Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="073a9-117">Also use interactive login with your Microsoft account, when you want toouse Resource Manager mode commands.</span></span>

<span data-ttu-id="073a9-118">Logon interativo é fácil: tipo `azure login` – sem opções – conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="073a9-118">Interactive login is easy: type `azure login` -- without any options -- as shown in hello following example:</span></span>

```
azure login
```                                                                                             

<span data-ttu-id="073a9-119">saída de Hello será algo parecido com hello seguinte:</span><span class="sxs-lookup"><span data-stu-id="073a9-119">hello output appears something like hello following:</span></span>

```         
info:    Executing command login
info:    toosign in, use a web browser tooopen hello page http://aka.ms/devicelogin. Enter hello code XXXXXXXXX tooauthenticate.
```
<span data-ttu-id="073a9-120">Copiar código Olá oferecido tooyou na saída do comando hello e abrir um navegador toohttp://aka.ms/devicelogin ou outra página, se especificado.</span><span class="sxs-lookup"><span data-stu-id="073a9-120">Copy hello code offered tooyou in hello command output, and open a browser toohttp://aka.ms/devicelogin, or other page if specified.</span></span> <span data-ttu-id="073a9-121">(Você pode abrir um navegador em Olá mesmo computador, ou em outro computador ou dispositivo.) Insira o código de saudação e, em seguida, você tooenter solicitadas Olá username e password para identidade Olá deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="073a9-121">(You can open a browser on hello same computer, or on a different computer or device.) Enter hello code, and then you are prompted tooenter hello username and password for hello identity you want toouse.</span></span> <span data-ttu-id="073a9-122">Quando esse processo for concluído, o shell de comando Olá conclui o logon de saudação.</span><span class="sxs-lookup"><span data-stu-id="073a9-122">When that process completes, hello command shell completes hello login.</span></span> <span data-ttu-id="073a9-123">Ele poderia ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="073a9-123">It might look something like:</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> <span data-ttu-id="073a9-124">Com o logon interativo, a autenticação e a autorização são executadas com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="073a9-124">With interactive login, authentication and authorization are performed using Azure Active Directory.</span></span> <span data-ttu-id="073a9-125">Se você usar uma identidade de conta da Microsoft, o processo de logon Olá acessa seu domínio do Active Directory do Azure padrão.</span><span class="sxs-lookup"><span data-stu-id="073a9-125">If you use a Microsoft account identity, hello login process accesses your Azure Active Directory default domain.</span></span> <span data-ttu-id="073a9-126">(Se você se inscreveu para obter uma conta gratuita do Azure, o Azure Active Directory criou um domínio padrão para a sua conta).</span><span class="sxs-lookup"><span data-stu-id="073a9-126">(If you signed up for a free Azure account, Azure Active Directory automatically created a default domain for your account.)</span></span>
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a><span data-ttu-id="073a9-127">Cenário 2: logon do Azure com um nome de usuário e senha</span><span class="sxs-lookup"><span data-stu-id="073a9-127">Scenario 2: azure login with a username and password</span></span>
<span data-ttu-id="073a9-128">Saudação de uso `azure login` com nome de usuário da saudação (`-u`) tooauthenticate parâmetro quando você quiser toouse um trabalho ou escola de conta que não exija a autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="073a9-128">Use hello `azure login` command with hello username (`-u`) parameter tooauthenticate when you want toouse a work or school account that doesn't require multifactor authentication.</span></span> <span data-ttu-id="073a9-129">Você será solicitado na linha de comando Olá senha hello (ou, opcionalmente, você pode passar senha hello como um parâmetro adicional do hello `azure login` comando).</span><span class="sxs-lookup"><span data-stu-id="073a9-129">You are prompted at hello command line for hello password (or you can optionally pass hello password as an additional parameter of hello `azure login` command).</span></span> <span data-ttu-id="073a9-130">Olá, exemplo a seguir passa Olá nome de usuário de uma conta organizacional:</span><span class="sxs-lookup"><span data-stu-id="073a9-130">hello following example passes hello username of an organizational account:</span></span>

    azure login -u myUserName@contoso.onmicrosoft.com

<span data-ttu-id="073a9-131">Você solicitado tooenter sua senha:</span><span class="sxs-lookup"><span data-stu-id="073a9-131">You are then prompted tooenter your password:</span></span>

    info:    Executing command login
    Password: *********

<span data-ttu-id="073a9-132">conclui o processo de logon Hello.</span><span class="sxs-lookup"><span data-stu-id="073a9-132">hello login process then completes.</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

<span data-ttu-id="073a9-133">Se esse for o primeiro log de tempo com essas credenciais, você deverá tooverify que você deseja toocache um token de autenticação.</span><span class="sxs-lookup"><span data-stu-id="073a9-133">If this is your first time logging in with these credentials, you are asked tooverify that you wish toocache an authentication token.</span></span> <span data-ttu-id="073a9-134">Esse aviso também ocorre se você tiver usado a saudação `azure logout` comando (descrito posteriormente no artigo Olá).</span><span class="sxs-lookup"><span data-stu-id="073a9-134">This prompt also occurs if you previously used hello `azure logout` command (described later in hello article).</span></span> <span data-ttu-id="073a9-135">toobypass esse prompt para cenários de automação, execute `azure login` com hello `-q` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="073a9-135">toobypass this prompt for automation scenarios, run `azure login` with hello `-q` parameter.</span></span>

## <a name="scenario-3-azure-login-with-a-service-principal"></a><span data-ttu-id="073a9-136">Cenário 3: logon do Azure com uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="073a9-136">Scenario 3: azure login with a service principal</span></span>
<span data-ttu-id="073a9-137">Se você criar uma entidade de serviço para um aplicativo do Active Directory e entidade de serviço Olá tem permissões em sua assinatura, você pode usar o hello `azure login` entidade de serviço do comando tooauthenticate hello.</span><span class="sxs-lookup"><span data-stu-id="073a9-137">If you create a service principal for an Active Directory application, and hello service principal has permissions on your subscription, you can use hello `azure login` command tooauthenticate hello service principal.</span></span> <span data-ttu-id="073a9-138">Dependendo do cenário, você pode fornecer credenciais de saudação da entidade de serviço hello como parâmetros explícitos de saudação `azure login` comando.</span><span class="sxs-lookup"><span data-stu-id="073a9-138">Depending on your scenario, you could provide hello credentials of hello service principal as explicit parameters of hello `azure login` command.</span></span> <span data-ttu-id="073a9-139">Por exemplo, hello comando a seguir passa nome principal do serviço hello e ID de locatário do Active Directory:</span><span class="sxs-lookup"><span data-stu-id="073a9-139">For example, hello following command passes hello service principal name and Active Directory tenant ID:</span></span>

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

<span data-ttu-id="073a9-140">Você forem solicitada tooprovide Olá senha.</span><span class="sxs-lookup"><span data-stu-id="073a9-140">You are then prompted tooprovide hello password.</span></span> <span data-ttu-id="073a9-141">Você também pode fornecer credenciais de saudação por meio de um código de script ou aplicativo CLI ou usar uma entidade de serviço do certificado tooauthenticate Olá não interativamente para cenários de automação.</span><span class="sxs-lookup"><span data-stu-id="073a9-141">You can also provide hello credentials through a CLI script or application code, or use a certificate tooauthenticate hello service principal non-interactively for automation scenarios.</span></span> <span data-ttu-id="073a9-142">Para obter detalhes e exemplos, confira [Autenticando uma entidade de serviço com o Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="073a9-142">For details and examples, see [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span></span>

## <a name="scenario-4-use-a-publish-settings-file"></a><span data-ttu-id="073a9-143">Cenário 4: usar um arquivo de configurações de publicação</span><span class="sxs-lookup"><span data-stu-id="073a9-143">Scenario 4: Use a publish settings file</span></span>
<span data-ttu-id="073a9-144">Se você precisar somente comandos da CLI de modo toouse Olá gerenciamento de serviços do Azure (por exemplo, toodeploy VMs do Azure no modelo de implantação clássico Olá), você pode se conectar usando um arquivo de configurações de publicação.</span><span class="sxs-lookup"><span data-stu-id="073a9-144">If you only need toouse hello Azure Service Management mode CLI commands (for example, toodeploy Azure VMs in hello classic deployment model), you can connect using a publish settings file.</span></span> <span data-ttu-id="073a9-145">Este método instala um certificado no computador local que permite que você tooperform tarefas de gerenciamento para como assinatura hello e certificado Olá são válidos.</span><span class="sxs-lookup"><span data-stu-id="073a9-145">This method installs a certificate on your local computer that allows you tooperform management tasks for as long as hello subscription and hello certificate are valid.</span></span>

* <span data-ttu-id="073a9-146">**Olá toodownload Publicar arquivo de configurações** para sua conta, certifique-se de que Olá CLI está no modo de gerenciamento de serviços, digitando `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="073a9-146">**toodownload hello publish settings file** for your account, ensure that hello CLI is in Service Management mode by typing `azure config mode asm`.</span></span> <span data-ttu-id="073a9-147">Em seguida, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="073a9-147">Then run hello following command:</span></span>

        azure account download

<span data-ttu-id="073a9-148">Isso abre o navegador padrão e solicita que você toosign em toohello [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="073a9-148">This opens your default browser and prompts you toosign in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="073a9-149">Depois de entrar, um arquivo `.publishsettings` é baixado.</span><span class="sxs-lookup"><span data-stu-id="073a9-149">After you sign in, a `.publishsettings` file downloads.</span></span> <span data-ttu-id="073a9-150">Anote onde esse arquivo está salvo.</span><span class="sxs-lookup"><span data-stu-id="073a9-150">Make note of where this file is saved.</span></span>

> [!NOTE]
> <span data-ttu-id="073a9-151">Se sua conta estiver associada a vários locatários do Active Directory do Azure, você pode ser solicitado tooselect que o Active Directory que você deseja toodownload as configurações de publicação do arquivo para.</span><span class="sxs-lookup"><span data-stu-id="073a9-151">If your account is associated with multiple Azure Active Directory tenants, you may be prompted tooselect which Active Directory you wish toodownload a publish settings file for.</span></span>
>
>

<span data-ttu-id="073a9-152">Uma vez selecionado usando a página de download do hello, ou visitando Olá portal clássico do Azure, hello selecionado do Active Directory torna-se saudação padrão usado pelo portal clássico do hello e página de download.</span><span class="sxs-lookup"><span data-stu-id="073a9-152">Once selected using hello download page, or by visiting hello Azure classic portal, hello selected Active Directory becomes hello default used by hello classic portal and download page.</span></span> <span data-ttu-id="073a9-153">Após o estabelecimento de um padrão, consulte o texto de saudação '**clique aqui a página de seleção de toohello tooreturn**' na parte superior de saudação da página de download de saudação.</span><span class="sxs-lookup"><span data-stu-id="073a9-153">Once a default has been established, you see hello text '**click here tooreturn toohello selection page**' at hello top of hello download page.</span></span> <span data-ttu-id="073a9-154">Use Olá fornecido a página de seleção do link tooreturn toohello.</span><span class="sxs-lookup"><span data-stu-id="073a9-154">Use hello provided link tooreturn toohello selection page.</span></span>

* <span data-ttu-id="073a9-155">**Olá tooimport Publicar arquivo de configurações**, execute hello seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="073a9-155">**tooimport hello publish settings file**, run hello following command:</span></span>

        azure account import <path tooyour .publishsettings file>

> [!IMPORTANT]
> <span data-ttu-id="073a9-156">Depois de importar suas configurações de publicação, você deve excluir Olá `.publishsettings` arquivo.</span><span class="sxs-lookup"><span data-stu-id="073a9-156">After importing your publish settings, you should delete hello `.publishsettings` file.</span></span> <span data-ttu-id="073a9-157">Ele não é exigido pela Olá CLI do Azure e apresenta um risco de segurança que pode ser usado toogain acesso tooyour assinatura.</span><span class="sxs-lookup"><span data-stu-id="073a9-157">It is no longer required by hello Azure CLI and presents a security risk as it could be used toogain access tooyour subscription.</span></span>
>
>

## <a name="cli-command-modes"></a><span data-ttu-id="073a9-158">Modos de comando da CLI</span><span class="sxs-lookup"><span data-stu-id="073a9-158">CLI command modes</span></span>
<span data-ttu-id="073a9-159">Olá CLI do Azure oferece dois modos de comando para trabalhar com recursos do Azure, com vários conjuntos de comandos:</span><span class="sxs-lookup"><span data-stu-id="073a9-159">hello Azure CLI provides two command modes for working with Azure resources, with different command sets:</span></span>

* <span data-ttu-id="073a9-160">**Modo do Gerenciador de recursos** - para trabalhar com recursos do Azure no modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="073a9-160">**Resource Manager mode** - for working with Azure resources in hello Resource Manager deployment model.</span></span> <span data-ttu-id="073a9-161">tooset nesse modo, execute `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="073a9-161">tooset this mode, run `azure config mode arm`.</span></span>
* <span data-ttu-id="073a9-162">**Modo de gerenciamento de serviço** - para trabalhar com recursos do Azure no modelo de implantação clássico hello.</span><span class="sxs-lookup"><span data-stu-id="073a9-162">**Service Management mode** - for working with Azure resources in hello classic deployment model.</span></span> <span data-ttu-id="073a9-163">tooset nesse modo, execute `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="073a9-163">tooset this mode, run `azure config mode asm`.</span></span>

<span data-ttu-id="073a9-164">Quando instalado pela primeira vez, Olá versão atual do hello que CLI está no modo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="073a9-164">When first installed, hello current release of hello CLI is in Resource Manager mode.</span></span>

> [!NOTE]
> <span data-ttu-id="073a9-165">modo do Gerenciador de recursos de saudação e modo de gerenciamento de serviço são mutuamente exclusivos.</span><span class="sxs-lookup"><span data-stu-id="073a9-165">hello Resource Manager mode and Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="073a9-166">Ou seja, os recursos criados no modo não podem ser gerenciados de saudação outro modo.</span><span class="sxs-lookup"><span data-stu-id="073a9-166">That is, resources created in one mode cannot be managed from hello other mode.</span></span>
>
>

## <a name="multiple-subscriptions"></a><span data-ttu-id="073a9-167">Várias assinaturas</span><span class="sxs-lookup"><span data-stu-id="073a9-167">Multiple subscriptions</span></span>
<span data-ttu-id="073a9-168">Se você tiver várias assinaturas do Azure, conectar-se tooAzure concede acesso tooall assinaturas associadas com suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="073a9-168">If you have multiple Azure subscriptions, connecting tooAzure grants access tooall subscriptions associated with your credentials.</span></span> <span data-ttu-id="073a9-169">Uma assinatura é selecionada como padrão hello e usada por Olá CLI do Azure ao executar operações.</span><span class="sxs-lookup"><span data-stu-id="073a9-169">One subscription is selected as hello default, and used by hello Azure CLI when performing operations.</span></span> <span data-ttu-id="073a9-170">Você pode exibir assinaturas hello, incluindo assinatura padrão hello, usando Olá `azure account list` comando.</span><span class="sxs-lookup"><span data-stu-id="073a9-170">You can view hello subscriptions, including hello current default subscription, using hello `azure account list` command.</span></span> <span data-ttu-id="073a9-171">Esse comando retorna a seguir toohello semelhante informações:</span><span class="sxs-lookup"><span data-stu-id="073a9-171">This command returns information similar toohello following:</span></span>

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

<span data-ttu-id="073a9-172">Em Olá anterior da lista, Olá **atual** coluna indica Olá atual padrão assinatura do Azure-sub-1.</span><span class="sxs-lookup"><span data-stu-id="073a9-172">In hello preceding list, hello **Current** column indicates hello current default subscription as Azure-sub-1.</span></span> <span data-ttu-id="073a9-173">assinatura padrão do hello toochange, use Olá `azure account set` de comando e especifique que você deseja que o padrão de saudação toobe de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="073a9-173">toochange hello default subscription, use hello `azure account set` command, and specify hello subscription that you wish toobe hello default.</span></span> <span data-ttu-id="073a9-174">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="073a9-174">For example:</span></span>

    azure account set Azure-sub-2

<span data-ttu-id="073a9-175">Isso altera o saudação padrão assinatura tooAzure-sub-2.</span><span class="sxs-lookup"><span data-stu-id="073a9-175">This changes hello default subscription tooAzure-sub-2.</span></span>

> [!NOTE]
> <span data-ttu-id="073a9-176">Alterando saudação padrão assinatura entra em vigor imediatamente e é uma alteração global; novos comandos de CLI do Azure, se você executá-los de Olá mesma instância de linha de comando ou uma instância diferente, use Olá nova assinatura de padrão.</span><span class="sxs-lookup"><span data-stu-id="073a9-176">Changing hello default subscription takes effect immediately, and is a global change; new Azure CLI commands, whether you run them from hello same command-line instance or a different instance, use hello new default subscription.</span></span>
>
>

<span data-ttu-id="073a9-177">Se você quiser toouse uma assinatura diferente do padrão com hello CLI do Azure, mas não quiser padrão atual do toochange hello, você pode usar o hello `--subscription` opção comando hello e forneça o nome de saudação de assinatura Olá desejar toouse para operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="073a9-177">If you wish toouse a non-default subscription with hello Azure CLI, but don't want toochange hello current default, you can use hello `--subscription` option for hello command and provide hello name of hello subscription you wish toouse for hello operation.</span></span>

<span data-ttu-id="073a9-178">Quando você estiver conectado tooyour assinatura do Azure, começar a usar o hello toowork de comandos de CLI do Azure com recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="073a9-178">Once you are connected tooyour Azure subscription, you can start using hello Azure CLI commands toowork with Azure resources.</span></span>

## <a name="storage-of-cli-settings"></a><span data-ttu-id="073a9-179">Armazenamento de configurações da CLI</span><span class="sxs-lookup"><span data-stu-id="073a9-179">Storage of CLI settings</span></span>
<span data-ttu-id="073a9-180">Se você fazer logon com hello `azure login` comando ou importar configurações de publicação, o perfil CLI e os logs são armazenados em um `.azure` diretório localizado no seu `user` directory.</span><span class="sxs-lookup"><span data-stu-id="073a9-180">Whether you log in with hello `azure login` command or import publish settings, your CLI profile and logs are stored in a `.azure` directory located in your `user` directory.</span></span> <span data-ttu-id="073a9-181">O diretório `user` está protegido pelo seu sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="073a9-181">Your `user` directory is protected by your operating system.</span></span> <span data-ttu-id="073a9-182">No entanto, recomendamos que você execute etapas adicionais tooencrypt seu `user` directory.</span><span class="sxs-lookup"><span data-stu-id="073a9-182">However, we recommend that you take additional steps tooencrypt your `user` directory.</span></span> <span data-ttu-id="073a9-183">Você pode fazer isso no hello maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="073a9-183">You can do so in hello following ways:</span></span>

* <span data-ttu-id="073a9-184">No Windows, modificar propriedades de diretório hello ou usar o BitLocker.</span><span class="sxs-lookup"><span data-stu-id="073a9-184">On Windows, modify hello directory properties or use BitLocker.</span></span>
* <span data-ttu-id="073a9-185">No Mac, ative o FileVault para diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="073a9-185">On Mac, turn on FileVault for hello directory.</span></span>
* <span data-ttu-id="073a9-186">No Ubuntu, use o recurso de diretório de Home criptografado de saudação.</span><span class="sxs-lookup"><span data-stu-id="073a9-186">On Ubuntu, use hello Encrypted Home directory feature.</span></span> <span data-ttu-id="073a9-187">Outras distribuições do Linux oferecem recursos semelhantes.</span><span class="sxs-lookup"><span data-stu-id="073a9-187">Other Linux distributions offer similar features.</span></span>

## <a name="logging-out"></a><span data-ttu-id="073a9-188">Fazendo logout</span><span class="sxs-lookup"><span data-stu-id="073a9-188">Logging out</span></span>
<span data-ttu-id="073a9-189">toolog out Olá use comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="073a9-189">toolog out, use hello following command:</span></span>

    azure logout -u <username>

<span data-ttu-id="073a9-190">Se assinaturas Olá associado conta Olá somente são autenticados com o Active Directory, o logout exclui informações de assinatura de saudação do perfil local hello.</span><span class="sxs-lookup"><span data-stu-id="073a9-190">If hello subscriptions associated with hello account are only authenticated with Active Directory, logging out deletes hello subscription information from hello local profile.</span></span> <span data-ttu-id="073a9-191">No entanto, se um arquivo de configurações de publicação também foi importado para assinaturas de hello, logoff somente informações do perfil local Olá relacionadas à exclusões do Active Directory.</span><span class="sxs-lookup"><span data-stu-id="073a9-191">However, if a publish settings file was also imported for hello subscriptions, logging out only deletes Active Directory related information from hello local profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="073a9-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="073a9-192">Next steps</span></span>
* <span data-ttu-id="073a9-193">toouse comandos de CLI do Azure, consulte [comandos de CLI do Azure no Gerenciador de recursos de modo](virtual-machines/azure-cli-arm-commands.md) e [comandos de CLI do Azure no modo de gerenciamento de serviço](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="073a9-193">toouse Azure CLI commands, see [Azure CLI commands in Resource Manager mode](virtual-machines/azure-cli-arm-commands.md) and [Azure CLI commands in Service Management mode](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>
* <span data-ttu-id="073a9-194">toolearn mais sobre Olá CLI do Azure, baixar o código-fonte, relatar problemas, ou contribuir toohello projeto, visite Olá [repositório GitHub para Olá CLI do Azure](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="073a9-194">toolearn more about hello Azure CLI, download source code, report problems, or contribute toohello project, visit hello [GitHub repository for hello Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="073a9-195">Se você tiver problemas ao usar o hello CLI do Azure ou o Azure, visite Olá [fóruns do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="073a9-195">If you encounter problems using hello Azure CLI, or Azure, visit hello [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>
