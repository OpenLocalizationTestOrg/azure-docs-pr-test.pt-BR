---
title: "aaaGet iniciado com análise Azure Data Lake usando o Azure PowerShell | Microsoft Docs"
description: "Usar o Azure PowerShell toocreate uma conta da análise Data Lake, criar um trabalho de análise Data Lake usando U-SQL e enviar o trabalho de saudação. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 8a4e901e-9656-4a60-90d0-d78ff2f00656
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/04/2017
ms.author: edmaca
ms.openlocfilehash: cb9b35352d1cc9a78337448b1d6835875a212e08
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-powershell"></a>Introdução ao Azure Data Lake Analytics usando o Azure PowerShell
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Saiba como toouse toocreate do PowerShell do Azure análise Azure Data Lake contas e, em seguida, enviar e executar trabalhos de U-SQL. Para saber mais sobre a Análise Data Lake, consulte a [Visão geral da Análise Data Lake do Azure](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar este tutorial, você deve ter Olá informações a seguir:

* **Uma conta da Análise Azure Data Lake**. Veja [Introdução ao Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-get-started-portal).
* **Uma estação de trabalho com o PowerShell do Azure**. Consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

## <a name="log-in-tooazure"></a>Faça logon no tooAzure

Este tutorial pressupõe que você já esteja familiarizado com o uso do Azure PowerShell. Em particular, você precisa tooknow como toolog em tooAzure. Consulte Olá [começar com o Azure PowerShell](https://docs.microsoft.com/en-us/powershell/azure/get-started-azureps) se precisar de Ajuda.

toolog com um nome de assinatura:

```
Login-AzureRmAccount -SubscriptionName "ContosoSubscription"
```

Em vez do nome da assinatura hello, você também pode usar um toolog de id de assinatura em:

```
Login-AzureRmAccount -SubscriptionId "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
```

Se for bem-sucedido, saída desse comando Olá aparência Olá texto a seguir:

```
Environment           : AzureCloud
Account               : joe@contoso.com
TenantId              : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionId        : "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"
SubscriptionName      : ContosoSubscription
CurrentStorageAccount :
```

## <a name="preparing-for-hello-tutorial"></a>Preparando para o tutorial Olá

trechos do PowerShell Olá neste tutorial usam essas variáveis toostore essas informações:

```
$rg = "<ResourceGroupName>"
$adls = "<DataLakeStoreAccountName>"
$adla = "<DataLakeAnalyticsAccountName>"
$location = "East US 2"
```

## <a name="get-information-about-a-data-lake-analytics-account"></a>Obter informações sobre uma conta do Data Lake Analytics

```
Get-AdlAnalyticsAccount -ResourceGroupName $rg -Name $adla  
```

## <a name="submit-a-u-sql-job"></a>Enviar um trabalho do U-SQL

Crie um script do PowerShell toohold variável Olá U-SQL.

```
$script = @"
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

"@
```

Envie o script hello.

```
$job = Submit-AdlJob -AccountName $adla –Script $script
```

Como alternativa, você pode salvar o script hello como um arquivo e enviar com hello comando a seguir:

```
$filename = "d:\test.usql"
$script | out-File $filename
$job = Submit-AdlJob -AccountName $adla –ScriptPath $filename
```


Obter status de saudação de um trabalho específico. Continue a usar este cmdlet até que você veja Olá trabalho está concluído.

```
$job = Get-AdlJob -AccountName $adla -JobId $job.JobId
```

Em vez de chamar Get-AdlAnalyticsJob repetidamente até que um trabalho é concluído, você pode usar o hello espera AdlJob cmdlet.

```
Wait-AdlJob -Account $adla -JobId $job.JobId
```

Baixe o arquivo de saída de hello.

```
Export-AdlStoreItem -AccountName $adls -Path "/data.csv" -Destination "C:\data.csv"
```

## <a name="see-also"></a>Consulte também
* toosee Olá mesmo tutorial usando outras ferramentas, clique em seletores de guia Olá na parte superior de saudação da página de saudação.
* toolearn U-SQL, consulte [começar com a linguagem da análise Azure Data Lake U-SQL](data-lake-analytics-u-sql-get-started.md).
* Para obter as tarefas de gerenciamento, confira [Gerenciar o Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-manage-use-portal.md).
