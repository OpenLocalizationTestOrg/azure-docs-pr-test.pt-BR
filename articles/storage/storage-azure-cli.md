---
title: Uso da CLI do Azure 2.0 com o Armazenamento do Azure | Microsoft Docs
description: "Saiba como usar a CLI (Interface de Linha de Comando) do Azure 2.0 com o Armazenamento do Azure para criar e gerenciar contas de armazenamento, bem como trabalhar com blobs e arquivos do Azure. O CLI do Azure 2.0 é uma ferramenta de plataforma cruzada escrita em Python."
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
ms.openlocfilehash: 6098216f7dd901ea48fb3ab969c7934cc288b247
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-20-with-azure-storage"></a><span data-ttu-id="dce3a-104">Uso da CLI do Azure 2.0 com o Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="dce3a-104">Using the Azure CLI 2.0 with Azure Storage</span></span>

<span data-ttu-id="dce3a-105">A CLI do Azure 2.0 de software livre e plataforma cruzada fornece um conjunto de comandos para trabalhar com a Plataforma Azure.</span><span class="sxs-lookup"><span data-stu-id="dce3a-105">The open-source, cross-platform Azure CLI 2.0 provides a set of commands for working with the Azure platform.</span></span> <span data-ttu-id="dce3a-106">Ela fornece grande parte das mesmas funcionalidades encontradas no [Portal do Azure](https://portal.azure.com), incluindo acesso a dados avançado.</span><span class="sxs-lookup"><span data-stu-id="dce3a-106">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com), including rich data access.</span></span>

<span data-ttu-id="dce3a-107">Neste guia, mostraremos como usar a [CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) para executar várias tarefas ao trabalhar com recursos na sua conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce3a-107">In this guide, we show you how to use the [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2) to perform several tasks working with resources in your Azure Storage account.</span></span> <span data-ttu-id="dce3a-108">É recomendável baixar e instalar ou atualizar para a versão mais recente da CLI 2.0 antes usar este guia.</span><span class="sxs-lookup"><span data-stu-id="dce3a-108">We recommend that you download and install or upgrade to the latest version of the CLI 2.0 before using this guide.</span></span>

<span data-ttu-id="dce3a-109">Os exemplos neste guia supõem o uso do shell Bash no Ubuntu, mas outras plataformas devem funcionar de forma semelhante.</span><span class="sxs-lookup"><span data-stu-id="dce3a-109">The examples in the guide assume the use of the Bash shell on Ubuntu, but other platforms should perform similarly.</span></span> 

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="prerequisites"></a><span data-ttu-id="dce3a-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dce3a-110">Prerequisites</span></span>
<span data-ttu-id="dce3a-111">Este guia pressupõe que você conhece os conceitos básicos do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce3a-111">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="dce3a-112">Ele também pressupõe que você é capaz de satisfazer os requisitos de criação de conta especificados abaixo para o serviço do Azure e de Armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dce3a-112">It also assumes that you're able to satisfy the account creation requirements that are specified below for Azure and the Storage service.</span></span>

### <a name="accounts"></a><span data-ttu-id="dce3a-113">Contas</span><span class="sxs-lookup"><span data-stu-id="dce3a-113">Accounts</span></span>
* <span data-ttu-id="dce3a-114">**Conta do Azure**: se você ainda não tiver uma assinatura do Azure, [crie uma conta gratuita do Azure](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="dce3a-114">**Azure account**: If you don't already have an Azure subscription, [create a free Azure account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="dce3a-115">**Conta de armazenamento**: veja [Criar uma conta de armazenamento](../storage/storage-create-storage-account.md#create-a-storage-account) em [Sobre as contas de armazenamento do Azure](../storage/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="dce3a-115">**Storage account**: See [Create a storage account](../storage/storage-create-storage-account.md#create-a-storage-account) in [About Azure storage accounts](../storage/storage-create-storage-account.md).</span></span>

### <a name="install-the-azure-cli-20"></a><span data-ttu-id="dce3a-116">Instalar a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="dce3a-116">Install the Azure CLI 2.0</span></span>

<span data-ttu-id="dce3a-117">Baixe e instale a CLI do Azure 2.0 seguindo as instruções descritas em [Instalar a CLI do Azure 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="dce3a-117">Download and install the Azure CLI 2.0 by following the instructions outlined in [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

> [!TIP]
> <span data-ttu-id="dce3a-118">Se você tiver problemas com a instalação, confira a seção [Solucionando problemas de instalação](/cli/azure/install-az-cli2#installation-troubleshooting) do artigo e o guia [Solucionar Problemas de Instalação](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="dce3a-118">If you have trouble with the installation, check out the [Installation Troubleshooting](/cli/azure/install-az-cli2#installation-troubleshooting) section of the article, and the [Install Troubleshooting](https://github.com/Azure/azure-cli/blob/master/doc/install_troubleshooting.md) guide on GitHub.</span></span>
>

## <a name="working-with-the-cli"></a><span data-ttu-id="dce3a-119">Trabalhando com a CLI</span><span class="sxs-lookup"><span data-stu-id="dce3a-119">Working with the CLI</span></span>

<span data-ttu-id="dce3a-120">Depois de instalar a CLI, você poderá usar o comando `az` na sua interface de linha de comando (Bash, Terminal e Prompt de Comando) para acessar os comandos da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce3a-120">Once you've installed the CLI, you can use the `az` command in your command-line interface (Bash, Terminal, Command Prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="dce3a-121">Digite o comando `az` para ver uma lista completa dos comandos de base (a saída de exemplo a seguir foi truncada):</span><span class="sxs-lookup"><span data-stu-id="dce3a-121">Type the `az` command to see a full list of the base commands (the following example output has been truncated):</span></span>

```
     /\
    /  \    _____   _ _ __ ___
   / /\ \  |_  / | | | \'__/ _ \
  / ____ \  / /| |_| | | |  __/
 /_/    \_\/___|\__,_|_|  \___|


Welcome to the cool new Azure CLI!

Here are the base commands:

    account          : Manage subscriptions.
    acr              : Manage Azure container registries.
    acs              : Manage Azure Container Services.
    ad               : Synchronize on-premises directories and manage Azure Active Directory
                       resources.
    ...
```

<span data-ttu-id="dce3a-122">Na sua interface de linha de comando, execute o comando `az storage --help` para listar os subgrupos do comando `storage`.</span><span class="sxs-lookup"><span data-stu-id="dce3a-122">In your command-line interface, execute the command `az storage --help` to list the `storage` command subgroups.</span></span> <span data-ttu-id="dce3a-123">As descrições dos subgrupos fornecem uma visão geral da funcionalidade que a CLI do Azure fornece para trabalhar com seus recursos de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dce3a-123">The descriptions of the subgroups provide an overview of the functionality the Azure CLI provides for working with your storage resources.</span></span>

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
    file     : File shares that use the standard SMB 3.0 protocol.
    logging  : Manage Storage service logging information.
    message  : Manage queue storage messages.
    metrics  : Manage Storage service metrics.
    queue    : Use queues to effectively scale applications according to traffic.
    share    : Manage file shares.
    table    : NoSQL key-value storage using semi-structured datasets.
```

## <a name="connect-the-cli-to-your-azure-subscription"></a><span data-ttu-id="dce3a-124">Conectar a CLI à assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="dce3a-124">Connect the CLI to your Azure subscription</span></span>

<span data-ttu-id="dce3a-125">Para trabalhar com os recursos na sua assinatura do Azure, você deve primeiro fazer logon na conta do Azure com `az login`.</span><span class="sxs-lookup"><span data-stu-id="dce3a-125">To work with the resources in your Azure subscription, you must first log in to your Azure account with `az login`.</span></span> <span data-ttu-id="dce3a-126">Há várias maneiras de fazer logon:</span><span class="sxs-lookup"><span data-stu-id="dce3a-126">There are several ways you can log in:</span></span>

* <span data-ttu-id="dce3a-127">**Logon Interativo**: `az login`</span><span class="sxs-lookup"><span data-stu-id="dce3a-127">**Interactive login**: `az login`</span></span>
* <span data-ttu-id="dce3a-128">**Faça logon com o nome de usuário e senha**: `az login -u johndoe@contoso.com -p VerySecret`</span><span class="sxs-lookup"><span data-stu-id="dce3a-128">**Log in with user name and password**: `az login -u johndoe@contoso.com -p VerySecret`</span></span>
  * <span data-ttu-id="dce3a-129">Isso não funciona com contas da Microsoft ou contas que usam autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="dce3a-129">This doesn't work with Microsoft accounts or accounts that use multi-factor authentication.</span></span>
* <span data-ttu-id="dce3a-130">**Faça logon com uma entidade de serviço**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span><span class="sxs-lookup"><span data-stu-id="dce3a-130">**Log in with a service principal**: `az login --service-principal -u http://azure-cli-2016-08-05-14-31-15 -p VerySecret --tenant contoso.onmicrosoft.com`</span></span>

## <a name="azure-cli-20-sample-script"></a><span data-ttu-id="dce3a-131">Script de exemplo da CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="dce3a-131">Azure CLI 2.0 sample script</span></span>

<span data-ttu-id="dce3a-132">Em seguida, trabalharemos com um pequeno script shell que emite alguns comandos básicos da CLI do Azure 2.0 para interagir com recursos do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce3a-132">Next, we'll work with a small shell script that issues a few basic Azure CLI 2.0 commands to interact with Azure Storage resources.</span></span> <span data-ttu-id="dce3a-133">Primeiro, o script cria um novo contêiner na sua conta de armazenamento e carrega um arquivo existente (como um blob) para esse contêiner.</span><span class="sxs-lookup"><span data-stu-id="dce3a-133">The script first creates a new container in your storage account, then uploads an existing file (as a blob) to that container.</span></span> <span data-ttu-id="dce3a-134">Ele lista todos os blobs no contêiner e, por fim, baixa o arquivo para um destino no computador local que você especificar.</span><span class="sxs-lookup"><span data-stu-id="dce3a-134">It then lists all blobs in the container, and finally, downloads the file to a destination on your local computer that you specify.</span></span>

```bash
#!/bin/bash
# A simple Azure Storage example script

export AZURE_STORAGE_ACCOUNT=<storage_account_name>
export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

export container_name=<container_name>
export blob_name=<blob_name>
export file_to_upload=<file_to_upload>
export destination_file=<destination_file>

echo "Creating the container..."
az storage container create --name $container_name

echo "Uploading the file..."
az storage blob upload --container-name $container_name --file $file_to_upload --name $blob_name

echo "Listing the blobs..."
az storage blob list --container-name $container_name --output table

echo "Downloading the file..."
az storage blob download --container-name $container_name --name $blob_name --file $destination_file --output table

echo "Done"
```

<span data-ttu-id="dce3a-135">**Configurar e executar o script**</span><span class="sxs-lookup"><span data-stu-id="dce3a-135">**Configure and run the script**</span></span>

1. <span data-ttu-id="dce3a-136">Abra o editor de texto de sua preferência, e copie e cole o script anterior no editor.</span><span class="sxs-lookup"><span data-stu-id="dce3a-136">Open your favorite text editor, then copy and paste the preceding script into the editor.</span></span>

2. <span data-ttu-id="dce3a-137">Em seguida, atualize as variáveis do script para refletir suas configurações.</span><span class="sxs-lookup"><span data-stu-id="dce3a-137">Next, update the script's variables to reflect your configuration settings.</span></span> <span data-ttu-id="dce3a-138">Substitua os seguintes valores conforme especificado:</span><span class="sxs-lookup"><span data-stu-id="dce3a-138">Replace the following values as specified:</span></span>

   * <span data-ttu-id="dce3a-139">**\<storage_account_name\>** O nome da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dce3a-139">**\<storage_account_name\>** The name of your storage account.</span></span>
   * <span data-ttu-id="dce3a-140">**\<storage_account_key\>** A tecla de acesso primária ou secundária para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dce3a-140">**\<storage_account_key\>** The primary or secondary access key for your storage account.</span></span>
   * <span data-ttu-id="dce3a-141">**\<container_name\>** Um nome para o novo contêiner que será criado, como “azure-cli-sample-container”.</span><span class="sxs-lookup"><span data-stu-id="dce3a-141">**\<container_name\>** A name the new container to create, such as "azure-cli-sample-container".</span></span>
   * <span data-ttu-id="dce3a-142">**\<blob_name\>** Um nome para o blob de destino no contêiner.</span><span class="sxs-lookup"><span data-stu-id="dce3a-142">**\<blob_name\>** A name for the destination blob in the container.</span></span>
   * <span data-ttu-id="dce3a-143">**\<file_to_upload\>** O caminho para o pequeno arquivo no seu computador local, tal como “~/images/HelloWorld.png”.</span><span class="sxs-lookup"><span data-stu-id="dce3a-143">**\<file_to_upload\>** The path to small file on your local computer, such as "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="dce3a-144">**\<destination_file\>** O caminho do arquivo de destino, como “~/downloadedImage.png”.</span><span class="sxs-lookup"><span data-stu-id="dce3a-144">**\<destination_file\>** The destination file path, such as "~/downloadedImage.png".</span></span>

3. <span data-ttu-id="dce3a-145">Depois de atualizar as variáveis necessárias, salve o script e sair do editor.</span><span class="sxs-lookup"><span data-stu-id="dce3a-145">After you've updated the necessary variables, save the script and exit your editor.</span></span> <span data-ttu-id="dce3a-146">As próximas etapas pressupõem que você nomeou seu script como **my_storage_sample.sh**.</span><span class="sxs-lookup"><span data-stu-id="dce3a-146">The next steps assume you've named your script **my_storage_sample.sh**.</span></span>

4. <span data-ttu-id="dce3a-147">Marque o script como executável, se necessário: `chmod +x my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="dce3a-147">Mark the script as executable, if necessary: `chmod +x my_storage_sample.sh`</span></span>

5. <span data-ttu-id="dce3a-148">Execute o script.</span><span class="sxs-lookup"><span data-stu-id="dce3a-148">Execute the script.</span></span> <span data-ttu-id="dce3a-149">Por exemplo, no Bash:`./my_storage_sample.sh`</span><span class="sxs-lookup"><span data-stu-id="dce3a-149">For example, in Bash: `./my_storage_sample.sh`</span></span>

<span data-ttu-id="dce3a-150">Você deverá ver uma saída semelhante à seguinte e o **\<destination_file\>** especificado no script deve aparecer no computador local.</span><span class="sxs-lookup"><span data-stu-id="dce3a-150">You should see output similar to the following, and the **\<destination_file\>** you specified in the script should appear on your local computer.</span></span>

```
Creating the container...
{
  "created": true
}
Uploading the file...
Percent complete: %100.0
Listing the blobs...
Name       Blob Type      Length  Content Type              Last Modified
---------  -----------  --------  ------------------------  -------------------------
README.md  BlockBlob        6700  application/octet-stream  2017-05-12T20:54:59+00:00
Downloading the file...
Name
---------
README.md
Done
```

> [!TIP]
> <span data-ttu-id="dce3a-151">A saída anterior está no formato de **tabela**.</span><span class="sxs-lookup"><span data-stu-id="dce3a-151">The preceding output is in **table** format.</span></span> <span data-ttu-id="dce3a-152">Você pode especificar qual formato de saída deve ser usado definindo o argumento `--output` nos comandos da sua CLI ou defina-o globalmente usando `az configure`.</span><span class="sxs-lookup"><span data-stu-id="dce3a-152">You can specify which output format to use by specifying the `--output` argument in your CLI commands, or set it globally using `az configure`.</span></span>
>

## <a name="manage-storage-accounts"></a><span data-ttu-id="dce3a-153">Gerenciar contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="dce3a-153">Manage storage accounts</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="dce3a-154">Criar uma nova conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="dce3a-154">Create a new storage account</span></span>
<span data-ttu-id="dce3a-155">Para usar o Armazenamento do Azure, você precisa de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dce3a-155">To use Azure Storage, you need a storage account.</span></span> <span data-ttu-id="dce3a-156">Depois de configurar seu computador para se [conectar à sua assinatura](#connect-to-your-azure-subscription), você pode criar uma nova conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce3a-156">You can create a new Azure Storage account after you've configured your computer to [connect to your subscription](#connect-to-your-azure-subscription).</span></span>

```azurecli
az storage account create \
    --location <location> \
    --name <account_name> \
    --resource-group <resource_group> \
    --sku <account_sku>
```

* <span data-ttu-id="dce3a-157">`--location` [Obrigatório]: local.</span><span class="sxs-lookup"><span data-stu-id="dce3a-157">`--location` [Required]: Location.</span></span> <span data-ttu-id="dce3a-158">Por exemplo, “Oeste dos EUA”.</span><span class="sxs-lookup"><span data-stu-id="dce3a-158">For example, "West US".</span></span>
* <span data-ttu-id="dce3a-159">`--name` [Obrigatório]: o nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dce3a-159">`--name` [Required]: The storage account name.</span></span> <span data-ttu-id="dce3a-160">O nome deve conter entre 3 e 24 caracteres, usando apenas alfanuméricos minúsculo.</span><span class="sxs-lookup"><span data-stu-id="dce3a-160">The name must be 3 to 24 characters in length, and use only lowercase alphanumeric characters.</span></span>
* <span data-ttu-id="dce3a-161">`--resource-group` [Obrigatório]: nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dce3a-161">`--resource-group` [Required]: Name of resource group.</span></span>
* <span data-ttu-id="dce3a-162">`--sku` [Obrigatório]: o SKU da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dce3a-162">`--sku` [Required]: The storage account SKU.</span></span> <span data-ttu-id="dce3a-163">Valores permitidos:</span><span class="sxs-lookup"><span data-stu-id="dce3a-163">Allowed values:</span></span>
  * `Premium_LRS`
  * `Standard_GRS`
  * `Standard_LRS`
  * `Standard_RAGRS`
  * `Standard_ZRS`

### <a name="set-default-azure-storage-account-environment-variables"></a><span data-ttu-id="dce3a-164">Definir as variáveis de ambiente da conta de armazenamento padrão do Azure</span><span class="sxs-lookup"><span data-stu-id="dce3a-164">Set default Azure storage account environment variables</span></span>
<span data-ttu-id="dce3a-165">Você pode ter várias contas de armazenamento na sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce3a-165">You can have multiple storage accounts in your Azure subscription.</span></span> <span data-ttu-id="dce3a-166">Para selecionar uma delas para usar em todos os comandos de armazenamento posteriores, você pode definir essas variáveis de ambiente:</span><span class="sxs-lookup"><span data-stu-id="dce3a-166">To select one of them to use for all subsequent storage commands, you can set these environment variables:</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="dce3a-167">Outra forma de definir uma conta de armazenamento padrão é usar a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="dce3a-167">Another way to set a default storage account is by using a connection string.</span></span> <span data-ttu-id="dce3a-168">Em primeiro lugar, obtenha a cadeia de conexão com o comando `show-connection-string`:</span><span class="sxs-lookup"><span data-stu-id="dce3a-168">First, get the connection string with the `show-connection-string` command:</span></span>

```azurecli
az storage account show-connection-string \
    --name <account_name> \
    --resource-group <resource_group>
```

<span data-ttu-id="dce3a-169">Em seguida, copie a cadeia de conexão de saída e defina a variável de ambiente `AZURE_STORAGE_CONNECTION_STRING` (pode ser necessário circunscrever a cadeia de conexão entre aspas):</span><span class="sxs-lookup"><span data-stu-id="dce3a-169">Then copy the output connection string and set the `AZURE_STORAGE_CONNECTION_STRING` environment variable (you might need to enclose the connection string in quotes):</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING="<connection_string>"
```

> [!NOTE]
> <span data-ttu-id="dce3a-170">Todos os exemplos nas seções a seguir deste artigo pressupõem que você definiu as variáveis de ambiente `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY`.</span><span class="sxs-lookup"><span data-stu-id="dce3a-170">All examples in the following sections of this article assume that you've set the `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY` environment variables.</span></span>
>

## <a name="create-and-manage-blobs"></a><span data-ttu-id="dce3a-171">Criar e gerenciar blobs</span><span class="sxs-lookup"><span data-stu-id="dce3a-171">Create and manage blobs</span></span>
<span data-ttu-id="dce3a-172">O Armazenamento de Blobs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar do mundo por meio de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="dce3a-172">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="dce3a-173">Esta seção pressupõe que você esteja familiarizado com o conceitos de Armazenamento de Blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce3a-173">This section assumes that you are already familiar with Azure Blob storage concepts.</span></span> <span data-ttu-id="dce3a-174">Para obter informações detalhadas, confira [Introdução ao Armazenamento de Blobs do Azure usando o .NET](storage-dotnet-how-to-use-blobs.md) e [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts) (Conceitos do serviço Blob).</span><span class="sxs-lookup"><span data-stu-id="dce3a-174">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](/rest/api/storageservices/blob-service-concepts).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="dce3a-175">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="dce3a-175">Create a container</span></span>
<span data-ttu-id="dce3a-176">Todos os blobs no armazenamento do Azure devem residir em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="dce3a-176">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="dce3a-177">Você pode criar um contêiner usando o comando `az storage container create`:</span><span class="sxs-lookup"><span data-stu-id="dce3a-177">You can create a container by using the `az storage container create` command:</span></span>

```azurecli
az storage container create --name <container_name>
```

<span data-ttu-id="dce3a-178">Você pode definir um dos três níveis de acesso de leitura para um novo contêiner especificando o argumento `--public-access` opcional:</span><span class="sxs-lookup"><span data-stu-id="dce3a-178">You can set one of three levels of read access for a new container by specifying the optional  `--public-access` argument:</span></span>

* <span data-ttu-id="dce3a-179">`off` (padrão): os dados do contêiner são privados para o proprietário da conta.</span><span class="sxs-lookup"><span data-stu-id="dce3a-179">`off` (default): Container data is private to the account owner.</span></span>
* <span data-ttu-id="dce3a-180">`blob`: acesso de leitura público para blobs.</span><span class="sxs-lookup"><span data-stu-id="dce3a-180">`blob`: Public read access for blobs.</span></span>
* <span data-ttu-id="dce3a-181">`container`: acesso de leitura e listagem público para todo o contêiner.</span><span class="sxs-lookup"><span data-stu-id="dce3a-181">`container`: Public read and list access to the entire container.</span></span>

<span data-ttu-id="dce3a-182">Para obter mais informações, consulte [Gerenciar acesso anônimo de leitura aos contêineres e blobs](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="dce3a-182">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>

### <a name="upload-a-blob-to-a-container"></a><span data-ttu-id="dce3a-183">Carregar um blob para um contêiner</span><span class="sxs-lookup"><span data-stu-id="dce3a-183">Upload a blob to a container</span></span>
<span data-ttu-id="dce3a-184">O Armazenamento de Blobs do Azure dá suporte a blobs de blocos, anexos e páginas.</span><span class="sxs-lookup"><span data-stu-id="dce3a-184">Azure Blob storage supports block, append, and page blobs.</span></span> <span data-ttu-id="dce3a-185">Carregue os blobs para um contêiner usando o comando `blob upload`:</span><span class="sxs-lookup"><span data-stu-id="dce3a-185">Upload blobs to a container by using the `blob upload` command:</span></span>

```azurecli
az storage blob upload \
    --file <local_file_path> \
    --container-name <container_name> \
    --name <blob_name>
```

 <span data-ttu-id="dce3a-186">Por padrão, o comando `blob upload` carrega os arquivos de *.vhd para blobs de página ou para blobs de blocos.</span><span class="sxs-lookup"><span data-stu-id="dce3a-186">By default, the `blob upload` command uploads *.vhd files to page blobs, or block blobs otherwise.</span></span> <span data-ttu-id="dce3a-187">Para especificar outro tipo ao carregar um blob, você pode usar o argumento `--type`; os valores permitido são `append`, `block` e `page`.</span><span class="sxs-lookup"><span data-stu-id="dce3a-187">To specify another type when you upload a blob, you can use the `--type` argument--allowed values are `append`, `block`, and `page`.</span></span>

 <span data-ttu-id="dce3a-188">Para obter mais informações sobre os blobs, consulte [Compreendendo os Blobs de Blocos, Anexos e Páginas](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span><span class="sxs-lookup"><span data-stu-id="dce3a-188">For more information on the different blob types, see [Understanding Block Blobs, Append Blobs, and Page Blobs](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs).</span></span>


### <a name="download-a-blob-from-a-container"></a><span data-ttu-id="dce3a-189">Baixar um blob de um contêiner</span><span class="sxs-lookup"><span data-stu-id="dce3a-189">Download a blob from a container</span></span>
<span data-ttu-id="dce3a-190">Este exemplo demonstra como baixar blobs de um contêiner:</span><span class="sxs-lookup"><span data-stu-id="dce3a-190">This example demonstrates how to download a blob from a container:</span></span>

```azurecli
az storage blob download \
    --container-name mycontainer \
    --name myblob.png \
    --file ~/mydownloadedblob.png
```

### <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="dce3a-191">Listar os blobs em um contêiner</span><span class="sxs-lookup"><span data-stu-id="dce3a-191">List the blobs in a container</span></span>

<span data-ttu-id="dce3a-192">Liste os blobs em um contêiner com o comando [az storage blob list](/cli/azure/storage/blob#list).</span><span class="sxs-lookup"><span data-stu-id="dce3a-192">List the blobs in a container with the [az storage blob list](/cli/azure/storage/blob#list) command.</span></span>

```azurecli
az storage blob list \
    --container-name mycontainer \
    --output table
```

### <a name="copy-blobs"></a><span data-ttu-id="dce3a-193">Copiar blobs</span><span class="sxs-lookup"><span data-stu-id="dce3a-193">Copy blobs</span></span>
<span data-ttu-id="dce3a-194">É possível copiar blobs em ou entre regiões e contas de armazenamento de modo assíncrono.</span><span class="sxs-lookup"><span data-stu-id="dce3a-194">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="dce3a-195">O exemplo a seguir demonstra como copiar blobs de uma conta de armazenamento para outra.</span><span class="sxs-lookup"><span data-stu-id="dce3a-195">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="dce3a-196">Primeiro, criamos um contêiner na conta de armazenamento de origem, especificando o acesso de leitura público para seus blobs.</span><span class="sxs-lookup"><span data-stu-id="dce3a-196">We first create a container in the source storage account, specifying public read-access for its blobs.</span></span> <span data-ttu-id="dce3a-197">Em seguida, carregue um arquivo para o contêiner e, finalmente, copie o blob desse contêiner para um contêiner na conta de armazenamento de destino.</span><span class="sxs-lookup"><span data-stu-id="dce3a-197">Next, we upload a file to the container, and finally, copy the blob from that container into a container in the destination storage account.</span></span>

```azurecli
# Create container in source account
az storage container create \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --name sourcecontainer \
    --public-access blob

# Upload blob to container in source account
az storage blob upload \
    --account-name sourceaccountname \
    --account-key sourceaccountkey \
    --container-name sourcecontainer \
    --file ~/Pictures/sourcefile.png \
    --name sourcefile.png

# Copy blob from source account to destination account (destcontainer must exist)
az storage blob copy start \
    --account-name destaccountname \
    --account-key destaccountkey \
    --destination-blob destfile.png \
    --destination-container destcontainer \
    --source-uri https://sourceaccountname.blob.core.windows.net/sourcecontainer/sourcefile.png
```

<span data-ttu-id="dce3a-198">No exemplo acima, o contêiner de destino já deve existir na conta de armazenamento de destino para que a operação de cópia seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="dce3a-198">In the above example, the destination container must already exist in the destination storage account for the copy operation to succeed.</span></span> <span data-ttu-id="dce3a-199">Além disso, o blob de origem especificado no argumento `--source-uri` deve incluir um token SAS (Assinatura de Acesso Compartilhado) ou ser acessível ao público, como neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="dce3a-199">Additionally, the source blob specified in the `--source-uri` argument must either include a shared access signature (SAS) token, or be publicly accessible, as in this example.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="dce3a-200">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="dce3a-200">Delete a blob</span></span>
<span data-ttu-id="dce3a-201">Para excluir um blob, use o comando `blob delete`:</span><span class="sxs-lookup"><span data-stu-id="dce3a-201">To delete a blob, use the `blob delete` command:</span></span>

```azurecli
az storage blob delete --container-name <container_name> --name <blob_name>
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="dce3a-202">Criar e gerenciar compartilhamentos de arquivos</span><span class="sxs-lookup"><span data-stu-id="dce3a-202">Create and manage file shares</span></span>
<span data-ttu-id="dce3a-203">O Armazenamento de Arquivos do Azure oferece armazenamento compartilhado para aplicativos que usam o protocolo SMB.</span><span class="sxs-lookup"><span data-stu-id="dce3a-203">Azure File storage offers shared storage for applications using the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="dce3a-204">As máquinas virtuais e os serviços de nuvem do Microsoft Azure, bem como aplicativos locais, podem compartilhar dados de arquivos por meio de compartilhamentos montados.</span><span class="sxs-lookup"><span data-stu-id="dce3a-204">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="dce3a-205">Você pode gerenciar compartilhamentos de arquivos e dados de arquivos por meio da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce3a-205">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="dce3a-206">Para obter mais informações sobre o Armazenamento de Arquivos do Azure, confira [Introdução ao Armazenamento de Arquivos do Azure no Windows](storage-dotnet-how-to-use-files.md) ou [Como usar o Armazenamento de Arquivos do Azure com o Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="dce3a-206">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="dce3a-207">Criar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="dce3a-207">Create a file share</span></span>
<span data-ttu-id="dce3a-208">Um compartilhamento de Arquivos do Azure é um compartilhamento de arquivos do SMB no Azure.</span><span class="sxs-lookup"><span data-stu-id="dce3a-208">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="dce3a-209">Todos os arquivos e diretórios devem ser criados em um compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="dce3a-209">All directories and files must be created in a file share.</span></span> <span data-ttu-id="dce3a-210">Uma conta de armazenamento pode conter um número ilimitado de compartilhamentos, e um compartilhamento pode conter um número ilimitado de arquivos, até os limites de capacidade da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="dce3a-210">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="dce3a-211">O exemplo a seguir cria um compartilhamento de arquivos denominado **myshare**.</span><span class="sxs-lookup"><span data-stu-id="dce3a-211">The following example creates a file share named **myshare**.</span></span>

```azurecli
az storage share create --name myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="dce3a-212">Criar um diretório</span><span class="sxs-lookup"><span data-stu-id="dce3a-212">Create a directory</span></span>
<span data-ttu-id="dce3a-213">Um diretório fornece uma estrutura hierárquica para um compartilhamento de arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="dce3a-213">A directory provides a hierarchical structure in an Azure file share.</span></span> <span data-ttu-id="dce3a-214">O exemplo a seguir cria um diretório denominado **myDir** no compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="dce3a-214">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
az storage directory create --name myDir --share-name myshare
```

<span data-ttu-id="dce3a-215">O caminho de um diretório pode incluir vários níveis, por exemplo **dir1/dir2**.</span><span class="sxs-lookup"><span data-stu-id="dce3a-215">A directory path can include multiple levels, for example **dir1/dir2**.</span></span> <span data-ttu-id="dce3a-216">No entanto, você deve garantir a existência de todos os diretórios pai antes de criar um subdiretório.</span><span class="sxs-lookup"><span data-stu-id="dce3a-216">However, you must ensure that all parent directories exist before creating a subdirectory.</span></span> <span data-ttu-id="dce3a-217">Por exemplo, para o caminho **dir1/dir2**, você deve primeiro criar o diretório **dir1**, em seguida, criar o diretório **dir2**.</span><span class="sxs-lookup"><span data-stu-id="dce3a-217">For example, for path **dir1/dir2**, you must first create directory **dir1**, then create directory **dir2**.</span></span>

### <a name="upload-a-local-file-to-a-share"></a><span data-ttu-id="dce3a-218">Carregar um arquivo local para um compartilhamento</span><span class="sxs-lookup"><span data-stu-id="dce3a-218">Upload a local file to a share</span></span>
<span data-ttu-id="dce3a-219">O exemplo a seguir carrega um arquivo de **~/temp/samplefile.txt** para a raiz do compartilhamento de arquivos **myshare**.</span><span class="sxs-lookup"><span data-stu-id="dce3a-219">The following example uploads a file from **~/temp/samplefile.txt** to root of the **myshare** file share.</span></span> <span data-ttu-id="dce3a-220">O argumento `--source` especifica o arquivo local existente para o upload.</span><span class="sxs-lookup"><span data-stu-id="dce3a-220">The `--source` argument specifies the existing local file to upload.</span></span>

```azurecli
az storage file upload --share-name myshare --source ~/temp/samplefile.txt
```

<span data-ttu-id="dce3a-221">Assim como na criação do diretório, você pode especificar um caminho de diretório no compartilhamento para carregar o arquivo para um diretório existente dentro do compartilhamento:</span><span class="sxs-lookup"><span data-stu-id="dce3a-221">As with directory creation, you can specify a directory path within the share to upload the file to an existing directory within the share:</span></span>

```azurecli
az storage file upload --share-name myshare/myDir --source ~/temp/samplefile.txt
```

<span data-ttu-id="dce3a-222">Um arquivo no compartilhamento pode ter até 1 TB.</span><span class="sxs-lookup"><span data-stu-id="dce3a-222">A file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-a-share"></a><span data-ttu-id="dce3a-223">Listar os arquivos em um compartilhamento</span><span class="sxs-lookup"><span data-stu-id="dce3a-223">List the files in a share</span></span>
<span data-ttu-id="dce3a-224">Você pode listar arquivos e diretórios em um compartilhamento usando o comando `az storage file list`:</span><span class="sxs-lookup"><span data-stu-id="dce3a-224">You can list files and directories in a share by using the `az storage file list` command:</span></span>

```azurecli
# List the files in the root of a share
az storage file list --share-name myshare --output table

# List the files in a directory within a share
az storage file list --share-name myshare/myDir --output table

# List the files in a path within a share
az storage file list --share-name myshare --path myDir/mySubDir/MySubDir2 --output table
```

### <a name="copy-files"></a><span data-ttu-id="dce3a-225">Copiar arquivos</span><span class="sxs-lookup"><span data-stu-id="dce3a-225">Copy files</span></span>      
<span data-ttu-id="dce3a-226">Você pode copiar um arquivo para outro arquivo, um arquivo para um blob ou um blob para um arquivo.</span><span class="sxs-lookup"><span data-stu-id="dce3a-226">You can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="dce3a-227">Por exemplo, para copiar um arquivo para um diretório em um compartilhamento diferente:</span><span class="sxs-lookup"><span data-stu-id="dce3a-227">For example, to copy a file to a directory in a different share:</span></span>        
        
```azurecli
az storage file copy start \
--source-share share1 --source-path dir1/file.txt \
--destination-share share2 --destination-path dir2/file.txt     
```

## <a name="next-steps"></a><span data-ttu-id="dce3a-228">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dce3a-228">Next steps</span></span>
<span data-ttu-id="dce3a-229">Veja alguns recursos adicionais para aprender mais sobre como trabalhar com a CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="dce3a-229">Here are some additional resources for learning more about working with the Azure CLI 2.0.</span></span>

* [<span data-ttu-id="dce3a-230">Introdução à CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="dce3a-230">Get started with Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/get-started-with-az-cli2)
* [<span data-ttu-id="dce3a-231">Referência de comandos da CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="dce3a-231">Azure CLI 2.0 command reference</span></span>](/cli/azure)
* [<span data-ttu-id="dce3a-232">CLI do Azure 2.0 no GitHub</span><span class="sxs-lookup"><span data-stu-id="dce3a-232">Azure CLI 2.0 on GitHub</span></span>](https://github.com/Azure/azure-cli)
