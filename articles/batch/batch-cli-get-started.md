---
title: "Introdução à CLI do Azure do Lote | Microsoft Docs"
description: "Obtenha uma introdução rápida dos comandos do Lote na CLI do Azure para gerenciar recursos de serviço do Lote do Azure"
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 07/20/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9bee0344ba70c50cda36a87ea617906283040ff9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a><span data-ttu-id="69b9d-103">Gerenciar recursos do Lote com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="69b9d-103">Manage Batch resources with Azure CLI</span></span>

<span data-ttu-id="69b9d-104">A CLI 2.0 do Azure é a nova experiência de linha de comando do Azure para gerenciar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="69b9d-104">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="69b9d-105">Ela pode ser usada em Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="69b9d-105">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="69b9d-106">A CLI do Azure 2.0 é otimizada para gerenciar e administrar os recursos do Azure na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="69b9d-106">Azure CLI 2.0 is optimized for managing and administering Azure resources from the command line.</span></span> <span data-ttu-id="69b9d-107">Você pode usar a CLI do Azure para gerenciar suas contas do Lote do Azure e para gerenciar recursos como grupos, trabalhos e tarefas.</span><span class="sxs-lookup"><span data-stu-id="69b9d-107">You can use the Azure CLI to manage your Azure Batch accounts and to manage resources such as pools, jobs, and tasks.</span></span> <span data-ttu-id="69b9d-108">Com a CLI do Azure, você pode criar scripts para diversas tarefas que você executa com as APIs do Lote, com o Portal do Azure e com cmdlets de PowerShell do Lote.</span><span class="sxs-lookup"><span data-stu-id="69b9d-108">With the Azure CLI, you can script many of the same tasks you carry out with the Batch APIs, Azure portal, and Batch PowerShell cmdlets.</span></span>

<span data-ttu-id="69b9d-109">Este artigo fornece uma visão geral do uso da [CLI do Azure versão 2.0](https://docs.microsoft.com/cli/azure/overview) com o Lote.</span><span class="sxs-lookup"><span data-stu-id="69b9d-109">This article provides an overview of using [Azure CLI version 2.0](https://docs.microsoft.com/cli/azure/overview) with Batch.</span></span> <span data-ttu-id="69b9d-110">Consulte [Introdução ao Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) para uma visão geral de como usar a CLI com o Azure.</span><span class="sxs-lookup"><span data-stu-id="69b9d-110">See [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) for an overview of using the CLI with Azure.</span></span>

<span data-ttu-id="69b9d-111">A Microsoft recomenda usar a versão mais recente da CLI do Azure, versão 2.0.</span><span class="sxs-lookup"><span data-stu-id="69b9d-111">Microsoft recommends using the latest version of the Azure CLI, version 2.0.</span></span> <span data-ttu-id="69b9d-112">Para saber mais sobre a versão 2.0, consulte [CLI do Azure 2.0 agora disponível](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span><span class="sxs-lookup"><span data-stu-id="69b9d-112">For more information about version 2.0, see [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span></span>

## <a name="set-up-the-azure-cli"></a><span data-ttu-id="69b9d-113">Configurar a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="69b9d-113">Set up the Azure CLI</span></span>

<span data-ttu-id="69b9d-114">Para instalar a CLI do Azure, siga as etapas descritas em [Instalar a CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="69b9d-114">To install the Azure CLI, follow the steps outlined in [Install the Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span></span>

> [!TIP]
> <span data-ttu-id="69b9d-115">Recomendamos que você atualize frequentemente sua instalação da CLI do Azure para aproveitar as atualizações e aprimoramentos do serviço.</span><span class="sxs-lookup"><span data-stu-id="69b9d-115">We recommend that you update your Azure CLI installation frequently to take advantage of service updates and enhancements.</span></span>
> 
> 

## <a name="command-help"></a><span data-ttu-id="69b9d-116">Ajuda de comando</span><span class="sxs-lookup"><span data-stu-id="69b9d-116">Command help</span></span>

<span data-ttu-id="69b9d-117">Você pode exibir um texto de ajuda para todo comando na CLI do Azure acrescentando `-h` ao comando.</span><span class="sxs-lookup"><span data-stu-id="69b9d-117">You can display help text for every command in the Azure CLI by appending `-h` to the command.</span></span> <span data-ttu-id="69b9d-118">Omita as outras opções.</span><span class="sxs-lookup"><span data-stu-id="69b9d-118">Omit any other options.</span></span> <span data-ttu-id="69b9d-119">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="69b9d-119">For example:</span></span>

* <span data-ttu-id="69b9d-120">Para obter ajuda sobre o comando `az`, insira: `az -h`</span><span class="sxs-lookup"><span data-stu-id="69b9d-120">To get help for the `az` command, enter: `az -h`</span></span>
* <span data-ttu-id="69b9d-121">Para obter uma lista de todos os comandos do Lote na CLI, use: `az batch -h`</span><span class="sxs-lookup"><span data-stu-id="69b9d-121">To get a list of all Batch commands in the CLI, use: `az batch -h`</span></span>
* <span data-ttu-id="69b9d-122">Para obter ajuda com a criação de uma conta do Lote, insira: `az batch account create -h`</span><span class="sxs-lookup"><span data-stu-id="69b9d-122">To get help on creating a Batch account, enter: `az batch account create -h`</span></span>

<span data-ttu-id="69b9d-123">Em caso de dúvida, use a opção de linha de comando `-h` para obter ajuda sobre qualquer comando da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="69b9d-123">When in doubt, use the `-h` command-line option to get help on any Azure CLI command.</span></span>

> [!NOTE]
> <span data-ttu-id="69b9d-124">Versões anteriores da CLI do Azure usavam `azure` para preceder um comando CLI.</span><span class="sxs-lookup"><span data-stu-id="69b9d-124">Earlier versions of the Azure CLI used `azure` to preface a CLI command.</span></span> <span data-ttu-id="69b9d-125">Na versão 2.0, todos os comandos agora são precedidos por `az`.</span><span class="sxs-lookup"><span data-stu-id="69b9d-125">In version 2.0, all commands are now prefaced with `az`.</span></span> <span data-ttu-id="69b9d-126">Não deixe de atualizar os scripts para usar a nova sintaxe com a versão 2.0.</span><span class="sxs-lookup"><span data-stu-id="69b9d-126">Be sure to update your scripts to use the new syntax with version 2.0.</span></span>
>
>  

<span data-ttu-id="69b9d-127">Além disso, consulte a documentação de referência da CLI do Azure para obter detalhes sobre [comandos da CLI do Azure para o Lote](https://docs.microsoft.com/cli/azure/batch).</span><span class="sxs-lookup"><span data-stu-id="69b9d-127">Additionally, refer to the Azure CLI reference documentation for details about [Azure CLI commands for Batch](https://docs.microsoft.com/cli/azure/batch).</span></span> 

## <a name="log-in-and-authenticate"></a><span data-ttu-id="69b9d-128">Fazer logon e autenticar</span><span class="sxs-lookup"><span data-stu-id="69b9d-128">Log in and authenticate</span></span>

<span data-ttu-id="69b9d-129">Para usar a CLI do Azure com o Lote, você precisa fazer logon e autenticar.</span><span class="sxs-lookup"><span data-stu-id="69b9d-129">To use the Azure CLI with Batch, you need to log in and authenticate.</span></span> <span data-ttu-id="69b9d-130">Siga estas duas etapas simples:</span><span class="sxs-lookup"><span data-stu-id="69b9d-130">There are two simple steps to follow:</span></span>

1. <span data-ttu-id="69b9d-131">**Faça logon no Azure.**</span><span class="sxs-lookup"><span data-stu-id="69b9d-131">**Log into Azure.**</span></span> <span data-ttu-id="69b9d-132">O logon no Azure fornece acesso a comandos do Azure Resource Manager, incluindo comandos do [serviço de gerenciamento em lotes](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="69b9d-132">Logging into Azure gives you access to Azure Resource Manager commands, including [Batch Management service](batch-management-dotnet.md) commands.</span></span>  
2. <span data-ttu-id="69b9d-133">**Faça logon em sua conta do Lote.**</span><span class="sxs-lookup"><span data-stu-id="69b9d-133">**Log into your Batch account.**</span></span> <span data-ttu-id="69b9d-134">O logon em sua conta do Lote fornece acesso a comandos do serviço Lote.</span><span class="sxs-lookup"><span data-stu-id="69b9d-134">Logging into your Batch account gives you access to Batch service commands.</span></span>   

### <a name="log-in-to-azure"></a><span data-ttu-id="69b9d-135">Fazer logon no Azure</span><span class="sxs-lookup"><span data-stu-id="69b9d-135">Log in to Azure</span></span>

<span data-ttu-id="69b9d-136">Existem algumas maneiras diferentes de fazer logon no Azure, descritas detalhadamente em [Entrar com a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span><span class="sxs-lookup"><span data-stu-id="69b9d-136">There are a few different ways to log into Azure, described in detail in [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span></span>

1. <span data-ttu-id="69b9d-137">[Fazer logon interativamente](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span><span class="sxs-lookup"><span data-stu-id="69b9d-137">[Log in interactively](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span></span> <span data-ttu-id="69b9d-138">Faça logon interativamente quando você estiver executando comandos da CLI do Azure na linha de comando.</span><span class="sxs-lookup"><span data-stu-id="69b9d-138">Log in interactively when you are running Azure CLI commands yourself from the command line.</span></span>
2. <span data-ttu-id="69b9d-139">[Fazer logon com uma entidade de serviço](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="69b9d-139">[Log in with a service principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span></span> <span data-ttu-id="69b9d-140">Faça logon com uma entidade de serviço quando você estiver executando comandos da CLI do Azure de um script ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="69b9d-140">Log in with a service principal when you are running Azure CLI commands from a script or an application.</span></span>

<span data-ttu-id="69b9d-141">Para os fins deste artigo, vamos mostrar como entrar no Azure interativamente.</span><span class="sxs-lookup"><span data-stu-id="69b9d-141">For the purposes of this article, we show how to log into Azure interactively.</span></span> <span data-ttu-id="69b9d-142">Digite [az login](https://docs.microsoft.com/cli/azure/#login) na linha de comando:</span><span class="sxs-lookup"><span data-stu-id="69b9d-142">Type [az login](https://docs.microsoft.com/cli/azure/#login) on the command line:</span></span>

```azurecli
# Log in to Azure and authenticate interactively.
az login
```

<span data-ttu-id="69b9d-143">O comando `az login` retorna um token que você pode usar para autenticar, conforme mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="69b9d-143">The `az login` command returns a token that you can use to authenticate, as shown here.</span></span> <span data-ttu-id="69b9d-144">Siga as instruções fornecidas para abrir uma página da Web e enviar o token do Azure:</span><span class="sxs-lookup"><span data-stu-id="69b9d-144">Follow the instructions provided to open a web page and submit the token to Azure:</span></span>

![Fazer logon no Azure](./media/batch-cli-get-started/az-login.png)

<span data-ttu-id="69b9d-146">Os exemplos listados na seção [Scripts de shell de exemplo](#sample-shell-scripts) também mostra como iniciar a sessão da CLI do Azure entrando no Azure interativamente.</span><span class="sxs-lookup"><span data-stu-id="69b9d-146">The examples listed in the [Sample shell scripts](#sample-shell-scripts) section also show how to start your Azure CLI session by logging into Azure interactively.</span></span> <span data-ttu-id="69b9d-147">Depois de fazer logon, você pode chamar comandos para trabalhar com recursos do gerenciamento em lotes, incluindo contas, chaves, pacotes de aplicativos e cotas do Lote.</span><span class="sxs-lookup"><span data-stu-id="69b9d-147">Once you have logged in, you can call commands to work with Batch Management resources, including Batch accounts, keys, application packages, and quotas.</span></span>  

### <a name="log-in-to-your-batch-account"></a><span data-ttu-id="69b9d-148">Fazer logon sua conta do Lote</span><span class="sxs-lookup"><span data-stu-id="69b9d-148">Log in to your Batch account</span></span>

<span data-ttu-id="69b9d-149">Para usar a CLI do Azure e gerenciar recursos do Lote, como pools, trabalhos e tarefas, você precisará entrar na sua conta do Lote e autenticar.</span><span class="sxs-lookup"><span data-stu-id="69b9d-149">To use the Azure CLI to manage Batch resources, such as pools, jobs, and tasks, you need to log into your Batch account and authenticate.</span></span> <span data-ttu-id="69b9d-150">Para entrar no serviço Lote, use o comando [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login).</span><span class="sxs-lookup"><span data-stu-id="69b9d-150">To log in to the Batch service, use the [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command.</span></span> 

<span data-ttu-id="69b9d-151">Você tem duas opções para autenticação na sua conta do Lote:</span><span class="sxs-lookup"><span data-stu-id="69b9d-151">You have two options for authenticating against your Batch account:</span></span>

- <span data-ttu-id="69b9d-152">**Usando a autenticação do Azure AD (Azure Active Directory)**</span><span class="sxs-lookup"><span data-stu-id="69b9d-152">**By using Azure Active Directory (Azure AD) authentication.**</span></span> 

    <span data-ttu-id="69b9d-153">A autenticação com o Azure AD é o padrão quando você usa a CLI do Azure com o Lote e é recomendada na maioria dos cenários.</span><span class="sxs-lookup"><span data-stu-id="69b9d-153">Authenticating with Azure AD is the default when you use the Azure CLI with Batch, and recommended for most scenarios.</span></span> 
    
    <span data-ttu-id="69b9d-154">Quando você entra no Azure interativamente, conforme descrito na seção anterior, as credenciais são armazenadas em cache para que a CLI do Azure possa entrar na conta do Lote usando as mesmas credenciais.</span><span class="sxs-lookup"><span data-stu-id="69b9d-154">When you log in to Azure interactively, as described in the previous section, your credentials are cached, so the Azure CLI can log you in to your Batch account using those same credentials.</span></span> <span data-ttu-id="69b9d-155">Se você entrar no Azure usando uma entidade de serviço, essas credenciais também serão usadas para entrar na sua conta do Lote.</span><span class="sxs-lookup"><span data-stu-id="69b9d-155">If you log in to Azure using a service principal, those credentials are also used to log in to your Batch account.</span></span>

    <span data-ttu-id="69b9d-156">Uma vantagem do Azure AD é que ele oferece RBAC (controle de acesso baseado em função).</span><span class="sxs-lookup"><span data-stu-id="69b9d-156">An advantage of Azure AD is that it offers role-based access control (RBAC).</span></span> <span data-ttu-id="69b9d-157">Com o RBAC, acesso de um usuário depende de suas funções atribuídas em vez da posse ou não de chaves da conta.</span><span class="sxs-lookup"><span data-stu-id="69b9d-157">With RBAC, a user's access depends on their assigned role, rather than whether or not they possess the account keys.</span></span> <span data-ttu-id="69b9d-158">Em vez de gerenciar chaves de conta, você pode gerenciar funções RBAC e permitir que o Azure AD lide com autenticação e acesso.</span><span class="sxs-lookup"><span data-stu-id="69b9d-158">Instead of managing account keys, you can manage RBAC roles, and let Azure AD handle access and authentication.</span></span>  

    <span data-ttu-id="69b9d-159">A autenticação com o Azure AD é necessária se você criou sua conta do Lote do Azure com seu modo de alocação de pool definido como 'Assinatura de usuário'.</span><span class="sxs-lookup"><span data-stu-id="69b9d-159">Authenticating with Azure AD is required if you created your Azure Batch account with its pool allocation mode set to 'User Subscription'.</span></span> 

    <span data-ttu-id="69b9d-160">Para entrar na sua conta do Lote usando o Azure AD, chame o comando [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login):</span><span class="sxs-lookup"><span data-stu-id="69b9d-160">To log in to your Batch account using Azure AD, call the [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command:</span></span> 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- <span data-ttu-id="69b9d-161">**Usando a autenticação de Chave compartilhada**</span><span class="sxs-lookup"><span data-stu-id="69b9d-161">**By using Shared Key authentication.**</span></span>

    <span data-ttu-id="69b9d-162">[Autenticação de chave compartilhada](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) usa suas chaves de acesso de conta a fim de autenticar comandos da CLI do Azure para o serviço Lote.</span><span class="sxs-lookup"><span data-stu-id="69b9d-162">[Shared Key authentication](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) uses your account access keys to authenticate Azure CLI commands for the Batch service.</span></span>

    <span data-ttu-id="69b9d-163">Se você estiver criando scripts da CLI do Azure para automatizar a chamada de comandos do Lote, poderá usar a autenticação de Chave Compartilhada ou uma entidade de serviço do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="69b9d-163">If you are creating Azure CLI scripts to automate calling Batch commands, you can use either Shared Key authentication, or an Azure AD service principal.</span></span> <span data-ttu-id="69b9d-164">Em alguns cenários, o uso da autenticação de Chave Compartilhada pode ser mais simples do que criar uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="69b9d-164">In some scenarios, using Shared Key authentication may be simpler than creating a service principal.</span></span>  

    <span data-ttu-id="69b9d-165">Para entrar usando autenticação de Chave Compartilhada, inclua a opção `--shared-key-auth` na linha de comando:</span><span class="sxs-lookup"><span data-stu-id="69b9d-165">To log in using Shared Key authentication, include the `--shared-key-auth` option on the command line:</span></span>

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

<span data-ttu-id="69b9d-166">Os exemplos listados na seção [Scripts de shell de exemplo](#sample-shell-scripts) mostram como entrar na conta do Lote com a CLI do Azure usando o Azure AD e a Chave Compartilhada.</span><span class="sxs-lookup"><span data-stu-id="69b9d-166">The examples listed in the [Sample shell scripts](#sample-shell-scripts) section show how to log into your Batch account with the Azure CLI using both Azure AD and Shared Key.</span></span>

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="69b9d-167">Usar modelos CLI do Lote do Azure e o arquivo de transferência (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="69b9d-167">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="69b9d-168">Você pode usar a CLI do Azure para executar trabalhos do Lote de ponta a ponta sem escrever código.</span><span class="sxs-lookup"><span data-stu-id="69b9d-168">You can use the Azure CLI to run Batch jobs end-to-end without writing code.</span></span> <span data-ttu-id="69b9d-169">Os arquivos de modelo do Lote dão suporte à criação de pools, trabalhos e tarefas com a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="69b9d-169">Batch template files support creating pools, jobs, and tasks with the Azure CLI.</span></span> <span data-ttu-id="69b9d-170">Você também pode usar a CLI do Azure para carregar arquivos de entrada de trabalho na conta de Armazenamento do Azure associada à conta do Lote e baixar arquivos de saída de trabalho dele.</span><span class="sxs-lookup"><span data-stu-id="69b9d-170">You can also use the Azure CLI to upload job input files to the Azure Storage account associated with the Batch account, and download job output files from it.</span></span> <span data-ttu-id="69b9d-171">Para saber mais, confira [Usar modelos da CLI do Lote do Azure e Transferência de Arquivos (Versão prévia)](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="69b9d-171">For more information, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

## <a name="sample-shell-scripts"></a><span data-ttu-id="69b9d-172">Scripts de shell de exemplo</span><span class="sxs-lookup"><span data-stu-id="69b9d-172">Sample shell scripts</span></span>

<span data-ttu-id="69b9d-173">Os scripts de exemplo listados na tabela a seguir mostram como usar os comandos da CLI do Azure com o serviço Lote e o serviço de gerenciamento em lotes para realizar tarefas comuns.</span><span class="sxs-lookup"><span data-stu-id="69b9d-173">The sample scripts listed in the following table show how to use Azure CLI commands with the Batch service and Batch Management service to accomplish common tasks.</span></span> <span data-ttu-id="69b9d-174">Esses scripts de exemplo cobrem muitos dos comandos disponíveis na CLI do Azure para o Lote.</span><span class="sxs-lookup"><span data-stu-id="69b9d-174">These sample scripts cover many of the commands available in the Azure CLI for Batch.</span></span> 

| <span data-ttu-id="69b9d-175">Script</span><span class="sxs-lookup"><span data-stu-id="69b9d-175">Script</span></span> | <span data-ttu-id="69b9d-176">Observações</span><span class="sxs-lookup"><span data-stu-id="69b9d-176">Notes</span></span> |
|---|---|
| [<span data-ttu-id="69b9d-177">Criar uma conta do Lote</span><span class="sxs-lookup"><span data-stu-id="69b9d-177">Create a Batch account</span></span>](./scripts/batch-cli-sample-create-account.md) | <span data-ttu-id="69b9d-178">Cria uma conta do Lote e associa uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="69b9d-178">Creates a Batch account and associates it with a storage account.</span></span> |
| [<span data-ttu-id="69b9d-179">Adicionar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="69b9d-179">Add an application</span></span>](./scripts/batch-cli-sample-add-application.md) | <span data-ttu-id="69b9d-180">Adiciona um aplicativo e carrega os binários do pacote.</span><span class="sxs-lookup"><span data-stu-id="69b9d-180">Adds an application and uploads packaged binaries.</span></span>|
| [<span data-ttu-id="69b9d-181">Gerenciar pools do Lote</span><span class="sxs-lookup"><span data-stu-id="69b9d-181">Manage Batch pools</span></span>](./scripts/batch-cli-sample-manage-pool.md) | <span data-ttu-id="69b9d-182">Demonstra como criar, redimensionar e gerenciar pools.</span><span class="sxs-lookup"><span data-stu-id="69b9d-182">Demonstrates creating, resizing, and managing pools.</span></span> |
| [<span data-ttu-id="69b9d-183">Executar um trabalho e tarefas com o Lote</span><span class="sxs-lookup"><span data-stu-id="69b9d-183">Run a job and tasks with Batch</span></span>](./scripts/batch-cli-sample-run-job.md) | <span data-ttu-id="69b9d-184">Demonstra como executar um trabalho e adicionar tarefas.</span><span class="sxs-lookup"><span data-stu-id="69b9d-184">Demonstrates running a job and adding tasks.</span></span> |

## <a name="json-files-for-resource-creation"></a><span data-ttu-id="69b9d-185">Arquivos JSON para a criação de recursos</span><span class="sxs-lookup"><span data-stu-id="69b9d-185">JSON files for resource creation</span></span>

<span data-ttu-id="69b9d-186">Ao criar recursos do Lote, como pools e trabalhos, você pode especificar um arquivo JSON contendo a nova configuração do recurso, em vez de passar seus parâmetros como opções da linha de comando.</span><span class="sxs-lookup"><span data-stu-id="69b9d-186">When you create Batch resources like pools and jobs, you can specify a JSON file containing the new resource's configuration instead of passing its parameters as command-line options.</span></span> <span data-ttu-id="69b9d-187">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="69b9d-187">For example:</span></span>

```azurecli
az batch pool create my_batch_pool.json
```

<span data-ttu-id="69b9d-188">Embora seja possível criar a maioria dos recursos do Lote usando apenas as opções de linha de comando, alguns recursos exigem a especificação de um arquivo formatado em JSON contendo os detalhes do recurso.</span><span class="sxs-lookup"><span data-stu-id="69b9d-188">While you can create most Batch resources using only command-line options, some features require that you specify a JSON-formatted file containing the resource details.</span></span> <span data-ttu-id="69b9d-189">Por exemplo, você deve usar um arquivo JSON se quiser especificar arquivos de recurso para uma tarefa de inicialização.</span><span class="sxs-lookup"><span data-stu-id="69b9d-189">For example, you must use a JSON file if you want to specify resource files for a start task.</span></span>

<span data-ttu-id="69b9d-190">Para ver a sintaxe JSON necessária para criar um recurso, consulte a documentação de [referência da API REST do Lote][rest_api].</span><span class="sxs-lookup"><span data-stu-id="69b9d-190">To see the JSON syntax required to create a resource, refer to the [Batch REST API reference][rest_api] documentation.</span></span> <span data-ttu-id="69b9d-191">Cada tópico "Adicionar *tipo de recurso*" na referência da API REST contém exemplos de scripts JSON para criar esse recurso.</span><span class="sxs-lookup"><span data-stu-id="69b9d-191">Each "Add *resource type*" topic in the REST API reference contains sample JSON scripts for creating that resource.</span></span> <span data-ttu-id="69b9d-192">Você pode usar esses exemplos de scripts JSON como modelos para que os arquivos JSON usem com a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="69b9d-192">You can use those sample JSON scripts as templates for JSON files to use with the Azure CLI.</span></span> <span data-ttu-id="69b9d-193">Por exemplo, para ver a sintaxe JSON para criação do pool, consulte [Adicionar um pool a uma conta][rest_add_pool].</span><span class="sxs-lookup"><span data-stu-id="69b9d-193">For example, to see the JSON syntax for pool creation, refer to [Add a pool to an account][rest_add_pool].</span></span>

<span data-ttu-id="69b9d-194">Para um exemplo de script que especifica um arquivo JSON, consulte [Executar um trabalho e tarefas com o Lote](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="69b9d-194">For a sample script that specifies a JSON file, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

> [!NOTE]
> <span data-ttu-id="69b9d-195">Se você especificar um arquivo JSON durante a criação de um recurso, todos os outros parâmetros especificados na linha de comando desse recurso serão ignorados.</span><span class="sxs-lookup"><span data-stu-id="69b9d-195">If you specify a JSON file when you create a resource, any other parameters that you specify on the command line for that resource are ignored.</span></span>
> 
> 

## <a name="efficient-queries-for-batch-resources"></a><span data-ttu-id="69b9d-196">Consultas eficientes para recursos do Lote</span><span class="sxs-lookup"><span data-stu-id="69b9d-196">Efficient queries for Batch resources</span></span>

<span data-ttu-id="69b9d-197">Cada tipo de recurso do Lote dá suporte a um comando `list` que consulta sua conta do Lote e lista os recursos desse tipo.</span><span class="sxs-lookup"><span data-stu-id="69b9d-197">Each Batch resource type supports a `list` command that queries your Batch account and lists resources of that type.</span></span> <span data-ttu-id="69b9d-198">Por exemplo, você pode listar os pools em sua conta e as tarefas em um trabalho:</span><span class="sxs-lookup"><span data-stu-id="69b9d-198">For example, you can list the pools in your account and the tasks in a job:</span></span>

```azurecli
az batch pool list
az batch task list --job-id job001
```

<span data-ttu-id="69b9d-199">Quando você consulta o serviço Lote com uma operação `list`, pode especificar uma cláusula OData para limitar a quantidade de dados retornados.</span><span class="sxs-lookup"><span data-stu-id="69b9d-199">When you query the Batch service with a `list` operation, you can specify an OData clause to limit the amount of data returned.</span></span> <span data-ttu-id="69b9d-200">Como toda a filtragem ocorre no lado do servidor, apenas os dados solicitados são transmitidos.</span><span class="sxs-lookup"><span data-stu-id="69b9d-200">Because all filtering occurs server-side, only the data you request crosses the wire.</span></span> <span data-ttu-id="69b9d-201">Use essas cláusulas para economizar largura de banda (e, portanto, tempo) ao executar operações de lista.</span><span class="sxs-lookup"><span data-stu-id="69b9d-201">Use these clauses to save bandwidth (and therefore time) when you perform list operations.</span></span>

<span data-ttu-id="69b9d-202">A tabela abaixo descreve as cláusulas OData com suporte no serviço Lote:</span><span class="sxs-lookup"><span data-stu-id="69b9d-202">The following table describes the OData clauses supported by the Batch service:</span></span>

| <span data-ttu-id="69b9d-203">Cláusula</span><span class="sxs-lookup"><span data-stu-id="69b9d-203">Clause</span></span> | <span data-ttu-id="69b9d-204">Descrição</span><span class="sxs-lookup"><span data-stu-id="69b9d-204">Description</span></span> |
|---|---|
| `--select-clause [select-clause]` | <span data-ttu-id="69b9d-205">Retorna um subconjunto de propriedades para cada entidade.</span><span class="sxs-lookup"><span data-stu-id="69b9d-205">Returns a subset of properties for each entity.</span></span> |
| `--filter-clause [filter-clause]` | <span data-ttu-id="69b9d-206">Retorna apenas as entidades que correspondem à expressão de OData especificada.</span><span class="sxs-lookup"><span data-stu-id="69b9d-206">Returns only entities that match the specified OData expression.</span></span> |
| `--expand-clause [expand-clause]` | <span data-ttu-id="69b9d-207">Obtém as informações de entidade em uma única chamada REST subjacente.</span><span class="sxs-lookup"><span data-stu-id="69b9d-207">Obtains the entity information in a single underlying REST call.</span></span> <span data-ttu-id="69b9d-208">A cláusula expand atualmente dá suporte apenas à propriedade `stats`.</span><span class="sxs-lookup"><span data-stu-id="69b9d-208">The expand clause currently supports only the `stats` property.</span></span> |

<span data-ttu-id="69b9d-209">Para um script de exemplo que mostra como usar uma cláusula OData, consulte [Executar um trabalho e tarefas com o Lote](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="69b9d-209">For a sample script that shows how to use an OData clause, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

<span data-ttu-id="69b9d-210">Para saber mais sobre como executar consultas de lista eficientes com cláusulas OData, consulte [Consultar o serviço Lote do Azure com eficiência](batch-efficient-list-queries.md).</span><span class="sxs-lookup"><span data-stu-id="69b9d-210">For more information on performing efficient list queries with OData clauses, see [Query the Azure Batch service efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="troubleshooting-tips"></a><span data-ttu-id="69b9d-211">Dicas de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="69b9d-211">Troubleshooting tips</span></span>

<span data-ttu-id="69b9d-212">As dicas abaixo poderão ajudar você quando estiver solucionando problemas da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="69b9d-212">The following tips may help when you are troubleshooting Azure CLI issues:</span></span>

* <span data-ttu-id="69b9d-213">Use `-h` para obter um **texto de ajuda** para qualquer comando da CLI</span><span class="sxs-lookup"><span data-stu-id="69b9d-213">Use `-h` to get **help text** for any CLI command</span></span>
* <span data-ttu-id="69b9d-214">Use `-v` e `-vv` para exibir saídas de comando **detalhadas**.</span><span class="sxs-lookup"><span data-stu-id="69b9d-214">Use `-v` and `-vv` to display **verbose** command output.</span></span> <span data-ttu-id="69b9d-215">Quando o sinalizador `-vv` é incluído, a CLI do Azure exibe as respostas e solicitações REST reais.</span><span class="sxs-lookup"><span data-stu-id="69b9d-215">When the `-vv` flag is included, the Azure CLI displays the actual REST requests and responses.</span></span> <span data-ttu-id="69b9d-216">Essas opções são úteis para exibir a saída completa do erro.</span><span class="sxs-lookup"><span data-stu-id="69b9d-216">These switches are handy for displaying full error output.</span></span>
* <span data-ttu-id="69b9d-217">Você pode exibir a **saída do comando como JSON** com a opção `--json`.</span><span class="sxs-lookup"><span data-stu-id="69b9d-217">You can view **command output as JSON** with the `--json` option.</span></span> <span data-ttu-id="69b9d-218">Por exemplo, o `az batch pool show pool001 --json` exibe propriedades do pool001 no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="69b9d-218">For example, `az batch pool show pool001 --json` displays pool001's properties in JSON format.</span></span> <span data-ttu-id="69b9d-219">Você pode copiar e modificar essa saída a fim de usá-la em um `--json-file` (consulte [Arquivos JSON](#json-files) anteriormente neste artigo).</span><span class="sxs-lookup"><span data-stu-id="69b9d-219">You can then copy and modify this output to use in a `--json-file` (see [JSON files](#json-files) earlier in this article).</span></span>
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting to any location.--->
* <span data-ttu-id="69b9d-220">O [Fórum do Lote][batch_forum] é monitorado por membros da equipe do Lote.</span><span class="sxs-lookup"><span data-stu-id="69b9d-220">The [Batch forum][batch_forum] is monitored by Batch team members.</span></span> <span data-ttu-id="69b9d-221">Você pode publicar suas perguntas nesse local caso tenha problemas ou queira obter ajuda com uma operação específica.</span><span class="sxs-lookup"><span data-stu-id="69b9d-221">You can post your questions there if you run into issues or would like help with a specific operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="69b9d-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="69b9d-222">Next steps</span></span>

* <span data-ttu-id="69b9d-223">Para saber mais sobre a CLI do Azure, veja a [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="69b9d-223">For more information about the Azure CLI, see the [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="69b9d-224">Para saber mais sobre recursos do Lote, consulte [Visão geral do Lote do Azure para desenvolvedores](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="69b9d-224">For more information about Batch resources, see [Overview of Azure Batch for developers](batch-api-basics.md).</span></span>
* <span data-ttu-id="69b9d-225">Para saber mais sobre como usar modelos do Lote para criar pools, trabalhos e tarefas sem escrever código, confira [Usar modelos da CLI do Lote do Azure e Transferência de Arquivos (Versão prévia)](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="69b9d-225">For more information about using Batch templates to create pools, jobs, and tasks without writing code, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
