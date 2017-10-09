---
title: "logs de aaaAnalyze site usando a análise do Azure Data Lake | Microsoft Docs"
description: "Saiba como o site tooanalyze registra usando análise Data Lake. "
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 3a196735-d0d9-4deb-ba68-c4b3f3be8403
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: saveenr
ms.openlocfilehash: d27aaca95ed2b643cfed7a17b0066bf7fa4a1bf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-website-logs-using-azure-data-lake-analytics"></a>Analisar logs de site usando o Azure Data Lake Analytics
Saiba como tooanalyze site logs usando a análise Data Lake, especialmente em descobrir quais Referenciadores resultou em erros quando a tentativa de site de saudação toovisit.

## <a name="prerequisites"></a>Pré-requisitos
* **Visual Studio 2015 ou Visual Studio 2013**.
* **[Ferramentas do Data Lake para Visual Studio](http://aka.ms/adltoolsvs)**.

    Depois que o Data Lake Tools para Visual Studio está instalado, você verá um **Data Lake** item Olá **ferramentas** menu do Visual Studio:

    ![Menu U-SQL do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-menu.png)
* **Um conhecimento básico de análise Data Lake e hello Data Lake Tools para Visual Studio**. tooget iniciado, consulte:

  * [Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* **Uma conta da Análise Data Lake.**  Confira [Create an Azure Data Lake Analytics account](data-lake-analytics-get-started-portal.md) (Criar uma conta do Azure Data Lake Analytics).
* **Carregar a conta do hello exemplo dados toohello análise Data Lake.** Consulte [toocopy arquivos de dados de exemplo](data-lake-analytics-get-started-portal.md).

    toorun um trabalho de análise Data Lake, você precisará de alguns dados. Embora Olá Data Lake Tools oferece suporte ao carregamento de dados, você usará toomake de dados de exemplo do hello tooupload portal Olá este tutorial toofollow mais fácil.

## <a name="connect-tooazure"></a>Conecte-se tooAzure
Antes de compilar e testar qualquer script U-SQL, primeiro você deve conectar tooAzure.

**tooconnect tooData análise Lake**

1. Abra o Visual Studio.
2. Clique em **Data Lake > Opções e configurações**.
3. Clique em **entrar**, ou **Alterar usuário** se alguém tiver se conectado e siga as instruções de saudação.
4. Clique em **Okey** tooclose Olá opções e configurações de caixa de diálogo.

**toobrowse suas contas da análise Data Lake**

1. No Visual Studio, abra o **Gerenciador de Servidores** pressionando **CTRL+ALT+S**.
2. No **Gerenciador de Servidores**, expanda **Azure** e **Data Lake Analytics**. Você deverá ver uma lista das suas contas da Análise Data Lake, caso haja alguma. Você não pode criar contas de análise Data Lake studio hello. toocreate uma conta, consulte [Introdução à análise Azure Data Lake usando o Portal do Azure](data-lake-analytics-get-started-portal.md) ou [começar a usar o Azure PowerShell de análise do Azure Data Lake](data-lake-analytics-get-started-powershell.md).

## <a name="develop-u-sql-application"></a>Desenvolver aplicativos U-SQL
Um aplicativo U-SQL é basicamente um script U-SQL. toolearn mais sobre U-SQL, consulte [começar com U-SQL](data-lake-analytics-u-sql-get-started.md).

Você pode adicionar o aplicativo de toohello adição operadores definidos pelo usuário.  Para obter mais informações, veja [Desenvolver operadores U-SQL definidos pelo usuário para trabalhos da Análise do Data Lake](data-lake-analytics-u-sql-develop-user-defined-operators.md).

**toocreate e enviar um trabalho de análise Data Lake**

1. Clique em Olá **arquivo > Novo > projeto**.
2. Selecione o tipo de projeto de U-SQL de saudação.

    ![novo projeto de U-SQL do Visual Studio](./media/data-lake-analytics-data-lake-tools-get-started/data-lake-analytics-data-lake-tools-new-project.png)
3. Clique em **OK**. O Visual Studio cria uma solução com um arquivo Script.usql.
4. Digite hello script a seguir no arquivo de Script.usql hello:

        // Create a database for easy reuse, so you don't need tooread from a file every time.
        CREATE DATABASE IF NOT EXISTS SampleDBTutorials;

        // Create a Table valued function. TVF ensures that your jobs fetch data from hello weblog file with hello correct schema.
        DROP FUNCTION IF EXISTS SampleDBTutorials.dbo.WeblogsView;
        CREATE FUNCTION SampleDBTutorials.dbo.WeblogsView()
        RETURNS @result TABLE
        (
            s_date DateTime,
            s_time string,
            s_sitename string,
            cs_method string,
            cs_uristem string,
            cs_uriquery string,
            s_port int,
            cs_username string,
            c_ip string,
            cs_useragent string,
            cs_cookie string,
            cs_referer string,
            cs_host string,
            sc_status int,
            sc_substatus int,
            sc_win32status int,
            sc_bytes int,
            cs_bytes int,
            s_timetaken int
        )
        AS
        BEGIN

            @result = EXTRACT
                s_date DateTime,
                s_time string,
                s_sitename string,
                cs_method string,
                cs_uristem string,
                cs_uriquery string,
                s_port int,
                cs_username string,
                c_ip string,
                cs_useragent string,
                cs_cookie string,
                cs_referer string,
                cs_host string,
                sc_status int,
                sc_substatus int,
                sc_win32status int,
                sc_bytes int,
                cs_bytes int,
                s_timetaken int
            FROM @"/Samples/Data/WebLog.log"
            USING Extractors.Text(delimiter:' ');
            RETURN;
        END;

        // Create a table for storing referrers and status
        DROP TABLE IF EXISTS SampleDBTutorials.dbo.ReferrersPerDay;
        @weblog = SampleDBTutorials.dbo.WeblogsView();
        CREATE TABLE SampleDBTutorials.dbo.ReferrersPerDay
        (
            INDEX idx1
            CLUSTERED(Year ASC)
            DISTRIBUTED BY HASH(Year)
        ) AS

        SELECT s_date.Year AS Year,
            s_date.Month AS Month,
            s_date.Day AS Day,
            cs_referer,
            sc_status,
            COUNT(DISTINCT c_ip) AS cnt
        FROM @weblog
        GROUP BY s_date,
                cs_referer,
                sc_status;

    Olá toounderstand U-SQL, consulte [Introdução à linguagem Data Lake análise U-SQL](data-lake-analytics-u-sql-get-started.md).    
5. Adicionar um novo projeto de tooyour de script U-SQL e digite Olá seguinte:

        // Query hello referrers that ran into errors
        @content =
            SELECT *
            FROM SampleDBTutorials.dbo.ReferrersPerDay
            WHERE sc_status >=400 AND sc_status < 500;

        OUTPUT @content
        too@"/Samples/Outputs/UnsuccessfulResponses.log"
        USING Outputters.Tsv();
6. Alternar o script U-SQL da primeira toohello voltar e Avançar toohello **enviar** botão, especifique a conta da análise.
7. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Script.usql** e, então, clique em **Compilar Script**. Verificar os resultados de saudação no painel de saída de hello.
8. No **Gerenciador de Soluções**, clique com o botão direito do mouse em **Script.usql** e, então, clique em **Enviar Script**.
9. Verifique se Olá **conta da análise** é hello onde deseja toorun Olá trabalho e, em seguida, clique em **enviar**. Resultados de envio e o link de trabalho estão disponíveis em hello Data Lake Tools para a janela de resultados do Visual Studio quando o envio de saudação é concluído.
10. Aguarde até que o trabalho de saudação é concluído com êxito.  Se o trabalho de saudação falhou, o arquivo de origem Olá provavelmente está ausente.  Consulte a seção pré-requisitos Olá deste tutorial. Para obter mais informações sobre solução de problemas, veja [Monitorar e solucionar problemas com trabalhos da Análise do Azure Data Lake](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md).

    Quando o trabalho de saudação for concluído, você deverá ver Olá tela a seguir:

    ![a Análise Data Lake analisa logs de site de blogs](./media/data-lake-analytics-analyze-weblogs/data-lake-analytics-analyze-weblogs-job-completed.png)
11. Agora, repita as etapas 7 a 10 para **Script1.usql**.

**saída de trabalho hello toosee**

1. De **Server Explorer**, expanda **Azure**, expanda **análise Data Lake**, expanda sua conta da análise Data Lake, expanda **ascontasdearmazenamento**, clique em conta de armazenamento do Data Lake saudação padrão e, em seguida, clique em **Explorer**.
2. Clique duas vezes em **exemplos** tooopen Olá pasta e, em seguida, clique duas vezes em **saídas**.
3. Clique duas vezes em **UnsuccessfulResponsees.log**.
4. Você pode também clique duas vezes em arquivo de saída de hello dentro do modo de exibição de gráfico de saudação do trabalho de saudação em ordem toonavigate diretamente toohello de saída.

## <a name="see-also"></a>Consulte também
tooget iniciado com análise Data Lake usando ferramentas diferentes, consulte:

* [Introdução à Análise do Data Lake usando o Portal do Azure](data-lake-analytics-get-started-portal.md)
* [Introdução à Análise Data Lake usando o Azure PowerShell](data-lake-analytics-get-started-powershell.md)
* [Introdução à Análise Data Lake usando o SDK do .NET](data-lake-analytics-get-started-net-sdk.md)
