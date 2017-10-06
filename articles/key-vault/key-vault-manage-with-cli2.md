---
title: Cofre de chave do Azure usando a CLI do aaaManage | Microsoft Docs
description: "Use este tutorial tooautomate as tarefas comuns no cofre de chaves usando Olá 2.0 do CLI"
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
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a><span data-ttu-id="ee712-103">Gerenciar o Key Vault usando a CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ee712-103">Manage Key Vault using CLI 2.0</span></span>
<span data-ttu-id="ee712-104">O Cofre da Chave do Azure está disponível na maioria das regiões.</span><span class="sxs-lookup"><span data-stu-id="ee712-104">Azure Key Vault is available in most regions.</span></span> <span data-ttu-id="ee712-105">Para obter mais informações, consulte Olá [página de preços do Cofre de chaves](https://azure.microsoft.com/pricing/details/key-vault/).</span><span class="sxs-lookup"><span data-stu-id="ee712-105">For more information, see hello [Key Vault pricing page](https://azure.microsoft.com/pricing/details/key-vault/).</span></span>

## <a name="introduction"></a><span data-ttu-id="ee712-106">Introdução</span><span class="sxs-lookup"><span data-stu-id="ee712-106">Introduction</span></span>
<span data-ttu-id="ee712-107">Use este tutorial toohelp você obter Introdução ao Azure Key Vault toocreate um contêiner protegido (um cofre) no Azure, toostore e gerenciar chaves de criptografia e segredos no Azure.</span><span class="sxs-lookup"><span data-stu-id="ee712-107">Use this tutorial toohelp you get started with Azure Key Vault toocreate a hardened container (a vault) in Azure, toostore and manage cryptographic keys and secrets in Azure.</span></span> <span data-ttu-id="ee712-108">Orienta você pelo processo de saudação do uso de Interface de linha de comando de plataforma cruzada do Azure toocreate um cofre que contém uma chave ou a senha que você pode usar com um aplicativo do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee712-108">It walks you through hello process of using Azure Cross-Platform Command-Line Interface toocreate a vault that contains a key or password that you can then use with an Azure application.</span></span> <span data-ttu-id="ee712-109">Em seguida, ele mostra como um aplicativo pode usar essa chave ou senha.</span><span class="sxs-lookup"><span data-stu-id="ee712-109">It then shows you how an application can then use that key or password.</span></span>

<span data-ttu-id="ee712-110">**Estimado tempo toocomplete:** 20 minutos</span><span class="sxs-lookup"><span data-stu-id="ee712-110">**Estimated time toocomplete:** 20 minutes</span></span>

> [!NOTE]
> <span data-ttu-id="ee712-111">Este tutorial não inclui instruções sobre como toowrite Olá aplicativo do Azure que uma das etapas de saudação inclui, que mostra como tooauthorize toouse um aplicativo uma chave ou segredo na chave Olá cofre.</span><span class="sxs-lookup"><span data-stu-id="ee712-111">This tutorial does not include instructions on how toowrite hello Azure application that one of hello steps includes, which shows how tooauthorize an application toouse a key or secret in hello key vault.</span></span>
>
> <span data-ttu-id="ee712-112">Este tutorial usa Olá 2.0 mais recentes de CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee712-112">This tutorial uses hello latest Azure CLI 2.0.</span></span>
>
>

<span data-ttu-id="ee712-113">Para obter informações gerais sobre o Cofre da Chave do Azure, consulte [O que é o Cofre da Chave do Azure?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="ee712-113">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ee712-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ee712-114">Prerequisites</span></span>
<span data-ttu-id="ee712-115">toocomplete neste tutorial, você deve ter Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee712-115">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="ee712-116">TooMicrosoft uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee712-116">A subscription tooMicrosoft Azure.</span></span> <span data-ttu-id="ee712-117">Se não tiver uma assinatura, você pode se inscrever para uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial).</span><span class="sxs-lookup"><span data-stu-id="ee712-117">If you do not have one, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial).</span></span>
* <span data-ttu-id="ee712-118">Interface de Linha de Comando versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ee712-118">Command-Line Interface version 2.0 or later.</span></span> <span data-ttu-id="ee712-119">tooinstall Olá a versão mais recente e conecte-se tooyour assinatura do Azure, consulte [instalar e configurar Olá 2.0 de Interface de linha de comando de plataforma cruzada do Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ee712-119">tooinstall hello latest version and connect tooyour Azure subscription, see [Install and Configure hello Azure Cross-Platform Command-Line Interface 2.0](/cli/azure/install-azure-cli).</span></span>
* <span data-ttu-id="ee712-120">Um aplicativo que será a chave de saudação toouse configurado ou a senha criados por você neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="ee712-120">An application that will be configured toouse hello key or password that you create in this tutorial.</span></span> <span data-ttu-id="ee712-121">Um aplicativo de exemplo está disponível no hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span><span class="sxs-lookup"><span data-stu-id="ee712-121">A sample application is available from hello [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343).</span></span> <span data-ttu-id="ee712-122">Para obter instruções, consulte Olá que acompanha o arquivo Leiame.</span><span class="sxs-lookup"><span data-stu-id="ee712-122">For instructions, see hello accompanying Readme file.</span></span>

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a><span data-ttu-id="ee712-123">Obtendo ajuda com a interface de linha de comando de plataforma cruzada do Azure</span><span class="sxs-lookup"><span data-stu-id="ee712-123">Getting help with Azure Cross-Platform Command-Line Interface</span></span>
<span data-ttu-id="ee712-124">Este tutorial presume que você esteja familiarizado com a interface de linha de comando da saudação (Bash, Terminal, prompt de comando)</span><span class="sxs-lookup"><span data-stu-id="ee712-124">This tutorial assumes that you are familiar with hello command-line interface (Bash, Terminal, Command prompt)</span></span>

<span data-ttu-id="ee712-125">Hello – ajuda -h parâmetro ou pode ser usado tooview ajuda para comandos específicos.</span><span class="sxs-lookup"><span data-stu-id="ee712-125">hello --help or -h parameter can be used tooview help for specific commands.</span></span> <span data-ttu-id="ee712-126">Como alternativa, hello azure help [comando] [Opções] formato também pode ser usado tooreturn Olá mesmas informações.</span><span class="sxs-lookup"><span data-stu-id="ee712-126">Alternately, hello azure help [command] [options] format can also be used tooreturn hello same information.</span></span> <span data-ttu-id="ee712-127">Por exemplo, a seguir Olá comandos retornam todas as mesmas informações de hello:</span><span class="sxs-lookup"><span data-stu-id="ee712-127">For example, hello following commands all return hello same information:</span></span>

```
az account set --help
az account set -h
```

<span data-ttu-id="ee712-128">Em caso de dúvida sobre parâmetros Olá necessários por um comando, consulte usando toohelp – ajuda, -h ou az help [comando].</span><span class="sxs-lookup"><span data-stu-id="ee712-128">When in doubt about hello parameters needed by a command, refer toohelp using --help, -h or az help [command].</span></span>

<span data-ttu-id="ee712-129">Você também pode ler Olá tutoriais tooget familiarizado com o Azure Resource Manager na Interface de linha de comando de plataforma cruzada do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee712-129">You can also read hello following tutorials tooget familiar with Azure Resource Manager in Azure Cross-Platform Command-Line Interface:</span></span>

* [<span data-ttu-id="ee712-130">Instalar a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee712-130">Install Azure CLI</span></span>](/cli/azure/install-azure-cli)
* [<span data-ttu-id="ee712-131">Introdução à CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="ee712-131">Get started with Azure CLI 2.0</span></span>](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a><span data-ttu-id="ee712-132">Conecte-se tooyour assinaturas</span><span class="sxs-lookup"><span data-stu-id="ee712-132">Connect tooyour subscriptions</span></span>
<span data-ttu-id="ee712-133">toolog usando uma conta organizacional, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee712-133">toolog in using an organizational account, use hello following command:</span></span>

```
az login -u username@domain.com -p password
```

<span data-ttu-id="ee712-134">ou se você quiser toolog no digitando interativamente</span><span class="sxs-lookup"><span data-stu-id="ee712-134">or if you want toolog in by typing interactively</span></span>

```
az login
```

<span data-ttu-id="ee712-135">Se você tiver várias assinaturas e desejar toospecify um um toouse específico para o Cofre de chaves do Azure, digite Olá assinaturas de saudação toosee para sua conta a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee712-135">If you have multiple subscriptions and want toospecify a specific one toouse for Azure Key Vault, type hello following toosee hello subscriptions for your account:</span></span>

```
az account list
```

<span data-ttu-id="ee712-136">Toouse de assinatura do hello de toospecify, em seguida,, tipo:</span><span class="sxs-lookup"><span data-stu-id="ee712-136">Then, toospecify hello subscription toouse, type:</span></span>

```
az account set --subscription <subscription name or ID>
```

<span data-ttu-id="ee712-137">Para obter mais informações sobre como configurar a Interface de Linha de Comando de plataforma cruzada do Azure, consulte [Instalar a CLI do Azure](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ee712-137">For more information about configuring Azure Cross-Platform Command-Line Interface, see [Install Azure CLI](/cli/azure/install-azure-cli).</span></span>

## <a name="create-a-new-resource-group"></a><span data-ttu-id="ee712-138">Criar um novo grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="ee712-138">Create a new resource group</span></span>
<span data-ttu-id="ee712-139">Ao usar o Gerenciador de Recursos do Azure, todos os recursos relacionados são criados em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ee712-139">When using Azure Resource Manager, all related resources are created inside a resource group.</span></span> <span data-ttu-id="ee712-140">Criaremos um novo grupo de recursos “ContosoResourceGroup” para este tutorial.</span><span class="sxs-lookup"><span data-stu-id="ee712-140">We will create a new resource group 'ContosoResourceGroup' for this tutorial.</span></span>

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

<span data-ttu-id="ee712-141">Olá primeiro parâmetro é o nome do grupo de recursos e Olá segundo parâmetro é o local de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee712-141">hello first parameter is resource group name and hello second parameter is hello location.</span></span> <span data-ttu-id="ee712-142">Para local, use o comando Olá `az account list-locations` tooidentify como toospecify toohello um local alternativo uma neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="ee712-142">For location, use hello command `az account list-locations` tooidentify how toospecify an alternative location toohello one in this example.</span></span> <span data-ttu-id="ee712-143">Se precisar de mais informações, digite: `az account list-locations -h`.</span><span class="sxs-lookup"><span data-stu-id="ee712-143">If you need more information, type: `az account list-locations -h`.</span></span>

## <a name="register-hello-key-vault-resource-provider"></a><span data-ttu-id="ee712-144">Registrar o provedor de recursos do Cofre de chaves Olá</span><span class="sxs-lookup"><span data-stu-id="ee712-144">Register hello Key Vault resource provider</span></span>
<span data-ttu-id="ee712-145">Verifique se o provedor de recursos do Cofre de Chaves está registrado em sua assinatura:</span><span class="sxs-lookup"><span data-stu-id="ee712-145">Make sure that Key Vault resource provider is registered in your subscription:</span></span>

```
az provider register -n Microsoft.KeyVault
```

<span data-ttu-id="ee712-146">Isso só precisa toobe feito uma vez por assinatura.</span><span class="sxs-lookup"><span data-stu-id="ee712-146">This only needs toobe done once per subscription.</span></span>

## <a name="create-a-key-vault"></a><span data-ttu-id="ee712-147">Criar um cofre de chave</span><span class="sxs-lookup"><span data-stu-id="ee712-147">Create a key vault</span></span>
<span data-ttu-id="ee712-148">Saudação de uso `az keyvault create` comando toocreate um cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="ee712-148">Use hello `az keyvault create` command toocreate a key vault.</span></span> <span data-ttu-id="ee712-149">Esse script tem três parâmetros obrigatórios: um nome de grupo de recursos, um nome de Cofre de chaves e localização geográfica hello.</span><span class="sxs-lookup"><span data-stu-id="ee712-149">This script has three mandatory parameters: a resource group name, a key vault name, and hello geographic location.</span></span>

<span data-ttu-id="ee712-150">Por exemplo, se você usar o nome do cofre Olá de ContosoKeyVault, nome do grupo de recursos de saudação do ContosoResourceGroup e o local de saudação do Leste Asiático, digite:</span><span class="sxs-lookup"><span data-stu-id="ee712-150">For example, if you use hello vault name of ContosoKeyVault, hello resource group name of ContosoResourceGroup, and hello location of East Asia, type:</span></span>
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

<span data-ttu-id="ee712-151">saída de Hello desse comando mostra as propriedades do Cofre de chaves de saudação que você acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="ee712-151">hello output of this command shows properties of hello key vault that you've just created.</span></span> <span data-ttu-id="ee712-152">Olá duas propriedades de mais importantes são:</span><span class="sxs-lookup"><span data-stu-id="ee712-152">hello two most important properties are:</span></span>

* <span data-ttu-id="ee712-153">**nome**: no exemplo hello, isso é ContosoKeyVault.</span><span class="sxs-lookup"><span data-stu-id="ee712-153">**name**: In hello example this is ContosoKeyVault.</span></span> <span data-ttu-id="ee712-154">Você usará esse nome para outros comandos do Key Vault.</span><span class="sxs-lookup"><span data-stu-id="ee712-154">You will use this name for other Key Vault commands.</span></span>
* <span data-ttu-id="ee712-155">**vaultUri**: no exemplo hello, isso é https://contosokeyvault.vault.azure.net.</span><span class="sxs-lookup"><span data-stu-id="ee712-155">**vaultUri**: In hello example this is https://contosokeyvault.vault.azure.net.</span></span> <span data-ttu-id="ee712-156">Aplicativos que usam seu cofre via API REST devem usar esse URI.</span><span class="sxs-lookup"><span data-stu-id="ee712-156">Applications that use your vault through its REST API must use this URI.</span></span>

<span data-ttu-id="ee712-157">Sua conta do Azure é agora tooperform autorizado todas as operações nesta chave de cofre.</span><span class="sxs-lookup"><span data-stu-id="ee712-157">Your Azure account is now authorized tooperform any operations on this key vault.</span></span> <span data-ttu-id="ee712-158">Até o momento, ninguém mais está.</span><span class="sxs-lookup"><span data-stu-id="ee712-158">As yet, nobody else is.</span></span>

## <a name="add-a-key-or-secret-toohello-key-vault"></a><span data-ttu-id="ee712-159">Adicionar uma chave ou segredo toohello Cofre de chaves</span><span class="sxs-lookup"><span data-stu-id="ee712-159">Add a key or secret toohello key vault</span></span>
<span data-ttu-id="ee712-160">Se você quiser Azure Key Vault toocreate uma chave protegida por software para você, use Olá `az key create` de comando e digite Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee712-160">If you want Azure Key Vault toocreate a software-protected key for you, use hello `az key create` command, and type hello following:</span></span>
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
<span data-ttu-id="ee712-161">No entanto, se você tiver uma chave existente em um arquivo. PEM salvo como arquivo local em um arquivo chamado softkey.pem que você deseja tooupload tooAzure Cofre de chaves, digite Olá seguir tooimport chave de saudação de saudação. Arquivo PEM, que protege a chave de saudação pelo software no hello serviço de Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="ee712-161">However, if you have an existing key in a .pem file saved as local file in a file named softkey.pem that you want tooupload tooAzure Key Vault, type hello following tooimport hello key from hello .PEM file, which protects hello key by software in hello Key Vault service:</span></span>
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
<span data-ttu-id="ee712-162">Agora você pode referenciar chave Olá que foi criada ou carregada tooAzure Cofre de chaves, usando seu URI.</span><span class="sxs-lookup"><span data-stu-id="ee712-162">You can now reference hello key that you created or uploaded tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="ee712-163">Use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways obter a versão atual do hello e usar **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget essa versão específica.</span><span class="sxs-lookup"><span data-stu-id="ee712-163">Use  **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways get hello current version, and use **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/cgacf4f763ar42ffb0a1gca546aygd87** tooget this specific version.</span></span>

<span data-ttu-id="ee712-164">tooadd um cofre toohello secreta, que é uma senha chamada SQLPassword e que tem o valor de saudação do Pa$ $w0rd tooAzure Cofre de chaves, Olá tipo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee712-164">tooadd a secret toohello vault, which is a password named SQLPassword and that has hello value of Pa$$w0rd tooAzure Key Vault, type hello following:</span></span>
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
<span data-ttu-id="ee712-165">Agora você pode referenciar essa senha que você adicionou tooAzure Cofre de chaves, usando seu URI.</span><span class="sxs-lookup"><span data-stu-id="ee712-165">You can now reference this password that you added tooAzure Key Vault, by using its URI.</span></span> <span data-ttu-id="ee712-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways obter a versão atual do hello e usar **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget essa versão específica.</span><span class="sxs-lookup"><span data-stu-id="ee712-166">Use **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways get hello current version, and use **https://ContosoVault.vault.azure.net/secrets/SQLPassword/90018dbb96a84117a0d2847ef8e7189d** tooget this specific version.</span></span>

<span data-ttu-id="ee712-167">Vejamos chave hello ou chave secreta que você acabou de criar:</span><span class="sxs-lookup"><span data-stu-id="ee712-167">Let's view hello key or secret that you just created:</span></span>

* <span data-ttu-id="ee712-168">tooview sua chave, tipo:`az keyvault key list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="ee712-168">tooview your key, type: `az keyvault key list --vault-name 'ContosoKeyVault'`</span></span>
* <span data-ttu-id="ee712-169">tooview seu segredo, tipo:`az keyvault secret list --vault-name 'ContosoKeyVault'`</span><span class="sxs-lookup"><span data-stu-id="ee712-169">tooview your secret, type: `az keyvault secret list --vault-name 'ContosoKeyVault'`</span></span>

## <a name="register-an-application-with-azure-active-directory"></a><span data-ttu-id="ee712-170">Registrar um aplicativo com o Active Directory do Azure</span><span class="sxs-lookup"><span data-stu-id="ee712-170">Register an application with Azure Active Directory</span></span>
<span data-ttu-id="ee712-171">Esta etapa geralmente seria feita por um desenvolvedor, em um computador separado.</span><span class="sxs-lookup"><span data-stu-id="ee712-171">This step would usually be done by a developer, on a separate computer.</span></span> <span data-ttu-id="ee712-172">Ele não é específico tooAzure Cofre de chaves, mas é incluído aqui, para fins de integridade.</span><span class="sxs-lookup"><span data-stu-id="ee712-172">It is not specific tooAzure Key Vault but is included here, for completeness.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee712-173">tutorial de saudação toocomplete, sua conta, cofre hello e aplicativo hello que registrar-se nesta etapa devem ser no hello mesmo diretório do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee712-173">toocomplete hello tutorial, your account, hello vault, and hello application that you will register in this step must all be in hello same Azure directory.</span></span>
>
>

<span data-ttu-id="ee712-174">Aplicativos que usam um cofre de chave devem ser autenticados usando um token do Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee712-174">Applications that use a key vault must authenticate by using a token from Azure Active Directory.</span></span> <span data-ttu-id="ee712-175">toodo, Olá proprietário do aplicativo hello deve primeiro registrar aplicativo hello no seu Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee712-175">toodo this, hello owner of hello application must first register hello application in their Azure Active Directory.</span></span> <span data-ttu-id="ee712-176">No final de saudação do registro, o proprietário do aplicativo hello obtém Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee712-176">At hello end of registration, hello application owner gets hello following values:</span></span>

* <span data-ttu-id="ee712-177">Um **ID do aplicativo** (também conhecido como uma ID de cliente) e **chave de autenticação** (também conhecido como segredo compartilhado Olá).</span><span class="sxs-lookup"><span data-stu-id="ee712-177">An **Application ID** (also known as a Client ID) and **authentication key** (also known as hello shared secret).</span></span> <span data-ttu-id="ee712-178">aplicativo Hello deve apresentar ambos tooAzure esses valores do Active Directory, tooget um token.</span><span class="sxs-lookup"><span data-stu-id="ee712-178">hello application must present both of these values tooAzure Active Directory, tooget a token.</span></span> <span data-ttu-id="ee712-179">Como o aplicativo hello está configurado toodo que isso depende do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="ee712-179">How hello application is configured toodo this depends on hello application.</span></span> <span data-ttu-id="ee712-180">Para Olá aplicativo de exemplo do Cofre de chaves, o proprietário do aplicativo hello define esses valores no arquivo App. config de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee712-180">For hello Key Vault sample application, hello application owner sets these values in hello app.config file.</span></span>

<span data-ttu-id="ee712-181">aplicativo de hello tooregister no Active Directory do Azure:</span><span class="sxs-lookup"><span data-stu-id="ee712-181">tooregister hello application in Azure Active Directory:</span></span>

1. <span data-ttu-id="ee712-182">Entrar toohello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee712-182">Sign in toohello Azure portal.</span></span>
2. <span data-ttu-id="ee712-183">Olá esquerda, clique em **Active Directory do Azure**e, em seguida, selecione o diretório de saudação na qual você registrará o seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee712-183">On hello left, click **Azure Active Directory**, and then select hello directory in which you will register your application.</span></span> <br> <br> 

> [!Note] 
> <span data-ttu-id="ee712-184">Você deve selecionar Olá Olá mesmo diretório que contém a assinatura do Azure com o qual você criou seu Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="ee712-184">You must select hello same directory that contains hello Azure subscription with which you created your key vault.</span></span> <span data-ttu-id="ee712-185">Se você não souber qual diretório isto é, clique em **configurações**, identificar Olá assinatura com a qual você criou seu Cofre de chaves e nome de saudação de observação do diretório Olá exibido na última coluna de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee712-185">If you do not know which directory this is, click **Settings**, identify hello subscription with which you created your key vault, and note hello name of hello directory displayed in hello last column.</span></span>

3. <span data-ttu-id="ee712-186">Clique em **APLICATIVOS**.</span><span class="sxs-lookup"><span data-stu-id="ee712-186">Click **APPLICATIONS**.</span></span> <span data-ttu-id="ee712-187">Se nenhum aplicativo adicionou tooyour diretório, essa página mostrará apenas Olá **adicionar um aplicativo** link.</span><span class="sxs-lookup"><span data-stu-id="ee712-187">If no apps have been added tooyour directory, this page will show only hello **Add an App** link.</span></span> <span data-ttu-id="ee712-188">Clique em link hello, ou como alternativa, você pode clicar em Olá **adicionar** na barra de comandos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee712-188">Click hello link, or alternatively, you can click hello **ADD** on hello command bar.</span></span>
4. <span data-ttu-id="ee712-189">Em Olá **Adicionar aplicativo** assistente, em Olá **o que fazer você deseja toodo?** , clique em **adicionar um aplicativo que minha organização esteja desenvolvendo**.</span><span class="sxs-lookup"><span data-stu-id="ee712-189">In hello **ADD APPLICATION** wizard, on hello **What do you want toodo?** page, click **Add an application my organization is developing**.</span></span>
5. <span data-ttu-id="ee712-190">Em Olá **Conte-nos sobre seu aplicativo** página, especifique um nome para seu aplicativo e selecione **aplicativo de WEB e/ou API WEB** (Olá padrão).</span><span class="sxs-lookup"><span data-stu-id="ee712-190">On hello **Tell us about your application** page, specify a name for your application and select **WEB APPLICATION AND/OR WEB API** (hello default).</span></span> <span data-ttu-id="ee712-191">Clique em próximo ícone de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee712-191">Click hello Next icon.</span></span>
6. <span data-ttu-id="ee712-192">Em Olá **propriedades do aplicativo** especifique Olá **URL de logon** e **URI da ID do aplicativo** para seu aplicativo da web.</span><span class="sxs-lookup"><span data-stu-id="ee712-192">On hello **App properties** page, specify hello **SIGN-ON URL** and **APP ID URI** for your web application.</span></span> <span data-ttu-id="ee712-193">Se seu aplicativo não tiver esses valores, você pode inventá-los para esta etapa (por exemplo, você poderia especificar http://test1.contoso.com para as duas caixas).</span><span class="sxs-lookup"><span data-stu-id="ee712-193">If your application does not have these values, you can make them up for this step (for example, you could specify http://test1.contoso.com for both boxes).</span></span> <span data-ttu-id="ee712-194">Não importa se existirem a esses sites; o importante é que aplicativo hello URI de ID para cada aplicativo é diferente para cada aplicativo em seu diretório.</span><span class="sxs-lookup"><span data-stu-id="ee712-194">It does not matter if these sites exist; what is important is that hello app ID URI for each application is different for every application in your directory.</span></span> <span data-ttu-id="ee712-195">diretório de saudação usa tooidentify essa cadeia de caracteres em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ee712-195">hello directory uses this string tooidentify your app.</span></span>
7. <span data-ttu-id="ee712-196">Clique em Olá ícone completa toosave suas alterações no Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="ee712-196">Click hello Complete icon toosave your changes in hello wizard.</span></span>
8. <span data-ttu-id="ee712-197">Na página início rápido hello, clique em **configurar**.</span><span class="sxs-lookup"><span data-stu-id="ee712-197">On hello Quick Start page, click **CONFIGURE**.</span></span>
9. <span data-ttu-id="ee712-198">Role toohello **chaves** seção, selecione a duração de saudação e, em seguida, clique em **salvar**.</span><span class="sxs-lookup"><span data-stu-id="ee712-198">Scroll toohello **keys** section, select hello duration, and then click **SAVE**.</span></span> <span data-ttu-id="ee712-199">página de saudação é atualizada e agora mostra um valor de chave.</span><span class="sxs-lookup"><span data-stu-id="ee712-199">hello page refreshes and now shows a key value.</span></span> <span data-ttu-id="ee712-200">Você deve configurar seu aplicativo com esse valor de chave e hello **ID do cliente** valor.</span><span class="sxs-lookup"><span data-stu-id="ee712-200">You must configure your application with this key value and hello **CLIENT ID** value.</span></span> <span data-ttu-id="ee712-201">(As instruções para esta configuração são específicas do aplicativo).</span><span class="sxs-lookup"><span data-stu-id="ee712-201">(Instructions for this configuration will be application-specific.)</span></span>
10. <span data-ttu-id="ee712-202">Copie valor de ID de cliente Olá nessa página, que você usará Olá próxima etapa tooset permissões em seu cofre.</span><span class="sxs-lookup"><span data-stu-id="ee712-202">Copy hello client ID value from this page, which you will use in hello next step tooset permissions on your vault.</span></span>

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a><span data-ttu-id="ee712-203">Autorizar Olá aplicativo toouse Olá chave ou segredo</span><span class="sxs-lookup"><span data-stu-id="ee712-203">Authorize hello application toouse hello key or secret</span></span>
<span data-ttu-id="ee712-204">tooauthorize Olá aplicativo tooaccess Olá chave ou segredo no cofre hello, use Olá `az keyvault set-policy` comando.</span><span class="sxs-lookup"><span data-stu-id="ee712-204">tooauthorize hello application tooaccess hello key or secret in hello vault, use hello `az keyvault set-policy` command.</span></span>

<span data-ttu-id="ee712-205">Por exemplo, se o nome do cofre for ContosoKeyVault e hello aplicativo deseja tooauthorize tem uma ID de cliente de 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, e você deseja tooauthorize Olá aplicativo toodecrypt e entre com as chaves em seu cofre, execute Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ee712-205">For example, if your vault name is ContosoKeyVault and hello application you want tooauthorize has a client ID of 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed, and you want tooauthorize hello application toodecrypt and sign with keys in your vault, then run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

<span data-ttu-id="ee712-206">Se você quiser tooauthorize esse mesmo segredos de tooread do aplicativo em seu cofre, execute o seguinte de saudação:</span><span class="sxs-lookup"><span data-stu-id="ee712-206">If you want tooauthorize that same application tooread secrets in your vault, run hello following:</span></span>
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a><span data-ttu-id="ee712-207">Se você quiser toouse um módulo de segurança de hardware (HSM)</span><span class="sxs-lookup"><span data-stu-id="ee712-207">If you want toouse a hardware security module (HSM)</span></span>
<span data-ttu-id="ee712-208">Para garantia extra, você pode importar ou gerar chaves em módulos de segurança de hardware (HSM) que nunca deixam o limite do HSM hello.</span><span class="sxs-lookup"><span data-stu-id="ee712-208">For added assurance, you can import or generate keys in hardware security modules (HSMs) that never leave hello HSM boundary.</span></span> <span data-ttu-id="ee712-209">Olá HSMs são FIPS 140-2 nível 2 validado.</span><span class="sxs-lookup"><span data-stu-id="ee712-209">hello HSMs are FIPS 140-2 Level 2 validated.</span></span> <span data-ttu-id="ee712-210">Se esse requisito não se aplica a tooyou, ignore esta seção e vá muito[excluir Cofre de chaves hello e chaves associadas e segredos](#delete-the-key-vault-and-associated-keys-and-secrets).</span><span class="sxs-lookup"><span data-stu-id="ee712-210">If this requirement doesn't apply tooyou, skip this section and go too[Delete hello key vault and associated keys and secrets](#delete-the-key-vault-and-associated-keys-and-secrets).</span></span>

<span data-ttu-id="ee712-211">toocreate essas chaves protegidas por HSM, você deve ter uma assinatura do cofre que dá suporte a chaves protegidas por HSM.</span><span class="sxs-lookup"><span data-stu-id="ee712-211">toocreate these HSM-protected keys, you must have a vault subscription that supports HSM-protected keys.</span></span>

<span data-ttu-id="ee712-212">Quando você cria keyvault Olá, adicione um parâmetro de 'sku' hello:</span><span class="sxs-lookup"><span data-stu-id="ee712-212">When you create hello keyvault, add hello 'sku' parameter:</span></span>

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
<span data-ttu-id="ee712-213">Você pode adicionar chaves protegidas por software (conforme mostrado anteriormente) e o Cofre de chaves protegidas por HSM toothis.</span><span class="sxs-lookup"><span data-stu-id="ee712-213">You can add software-protected keys (as shown earlier) and HSM-protected keys toothis vault.</span></span> <span data-ttu-id="ee712-214">toocreate uma chave protegida por HSM, too'HSM de parâmetro de destino do conjunto de saudação ':</span><span class="sxs-lookup"><span data-stu-id="ee712-214">toocreate an HSM-protected key, set hello Destination parameter too'HSM':</span></span>

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

<span data-ttu-id="ee712-215">Você pode usar o hello após o comando tooimport uma chave de um arquivo. PEM em seu computador.</span><span class="sxs-lookup"><span data-stu-id="ee712-215">You can use hello following command tooimport a key from a .pem file on your computer.</span></span> <span data-ttu-id="ee712-216">Este comando importa chave Olá para HSMs em Olá serviço de Cofre de chaves:</span><span class="sxs-lookup"><span data-stu-id="ee712-216">This command imports hello key into HSMs in hello Key Vault service:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
<span data-ttu-id="ee712-217">comando Avançar Olá importa um "Traga sua própria chave" pacote (BYOK).</span><span class="sxs-lookup"><span data-stu-id="ee712-217">hello next command imports a “bring your own key" (BYOK) package.</span></span> <span data-ttu-id="ee712-218">Isso permite que você gerar sua chave em seu HSM local e transferi-la tooHSMs no hello serviço de Cofre de chaves sem chave Olá deixando o limite do HSM hello:</span><span class="sxs-lookup"><span data-stu-id="ee712-218">This lets you generate your key in your local HSM, and transfer it tooHSMs in hello Key Vault service, without hello key leaving hello HSM boundary:</span></span>

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
<span data-ttu-id="ee712-219">Para obter mais instruções sobre como toogenerate esse pacote BYOK, consulte [como toouse HSM-Protected chaves com Cofre de chaves do Azure](key-vault-hsm-protected-keys.md).</span><span class="sxs-lookup"><span data-stu-id="ee712-219">For more detailed instructions about how toogenerate this BYOK package, see [How toouse HSM-Protected Keys with Azure Key Vault](key-vault-hsm-protected-keys.md).</span></span>

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a><span data-ttu-id="ee712-220">Excluir o Cofre de chaves hello e chaves associadas e segredos</span><span class="sxs-lookup"><span data-stu-id="ee712-220">Delete hello key vault and associated keys and secrets</span></span>
<span data-ttu-id="ee712-221">Se você não precisar mais Cofre de chaves hello e chave de saudação ou segredo que ele contém, você pode excluir o Cofre de chaves hello usando Olá `az keyvault delete` comando:</span><span class="sxs-lookup"><span data-stu-id="ee712-221">If you no longer need hello key vault and hello key or secret that it contains, you can delete hello key vault by using hello `az keyvault delete` command:</span></span>

```
az keyvault delete --name 'ContosoKeyVault'
```

<span data-ttu-id="ee712-222">Ou, você pode excluir um grupo de recursos do Azure inteiro, que inclui o Cofre de chaves de saudação e outros recursos incluídos no grupo:</span><span class="sxs-lookup"><span data-stu-id="ee712-222">Or, you can delete an entire Azure resource group, which includes hello key vault and any other resources that you included in that group:</span></span>

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a><span data-ttu-id="ee712-223">Outros comandos da interface de linha de comando de plataforma cruzada do Azure</span><span class="sxs-lookup"><span data-stu-id="ee712-223">Other Azure Cross-Platform Command-line Interface Commands</span></span>
<span data-ttu-id="ee712-224">Outros comandos que podem ser úteis para gerenciar o Cofre da Chave do Azure.</span><span class="sxs-lookup"><span data-stu-id="ee712-224">Other commands that you might useful for managing Azure Key Vault.</span></span>

<span data-ttu-id="ee712-225">Este comando lista uma exibição em tabela de todas as chaves e propriedades selecionadas:</span><span class="sxs-lookup"><span data-stu-id="ee712-225">This command lists a tabular display of all keys and selected properties:</span></span>

<span data-ttu-id="ee712-226">az keyvault key list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="ee712-226">az keyvault key list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="ee712-227">Este comando exibe uma lista completa das propriedades de chave especificado hello:</span><span class="sxs-lookup"><span data-stu-id="ee712-227">This command displays a full list of properties for hello specified key:</span></span>

<span data-ttu-id="ee712-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="ee712-228">az keyvault key show --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="ee712-229">Este comando lista uma exibição em tabela de todos os nomes de segredos e propriedades selecionadas:</span><span class="sxs-lookup"><span data-stu-id="ee712-229">This command lists a tabular display of all secret names and selected properties:</span></span>

<span data-ttu-id="ee712-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span><span class="sxs-lookup"><span data-stu-id="ee712-230">az keyvault secret list --vault-name 'ContosoKeyVault'</span></span>

<span data-ttu-id="ee712-231">Aqui está um exemplo de como tooremove uma chave específica:</span><span class="sxs-lookup"><span data-stu-id="ee712-231">Here's an example of how tooremove a specific key:</span></span>

<span data-ttu-id="ee712-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span><span class="sxs-lookup"><span data-stu-id="ee712-232">az keyvault key delete --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey'</span></span>

<span data-ttu-id="ee712-233">Aqui está um exemplo de como tooremove um segredo específico:</span><span class="sxs-lookup"><span data-stu-id="ee712-233">Here's an example of how tooremove a specific secret:</span></span>

<span data-ttu-id="ee712-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span><span class="sxs-lookup"><span data-stu-id="ee712-234">az keyvault secret delete --vault-name 'ContosoKeyVault' --name 'SQLPassword'</span></span>


## <a name="next-steps"></a><span data-ttu-id="ee712-235">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ee712-235">Next steps</span></span>
<span data-ttu-id="ee712-236">Para obter a referência completa da CLI do Azure de comandos do cofre de chaves, consulte [referência da CLI do Key Vault](/cli/azure/keyvault)</span><span class="sxs-lookup"><span data-stu-id="ee712-236">For complete Azure CLI reference for key vault commands, see [Key Vault CLI reference](/cli/azure/keyvault)</span></span>

<span data-ttu-id="ee712-237">Para referências de programação, consulte [Olá guia do desenvolvedor do Azure Key Vault](key-vault-developers-guide.md).</span><span class="sxs-lookup"><span data-stu-id="ee712-237">For programming references, see [hello Azure Key Vault developer's guide](key-vault-developers-guide.md).</span></span>
