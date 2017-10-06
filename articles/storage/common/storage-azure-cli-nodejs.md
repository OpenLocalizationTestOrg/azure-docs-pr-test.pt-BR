---
title: "Olá aaaUsing 1.0 da CLI do Azure com o armazenamento do Azure | Microsoft Docs"
description: "Saiba como toouse hello Azure Interface de linha de comando (CLI do Azure) 1.0 com toocreate de armazenamento do Azure e gerencie contas de armazenamento e trabalhar com arquivos e blobs do Azure. Olá CLI do Azure é uma ferramenta de plataforma cruzada"
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
ms.openlocfilehash: 25e459403dde631741403c8722ed07beafac35c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cli-10-with-azure-storage"></a><span data-ttu-id="a5e44-104">Usando Olá 1.0 da CLI do Azure com o armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="a5e44-104">Using hello Azure CLI 1.0 with Azure Storage</span></span>

## <a name="overview"></a><span data-ttu-id="a5e44-105">Visão geral</span><span class="sxs-lookup"><span data-stu-id="a5e44-105">Overview</span></span>

<span data-ttu-id="a5e44-106">Olá CLI do Azure fornece um conjunto de software livre, multiplataforma comandos para trabalhar com hello plataforma Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e44-106">hello Azure CLI provides a set of open source, cross-platform commands for working with hello Azure Platform.</span></span> <span data-ttu-id="a5e44-107">Ele fornece grande parte da saudação mesma funcionalidade encontrada no hello [portal do Azure](https://portal.azure.com) funcionalidade de acesso a dados também é tão avançados.</span><span class="sxs-lookup"><span data-stu-id="a5e44-107">It provides much of hello same functionality found in hello [Azure portal](https://portal.azure.com) as well as rich data access functionality.</span></span>

<span data-ttu-id="a5e44-108">Neste guia, exploraremos como toouse [Azure Interface de linha de comando (CLI do Azure)](../../cli-install-nodejs.md) tooperform uma variedade de tarefas de administração e desenvolvimento com o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e44-108">In this guide, we'll explore how toouse [Azure Command-Line Interface (Azure CLI)](../../cli-install-nodejs.md) tooperform a variety of development and administration tasks with Azure Storage.</span></span> <span data-ttu-id="a5e44-109">É recomendável baixar e instalar ou atualizar toohello CLI do Azure mais recentes antes de usar este guia.</span><span class="sxs-lookup"><span data-stu-id="a5e44-109">We recommend that you download and install or upgrade toohello latest Azure CLI before using this guide.</span></span>

<span data-ttu-id="a5e44-110">Este guia pressupõe que você entender os conceitos básicos de saudação do armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e44-110">This guide assumes that you understand hello basic concepts of Azure Storage.</span></span> <span data-ttu-id="a5e44-111">Guia de saudação fornece vários scripts toodemonstrate uso Olá Olá CLI do Azure com o armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e44-111">hello guide provides a number of scripts toodemonstrate hello usage of hello Azure CLI with Azure Storage.</span></span> <span data-ttu-id="a5e44-112">Ser tooupdate-se de que variáveis de script hello com base na sua configuração antes de executar cada script.</span><span class="sxs-lookup"><span data-stu-id="a5e44-112">Be sure tooupdate hello script variables based on your configuration before running each script.</span></span>

> [!NOTE]
> <span data-ttu-id="a5e44-113">Guia de saudação fornece exemplos de comando e script de CLI do Azure Olá para contas de armazenamento clássicos.</span><span class="sxs-lookup"><span data-stu-id="a5e44-113">hello guide provides hello Azure CLI command and script examples for classic storage accounts.</span></span> <span data-ttu-id="a5e44-114">Consulte [hello usando a CLI do Azure para Mac, Linux e Windows com o gerenciamento de recursos do Azure](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) para comandos de CLI do Azure para contas de armazenamento do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="a5e44-114">See [Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects) for Azure CLI commands for Resource Manager storage accounts.</span></span>
>
>

[!INCLUDE [storage-cli-versions](../../../includes/storage-cli-versions.md)]

## <a name="get-started-with-azure-storage-and-hello-azure-cli-in-5-minutes"></a><span data-ttu-id="a5e44-115">Introdução ao armazenamento do Azure e hello CLI do Azure em 5 minutos</span><span class="sxs-lookup"><span data-stu-id="a5e44-115">Get started with Azure Storage and hello Azure CLI in 5 minutes</span></span>
<span data-ttu-id="a5e44-116">Nos exemplos deste guia, usamos o Ubuntu, mas outras plataformas de sistema operacional devem funcionar de forma semelhante.</span><span class="sxs-lookup"><span data-stu-id="a5e44-116">This guide uses Ubuntu for examples, but other OS platforms should perform similarly.</span></span>

<span data-ttu-id="a5e44-117">**Novo tooAzure:** obter uma assinatura Microsoft Azure e uma conta da Microsoft associada à assinatura.</span><span class="sxs-lookup"><span data-stu-id="a5e44-117">**New tooAzure:** Get a Microsoft Azure subscription and a Microsoft account associated with that subscription.</span></span> <span data-ttu-id="a5e44-118">Para saber mais sobre as opções de compra do Azure, confira [Avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/), [Opções de compra](https://azure.microsoft.com/pricing/purchase-options/) e [Ofertas para membros](https://azure.microsoft.com/pricing/member-offers/) (para membros do MSDN, Microsoft Partner Network e BizSpark, entre outros programas da Microsoft).</span><span class="sxs-lookup"><span data-stu-id="a5e44-118">For information on Azure purchase options, see [Free Trial](https://azure.microsoft.com/pricing/free-trial/), [Purchase Options](https://azure.microsoft.com/pricing/purchase-options/), and [Member Offers](https://azure.microsoft.com/pricing/member-offers/) (for members of MSDN, Microsoft Partner Network, and BizSpark, and other Microsoft programs).</span></span>

<span data-ttu-id="a5e44-119">Consulte [Atribuindo funções de administrador no Azure AD (Azure Active Directory)](https://msdn.microsoft.com/library/azure/hh531793.aspx) para obter mais informações sobre as assinaturas do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e44-119">See [Assigning administrator roles in Azure Active Directory (Azure AD)](https://msdn.microsoft.com/library/azure/hh531793.aspx) for more information about Azure subscriptions.</span></span>

<span data-ttu-id="a5e44-120">**Depois de criar uma assinatura e conta do Microsoft Azure:**</span><span class="sxs-lookup"><span data-stu-id="a5e44-120">**After creating a Microsoft Azure subscription and account:**</span></span>

1. <span data-ttu-id="a5e44-121">Baixe e instale Olá CLI do Azure seguindo as instruções de saudação descrita em [instalação Olá CLI do Azure](../../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="a5e44-121">Download and install hello Azure CLI following hello instructions outlined in [Install hello Azure CLI](../../cli-install-nodejs.md).</span></span>
2. <span data-ttu-id="a5e44-122">Quando hello CLI do Azure foi instalado, você será capaz de toouse hello azure comando de comandos de CLI do Azure sua interface de linha de comando (Bash, Terminal, prompt de comando) tooaccess hello.</span><span class="sxs-lookup"><span data-stu-id="a5e44-122">Once hello Azure CLI has been installed, you will be able toouse hello azure command from your command-line interface (Bash, Terminal, Command prompt) tooaccess hello Azure CLI commands.</span></span> <span data-ttu-id="a5e44-123">Saudação de tipo _azure_ comando e você verá Olá saída a seguir.</span><span class="sxs-lookup"><span data-stu-id="a5e44-123">Type hello _azure_ command and you should see hello following output.</span></span>

    ![Saída de comando do Azure](./media/storage-azure-cli/azure_command.png)   
3. <span data-ttu-id="a5e44-125">Na interface de linha de comando hello, digite `azure storage` toolist todas Olá comandos de armazenamento do azure e obter uma primeira impressão de saudação de funcionalidades Olá CLI do Azure fornece.</span><span class="sxs-lookup"><span data-stu-id="a5e44-125">In hello command-line interface, type `azure storage` toolist out all hello azure storage commands and get a first impression of hello functionalities hello Azure CLI provides.</span></span> <span data-ttu-id="a5e44-126">Você pode digitar o nome de comando com **-h** parâmetro (por exemplo, `azure storage share create -h`) toosee detalhes da sintaxe de comando.</span><span class="sxs-lookup"><span data-stu-id="a5e44-126">You can type command name with **-h** parameter (for example, `azure storage share create -h`) toosee details of command syntax.</span></span>
4. <span data-ttu-id="a5e44-127">Agora, vamos dar um script simples que mostra tooaccess de comandos de CLI do Azure básico armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e44-127">Now, we'll give you a simple script that shows basic Azure CLI commands tooaccess Azure Storage.</span></span> <span data-ttu-id="a5e44-128">script Hello primeiro solicitará tooset duas variáveis para a conta de armazenamento e a chave.</span><span class="sxs-lookup"><span data-stu-id="a5e44-128">hello script will first ask you tooset two variables for your storage account and key.</span></span> <span data-ttu-id="a5e44-129">Em seguida, script hello criará um novo contêiner nessa nova conta de armazenamento e carregar um contêiner de toothat de (blob) do arquivo de imagem existente.</span><span class="sxs-lookup"><span data-stu-id="a5e44-129">Then, hello script will create a new container in this new storage account and upload an existing image file (blob) toothat container.</span></span> <span data-ttu-id="a5e44-130">Depois que o script hello lista todos os blobs nesse contêiner, ele baixará Olá imagem arquivo toohello diretório de destino que existe no computador local hello.</span><span class="sxs-lookup"><span data-stu-id="a5e44-130">After hello script lists all blobs in that container, it will download hello image file toohello destination directory which exists on hello local computer.</span></span>

    ```azurecli
    #!/bin/bash
    # A simple Azure storage example

    export AZURE_STORAGE_ACCOUNT=<storage_account_name>
    export AZURE_STORAGE_ACCESS_KEY=<storage_account_key>

    export container_name=<container_name>
    export blob_name=<blob_name>
    export image_to_upload=<image_to_upload>
    export destination_folder=<destination_folder>

    echo "Creating hello container..."
    azure storage container create $container_name

    echo "Uploading hello image..."
    azure storage blob upload $image_to_upload $container_name $blob_name

    echo "Listing hello blobs..."
    azure storage blob list $container_name

    echo "Downloading hello image..."
    azure storage blob download $container_name $blob_name $destination_folder

    echo "Done"
    ```

5. <span data-ttu-id="a5e44-131">No computador local, abra o editor de texto de sua preferência (vim, por exemplo).</span><span class="sxs-lookup"><span data-stu-id="a5e44-131">In your local computer, open your preferred text editor (vim for example).</span></span> <span data-ttu-id="a5e44-132">Digite hello acima script em seu editor de texto.</span><span class="sxs-lookup"><span data-stu-id="a5e44-132">Type hello above script into your text editor.</span></span>
6. <span data-ttu-id="a5e44-133">Agora, você precisa de variáveis de script hello tooupdate com base em suas definições de configuração.</span><span class="sxs-lookup"><span data-stu-id="a5e44-133">Now, you need tooupdate hello script variables based on your configuration settings.</span></span>

   * <span data-ttu-id="a5e44-134">**< Storage_account_name >** usar Olá considerando o nome do script hello ou digitar um novo nome para sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a5e44-134">**<storage_account_name>** Use hello given name in hello script or enter a new name for your storage account.</span></span> <span data-ttu-id="a5e44-135">**Importante:** nome Olá Olá da conta de armazenamento deve ser exclusivo no Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e44-135">**Important:** hello name of hello storage account must be unique in Azure.</span></span> <span data-ttu-id="a5e44-136">Ele também deve ter somente letras minúsculas!</span><span class="sxs-lookup"><span data-stu-id="a5e44-136">It must be lowercase, too!</span></span>
   * <span data-ttu-id="a5e44-137">**< storage_account_key >** chave de acesso de saudação da sua conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a5e44-137">**<storage_account_key>** hello access key of your storage account.</span></span>
   * <span data-ttu-id="a5e44-138">**< Container_name >** Use Olá considerando o nome do script hello ou digite um novo nome para seu contêiner.</span><span class="sxs-lookup"><span data-stu-id="a5e44-138">**<container_name>** Use hello given name in hello script or enter a new name for your container.</span></span>
   * <span data-ttu-id="a5e44-139">**< Image_to_upload >** inserir uma imagem de tooa caminho no computador local, como: "~ / images/HelloWorld.png".</span><span class="sxs-lookup"><span data-stu-id="a5e44-139">**<image_to_upload>** Enter a path tooa picture on your local computer, such as: "~/images/HelloWorld.png".</span></span>
   * <span data-ttu-id="a5e44-140">**< Destination_folder >** Enter um arquivos de toostore de diretório local do caminho tooa baixado do armazenamento do Azure, como: "~/downloadImages".</span><span class="sxs-lookup"><span data-stu-id="a5e44-140">**<destination_folder>** Enter a path tooa local directory toostore files downloaded from Azure Storage, such as: "~/downloadImages".</span></span>
7. <span data-ttu-id="a5e44-141">Depois que você atualizou variáveis necessárias de saudação em vim, pressionar combinações de teclas `ESC`, `:`, `wq!` toosave script de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e44-141">After you've updated hello necessary variables in vim, press key combinations `ESC`, `:`, `wq!` toosave hello script.</span></span>
8. <span data-ttu-id="a5e44-142">toorun esse script, simplesmente tipo hello script nome de arquivo no console do hello bash.</span><span class="sxs-lookup"><span data-stu-id="a5e44-142">toorun this script, simply type hello script file name in hello bash console.</span></span> <span data-ttu-id="a5e44-143">Depois que esse script é executado, você deve ter uma pasta de destino que inclui o arquivo de imagem Olá baixado.</span><span class="sxs-lookup"><span data-stu-id="a5e44-143">After this script runs, you should have a local destination folder that includes hello downloaded image file.</span></span> <span data-ttu-id="a5e44-144">Olá captura de tela a seguir mostra um exemplo de saída:</span><span class="sxs-lookup"><span data-stu-id="a5e44-144">hello following screenshot shows an example output:</span></span>

<span data-ttu-id="a5e44-145">Após a execução do script hello, você deve ter uma pasta de destino que inclui o arquivo de imagem Olá baixado.</span><span class="sxs-lookup"><span data-stu-id="a5e44-145">After hello script runs, you should have a local destination folder that includes hello downloaded image file.</span></span>

## <a name="manage-storage-accounts-with-hello-azure-cli"></a><span data-ttu-id="a5e44-146">Gerenciar contas de armazenamento com hello CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="a5e44-146">Manage storage accounts with hello Azure CLI</span></span>
### <a name="connect-tooyour-azure-subscription"></a><span data-ttu-id="a5e44-147">Conecte-se tooyour assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="a5e44-147">Connect tooyour Azure subscription</span></span>
<span data-ttu-id="a5e44-148">Embora a maioria dos comandos de armazenamento Olá funcione sem uma assinatura do Azure, recomendamos que você tooconnect tooyour assinatura Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e44-148">While most of hello storage commands will work without an Azure subscription, we recommend you tooconnect tooyour subscription from hello Azure CLI.</span></span> <span data-ttu-id="a5e44-149">tooconfigure Olá CLI do Azure toowork com sua assinatura, execute as etapas de saudação em [conectar tooan assinatura do Azure do hello CLI do Azure](../../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="a5e44-149">tooconfigure hello Azure CLI toowork with your subscription, follow hello steps in [Connect tooan Azure subscription from hello Azure CLI](../../xplat-cli-connect.md).</span></span>

### <a name="create-a-new-storage-account"></a><span data-ttu-id="a5e44-150">Criar uma nova conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a5e44-150">Create a new storage account</span></span>
<span data-ttu-id="a5e44-151">toouse armazenamento do Azure, você precisará de uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a5e44-151">toouse Azure storage, you will need a storage account.</span></span> <span data-ttu-id="a5e44-152">Depois de configurar sua assinatura do computador tooconnect tooyour, você pode criar uma nova conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e44-152">You can create a new Azure storage account after you have configured your computer tooconnect tooyour subscription.</span></span>

```azurecli
azure storage account create <account_name>
```

<span data-ttu-id="a5e44-153">nome de saudação da sua conta de armazenamento deve ter entre 3 e 24 caracteres de comprimento e usar números e letras minúsculas apenas.</span><span class="sxs-lookup"><span data-stu-id="a5e44-153">hello name of your storage account must be between 3 and 24 characters in length and use numbers and lower-case letters only.</span></span>

### <a name="set-a-default-azure-storage-account-in-environment-variables"></a><span data-ttu-id="a5e44-154">Definir uma conta de armazenamento padrão do Azure nas variáveis de ambiente</span><span class="sxs-lookup"><span data-stu-id="a5e44-154">Set a default Azure storage account in environment variables</span></span>
<span data-ttu-id="a5e44-155">Você pode ter várias contas de armazenamento na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="a5e44-155">You can have multiple storage accounts in your subscription.</span></span> <span data-ttu-id="a5e44-156">Você pode escolher um deles e defini-la no hello variáveis de ambiente para todo o armazenamento Olá comandos no hello mesmo sessão.</span><span class="sxs-lookup"><span data-stu-id="a5e44-156">You can choose one of them and set it in hello environment variables for all hello storage commands in hello same session.</span></span> <span data-ttu-id="a5e44-157">Isso permite que você toorun armazenamento de CLI do Azure Olá comandos sem especificar o armazenamento de saudação de conta e chave explicitamente.</span><span class="sxs-lookup"><span data-stu-id="a5e44-157">This enables you toorun hello Azure CLI storage commands without specifying hello storage account and key explicitly.</span></span>

```azurecli
export AZURE_STORAGE_ACCOUNT=<account_name>
export AZURE_STORAGE_ACCESS_KEY=<key>
```

<span data-ttu-id="a5e44-158">Outra maneira tooset uma conta de armazenamento padrão está usando a cadeia de caracteres de conexão.</span><span class="sxs-lookup"><span data-stu-id="a5e44-158">Another way tooset a default storage account is using connection string.</span></span> <span data-ttu-id="a5e44-159">Em primeiro lugar, obter cadeia de caracteres de conexão de saudação pelo comando:</span><span class="sxs-lookup"><span data-stu-id="a5e44-159">Firstly get hello connection string by command:</span></span>

```azurecli
azure storage account connectionstring show <account_name>
```

<span data-ttu-id="a5e44-160">Copie a cadeia de caracteres de conexão de saída hello e defina-a como tooenvironment variável:</span><span class="sxs-lookup"><span data-stu-id="a5e44-160">Then copy hello output connection string and set it tooenvironment variable:</span></span>

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=<connection_string>
```

## <a name="create-and-manage-blobs"></a><span data-ttu-id="a5e44-161">Criar e gerenciar blobs</span><span class="sxs-lookup"><span data-stu-id="a5e44-161">Create and manage blobs</span></span>
<span data-ttu-id="a5e44-162">Armazenamento de BLOBs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, como texto ou dados binários, que podem ser acessados de qualquer lugar Olá, mundo via HTTP ou HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a5e44-162">Azure Blob storage is a service for storing large amounts of unstructured data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="a5e44-163">Esta seção pressupõe que você já esteja familiarizado com conceitos de armazenamento de BLOBs do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a5e44-163">This section assumes that you are already familiar with hello Azure Blob storage concepts.</span></span> <span data-ttu-id="a5e44-164">Para obter informações detalhadas, confira [Introdução ao Armazenamento de Blobs do Azure usando o .NET](../blobs/storage-dotnet-how-to-use-blobs.md) e [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx) (Conceitos do serviço Blob).</span><span class="sxs-lookup"><span data-stu-id="a5e44-164">For detailed information, see [Get started with Azure Blob storage using .NET](../blobs/storage-dotnet-how-to-use-blobs.md) and [Blob Service Concepts](http://msdn.microsoft.com/library/azure/dd179376.aspx).</span></span>

### <a name="create-a-container"></a><span data-ttu-id="a5e44-165">Criar um contêiner</span><span class="sxs-lookup"><span data-stu-id="a5e44-165">Create a container</span></span>
<span data-ttu-id="a5e44-166">Todos os blobs no armazenamento do Azure devem residir em um contêiner.</span><span class="sxs-lookup"><span data-stu-id="a5e44-166">Every blob in Azure storage must be in a container.</span></span> <span data-ttu-id="a5e44-167">Você pode criar um contêiner privado usando Olá `azure storage container create` comando:</span><span class="sxs-lookup"><span data-stu-id="a5e44-167">You can create a private container using hello `azure storage container create` command:</span></span>

```azurecli
azure storage container create mycontainer
```

> [!NOTE]
> <span data-ttu-id="a5e44-168">Há três níveis de acesso de leitura anônimo: **Desativado**, **Blob** e **Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="a5e44-168">There are three levels of anonymous read access: **Off**, **Blob**, and **Container**.</span></span> <span data-ttu-id="a5e44-169">tooprevent anônimo acessar tooblobs, Olá permissão parâmetro muito**Off**.</span><span class="sxs-lookup"><span data-stu-id="a5e44-169">tooprevent anonymous access tooblobs, set hello Permission parameter too**Off**.</span></span> <span data-ttu-id="a5e44-170">Por padrão, o novo contêiner de saudação é particular e pode ser acessado somente pelo proprietário da conta hello.</span><span class="sxs-lookup"><span data-stu-id="a5e44-170">By default, hello new container is private and can be accessed only by hello account owner.</span></span> <span data-ttu-id="a5e44-171">público anônimo tooallow leitura tooblob acessar os recursos, mas não toocontainer metadados ou toohello a lista de blobs no contêiner Olá, defina o parâmetro de permissão de saudação muito**Blob**.</span><span class="sxs-lookup"><span data-stu-id="a5e44-171">tooallow anonymous public read access tooblob resources, but not toocontainer metadata or toohello list of blobs in hello container, set hello Permission parameter too**Blob**.</span></span> <span data-ttu-id="a5e44-172">público completo tooallow leitura tooblob acessar os recursos, os metadados de contêiner e lista de saudação de blobs no contêiner de saudação, defina o parâmetro de permissão de saudação muito**contêiner**.</span><span class="sxs-lookup"><span data-stu-id="a5e44-172">tooallow full public read access tooblob resources, container metadata, and hello list of blobs in hello container, set hello Permission parameter too**Container**.</span></span> <span data-ttu-id="a5e44-173">Para obter mais informações, consulte [gerenciar o acesso de leitura anônimo toocontainers e blobs](../blobs/storage-manage-access-to-resources.md).</span><span class="sxs-lookup"><span data-stu-id="a5e44-173">For more information, see [Manage anonymous read access toocontainers and blobs](../blobs/storage-manage-access-to-resources.md).</span></span>
>
>

### <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="a5e44-174">Carregar um blob em um contêiner</span><span class="sxs-lookup"><span data-stu-id="a5e44-174">Upload a blob into a container</span></span>
<span data-ttu-id="a5e44-175">O Armazenamento de Blob do Azure oferece suporte a blobs de blocos e a blobs de páginas.</span><span class="sxs-lookup"><span data-stu-id="a5e44-175">Azure Blob Storage supports block blobs and page blobs.</span></span> <span data-ttu-id="a5e44-176">Para saber mais, confira [Noções básicas sobre Blobs de bloco, Blobs de acréscimo e Blobs de página](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5e44-176">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

<span data-ttu-id="a5e44-177">blobs tooupload tooa contêiner, você pode usar o hello `azure storage blob upload`.</span><span class="sxs-lookup"><span data-stu-id="a5e44-177">tooupload blobs in tooa container, you can use hello `azure storage blob upload`.</span></span> <span data-ttu-id="a5e44-178">Por padrão, esse comando carrega o blob de blocos de tooa Olá arquivos locais.</span><span class="sxs-lookup"><span data-stu-id="a5e44-178">By default, this command uploads hello local files tooa block blob.</span></span> <span data-ttu-id="a5e44-179">tipo de saudação toospecify blob Olá, você pode usar Olá `--blobtype` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="a5e44-179">toospecify hello type for hello blob, you can use hello `--blobtype` parameter.</span></span>

```azurecli
azure storage blob upload '~/images/HelloWorld.png' mycontainer myBlockBlob
```

### <a name="download-blobs-from-a-container"></a><span data-ttu-id="a5e44-180">Baixar blobs de um contêiner</span><span class="sxs-lookup"><span data-stu-id="a5e44-180">Download blobs from a container</span></span>
<span data-ttu-id="a5e44-181">saudação de exemplo a seguir demonstra como toodownload blobs de um contêiner.</span><span class="sxs-lookup"><span data-stu-id="a5e44-181">hello following example demonstrates how toodownload blobs from a container.</span></span>

```azurecli
azure storage blob download mycontainer myBlockBlob '~/downloadImages/downloaded.png'
```

### <a name="copy-blobs"></a><span data-ttu-id="a5e44-182">Copiar blobs</span><span class="sxs-lookup"><span data-stu-id="a5e44-182">Copy blobs</span></span>
<span data-ttu-id="a5e44-183">É possível copiar blobs em ou entre regiões e contas de armazenamento de modo assíncrono.</span><span class="sxs-lookup"><span data-stu-id="a5e44-183">You can copy blobs within or across storage accounts and regions asynchronously.</span></span>

<span data-ttu-id="a5e44-184">Olá exemplo a seguir demonstra como blobs de toocopy do armazenamento de uma conta tooanother.</span><span class="sxs-lookup"><span data-stu-id="a5e44-184">hello following example demonstrates how toocopy blobs from one storage account tooanother.</span></span> <span data-ttu-id="a5e44-185">Neste exemplo, podemos criar um contêiner onde os blobs podem ser acessados pública e anonimamente.</span><span class="sxs-lookup"><span data-stu-id="a5e44-185">In this sample we create a container where blobs are publicly, anonymously accessible.</span></span>

```azurecli
azure storage container create mycontainer2 -a <accountName2> -k <accountKey2> -p Blob

azure storage blob upload '~/Images/HelloWorld.png' mycontainer2 myBlockBlob2 -a <accountName2> -k <accountKey2>

azure storage blob copy start 'https://<accountname2>.blob.core.windows.net/mycontainer2/myBlockBlob2' mycontainer
```

<span data-ttu-id="a5e44-186">Neste exemplo, é executada uma cópia assíncrona.</span><span class="sxs-lookup"><span data-stu-id="a5e44-186">This sample performs an asynchronous copy.</span></span> <span data-ttu-id="a5e44-187">Você pode monitorar o status de saudação de cada operação de cópia executando Olá `azure storage blob copy show` operação.</span><span class="sxs-lookup"><span data-stu-id="a5e44-187">You can monitor hello status of each copy operation by running hello `azure storage blob copy show` operation.</span></span>

<span data-ttu-id="a5e44-188">Observe que Olá URL de origem fornecido para uma operação de cópia de saudação deve ser acessível publicamente ou incluir um token SAS (assinatura de acesso compartilhado).</span><span class="sxs-lookup"><span data-stu-id="a5e44-188">Note that hello source URL provided for hello copy operation must either be publicly accessible, or include a SAS (shared access signature) token.</span></span>

### <a name="delete-a-blob"></a><span data-ttu-id="a5e44-189">Excluir um blob</span><span class="sxs-lookup"><span data-stu-id="a5e44-189">Delete a blob</span></span>
<span data-ttu-id="a5e44-190">toodelete um blob, use Olá comando abaixo:</span><span class="sxs-lookup"><span data-stu-id="a5e44-190">toodelete a blob, use hello below command:</span></span>

```azurecli
azure storage blob delete mycontainer myBlockBlob2
```

## <a name="create-and-manage-file-shares"></a><span data-ttu-id="a5e44-191">Criar e gerenciar compartilhamentos de arquivos</span><span class="sxs-lookup"><span data-stu-id="a5e44-191">Create and manage file shares</span></span>
<span data-ttu-id="a5e44-192">Armazenamento de arquivo do Azure oferece armazenamento compartilhado para aplicativos que usam protocolo SMB padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e44-192">Azure File storage offers shared storage for applications using hello standard SMB protocol.</span></span> <span data-ttu-id="a5e44-193">As máquinas virtuais e os serviços de nuvem do Microsoft Azure, bem como aplicativos locais, podem compartilhar dados de arquivos por meio de compartilhamentos montados.</span><span class="sxs-lookup"><span data-stu-id="a5e44-193">Microsoft Azure virtual machines and cloud services, as well as on-premises applications, can share file data via mounted shares.</span></span> <span data-ttu-id="a5e44-194">Você pode gerenciar compartilhamentos de arquivos e dados de arquivo por meio de saudação CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e44-194">You can manage file shares and file data via hello Azure CLI.</span></span> <span data-ttu-id="a5e44-195">Para obter mais informações sobre o armazenamento de arquivo do Azure, consulte [Introdução ao armazenamento de arquivo do Azure no Windows](../storage-dotnet-how-to-use-files.md) ou [como toouse armazenamento de arquivo do Azure com Linux](../storage-how-to-use-files-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a5e44-195">For more information on Azure File storage, see [Get started with Azure File storage on Windows](../storage-dotnet-how-to-use-files.md) or [How toouse Azure File storage with Linux](../storage-how-to-use-files-linux.md).</span></span>

### <a name="create-a-file-share"></a><span data-ttu-id="a5e44-196">Criar um compartilhamento de arquivos</span><span class="sxs-lookup"><span data-stu-id="a5e44-196">Create a file share</span></span>
<span data-ttu-id="a5e44-197">Um compartilhamento de Arquivos do Azure é um compartilhamento de arquivos do SMB no Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e44-197">An Azure File share is an SMB file share in Azure.</span></span> <span data-ttu-id="a5e44-198">Todos os arquivos e diretórios devem ser criados em um compartilhamento de arquivos.</span><span class="sxs-lookup"><span data-stu-id="a5e44-198">All directories and files must be created in a file share.</span></span> <span data-ttu-id="a5e44-199">Uma conta pode conter um número ilimitado de compartilhamentos e um compartilhamento pode armazenar um número ilimitado de arquivos, se os limites de capacidade toohello Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="a5e44-199">An account can contain an unlimited number of shares, and a share can store an unlimited number of files, up toohello capacity limits of hello storage account.</span></span> <span data-ttu-id="a5e44-200">Olá, exemplo a seguir cria um compartilhamento de arquivos chamado **MeuCompartilhamento**.</span><span class="sxs-lookup"><span data-stu-id="a5e44-200">hello following example creates a file share named **myshare**.</span></span>

```azurecli
azure storage share create myshare
```

### <a name="create-a-directory"></a><span data-ttu-id="a5e44-201">Criar um diretório</span><span class="sxs-lookup"><span data-stu-id="a5e44-201">Create a directory</span></span>
<span data-ttu-id="a5e44-202">Um diretório fornece uma estrutura hierárquica opcional para um compartilhamento de arquivos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5e44-202">A directory provides an optional hierarchical structure for an Azure file share.</span></span> <span data-ttu-id="a5e44-203">Olá, exemplo a seguir cria um diretório chamado **myDir** no compartilhamento de arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="a5e44-203">hello following example creates a directory named **myDir** in hello file share.</span></span>

```azurecli
azure storage directory create myshare myDir
```

<span data-ttu-id="a5e44-204">Observe que esse caminho de diretório pode incluir vários níveis, *por exemplo*: **a/b**.</span><span class="sxs-lookup"><span data-stu-id="a5e44-204">Note that directory path can include multiple levels, *e.g.*, **a/b**.</span></span> <span data-ttu-id="a5e44-205">No entanto, você deve garantir a existência de todos os diretórios pai.</span><span class="sxs-lookup"><span data-stu-id="a5e44-205">However, you must ensure that all parent directories exist.</span></span> <span data-ttu-id="a5e44-206">Por exemplo, para o caminho **a/b**, você deve criar o diretório **a** primeiro e, em seguida, o diretório **b**.</span><span class="sxs-lookup"><span data-stu-id="a5e44-206">For example, for path **a/b**, you must create directory **a** first, then create directory **b**.</span></span>

### <a name="upload-a-local-file-toodirectory"></a><span data-ttu-id="a5e44-207">Carregar um arquivo local toodirectory</span><span class="sxs-lookup"><span data-stu-id="a5e44-207">Upload a local file toodirectory</span></span>
<span data-ttu-id="a5e44-208">Olá, exemplo a seguir carrega um arquivo de **~/temp/samplefile.txt** toohello **myDir** directory.</span><span class="sxs-lookup"><span data-stu-id="a5e44-208">hello following example uploads a file from **~/temp/samplefile.txt** toohello **myDir** directory.</span></span> <span data-ttu-id="a5e44-209">Edite o caminho do arquivo hello para que ele aponte tooa de arquivo válido no computador local:</span><span class="sxs-lookup"><span data-stu-id="a5e44-209">Edit hello file path so that it points tooa valid file on your local machine:</span></span>

```azurecli
azure storage file upload '~/temp/samplefile.txt' myshare myDir
```

<span data-ttu-id="a5e44-210">Observe que pode ser um arquivo no compartilhamento de saudação até too1 TB de tamanho.</span><span class="sxs-lookup"><span data-stu-id="a5e44-210">Note that a file in hello share can be up too1 TB in size.</span></span>

### <a name="list-hello-files-in-hello-share-root-or-directory"></a><span data-ttu-id="a5e44-211">Listar arquivos Olá na raiz do compartilhamento de saudação ou diretório</span><span class="sxs-lookup"><span data-stu-id="a5e44-211">List hello files in hello share root or directory</span></span>
<span data-ttu-id="a5e44-212">Você pode listar arquivos hello e subdiretórios em uma compartilhamento de raiz ou um diretório usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="a5e44-212">You can list hello files and subdirectories in a share root or a directory using hello following command:</span></span>

```azurecli
azure storage file list myshare myDir
```

<span data-ttu-id="a5e44-213">Observe que esse nome de diretório Olá é opcional para Olá operação de listagem.</span><span class="sxs-lookup"><span data-stu-id="a5e44-213">Note that hello directory name is optional for hello listing operation.</span></span> <span data-ttu-id="a5e44-214">Se omitido, o comando de saudação lista conteúdo de saudação do diretório raiz de saudação do compartilhamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e44-214">If omitted, hello command lists hello contents of hello root directory of hello share.</span></span>

### <a name="copy-files"></a><span data-ttu-id="a5e44-215">Copiar arquivos</span><span class="sxs-lookup"><span data-stu-id="a5e44-215">Copy files</span></span>
<span data-ttu-id="a5e44-216">Começando com a versão 0.9.8 da CLI do Azure, você pode copiar um arquivo de tooanother, um blob de tooa de arquivo ou um arquivo de tooa de blob.</span><span class="sxs-lookup"><span data-stu-id="a5e44-216">Beginning with version 0.9.8 of Azure CLI, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="a5e44-217">Abaixo, demonstraremos como tooperform esses copiam operações usando os comandos CLI.</span><span class="sxs-lookup"><span data-stu-id="a5e44-217">Below we demonstrate how tooperform these copy operations using CLI commands.</span></span> <span data-ttu-id="a5e44-218">toocopy um novo diretório de arquivo toohello:</span><span class="sxs-lookup"><span data-stu-id="a5e44-218">toocopy a file toohello new directory:</span></span>

```azurecli
azure storage file copy start --source-share srcshare --source-path srcdir/hello.txt --dest-share destshare
    --dest-path destdir/hellocopy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

<span data-ttu-id="a5e44-219">toocopy um diretório de arquivo de blob tooa:</span><span class="sxs-lookup"><span data-stu-id="a5e44-219">toocopy a blob tooa file directory:</span></span>

```azurecli
azure storage file copy start --source-container srcctn --source-blob hello2.txt --dest-share hello
    --dest-path hellodir/hello2copy.txt --connection-string $srcConnectionString --dest-connection-string $destConnectionString
```

## <a name="next-steps"></a><span data-ttu-id="a5e44-220">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a5e44-220">Next Steps</span></span>

<span data-ttu-id="a5e44-221">Você pode encontrar a referência de comandos da CLI 1.0 do Azure para trabalhar com recursos de Armazenamento aqui:</span><span class="sxs-lookup"><span data-stu-id="a5e44-221">You can find Azure CLI 1.0 command reference for working with Storage resources here:</span></span>

* [<span data-ttu-id="a5e44-222">Comandos da CLI do Azure no modo Resource Manager</span><span class="sxs-lookup"><span data-stu-id="a5e44-222">Azure CLI commands in Resource Manager mode</span></span>](../../virtual-machines/azure-cli-arm-commands.md#azure-storage-commands-to-manage-your-storage-objects)
* [<span data-ttu-id="a5e44-223">Comandos da CLI do Azure no modo Gerenciamento de Serviços do Azure</span><span class="sxs-lookup"><span data-stu-id="a5e44-223">Azure CLI commands in Azure Service Management mode</span></span>](../../cli-install-nodejs.md)

<span data-ttu-id="a5e44-224">Pode também desejar Olá tootry [2.0 do CLI do Azure](../storage-azure-cli.md), nosso CLI de última geração escritos em Python, para uso com o modelo de implantação do Gerenciador de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="a5e44-224">You may also like tootry hello [Azure CLI 2.0](../storage-azure-cli.md), our next-generation CLI written in Python, for use with hello Resource Manager deployment model.</span></span>
