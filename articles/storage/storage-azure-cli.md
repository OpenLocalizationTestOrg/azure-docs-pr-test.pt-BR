---
title: "Olá aaaUsing 2.0 do CLI do Azure com o armazenamento do Azure | Microsoft Docs"
description: "Saiba como toouse hello Azure Interface de linha de comando (CLI do Azure) 2.0 com toocreate de armazenamento do Azure e gerencie contas de armazenamento e trabalhar com arquivos e blobs do Azure. Olá 2.0 do CLI do Azure é uma ferramenta de plataforma cruzada escrita em Python."
services: storage
documentationcenter: na
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: article
ms.date: 06/02/2017
ms.author: marsma
ms.openlocfilehash: 38402373dcd87f1ef05471a02353c77d58f1a9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-20-with-azure-storage"></a><span data-ttu-id="8b988-104">Usando Olá 2.0 do CLI do Azure com o armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="8b988-104">Using hello Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="8b988-105">Olá código-fonte, a plataforma cruzada do Azure CLI 2.0 fornece um conjunto de comandos para trabalhar com hello plataforma Windows Azure.</span><span class="sxs-lookup"><span data-stu-id="8b988-105">hello open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with hello Azure platform.</span></span> <span data-ttu-id="8b988-106">Ele fornece grande parte da saudação mesma funcionalidade encontrada no hello [portal do Azure](https://portal.azure.com), incluindo o acesso de dados avançados.</span><span class="sxs-lookup"><span data-stu-id="8b988-106">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="8b988-107">Neste guia, mostramos como Olá toouse [2.0 do CLI do Azure](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform várias tarefas trabalhando com recursos em sua conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b988-107">In this guide, we show you how toouse hello [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) tooperform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="8b988-108">É recomendável baixar e instalar ou atualizar a versão mais recente toohello de saudação CLI 2.0 antes de usar este guia.</span><span class="sxs-lookup"><span data-stu-id="8b988-108">We recommend that you download and install or upgrade toohello latest version of hello CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="8b988-109">exemplos de saudação guia Olá assumem uso Olá Olá shell Bash no Ubuntu, mas outras plataformas devem ser executadas da mesma forma.</span><span class="sxs-lookup"><span data-stu-id="8b988-109">hello examples in hello guide assume hello use of hello Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="8b988-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8b988-110">Prerequisites</span></span>
<span data-ttu-id="8b988-111">Este guia pressupõe que você entender os conceitos básicos de saudação do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b988-111">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="8b988-112">Ele também pressupõe que você é capaz de toosatisfy Olá conta criação requisitos especificados abaixo para o Azure e Olá serviço de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b988-112">It also assumes that you're able toosatisfy hello account creation requirements that are specified below for Azure and hello Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="8b988-113">Contas</span><span class="sxs-lookup"><span data-stu-id="8b988-113">Accounts</span></span>
* <span data-ttu-id="8b988-114">**Conta do Azure**: se você ainda não tiver uma assinatura do Azure, [crie uma conta gratuita do Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="8b988-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="8b988-115">**Conta de armazenamento**: veja [Criar uma conta de armazenamento](../storage/storage-create-storage-account.md#create-a-storage-account) em [Sobre as contas de armazenamento do Azure](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8b988-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="install-hello-azure-cli-20"></a><span data-ttu-id="8b988-116">Instalar Olá 2.0 do CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8b988-116">Install hello Azure CLI 2.0</span></span>

<span data-ttu-id="8b988-117">Baixe e instale o hello Azure CLI 2.0 seguindo as instruções Olá descritas no [instalar o Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="8b988-117">Download and install hello Azure CLI 2.0 by following hello instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="8b988-118">Se você tiver problemas com a instalação Olá, confira Olá [solução de problemas de instalação](/cli/azure/install-az-cli2#installation-troubleshooting) seção do artigo hello e hello [instalar de solução de problemas](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guia no GitHub.</span><span class="sxs-lookup"><span data-stu-id="8b988-118">If you have trouble with hello installation, check out hello [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of hello article, and hello [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-hello-cli"></a><span data-ttu-id="8b988-119">Trabalhando com hello CLI</span><span class="sxs-lookup"><span data-stu-id="8b988-119">Working with hello CLI</span></span>

<span data-ttu-id="8b988-120">Depois de instalar a saudação CLI, você pode usar o hello `az` comando em seus comandos de CLI do Azure de saudação de tooaccess de interface de linha de comando (Bash, Terminal, Prompt de comando).</span><span class="sxs-lookup"><span data-stu-id="8b988-120">Once you've installed hello CLI, you can use hello `az` command in your command-line interface (Bash, Terminal, Command Prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="8b988-121">Saudação de tipo `az` toosee comando uma lista completa de comandos de base hello (Olá saída de exemplo a seguir foi truncada):</span><span class="sxs-lookup"><span data-stu-id="8b988-121">Type hello `az` command toosee a full list of hello base commands (hello following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome toohello cool new Azure CLI!

Here are hello base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="8b988-122">Na sua interface de linha de comando, execute o comando Olá `az storage --help` Olá toolist `storage` subgrupos de comando.</span><span class="sxs-lookup"><span data-stu-id="8b988-122">In your command-line interface, execute hello command `az storage --help` toolist hello `storage` command subgroups.</span></span> <span data-ttu-id="8b988-123">descrições de saudação de subgrupos de saudação fornecem uma visão geral da saudação de funcionalidade Olá que CLI do Azure fornece para trabalhar com seus recursos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b988-123">hello descriptions of hello subgroups provide an overview of hello functionality hello Azure CLI provides for working with your storage resources.</span></span>

```
Group
    az storage: Durable, highly available, and massively scalable cloud storage.

Subgroups:
    account  : Manage storage accounts.
    blob     : Object storage for unstructured data.
    container: Manage blob storage containers.
    cors     : Manage Storage service Cross-Origin Resource Sharing (CORS).
    directory: Manage file storage directories.
    entity   : Manage table storage entities.
    file     : File shares that use hello standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues tooeffectively scale applications according tootraffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-hello-cli-tooyour-azure-subscription"></a><span data-ttu-id="8b988-124">Conecte-se Olá CLI tooyour assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="8b988-124">Connect hello CLI tooyour Azure subscription</span></span>

<span data-ttu-id="8b988-125">toowork com recursos de saudação na sua assinatura do Azure, você deve primeiro fazer logon no tooyour conta do Azure com `az login`.</span><span class="sxs-lookup"><span data-stu-id="8b988-125">toowork with hello resources in your Azure subscription, you must first log in tooyour Azure account with `az login`.</span></span> <span data-ttu-id="8b988-126">Há várias maneiras de fazer logon:</span><span class="sxs-lookup"><span data-stu-id="8b988-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="8b988-127">**Logon Interativo**: `az login`</span><span class="sxs-lookup"><span data-stu-id="8b988-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="8b988-128">**Faça logon com o nome de usuário e senha**: `az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="8b988-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="8b988-129">Isso não funciona com contas da Microsoft ou contas que usam autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="8b988-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="8b988-130">**Faça logon com uma entidade de serviço**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="8b988-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="8b988-131">Script de exemplo da CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8b988-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="8b988-132">Em seguida, trabalharemos com um script de shell pequeno que emite alguns toointeract básica de comandos 2.0 do CLI do Azure com recursos de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b988-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands toointeract with Azure Storage resources.</span></span> <span data-ttu-id="8b988-133">script Hello primeiro cria um novo contêiner na conta de armazenamento, em seguida, carrega um contêiner existente de toothat de arquivo (como um blob).</span><span class="sxs-lookup"><span data-stu-id="8b988-133">hello script first creates a new container in your storage account, then uploads an existing file (as a blob) toothat container.</span></span> <span data-ttu-id="8b988-134">Ele listará todos os blobs no contêiner Olá e por fim, baixa Olá arquivo tooa de destino no computador local que você especificar.</span><span class="sxs-lookup"><span data-stu-id="8b988-134">It then lists all blobs in hello container, and finally, downloads hello file tooa destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating hello container..."
az storage container create --name $container_name

echo "Uploading hello file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing hello blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading hello file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="8b988-135">**Configurar e executar o script hello**</span><span class="sxs-lookup"><span data-stu-id="8b988-135">**Configure and run hello script**</span></span>

1. <span data-ttu-id="8b988-136">Abra o editor de texto favorito, copiar e colar Olá precede o script no editor de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b988-136">Open your favorite text editor, then copy and paste hello preceding script into hello editor.</span></span>

2. <span data-ttu-id="8b988-137">Em seguida, atualize as configurações de tooreflect de variáveis do script hello.</span><span class="sxs-lookup"><span data-stu-id="8b988-137">Next, update hello script's variables tooreflect your configuration settings.</span></span> <span data-ttu-id="8b988-138">Substitua Olá valores conforme especificado a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b988-138">Replace hello following values as specified:</span></span>

   * <span data-ttu-id="8b988-139">**\<storage_account_name\>**  nome de saudação da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b988-139">**\<storage_account_name\>** hello name of your storage account.</span></span>
   * <span data-ttu-id="8b988-140">**\<storage_account_key\>**  chave de acesso primária ou secundária Olá para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b988-140">**\<storage_account_key\>** hello primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="8b988-141">**\<container_name\>**  um nome hello novo toocreate de contêiner, como "azure-cli-exemplo-container".</span><span class="sxs-lookup"><span data-stu-id="8b988-141">**\<container_name\>** A name hello new container toocreate, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="8b988-142">**\<blob_name\>**  um nome para o blob de destino Olá no contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b988-142">**\<blob_name\>** A name for hello destination blob in hello container.</span></span>
   * <span data-ttu-id="8b988-143">**\<file_to_upload\>**  Olá caminho toosmall arquivo no computador local, como "~ / images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="8b988-143">**\<file_to_upload\>** hello path toosmall file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="8b988-144">**\<destination_file\>**  Olá o caminho do arquivo de destino, como "~ / downloadedImage.png".</span><span class="sxs-lookup"><span data-stu-id="8b988-144">**\<destination_file\>** hello destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="8b988-145">Depois que você atualizou variáveis necessárias Olá, Salvar script hello e sair de seu editor.</span><span class="sxs-lookup"><span data-stu-id="8b988-145">After you've updated hello necessary variables, save hello script and exit your editor.</span></span> <span data-ttu-id="8b988-146">as próximas etapas Olá supõem nomear seu script **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="8b988-146">hello next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="8b988-147">Marque o script hello como executável, se necessário:`chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="8b988-147">Mark hello script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="8b988-148">Execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="8b988-148">Execute hello script.</span></span> <span data-ttu-id="8b988-149">Por exemplo, no Bash:`./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="8b988-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="8b988-150">Você deve ver saída semelhante toohello seguinte e Olá  **\<destination_file\>**  especificado no hello script deve aparecer no computador local.</span><span class="sxs-lookup"><span data-stu-id="8b988-150">You should see output similar toohello following, and hello **\<destination_file\>** you specified in hello script should appear on your local computer.</span></span>

```
Creating hello container...
{
  "created": true
}
Uploading hello file...
Percent complete: %100.0
Listing hello blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading hello file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="8b988-151">Olá anterior de saída é em **tabela** formato.</span><span class="sxs-lookup"><span data-stu-id="8b988-151">hello preceding output is in **table** format.</span></span> <span data-ttu-id="8b988-152">Você pode especificar qual saída formato toouse especificando Olá `--output` argumento em seus comandos de CLI ou definido globalmente usando `az configure`.</span><span class="sxs-lookup"><span data-stu-id="8b988-152">You can specify which output format toouse by specifying hello `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="8b988-153">Gerenciar contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="8b988-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="8b988-154">Criar uma nova conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="8b988-154">Create a new storage account</span></span>
<span data-ttu-id="8b988-155">toouse armazenamento do Azure, você precisa de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b988-155">toouse Azure Storage, you need a storage account.</span></span> <span data-ttu-id="8b988-156">Você pode criar uma nova conta de armazenamento do Azure depois que você tiver configurado seu computador muito[conectar assinatura tooyour](#connect-to-your-azure-subscription).</span><span class="sxs-lookup"><span data-stu-id="8b988-156">You can create a new Azure Storage account after you've configured your computer too[connect tooyour subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="8b988-157">`--location` [Obrigatório]: local.</span><span class="sxs-lookup"><span data-stu-id="8b988-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="8b988-158">Por exemplo, “Oeste dos EUA”.</span><span class="sxs-lookup"><span data-stu-id="8b988-158">For example, "West US".</span></span>
* <span data-ttu-id="8b988-159">`--name`[Obrigatório]: nome de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="8b988-159">`--name` [Required]: hello storage account name.</span></span> <span data-ttu-id="8b988-160">Olá nome deve ter 3 caracteres too24 e usar apenas caracteres alfanuméricos minúsculos.</span><span class="sxs-lookup"><span data-stu-id="8b988-160">hello name must be 3 too24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="8b988-161">`--resource-group` [Obrigatório]: nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="8b988-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="8b988-162">`--sku`[Obrigatório]: Olá SKU de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b988-162">`--sku` [Required]: hello storage account SKU.</span></span> <span data-ttu-id="8b988-163">Valores permitidos:</span><span class="sxs-lookup"><span data-stu-id="8b988-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="8b988-164">Definir as variáveis de ambiente da conta de armazenamento padrão do Azure</span><span class="sxs-lookup"><span data-stu-id="8b988-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="8b988-165">Você pode ter várias contas de armazenamento na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b988-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="8b988-166">tooselect um deles toouse para armazenamento subsequentes todos os comandos, você pode definir essas variáveis de ambiente:</span><span class="sxs-lookup"><span data-stu-id="8b988-166">tooselect one of them toouse for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="8b988-167">É uma conta de armazenamento padrão tooset de outra forma usando uma cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="8b988-167">Another way tooset a default storage account is by using a connection string.</span></span> <span data-ttu-id="8b988-168">Primeiro, obtenha a cadeia de caracteres de conexão de saudação com hello `show-connection-string` comando:</span><span class="sxs-lookup"><span data-stu-id="8b988-168">First, get hello connection string with hello `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="8b988-169">Em seguida, Olá de cópia de saída de cadeia de caracteres de conexão e defina Olá `AZURE_STORAGE_CONNECTION_STRING` variável de ambiente (talvez seja necessário tooenclose cadeia de conexão Olá entre aspas):</span><span class="sxs-lookup"><span data-stu-id="8b988-169">Then copy hello output connection string and set hello `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need tooenclose hello connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="8b988-170">Todos os exemplos na Olá seções deste artigo a seguir pressupõem que você definiu Olá `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY` variáveis de ambiente.</span><span class="sxs-lookup"><span data-stu-id="8b988-170">All examples in hello following sections of this article assume that you've set hello `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="8b988-171">Criar e gerenciar blobs</span><span class="sxs-lookup"><span data-stu-id="8b988-171">Create and manage blobs</span></span>
<span data-ttu-id="8b988-172">Armazenamento de BLOBs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar Olá, mundo via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="8b988-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="8b988-173">Esta seção pressupõe que você esteja familiarizado com o conceitos de Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b988-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="8b988-174">Para obter informações detalhadas, confira [Introdução ao Armazenamento de Blobs do Azure usando o .NET](storage-dotnet-how-to-use-blobs.md) e [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts) (Conceitos do serviço Blob).</span><span class="sxs-lookup"><span data-stu-id="8b988-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="8b988-175">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="8b988-175">Create a container</span></span>
<span data-ttu-id="8b988-176">Todos os blobs no armazenamento do Azure devem residir em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="8b988-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="8b988-177">Você pode criar um contêiner usando Olá `az storage container create` comando:</span><span class="sxs-lookup"><span data-stu-id="8b988-177">You can create a container by using hello `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="8b988-178">Você pode definir um dos três níveis de acesso de leitura para um novo contêiner especificando Olá opcional `--public-access` argumento:</span><span class="sxs-lookup"><span data-stu-id="8b988-178">You can set one of three levels of read access for a new container by specifying hello optional  `--public-access` argument:</span></span>

* <span data-ttu-id="8b988-179">`off`(padrão): os dados do contêiner são privado toohello proprietário da conta.</span><span class="sxs-lookup"><span data-stu-id="8b988-179">`off` (default): Container data is private toohello account owner.</span></span>
* <span data-ttu-id="8b988-180">`blob`: acesso de leitura público para blobs.</span><span class="sxs-lookup"><span data-stu-id="8b988-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="8b988-181">`container`: Leitura e listagem acesso toohello todo contêiner público.</span><span class="sxs-lookup"><span data-stu-id="8b988-181">`container`: Public read and list access toohello entire container.</span></span>

<span data-ttu-id="8b988-182">Para obter mais informações, consulte [gerenciar o acesso de leitura anônimo toocontainers e blobs](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="8b988-182">For more information, see [Manage anonymous read access toocontainers and blobs](storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-tooa-container"></a><span data-ttu-id="8b988-183">Carregar um contêiner de blob tooa</span><span class="sxs-lookup"><span data-stu-id="8b988-183">Upload a blob tooa container</span></span>
<span data-ttu-id="8b988-184">O Armazenamento de Blobs do Azure dá suporte a blobs de blocos, anexos e páginas.</span><span class="sxs-lookup"><span data-stu-id="8b988-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="8b988-185">Carregar blobs tooa contêiner usando Olá `blob upload` comando:</span><span class="sxs-lookup"><span data-stu-id="8b988-185">Upload blobs tooa container by using hello `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="8b988-186">Por padrão, Olá `blob upload` comando carrega os blobs de toopage arquivos VHD ou outra forma de blobs de bloco.</span><span class="sxs-lookup"><span data-stu-id="8b988-186">By default, hello `blob upload` command uploads *.vhd files toopage blobs, or block blobs otherwise.</span></span> <span data-ttu-id="8b988-187">toospecify outro tipo quando você carregar um blob, você pode usar o hello `--type` argumento--os valores permitido são `append`, `block`, e `page`.</span><span class="sxs-lookup"><span data-stu-id="8b988-187">toospecify another type when you upload a blob, you can use hello `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="8b988-188">Para obter mais informações sobre tipos de blob diferente hello, consulte [Compreendendo Blobs de bloco, Blobs de acréscimo e Blobs de página](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="8b988-188">For more information on hello different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="8b988-189">Baixar um blob de um contêiner</span><span class="sxs-lookup"><span data-stu-id="8b988-189">Download a blob from a container</span></span>
<span data-ttu-id="8b988-190">Este exemplo demonstra como toodownload um blob de um contêiner:</span><span class="sxs-lookup"><span data-stu-id="8b988-190">This example demonstrates how toodownload a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="8b988-191">Saudação de listar blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="8b988-191">List hello blobs in a container</span></span>

<span data-ttu-id="8b988-192">Listar blobs Olá em um contêiner com hello [lista de blob de armazenamento az](/cli/azure/storage/blob#list) comando.</span><span class="sxs-lookup"><span data-stu-id="8b988-192">List hello blobs in a container with hello [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="8b988-193">Copiar blobs</span><span class="sxs-lookup"><span data-stu-id="8b988-193">Copy blobs</span></span>
<span data-ttu-id="8b988-194">É possível copiar blobs em ou entre regiões e contas de armazenamento de modo assíncrono.</span><span class="sxs-lookup"><span data-stu-id="8b988-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="8b988-195">Olá exemplo a seguir demonstra como blobs de toocopy do armazenamento de uma conta tooanother.</span><span class="sxs-lookup"><span data-stu-id="8b988-195">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="8b988-196">Primeiro criamos um contêiner na conta de armazenamento de origem hello, especificando o acesso de leitura público para seus blobs.</span><span class="sxs-lookup"><span data-stu-id="8b988-196">We first create a container in hello source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="8b988-197">Em seguida, podemos carregar um contêiner de toohello de arquivo e, finalmente, copiar o blob de saudação do contêiner em um contêiner na conta de armazenamento de destino hello.</span><span class="sxs-lookup"><span data-stu-id="8b988-197">Next, we upload a file toohello container, and finally, copy hello blob from that container into a container in hello destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob toocontainer in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account toodestination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="8b988-198">Em Olá exemplo acima, o contêiner de destino Olá já deve existir na conta de armazenamento de destino Olá para Olá toosucceed de operação de cópia.</span><span class="sxs-lookup"><span data-stu-id="8b988-198">In hello above example, hello destination container must already exist in hello destination storage account for hello copy operation toosucceed.</span></span> <span data-ttu-id="8b988-199">Além disso, Olá blob de origem especificado no hello `--source-uri` argumento deve incluir um token de assinatura (SAS) de acesso compartilhado ou ser acessíveis publicamente, como neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="8b988-199">Additionally, hello source blob specified in hello `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="8b988-200">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="8b988-200">Delete a blob</span></span>
<span data-ttu-id="8b988-201">toodelete um blob, use Olá `blob delete` comando:</span><span class="sxs-lookup"><span data-stu-id="8b988-201">toodelete a blob, use hello `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="8b988-202">Criar e gerenciar compartilhamentos de arquivos</span><span class="sxs-lookup"><span data-stu-id="8b988-202">Create and manage file shares</span></span>
<span data-ttu-id="8b988-203">Armazenamento de arquivo do Azure oferece armazenamento compartilhado para aplicativos que usam o protocolo de bloco de mensagens de servidor (SMB) saudação.</span><span class="sxs-lookup"><span data-stu-id="8b988-203">Azure File storage offers shared storage for applications using hello Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="8b988-204">As máquinas virtuais e os serviços de nuvem do Microsoft Azure, bem como aplicativos locais, podem compartilhar dados de arquivos por meio de compartilhamentos montados.</span><span class="sxs-lookup"><span data-stu-id="8b988-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="8b988-205">Você pode gerenciar compartilhamentos de arquivos e dados de arquivo por meio de saudação CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b988-205">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="8b988-206">Para obter mais informações sobre o armazenamento de arquivo do Azure, consulte [Introdução ao armazenamento de arquivo do Azure no Windows](storage-dotnet-how-to-use-files.md) ou [como toouse armazenamento de arquivo do Azure com Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8b988-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="8b988-207">Criar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="8b988-207">Create a file share</span></span>
<span data-ttu-id="8b988-208">Um compartilhamento de Arquivos do Azure é um compartilhamento de arquivos do SMB no Azure.</span><span class="sxs-lookup"><span data-stu-id="8b988-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="8b988-209">Todos os arquivos e diretórios devem ser criados em um compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="8b988-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="8b988-210">Uma conta pode conter um número ilimitado de compartilhamentos e um compartilhamento pode armazenar um número ilimitado de arquivos, se os limites de capacidade toohello Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="8b988-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="8b988-211">Olá, exemplo a seguir cria um compartilhamento de arquivos chamado **MeuCompartilhamento**.</span><span class="sxs-lookup"><span data-stu-id="8b988-211">hello following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="8b988-212">Criar um diretório</span><span class="sxs-lookup"><span data-stu-id="8b988-212">Create a directory</span></span>
<span data-ttu-id="8b988-213">Um diretório fornece uma estrutura hierárquica para um compartilhamento de arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b988-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="8b988-214">Olá, exemplo a seguir cria um diretório chamado **myDir** no compartilhamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="8b988-214">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="8b988-215">O caminho de um diretório pode incluir vários níveis, por exemplo **dir1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="8b988-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="8b988-216">No entanto, você deve garantir a existência de todos os diretórios pai antes de criar um subdiretório.</span><span class="sxs-lookup"><span data-stu-id="8b988-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="8b988-217">Por exemplo, para o caminho **dir1/dir2**, você deve primeiro criar o diretório **dir1**, em seguida, criar o diretório **dir2**.</span><span class="sxs-lookup"><span data-stu-id="8b988-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-tooa-share"></a><span data-ttu-id="8b988-218">Carregar um compartilhamento de arquivo local tooa</span><span class="sxs-lookup"><span data-stu-id="8b988-218">Upload a local file tooa share</span></span>
<span data-ttu-id="8b988-219">Olá, exemplo a seguir carrega um arquivo de **~/temp/samplefile.txt** tooroot de saudação **MeuCompartilhamento** compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="8b988-219">hello following example uploads a file from **~/temp/samplefile.txt** tooroot of hello **myshare** file share.</span></span> <span data-ttu-id="8b988-220">Olá `--source` argumento especifica tooupload de arquivo local existente hello.</span><span class="sxs-lookup"><span data-stu-id="8b988-220">hello `--source` argument specifies hello existing local file tooupload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="8b988-221">Assim como acontece com a criação de diretório, você pode especificar um caminho de diretório Dentro Olá compartilhamento tooupload Olá arquivo tooan diretório existente no compartilhamento de saudação:</span><span class="sxs-lookup"><span data-stu-id="8b988-221">As with directory creation, you can specify a directory path within hello share tooupload hello file tooan existing directory within hello share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="8b988-222">Pode ser um arquivo no compartilhamento de saudação até too1 TB de tamanho.</span><span class="sxs-lookup"><span data-stu-id="8b988-222">A file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-a-share"></a><span data-ttu-id="8b988-223">Listar Olá arquivos em um compartilhamento</span><span class="sxs-lookup"><span data-stu-id="8b988-223">List hello files in a share</span></span>
<span data-ttu-id="8b988-224">Você pode listar arquivos e diretórios em um compartilhamento usando Olá `az storage file list` comando:</span><span class="sxs-lookup"><span data-stu-id="8b988-224">You can list files and directories in a share by using hello `az storage file list` command:</span></span>

```azurecli
# List hello files in hello root of a share
az storage file list --share-name myshare --output table

# List hello files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List hello files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="8b988-225">Copiar arquivos</span><span class="sxs-lookup"><span data-stu-id="8b988-225">Copy files</span></span>      
<span data-ttu-id="8b988-226">Você pode copiar um arquivo de tooanother, um blob de tooa de arquivo ou um arquivo de tooa de blob.</span><span class="sxs-lookup"><span data-stu-id="8b988-226">You can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="8b988-227">Por exemplo, um arquivo tooa diretório em um compartilhamento diferente de toocopy:</span><span class="sxs-lookup"><span data-stu-id="8b988-227">For example, toocopy a file tooa directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="8b988-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8b988-228">Next steps</span></span>
<span data-ttu-id="8b988-229">Aqui estão alguns recursos adicionais para aprender mais sobre como trabalhar com hello 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b988-229">Here are some additional resources for learning more about working with hello Azure CLI 2.0.</span></span>

* [<span data-ttu-id="8b988-230">Introdução à CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8b988-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="8b988-231">Referência de comandos da CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="8b988-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="8b988-232">CLI do Azure 2.0 no GitHub</span><span class="sxs-lookup"><span data-stu-id="8b988-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
