---
title: Gerenciar Azure Key Vault usando CLI | Microsoft Docs
description: Use este tutorial para automatizar tarefas comuns no Key Vault usando a CLI 2.0
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 5da9f5eceda71ac85259193e0f183c72813e1679
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="6a2e0-103">Gerenciar o Key Vault usando a CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="6a2e0-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="6a2e0-104">O Cofre da Chave do Azure está disponível na maioria das regiões.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="6a2e0-105">Para obter mais informações, consulte a [Página de preços do Cofre da Chave](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="6a2e0-105">For more information, see the [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="6a2e0-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="6a2e0-106">Introduction</span></span>
<span data-ttu-id="6a2e0-107">Use este tutorial para ajudá-lo a começar a usar o Cofre da Chave do Azure para criar um contêiner de proteção avançado (um cofre) no Azure, para armazenar e gerenciar chaves de criptografia e segredos no Azure.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-107">Use this tutorial to help you get started with Azure Key Vault to create a hardened container (a vault) in Azure, to store and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="6a2e0-108">Ele mostra o passo a passo do processo de uso da interface de linha de comando de plataforma cruzada do Azure para criar um cofre que contém uma chave ou senha que você pode usar com um aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-108">It walks you through the process of using Azure Cross-Platform Command-Line Interface to create a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="6a2e0-109">Em seguida, ele mostra como um aplicativo pode usar essa chave ou senha.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="6a2e0-110">**Tempo estimado para conclusão:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="6a2e0-110">**Estimated time to complete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="6a2e0-111">Este tutorial não inclui instruções sobre como escrever o aplicativo do Azure incluído em uma das etapas, que mostra como autorizar um aplicativo a usar uma chave ou um segredo do cofre da chave.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-111">This tutorial does not include instructions on how to write the Azure application that one of the steps includes, which shows how to authorize an application to use a key or secret in the key vault.</span></span>
>
> <span data-ttu-id="6a2e0-112">Este tutorial usa a última CLI 2.0 do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-112">This tutorial uses the latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="6a2e0-113">Para obter informações gerais sobre o Cofre da Chave do Azure, consulte [O que é o Cofre da Chave do Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="6a2e0-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6a2e0-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6a2e0-114">Prerequisites</span></span>
<span data-ttu-id="6a2e0-115">Para concluir este tutorial, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-115">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="6a2e0-116">Uma assinatura do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-116">A subscription to Microsoft Azure.</span></span> <span data-ttu-id="6a2e0-117">Se não tiver uma assinatura, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="6a2e0-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="6a2e0-118">Interface de Linha de Comando versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="6a2e0-119">Para instalar a última versão e conectá-la à sua assinatura do Azure, consulte [Instalar e configurar a Interface de Linha de Comando 2.0 de plataforma cruzada do Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6a2e0-119">To install the latest version and connect to your Azure subscription, see [Install and Configure the Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="6a2e0-120">Um aplicativo que será configurado para usar a chave ou senha que você criará neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-120">An application that will be configured to use the key or password that you create in this tutorial.</span></span> <span data-ttu-id="6a2e0-121">Um aplicativo de exemplo está disponível no [Centro de Download da Microsoft](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="6a2e0-121">A sample application is available from the [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="6a2e0-122">Para obter instruções, consulte o arquivo Leiame.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-122">For instructions, see the accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="6a2e0-123">Obtendo ajuda com a interface de linha de comando de plataforma cruzada do Azure</span><span class="sxs-lookup"><span data-stu-id="6a2e0-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="6a2e0-124">Este tutorial pressupõe que você esteja familiarizado com a interface de linha de comando (Bash, Terminal, Prompt de Comando)</span><span class="sxs-lookup"><span data-stu-id="6a2e0-124">This tutorial assumes that you are familiar with the command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="6a2e0-125">O parâmetro --help ou -h pode ser usado para exibir a ajuda de comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-125">The --help or -h parameter can be used to view help for specific commands.</span></span> <span data-ttu-id="6a2e0-126">Como alternativa, o formato azure help [comando] [opções] também pode ser usado para retornar as mesmas informações.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-126">Alternately, The azure help [command] [options] format can also be used to return the same information.</span></span> <span data-ttu-id="6a2e0-127">Por exemplo, todos os seguintes comandos retornam as mesmas informações:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-127">For example, the following commands all return the same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="6a2e0-128">Em caso de dúvida sobre os parâmetros necessários para um comando, consulte a ajuda usando --help, -h ou az help [comando].</span><span class="sxs-lookup"><span data-stu-id="6a2e0-128">When in doubt about the parameters needed by a command, refer to help using --help, -h or az help [command].</span></span>

<span data-ttu-id="6a2e0-129">Você pode ler também os tutoriais a seguir para se familiarizar com o Gerenciador de Recursos do Azure na interface de linha de comando da plataforma cruzada do Azure:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-129">You can also read the following tutorials to get familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="6a2e0-130">Instalar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="6a2e0-131">Introdução à CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="6a2e0-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-to-your-subscriptions"></a><span data-ttu-id="6a2e0-132">Conectar-se às suas assinaturas</span><span class="sxs-lookup"><span data-stu-id="6a2e0-132">Connect to your subscriptions</span></span>
<span data-ttu-id="6a2e0-133">Para fazer logon usando uma conta institucional, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-133">To log in using an organizational account, use the following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="6a2e0-134">ou se deseja fazer logon digitando interativamente</span><span class="sxs-lookup"><span data-stu-id="6a2e0-134">or if you want to log in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="6a2e0-135">Se você tiver várias assinaturas e quiser especificar uma a ser usada para o Cofre da Chave do Azure, digite o seguinte para ver as assinaturas da sua conta:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-135">If you have multiple subscriptions and want to specify a specific one to use for Azure Key Vault, type the following to see the subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="6a2e0-136">Depois, para especificar a assinatura a ser usada, digite:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-136">Then, to specify the subscription to use, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="6a2e0-137">Para obter mais informações sobre como configurar a Interface de Linha de Comando de plataforma cruzada do Azure, consulte [Instalar a CLI do Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6a2e0-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="6a2e0-138">Criar um novo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6a2e0-138">Create a new resource group</span></span>
<span data-ttu-id="6a2e0-139">Ao usar o Gerenciador de Recursos do Azure, todos os recursos relacionados são criados em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="6a2e0-140">Criaremos um novo grupo de recursos “ContosoResourceGroup” para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="6a2e0-141">O primeiro parâmetro é o nome do grupo de recursos e o segundo parâmetro é o local.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-141">The first parameter is resource group name and the second parameter is the location.</span></span> <span data-ttu-id="6a2e0-142">Para o local, use o comando `az account list-locations` para identificar como especificar um local alternativo ao deste exemplo.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-142">For location, use the command `az account list-locations` to identify how to specify an alternative location to the one in this example.</span></span> <span data-ttu-id="6a2e0-143">Se precisar de mais informações, digite: `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-the-key-vault-resource-provider"></a><span data-ttu-id="6a2e0-144">Registrar o provedor de recursos do Cofre de Chaves</span><span class="sxs-lookup"><span data-stu-id="6a2e0-144">Register the Key Vault resource provider</span></span>
<span data-ttu-id="6a2e0-145">Verifique se o provedor de recursos do Cofre de Chaves está registrado em sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="6a2e0-146">Isso só precisa ser feito uma vez por assinatura.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-146">This only needs to be done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="6a2e0-147">Criar um cofre de chave</span><span class="sxs-lookup"><span data-stu-id="6a2e0-147">Create a key vault</span></span>
<span data-ttu-id="6a2e0-148">Use o comando `az keyvault create` para criar um cofre de chave.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-148">Use the `az keyvault create` command to create a key vault.</span></span> <span data-ttu-id="6a2e0-149">Esse script tem três parâmetros obrigatórios: um nome do grupo de recursos, um nome do cofre da chave e a localização geográfica.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-149">This script has three mandatory parameters: a resource group name, a key vault name, and the geographic location.</span></span>

<span data-ttu-id="6a2e0-150">Por exemplo, se você usar o nome de cofre ContosoKeyVault, o nome do grupo de recursos ContosoResourceGroup e o local Ásia Oriental, digite:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-150">For example, if you use the vault name of ContosoKeyVault, the resource group name of ContosoResourceGroup, and the location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="6a2e0-151">A saída do comando mostra as propriedades do cofre da chave que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-151">The output of this command shows properties of the key vault that you've just created.</span></span> <span data-ttu-id="6a2e0-152">As duas propriedades mais importantes são:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-152">The two most important properties are:</span></span>

* <span data-ttu-id="6a2e0-153">**name**: no exemplo, é ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-153">**name**: In the example this is ContosoKeyVault.</span></span> <span data-ttu-id="6a2e0-154">Você usará esse nome para outros comandos do Key Vault.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="6a2e0-155">**vaultUri**: no exemplo, isso é https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-155">**vaultUri**: In the example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="6a2e0-156">Aplicativos que usam seu cofre via API REST devem usar esse URI.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="6a2e0-157">Sua conta do Azure agora está autorizada a executar qualquer operação neste cofre de chave.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-157">Your Azure account is now authorized to perform any operations on this key vault.</span></span> <span data-ttu-id="6a2e0-158">Até o momento, ninguém mais está.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-to-the-key-vault"></a><span data-ttu-id="6a2e0-159">Adicionar uma chave ou segredo ao cofre da chave</span><span class="sxs-lookup"><span data-stu-id="6a2e0-159">Add a key or secret to the key vault</span></span>
<span data-ttu-id="6a2e0-160">Se você quiser que o Cofre da Chave do Azure crie uma chave protegida por software para você, use o comando `az key create` e digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-160">If you want Azure Key Vault to create a software-protected key for you, use the `az key create` command, and type the following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="6a2e0-161">No entanto, se você tiver uma chave existente em um arquivo PEM salvo como arquivo local em um arquivo chamado softkey.pem que você deseja carregar no Cofre da Chave do Azure, digite o seguinte para importar a chave do arquivo PEM, o qual protege a chave pelo software no serviço de Cofre da Chave:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want to upload to Azure Key Vault, type the following to import the key from the .PEM file, which protects the key by software in the Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="6a2e0-162">Agora você pode fazer referência à chave que criada ou carregada no Cofre da Chave do Azure, usando o URI.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-162">You can now reference the key that you created or uploaded to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="6a2e0-163">Use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** para sempre obter a versão atual e use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** para obter esta versão específica.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** to always get the current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** to get this specific version.</span></span>

<span data-ttu-id="6a2e0-164">Para adicionar um segredo ao cofre, que é uma senha chamada SQLPassword e que tem o valor Pa$$w0rd no Cofre da Chave do Azure, digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-164">To add a secret to the vault, which is a password named SQLPassword and that has the value of Pa$$w0rd to Azure Key Vault, type the following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="6a2e0-165">Agora, você pode fazer referência a essa senha que foi adicionada ao Cofre da Chave do Azure usando seu URI.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-165">You can now reference this password that you added to Azure Key Vault, by using its URI.</span></span> <span data-ttu-id="6a2e0-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** para sempre obter a versão atual e use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** para obter esta versão específica.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** to always get the current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** to get this specific version.</span></span>

<span data-ttu-id="6a2e0-167">Vamos exibir a chave ou o segredo que você acabou de criar:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-167">Let's view the key or secret that you just created:</span></span>

* <span data-ttu-id="6a2e0-168">Para exibir a chave, digite: `az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="6a2e0-168">To view your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="6a2e0-169">Para exibir o segredo, digite: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="6a2e0-169">To view your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="6a2e0-170">Registrar um aplicativo com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="6a2e0-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="6a2e0-171">Esta etapa geralmente seria feita por um desenvolvedor, em um computador separado.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="6a2e0-172">Ela não é específica ao Cofre da Chave do Azure, mas é incluída aqui para que as informações fiquem completas.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-172">It is not specific to Azure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6a2e0-173">Para concluir o tutorial, sua conta, o cofre e o aplicativo que você registrará nesta etapa devem todos estar no mesmo diretório do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-173">To complete the tutorial, your account, the vault, and the application that you will register in this step must all be in the same Azure directory.</span></span>
>
>

<span data-ttu-id="6a2e0-174">Aplicativos que usam um cofre de chave devem ser autenticados usando um token do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="6a2e0-175">Para fazer isso, o proprietário do aplicativo deve primeiro registrar o aplicativo no seu Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-175">To do this, the owner of the application must first register the application in their Azure Active Directory.</span></span> <span data-ttu-id="6a2e0-176">No final do registro, o proprietário do aplicativo obtém os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-176">At the end of registration, the application owner gets the following values:</span></span>

* <span data-ttu-id="6a2e0-177">Uma **ID do Aplicativo** (também conhecida como ID do Cliente) e a **chave de autenticação** (também conhecida como segredo compartilhado).</span><span class="sxs-lookup"><span data-stu-id="6a2e0-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as the shared secret).</span></span> <span data-ttu-id="6a2e0-178">O aplicativo deve apresentar esses dois valores ao Active Directory do Azure para obter um token.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-178">The application must present both of these values to Azure Active Directory, to get a token.</span></span> <span data-ttu-id="6a2e0-179">Como o aplicativo é configurado para fazer isso depende do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-179">How the application is configured to do this depends on the application.</span></span> <span data-ttu-id="6a2e0-180">Para o aplicativo de exemplo do Cofre da Chave, o proprietário do aplicativo define esses valores no arquivo app.config.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-180">For the Key Vault sample application, the application owner sets these values in the app.config file.</span></span>

<span data-ttu-id="6a2e0-181">Para registrar seu aplicativo com o Active Directory do Azure:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-181">To register the application in Azure Active Directory:</span></span>

1. <span data-ttu-id="6a2e0-182">Entre no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-182">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="6a2e0-183">À esquerda, clique em **Azure Active Directory** e selecione o diretório no qual você registrará o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-183">On the left, click **Azure Active Directory**, and then select the directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="6a2e0-184">Você deve selecionar o mesmo diretório que contém a assinatura do Azure com a qual você criou o cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-184">You must select the same directory that contains the Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="6a2e0-185">Se você não souber qual é o diretório, clique em **Configurações**, identifique a assinatura com a qual você criou o cofre de chave e anote o nome do diretório exibido na última coluna.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-185">If you do not know which directory this is, click **Settings**, identify the subscription with which you created your key vault, and note the name of the directory displayed in the last column.</span></span>

3. <span data-ttu-id="6a2e0-186">Clique em **APLICATIVOS**.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="6a2e0-187">Se nenhum aplicativo tiver sido adicionado ao seu diretório, essa página mostrará somente o link **Adicionar um Aplicativo** .</span><span class="sxs-lookup"><span data-stu-id="6a2e0-187">If no apps have been added to your directory, this page will show only the **Add an App** link.</span></span> <span data-ttu-id="6a2e0-188">Clique no link ou em **ADICIONAR** na barra de comandos.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-188">Click the link, or alternatively, you can click the **ADD** on the command bar.</span></span>
4. <span data-ttu-id="6a2e0-189">No assistente **ADICIONAR APLICATIVO** na página **O que você deseja fazer?**, clique em **Adicionar um aplicativo que minha organização está desenvolvendo**.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-189">In the **ADD APPLICATION** wizard, on the **What do you want to do?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="6a2e0-190">Na página **Conte-nos sobre seu aplicativo**, especifique um nome para seu aplicativo e selecione **APLICATIVO WEB E/OU API WEB** (o padrão).</span><span class="sxs-lookup"><span data-stu-id="6a2e0-190">On the **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (the default).</span></span> <span data-ttu-id="6a2e0-191">Clique no ícone Avançar.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-191">Click the Next icon.</span></span>
6. <span data-ttu-id="6a2e0-192">Na página **Propriedades do aplicativo**, especifique a **URL DE LOGON** e o **URI DA ID DO aplicativo** para seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-192">On the **App properties** page, specify the **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="6a2e0-193">Se seu aplicativo não tiver esses valores, você pode inventá-los para esta etapa (por exemplo, você poderia especificar http://test1.contoso.com para as duas caixas).</span><span class="sxs-lookup"><span data-stu-id="6a2e0-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="6a2e0-194">Não importa se os sites existem, o importante é que o URI de ID de cada aplicativo é diferente para todos os aplicativos no diretório.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-194">It does not matter if these sites exist; what is important is that the app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="6a2e0-195">O diretório usa essa cadeia de caracteres para identificar seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-195">The directory uses this string to identify your app.</span></span>
7. <span data-ttu-id="6a2e0-196">Clique no ícone Concluído para salvar suas alterações no assistente.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-196">Click the Complete icon to save your changes in the wizard.</span></span>
8. <span data-ttu-id="6a2e0-197">Na página de Início Rápido, clique em **CONFIGURAR**.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-197">On the Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="6a2e0-198">Role até a seção **chaves**, selecione a duração, em seguida, clique em **SALVAR**.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-198">Scroll to the **keys** section, select the duration, and then click **SAVE**.</span></span> <span data-ttu-id="6a2e0-199">A página é atualizada e passa a mostrar um valor de chave.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-199">The page refreshes and now shows a key value.</span></span> <span data-ttu-id="6a2e0-200">Você deve configurar seu aplicativo com esse valor de chave e o valor da **ID DO CLIENTE** .</span><span class="sxs-lookup"><span data-stu-id="6a2e0-200">You must configure your application with this key value and the **CLIENT ID** value.</span></span> <span data-ttu-id="6a2e0-201">(As instruções para esta configuração são específicas do aplicativo).</span><span class="sxs-lookup"><span data-stu-id="6a2e0-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="6a2e0-202">Copie o valor da ID do cliente desta página, que você usará na próxima etapa para definir as permissões no cofre.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-202">Copy the client ID value from this page, which you will use in the next step to set permissions on your vault.</span></span>

## <a name="authorize-the-application-to-use-the-key-or-secret"></a><span data-ttu-id="6a2e0-203">Autorizar o aplicativo a usar a chave ou o segredo</span><span class="sxs-lookup"><span data-stu-id="6a2e0-203">Authorize the application to use the key or secret</span></span>
<span data-ttu-id="6a2e0-204">Para autorizar o aplicativo a acessar a chave ou o segredo no cofre, use o comando `az keyvault set-policy`.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-204">To authorize the application to access the key or secret in the vault, use the `az keyvault set-policy` command.</span></span>

<span data-ttu-id="6a2e0-205">Por exemplo, se o nome do cofre for ContosoKeyVault e o aplicativo que você quer autorizar tiver a ID de cliente 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, e você quiser autorizar o aplicativo a descriptografar e assinar com chaves em seu cofre. Em seguida, execute o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-205">For example, if your vault name is ContosoKeyVault and the application you want to authorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want to authorize the application to decrypt and sign with keys in your vault, then run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="6a2e0-206">Se você deseja autorizar que o mesmo aplicativo leia segredos em seu cofre, execute o seguinte:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-206">If you want to authorize that same application to read secrets in your vault, run the following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-to-use-a-hardware-security-module-hsm"></a><span data-ttu-id="6a2e0-207">Se quiser usar um HSM (módulo de segurança de hardware)</span><span class="sxs-lookup"><span data-stu-id="6a2e0-207">If you want to use a hardware security module (HSM)</span></span>
<span data-ttu-id="6a2e0-208">Para garantia extra, você pode importar ou gerar chaves em HSMs (módulos de segurança de hardware) que nunca deixam os limites do HSM.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave the HSM boundary.</span></span> <span data-ttu-id="6a2e0-209">Os HSMs têm certificação FIPS 140-2 Nível 2.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-209">The HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="6a2e0-210">Se esse requisito não se aplicar a você, ignore esta seção e vá para [Excluir o cofre de chave e chaves e segredos associados](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="6a2e0-210">If this requirement doesn't apply to you, skip this section and go to [Delete the key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="6a2e0-211">Para criar essas chaves protegidas por HSM, você deve ter uma assinatura de cofre que dê suporte a chaves protegidas por HSM.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-211">To create these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="6a2e0-212">Ao criar o keyvault, adicione o parâmetro "SKU":</span><span class="sxs-lookup"><span data-stu-id="6a2e0-212">When you create the keyvault, add the 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="6a2e0-213">Você pode adicionar chaves protegidas por software (conforme mostrado anteriormente) e por HSM a este cofre.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-213">You can add software-protected keys (as shown earlier) and HSM-protected keys to this vault.</span></span> <span data-ttu-id="6a2e0-214">Para criar uma chave protegida por HSM, defina o parâmetro de Destino como “HSM”:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-214">To create an HSM-protected key, set the Destination parameter to 'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="6a2e0-215">Você pode usar o comando a seguir para importar uma chave de um arquivo PEM para seu computador.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-215">You can use the following command to import a key from a .pem file on your computer.</span></span> <span data-ttu-id="6a2e0-216">Esse comando importa a chave para os HSMs no serviço de Cofre da Chave:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-216">This command imports the key into HSMs in the Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="6a2e0-217">O próximo comando importa um pacote de BYOK ("traga sua própria chave").</span><span class="sxs-lookup"><span data-stu-id="6a2e0-217">The next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="6a2e0-218">Isso permite gerar sua chave no HSM local e transferi-la para os HSMs no serviço de Cofre da Chave, sem que a chave deixe os limites do HSM:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-218">This lets you generate your key in your local HSM, and transfer it to HSMs in the Key Vault service, without the key leaving the HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="6a2e0-219">Para obter instruções mais detalhadas sobre como gerar esse pacote de BYOK, consulte [Como usar Chaves Protegidas por HSM com o Cofre da Chave do Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="6a2e0-219">For more detailed instructions about how to generate this BYOK package, see [How to use HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-the-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="6a2e0-220">Excluir o cofre de chave e chaves e segredos associados</span><span class="sxs-lookup"><span data-stu-id="6a2e0-220">Delete the key vault and associated keys and secrets</span></span>
<span data-ttu-id="6a2e0-221">Se você não precisar mais do cofre de chaves e da chave ou do segredo contido nela, poderá excluir o cofre de chaves usando o comando `az keyvault delete`:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-221">If you no longer need the key vault and the key or secret that it contains, you can delete the key vault by using the `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="6a2e0-222">Ou você pode excluir um grupo de recursos do Azure inteiro, que inclui o cofre de chave e quaisquer outros recursos incluídos nesse grupo:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-222">Or, you can delete an entire Azure resource group, which includes the key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="6a2e0-223">Outros comandos da interface de linha de comando de plataforma cruzada do Azure</span><span class="sxs-lookup"><span data-stu-id="6a2e0-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="6a2e0-224">Outros comandos que podem ser úteis para gerenciar o Cofre da Chave do Azure.</span><span class="sxs-lookup"><span data-stu-id="6a2e0-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="6a2e0-225">Este comando lista uma exibição em tabela de todas as chaves e propriedades selecionadas:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="6a2e0-226">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="6a2e0-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="6a2e0-227">Este comando exibe uma lista completa de propriedades para a chave especificada:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-227">This command displays a full list of properties for the specified key:</span></span>

<span data-ttu-id="6a2e0-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="6a2e0-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="6a2e0-229">Este comando lista uma exibição em tabela de todos os nomes de segredos e propriedades selecionadas:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="6a2e0-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="6a2e0-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="6a2e0-231">Aqui está um exemplo de como remover uma chave específica:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-231">Here's an example of how to remove a specific key:</span></span>

<span data-ttu-id="6a2e0-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="6a2e0-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="6a2e0-233">Aqui está um exemplo de como remover um segredo específica:</span><span class="sxs-lookup"><span data-stu-id="6a2e0-233">Here's an example of how to remove a specific secret:</span></span>

<span data-ttu-id="6a2e0-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="6a2e0-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="6a2e0-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6a2e0-235">Next steps</span></span>
<span data-ttu-id="6a2e0-236">Para obter a referência completa da CLI do Azure de comandos do cofre de chaves, consulte [referência da CLI do Key Vault](/cli/azure/keyvault)</span><span class="sxs-lookup"><span data-stu-id="6a2e0-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="6a2e0-237">Para referências de programação, consulte [Guia do desenvolvedor do Cofre da Chave do Azure](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="6a2e0-237">For programming references, see [the Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
