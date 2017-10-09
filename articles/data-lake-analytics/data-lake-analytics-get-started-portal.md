---
title: "aaaGet iniciado com análise Azure Data Lake usando o portal do Azure | Microsoft Docs"
description: "Saiba como Olá toouse toocreate portal do Azure uma conta da análise Data Lake, criar um trabalho de análise Data Lake usando U-SQL e enviar o trabalho de saudação. "
services: data-lake-analytics
documentationcenter: 
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: b1584d16-e0d2-4019-ad1f-f04be8c5b430
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/21/2017
ms.author: edmaca
ms.openlocfilehash: 6bb54404fa42cfed25b18bc2bfb7c72e6c361149
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-azure-portal"></a>Introdução ao Azure Data Lake Analytics usando o Portal do Azure
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Saiba como toouse Olá contas de análise do Azure Data Lake toocreate portal do Azure, definir trabalhos em [U-SQL](data-lake-analytics-u-sql-get-started.md)e envie-o serviço de análise Data Lake toohello trabalhos. Para saber mais sobre a Análise Data Lake, consulte a [Visão geral da Análise Data Lake do Azure](data-lake-analytics-overview.md).

## <a name="prerequisites"></a>Pré-requisitos

Antes de começar este tutorial, você deve ter uma **assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-a-data-lake-analytics-account"></a>Criar uma conta da Análise Data Lake

Agora, você criará uma análise Data Lake e um repositório Data Lake conta em Olá mesmo tempo.  Esta etapa é simple e leva apenas sobre toofinish de 60 segundos.

1. Logon toohello [portal do Azure](https://portal.azure.com).
2. Clique em **Novo** >  **Data + Analytics** > **Data Lake Analytics**.
3. Selecione os valores para Olá itens a seguir:
   * **Nome**: Nome de sua conta do Data Lake Analytics (são permitidos somente letras minúsculas e números).
   * **Assinatura**: escolha Olá assinatura do Azure usada para Olá conta da análise.
   * **Grupo de Recursos**. Selecione um Grupo de Recursos do Azure existente ou crie um novo.
   * **Local**. Selecione um data center do Azure para a conta de análise Data Lake hello.
   * **Repositório data Lake**: siga as instruções de saudação toocreate uma nova conta do repositório Data Lake ou selecione um existente. 
4. Opcionalmente, selecione um tipo de preço para sua conta Data Lake Analytics.
5. Clique em **Criar**. 


## <a name="your-first-u-sql-script"></a>Seu primeiro script U-SQL

Olá texto a seguir é um script U-SQL muito simple. Tudo o que ele faz é definir um pequeno conjunto de dados no script hello e, em seguida, gravar o conjunto de dados fora do repositório Data Lake do toohello padrão como um arquivo chamado `/data.csv`.

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

## <a name="submit-a-u-sql-job"></a>Enviar um trabalho do U-SQL

1. Na conta da análise Data Lake do hello, clique em **novo trabalho**.
2. Colar texto de saudação do hello script U-SQL mostrado acima. 
3. Clique em **Enviar Trabalho**.   
4. Aguarde até que as alterações de status do trabalho Olá muito**êxito**.
5. Se a falha no trabalho de hello, consulte [monitorar e solucionar problemas de trabalhos da análise Data Lake](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).
6. Clique em Olá **saída** guia e, em seguida, clique em `data.csv`. 

## <a name="see-also"></a>Consulte também

* tooget iniciar o desenvolvimento de aplicativos de U-SQL, consulte [scripts de desenvolver U-SQL usando o Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* toolearn U-SQL, consulte [começar com a linguagem da análise Azure Data Lake U-SQL](data-lake-analytics-u-sql-get-started.md).
* Para obter as tarefas de gerenciamento, confira [Gerenciar o Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-manage-use-portal.md).
