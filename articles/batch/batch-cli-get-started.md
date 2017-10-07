---
title: aaaGet iniciado com a CLI do Azure para o lote | Microsoft Docs
description: "Obter uma introdução rápida toohello comandos de lote em CLI do Azure para gerenciamento de recursos de serviço de lote do Azure"
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
ms.openlocfilehash: 14f28311ecb16c8097d0d304a4ad89de282a2e9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-batch-resources-with-azure-cli"></a><span data-ttu-id="f82c1-103">Gerenciar recursos do Lote com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f82c1-103">Manage Batch resources with Azure CLI</span></span>

<span data-ttu-id="f82c1-104">Olá 2.0 do CLI do Azure é a nova experiência de linha de comando do Azure para gerenciar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f82c1-104">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="f82c1-105">Ela pode ser usada em Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="f82c1-105">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="f82c1-106">2.0 do CLI do Azure é otimizado para gerenciar e administrar os recursos do Azure da linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="f82c1-106">Azure CLI 2.0 is optimized for managing and administering Azure resources from hello command line.</span></span> <span data-ttu-id="f82c1-107">Você pode usar o hello CLI do Azure toomanage suas contas de lote do Azure e os recursos de toomanage como pools, trabalhos e tarefas.</span><span class="sxs-lookup"><span data-stu-id="f82c1-107">You can use hello Azure CLI toomanage your Azure Batch accounts and toomanage resources such as pools, jobs, and tasks.</span></span> <span data-ttu-id="f82c1-108">Com hello CLI do Azure, você pode gerar um script muitas Olá Olá de mesmas tarefas que você executa com APIs de lote, o portal do Azure e cmdlets do PowerShell do lote.</span><span class="sxs-lookup"><span data-stu-id="f82c1-108">With hello Azure CLI, you can script many of hello same tasks you carry out with hello Batch APIs, Azure portal, and Batch PowerShell cmdlets.</span></span>

<span data-ttu-id="f82c1-109">Este artigo fornece uma visão geral do uso da [CLI do Azure versão 2.0](https://docs.microsoft.com/cli/azure/overview) com o Lote.</span><span class="sxs-lookup"><span data-stu-id="f82c1-109">This article provides an overview of using [Azure CLI version 2.0](https://docs.microsoft.com/cli/azure/overview) with Batch.</span></span> <span data-ttu-id="f82c1-110">Consulte [Introdução ao Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) para obter uma visão geral do uso de saudação CLI com o Azure.</span><span class="sxs-lookup"><span data-stu-id="f82c1-110">See [Get started with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-azure-cli) for an overview of using hello CLI with Azure.</span></span>

<span data-ttu-id="f82c1-111">A Microsoft recomenda usar Olá última versão do hello CLI do Azure, versão 2.0.</span><span class="sxs-lookup"><span data-stu-id="f82c1-111">Microsoft recommends using hello latest version of hello Azure CLI, version 2.0.</span></span> <span data-ttu-id="f82c1-112">Para saber mais sobre a versão 2.0, consulte [CLI do Azure 2.0 agora disponível](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span><span class="sxs-lookup"><span data-stu-id="f82c1-112">For more information about version 2.0, see [Azure Command Line 2.0 now generally available](https://azure.microsoft.com/blog/announcing-general-availability-of-vm-storage-and-network-azure-cli-2-0/).</span></span>

## <a name="set-up-hello-azure-cli"></a><span data-ttu-id="f82c1-113">Configurar Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f82c1-113">Set up hello Azure CLI</span></span>

<span data-ttu-id="f82c1-114">Olá tooinstall CLI do Azure, execute as etapas de saudação descritas em [instalação Olá CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="f82c1-114">tooinstall hello Azure CLI, follow hello steps outlined in [Install hello Azure CLI](https://docs.microsoft.com/cli/azure/install-azure-cli.md).</span></span>

> [!TIP]
> <span data-ttu-id="f82c1-115">Recomendamos que você atualize sua instalação de CLI do Azure com frequência tootake vantagem do serviço de atualizações e aprimoramentos.</span><span class="sxs-lookup"><span data-stu-id="f82c1-115">We recommend that you update your Azure CLI installation frequently tootake advantage of service updates and enhancements.</span></span>
> 
> 

## <a name="command-help"></a><span data-ttu-id="f82c1-116">Ajuda de comando</span><span class="sxs-lookup"><span data-stu-id="f82c1-116">Command help</span></span>

<span data-ttu-id="f82c1-117">Você pode exibir o texto de ajuda para cada comando em Olá CLI do Azure, acrescentando `-h` toohello comando.</span><span class="sxs-lookup"><span data-stu-id="f82c1-117">You can display help text for every command in hello Azure CLI by appending `-h` toohello command.</span></span> <span data-ttu-id="f82c1-118">Omita as outras opções.</span><span class="sxs-lookup"><span data-stu-id="f82c1-118">Omit any other options.</span></span> <span data-ttu-id="f82c1-119">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f82c1-119">For example:</span></span>

* <span data-ttu-id="f82c1-120">Ajuda de tooget para Olá `az` de comando, digite:`az -h`</span><span class="sxs-lookup"><span data-stu-id="f82c1-120">tooget help for hello `az` command, enter: `az -h`</span></span>
* <span data-ttu-id="f82c1-121">tooget uma lista de todos os comandos de lote no hello CLI, use:`az batch -h`</span><span class="sxs-lookup"><span data-stu-id="f82c1-121">tooget a list of all Batch commands in hello CLI, use: `az batch -h`</span></span>
* <span data-ttu-id="f82c1-122">tooget ajuda sobre como criar uma conta em lotes, digite:`az batch account create -h`</span><span class="sxs-lookup"><span data-stu-id="f82c1-122">tooget help on creating a Batch account, enter: `az batch account create -h`</span></span>

<span data-ttu-id="f82c1-123">Em caso de dúvida, use Olá `-h` opção de linha de comando tooget ajuda sobre qualquer comando CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="f82c1-123">When in doubt, use hello `-h` command-line option tooget help on any Azure CLI command.</span></span>

> [!NOTE]
> <span data-ttu-id="f82c1-124">Versões anteriores do hello CLI do Azure usado `azure` toopreface um comando CLI.</span><span class="sxs-lookup"><span data-stu-id="f82c1-124">Earlier versions of hello Azure CLI used `azure` toopreface a CLI command.</span></span> <span data-ttu-id="f82c1-125">Na versão 2.0, todos os comandos agora são precedidos por `az`.</span><span class="sxs-lookup"><span data-stu-id="f82c1-125">In version 2.0, all commands are now prefaced with `az`.</span></span> <span data-ttu-id="f82c1-126">Ser tooupdate-se de que seus scripts toouse Olá nova sintaxe com a versão 2.0.</span><span class="sxs-lookup"><span data-stu-id="f82c1-126">Be sure tooupdate your scripts toouse hello new syntax with version 2.0.</span></span>
>
>  

<span data-ttu-id="f82c1-127">Além disso, consulte a documentação de referência toohello CLI do Azure para obter detalhes sobre [comandos de CLI do Azure para o lote](https://docs.microsoft.com/cli/azure/batch).</span><span class="sxs-lookup"><span data-stu-id="f82c1-127">Additionally, refer toohello Azure CLI reference documentation for details about [Azure CLI commands for Batch](https://docs.microsoft.com/cli/azure/batch).</span></span> 

## <a name="log-in-and-authenticate"></a><span data-ttu-id="f82c1-128">Fazer logon e autenticar</span><span class="sxs-lookup"><span data-stu-id="f82c1-128">Log in and authenticate</span></span>

<span data-ttu-id="f82c1-129">Olá toouse CLI do Azure com o lote, você precisa toolog no e autenticar.</span><span class="sxs-lookup"><span data-stu-id="f82c1-129">toouse hello Azure CLI with Batch, you need toolog in and authenticate.</span></span> <span data-ttu-id="f82c1-130">Há dois toofollow de etapas simples:</span><span class="sxs-lookup"><span data-stu-id="f82c1-130">There are two simple steps toofollow:</span></span>

1. <span data-ttu-id="f82c1-131">**Faça logon no Azure.**</span><span class="sxs-lookup"><span data-stu-id="f82c1-131">**Log into Azure.**</span></span> <span data-ttu-id="f82c1-132">Fazendo logon no Azure fornece acesso a comandos do Gerenciador de recursos tooAzure, incluindo [serviço de gerenciamento de lote](batch-management-dotnet.md) comandos.</span><span class="sxs-lookup"><span data-stu-id="f82c1-132">Logging into Azure gives you access tooAzure Resource Manager commands, including [Batch Management service](batch-management-dotnet.md) commands.</span></span>  
2. <span data-ttu-id="f82c1-133">**Faça logon em sua conta do Lote.**</span><span class="sxs-lookup"><span data-stu-id="f82c1-133">**Log into your Batch account.**</span></span> <span data-ttu-id="f82c1-134">Fazer logon no seu dá conta de lote você acessar tooBatch comandos de serviço.</span><span class="sxs-lookup"><span data-stu-id="f82c1-134">Logging into your Batch account gives you access tooBatch service commands.</span></span>   

### <a name="log-in-tooazure"></a><span data-ttu-id="f82c1-135">Faça logon no tooAzure</span><span class="sxs-lookup"><span data-stu-id="f82c1-135">Log in tooAzure</span></span>

<span data-ttu-id="f82c1-136">Há alguns toolog de maneiras diferentes para o Azure, descrito detalhadamente na [fazer logon com o Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span><span class="sxs-lookup"><span data-stu-id="f82c1-136">There are a few different ways toolog into Azure, described in detail in [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli):</span></span>

1. <span data-ttu-id="f82c1-137">[Fazer logon interativamente](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span><span class="sxs-lookup"><span data-stu-id="f82c1-137">[Log in interactively](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#interactive-log-in).</span></span> <span data-ttu-id="f82c1-138">Faça logon interativamente quando você estiver executando os comandos de CLI do Azure da linha de comando hello.</span><span class="sxs-lookup"><span data-stu-id="f82c1-138">Log in interactively when you are running Azure CLI commands yourself from hello command line.</span></span>
2. <span data-ttu-id="f82c1-139">[Fazer logon com uma entidade de serviço](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span><span class="sxs-lookup"><span data-stu-id="f82c1-139">[Log in with a service principal](https://docs.microsoft.com/cli/azure/authenticate-azure-cli#logging-in-with-a-service-principal).</span></span> <span data-ttu-id="f82c1-140">Faça logon com uma entidade de serviço quando você estiver executando comandos da CLI do Azure de um script ou aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f82c1-140">Log in with a service principal when you are running Azure CLI commands from a script or an application.</span></span>

<span data-ttu-id="f82c1-141">Para fins de saudação deste artigo, mostramos como toolog no Azure interativamente.</span><span class="sxs-lookup"><span data-stu-id="f82c1-141">For hello purposes of this article, we show how toolog into Azure interactively.</span></span> <span data-ttu-id="f82c1-142">Tipo [logon az](https://docs.microsoft.com/cli/azure/#login) na linha de comando hello:</span><span class="sxs-lookup"><span data-stu-id="f82c1-142">Type [az login](https://docs.microsoft.com/cli/azure/#login) on hello command line:</span></span>

```azurecli
# Log in tooAzure and authenticate interactively.
az login
```

<span data-ttu-id="f82c1-143">Olá `az login` comando retorna um token que você pode usar tooauthenticate, conforme mostrado aqui.</span><span class="sxs-lookup"><span data-stu-id="f82c1-143">hello `az login` command returns a token that you can use tooauthenticate, as shown here.</span></span> <span data-ttu-id="f82c1-144">Execute Olá instruções fornecidas tooopen uma página da web e enviar tooAzure token hello:</span><span class="sxs-lookup"><span data-stu-id="f82c1-144">Follow hello instructions provided tooopen a web page and submit hello token tooAzure:</span></span>

![Faça logon no tooAzure](./media/batch-cli-get-started/az-login.png)

<span data-ttu-id="f82c1-146">exemplos de saudação listados no hello [scripts de shell de exemplo](#sample-shell-scripts) seção também mostra como toostart sua sessão de CLI do Azure fazendo logon interativamente no Azure.</span><span class="sxs-lookup"><span data-stu-id="f82c1-146">hello examples listed in hello [Sample shell scripts](#sample-shell-scripts) section also show how toostart your Azure CLI session by logging into Azure interactively.</span></span> <span data-ttu-id="f82c1-147">Depois de você ter conectado, você pode chamar comandos toowork com recursos de gerenciamento em lote, incluindo contas, chaves, pacotes de aplicativos e cotas do lote.</span><span class="sxs-lookup"><span data-stu-id="f82c1-147">Once you have logged in, you can call commands toowork with Batch Management resources, including Batch accounts, keys, application packages, and quotas.</span></span>  

### <a name="log-in-tooyour-batch-account"></a><span data-ttu-id="f82c1-148">Faça logon no tooyour conta em lotes</span><span class="sxs-lookup"><span data-stu-id="f82c1-148">Log in tooyour Batch account</span></span>

<span data-ttu-id="f82c1-149">toouse Olá CLI do Azure toomanage recursos de lote, como pools, trabalhos e tarefas, você precisa toolog em sua conta de lote e autentica.</span><span class="sxs-lookup"><span data-stu-id="f82c1-149">toouse hello Azure CLI toomanage Batch resources, such as pools, jobs, and tasks, you need toolog into your Batch account and authenticate.</span></span> <span data-ttu-id="f82c1-150">toolog em toohello serviço de lote, use Olá [logon de conta de lote az](https://docs.microsoft.com/cli/azure/batch/account#login) comando.</span><span class="sxs-lookup"><span data-stu-id="f82c1-150">toolog in toohello Batch service, use hello [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command.</span></span> 

<span data-ttu-id="f82c1-151">Você tem duas opções para autenticação na sua conta do Lote:</span><span class="sxs-lookup"><span data-stu-id="f82c1-151">You have two options for authenticating against your Batch account:</span></span>

- <span data-ttu-id="f82c1-152">**Usando a autenticação do Azure AD (Azure Active Directory)**</span><span class="sxs-lookup"><span data-stu-id="f82c1-152">**By using Azure Active Directory (Azure AD) authentication.**</span></span> 

    <span data-ttu-id="f82c1-153">Autenticar com o AD do Azure é o padrão de hello quando você usa Olá CLI do Azure com o lote e recomendado na maioria dos cenários.</span><span class="sxs-lookup"><span data-stu-id="f82c1-153">Authenticating with Azure AD is hello default when you use hello Azure CLI with Batch, and recommended for most scenarios.</span></span> 
    
    <span data-ttu-id="f82c1-154">Quando você efetuar logon interativamente, conforme descrito na seção anterior Olá em tooAzure, suas credenciais são armazenadas em cache, para que Olá CLI do Azure pode fazer o logon tooyour usando as mesmas credenciais de conta do lote.</span><span class="sxs-lookup"><span data-stu-id="f82c1-154">When you log in tooAzure interactively, as described in hello previous section, your credentials are cached, so hello Azure CLI can log you in tooyour Batch account using those same credentials.</span></span> <span data-ttu-id="f82c1-155">Se você efetuar logon em tooAzure usando uma entidade de serviço, essas credenciais também são toolog usado em tooyour conta do lote.</span><span class="sxs-lookup"><span data-stu-id="f82c1-155">If you log in tooAzure using a service principal, those credentials are also used toolog in tooyour Batch account.</span></span>

    <span data-ttu-id="f82c1-156">Uma vantagem do Azure AD é que ele oferece RBAC (controle de acesso baseado em função).</span><span class="sxs-lookup"><span data-stu-id="f82c1-156">An advantage of Azure AD is that it offers role-based access control (RBAC).</span></span> <span data-ttu-id="f82c1-157">Com o RBAC, acesso do usuário depende de sua função atribuída, em vez de estarem ou não possui chaves de conta Olá.</span><span class="sxs-lookup"><span data-stu-id="f82c1-157">With RBAC, a user's access depends on their assigned role, rather than whether or not they possess hello account keys.</span></span> <span data-ttu-id="f82c1-158">Em vez de gerenciar chaves de conta, você pode gerenciar funções RBAC e permitir que o Azure AD lide com autenticação e acesso.</span><span class="sxs-lookup"><span data-stu-id="f82c1-158">Instead of managing account keys, you can manage RBAC roles, and let Azure AD handle access and authentication.</span></span>  

    <span data-ttu-id="f82c1-159">Autenticar com o AD do Azure é necessária se você criou sua conta de lote do Azure com o modo de alocação do pool definido too'User assinatura '.</span><span class="sxs-lookup"><span data-stu-id="f82c1-159">Authenticating with Azure AD is required if you created your Azure Batch account with its pool allocation mode set too'User Subscription'.</span></span> 

    <span data-ttu-id="f82c1-160">toolog em tooyour lote conta usando o Azure AD, chame Olá [logon de conta de lote az](https://docs.microsoft.com/cli/azure/batch/account#login) comando:</span><span class="sxs-lookup"><span data-stu-id="f82c1-160">toolog in tooyour Batch account using Azure AD, call hello [az batch account login](https://docs.microsoft.com/cli/azure/batch/account#login) command:</span></span> 

    ```azurecli
    az batch account login -g myresource group -n mybatchaccount
    ```

- <span data-ttu-id="f82c1-161">**Usando a autenticação de Chave compartilhada**</span><span class="sxs-lookup"><span data-stu-id="f82c1-161">**By using Shared Key authentication.**</span></span>

    <span data-ttu-id="f82c1-162">[Autenticação de chave compartilhada](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) serviço de lote usa tooauthenticate comandos de CLI do Azure para Olá das chaves de acesso à sua conta.</span><span class="sxs-lookup"><span data-stu-id="f82c1-162">[Shared Key authentication](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service#authentication-via-shared-key) uses your account access keys tooauthenticate Azure CLI commands for hello Batch service.</span></span>

    <span data-ttu-id="f82c1-163">Se você estiver criando scripts de CLI do Azure tooautomate chamados comandos de lote, você pode usar a autenticação de chave compartilhada ou uma entidade de serviço do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="f82c1-163">If you are creating Azure CLI scripts tooautomate calling Batch commands, you can use either Shared Key authentication, or an Azure AD service principal.</span></span> <span data-ttu-id="f82c1-164">Em alguns cenários, o uso da autenticação de Chave Compartilhada pode ser mais simples do que criar uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="f82c1-164">In some scenarios, using Shared Key authentication may be simpler than creating a service principal.</span></span>  

    <span data-ttu-id="f82c1-165">toolog usando a autenticação de chave compartilhada incluem hello `--shared-key-auth` opção na linha de comando hello:</span><span class="sxs-lookup"><span data-stu-id="f82c1-165">toolog in using Shared Key authentication, include hello `--shared-key-auth` option on hello command line:</span></span>

    ```azurecli
    az batch account login -g myresourcegroup -n mybatchaccount --shared-key-auth
    ```

<span data-ttu-id="f82c1-166">exemplos de saudação listados no hello [scripts de shell de exemplo](#sample-shell-scripts) seção mostrará como toolog em sua conta de lote com hello CLI do Azure usando AD do Azure e a chave compartilhada.</span><span class="sxs-lookup"><span data-stu-id="f82c1-166">hello examples listed in hello [Sample shell scripts](#sample-shell-scripts) section show how toolog into your Batch account with hello Azure CLI using both Azure AD and Shared Key.</span></span>

## <a name="use-azure-batch-cli-templates-and-file-transfer-preview"></a><span data-ttu-id="f82c1-167">Usar modelos CLI do Lote do Azure e o arquivo de transferência (Versão prévia)</span><span class="sxs-lookup"><span data-stu-id="f82c1-167">Use Azure Batch CLI Templates and File Transfer (Preview)</span></span>

<span data-ttu-id="f82c1-168">Você pode usar o hello CLI do Azure toorun lote trabalhos ponta a ponta sem escrever código.</span><span class="sxs-lookup"><span data-stu-id="f82c1-168">You can use hello Azure CLI toorun Batch jobs end-to-end without writing code.</span></span> <span data-ttu-id="f82c1-169">Suporte para arquivos de modelo do lote Criando pools, trabalhos e tarefas com hello CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="f82c1-169">Batch template files support creating pools, jobs, and tasks with hello Azure CLI.</span></span> <span data-ttu-id="f82c1-170">Você também pode usar arquivos de entrada de trabalho Olá CLI do Azure tooupload toohello conta de armazenamento do Azure associada a saudação conta de lote e baixar arquivos de saída de trabalho dele.</span><span class="sxs-lookup"><span data-stu-id="f82c1-170">You can also use hello Azure CLI tooupload job input files toohello Azure Storage account associated with hello Batch account, and download job output files from it.</span></span> <span data-ttu-id="f82c1-171">Para saber mais, confira [Usar modelos da CLI do Lote do Azure e Transferência de Arquivos (Versão prévia)](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f82c1-171">For more information, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

## <a name="sample-shell-scripts"></a><span data-ttu-id="f82c1-172">Scripts de shell de exemplo</span><span class="sxs-lookup"><span data-stu-id="f82c1-172">Sample shell scripts</span></span>

<span data-ttu-id="f82c1-173">scripts de exemplo Hello listadas na Olá Mostrar tabela a seguir como os comandos toouse CLI do Azure com o serviço de lote hello e tarefas comuns de tooaccomplish de serviço de gerenciamento em lote.</span><span class="sxs-lookup"><span data-stu-id="f82c1-173">hello sample scripts listed in hello following table show how toouse Azure CLI commands with hello Batch service and Batch Management service tooaccomplish common tasks.</span></span> <span data-ttu-id="f82c1-174">Esses scripts de exemplo incluir vários comandos de saudação disponíveis no hello CLI do Azure para o lote.</span><span class="sxs-lookup"><span data-stu-id="f82c1-174">These sample scripts cover many of hello commands available in hello Azure CLI for Batch.</span></span> 

| <span data-ttu-id="f82c1-175">Script</span><span class="sxs-lookup"><span data-stu-id="f82c1-175">Script</span></span> | <span data-ttu-id="f82c1-176">Observações</span><span class="sxs-lookup"><span data-stu-id="f82c1-176">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f82c1-177">Criar uma conta do Lote</span><span class="sxs-lookup"><span data-stu-id="f82c1-177">Create a Batch account</span></span>](./scripts/batch-cli-sample-create-account.md) | <span data-ttu-id="f82c1-178">Cria uma conta do Lote e associa uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="f82c1-178">Creates a Batch account and associates it with a storage account.</span></span> |
| [<span data-ttu-id="f82c1-179">Adicionar um aplicativo</span><span class="sxs-lookup"><span data-stu-id="f82c1-179">Add an application</span></span>](./scripts/batch-cli-sample-add-application.md) | <span data-ttu-id="f82c1-180">Adiciona um aplicativo e carrega os binários do pacote.</span><span class="sxs-lookup"><span data-stu-id="f82c1-180">Adds an application and uploads packaged binaries.</span></span>|
| [<span data-ttu-id="f82c1-181">Gerenciar pools do Lote</span><span class="sxs-lookup"><span data-stu-id="f82c1-181">Manage Batch pools</span></span>](./scripts/batch-cli-sample-manage-pool.md) | <span data-ttu-id="f82c1-182">Demonstra como criar, redimensionar e gerenciar pools.</span><span class="sxs-lookup"><span data-stu-id="f82c1-182">Demonstrates creating, resizing, and managing pools.</span></span> |
| [<span data-ttu-id="f82c1-183">Executar um trabalho e tarefas com o Lote</span><span class="sxs-lookup"><span data-stu-id="f82c1-183">Run a job and tasks with Batch</span></span>](./scripts/batch-cli-sample-run-job.md) | <span data-ttu-id="f82c1-184">Demonstra como executar um trabalho e adicionar tarefas.</span><span class="sxs-lookup"><span data-stu-id="f82c1-184">Demonstrates running a job and adding tasks.</span></span> |

## <a name="json-files-for-resource-creation"></a><span data-ttu-id="f82c1-185">Arquivos JSON para a criação de recursos</span><span class="sxs-lookup"><span data-stu-id="f82c1-185">JSON files for resource creation</span></span>

<span data-ttu-id="f82c1-186">Quando você criar recursos de lote como pools e trabalhos, você pode especificar um arquivo JSON que contém a configuração do recurso novo Olá em vez de passar os parâmetros como opções de linha de comando.</span><span class="sxs-lookup"><span data-stu-id="f82c1-186">When you create Batch resources like pools and jobs, you can specify a JSON file containing hello new resource's configuration instead of passing its parameters as command-line options.</span></span> <span data-ttu-id="f82c1-187">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f82c1-187">For example:</span></span>

```azurecli
az batch pool create my_batch_pool.json
```

<span data-ttu-id="f82c1-188">Embora você possa criar a maioria dos recursos de lote usando apenas as opções de linha de comando, alguns recursos exigem que você especifique um arquivo no formato JSON que contém detalhes do recurso hello.</span><span class="sxs-lookup"><span data-stu-id="f82c1-188">While you can create most Batch resources using only command-line options, some features require that you specify a JSON-formatted file containing hello resource details.</span></span> <span data-ttu-id="f82c1-189">Por exemplo, você deve usar um arquivo JSON se você quiser que os arquivos de recursos de toospecify para uma tarefa inicial.</span><span class="sxs-lookup"><span data-stu-id="f82c1-189">For example, you must use a JSON file if you want toospecify resource files for a start task.</span></span>

<span data-ttu-id="f82c1-190">Olá toosee sintaxe JSON necessário toocreate um recurso, consulte toohello [referência da API REST de lote] [ rest_api] documentação.</span><span class="sxs-lookup"><span data-stu-id="f82c1-190">toosee hello JSON syntax required toocreate a resource, refer toohello [Batch REST API reference][rest_api] documentation.</span></span> <span data-ttu-id="f82c1-191">Cada "adicionar *tipo de recurso*" tópico na referência da API REST de saudação contém scripts de JSON de exemplo para a criação desse recurso.</span><span class="sxs-lookup"><span data-stu-id="f82c1-191">Each "Add *resource type*" topic in hello REST API reference contains sample JSON scripts for creating that resource.</span></span> <span data-ttu-id="f82c1-192">Você pode usar esses scripts JSON de exemplo como modelo para JSON arquivos toouse com hello CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="f82c1-192">You can use those sample JSON scripts as templates for JSON files toouse with hello Azure CLI.</span></span> <span data-ttu-id="f82c1-193">Por exemplo, toosee Olá sintaxe JSON para a criação do pool, consulte muito[adicionar uma conta do pool de tooan][rest_add_pool].</span><span class="sxs-lookup"><span data-stu-id="f82c1-193">For example, toosee hello JSON syntax for pool creation, refer too[Add a pool tooan account][rest_add_pool].</span></span>

<span data-ttu-id="f82c1-194">Para um exemplo de script que especifica um arquivo JSON, consulte [Executar um trabalho e tarefas com o Lote](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="f82c1-194">For a sample script that specifies a JSON file, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f82c1-195">Se você especificar um arquivo JSON quando você cria um recurso, quaisquer outros parâmetros que você especificou na linha de comando Olá para esse recurso são ignorados.</span><span class="sxs-lookup"><span data-stu-id="f82c1-195">If you specify a JSON file when you create a resource, any other parameters that you specify on hello command line for that resource are ignored.</span></span>
> 
> 

## <a name="efficient-queries-for-batch-resources"></a><span data-ttu-id="f82c1-196">Consultas eficientes para recursos do Lote</span><span class="sxs-lookup"><span data-stu-id="f82c1-196">Efficient queries for Batch resources</span></span>

<span data-ttu-id="f82c1-197">Cada tipo de recurso do Lote dá suporte a um comando `list` que consulta sua conta do Lote e lista os recursos desse tipo.</span><span class="sxs-lookup"><span data-stu-id="f82c1-197">Each Batch resource type supports a `list` command that queries your Batch account and lists resources of that type.</span></span> <span data-ttu-id="f82c1-198">Por exemplo, você pode listar os pools de saudação em suas tarefas de conta e hello em um trabalho:</span><span class="sxs-lookup"><span data-stu-id="f82c1-198">For example, you can list hello pools in your account and hello tasks in a job:</span></span>

```azurecli
az batch pool list
az batch task list --job-id job001
```

<span data-ttu-id="f82c1-199">Quando você consulta o serviço de lote Olá com um `list` operação, você pode especificar um valor de saudação do OData cláusula toolimit dos dados retornados.</span><span class="sxs-lookup"><span data-stu-id="f82c1-199">When you query hello Batch service with a `list` operation, you can specify an OData clause toolimit hello amount of data returned.</span></span> <span data-ttu-id="f82c1-200">Como toda a filtragem ocorre no lado do servidor, somente dados Olá que solicitar cruzem durante a transmissão hello.</span><span class="sxs-lookup"><span data-stu-id="f82c1-200">Because all filtering occurs server-side, only hello data you request crosses hello wire.</span></span> <span data-ttu-id="f82c1-201">Usar largura de banda de toosave essas cláusulas (e, portanto, o tempo) quando você executa operações de lista.</span><span class="sxs-lookup"><span data-stu-id="f82c1-201">Use these clauses toosave bandwidth (and therefore time) when you perform list operations.</span></span>

<span data-ttu-id="f82c1-202">Olá tabela a seguir descreve as cláusulas de OData Olá suportadas pelo serviço de lote de saudação:</span><span class="sxs-lookup"><span data-stu-id="f82c1-202">hello following table describes hello OData clauses supported by hello Batch service:</span></span>

| <span data-ttu-id="f82c1-203">Cláusula</span><span class="sxs-lookup"><span data-stu-id="f82c1-203">Clause</span></span> | <span data-ttu-id="f82c1-204">Descrição</span><span class="sxs-lookup"><span data-stu-id="f82c1-204">Description</span></span> |
|---|---|
| `--select-clause [select-clause]` | <span data-ttu-id="f82c1-205">Retorna um subconjunto de propriedades para cada entidade.</span><span class="sxs-lookup"><span data-stu-id="f82c1-205">Returns a subset of properties for each entity.</span></span> |
| `--filter-clause [filter-clause]` | <span data-ttu-id="f82c1-206">Retorna apenas as entidades que correspondem a saudação especificado expressão do OData.</span><span class="sxs-lookup"><span data-stu-id="f82c1-206">Returns only entities that match hello specified OData expression.</span></span> |
| `--expand-clause [expand-clause]` | <span data-ttu-id="f82c1-207">Obtém informações de entidade de saudação em uma única chamada REST subjacente.</span><span class="sxs-lookup"><span data-stu-id="f82c1-207">Obtains hello entity information in a single underlying REST call.</span></span> <span data-ttu-id="f82c1-208">Olá expanda cláusula atualmente suporta apenas Olá `stats` propriedade.</span><span class="sxs-lookup"><span data-stu-id="f82c1-208">hello expand clause currently supports only hello `stats` property.</span></span> |

<span data-ttu-id="f82c1-209">Para obter um exemplo de script que mostra como toouse uma cláusula de OData, consulte [executar um trabalho e tarefas com lotes](./scripts/batch-cli-sample-run-job.md).</span><span class="sxs-lookup"><span data-stu-id="f82c1-209">For a sample script that shows how toouse an OData clause, see [Run a job and tasks with Batch](./scripts/batch-cli-sample-run-job.md).</span></span>

<span data-ttu-id="f82c1-210">Para obter mais informações sobre como executar consultas da lista eficiente com cláusulas de OData, consulte [consultar o serviço de lote do Azure Olá com eficiência](batch-efficient-list-queries.md).</span><span class="sxs-lookup"><span data-stu-id="f82c1-210">For more information on performing efficient list queries with OData clauses, see [Query hello Azure Batch service efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="troubleshooting-tips"></a><span data-ttu-id="f82c1-211">Dicas de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="f82c1-211">Troubleshooting tips</span></span>

<span data-ttu-id="f82c1-212">Olá dicas a seguir podem ajudar a quando estiver solucionando problemas de CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="f82c1-212">hello following tips may help when you are troubleshooting Azure CLI issues:</span></span>

* <span data-ttu-id="f82c1-213">Use `-h` tooget **texto de Ajuda** para qualquer comando CLI</span><span class="sxs-lookup"><span data-stu-id="f82c1-213">Use `-h` tooget **help text** for any CLI command</span></span>
* <span data-ttu-id="f82c1-214">Use `-v` e `-vv` toodisplay **detalhado** saída de comando.</span><span class="sxs-lookup"><span data-stu-id="f82c1-214">Use `-v` and `-vv` toodisplay **verbose** command output.</span></span> <span data-ttu-id="f82c1-215">Olá quando `-vv` sinalizador for incluído, Olá CLI do Azure exibe Olá reais solicitações e respostas REST.</span><span class="sxs-lookup"><span data-stu-id="f82c1-215">When hello `-vv` flag is included, hello Azure CLI displays hello actual REST requests and responses.</span></span> <span data-ttu-id="f82c1-216">Essas opções são úteis para exibir a saída completa do erro.</span><span class="sxs-lookup"><span data-stu-id="f82c1-216">These switches are handy for displaying full error output.</span></span>
* <span data-ttu-id="f82c1-217">Você pode exibir **comando saída como JSON** com hello `--json` opção.</span><span class="sxs-lookup"><span data-stu-id="f82c1-217">You can view **command output as JSON** with hello `--json` option.</span></span> <span data-ttu-id="f82c1-218">Por exemplo, o `az batch pool show pool001 --json` exibe propriedades do pool001 no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="f82c1-218">For example, `az batch pool show pool001 --json` displays pool001's properties in JSON format.</span></span> <span data-ttu-id="f82c1-219">Você pode copiar e modificar toouse essa saída em um `--json-file` (consulte [arquivos JSON](#json-files) anteriormente neste artigo).</span><span class="sxs-lookup"><span data-stu-id="f82c1-219">You can then copy and modify this output toouse in a `--json-file` (see [JSON files](#json-files) earlier in this article).</span></span>
<!---Loc Comment: Please, check link [JSON files] since it's not redirecting tooany location.--->
* <span data-ttu-id="f82c1-220">Olá [Fórum do lote] [ batch_forum] é monitorada por membros da equipe em lotes.</span><span class="sxs-lookup"><span data-stu-id="f82c1-220">hello [Batch forum][batch_forum] is monitored by Batch team members.</span></span> <span data-ttu-id="f82c1-221">Você pode publicar suas perguntas nesse local caso tenha problemas ou queira obter ajuda com uma operação específica.</span><span class="sxs-lookup"><span data-stu-id="f82c1-221">You can post your questions there if you run into issues or would like help with a specific operation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f82c1-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f82c1-222">Next steps</span></span>

* <span data-ttu-id="f82c1-223">Para obter mais informações sobre Olá CLI do Azure, consulte Olá [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f82c1-223">For more information about hello Azure CLI, see hello [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>
* <span data-ttu-id="f82c1-224">Para saber mais sobre recursos do Lote, consulte [Visão geral do Lote do Azure para desenvolvedores](batch-api-basics.md).</span><span class="sxs-lookup"><span data-stu-id="f82c1-224">For more information about Batch resources, see [Overview of Azure Batch for developers](batch-api-basics.md).</span></span>
* <span data-ttu-id="f82c1-225">Para obter mais informações sobre como usar pools de toocreate modelos, trabalhos e tarefas em lotes sem escrever código, consulte [usar modelos de CLI de lote do Azure e transferência de arquivos (visualização)](batch-cli-templates.md).</span><span class="sxs-lookup"><span data-stu-id="f82c1-225">For more information about using Batch templates toocreate pools, jobs, and tasks without writing code, see [Use Azure Batch CLI Templates and File Transfer (Preview)](batch-cli-templates.md).</span></span>

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
