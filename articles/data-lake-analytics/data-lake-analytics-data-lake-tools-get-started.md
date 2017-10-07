---
title: scripts de aaaDevelop U-SQL usando o Data Lake Tools para Visual Studio | Microsoft Docs
description: Saiba como tooinstall Data Lake ferramentas para Visual Studio e os scripts de U-SQL toodevelop e teste.
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: jhubbard
editor: cgronlun
ms.assetid: ad8a6992-02c7-47d4-a108-62fc5a0777a3
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/28/2017
ms.author: saveenr, yanacai
ms.openlocfilehash: 7a0c02c275b8cefecbe784ba63969cbf24a150d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-u-sql-scripts-by-using-data-lake-tools-for-visual-studio"></a>Desenvolvimento de scripts U-SQL usando as ferramentas do Data Lake para Visual Studio
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]


Saiba como contas de análise do Azure Data Lake toocreate do Visual Studio toouse, definir trabalhos em [U-SQL](data-lake-analytics-u-sql-get-started.md)e envie-o serviço de análise Data Lake toohello trabalhos. Para saber mais sobre a Análise Data Lake, consulte a [Visão geral da Análise Data Lake do Azure](data-lake-analytics-overview.md).


## <a name="prerequisites"></a>Pré-requisitos

* **Visual Studio**: há suporte para todas as edições, exceto Express.
    * Visual Studio 2017
    * Visual Studio 2015
    * Visual Studio 2013
* **SDK do Microsoft Azure para .NET** versão 2.7.1 ou posterior.  Instalá-lo usando Olá [instalador de plataforma da Web](http://www.microsoft.com/web/downloads/platform.aspx).
* Uma conta do **Data Lake Analytics**. toocreate uma conta, consulte [Introdução à análise Azure Data Lake usando o portal do Azure](data-lake-analytics-get-started-portal.md).

## <a name="install-azure-data-lake-tools-for-visual-studio"></a>Instale as Ferramentas do Azure Data Lake para Visual Studio 

Baixe e instale o Azure Data Lake Tools para Visual Studio [do Centro de Download da saudação](http://aka.ms/adltoolsvs). Após a instalação, observe que:
* Olá **Server Explorer** > **Azure** nó contém um **análise Data Lake** nó. 
* Olá **ferramentas** menu tem uma **Data Lake** item.

## <a name="connect-tooan-azure-data-lake-analytics-account"></a>Conecte-se a conta de análise do Azure Data Lake tooan

1. Abra o Visual Studio.
2. Abra o Gerenciador de servidores selecionando a **Vista** do  > **Server Explorer**.
3. Clique o botão direito do mouse no **Azure**. Em seguida, selecione **conectar tooMicrosoft assinatura do Azure** e siga as instruções de saudação.
4. No Gerenciador de servidores, selecione **Azure** > **Data Lake Analytics**. Você verá uma lista das suas contas do Data Lake Analytics.


## <a name="write-your-first-u-sql-script"></a>Escreve seu primeiro script U-SQL

Olá texto a seguir é um script U-SQL simples. Ele define um conjunto de dados pequeno e gravações de repositório do conjunto de dados toohello padrão Data Lake como um arquivo chamado `/data.csv`.

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

### <a name="submit-a-data-lake-analytics-job"></a>Enviar um trabalho da Análise Data Lake

1. Selecione **Arquivo** > **Novo** > **Projeto**.

2. Selecione Olá **projeto U-SQL** digite e, em seguida, clique em **Okey**. O Visual Studio cria uma solução com um arquivo **Script.usql**.

3. Cole o script anterior Olá a saudação **Script.usql** janela.

4. No canto superior esquerdo Olá Olá **Script.usql** janela, especifique a conta da análise Data Lake de saudação.

    ![Enviar projeto de U-SQL do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job.png)

5. No canto superior esquerdo Olá Olá **Script.usql** janela, selecione **enviar**.
6. Verifique se Olá **conta da análise**e, em seguida, selecione **enviar**. Resultados de envio estão disponíveis em Olá Data Lake Tools para Visual Studio obter os resultados após a conclusão do envio de saudação.

    ![Enviar projeto de U-SQL do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-submit-job-advanced.png)
7. toosee hello mais recente trabalho status e a atualização de tela hello, clique em **atualizar**. Quando o trabalho de saudação for bem-sucedido, ele mostra Olá **trabalho gráfico**, **operações de metadados**, **histórico de estado**, e **diagnóstico**:

    ![Gráfico de desempenho de trabalho de Análise Data Lake do SQL-U do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-performance-graph.png)

   * **Resumo do trabalho** mostra Olá resumo do trabalho de saudação.   
   * **Detalhes do trabalho** mostra informações mais específicas sobre o trabalho de hello, incluindo o script hello, recursos e vértices.
   * **Gráfico de trabalho** visualiza o progresso de saudação do trabalho de saudação.
   * **Operações de metadados** mostra todas as ações de saudação efetuados no catálogo de saudação U-SQL.
   * **Dados** mostra todas as entradas de saudação e saídas.
   * **Diagnósticos** fornece uma análise avançada para otimização de desempenho e a execução do trabalho.

### <a name="toocheck-job-state"></a>estado do trabalho toocheck

1. No Gerenciador de servidores, selecione **Azure** > **Data Lake Analytics**. 
2. Expanda o nome da conta Olá análise Data Lake.
3. Clique duas vezes em **Trabalhos**.
4. Selecione o trabalho de saudação enviada anteriormente.

### <a name="toosee-hello-output-of-a-job"></a>saída de hello toosee de um trabalho

1. No Gerenciador de servidores, procure toohello trabalho enviado.
2. Clique em Olá **dados** guia.
3. Em Olá **saídas do trabalho** guia, selecione Olá `"/data.csv"` arquivo.

## <a name="next-steps"></a>Próximas etapas

* [Execute scripts U-SQL em sua estação de trabalho para teste e depuração](data-lake-analytics-data-lake-tools-local-run.md)
* [Depurar o código C# em trabalhos U-SQL](data-lake-analytics-debug-u-sql-jobs.md)
* [Use hello Azure Data Lake Tools para Visual Studio Code](data-lake-analytics-data-lake-tools-for-vscode.md)
