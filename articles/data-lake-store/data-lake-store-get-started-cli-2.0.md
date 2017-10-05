---
title: "Use a interface de linha de comando do Azure 2.0 para começar a usar o Azure Data Lake Store | Microsoft Docs"
description: "Usar a linha de comando da plataforma cruzada do Azure 2.0 para criar uma conta do Data Lake Store e executar operações básicas"
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
ms.openlocfilehash: ed78d25f2bac0a9996f1796ee503f31a36940977
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a><span data-ttu-id="a71f0-103">Introdução ao Azure Data Lake Store usando a CLI do Azure 2.0</span><span class="sxs-lookup"><span data-stu-id="a71f0-103">Get started with Azure Data Lake Store using Azure CLI 2.0</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a71f0-104">Portal</span><span class="sxs-lookup"><span data-stu-id="a71f0-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="a71f0-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a71f0-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="a71f0-106">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="a71f0-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="a71f0-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="a71f0-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="a71f0-108">API REST</span><span class="sxs-lookup"><span data-stu-id="a71f0-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="a71f0-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="a71f0-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="a71f0-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="a71f0-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="a71f0-111">Python</span><span class="sxs-lookup"><span data-stu-id="a71f0-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="a71f0-112">Saiba como usar a CLI 2.0 para criar uma conta do Azure Data Lake Store e executar operações básicas, como criar pastas, carregar e baixar arquivos de dados, excluir sua conta, etc. Para saber mais sobre o Data Lake Store, veja [Visão geral do Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a71f0-112">Learn how to use Azure CLI 2.0 to create an Azure Data Lake Store account and perform basic operations such as create folders, upload and download data files, delete your account, etc. For more information about Data Lake Store, see [Overview of Data Lake Store](data-lake-store-overview.md).</span></span>

<span data-ttu-id="a71f0-113">A CLI 2.0 do Azure é a nova experiência de linha de comando do Azure para gerenciar recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="a71f0-113">The Azure CLI 2.0 is Azure's new command-line experience for managing Azure resources.</span></span> <span data-ttu-id="a71f0-114">Ela pode ser usada em Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="a71f0-114">It can be used on macOS, Linux, and Windows.</span></span> <span data-ttu-id="a71f0-115">Para obter mais informações, consulte [Visão geral da CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="a71f0-115">For more information, see [Overview of Azure CLI 2.0](https://docs.microsoft.com/cli/azure/overview).</span></span> <span data-ttu-id="a71f0-116">Você também pode examinar a [referência da CLI 2.0 do Azure Data Lake Store](https://docs.microsoft.com/cli/azure/dls) para obter uma lista completa de comandos e sintaxes.</span><span class="sxs-lookup"><span data-stu-id="a71f0-116">You can also look at the [Azure Data Lake Store CLI 2.0 reference](https://docs.microsoft.com/cli/azure/dls) for a complete list of commands and syntax.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a71f0-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a71f0-117">Prerequisites</span></span>
<span data-ttu-id="a71f0-118">Antes de começar este artigo, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a71f0-118">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="a71f0-119">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="a71f0-119">**An Azure subscription**.</span></span> <span data-ttu-id="a71f0-120">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="a71f0-120">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="a71f0-121">**CLI do Azure 2.0** -consulte [Instalar a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="a71f0-121">**Azure CLI 2.0** - See [Install Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) for instructions.</span></span>

## <a name="authentication"></a><span data-ttu-id="a71f0-122">Autenticação</span><span class="sxs-lookup"><span data-stu-id="a71f0-122">Authentication</span></span>

<span data-ttu-id="a71f0-123">Este artigo usa uma abordagem de autenticação mais simples com o Data Lake Store, em que você faz logon como um usuário final.</span><span class="sxs-lookup"><span data-stu-id="a71f0-123">This article uses a simpler authentication approach with Data Lake Store where you log in as an end-user user.</span></span> <span data-ttu-id="a71f0-124">O nível de acesso à conta do Data Lake Store e ao sistema de arquivos é controlado pelo nível de acesso do usuário conectado.</span><span class="sxs-lookup"><span data-stu-id="a71f0-124">The access level to Data Lake Store account and file system is then governed by the access level of the logged in user.</span></span> <span data-ttu-id="a71f0-125">No entanto, há outras abordagens para autenticar com o Data Lake Store, que são a **autenticação de usuário final** ou a **autenticação serviço a serviço**.</span><span class="sxs-lookup"><span data-stu-id="a71f0-125">However, there are other approaches as well to authenticate with Data Lake Store, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="a71f0-126">Para obter instruções e saber mais sobre como se autenticar, veja [Autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [Autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="a71f0-126">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>


## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="a71f0-127">Entre na sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="a71f0-127">Log in to your Azure subscription</span></span>

1. <span data-ttu-id="a71f0-128">Faça logon em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="a71f0-128">Log into your Azure subscription.</span></span>

    ```azurecli
    az login
    ```

    <span data-ttu-id="a71f0-129">Você recebe um código para usar na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="a71f0-129">You get a code to use in the next step.</span></span> <span data-ttu-id="a71f0-130">Use um navegador da Web para abrir a página https://aka.ms/devicelogin e insira o código para autenticar.</span><span class="sxs-lookup"><span data-stu-id="a71f0-130">Use a web browser to open the page https://aka.ms/devicelogin and enter the code to authenticate.</span></span> <span data-ttu-id="a71f0-131">Você precisará fazer logon usando suas credenciais.</span><span class="sxs-lookup"><span data-stu-id="a71f0-131">You are prompted to log in using your credentials.</span></span>

2. <span data-ttu-id="a71f0-132">Depois de fazer logon, a janela listará todas as assinaturas do Azure que estão associadas à conta.</span><span class="sxs-lookup"><span data-stu-id="a71f0-132">Once you log in, the window lists all the Azure subscriptions that are associated with your account.</span></span> <span data-ttu-id="a71f0-133">Use o comando a seguir para usar uma assinatura específica.</span><span class="sxs-lookup"><span data-stu-id="a71f0-133">Use the following command to use a specific subscription.</span></span>
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="a71f0-134">Criar uma conta do Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="a71f0-134">Create an Azure Data Lake Store account</span></span>

1. <span data-ttu-id="a71f0-135">Crie um novo grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="a71f0-135">Create a new resource group.</span></span> <span data-ttu-id="a71f0-136">No comando a seguir fornecem os valores de parâmetro que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="a71f0-136">In the following command, provide the parameter values you want to use.</span></span> <span data-ttu-id="a71f0-137">Se o nome do local contiver espaços, coloque-o entre aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="a71f0-137">If the location name contains spaces, put it in quotes.</span></span> <span data-ttu-id="a71f0-138">Por exemplo "Leste dos EUA 2".</span><span class="sxs-lookup"><span data-stu-id="a71f0-138">For example "East US 2".</span></span> 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. <span data-ttu-id="a71f0-139">Crie uma conta do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a71f0-139">Create the Data Lake Store account.</span></span>
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="a71f0-140">Criar pastas na conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="a71f0-140">Create folders in a Data Lake Store account</span></span>

<span data-ttu-id="a71f0-141">Você pode criar pastas em sua conta do Repositório Azure Data Lake para gerenciar e armazenar dados.</span><span class="sxs-lookup"><span data-stu-id="a71f0-141">You can create folders under your Azure Data Lake Store account to manage and store data.</span></span> <span data-ttu-id="a71f0-142">Use o seguinte comando para criar uma pasta chamada **mynewfolder** na raiz do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a71f0-142">Use the following command to create a folder called **mynewfolder** at the root of the Data Lake Store.</span></span>

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> <span data-ttu-id="a71f0-143">O parâmetro `--folder` faz com que o comando cria uma pasta.</span><span class="sxs-lookup"><span data-stu-id="a71f0-143">The `--folder` parameter ensures that the command creates a folder.</span></span> <span data-ttu-id="a71f0-144">Se esse parâmetro não estiver presente, o comando criará um arquivo vazio chamado mynewfolder na raiz da conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="a71f0-144">If this parameter is not present, the command creates an empty file called mynewfolder at the root of the Data Lake Store account.</span></span>
> 
>

## <a name="upload-data-to-a-data-lake-store-account"></a><span data-ttu-id="a71f0-145">Carregar dados na conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a71f0-145">Upload data to a Data Lake Store account</span></span>

<span data-ttu-id="a71f0-146">É possível carregar dados no Data Lake Store diretamente no nível da raiz ou em uma pasta que você criou na conta.</span><span class="sxs-lookup"><span data-stu-id="a71f0-146">You can upload data to Data Lake Store directly at the root level or to a folder that you created within the account.</span></span> <span data-ttu-id="a71f0-147">Os trechos de código abaixo demonstram como carregar alguns dados de exemplo no diretório (**mynewdirectory**) criado na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="a71f0-147">The snippets below demonstrate how to upload some sample data to the folder (**mynewfolder**) you created in the previous section.</span></span>

<span data-ttu-id="a71f0-148">Se estiver procurando alguns dados de exemplo para carregar, é possível obter a pasta **Dados da Ambulância** no [Repositório Git do Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span><span class="sxs-lookup"><span data-stu-id="a71f0-148">If you are looking for some sample data to upload, you can get the **Ambulance Data** folder from the [Azure Data Lake Git Repository](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).</span></span> <span data-ttu-id="a71f0-149">Baixe o arquivo e armazene-o em um diretório local no computador, como C:\sampledata\.</span><span class="sxs-lookup"><span data-stu-id="a71f0-149">Download the file and store it in a local directory on your computer, such as  C:\sampledata\.</span></span>

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> <span data-ttu-id="a71f0-150">Para o destino, você deve especificar o caminho completo, incluindo o nome do arquivo.</span><span class="sxs-lookup"><span data-stu-id="a71f0-150">For the destination, you must specify the complete path including the file name.</span></span>
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a><span data-ttu-id="a71f0-151">Listar arquivos em uma conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a71f0-151">List files in a Data Lake Store account</span></span>

<span data-ttu-id="a71f0-152">Use o comando a seguir para listar os arquivos em uma conta do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a71f0-152">Use the following command to list the files in a Data Lake Store account.</span></span>

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

<span data-ttu-id="a71f0-153">A saída desse comando deve ser:</span><span class="sxs-lookup"><span data-stu-id="a71f0-153">The output of this should be similar to the following:</span></span>

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

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a><span data-ttu-id="a71f0-154">Renomear, baixar e excluir dados de uma conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a71f0-154">Rename, download, and delete data from a Data Lake Store account</span></span> 

* <span data-ttu-id="a71f0-155">**Para renomear um arquivo**, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a71f0-155">**To rename a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* <span data-ttu-id="a71f0-156">**Para baixar um arquivo**, use o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="a71f0-156">**To download a file**, use the following command.</span></span> <span data-ttu-id="a71f0-157">Verifique se o caminho de destino especificado já existe.</span><span class="sxs-lookup"><span data-stu-id="a71f0-157">Make sure the destination path you specify already exists.</span></span>
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > <span data-ttu-id="a71f0-158">O comando criará a pasta de destino se ela não existir.</span><span class="sxs-lookup"><span data-stu-id="a71f0-158">The command creates the destination folder if it does not exist.</span></span>
    > 
    >

* <span data-ttu-id="a71f0-159">**Para excluir um arquivo**, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a71f0-159">**To delete a file**, use the following command:</span></span>
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    <span data-ttu-id="a71f0-160">Se você quiser excluir a pasta **mynewfolder** e o arquivo **vehicle1_09142014_copy.csv** juntos em um comando, use o parâmetro -- recurse</span><span class="sxs-lookup"><span data-stu-id="a71f0-160">If you want to delete the folder **mynewfolder** and the file **vehicle1_09142014_copy.csv** together in one command, use the --recurse parameter</span></span>

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a><span data-ttu-id="a71f0-161">Trabalhar com permissões e ACLs para uma conta do Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a71f0-161">Work with permissions and ACLs for a Data Lake Store account</span></span>

<span data-ttu-id="a71f0-162">Nesta seção, saiba mais sobre como gerenciar ACLs e permissões usando a CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="a71f0-162">In this section you learn about how to manage ACLs and permissions using Azure CLI 2.0.</span></span> <span data-ttu-id="a71f0-163">Para obter uma discussão detalhada sobre como as ACLs são implementadas no Azure Data Lake Store, confira [Controle de acesso no Azure Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="a71f0-163">For a detailed discussion on how ACLs are implemented in Azure Data Lake Store, see [Access control in Azure Data Lake Store](data-lake-store-access-control.md).</span></span>

* <span data-ttu-id="a71f0-164">**Para atualizar o proprietário de um arquivo/pasta**, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a71f0-164">**To update the owner of a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="a71f0-165">**Para atualizar as permissões para uma arquivo/pasta**, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a71f0-165">**To update the permissions for a file/folder**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* <span data-ttu-id="a71f0-166">**Para obter as ACLs para um determinado caminho**, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a71f0-166">**To get the ACLs for a given path**, use the following command:</span></span>

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    <span data-ttu-id="a71f0-167">A saída deverá ser semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="a71f0-167">The output should be similar to the following:</span></span>

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

* <span data-ttu-id="a71f0-168">**Para definir uma entrada de uma ACL**, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a71f0-168">**To set an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* <span data-ttu-id="a71f0-169">**Para remover uma entrada de uma ACL**, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a71f0-169">**To remove an entry for an ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* <span data-ttu-id="a71f0-170">**Para remover uma ACL padrão inteira**, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a71f0-170">**To remove an entire default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* <span data-ttu-id="a71f0-171">**Para remover uma ACL não padrão inteira**, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a71f0-171">**To remove an entire non-default ACL**, use the following command:</span></span>

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="a71f0-172">Excluir uma conta do Repositório do Data Lake</span><span class="sxs-lookup"><span data-stu-id="a71f0-172">Delete a Data Lake Store account</span></span>
<span data-ttu-id="a71f0-173">Use o comando a seguir para excluir sua conta do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a71f0-173">Use the following command to delete a Data Lake Store account.</span></span>

```azurecli
az dls account delete --account mydatalakestore
```

<span data-ttu-id="a71f0-174">Quando solicitado, insira **Y** para excluir a conta.</span><span class="sxs-lookup"><span data-stu-id="a71f0-174">When prompted, enter **Y** to delete the account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a71f0-175">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a71f0-175">Next steps</span></span>

* [<span data-ttu-id="a71f0-176">Referência da CLI 2.0 do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a71f0-176">Azure Data Lake Store CLI 2.0 reference</span></span>](https://docs.microsoft.com/cli/azure/dls)
* [<span data-ttu-id="a71f0-177">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="a71f0-177">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="a71f0-178">Usar a Análise Data Lake do Azure com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="a71f0-178">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="a71f0-179">Usar o Azure HDInsight com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="a71f0-179">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
