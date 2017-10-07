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
# <a name="get-started-with-azure-data-lake-store-using-azure-cli-20"></a>Introdução ao Azure Data Lake Store usando a CLI do Azure 2.0
> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [SDK .NET](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [CLI 2.0 do Azure](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Saiba como toocreate toouse 2.0 do CLI do Azure uma Data Lake do Azure armazenam conta e executar operações básicas, como criar pastas, carregar e baixar arquivos de dados, excluir sua conta, etc. Para saber mais sobre o Data Lake Store, veja [Visão geral do Data Lake Store](data-lake-store-overview.md).

Olá 2.0 do CLI do Azure é a nova experiência de linha de comando do Azure para gerenciar recursos do Azure. Ela pode ser usada em Windows, Linux e macOS. Para obter mais informações, consulte [Visão geral da CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/overview). Você também pode examinar Olá [referência do armazenamento do Azure Data Lake CLI 2.0](https://docs.microsoft.com/cli/azure/dls) para obter uma lista completa de comandos e sintaxe.


## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este artigo, você deve ter o seguinte hello:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

* **CLI do Azure 2.0** -consulte [Instalar a CLI do Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli) para obter instruções.

## <a name="authentication"></a>Autenticação

Este artigo usa uma abordagem de autenticação mais simples com o Data Lake Store, em que você faz logon como um usuário final. Olá acesso nível tooData Lake repositório conta de sistema de arquivos e, em seguida, é controlado pelo nível de acesso de saudação do hello usuário conectado no. No entanto, há outras abordagens como tooauthenticate bem com repositório Data Lake, que são **autenticação do usuário final** ou **autenticação de serviço a serviço**. Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).


## <a name="log-in-tooyour-azure-subscription"></a>Faça logon no tooyour assinatura do Azure

1. Faça logon em sua assinatura do Azure.

    ```azurecli
    az login
    ```

    Você obtém um código toouse na próxima etapa do hello. Usar uma web navegador tooopen Olá página https://aka.ms/devicelogin e insira Olá código tooauthenticate. Você está toolog solicitada usando suas credenciais.

2. Depois de fazer logon em todas as listas de janelas do Olá Olá assinaturas do Azure que estão associadas com sua conta. Use Olá após o comando toouse uma assinatura específica.
   
    ```azurecli
    az account set --subscription <subscription id> 
    ```

## <a name="create-an-azure-data-lake-store-account"></a>Criar uma conta do Repositório Azure Data Lake

1. Crie um novo grupo de recursos. Olá comando a seguir, forneça Olá valores de parâmetro que você deseja toouse. Se Olá local nome contiver espaços, coloque-o entre aspas. Por exemplo "Leste dos EUA 2". 
   
    ```azurecli
    az group create --location "East US 2" --name myresourcegroup
    ```

2. Crie conta de repositório Data Lake hello.
   
    ```azurecli
    az dls account create --account mydatalakestore --resource-group myresourcegroup
    ```

## <a name="create-folders-in-a-data-lake-store-account"></a>Criar pastas na conta do Repositório Data Lake

Você pode criar pastas em seu toomanage de conta do repositório Azure Data Lake e armazenar dados. Saudação de uso após o comando toocreate uma pasta chamada **mynewfolder** na raiz de saudação do hello repositório Data Lake.

```azurecli
az dls fs create --account mydatalakestore --path /mynewfolder --folder
```

> [!NOTE]
> Olá `--folder` parâmetro garante que o comando Olá cria uma pasta. Se esse parâmetro não estiver presente, o comando Olá cria um arquivo vazio chamado mynewfolder na raiz de saudação do hello conta do repositório Data Lake.
> 
>

## <a name="upload-data-tooa-data-lake-store-account"></a>Carregar conta de repositório Data Lake tooa dados

Você pode carregar repositório data Lake de tooData diretamente no hello nível ou tooa pasta raiz que você criou na conta de saudação. trechos de saudação a seguir demonstram como tooupload alguma pasta de toohello de dados de exemplo (**mynewfolder**) criado na seção anterior hello.

Se você estiver procurando por alguns tooupload de dados de exemplo, você pode obter Olá **ambulância dados** pasta Olá [repositório Git do Azure Data Lake](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData). Baixe o arquivo hello e armazená-lo em um diretório local no seu computador, como C:\sampledata\.

```azurecli
az dls fs upload --account mydatalakestore --source-path "C:\SampleData\AmbulanceData\vehicle1_09142014.csv" --destination-path "/mynewfolder/vehicle1_09142014.csv"
```

> [!NOTE]
> Para destino hello, você deve especificar o caminho completo hello, incluindo o nome do arquivo hello.
> 
>


## <a name="list-files-in-a-data-lake-store-account"></a>Listar arquivos em uma conta do Data Lake Store

Use Olá seguintes comando toolist Olá arquivos em uma conta do repositório Data Lake.

```azurecli
az dls fs list --account mydatalakestore --path /mynewfolder
```

saída de Hello isso deve ser a seguir toohello semelhante:

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

## <a name="rename-download-and-delete-data-from-a-data-lake-store-account"></a>Renomear, baixar e excluir dados de uma conta do Data Lake Store 

* **um arquivo de toorename**, use Olá comando a seguir:
  
    ```azurecli
    az dls fs move --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014.csv --destination-path /mynewfolder/vehicle1_09142014_copy.csv
    ```

* **um arquivo de toodownload**, use Olá comando a seguir. Verifique se o caminho de destino de saudação especificado já existe.
  
    ```azurecli     
    az dls fs download --account mydatalakestore --source-path /mynewfolder/vehicle1_09142014_copy.csv --destination-path "C:\mysampledata\vehicle1_09142014_copy.csv"
    ```

    > [!NOTE]
    > comando Olá cria a pasta de destino de saudação se ele não existe.
    > 
    >

* **um arquivo de toodelete**, use Olá comando a seguir:
  
    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder/vehicle1_09142014_copy.csv
    ```

    Se você quiser toodelete Olá pasta **mynewfolder** e arquivo hello **vehicle1_09142014_copy.csv** juntos em um comando, use hello – recurse parâmetro

    ```azurecli
    az dls fs delete --account mydatalakestore --path /mynewfolder --recurse
    ```

## <a name="work-with-permissions-and-acls-for-a-data-lake-store-account"></a>Trabalhar com permissões e ACLs para uma conta do Data Lake Store

Nesta seção, você aprenderá sobre como toomanage ACLs e permissões usando 2.0 do CLI do Azure. Para obter uma discussão detalhada sobre como as ACLs são implementadas no Azure Data Lake Store, confira [Controle de acesso no Azure Data Lake Store](data-lake-store-access-control.md).

* **proprietário de saudação tooupdate de um arquivo/pasta**, usar Olá comando a seguir:

    ```azurecli
    az dls fs access set-owner --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --group 80a3ed5f-959e-4696-ba3c-d3c8b2db6766 --owner 6361e05d-c381-4275-a932-5535806bb323
    ```

* **permissões de saudação tooupdate para uma arquivo/pasta**, usar Olá comando a seguir:

    ```azurecli
    az dls fs access set-permission --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv --permission 777
    ```
    
* **Olá tooget ACLs para um determinado caminho**, use Olá comando a seguir:

    ```azurecli
    az dls fs access show --account mydatalakestore --path /mynewfolder/vehicle1_09142014.csv
    ```

    saída de Hello deve ser a seguir toohello semelhante:

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

* **uma entrada para uma ACL de tooset**, use Olá comando a seguir:

    ```azurecli
    az dls fs access set-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323:-w-
    ```

* **uma entrada para uma ACL de tooremove**, use Olá comando a seguir:

    ```azurecli
    az dls fs access remove-entry --account mydatalakestore --path /mynewfolder --acl-spec user:6360e05d-c381-4275-a932-5535806bb323
    ```

* **tooremove um padrão de inteiro ACL**, use Olá comando a seguir:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder --default-acl
    ```

* **tooremove uma ACL padrão não inteira**, use Olá comando a seguir:

    ```azurecli
    az dls fs access remove-all --account mydatalakestore --path /mynewfolder
    ```
    
## <a name="delete-a-data-lake-store-account"></a>Excluir uma conta do Repositório do Data Lake
Use Olá após o comando toodelete uma conta do repositório Data Lake.

```azurecli
az dls account delete --account mydatalakestore
```

Quando solicitado, insira **Y** toodelete conta de saudação.

## <a name="next-steps"></a>Próximas etapas

* [Referência da CLI 2.0 do Azure Data Lake Store](https://docs.microsoft.com/cli/azure/dls)
* [Proteger dados no Repositório Data Lake](data-lake-store-secure-data.md)
* [Usar a Análise Data Lake do Azure com o Repositório Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Usar o Azure HDInsight com o Repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)

[azure-command-line-tools]: ../xplat-cli-install.md
