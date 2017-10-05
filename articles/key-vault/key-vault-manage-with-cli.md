---
title: Gerenciar Azure Key Vault usando CLI | Microsoft Docs
description: Use este tutorial para automatizar tarefas comuns no Cofre da Chave usando a CLI
services: key-vault
documentationcenter: 
author: BrucePerlerMS
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 66be6e44-684a-411b-802e-884628458ae7
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: bruceper
ms.openlocfilehash: c2565a742ce4f6ab5f7639a54c4a475f00cbc260
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli"></a><span data-ttu-id="c3976-103">Gerenciar Cofre da Chave usando a CLI</span><span class="sxs-lookup"><span data-stu-id="c3976-103">Manage Key Vault using CLI</span></span>

<span data-ttu-id="c3976-104">O Cofre da Chave do Azure está disponível na maioria das regiões.</span><span class="sxs-lookup"><span data-stu-id="c3976-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="c3976-105">Para obter mais informações, consulte a [Página de preços do Cofre da Chave](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="c3976-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="c3976-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="c3976-106">Introduction</span></span>

<span data-ttu-id="c3976-107">Use este tutorial para ajudá-lo a começar a usar o Cofre da Chave do Azure para criar um contêiner de proteção avançado (um cofre) no Azure, para armazenar e gerenciar chaves de criptografia e segredos no Azure.</span><span class="sxs-lookup"><span data-stu-id="c3976-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="c3976-108">Ele mostra o passo a passo do processo de uso da interface de linha de comando de plataforma cruzada do Azure para criar um cofre que contém uma chave ou senha que você pode usar com um aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3976-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="c3976-109">Em seguida, ele mostra como um aplicativo pode usar essa chave ou senha.</span><span class="sxs-lookup"><span data-stu-id="c3976-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="c3976-110">**Tempo estimado para conclusão:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="c3976-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="c3976-111">Este tutorial não inclui instruções sobre como escrever o aplicativo do Azure incluído em uma das etapas, que mostra como autorizar um aplicativo a usar uma chave ou um segredo do cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="c3976-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
> 
> <span data-ttu-id="c3976-112">No momento, não é possível configurar o Cofre da Chave do Azure no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3976-112">Currently, you cannot configure Azure Key Vault in the Azure portal.</span></span> <span data-ttu-id="c3976-113">Em vez disso, use as instruções da Interface de Linha de Comando de Plataforma Cruzada do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3976-113">Instead, use these Cross-Platform Command-Line Interface  instructions.</span></span> <span data-ttu-id="c3976-114">Ou, para obter instruções do PowerShell do Azure, consulte [este tutorial equivalente](key-vault-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c3976-114">Or, for Azure PowerShell instructions, see [this equivalent tutorial](key-vault-get-started.md).</span></span>
> 
> 

<span data-ttu-id="c3976-115">Para obter informações gerais sobre o Cofre da Chave do Azure, consulte [O que é o Cofre da Chave do Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="c3976-115">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3976-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c3976-116">Prerequisites</span></span>

<span data-ttu-id="c3976-117">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="c3976-117">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="c3976-118">Uma assinatura do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c3976-118">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="c3976-119">Se não tiver uma assinatura, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="c3976-119">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="c3976-120">Interface de Linha de Comando versão 0.9.1 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="c3976-120">Command-Line Interface version 0.9.1 or later.</span></span> <span data-ttu-id="c3976-121">Para instalar a versão mais recente e conectá-la à sua assinatura do Azure, consulte [Instalar e configurar a interface de linha de comando entre plataformas do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c3976-121">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>
* <span data-ttu-id="c3976-122">Um aplicativo que será configurado para usar a chave ou senha que você criará neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="c3976-122">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="c3976-123">Um aplicativo de exemplo está disponível no [Centro de Download da Microsoft](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="c3976-123">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="c3976-124">Para obter instruções, consulte o arquivo Leiame.</span><span class="sxs-lookup"><span data-stu-id="c3976-124">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="c3976-125">Obtendo ajuda com a interface de linha de comando de plataforma cruzada do Azure</span><span class="sxs-lookup"><span data-stu-id="c3976-125">Getting help with Azure Cross-Platform Command-Line Interface</span></span>

<span data-ttu-id="c3976-126">Este tutorial pressupõe que você esteja familiarizado com a interface de linha de comando (Bash, Terminal, Prompt de Comando)</span><span class="sxs-lookup"><span data-stu-id="c3976-126">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="c3976-127">O parâmetro --help ou -h pode ser usado para exibir a ajuda de comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="c3976-127">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="c3976-128">Como alternativa, o formato azure help [comando] [opções] também pode ser usado para retornar as mesmas informações.</span><span class="sxs-lookup"><span data-stu-id="c3976-128">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="c3976-129">Por exemplo, todos os seguintes comandos retornam as mesmas informações:</span><span class="sxs-lookup"><span data-stu-id="c3976-129">For example, the following commands all return the same information:</span></span>

    azure account set --help

    azure account set -h

    azure help account set

<span data-ttu-id="c3976-130">Em caso de dúvida sobre os parâmetros necessários para um comando, consulte a Ajuda usando --help, -h ou azure help [comando].</span><span class="sxs-lookup"><span data-stu-id="c3976-130">When in doubt about the parameters needed by a command, refer to help using --help, -h or azure help [command].</span></span>

<span data-ttu-id="c3976-131">Você pode ler também os tutoriais a seguir para se familiarizar com o Gerenciador de Recursos do Azure na interface de linha de comando da plataforma cruzada do Azure:</span><span class="sxs-lookup"><span data-stu-id="c3976-131">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="c3976-132">Como Instalar e configurar a interface de linha de comando de plataforma cruzada do Azure</span><span class="sxs-lookup"><span data-stu-id="c3976-132">How to install and configure Azure Cross-Platform Command Line Interface</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="c3976-133">Usando a interface de linha de comando de plataforma cruzada do Azure com o Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="c3976-133">Using Azure Cross-Platform Command-Line Interface with Azure Resource Manager</span></span>](../xplat-cli-azure-resource-manager.md)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="c3976-134">Conectar-se às suas assinaturas</span><span class="sxs-lookup"><span data-stu-id="c3976-134">Connect to your subscriptions</span></span>

<span data-ttu-id="c3976-135">Para fazer logon usando uma conta institucional, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c3976-135">To log in using an organizational account, use the following command:</span></span>

    azure login -u username -p password

<span data-ttu-id="c3976-136">ou se deseja fazer logon digitando interativamente</span><span class="sxs-lookup"><span data-stu-id="c3976-136">or if you want to log in by typing interactively</span></span>

    azure login

> [!NOTE]
> <span data-ttu-id="c3976-137">O método de logon só funciona com contas institucionais.</span><span class="sxs-lookup"><span data-stu-id="c3976-137">The login method only works with organizational account.</span></span> <span data-ttu-id="c3976-138">Uma conta institucional é um usuário gerenciado pela organização e definido no locatário do Active Directory do Azure da organização.</span><span class="sxs-lookup"><span data-stu-id="c3976-138">An organizational account is a user that is managed by your organization, and defined in your organization's Azure Active Directory tenant.</span></span>
> 
> 

<span data-ttu-id="c3976-139">Se não tiver uma conta institucional e estiver usando uma conta da Microsoft para fazer logon na assinatura do Azure, você poderá criar facilmente uma usando as etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="c3976-139">If you do not currently have an organizational account, and are using a Microsoft account to log in to your Azure subscription, you can easily create one using the following steps.</span></span>

1. <span data-ttu-id="c3976-140">Faça logon no [Portal de Gerenciamento do Azure](https://manage.windowsazure.com/)e clique em Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c3976-140">Login to the Login to the [Azure Management Portal](https://manage.windowsazure.com/), and click on Active Directory.</span></span>
2. <span data-ttu-id="c3976-141">Se não houver diretório, selecione Criar o diretório e forneça as informações solicitadas.</span><span class="sxs-lookup"><span data-stu-id="c3976-141">If no directory exists, select Create your directory and provide the requested information.</span></span>
3. <span data-ttu-id="c3976-142">Selecione o diretório e adicione um novo usuário.</span><span class="sxs-lookup"><span data-stu-id="c3976-142">Select your directory and add a new user.</span></span> <span data-ttu-id="c3976-143">Esse novo usuário é uma conta institucional.</span><span class="sxs-lookup"><span data-stu-id="c3976-143">This new user is an organizational account.</span></span> <span data-ttu-id="c3976-144">Durante a criação do usuário, você receberá um endereço de email para o usuário e uma senha temporária.</span><span class="sxs-lookup"><span data-stu-id="c3976-144">During the creation of the user, you will be supplied with both an e-mail address for the user and a temporary password.</span></span> <span data-ttu-id="c3976-145">Salve essas informações como elas são usadas em outra etapa.</span><span class="sxs-lookup"><span data-stu-id="c3976-145">Save this information as it is used in another step.</span></span>
4. <span data-ttu-id="c3976-146">No portal, selecione Configurações e Administradores.</span><span class="sxs-lookup"><span data-stu-id="c3976-146">From the portal, select Settings and then select Administrators.</span></span> <span data-ttu-id="c3976-147">Selecione Adicionar e adicione o novo usuário como um coadministrador.</span><span class="sxs-lookup"><span data-stu-id="c3976-147">Select Add, and add the new user as a co-administrator.</span></span> <span data-ttu-id="c3976-148">Isso permite que a conta institucional gerencie a assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3976-148">This allows the organizational account to manage your Azure subscription.</span></span>
5. <span data-ttu-id="c3976-149">Por fim, faça logoff do portal do Azure e refaça logon usando a nova conta institucional.</span><span class="sxs-lookup"><span data-stu-id="c3976-149">Finally, log out of the Azure portal and then log back in using the new organizational account.</span></span> <span data-ttu-id="c3976-150">Se este for o primeiro logon usando essa conta, você deverá alterar a senha.</span><span class="sxs-lookup"><span data-stu-id="c3976-150">If this is the first time logging in with this account, you will be prompted to change the password.</span></span>

<span data-ttu-id="c3976-151">Para obter mais informações sobre como usar contas institucionais no Microsoft Azure, consulte [Inscrever-se no Microsoft Azure como uma organização](../active-directory/sign-up-organization.md).</span><span class="sxs-lookup"><span data-stu-id="c3976-151">For more information about using an organizational account with Microsoft Azure, see [Sign up for Microsoft Azure as an Organization](../active-directory/sign-up-organization.md).</span></span>

<span data-ttu-id="c3976-152">Se você tiver várias assinaturas e quiser especificar uma a ser usada para o Cofre da Chave do Azure, digite o seguinte para ver as assinaturas da sua conta:</span><span class="sxs-lookup"><span data-stu-id="c3976-152">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

    azure account list

<span data-ttu-id="c3976-153">Depois, para especificar a assinatura a ser usada, digite:</span><span class="sxs-lookup"><span data-stu-id="c3976-153">Then, to specify the subscription to use, type:</span></span>

    azure account set <subscription name>

<span data-ttu-id="c3976-154">Para obter mais informações sobre como configurar a interface de linha de comando de plataforma cruzada do Azure, consulte [Como instalar e configurar a interface de linha de comando entre plataformas do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="c3976-154">For more information about configuring Azure Cross-Platform Command-Line Interface, see [How to Install and Configure Azure Cross-Platform Command-Line Interface](../cli-install-nodejs.md).</span></span>

## <a name="switch-to-using-azure-resource-manager"></a><span data-ttu-id="c3976-155">Alternar para o Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="c3976-155">Switch to using Azure Resource Manager</span></span>
<span data-ttu-id="c3976-156">O Cofre da Chave requer o Gerenciador de Recursos do Azure. Por isso, digite o seguinte para alternar para o modo do Gerenciador de Recursos do Azure:</span><span class="sxs-lookup"><span data-stu-id="c3976-156">The Key Vault requires Azure Resource Manager, so type the following to switch to Azure Resource Manager mode:</span></span>

    azure config mode arm

## <a name="create-a-new-resource-group"></a><span data-ttu-id="c3976-157">Criar um novo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="c3976-157">Create a new resource group</span></span>
<span data-ttu-id="c3976-158">Ao usar o Gerenciador de Recursos do Azure, todos os recursos relacionados são criados em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="c3976-158">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="c3976-159">Criaremos um novo grupo de recursos “ContosoResourceGroup” para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="c3976-159">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

    azure group create 'ContosoResourceGroup' 'East Asia'

<span data-ttu-id="c3976-160">O primeiro parâmetro é o nome do grupo de recursos e o segundo parâmetro é o local.</span><span class="sxs-lookup"><span data-stu-id="c3976-160">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="c3976-161">Para o local, use o comando `azure location list` para identificar como especificar um local alternativo ao deste exemplo.</span><span class="sxs-lookup"><span data-stu-id="c3976-161">For location, use the command `azure location list` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="c3976-162">Se precisar de mais informações, digite: `azure help location`</span><span class="sxs-lookup"><span data-stu-id="c3976-162">If you need more information, type: `azure help location`</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="c3976-163">Registrar o provedor de recursos do Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="c3976-163">Register the Key Vault resource provider</span></span>
<span data-ttu-id="c3976-164">Verifique se o provedor de recursos do Cofre de Chaves está registrado em sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="c3976-164">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

`azure provider register Microsoft.KeyVault`

<span data-ttu-id="c3976-165">Isso só precisa ser feito uma vez por assinatura.</span><span class="sxs-lookup"><span data-stu-id="c3976-165">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="c3976-166">Criar um cofre de chave</span><span class="sxs-lookup"><span data-stu-id="c3976-166">Create a key vault</span></span>

<span data-ttu-id="c3976-167">Use o comando `azure keyvault create` para criar um cofre de chave.</span><span class="sxs-lookup"><span data-stu-id="c3976-167">Use the `azure keyvault create` command to create a key vault.</span></span> <span data-ttu-id="c3976-168">Esse script tem três parâmetros obrigatórios: um nome do grupo de recursos, um nome do cofre da chave e a localização geográfica.</span><span class="sxs-lookup"><span data-stu-id="c3976-168">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="c3976-169">Por exemplo, se você usar o nome de cofre ContosoKeyVault, o nome do grupo de recursos ContosoResourceGroup e o local Ásia Oriental, digite:</span><span class="sxs-lookup"><span data-stu-id="c3976-169">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>

    azure keyvault create --vault-name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'

<span data-ttu-id="c3976-170">A saída do comando mostra as propriedades do cofre da chave que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="c3976-170">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="c3976-171">As duas propriedades mais importantes são:</span><span class="sxs-lookup"><span data-stu-id="c3976-171">The two most important properties are:</span></span>

* <span data-ttu-id="c3976-172">**Name**: no exemplo, é ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="c3976-172">**Name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="c3976-173">Você usará esse nome para outros cmdlets do Cofre da Chave.</span><span class="sxs-lookup"><span data-stu-id="c3976-173">You will use this name for other Key Vault cmdlets.</span></span>
* <span data-ttu-id="c3976-174">**vaultUri**: no exemplo, isso é https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="c3976-174">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="c3976-175">Aplicativos que usam seu cofre via API REST devem usar esse URI.</span><span class="sxs-lookup"><span data-stu-id="c3976-175">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="c3976-176">Sua conta do Azure agora está autorizada a executar qualquer operação neste cofre de chave.</span><span class="sxs-lookup"><span data-stu-id="c3976-176">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="c3976-177">Até o momento, ninguém mais está.</span><span class="sxs-lookup"><span data-stu-id="c3976-177">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="c3976-178">Adicionar uma chave ou segredo ao cofre da chave</span><span class="sxs-lookup"><span data-stu-id="c3976-178">Add a key or secret to the key vault</span></span>

<span data-ttu-id="c3976-179">Se você quiser que o Cofre da Chave do Azure crie uma chave protegida por software para você, use o comando `azure key create` e digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c3976-179">If you want Azure Key Vault to create a software-protected key for you, use the `azure key create` command, and type the following:</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --destination software

<span data-ttu-id="c3976-180">No entanto, se você tiver uma chave existente em um arquivo PEM salvo como arquivo local em um arquivo chamado softkey.pem que você deseja carregar no Cofre da Chave do Azure, digite o seguinte para importar a chave do arquivo PEM, o qual protege a chave pelo software no serviço de Cofre da Chave:</span><span class="sxs-lookup"><span data-stu-id="c3976-180">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey' --pem-file './softkey.pem' --password 'PaSSWORD' --destination software

<span data-ttu-id="c3976-181">Agora você pode fazer referência à chave que criada ou carregada no Cofre da Chave do Azure, usando o URI.</span><span class="sxs-lookup"><span data-stu-id="c3976-181">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="c3976-182">Use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** para sempre obter a versão atual e use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** para obter esta versão específica.</span><span class="sxs-lookup"><span data-stu-id="c3976-182">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="c3976-183">Para adicionar um segredo ao cofre, que é uma senha chamada SQLPassword e que tem o valor Pa$$w0rd no Cofre da Chave do Azure, digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c3976-183">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>

    azure keyvault secret set --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword' --value 'Pa$$w0rd'

<span data-ttu-id="c3976-184">Agora, você pode fazer referência a essa senha que foi adicionada ao Cofre da Chave do Azure usando seu URI.</span><span class="sxs-lookup"><span data-stu-id="c3976-184">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="c3976-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** para sempre obter a versão atual e use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** para obter esta versão específica.</span><span class="sxs-lookup"><span data-stu-id="c3976-185">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="c3976-186">Vamos exibir a chave ou o segredo que você acabou de criar:</span><span class="sxs-lookup"><span data-stu-id="c3976-186">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="c3976-187">Para exibir a chave, digite: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="c3976-187">To view your key, type: `azure keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="c3976-188">Para exibir o segredo, digite: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="c3976-188">To view your secret, type: `azure keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="c3976-189">Registrar um aplicativo com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="c3976-189">Register an application with Azure Active Directory</span></span>

<span data-ttu-id="c3976-190">Esta etapa geralmente seria feita por um desenvolvedor, em um computador separado.</span><span class="sxs-lookup"><span data-stu-id="c3976-190">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="c3976-191">Ela não é específica ao Cofre da Chave do Azure, mas é incluída aqui para que as informações fiquem completas.</span><span class="sxs-lookup"><span data-stu-id="c3976-191">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c3976-192">Para concluir o tutorial, sua conta, o cofre e o aplicativo que você registrará nesta etapa devem todos estar no mesmo diretório do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3976-192">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
> 
> 

<span data-ttu-id="c3976-193">Aplicativos que usam um cofre de chave devem ser autenticados usando um token do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3976-193">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="c3976-194">Para fazer isso, o proprietário do aplicativo deve primeiro registrar o aplicativo no seu Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3976-194">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="c3976-195">No final do registro, o proprietário do aplicativo obtém os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="c3976-195">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="c3976-196">Uma **ID do Aplicativo** (também conhecida como ID do Cliente) e a **chave de autenticação** (também conhecida como segredo compartilhado).</span><span class="sxs-lookup"><span data-stu-id="c3976-196">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="c3976-197">O aplicativo deve apresentar esses dois valores ao Active Directory do Azure para obter um token.</span><span class="sxs-lookup"><span data-stu-id="c3976-197">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="c3976-198">Como o aplicativo é configurado para fazer isso depende do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c3976-198">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="c3976-199">Para o aplicativo de exemplo do Cofre da Chave, o proprietário do aplicativo define esses valores no arquivo app.config.</span><span class="sxs-lookup"><span data-stu-id="c3976-199">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="c3976-200">Para registrar seu aplicativo com o Active Directory do Azure:</span><span class="sxs-lookup"><span data-stu-id="c3976-200">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="c3976-201">Entre no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3976-201">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="c3976-202">À esquerda, clique em **Active Directory**e selecione o diretório no qual você registrará o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c3976-202">On the left, click **Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

>[!NOTE] 
> <span data-ttu-id="c3976-203">Você deve selecionar o mesmo diretório que contém a assinatura do Azure com a qual você criou o cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="c3976-203">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="c3976-204">Se você não souber qual é o diretório, clique em **Configurações**, identifique a assinatura com a qual você criou o cofre de chave e anote o nome do diretório exibido na última coluna.</span><span class="sxs-lookup"><span data-stu-id="c3976-204">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="c3976-205">Clique em **APLICATIVOS**.</span><span class="sxs-lookup"><span data-stu-id="c3976-205">Click **APPLICATIONS**.</span></span> <span data-ttu-id="c3976-206">Se nenhum aplicativo tiver sido adicionado ao seu diretório, essa página mostrará somente o link **Adicionar um Aplicativo** .</span><span class="sxs-lookup"><span data-stu-id="c3976-206">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="c3976-207">Clique no link ou em **ADICIONAR** na barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="c3976-207">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="c3976-208">No assistente **ADICIONAR APLICATIVO** na página **O que você deseja fazer?**, clique em **Adicionar um aplicativo que minha organização está desenvolvendo**.</span><span class="sxs-lookup"><span data-stu-id="c3976-208">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="c3976-209">Na página **Conte-nos sobre seu aplicativo**, especifique um nome para seu aplicativo e selecione **APLICATIVO WEB E/OU API WEB** (o padrão).</span><span class="sxs-lookup"><span data-stu-id="c3976-209">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="c3976-210">Clique no ícone Avançar.</span><span class="sxs-lookup"><span data-stu-id="c3976-210">Click the Next icon.</span></span>
6. <span data-ttu-id="c3976-211">Na página **Propriedades do aplicativo**, especifique a **URL DE LOGON** e o **URI DA ID DO aplicativo** para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="c3976-211">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="c3976-212">Se seu aplicativo não tiver esses valores, você pode inventá-los para esta etapa (por exemplo, você poderia especificar http://test1.contoso.com para as duas caixas).</span><span class="sxs-lookup"><span data-stu-id="c3976-212">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="c3976-213">Não importa se os sites existem, o importante é que o URI de ID de cada aplicativo é diferente para todos os aplicativos no diretório.</span><span class="sxs-lookup"><span data-stu-id="c3976-213">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="c3976-214">O diretório usa essa cadeia de caracteres para identificar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c3976-214">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="c3976-215">Clique no ícone Concluído para salvar suas alterações no assistente.</span><span class="sxs-lookup"><span data-stu-id="c3976-215">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="c3976-216">Na página de Início Rápido, clique em **CONFIGURAR**.</span><span class="sxs-lookup"><span data-stu-id="c3976-216">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="c3976-217">Role até a seção **chaves**, selecione a duração, em seguida, clique em **SALVAR**.</span><span class="sxs-lookup"><span data-stu-id="c3976-217">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="c3976-218">A página é atualizada e passa a mostrar um valor de chave.</span><span class="sxs-lookup"><span data-stu-id="c3976-218">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="c3976-219">Você deve configurar seu aplicativo com esse valor de chave e o valor da **ID DO CLIENTE** .</span><span class="sxs-lookup"><span data-stu-id="c3976-219">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="c3976-220">(As instruções para esta configuração são específicas do aplicativo).</span><span class="sxs-lookup"><span data-stu-id="c3976-220">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="c3976-221">Copie o valor da ID do cliente desta página, que você usará na próxima etapa para definir as permissões no cofre.</span><span class="sxs-lookup"><span data-stu-id="c3976-221">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="c3976-222">Autorizar o aplicativo a usar a chave ou o segredo</span><span class="sxs-lookup"><span data-stu-id="c3976-222">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="c3976-223">Para autorizar o aplicativo a acessar a chave ou o segredo no cofre, use o comando `azure keyvault set-policy`.</span><span class="sxs-lookup"><span data-stu-id="c3976-223">To authorize the application to access the key or secret in the vault, use the `azure keyvault set-policy` command.</span></span>

<span data-ttu-id="c3976-224">Por exemplo, se o nome do cofre for ContosoKeyVault e o aplicativo que você quer autorizar tiver a ID de cliente 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, e você quiser autorizar o aplicativo a descriptografar e assinar com chaves em seu cofre. Em seguida, execute o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c3976-224">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-keys '[\"decrypt\",\"sign\"]'

> [!NOTE]
> <span data-ttu-id="c3976-225">Se você estiver executando no prompt de comando do Windows, será necessário substituir aspas por aspas duplas e também inserir escape nas aspas duplas internas.</span><span class="sxs-lookup"><span data-stu-id="c3976-225">If you are running on Windows command prompt, you should replace single quotes with double quotes, and also escape the internal double quotes.</span></span> <span data-ttu-id="c3976-226">Por exemplo: "[\"decrypt\",\"sign\"]".</span><span class="sxs-lookup"><span data-stu-id="c3976-226">For example: "[\"decrypt\",\"sign\"]".</span></span>
> 
> 

<span data-ttu-id="c3976-227">Se você deseja autorizar que o mesmo aplicativo leia segredos em seu cofre, execute o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c3976-227">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>

    azure keyvault set-policy --vault-name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --perms-to-secrets '[\"get\"]'

## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="c3976-228">Se quiser usar um HSM (módulo de segurança de hardware)</span><span class="sxs-lookup"><span data-stu-id="c3976-228">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="c3976-229">Para garantia extra, você pode importar ou gerar chaves em HSMs (módulos de segurança de hardware) que nunca deixam os limites do HSM.</span><span class="sxs-lookup"><span data-stu-id="c3976-229">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="c3976-230">Os HSMs têm certificação FIPS 140-2 Nível 2.</span><span class="sxs-lookup"><span data-stu-id="c3976-230">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="c3976-231">Se esse requisito não se aplicar a você, ignore esta seção e vá para [Excluir o cofre de chave e chaves e segredos associados](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="c3976-231">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="c3976-232">Para criar essas chaves protegidas por HSM, você deve ter uma assinatura de cofre que dê suporte a chaves protegidas por HSM.</span><span class="sxs-lookup"><span data-stu-id="c3976-232">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="c3976-233">Ao criar o keyvault, adicione o parâmetro "SKU":</span><span class="sxs-lookup"><span data-stu-id="c3976-233">When you create the keyvault, add the 'sku' parameter:</span></span>

    azure azure keyvault create --vault-name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'

<span data-ttu-id="c3976-234">Você pode adicionar chaves protegidas por software (conforme mostrado anteriormente) e por HSM a este cofre.</span><span class="sxs-lookup"><span data-stu-id="c3976-234">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="c3976-235">Para criar uma chave protegida por HSM, defina o parâmetro de Destino como “HSM”:</span><span class="sxs-lookup"><span data-stu-id="c3976-235">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

    azure keyvault key create --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --destination 'HSM'

<span data-ttu-id="c3976-236">Você pode usar o comando a seguir para importar uma chave de um arquivo PEM para seu computador.</span><span class="sxs-lookup"><span data-stu-id="c3976-236">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="c3976-237">Esse comando importa a chave para os HSMs no serviço de Cofre da Chave:</span><span class="sxs-lookup"><span data-stu-id="c3976-237">This command imports the key into HSMs in the Key Vault service:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --destination 'HSM' --password 'PaSSWORD'

<span data-ttu-id="c3976-238">O próximo comando importa um pacote de BYOK ("traga sua própria chave").</span><span class="sxs-lookup"><span data-stu-id="c3976-238">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="c3976-239">Isso permite gerar sua chave no HSM local e transferi-la para os HSMs no serviço de Cofre da Chave, sem que a chave deixe os limites do HSM:</span><span class="sxs-lookup"><span data-stu-id="c3976-239">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

    azure keyvault key import --vault-name 'ContosoKeyVaultHSM' --key-name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --destination 'HSM'

<span data-ttu-id="c3976-240">Para obter instruções mais detalhadas sobre como gerar esse pacote de BYOK, consulte [Como usar Chaves Protegidas por HSM com o Cofre da Chave do Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="c3976-240">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="c3976-241">Excluir o cofre de chave e chaves e segredos associados</span><span class="sxs-lookup"><span data-stu-id="c3976-241">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="c3976-242">Se não precisar mais do cofre da chave e da chave ou do segredo contido nele, você pode excluir o cofre da chave usando o comando keyvault delete:</span><span class="sxs-lookup"><span data-stu-id="c3976-242">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the azure keyvault delete command:</span></span>

    azure keyvault delete --vault-name 'ContosoKeyVault'

<span data-ttu-id="c3976-243">Ou você pode excluir um grupo de recursos do Azure inteiro, que inclui o cofre de chave e quaisquer outros recursos incluídos nesse grupo:</span><span class="sxs-lookup"><span data-stu-id="c3976-243">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

    azure group delete --name 'ContosoResourceGroup'


## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="c3976-244">Outros comandos da interface de linha de comando de plataforma cruzada do Azure</span><span class="sxs-lookup"><span data-stu-id="c3976-244">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="c3976-245">Outros comandos que podem ser úteis para gerenciar o Cofre da Chave do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3976-245">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="c3976-246">Este comando lista uma exibição em tabela de todas as chaves e propriedades selecionadas:</span><span class="sxs-lookup"><span data-stu-id="c3976-246">This command lists a tabular display of all keys and selected properties:</span></span>

    azure keyvault key list --vault-name 'ContosoKeyVault'

<span data-ttu-id="c3976-247">Este comando exibe uma lista completa de propriedades para a chave especificada:</span><span class="sxs-lookup"><span data-stu-id="c3976-247">This command displays a full list of properties for the specified key:</span></span>

    azure keyvault key show --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="c3976-248">Este comando lista uma exibição em tabela de todos os nomes de segredos e propriedades selecionadas:</span><span class="sxs-lookup"><span data-stu-id="c3976-248">This command lists a tabular display of all secret names and selected properties:</span></span>

    azure keyvault secret list --vault-name 'ContosoKeyVault'

<span data-ttu-id="c3976-249">Aqui está um exemplo de como remover uma chave específica:</span><span class="sxs-lookup"><span data-stu-id="c3976-249">Here's an example of how to remove a specific key:</span></span>

    azure keyvault key delete --vault-name 'ContosoKeyVault' --key-name 'ContosoFirstKey'

<span data-ttu-id="c3976-250">Aqui está um exemplo de como remover um segredo específica:</span><span class="sxs-lookup"><span data-stu-id="c3976-250">Here's an example of how to remove a specific secret:</span></span>

    azure keyvault secret delete --vault-name 'ContosoKeyVault' --secret-name 'SQLPassword'


## <a name="next-steps"></a><span data-ttu-id="c3976-251">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c3976-251">Next steps</span></span>
<span data-ttu-id="c3976-252">Para referências de programação, consulte [Guia do desenvolvedor do Cofre da Chave do Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="c3976-252">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>

