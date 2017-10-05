---
title: Fazer logon no Azure a partir da CLI | Microsoft Docs
description: "Conectar-se à assinatura do Azure a partir da CLI (Interface de Linha de Comando) do Azure para Mac, Linux e Windows"
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
ms.openlocfilehash: 31efab60690b54faf7992251fcd01e307c4464f2
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="log-in-to-azure-from-the-azure-cli"></a><span data-ttu-id="8580b-103">Faça logon no Azure no Azure CLI</span><span class="sxs-lookup"><span data-stu-id="8580b-103">Log in to Azure from the Azure CLI</span></span>
<span data-ttu-id="8580b-104">O Azure CLI é um conjunto de comandos de plataforma cruzada de software livre para trabalhar com recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8580b-104">The Azure CLI is a set of open-source, cross-platform commands for working with Azure resources.</span></span> <span data-ttu-id="8580b-105">Este artigo descreve as diferentes maneiras de fornecer as credenciais de conta do Azure para conectar o Azure CLI à sua assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="8580b-105">This article describes the different ways to provide your Azure account credentials to connect the Azure CLI to your Azure subscription:</span></span>

* <span data-ttu-id="8580b-106">Execute o comando CLI `azure login` para autenticar por meio do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8580b-106">Run the `azure login` CLI command to authenticate through Azure Active Directory.</span></span> <span data-ttu-id="8580b-107">Este método fornece acesso a comandos CLI em ambos os [modos de comando](#cli-command-modes).</span><span class="sxs-lookup"><span data-stu-id="8580b-107">This method gives you access to CLI commands in both [command modes](#cli-command-modes).</span></span> <span data-ttu-id="8580b-108">Quando você executa o comando sem opções adicionais, o `azure login` solicitará que você continue efetuando logon interativamente por meio de um portal da Web.</span><span class="sxs-lookup"><span data-stu-id="8580b-108">When you run the command without additional options, `azure login` prompts you to continue logging in interactively through a web portal.</span></span> <span data-ttu-id="8580b-109">Para mais opções de comando do `azure login`, consulte os cenários neste artigo ou digite `azure login --help`.</span><span class="sxs-lookup"><span data-stu-id="8580b-109">For additional `azure login` command options, see the scenarios in this article, or type `azure login --help`.</span></span>
* <span data-ttu-id="8580b-110">Se você precisar usar comandos CLI do modo do gerenciamento de serviços do Azure (não recomendado para a maioria das implantações novas), é possível baixar e instalar um arquivo de configurações de publicação no seu computador.</span><span class="sxs-lookup"><span data-stu-id="8580b-110">If you only need to use Azure Service Management mode CLI commands (not recommended for most new deployments), you can download and install a publish settings file on your computer.</span></span>

<span data-ttu-id="8580b-111">Se você ainda não tiver instalado a CLI, consulte [Instalar a CLI do Azure](cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="8580b-111">If you haven't already installed the CLI, see [Install the Azure CLI](cli-install-nodejs.md).</span></span> <span data-ttu-id="8580b-112">Se você não tiver uma assinatura do Azure, poderá criar uma [conta gratuita](http://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="8580b-112">If you don't have an Azure subscription, you can create a [free account](http://azure.microsoft.com/free/) in just a couple of minutes.</span></span>

<span data-ttu-id="8580b-113">Para obter informações sobre identidades de outra conta e sobre as assinaturas do Azure, confira [Como as assinaturas do Azure como são associadas ao Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="8580b-113">For background about different account identities and Azure subscriptions, see [How Azure subscriptions are associated with Azure Active Directory](active-directory/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <a name="scenario-1-azure-login-with-interactive-login"></a><span data-ttu-id="8580b-114">Cenário 1: logon do azure com logon interativo</span><span class="sxs-lookup"><span data-stu-id="8580b-114">Scenario 1: azure login with interactive login</span></span>
<span data-ttu-id="8580b-115">Com certas contas, o CLI exige que você execute `azure login` e, em seguida, continue o processo de logon com um navegador da web por meio de um portal da web, um processo chamado *logon interativo*.</span><span class="sxs-lookup"><span data-stu-id="8580b-115">With certain accounts, the CLI requires you to run `azure login` and then continue the login process with a web browser through a web portal, a process called *interactive login*.</span></span> <span data-ttu-id="8580b-116">Uma razão comum é quando você tem uma conta corporativa ou escolar (também chamada de uma *conta organizacional*) que é configurada para exigir autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="8580b-116">A common reason is when you have a work or school account (also called an *organizational account*) that is set up to require multifactor authentication.</span></span> <span data-ttu-id="8580b-117">Use também o logon interativo com sua conta da Microsoft quando desejar usar comandos do modo de Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="8580b-117">Also use interactive login with your Microsoft account, when you want to use Resource Manager mode commands.</span></span>

<span data-ttu-id="8580b-118">O logon interativo é fácil: digite `azure login` – sem opções – conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="8580b-118">Interactive login is easy: type `azure login` -- without any options -- as shown in the following example:</span></span>

```
azure login
```                                                                                             

<span data-ttu-id="8580b-119">A saída deve ter uma aparência semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="8580b-119">The output appears something like the following:</span></span>

```         
info:    Executing command login
info:    To sign in, use a web browser to open the page http://aka.ms/devicelogin. Enter the code XXXXXXXXX to authenticate.
```
<span data-ttu-id="8580b-120">Copie o código oferecido na saída do comando e abra em um navegador a página http://aka.ms/devicelogin ou outra página se especificado.</span><span class="sxs-lookup"><span data-stu-id="8580b-120">Copy the code offered to you in the command output, and open a browser to http://aka.ms/devicelogin, or other page if specified.</span></span> <span data-ttu-id="8580b-121">(Você pode abrir um navegador no mesmo computador ou em outro computador ou dispositivo). Digite o código; em seguida, você será solicitado a inserir o nome de usuário e a senha para a identidade que deseja usar.</span><span class="sxs-lookup"><span data-stu-id="8580b-121">(You can open a browser on the same computer, or on a different computer or device.) Enter the code, and then you are prompted to enter the username and password for the identity you want to use.</span></span> <span data-ttu-id="8580b-122">Quando o processo for concluído, o shell de comando concluirá o logon.</span><span class="sxs-lookup"><span data-stu-id="8580b-122">When that process completes, the command shell completes the login.</span></span> <span data-ttu-id="8580b-123">Ele poderia ser semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="8580b-123">It might look something like:</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    info:    Added subscription Azure Free Trial
    info:    Setting subscription "Visual Studio Ultimate with MSDN" as default
    +
    info:    login command OK

> [!NOTE]
> <span data-ttu-id="8580b-124">Com o logon interativo, a autenticação e a autorização são executadas com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8580b-124">With interactive login, authentication and authorization are performed using Azure Active Directory.</span></span> <span data-ttu-id="8580b-125">Se você usar uma identidade de conta da Microsoft, o processo de logon acessará seu domínio padrão do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8580b-125">If you use a Microsoft account identity, the login process accesses your Azure Active Directory default domain.</span></span> <span data-ttu-id="8580b-126">(Se você se inscreveu para obter uma conta gratuita do Azure, o Azure Active Directory criou um domínio padrão para a sua conta).</span><span class="sxs-lookup"><span data-stu-id="8580b-126">(If you signed up for a free Azure account, Azure Active Directory automatically created a default domain for your account.)</span></span>
>
>

## <a name="scenario-2-azure-login-with-a-username-and-password"></a><span data-ttu-id="8580b-127">Cenário 2: logon do Azure com um nome de usuário e senha</span><span class="sxs-lookup"><span data-stu-id="8580b-127">Scenario 2: azure login with a username and password</span></span>
<span data-ttu-id="8580b-128">Use o comando `azure login` com o parâmetro (`-u`) de nome de usuário para autenticação quando você deseja usar uma conta corporativa ou de estudante que não exija autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="8580b-128">Use the `azure login` command with the username (`-u`) parameter to authenticate when you want to use a work or school account that doesn't require multifactor authentication.</span></span> <span data-ttu-id="8580b-129">Você é solicitado na linha de comando para a senha (ou, opcionalmente, pode passar a senha como um parâmetro adicional do comando `azure login`).</span><span class="sxs-lookup"><span data-stu-id="8580b-129">You are prompted at the command line for the password (or you can optionally pass the password as an additional parameter of the `azure login` command).</span></span> <span data-ttu-id="8580b-130">O exemplo a seguir passa o nome de usuário de uma conta organizacional:</span><span class="sxs-lookup"><span data-stu-id="8580b-130">The following example passes the username of an organizational account:</span></span>

    azure login -u myUserName@contoso.onmicrosoft.com

<span data-ttu-id="8580b-131">Você será solicitado a inserir sua senha:</span><span class="sxs-lookup"><span data-stu-id="8580b-131">You are then prompted to enter your password:</span></span>

    info:    Executing command login
    Password: *********

<span data-ttu-id="8580b-132">O processo de logon é concluído.</span><span class="sxs-lookup"><span data-stu-id="8580b-132">The login process then completes.</span></span>

    info:    Added subscription Visual Studio Ultimate with MSDN
    +
    info:    login command OK

<span data-ttu-id="8580b-133">Se essa for a primeira vez fazendo logon com essas credenciais, você será solicitado a verificar se deseja armazenar um token de autenticação no cache.</span><span class="sxs-lookup"><span data-stu-id="8580b-133">If this is your first time logging in with these credentials, you are asked to verify that you wish to cache an authentication token.</span></span> <span data-ttu-id="8580b-134">Esse aviso também ocorrerá se você tiver usado anteriormente o comando `azure logout` (descrito mais abaixo no artigo).</span><span class="sxs-lookup"><span data-stu-id="8580b-134">This prompt also occurs if you previously used the `azure logout` command (described later in the article).</span></span> <span data-ttu-id="8580b-135">Para ignorar esse aviso em cenários de automação, execute `azure login` com o parâmetro `-q`.</span><span class="sxs-lookup"><span data-stu-id="8580b-135">To bypass this prompt for automation scenarios, run `azure login` with the `-q` parameter.</span></span>

## <a name="scenario-3-azure-login-with-a-service-principal"></a><span data-ttu-id="8580b-136">Cenário 3: logon do Azure com uma entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="8580b-136">Scenario 3: azure login with a service principal</span></span>
<span data-ttu-id="8580b-137">Se você criar uma entidade de serviço para um aplicativo do Active Directory e a entidade de serviço tiver permissões em sua assinatura, é possível usar o comando `azure login` para autenticar a entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="8580b-137">If you create a service principal for an Active Directory application, and the service principal has permissions on your subscription, you can use the `azure login` command to authenticate the service principal.</span></span> <span data-ttu-id="8580b-138">Dependendo do cenário, você pode fornecer as credenciais da entidade de serviço como parâmetros explícitos do comando `azure login`.</span><span class="sxs-lookup"><span data-stu-id="8580b-138">Depending on your scenario, you could provide the credentials of the service principal as explicit parameters of the `azure login` command.</span></span> <span data-ttu-id="8580b-139">Por exemplo, o comando a seguir passa o nome da entidade do serviço e a ID de locatário do Active Directory:</span><span class="sxs-lookup"><span data-stu-id="8580b-139">For example, the following command passes the service principal name and Active Directory tenant ID:</span></span>

    azure login -u https://www.contoso.org/example --service-principal --tenant myTenantID

<span data-ttu-id="8580b-140">Você será solicitado a inserir sua senha.</span><span class="sxs-lookup"><span data-stu-id="8580b-140">You are then prompted to provide the password.</span></span> <span data-ttu-id="8580b-141">Você também pode fornecer as credenciais por meio de um código de script ou aplicativo CLI ou usar um certificado para autenticar a entidade de serviço de maneira não interativa para cenários de automação.</span><span class="sxs-lookup"><span data-stu-id="8580b-141">You can also provide the credentials through a CLI script or application code, or use a certificate to authenticate the service principal non-interactively for automation scenarios.</span></span> <span data-ttu-id="8580b-142">Para obter detalhes e exemplos, confira [Autenticando uma entidade de serviço com o Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span><span class="sxs-lookup"><span data-stu-id="8580b-142">For details and examples, see [Authenticating a service principal with Azure Resource Manager](resource-group-authenticate-service-principal-cli.md).</span></span>

## <a name="scenario-4-use-a-publish-settings-file"></a><span data-ttu-id="8580b-143">Cenário 4: usar um arquivo de configurações de publicação</span><span class="sxs-lookup"><span data-stu-id="8580b-143">Scenario 4: Use a publish settings file</span></span>
<span data-ttu-id="8580b-144">Se você precisa apenas usar os comandos de CLI do modo Gerenciamento de Serviços do Azure (por exemplo, para implantar VMs do Azure no modelo de implantação clássico), pode se conectar usando um arquivo de configurações de publicação.</span><span class="sxs-lookup"><span data-stu-id="8580b-144">If you only need to use the Azure Service Management mode CLI commands (for example, to deploy Azure VMs in the classic deployment model), you can connect using a publish settings file.</span></span> <span data-ttu-id="8580b-145">Esse método instala um certificado no computador local que permite executar tarefas de gerenciamento durante o tempo em que a assinatura e o certificado forem válidos.</span><span class="sxs-lookup"><span data-stu-id="8580b-145">This method installs a certificate on your local computer that allows you to perform management tasks for as long as the subscription and the certificate are valid.</span></span>

* <span data-ttu-id="8580b-146">**Para baixar o arquivo de configurações de publicação** para sua conta, certifique-se de que o CLI esteja no modo de Gerenciamento de Serviço digitando `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="8580b-146">**To download the publish settings file** for your account, ensure that the CLI is in Service Management mode by typing `azure config mode asm`.</span></span> <span data-ttu-id="8580b-147">Em seguida, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8580b-147">Then run the following command:</span></span>

        azure account download

<span data-ttu-id="8580b-148">Isso abre o navegador padrão e solicita que você entre no [portal clássico do Azure](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="8580b-148">This opens your default browser and prompts you to sign in to the [Azure classic portal](https://manage.windowsazure.com).</span></span> <span data-ttu-id="8580b-149">Depois de entrar, um arquivo `.publishsettings` é baixado.</span><span class="sxs-lookup"><span data-stu-id="8580b-149">After you sign in, a `.publishsettings` file downloads.</span></span> <span data-ttu-id="8580b-150">Anote onde esse arquivo está salvo.</span><span class="sxs-lookup"><span data-stu-id="8580b-150">Make note of where this file is saved.</span></span>

> [!NOTE]
> <span data-ttu-id="8580b-151">Se a conta estiver associada a vários locatários do Active Directory do Azure, você deverá selecionar para qual Active Directory você deseja baixar um arquivo de configurações de publicação.</span><span class="sxs-lookup"><span data-stu-id="8580b-151">If your account is associated with multiple Azure Active Directory tenants, you may be prompted to select which Active Directory you wish to download a publish settings file for.</span></span>
>
>

<span data-ttu-id="8580b-152">Depois de selecionado por meio da página de download ou acessando o Portal Clássico do Azure, o Active Directory escolhido se torna o padrão usado pelo portal clássico e pela página de download.</span><span class="sxs-lookup"><span data-stu-id="8580b-152">Once selected using the download page, or by visiting the Azure classic portal, the selected Active Directory becomes the default used by the classic portal and download page.</span></span> <span data-ttu-id="8580b-153">Depois que um padrão tiver sido estabelecido, você verá o texto `**clique aqui para retornar à página de seleção**` na parte superior da página de download.</span><span class="sxs-lookup"><span data-stu-id="8580b-153">Once a default has been established, you see the text '**click here to return to the selection page**' at the top of the download page.</span></span> <span data-ttu-id="8580b-154">Use o link fornecido para retornar à página de seleção.</span><span class="sxs-lookup"><span data-stu-id="8580b-154">Use the provided link to return to the selection page.</span></span>

* <span data-ttu-id="8580b-155">**Para importar o arquivo de configurações de publicação**, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8580b-155">**To import the publish settings file**, run the following command:</span></span>

        azure account import <path to your .publishsettings file>

> [!IMPORTANT]
> <span data-ttu-id="8580b-156">Depois de importar as suas configurações de publicação, exclua o arquivo `.publishsettings`.</span><span class="sxs-lookup"><span data-stu-id="8580b-156">After importing your publish settings, you should delete the `.publishsettings` file.</span></span> <span data-ttu-id="8580b-157">Ele não é mais exigido pelas CLI do Azure e apresenta um risco de segurança já que pode ser usado para obter acesso à sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="8580b-157">It is no longer required by the Azure CLI and presents a security risk as it could be used to gain access to your subscription.</span></span>
>
>

## <a name="cli-command-modes"></a><span data-ttu-id="8580b-158">Modos de comando da CLI</span><span class="sxs-lookup"><span data-stu-id="8580b-158">CLI command modes</span></span>
<span data-ttu-id="8580b-159">A CLI do Azure fornece dois modos de comando para trabalhar com recursos do Azure, com vários conjuntos de comandos:</span><span class="sxs-lookup"><span data-stu-id="8580b-159">The Azure CLI provides two command modes for working with Azure resources, with different command sets:</span></span>

* <span data-ttu-id="8580b-160">**Modo do Gerenciador de Recursos** – para trabalhar com recursos do Azure no modelo de implantação do Gerenciador de Recursos.</span><span class="sxs-lookup"><span data-stu-id="8580b-160">**Resource Manager mode** - for working with Azure resources in the Resource Manager deployment model.</span></span> <span data-ttu-id="8580b-161">Para definir esse modo, execute `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="8580b-161">To set this mode, run `azure config mode arm`.</span></span>
* <span data-ttu-id="8580b-162">**Modo Gerenciamento de Serviços** – para trabalhar com recursos do Azure no modelo de implantação clássico.</span><span class="sxs-lookup"><span data-stu-id="8580b-162">**Service Management mode** - for working with Azure resources in the classic deployment model.</span></span> <span data-ttu-id="8580b-163">Para definir esse modo, execute `azure config mode asm`.</span><span class="sxs-lookup"><span data-stu-id="8580b-163">To set this mode, run `azure config mode asm`.</span></span>

<span data-ttu-id="8580b-164">Quando instalado pela primeira vez, a versão atual do CLI está no modo do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="8580b-164">When first installed, the current release of the CLI is in Resource Manager mode.</span></span>

> [!NOTE]
> <span data-ttu-id="8580b-165">O modo do Gerenciador de Recursos e o modo do Gerenciamento de Serviços são mutuamente excludentes.</span><span class="sxs-lookup"><span data-stu-id="8580b-165">The Resource Manager mode and Service Management mode are mutually exclusive.</span></span> <span data-ttu-id="8580b-166">Ou seja, recursos criados em um modo não podem ser gerenciados no outro modo.</span><span class="sxs-lookup"><span data-stu-id="8580b-166">That is, resources created in one mode cannot be managed from the other mode.</span></span>
>
>

## <a name="multiple-subscriptions"></a><span data-ttu-id="8580b-167">Várias assinaturas</span><span class="sxs-lookup"><span data-stu-id="8580b-167">Multiple subscriptions</span></span>
<span data-ttu-id="8580b-168">Se você tiver várias assinaturas do Azure, a conexão ao Azure dará acesso a todas as assinaturas associadas às suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="8580b-168">If you have multiple Azure subscriptions, connecting to Azure grants access to all subscriptions associated with your credentials.</span></span> <span data-ttu-id="8580b-169">Uma assinatura é selecionada como padrão e usada pela CLI do Azure durante a realização das operações.</span><span class="sxs-lookup"><span data-stu-id="8580b-169">One subscription is selected as the default, and used by the Azure CLI when performing operations.</span></span> <span data-ttu-id="8580b-170">Você pode exibir as assinaturas, incluindo a assinatura padrão atual, usando o comando `azure account list`.</span><span class="sxs-lookup"><span data-stu-id="8580b-170">You can view the subscriptions, including the current default subscription, using the `azure account list` command.</span></span> <span data-ttu-id="8580b-171">Esse comando retorna informações semelhantes às seguintes:</span><span class="sxs-lookup"><span data-stu-id="8580b-171">This command returns information similar to the following:</span></span>

    info:    Executing command account list
    data:    Name              Id                                    Current
    data:    ----------------  ------------------------------------  -------
    data:    Azure-sub-1       ####################################  true
    data:    Azure-sub-2       ####################################  false

<span data-ttu-id="8580b-172">Na lista anterior, a coluna **Atual** indica a assinatura padrão atual como Azure-sub-1.</span><span class="sxs-lookup"><span data-stu-id="8580b-172">In the preceding list, the **Current** column indicates the current default subscription as Azure-sub-1.</span></span> <span data-ttu-id="8580b-173">Para alterar a assinatura padrão, use o comando `azure account set` e especifique a assinatura que você deseja que seja a padrão.</span><span class="sxs-lookup"><span data-stu-id="8580b-173">To change the default subscription, use the `azure account set` command, and specify the subscription that you wish to be the default.</span></span> <span data-ttu-id="8580b-174">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8580b-174">For example:</span></span>

    azure account set Azure-sub-2

<span data-ttu-id="8580b-175">Isso muda a assinatura padrão para o Azure sub-2.</span><span class="sxs-lookup"><span data-stu-id="8580b-175">This changes the default subscription to Azure-sub-2.</span></span>

> [!NOTE]
> <span data-ttu-id="8580b-176">A alteração da assinatura padrão entra em vigor imediatamente e é uma alteração global. Novos comandos do Azure CLI, executados na mesma instância de linha de comando ou em outra instância, usarão a nova assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="8580b-176">Changing the default subscription takes effect immediately, and is a global change; new Azure CLI commands, whether you run them from the same command-line instance or a different instance, use the new default subscription.</span></span>
>
>

<span data-ttu-id="8580b-177">Se quiser usar uma assinatura não padrão com a CLI do Azure, mas não quiser alterar o padrão atual, você poderá usar a opção `--subscription` do comando e fornecer o nome da assinatura que deseja usar na operação.</span><span class="sxs-lookup"><span data-stu-id="8580b-177">If you wish to use a non-default subscription with the Azure CLI, but don't want to change the current default, you can use the `--subscription` option for the command and provide the name of the subscription you wish to use for the operation.</span></span>

<span data-ttu-id="8580b-178">Uma vez conectado à sua assinatura do Azure, você pode começar a usar os comandos da CLI do Azure para trabalhar com recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8580b-178">Once you are connected to your Azure subscription, you can start using the Azure CLI commands to work with Azure resources.</span></span>

## <a name="storage-of-cli-settings"></a><span data-ttu-id="8580b-179">Armazenamento de configurações da CLI</span><span class="sxs-lookup"><span data-stu-id="8580b-179">Storage of CLI settings</span></span>
<span data-ttu-id="8580b-180">Quer você faça logon com o comando `azure login` ou importe as configurações de publicação, os seus logs e perfil CLI serão armazenados em um diretório `.azure` localizado no seu diretório `user`.</span><span class="sxs-lookup"><span data-stu-id="8580b-180">Whether you log in with the `azure login` command or import publish settings, your CLI profile and logs are stored in a `.azure` directory located in your `user` directory.</span></span> <span data-ttu-id="8580b-181">O diretório `user` está protegido pelo seu sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="8580b-181">Your `user` directory is protected by your operating system.</span></span> <span data-ttu-id="8580b-182">No entanto, é recomendável que você execute etapas adicionais para criptografar seu diretório `user` .</span><span class="sxs-lookup"><span data-stu-id="8580b-182">However, we recommend that you take additional steps to encrypt your `user` directory.</span></span> <span data-ttu-id="8580b-183">Você pode fazer isso das seguintes maneiras:</span><span class="sxs-lookup"><span data-stu-id="8580b-183">You can do so in the following ways:</span></span>

* <span data-ttu-id="8580b-184">No Windows, modifique as propriedades do diretório ou use o BitLocker.</span><span class="sxs-lookup"><span data-stu-id="8580b-184">On Windows, modify the directory properties or use BitLocker.</span></span>
* <span data-ttu-id="8580b-185">No Mac, ative o FileVault para o diretório.</span><span class="sxs-lookup"><span data-stu-id="8580b-185">On Mac, turn on FileVault for the directory.</span></span>
* <span data-ttu-id="8580b-186">No Ubuntu, use o recurso de diretório inicial criptografado.</span><span class="sxs-lookup"><span data-stu-id="8580b-186">On Ubuntu, use the Encrypted Home directory feature.</span></span> <span data-ttu-id="8580b-187">Outras distribuições do Linux oferecem recursos semelhantes.</span><span class="sxs-lookup"><span data-stu-id="8580b-187">Other Linux distributions offer similar features.</span></span>

## <a name="logging-out"></a><span data-ttu-id="8580b-188">Fazendo logout</span><span class="sxs-lookup"><span data-stu-id="8580b-188">Logging out</span></span>
<span data-ttu-id="8580b-189">Para fazer logoff, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="8580b-189">To log out, use the following command:</span></span>

    azure logout -u <username>

<span data-ttu-id="8580b-190">Se as assinaturas associadas à conta forem autenticadas apenas com o Active Directory, o logoff excluirá as informações da assinatura do perfil local.</span><span class="sxs-lookup"><span data-stu-id="8580b-190">If the subscriptions associated with the account are only authenticated with Active Directory, logging out deletes the subscription information from the local profile.</span></span> <span data-ttu-id="8580b-191">No entanto, se um arquivo de configurações de publicação também tiver sido importado para as assinaturas, o logoff excluirá apenas as informações relacionadas ao Active Directory do perfil local.</span><span class="sxs-lookup"><span data-stu-id="8580b-191">However, if a publish settings file was also imported for the subscriptions, logging out only deletes Active Directory related information from the local profile.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8580b-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8580b-192">Next steps</span></span>
* <span data-ttu-id="8580b-193">Para usar os comandos da CLI do Azure, confira [Comandos da CLI do Azure no modo do Gerenciador de Recursos](virtual-machines/azure-cli-arm-commands.md) e [comandos da CLI do Azure no modo Gerenciamento de Serviços do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="8580b-193">To use Azure CLI commands, see [Azure CLI commands in Resource Manager mode](virtual-machines/azure-cli-arm-commands.md) and [Azure CLI commands in Service Management mode](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2).</span></span>
* <span data-ttu-id="8580b-194">Para saber mais sobre a CLI do Azure, baixar o código-fonte, relatar problemas ou colaborar com o projeto, visite o [Repositório GitHub para a CLI do Azure](https://github.com/azure/azure-xplat-cli).</span><span class="sxs-lookup"><span data-stu-id="8580b-194">To learn more about the Azure CLI, download source code, report problems, or contribute to the project, visit the [GitHub repository for the Azure CLI](https://github.com/azure/azure-xplat-cli).</span></span>
* <span data-ttu-id="8580b-195">Se tiver problemas ao usar a CLI do Azure ou o Azure, visite os [Fóruns do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span><span class="sxs-lookup"><span data-stu-id="8580b-195">If you encounter problems using the Azure CLI, or Azure, visit the [Azure Forums](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurescripting).</span></span>
