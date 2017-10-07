---
title: "aaaGet iniciado com análise Azure Data Lake usando 2.0 do CLI do Azure | Microsoft Docs"
description: "Saiba como toouse Olá 2.0 de Interface de linha de comando do Azure toocreate uma conta da análise Data Lake, criar um trabalho de análise Data Lake usando U-SQL e enviar o trabalho de saudação. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/18/2017
ms.author: jgao
ms.openlocfilehash: c4e91c0d3526e4932c2948c0a326d4cedc985791
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-cli-20"></a>Introdução ao Azure Data Lake Analytics usando a CLI do Azure 2.0
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Neste tutorial, você desenvolverá um trabalho que lê um arquivo TSV (Valores Separados por Tabulação) e irá convertê-lo em um arquivo CSV (valores separados por vírgula). ferramentas de toogo por meio de saudação mesmo tutorial usando outros com suporte, use Olá suspensa lista na parte superior da saudação desta seção.

## <a name="prerequisites"></a>Pré-requisitos
Antes de começar este tutorial, você deve ter Olá itens a seguir:

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **CLI 2.0 do Azure**. Consulte [Instalar e configurar a CLI do Azure](https://docs.microsoft.com/cli/azure/install-azure-cli).

## <a name="log-in-tooazure"></a>Faça logon no tooAzure

toolog em tooyour assinatura do Azure:

```
azurecli
az login
```

Você é solicitado toobrowse tooa URL e insira um código de autenticação.  E, em seguida, siga Olá instruções tooenter suas credenciais.

Depois de fazer logon, o comando de logon de saudação lista suas assinaturas.

toouse uma assinatura específica:

```
az account set --subscription <subscription id>
```

## <a name="create-data-lake-analytics-account"></a>Criar conta da Análise Data Lake
Você precisa ter uma conta do Data Lake Analytics antes de executar trabalhos. toocreate uma conta da análise Data Lake, você deve especificar Olá itens a seguir:

* **Grupo de recursos do Azure**. É necessário criar uma conta do Data Lake Analytics em um grupo de Recursos do Azure. [Gerenciador de recursos do Azure](../azure-resource-manager/resource-group-overview.md) permite que você toowork com recursos de saudação em seu aplicativo como um grupo. Você pode implantar, atualizar ou excluir todos os recursos de saudação para seu aplicativo em uma única operação coordenado.  

toolist Olá grupos de recursos existentes em sua assinatura:

```
az group list
```

toocreate um novo grupo de recursos:

```
az group create --name "<Resource Group Name>" --location "<Azure Location>"
```

* **Nome da conta do Data Lake Analytics**. Cada conta do Data Lake Analytics tem um nome.
* **Local**. Use um dos Olá data centers do Azure que dá suporte à análise Data Lake.
* **Conta padrão do Data Lake Store**: cada conta do Data Lake Analytics tem uma conta padrão do Data Lake Store.

conta de repositório Data Lake existente Olá de toolist:

```
az dls account list
```

toocreate uma nova conta do repositório Data Lake:

```azurecli
az dls account create --account "<Data Lake Store Account Name>" --resource-group "<Resource Group Name>"
```

Use Olá sintaxe toocreate uma conta da análise Data Lake a seguir:

```
az dla account create --account "<Data Lake Analytics Account Name>" --resource-group "<Resource Group Name>" --location "<Azure location>" --default-data-lake-store "<Default Data Lake Store Account Name>"
```

Depois de criar uma conta, você pode usar o hello contas de saudação toolist comandos a seguir e mostrar os detalhes da conta:

```
az dla account list
az dla account show --account "<Data Lake Analytics Account Name>"            
```

## <a name="upload-data-toodata-lake-store"></a>Carregar dados tooData Lake repositório
Neste tutorial, você processa alguns logs de pesquisa.  log de saudação de pesquisa pode ser armazenado no repositório Data Lake ou armazenamento de BLOBs do Azure.

Olá portal do Azure fornece uma interface de usuário para copiar alguns exemplo dados arquivos toohello repositório Data Lake conta padrão, que incluem um arquivo de log de pesquisa. Consulte [preparar os dados de origem](data-lake-analytics-get-started-portal.md) conta de repositório Data Lake tooupload Olá dados toohello padrão.

arquivos de tooupload usando 2.0 do CLI, use Olá comandos a seguir:

```
az dls fs upload --account "<Data Lake Store Account Name>" --source-path "<Source File Path>" --destination-path "<Destination File Path>"
az dls fs list --account "<Data Lake Store Account Name>" --path "<Path>"
```

A Análise Data Lake também pode acessar o armazenamento de Blob do Azure.  Para carregar o armazenamento de Blob de tooAzure de dados, consulte [hello usando a CLI do Azure com o armazenamento do Azure](../storage/common/storage-azure-cli.md).

## <a name="submit-data-lake-analytics-jobs"></a>Enviar trabalhos da Análise Data Lake
trabalhos de análise Data Lake Olá são escritos em Olá linguagem U-SQL. toolearn mais sobre U-SQL, consulte [Introdução à linguagem U-SQL](data-lake-analytics-u-sql-get-started.md) e [U-SQL idioma eence](http://go.microsoft.com/fwlink/?LinkId=691348).

**toocreate um script de trabalho de análise Data Lake**

Criar um arquivo de texto com o script U-SQL a seguir e salve a estação de trabalho tooyour arquivo de texto de saudação:

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    too"/data.csv"
    USING Outputters.Csv();
```

Este script U-SQL lê o arquivo de dados de origem de hello usando **Extractors.Tsv()**e, em seguida, cria um arquivo csv usando **Outputters.Csv()**.

Não modifique dois caminhos de saudação, a menos que você copia o arquivo de origem de saudação em um local diferente.  Análise data Lake cria a pasta de saída de hello se ele não existir.

É mais simples toouse os caminhos relativos para os arquivos armazenados em contas do repositório Data Lake padrão. Você também pode usar caminhos absolutos.  Por exemplo:

```
adl://<Data LakeStorageAccountName>.azuredatalakestore.net:443/Samples/Data/SearchLog.tsv
```

Você deve usar arquivos de tooaccess caminhos absolutos em contas de armazenamento vinculadas.  sintaxe de saudação para arquivos armazenados na conta de armazenamento do Azure vinculada é:

```
wasb://<BlobContainerName>@<StorageAccountName>.blob.core.windows.net/Samples/Data/SearchLog.tsv
```

> [!NOTE]
> Não há suporte para o contêiner de Blob do Azure com blobs públicos.      
> Não há suporte para o contêiner de Blob do Azure com contêineres públicos.      
>

**trabalhos de toosubmit**

Use Olá sintaxe toosubmit um trabalho a seguir.

```
az dla job submit --account "<Data Lake Analytics Account Name>" --job-name "<Job Name>" --script "<Script Path and Name>"
```

Por exemplo:

```
az dla job submit --account "myadlaaccount" --job-name "myadlajob" --script @"C:\DLA\myscript.txt"
```

**trabalhos de toolist e mostrar detalhes do trabalho**

```
azurecli
az dla job list --account "<Data Lake Analytics Account Name>"
az dla job show --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

**trabalhos de toocancel**

```
az dla job cancel --account "<Data Lake Analytics Account Name>" --job-identity "<Job Id>"
```

## <a name="retrieve-job-results"></a>Recuperar os resultados do trabalho

Depois que um trabalho é concluído, você pode usar Olá Olá comandos toolist nos arquivos de saída a seguir e baixar arquivos de saudação:

```
az dls fs list --account "<Data Lake Store Account Name>" --source-path "/Output" --destination-path "<Destintion>"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv"
az dls fs preview --account "<Data Lake Store Account Name>" --path "/Output/SearchLog-from-Data-Lake.csv" --length 128 --offset 0
az dls fs downlod --account "<Data Lake Store Account Name>" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "<Destination Path and File Name>"
```

Por exemplo:

```
az dls fs downlod --account "myadlsaccount" --source-path "/Output/SearchLog-from-Data-Lake.csv" --destintion-path "C:\DLA\myfile.csv"
```

## <a name="pipelines-and-recurrences"></a>Pipelines e recorrências

**Obter informações sobre pipelines e recorrências**

Saudação de uso `az dla job pipeline` comandos informações de pipeline Olá toosee trabalhos enviados anteriormente.

```
az dla job pipeline list --account "<Data Lake Analytics Account Name>"

az dla job pipeline show --account "<Data Lake Analytics Account Name>" --pipeline-identity "<Pipeline ID>"
```

Saudação de uso `az dla job recurrence` comandos toosee as informações de recorrência Olá para trabalhos enviados anteriormente.

```
az dla job recurrence list --account "<Data Lake Analytics Account Name>"

az dla job recurrence show --account "<Data Lake Analytics Account Name>" --recurrence-identity "<Recurrence ID>"
```

## <a name="next-steps"></a>Próximas etapas

* Olá toosee documento de referência do Data Lake análise CLI 2.0, consulte [análise Data Lake](https://docs.microsoft.com/cli/azure/dla).
* Olá toosee documento de referência da CLI de repositório Data Lake 2.0, consulte [repositório Data Lake](https://docs.microsoft.com/cli/azure/dls).
* toosee uma consulta mais complexa, consulte [site analisar logs usando a análise do Azure Data Lake](data-lake-analytics-analyze-weblogs.md).
