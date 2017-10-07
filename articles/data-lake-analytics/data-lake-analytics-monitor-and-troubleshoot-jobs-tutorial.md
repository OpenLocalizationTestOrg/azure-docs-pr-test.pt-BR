---
title: "trabalhos de análise do Azure Data Lake aaaTroubleshoot usando o Portal do Azure | Microsoft Docs"
description: "Saiba como toouse Olá trabalhos de análise Data Lake tootroubleshoot Portal do Azure. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: b7066d81-3142-474f-8a34-32b0b39656dc
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: e810d56bab8f1a8254721ec9906bb6a4508dc22a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-data-lake-analytics-jobs-using-azure-portal"></a>Solucionar problemas em trabalhos da Análise do Azure Data Lake usando o Portal do Azure
Saiba como toouse Olá trabalhos de análise Data Lake tootroubleshoot Portal do Azure.

Neste tutorial, você será um problema ausente do arquivo de origem de instalação e usar hello Azure Portal tootroubleshoot Olá problema.

## <a name="submit-a-data-lake-analytics-job"></a>Enviar um trabalho da Análise Data Lake

Envie Olá trabalho U-SQL a seguir:

```
@searchlog =
   EXTRACT UserId          int,
           Start           DateTime,
           Region          string,
           Query           string,
           Duration        int?,
           Urls            string,
           ClickedUrls     string
   FROM "/Samples/Data/SearchLog.tsv1"
   USING Extractors.Tsv();

OUTPUT @searchlog   
   too"/output/SearchLog-from-adls.csv"
   USING Outputters.Csv();
```
    
Olá definido no script de saudação do arquivo de origem é **/Samples/Data/SearchLog.tsv1**, onde deve ser **/Samples/Data/SearchLog.tsv**.


## <a name="troubleshoot-hello-job"></a>Solucionar problemas de trabalho Olá

**toosee todos os trabalhos de Olá**

1. De Olá portal do Azure, clique em **Microsoft Azure** no canto superior esquerdo da saudação.
2. Clique em Olá lado a lado com o seu nome de conta da análise Data Lake.  Resumo do trabalho de saudação é mostrado na Olá **Job Management** lado a lado.

    ![Gerenciamento de trabalhos da Análise Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-job-management.png)

    Gerenciamento de trabalho de saudação fornece rapidamente Olá status do trabalho. Observe que há um trabalho com falha.
3. Clique em Olá **gerenciamento de trabalho** trabalhos de saudação toosee lado a lado. trabalhos de saudação são categorizados em **executando**, **em fila**, e **finalizado**. Você deverá ver o trabalho com falha em Olá **finalizado** seção. Ele deverá ser o primeiro na lista de saudação. Quando você tiver muitos trabalhos, você pode clicar em **filtro** toohelp você toolocate trabalhos.

    ![Trabalhos de filtragem da Análise Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-filter-jobs.png)
4. Clique em trabalho com falha de saudação de detalhes do trabalho Olá lista tooopen Olá em uma nova folha:

    ![Trabalho com falha da Análise Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job.png)

    Saudação de aviso **reenviar** botão. Depois de corrigir o problema de saudação, você pode enviar novamente trabalho hello.
5. Clique em parte destacada da saudação anterior captura de tela tooopen Olá detalhes do erro.  Você verá algo semelhante ao seguinte:

    ![Detalhes do trabalho com falha da Análise Azure Data Lake](./media/data-lake-analytics-monitor-and-troubleshoot-tutorial/data-lake-analytics-failed-job-details.png)

    Ele informa a pasta de origem Olá não foi encontrada.
6. Clique em **Duplicar Script**.
7. Saudação de atualização **FROM** a seguir toohello caminho:

    "/Samples/Data/SearchLog.tsv"
8. Clique em **Enviar Trabalho**.

## <a name="see-also"></a>Confira também
* [Visão geral da Análise Azure Data Lake](data-lake-analytics-overview.md)
* [Introdução à Análise Azure Data Lake usando o Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Introdução ao U-SQL da Análise Azure Data Lake usando o Visual Studio](data-lake-analytics-u-sql-get-started.md)
* [Gerenciar a Análise do Azure Data Lake usando o Portal do Azure](data-lake-analytics-manage-use-portal.md)
