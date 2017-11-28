---
title: "aaaUse 2.0 de linha de comando do Azure interface tooget Introdução ao repositório Azure Data Lake | Microsoft Docs"
description: "Use a linha de comando de plataforma cruzada do Azure 2.0 toocreate uma conta do repositório Data Lake e executar operações básicas"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 4ffa0f4a-1cca-46ac-803d-1fc8538c685b
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 374dcd6cdbc13ad19f6c65502329986ecae60ef2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="0b17d-103">Introdução ao Azure Data Lake Store usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="0b17d-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="0b17d-104">Portal</span><span class="sxs-lookup"><span data-stu-id="0b17d-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="0b17d-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="0b17d-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="0b17d-106">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="0b17d-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="0b17d-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="0b17d-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="0b17d-108">API REST</span><span class="sxs-lookup"><span data-stu-id="0b17d-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="0b17d-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="0b17d-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="0b17d-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="0b17d-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="0b17d-111">Python</span><span class="sxs-lookup"><span data-stu-id="0b17d-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="0b17d-112">Saiba como toocreate toouse 2.0 do CLI do Azure uma Data Lake do Azure armazenam conta e executar operações básicas, como criar pastas, carregar e baixar arquivos de dados, excluir sua conta, etc. Para saber mais sobre o Data Lake Store, veja [Visão geral do Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0b17d-112">Learn how toouse Azure CLI 2.0 toocreate an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="0b17d-113">Olá 2.0 do CLI do Azure é a nova experiência de linha de comando do Azure para gerenciar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b17d-113">hello Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="0b17d-114">Ela pode ser usada em Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="0b17d-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="0b17d-115">Para obter mais informações, consulte [Visão geral da CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="0b17d-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="0b17d-116">Você também pode examinar Olá [referência do armazenamento do Azure Data Lake CLI 2.0](https://docs.microsoft.com/cli/azure/dls) para obter uma lista completa de comandos e sintaxe.</span><span class="sxs-lookup"><span data-stu-id="0b17d-116">You can also look at hello [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0b17d-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0b17d-117">Prerequisites</span></span>
<span data-ttu-id="0b17d-118">Antes de começar este artigo, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="0b17d-118">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="0b17d-119">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="0b17d-119">**An Azure subscription**.</span></span> <span data-ttu-id="0b17d-120">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0b17d-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="0b17d-121">**CLI do Azure 2.0** -consulte [Instalar a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="0b17d-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="0b17d-122">Autenticação</span><span class="sxs-lookup"><span data-stu-id="0b17d-122">Authentication</span></span>

<span data-ttu-id="0b17d-123">Este artigo usa uma abordagem de autenticação mais simples com o Data Lake Store, em que você faz logon como um usuário final.</span><span class="sxs-lookup"><span data-stu-id="0b17d-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="0b17d-124">Olá acesso nível tooData Lake repositório conta de sistema de arquivos e, em seguida, é controlado pelo nível de acesso de saudação do hello usuário conectado no.</span><span class="sxs-lookup"><span data-stu-id="0b17d-124">hello access level tooData Lake Store account and file system is then governed by hello access level of hello logged in user.</span></span> <span data-ttu-id="0b17d-125">No entanto, há outras abordagens como tooauthenticate bem com repositório Data Lake, que são **autenticação do usuário final** ou **autenticação de serviço a serviço**.</span><span class="sxs-lookup"><span data-stu-id="0b17d-125">However, there are other approaches as well tooauthenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="0b17d-126">Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="0b17d-126">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="0b17d-127">Faça logon no tooyour assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="0b17d-127">Log in tooyour Azure subscription</span></span>

1. <span data-ttu-id="0b17d-128">Faça logon em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b17d-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="0b17d-129">Você obtém um código toouse na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="0b17d-129">You get a code toouse in hello next step.</span></span> <span data-ttu-id="0b17d-130">Usar uma web navegador tooopen Olá página https://aka.ms/devicelogin e insira Olá código tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="0b17d-130">Use a web browser tooopen hello page https://aka.ms/devicelogin and enter hello code tooauthenticate.</span></span> <span data-ttu-id="0b17d-131">Você está toolog solicitada usando suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="0b17d-131">You are prompted toolog in using your credentials.</span></span>

2. <span data-ttu-id="0b17d-132">Depois de fazer logon em todas as listas de janelas do Olá Olá assinaturas do Azure que estão associadas com sua conta.</span><span class="sxs-lookup"><span data-stu-id="0b17d-132">Once you log in, hello window lists all hello Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="0b17d-133">Use Olá após o comando toouse uma assinatura específica.</span><span class="sxs-lookup"><span data-stu-id="0b17d-133">Use hello following command toouse a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="0b17d-134">Criar uma conta do Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="0b17d-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="0b17d-135">Crie um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0b17d-135">Create a new resource group.</span></span> <span data-ttu-id="0b17d-136">Olá comando a seguir, forneça Olá valores de parâmetro que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="0b17d-136">In hello following command, provide hello parameter values you want toouse.</span></span> <span data-ttu-id="0b17d-137">Se Olá local nome contiver espaços, coloque-o entre aspas.</span><span class="sxs-lookup"><span data-stu-id="0b17d-137">If hello location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="0b17d-138">Por exemplo "Leste dos EUA 2".</span><span class="sxs-lookup"><span data-stu-id="0b17d-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="0b17d-139">Crie conta de repositório Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="0b17d-139">Create hello Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="0b17d-140">Criar pastas na conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="0b17d-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="0b17d-141">Você pode criar pastas em seu toomanage de conta do repositório Azure Data Lake e armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="0b17d-141">You can create folders under your Azure Data Lake Store account toomanage and store data.</span></span> <span data-ttu-id="0b17d-142">Saudação de uso após o comando toocreate uma pasta chamada **mynewfolder** na raiz de saudação do hello repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0b17d-142">Use hello following command toocreate a folder called **mynewfolder** at hello root of hello Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="0b17d-143">Olá `--folder` parâmetro garante que o comando Olá cria uma pasta.</span><span class="sxs-lookup"><span data-stu-id="0b17d-143">hello `--folder` parameter ensures that hello command creates a folder.</span></span> <span data-ttu-id="0b17d-144">Se esse parâmetro não estiver presente, o comando Olá cria um arquivo vazio chamado mynewfolder na raiz de saudação do hello conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0b17d-144">If this parameter is not present, hello command creates an empty file called mynewfolder at hello root of hello Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a><span data-ttu-id="0b17d-145">Carregar conta de repositório Data Lake tooa dados</span><span class="sxs-lookup"><span data-stu-id="0b17d-145">Upload data tooa Data Lake Store account</span></span>

<span data-ttu-id="0b17d-146">Você pode carregar repositório data Lake de tooData diretamente no hello nível ou tooa pasta raiz que você criou na conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b17d-146">You can upload data tooData Lake Store directly at hello root level or tooa folder that you created within hello account.</span></span> <span data-ttu-id="0b17d-147">trechos de saudação a seguir demonstram como tooupload alguma pasta de toohello de dados de exemplo (**mynewfolder**) criado na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="0b17d-147">hello snippets below demonstrate how tooupload some sample data toohello folder (**mynewfolder**) you created in hello previous section.</span></span>

<span data-ttu-id="0b17d-148">Se você estiver procurando por alguns tooupload de dados de exemplo, você pode obter Olá **ambulância dados** pasta Olá [repositório Git do Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="0b17d-148">If you are looking for some sample data tooupload, you can get hello **Ambulance Data** folder from hello [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="0b17d-149">Baixe o arquivo hello e armazená-lo em um diretório local no seu computador, como C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="0b17d-149">Download hello file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="0b17d-150">Para destino hello, você deve especificar o caminho completo hello, incluindo o nome do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="0b17d-150">For hello destination, you must specify hello complete path including hello file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="0b17d-151">Listar arquivos em uma conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0b17d-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="0b17d-152">Use Olá seguintes comando toolist Olá arquivos em uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0b17d-152">Use hello following command toolist hello files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="0b17d-153">saída de Hello isso deve ser a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="0b17d-153">hello output of this should be similar toohello following:</span></span>

    [
        {
            "accessTime": 1491323529542,
            "aclBit": false,
            "blockSize": 268435456,
            "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "length": 1589881,
            "modificationTime": 1491323531638,
            "msExpirationTime": 0,
            "name": "mynewfolder/vehicle1_09142014.csv",
            "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
            "pathSuffix": "vehicle1_09142014.csv",
            "permission": "770",
            "replication": 1,
            "type": "FILE"
        }
    ]

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="0b17d-154">Renomear, baixar e excluir dados de uma conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0b17d-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="0b17d-155">**um arquivo de toorename**, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b17d-155">**toorename a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="0b17d-156">**um arquivo de toodownload**, use Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="0b17d-156">**toodownload a file**, use hello following command.</span></span> <span data-ttu-id="0b17d-157">Verifique se o caminho de destino de saudação especificado já existe.</span><span class="sxs-lookup"><span data-stu-id="0b17d-157">Make sure hello destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="0b17d-158">comando Olá cria a pasta de destino de saudação se ele não existe.</span><span class="sxs-lookup"><span data-stu-id="0b17d-158">hello command creates hello destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="0b17d-159">**um arquivo de toodelete**, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b17d-159">**toodelete a file**, use hello following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="0b17d-160">Se você quiser toodelete Olá pasta **mynewfolder** e arquivo hello **vehicle1_09142014_copy.csv** juntos em um comando, use hello – recurse parâmetro</span><span class="sxs-lookup"><span data-stu-id="0b17d-160">If you want toodelete hello folder **mynewfolder** and hello file **vehicle1_09142014_copy.csv** together in one command, use hello --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="0b17d-161">Trabalhar com permissões e ACLs para uma conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0b17d-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="0b17d-162">Nesta seção, você aprenderá sobre como toomanage ACLs e permissões usando 2.0 do CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="0b17d-162">In this section you learn about how toomanage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="0b17d-163">Para obter uma discussão detalhada sobre como as ACLs são implementadas no Azure Data Lake Store, confira [Controle de acesso no Azure Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="0b17d-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="0b17d-164">**proprietário de saudação tooupdate de um arquivo/pasta**, usar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b17d-164">**tooupdate hello owner of a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="0b17d-165">**permissões de saudação tooupdate para uma arquivo/pasta**, usar Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b17d-165">**tooupdate hello permissions for a file/folder**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="0b17d-166">**Olá tooget ACLs para um determinado caminho**, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b17d-166">**tooget hello ACLs for a given path**, use hello following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="0b17d-167">saída de Hello deve ser a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="0b17d-167">hello output should be similar toohello following:</span></span>

        {
            "entries": [
            "user::rwx",
            "group::rwx",
            "other::---"
          ],
          "group": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "owner": "1808bd5f-62af-45f4-89d8-03c5e81bac20",
          "permission": "770",
          "stickyBit": false
        }

* <span data-ttu-id="0b17d-168">**uma entrada para uma ACL de tooset**, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b17d-168">**tooset an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="0b17d-169">**uma entrada para uma ACL de tooremove**, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b17d-169">**tooremove an entry for an ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="0b17d-170">**tooremove um padrão de inteiro ACL**, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b17d-170">**tooremove an entire default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="0b17d-171">**tooremove uma ACL padrão não inteira**, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="0b17d-171">**tooremove an entire non-default ACL**, use hello following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="0b17d-172">Excluir uma conta do Repositório do Data Lake</span><span class="sxs-lookup"><span data-stu-id="0b17d-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="0b17d-173">Use Olá após o comando toodelete uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="0b17d-173">Use hello following command toodelete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="0b17d-174">Quando solicitado, insira **Y** toodelete conta de saudação.</span><span class="sxs-lookup"><span data-stu-id="0b17d-174">When prompted, enter **Y** toodelete hello account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0b17d-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0b17d-175">Next steps</span></span>

* [<span data-ttu-id="0b17d-176">Referência da CLI 2.0 do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="0b17d-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="0b17d-177">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="0b17d-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="0b17d-178">Usar a Análise Data Lake do Azure com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="0b17d-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="0b17d-179">Usar o Azure HDInsight com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="0b17d-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
