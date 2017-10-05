---
title: Usando a CLI 1.0 do Azure com o Armazenamento do Azure | Microsoft Docs
description: "Saiba como usar a CLI (Interface de Linha de Comando) 1.0 do Azure com o Armazenamento do Azure para criar e gerenciar contas de armazenamento, bem como trabalhar com blobs e arquivos do Azure. A CLI do Azure é uma ferramenta de plataforma cruzada"
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: b502232a-e8f6-4d6c-befd-3476592e0e35
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/30/2017
ms.author: seguler
ms.openlocfilehash: b246d8813a41d353a9c0fa31fe838e025fc93046
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="using-the-azure-cli-10-with-azure-storage"></a><span data-ttu-id="cb482-104">Usando a CLI 1.0 do Azure com o Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="cb482-104">Using the Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="cb482-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="cb482-105">Overview</span></span>

<span data-ttu-id="cb482-106">A CLI do Azure fornece um conjunto de comandos entre plataformas de software livre para trabalhar com a Plataforma Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-106">The Azure CLI provides a set of open source, cross-platform commands for working with the Azure Platform.</span></span> <span data-ttu-id="cb482-107">Ela fornece grande parte das mesmas funcionalidades encontradas no [Portal do Azure](https://portal.azure.com) , bem como funcionalidades avançadas de acesso a dados.</span><span class="sxs-lookup"><span data-stu-id="cb482-107">It provides much of the same functionality found in the [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="cb482-108">Neste guia, exploraremos como usar a [CLI (Interface de Linha de Comando) do Azure](../cli-install-nodejs.md) para executar uma variedade de tarefas de administração e desenvolvimento com o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-108">In this guide, we'll explore how to use [Azure Command-Line Interface (Azure CLI)](../cli-install-nodejs.md) to perform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="cb482-109">É recomendável baixar e instalar ou atualizar para a CLI mais recente do Azure antes usar este guia.</span><span class="sxs-lookup"><span data-stu-id="cb482-109">We recommend that you download and install or upgrade to the latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="cb482-110">Este guia pressupõe que você conhece os conceitos básicos do Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-110">This guide assumes that you understand the basic concepts of Azure Storage.</span></span> <span data-ttu-id="cb482-111">Este guia fornece vários scripts que demonstram o uso da CLI do Azure com o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-111">The guide provides a number of scripts to demonstrate the usage of the Azure CLI with Azure Storage.</span></span> <span data-ttu-id="cb482-112">Não se esqueça de atualizar as variáveis de script com base na sua configuração antes de executar cada script.</span><span class="sxs-lookup"><span data-stu-id="cb482-112">Be sure to update the script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="cb482-113">O guia fornece exemplos de comando e scripts da CLI do Azure para contas de armazenamento clássico.</span><span class="sxs-lookup"><span data-stu-id="cb482-113">The guide provides the Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="cb482-114">Consulte [Usando a CLI do Azure para Mac, Linux e Windows com o Gerenciamento de Recursos do Azure](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) para ver comandos da CLI do Azure para contas de armazenamento do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cb482-114">See [Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-the-azure-cli-in-5-minutes"></a><span data-ttu-id="cb482-115">Introdução ao Armazenamento do Azure e à CLI do Azure em 5 minutos</span><span class="sxs-lookup"><span data-stu-id="cb482-115">Get started with Azure Storage and the Azure CLI in 5 minutes</span></span>
<span data-ttu-id="cb482-116">Nos exemplos deste guia, usamos o Ubuntu, mas outras plataformas de sistema operacional devem funcionar de forma semelhante.</span><span class="sxs-lookup"><span data-stu-id="cb482-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="cb482-117">**Novo no Azure:** obtenha uma assinatura do Microsoft Azure e uma conta da Microsoft associada a essa assinatura.</span><span class="sxs-lookup"><span data-stu-id="cb482-117">**New to Azure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="cb482-118">Para saber mais sobre as opções de compra do Azure, confira [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/), [Opções de compra](https://azure.microsoft.com/pricing/purchase-options/) e [Ofertas para membros](https://azure.microsoft.com/pricing/member-offers/) (para membros do MSDN, Microsoft Partner Network e BizSpark, entre outros programas da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="cb482-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="cb482-119">Consulte [Atribuindo funções de administrador no Azure AD (Azure Active Directory)](https://msdn.microsoft.com/library/azure/hh531793.aspx) para obter mais informações sobre as assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="cb482-120">**Depois de criar uma assinatura e conta do Microsoft Azure:**</span><span class="sxs-lookup"><span data-stu-id="cb482-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="cb482-121">Baixe e instale a CLI do Azure seguindo as instruções descritas em [Instalar a CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="cb482-121">Download and install the Azure CLI following the instructions outlined in [Install the Azure CLI](../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="cb482-122">Quando a CLI do Azure estiver instalada, você poderá usar o comando azure na sua interface de linha de comando (Bash, Terminal, Prompt de comando) para acessar os comandos da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-122">Once the Azure CLI has been installed, you will be able to use the azure command from your command-line interface (Bash, Terminal, Command prompt) to access the Azure CLI commands.</span></span> <span data-ttu-id="cb482-123">Digite o comando _azure_ e você deverá ver a saída a seguir.</span><span class="sxs-lookup"><span data-stu-id="cb482-123">Type the _azure_ command and you should see the following output.</span></span>

    ![Saída de comando do Azure][Image1]
3. <span data-ttu-id="cb482-125">Na interface de linha de comando, digite `azure storage` para listar todos os comandos de armazenamento do Azure e obter uma primeira impressão das funcionalidades fornecidas pela CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-125">In the command-line interface, type `azure storage` to list out all the azure storage commands and get a first impression of the functionalities the Azure CLI provides.</span></span> <span data-ttu-id="cb482-126">Você pode digitar o nome do comando com o parâmetro **-h** (por exemplo, `azure storage share create -h`) para ver os detalhes da sintaxe do comando.</span><span class="sxs-lookup"><span data-stu-id="cb482-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) to see details of command syntax.</span></span>
4. <span data-ttu-id="cb482-127">Agora, você terá um script simples que mostra os comandos básicos da CLI do Azure para acessar o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-127">Now, we'll give you a simple script that shows basic Azure CLI commands to access Azure Storage.</span></span> <span data-ttu-id="cb482-128">Primeiramente, o script solicitará que você defina duas variáveis para sua conta e chave de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cb482-128">The script will first ask you to set two variables for your storage account and key.</span></span> <span data-ttu-id="cb482-129">Em seguida, o script criará um novo contêiner nessa nova conta de armazenamento e carregará um arquivo de imagem existente (blob) nesse contêiner.</span><span class="sxs-lookup"><span data-stu-id="cb482-129">Then, the script will create a new container in this new storage account and upload an existing image file (blob) to that container.</span></span> <span data-ttu-id="cb482-130">Depois que o script listar todos os blobs nesse contêiner, ele baixará o arquivo de imagem no diretório de destino, que existe no computador local.</span><span class="sxs-lookup"><span data-stu-id="cb482-130">After the script lists all blobs in that container, it will download the image file to the destination directory which exists on the local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating the container..."
    azure storage container create $container_name

    echo "Uploading the image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing the blobs..."
    azure storage blob list $container_name

    echo "Downloading the image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="cb482-131">No computador local, abra o editor de texto de sua preferência (vim, por exemplo).</span><span class="sxs-lookup"><span data-stu-id="cb482-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="cb482-132">Digite o script acima no editor de texto.</span><span class="sxs-lookup"><span data-stu-id="cb482-132">Type the above script into your text editor.</span></span>
6. <span data-ttu-id="cb482-133">Agora, você precisa atualizar as variáveis de script com base nas suas configurações.</span><span class="sxs-lookup"><span data-stu-id="cb482-133">Now, you need to update the script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="cb482-134">**<nome_da_conta_de_armazenamento>** Use o nome fornecido no script ou insira um novo nome para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cb482-134">**<storage_account_name>** Use the given name in the script or enter a new name for your storage account.</span></span> <span data-ttu-id="cb482-135">**Importante:** o nome da conta de armazenamento deve ser exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-135">**Important:** The name of the storage account must be unique in Azure.</span></span> <span data-ttu-id="cb482-136">Ele também deve ter somente letras minúsculas!</span><span class="sxs-lookup"><span data-stu-id="cb482-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="cb482-137">**<chave_da_conta_de_armazenamento>** A chave de acesso da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cb482-137">**<storage_account_key>** The access key of your storage account.</span></span>
   * <span data-ttu-id="cb482-138">**<nome_do_contêiner>** Use o nome fornecido no script ou insira um novo nome para o contêiner.</span><span class="sxs-lookup"><span data-stu-id="cb482-138">**<container_name>** Use the given name in the script or enter a new name for your container.</span></span>
   * <span data-ttu-id="cb482-139">**<imagem_a_ser_carregada>** Insira um caminho para uma imagem em seu computador local, como: "~/images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="cb482-139">**<image_to_upload>** Enter a path to a picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="cb482-140">**<pasta_de_destino>** Insira um caminho para um diretório local de modo a armazenar os arquivos baixados do Armazenamento do Azure, como: "~/downloadImages".</span><span class="sxs-lookup"><span data-stu-id="cb482-140">**<destination_folder>** Enter a path to a local directory to store files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="cb482-141">Depois de atualizar as variáveis necessárias no vim, pressione as combinações de teclas `ESC`, `:`, `wq!` para salvar o script.</span><span class="sxs-lookup"><span data-stu-id="cb482-141">After you've updated the necessary variables in vim, press key combinations `ESC`, `:`, `wq!` to save the script.</span></span>
8. <span data-ttu-id="cb482-142">Para executar esse script, basta digitar o nome do arquivo de script no console do bash.</span><span class="sxs-lookup"><span data-stu-id="cb482-142">To run this script, simply type the script file name in the bash console.</span></span> <span data-ttu-id="cb482-143">Após execução desse script, você deverá ter uma pasta de destino local que inclua o arquivo de imagem baixado.</span><span class="sxs-lookup"><span data-stu-id="cb482-143">After this script runs, you should have a local destination folder that includes the downloaded image file.</span></span> <span data-ttu-id="cb482-144">A captura de tela a seguir mostra um exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="cb482-144">The following screenshot shows an example output:</span></span>

<span data-ttu-id="cb482-145">Depois que o script é executado, você deve ter uma pasta de destino que inclui o arquivo de imagem baixada.</span><span class="sxs-lookup"><span data-stu-id="cb482-145">After the script runs, you should have a local destination folder that includes the downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-the-azure-cli"></a><span data-ttu-id="cb482-146">Gerenciar contas de armazenamento com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="cb482-146">Manage storage accounts with the Azure CLI</span></span>
### <a name="connect-to-your-azure-subscription"></a><span data-ttu-id="cb482-147">Conecte-se à sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="cb482-147">Connect to your Azure subscription</span></span>
<span data-ttu-id="cb482-148">Embora a maioria dos comandos de armazenamento funcione sem uma assinatura do Azure, é recomendável se conectar à sua assinatura na CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-148">While most of the storage commands will work without an Azure subscription, we recommend you to connect to your subscription from the Azure CLI.</span></span> <span data-ttu-id="cb482-149">Para configurar a CLI do Azure para trabalhar com sua assinatura, siga as etapas em [Conectar uma assinatura do Azure da CLI do Azure](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="cb482-149">To configure the Azure CLI to work with your subscription, follow the steps in [Connect to an Azure subscription from the Azure CLI](../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="cb482-150">Criar uma nova conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="cb482-150">Create a new storage account</span></span>
<span data-ttu-id="cb482-151">Você precisa de uma conta de armazenamento para usar o Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-151">To use Azure storage, you will need a storage account.</span></span> <span data-ttu-id="cb482-152">Depois de configurar seu computador para se conectar à sua assinatura, você pode criar uma nova conta de Armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-152">You can create a new Azure storage account after you have configured your computer to connect to your subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="cb482-153">O nome da conta de armazenamento deve ter entre 3 e 24 caracteres, usar números e apenas letras minúsculas.</span><span class="sxs-lookup"><span data-stu-id="cb482-153">The name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="cb482-154">Definir uma conta de armazenamento padrão do Azure nas variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="cb482-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="cb482-155">Você pode ter várias contas de armazenamento na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="cb482-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="cb482-156">É possível escolher uma delas e defini-la nas variáveis de ambiente para todos os comandos de armazenamento na mesma sessão.</span><span class="sxs-lookup"><span data-stu-id="cb482-156">You can choose one of them and set it in the environment variables for all the storage commands in the same session.</span></span> <span data-ttu-id="cb482-157">Isso permite executar os comandos de armazenamento da CLI do Azure sem especificar explicitamente a chave e a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cb482-157">This enables you to run the Azure CLI storage commands without specifying the storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="cb482-158">Outra forma de definir uma conta de armazenamento padrão é usar a cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="cb482-158">Another way to set a default storage account is using connection string.</span></span> <span data-ttu-id="cb482-159">Em primeiro lugar, obtenha a cadeia de conexão pelo comando:</span><span class="sxs-lookup"><span data-stu-id="cb482-159">Firstly get the connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="cb482-160">Em seguida, copie a cadeia de conexão de saída e a defina como variável de ambiente:</span><span class="sxs-lookup"><span data-stu-id="cb482-160">Then copy the output connection string and set it to environment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="cb482-161">Criar e gerenciar blobs</span><span class="sxs-lookup"><span data-stu-id="cb482-161">Create and manage blobs</span></span>
<span data-ttu-id="cb482-162">O Armazenamento de Blobs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar do mundo por meio de HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="cb482-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="cb482-163">Esta seção pressupõe que você esteja familiarizado com o conceitos de Armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-163">This section assumes that you are already familiar with the Azure Blob storage concepts.</span></span> <span data-ttu-id="cb482-164">Para obter informações detalhadas, confira [Introdução ao Armazenamento de Blobs do Azure usando o .NET](storage-dotnet-how-to-use-blobs.md) e [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx) (Conceitos do serviço Blob).</span><span class="sxs-lookup"><span data-stu-id="cb482-164">For detailed information, see [Get started with Azure Blob storage using .NET](storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="cb482-165">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="cb482-165">Create a container</span></span>
<span data-ttu-id="cb482-166">Todos os blobs no armazenamento do Azure devem residir em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="cb482-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="cb482-167">Você pode criar um contêiner privado usando o comando `azure storage container create` :</span><span class="sxs-lookup"><span data-stu-id="cb482-167">You can create a private container using the `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="cb482-168">Há três níveis de acesso de leitura anônimo: **Desativado**, **Blob** e **Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="cb482-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="cb482-169">Para evitar o acesso anônimo a blobs, defina o parâmetro de permissão como **Desativado**.</span><span class="sxs-lookup"><span data-stu-id="cb482-169">To prevent anonymous access to blobs, set the Permission parameter to **Off**.</span></span> <span data-ttu-id="cb482-170">Por padrão, o novo contêiner é privado e pode ser acessado apenas pelo proprietário da conta.</span><span class="sxs-lookup"><span data-stu-id="cb482-170">By default, the new container is private and can be accessed only by the account owner.</span></span> <span data-ttu-id="cb482-171">Para permitir acesso de leitura público anônimo a recursos de blob, mas não aos metadados do contêiner ou à lista de blobs no contêiner, defina o parâmetro de permissão como **Blob**.</span><span class="sxs-lookup"><span data-stu-id="cb482-171">To allow anonymous public read access to blob resources, but not to container metadata or to the list of blobs in the container, set the Permission parameter to **Blob**.</span></span> <span data-ttu-id="cb482-172">Para permitir acesso de leitura público completo a recursos, metadados do contêiner e à lista de blobs no contêiner, defina o parâmetro de permissão como **Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="cb482-172">To allow full public read access to blob resources, container metadata, and the list of blobs in the container, set the Permission parameter to **Container**.</span></span> <span data-ttu-id="cb482-173">Para obter mais informações, consulte [Gerenciar acesso anônimo de leitura aos contêineres e blobs](storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="cb482-173">For more information, see [Manage anonymous read access to containers and blobs](storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="cb482-174">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="cb482-174">Upload a blob into a container</span></span>
<span data-ttu-id="cb482-175">O Armazenamento de Blob do Azure oferece suporte a blobs de blocos e a blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="cb482-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="cb482-176">Para saber mais, confira [Noções básicas sobre Blobs de bloco, Blobs de acréscimo e Blobs de página](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="cb482-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="cb482-177">Para carregar blobs em um contêiner, você poderá usar `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="cb482-177">To upload blobs in to a container, you can use the `azure storage blob upload`.</span></span> <span data-ttu-id="cb482-178">Por padrão, esse comando carrega os arquivos locais para um blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="cb482-178">By default, this command uploads the local files to a block blob.</span></span> <span data-ttu-id="cb482-179">Para especificar o tipo de blob, você pode usar o parâmetro `--blobtype` .</span><span class="sxs-lookup"><span data-stu-id="cb482-179">To specify the type for the blob, you can use the `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="cb482-180">Baixar blobs de um contêiner</span><span class="sxs-lookup"><span data-stu-id="cb482-180">Download blobs from a container</span></span>
<span data-ttu-id="cb482-181">O exemplo a seguir demonstra como baixar blobs de um contêiner.</span><span class="sxs-lookup"><span data-stu-id="cb482-181">The following example demonstrates how to download blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="cb482-182">Copiar blobs</span><span class="sxs-lookup"><span data-stu-id="cb482-182">Copy blobs</span></span>
<span data-ttu-id="cb482-183">É possível copiar blobs em ou entre regiões e contas de armazenamento de modo assíncrono.</span><span class="sxs-lookup"><span data-stu-id="cb482-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="cb482-184">O exemplo a seguir demonstra como copiar blobs de uma conta de armazenamento para outra.</span><span class="sxs-lookup"><span data-stu-id="cb482-184">The following example demonstrates how to copy blobs from one storage account to another.</span></span> <span data-ttu-id="cb482-185">Neste exemplo, podemos criar um contêiner onde os blobs podem ser acessados pública e anonimamente.</span><span class="sxs-lookup"><span data-stu-id="cb482-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="cb482-186">Neste exemplo, é executada uma cópia assíncrona.</span><span class="sxs-lookup"><span data-stu-id="cb482-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="cb482-187">Você pode monitorar o status de cada operação de cópia, executando a operação `azure storage blob copy show` .</span><span class="sxs-lookup"><span data-stu-id="cb482-187">You can monitor the status of each copy operation by running the `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="cb482-188">Observe que a URL de origem fornecida para a operação de cópia deve ser acessível publicamente ou incluir um token SAS (assinatura de acesso compartilhado).</span><span class="sxs-lookup"><span data-stu-id="cb482-188">Note that the source URL provided for the copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="cb482-189">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="cb482-189">Delete a blob</span></span>
<span data-ttu-id="cb482-190">Para excluir um blob, use o comando abaixo:</span><span class="sxs-lookup"><span data-stu-id="cb482-190">To delete a blob, use the below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="cb482-191">Criar e gerenciar compartilhamentos de arquivos</span><span class="sxs-lookup"><span data-stu-id="cb482-191">Create and manage file shares</span></span>
<span data-ttu-id="cb482-192">O Armazenamento de Arquivos do Azure oferece o armazenamento compartilhado para aplicativos com o uso do protocolo SMB padrão.</span><span class="sxs-lookup"><span data-stu-id="cb482-192">Azure File storage offers shared storage for applications using the standard SMB protocol.</span></span> <span data-ttu-id="cb482-193">As máquinas virtuais e os serviços de nuvem do Microsoft Azure, bem como aplicativos locais, podem compartilhar dados de arquivos por meio de compartilhamentos montados.</span><span class="sxs-lookup"><span data-stu-id="cb482-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="cb482-194">Você pode gerenciar compartilhamentos de arquivos e dados de arquivos por meio da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-194">You can manage file shares and file data via the Azure CLI.</span></span> <span data-ttu-id="cb482-195">Para obter mais informações sobre o Armazenamento de Arquivos do Azure, confira [Introdução ao Armazenamento de Arquivos do Azure no Windows](storage-dotnet-how-to-use-files.md) ou [Como usar o Armazenamento de Arquivos do Azure com o Linux](storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="cb482-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](storage-dotnet-how-to-use-files.md) or [How to use Azure File storage with Linux](storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="cb482-196">Criar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="cb482-196">Create a file share</span></span>
<span data-ttu-id="cb482-197">Um compartilhamento de Arquivos do Azure é um compartilhamento de arquivos do SMB no Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="cb482-198">Todos os arquivos e diretórios devem ser criados em um compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="cb482-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="cb482-199">Uma conta de armazenamento pode conter um número ilimitado de compartilhamentos, e um compartilhamento pode conter um número ilimitado de arquivos, até os limites de capacidade da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cb482-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up to the capacity limits of the storage account.</span></span> <span data-ttu-id="cb482-200">O exemplo a seguir cria um compartilhamento de arquivos denominado **myshare**.</span><span class="sxs-lookup"><span data-stu-id="cb482-200">The following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="cb482-201">Criar um diretório</span><span class="sxs-lookup"><span data-stu-id="cb482-201">Create a directory</span></span>
<span data-ttu-id="cb482-202">Um diretório fornece uma estrutura hierárquica opcional para um compartilhamento de arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb482-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="cb482-203">O exemplo a seguir cria um diretório denominado **myDir** no compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="cb482-203">The following example creates a directory named **myDir** in the file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="cb482-204">Observe que esse caminho de diretório pode incluir vários níveis, *por exemplo*: **a/b**.</span><span class="sxs-lookup"><span data-stu-id="cb482-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="cb482-205">No entanto, você deve garantir a existência de todos os diretórios pai.</span><span class="sxs-lookup"><span data-stu-id="cb482-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="cb482-206">Por exemplo, para o caminho **a/b**, você deve criar o diretório **a** primeiro e, em seguida, o diretório **b**.</span><span class="sxs-lookup"><span data-stu-id="cb482-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-to-directory"></a><span data-ttu-id="cb482-207">Carregar um arquivo local no diretório</span><span class="sxs-lookup"><span data-stu-id="cb482-207">Upload a local file to directory</span></span>
<span data-ttu-id="cb482-208">O exemplo a seguir carrega um arquivo de **~/temp/samplefile.txt** no diretório **myDir**.</span><span class="sxs-lookup"><span data-stu-id="cb482-208">The following example uploads a file from **~/temp/samplefile.txt** to the **myDir** directory.</span></span> <span data-ttu-id="cb482-209">Edite o caminho do arquivo para que ele aponte para um arquivo válido em seu computador local:</span><span class="sxs-lookup"><span data-stu-id="cb482-209">Edit the file path so that it points to a valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="cb482-210">Observe que um arquivo no compartilhamento pode ter até 1 TB.</span><span class="sxs-lookup"><span data-stu-id="cb482-210">Note that a file in the share can be up to 1 TB in size.</span></span>

### <a name="list-the-files-in-the-share-root-or-directory"></a><span data-ttu-id="cb482-211">Listar os arquivos no diretório ou na raiz de compartilhamento</span><span class="sxs-lookup"><span data-stu-id="cb482-211">List the files in the share root or directory</span></span>
<span data-ttu-id="cb482-212">É possível listar os arquivos e subdiretórios em um diretório ou uma raiz de compartilhamento usando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="cb482-212">You can list the files and subdirectories in a share root or a directory using the following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="cb482-213">Observe que o nome do diretório é opcional para a operação de listagem.</span><span class="sxs-lookup"><span data-stu-id="cb482-213">Note that the directory name is optional for the listing operation.</span></span> <span data-ttu-id="cb482-214">Se omitido, o comando listará o conteúdo do diretório raiz do compartilhamento.</span><span class="sxs-lookup"><span data-stu-id="cb482-214">If omitted, the command lists the contents of the root directory of the share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="cb482-215">Copiar arquivos</span><span class="sxs-lookup"><span data-stu-id="cb482-215">Copy files</span></span>
<span data-ttu-id="cb482-216">A partir da versão 0.9.8 da CLI do Azure, você pode copiar um arquivo para outro arquivo, um arquivo para um blob ou um blob para um arquivo.</span><span class="sxs-lookup"><span data-stu-id="cb482-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="cb482-217">A seguir, demonstramos como executar essas operações de cópia usando comandos CLI.</span><span class="sxs-lookup"><span data-stu-id="cb482-217">Below we demonstrate how to perform these copy operations using CLI commands.</span></span> <span data-ttu-id="cb482-218">Para copiar um arquivo para o novo diretório:</span><span class="sxs-lookup"><span data-stu-id="cb482-218">To copy a file to the new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="cb482-219">Para copiar um blob para um diretório de arquivos:</span><span class="sxs-lookup"><span data-stu-id="cb482-219">To copy a blob to a file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="cb482-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb482-220">Next Steps</span></span>

<span data-ttu-id="cb482-221">Você pode encontrar a referência de comandos da CLI 1.0 do Azure para trabalhar com recursos de Armazenamento aqui:</span><span class="sxs-lookup"><span data-stu-id="cb482-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="cb482-222">Comandos da CLI do Azure no modo Resource Manager</span><span class="sxs-lookup"><span data-stu-id="cb482-222">Azure CLI commands in Resource Manager mode</span></span>](../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="cb482-223">Comandos da CLI do Azure no modo Gerenciamento de Serviços do Azure</span><span class="sxs-lookup"><span data-stu-id="cb482-223">Azure CLI commands in Azure Service Management mode</span></span>](../cli-install-nodejs.md)

<span data-ttu-id="cb482-224">Talvez você também queira testar a [CLI do Azure 2.0](storage-azure-cli.md), nossa CLI de próxima geração escrita em Python para uso com o modelo de implantação do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="cb482-224">You may also like to try the [Azure CLI 2.0](storage-azure-cli.md), our next-generation CLI written in Python, for use with the Resource Manager deployment model.</span></span>

[Image1]: ./media/storage-azure-cli/azure_command.png
