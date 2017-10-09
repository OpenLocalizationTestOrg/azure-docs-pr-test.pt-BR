---
title: "ferramentas de aaaData Lake para Visual Studio com a área restrita do Hortonworks - HDInsight do Azure | Microsoft Docs"
description: "Saiba como toouse Olá ferramentas do Azure Data Lake para Visual Studio com a área restrita de Hortonworks Olá executados em uma VM local. Com essas ferramentas, você pode criar e executar trabalhos de Hive e Pig em área restrita Olá e exibir saída de trabalho e o histórico."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e3434c45-95d1-4b96-ad4c-fb59870e2ff0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/11/2017
ms.author: larryfr
ms.openlocfilehash: 7a3406b28d87d953e9b5be387faa86268f47b935
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-azure-data-lake-tools-for-visual-studio-with-hello-hortonworks-sandbox"></a>Usar ferramentas do Azure Data Lake Olá para o Visual Studio com Olá Hortonworks Sandbox

O Azure Data Lake inclui ferramentas para trabalhar com clusters Hadoop genéricos. Este documento fornece as etapas de saudação necessárias ferramentas de Data Lake toouse Olá com hello Hortonworks Sandbox em execução em uma máquina virtual local.

Olá Hortonworks Sandbox permite que você toowork com Hadoop localmente no seu ambiente de desenvolvimento. Depois de desenvolver uma solução e deseja toodeploy-la em grande escala, em seguida, você pode mover o cluster do HDInsight tooan.

## <a name="prerequisites"></a>Pré-requisitos

* Olá Hortonworks área restrita, em execução em uma máquina virtual em seu ambiente de desenvolvimento. Este documento foi gravado e testado com a área restrita de saudação executando em Oracle VirtualBox. Para obter informações sobre a configuração de proteção hello, consulte Olá [começar com a área restrita do hello Hortonworks.](hdinsight-hadoop-emulator-get-started.md) .

* Visual Studio 2013, Visual Studio 2015 ou Visual Studio 2017 (qualquer edição).

* Olá [SDK do Azure para .NET](https://azure.microsoft.com/downloads/) 2.7.1 ou posterior.

* Olá [Azure Data Lake ferramentas para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="configure-passwords-for-hello-sandbox"></a>Configurar senhas para a área restrita de saudação

Certifique-se de que Olá que hortonworks Sandbox está em execução. Siga as etapas de Olá Olá [começar a saudação Hortonworks Sandbox](hdinsight-hadoop-emulator-get-started.md#set-sandbox-passwords) documento. Essas etapas configuram senha Olá Olá SSH `root` conta e Olá Ambari `admin` conta. Essas senhas são usadas quando você se conectar toohello sandbox do Visual Studio.

## <a name="connect-hello-tools-toohello-sandbox"></a>Conecte-se a área restrita do hello ferramentas toohello

1. Abra o Visual Studio e selecione **Exibir**, **Gerenciador de Servidores**.

2. De **Server Explorer**, Olá do botão direito do mouse **HDInsight** entrada e, em seguida, selecione **conectar tooHDInsight emulador**.

    ![Captura de tela do Gerenciador de servidores, com tooHDInsight conectar emulador realçado](./media/hdinsight-hadoop-emulator-visual-studio/connect-emulator.png)

3. De saudação **conectar tooHDInsight emulador** caixa de diálogo, digite a senha de saudação que você configurou para Ambari.

    ![Captura de tela da caixa de diálogo, com a caixa de texto de senha realçada](./media/hdinsight-hadoop-emulator-visual-studio/enter-ambari-password.png)

    Selecione **próximo** toocontinue.

4. Saudação de uso **senha** senha de saudação do campo tooenter configurados para hello `root` conta. Deixe Olá outros campos com valor de padrão de saudação.

    ![Captura de tela da caixa de diálogo, com a caixa de texto de senha realçada](./media/hdinsight-hadoop-emulator-visual-studio/enter-root-password.png)

    Selecione **próximo** toocontinue.

5. Espera para validação de saudação toofinish de serviços. Em alguns casos, a validação pode falhar e solicitará que você tooupdate configuração de saudação. Se a validação falhar, selecione **atualização**e aguarde a configuração hello e verificação de saudação toofinish de serviço.

    ![Captura de tela da caixa de diálogo, com o botão Atualizar realçado](./media/hdinsight-hadoop-emulator-visual-studio/fail-and-update.png)

    > [!NOTE]
    > o processo de atualização Olá usa Ambari toomodify Olá Hortonworks Sandbox configuração toowhat esperada por ferramentas de Data Lake Olá para o Visual Studio.

6. Depois que a validação foi concluída, selecione **concluir** toocomplete configuração.
    ![Captura de tela da caixa de diálogo, com o botão Concluir realçado](./media/hdinsight-hadoop-emulator-visual-studio/finished-connect.png)

     >[!NOTE]
     > Dependendo da velocidade da saudação do seu ambiente de desenvolvimento e Olá quantidade de memória alocada a máquina virtual de toohello, tirar tooconfigure de vários minutos e validar serviços hello.

Depois de seguir essas etapas, você agora tem um **cluster local do HDInsight** entrada no Gerenciador de servidores, sob Olá **HDInsight** seção.

## <a name="write-a-hive-query"></a>Escrever uma consulta do Hive

O Hive fornece uma linguagem de consulta do tipo SQL (HiveQL) para trabalhar com os dados estruturados. As etapas a seguir de saudação do uso toolearn como toorun sob demanda consultas no cluster local hello.

1. Em **Server Explorer**, entrada Olá para o cluster local de saudação que você adicionou anteriormente e, em seguida, selecione **escrever uma consulta de Hive**.

    ![Captura de tela do Gerenciador de Servidores, com a opção Escrever uma Consulta do Hive realçada](./media/hdinsight-hadoop-emulator-visual-studio/write-hive-query.png)

    Uma nova janela de consulta é exibida. Aqui, você pode rapidamente escrever e enviar um cluster local do toohello de consulta.

2. Na nova janela de consulta hello, digite Olá comando a seguir:

        select count(*) from sample_08;

    consulta de saudação toorun, selecione **enviar** na parte superior de saudação da janela de saudação. Deixe os outros valores hello (**lote** e o nome do servidor) com valores padrão de saudação.

    ![Captura de tela da janela de consulta, com o botão de envio Olá realçado](./media/hdinsight-hadoop-emulator-visual-studio/submit-hive.png)

    Você também pode usar menu suspenso de saudação Avançar muito**enviar** tooselect **avançado**. Opções avançadas permitem opções adicionais de tooprovide ao enviar trabalho hello.

    ![Captura de tela da caixa de diálogo Enviar Script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-hive.png)

3. Depois que você enviar consulta hello, status do trabalho Olá é exibida. status do trabalho Olá exibe informações sobre o trabalho Olá conforme ela é processada pelo Hadoop. **Estado do trabalho** fornece o status de saudação do trabalho de saudação. estado de saudação é atualizado periodicamente, ou você pode usar o hello atualizar ícone toorefresh Olá estado manualmente.

    ![Captura de tela da caixa de diálogo Exibir Trabalho, com o Estado do Trabalho realçado](./media/hdinsight-hadoop-emulator-visual-studio/job-state.png)

    Depois de saudação **estado do trabalho** muda muito**concluído**, um direcionado acíclico Graph (DAG) é exibido. Este diagrama descreve o caminho de execução de saudação foi determinado por Tez durante o processamento de consulta de Hive hello. Tez é o mecanismo de execução de padrão Olá para o Hive no cluster local hello.

    > [!NOTE]
    > Tez também é o padrão de hello quando você estiver usando clusters HDInsight baseados em Linux. Não é padrão Olá no HDInsight baseados no Windows. toouse-lo, você deve adicionar a linha hello `set hive.execution.engine = tez;` toohello a partir de sua consulta de Hive.

    Saudação de uso **saída de trabalho** vincular a saída de hello tooview. Nesse caso, é 823, número de saudação de linhas na tabela de sample_08 hello. Você pode exibir informações de diagnóstico sobre o trabalho de saudação usando Olá **Log trabalho** e **baixar YARN Log** links.

4. Você também pode executar trabalhos de Hive interativamente alterando Olá **lote** campo muito**interativo**. Em seguida, selecione **Executar**.

    ![Captura de tela dos botões Interativo e Executar realçados](./media/hdinsight-hadoop-emulator-visual-studio/interactive-query.png)

    Uma consulta interativa fluxos Olá log de saída gerado durante o processamento toohello **HiveServer2 saída** janela.

    > [!NOTE]
    > Hello informações é Olá mesmo que está disponível no hello **Log trabalho** link depois que um trabalho foi concluído.

    ![Captura de tela do log de saída](./media/hdinsight-hadoop-emulator-visual-studio/hiveserver2-output.png)

## <a name="create-a-hive-project"></a>Criar um projeto do Hive

Você também pode criar um projeto que contém vários scripts do Hive. Use um projeto quando você tiver scripts relacionados ou toostore scripts em um sistema de controle de versão.

1. No Visual Studio, selecione **Arquivo**, **Novo** e **Projeto**.

2. Na lista de saudação de projetos, expanda **modelos**, expanda **Azure Data Lake**e, em seguida, selecione **HIVE (HDInsight)**. Saudação de modelos, selecione lista **Hive exemplo**. Insira um nome e um local e selecione **OK**.

    ![Captura de tela da janela Novo Projeto com Azure Data Lake, HIVE, Amostra do Hive e OK realçados](./media/hdinsight-hadoop-emulator-visual-studio/new-hive-project.png)

Olá **exemplo Hive** projeto contém dois scripts, **WebLogAnalysis.hql** e **SensorDataAnalysis.hql**. Você pode enviar esses scripts usando Olá mesmo **enviar** botão na parte superior de saudação da janela de saudação.

## <a name="create-a-pig-project"></a>Criar um projeto Pig

Enquanto o Hive fornece uma linguagem semelhante ao SQL para trabalhar com os dados estruturados, o Pig funciona executando transformações nos dados. Pig fornece uma linguagem (Pig latino) que permite a você toodevelop um pipeline de transformações. toouse Pig com o cluster local do hello, siga estas etapas:

1. Abra o Visual Studio, selecione **Arquivo**, **Novo** e **Projeto**. Na lista de saudação de projetos, expanda **modelos**, expanda **Azure Data Lake**e, em seguida, selecione **Pig (HDInsight)**. Saudação de modelos, selecione lista **Pig aplicativo**. Insira um nome e local e selecione **OK**.

    ![Captura de tela da janela Novo Projeto com Azure Data Lake, Pig, Aplicativo Pig e OK realçados](./media/hdinsight-hadoop-emulator-visual-studio/new-pig.png)

2. Digite hello depois do texto como conteúdo de saudação do hello **script.pig** arquivo que foi criado com este projeto.

        a = LOAD '/demo/data/Website/Website-Logs' AS (
            log_id:int,
            ip_address:chararray,
            date:chararray,
            time:chararray,
            landing_page:chararray,
            source:chararray);
        b = FILTER a BY (log_id > 100);
        c = GROUP b BY ip_address;
        DUMP c;

    Enquanto Pig usa uma linguagem diferente de Hive, como executar trabalhos de saudação é consistente entre os dois idiomas, por meio de saudação **enviar** botão. Olá selecionando lista suspensa ao lado de **enviar** exibe uma caixa de diálogo de envio avançados de Pig.

    ![Captura de tela da caixa de diálogo Enviar Script](./media/hdinsight-hadoop-emulator-visual-studio/advanced-pig.png)

3. Olá status do trabalho e de saída também é exibida, Olá mesmo como uma consulta de Hive.

    ![Captura de tela de um trabalho de Pig concluído](./media/hdinsight-hadoop-emulator-visual-studio/completed-pig.png)

## <a name="view-jobs"></a>Exibir trabalhos

Data Lake ferramentas também permitem que você tooeasily exibir informações sobre os trabalhos que foram executados no Hadoop. Use Olá etapas toosee Olá os trabalhos que foram executados no cluster local Olá a seguir.

1. De **Server Explorer**, cluster local hello e, em seguida, selecione **Exibir trabalhos**. Uma lista de trabalhos que foram enviados toohello cluster é exibida.

    ![Captura de tela do Gerenciador de Servidores, com a opção Exibir Trabalhos realçada](./media/hdinsight-hadoop-emulator-visual-studio/view-jobs.png)

2. Na lista de saudação de trabalhos, selecione um detalhes do trabalho Olá tooview.

    ![Captura de tela de trabalho de navegador, com um dos trabalhos de saudação realçados](./media/hdinsight-hadoop-emulator-visual-studio/view-job-details.png)

    informações de saudação exibidas são semelhante toowhat que consulte após executar uma consulta de Hive ou Pig, incluindo links tooview Olá saída e informações de log.

3. Você também pode modificar e envie novamente o trabalho de saudação aqui.

## <a name="view-hive-databases"></a>Exibir bancos de dados do Hive

1. Em **Server Explorer**, expanda Olá **cluster local do HDInsight** entrada e, em seguida, expanda **bancos de dados de Hive**. Olá **padrão** e **xademo** bancos de dados no cluster local Olá são exibidos. Expandir um banco de dados mostra tabelas Olá no banco de dados de saudação.

    ![Captura de tela do Gerenciador de Servidores, com os bancos de dados realçados](./media/hdinsight-hadoop-emulator-visual-studio/expanded-databases.png)

2. Expandindo uma tabela exibe colunas Olá para aquela tabela. dados de saudação do modo de exibição tooquickly, uma tabela e selecione **exibição Top 100 linhas**.

    ![Captura de tela do Gerenciador de Servidores, com a tabela expandida e a opção Exibir as 100 Primeiras Linhas selecionada](./media/hdinsight-hadoop-emulator-visual-studio/view-100.png)

### <a name="database-and-table-properties"></a>Propriedades do banco de dados e da tabela

Você pode exibir as propriedades de saudação de um banco de dados ou tabela. Selecionando **propriedades** exibe detalhes de item de saudação selecionada na janela de propriedades de saudação. Por exemplo, consulte informações Olá Olá captura de tela a seguir mostradas:

![Captura de tela da janela Propriedades](./media/hdinsight-hadoop-emulator-visual-studio/properties.png)

### <a name="create-a-table"></a>Criar uma tabela

toocreate uma tabela, um banco de dados e, em seguida, selecione **Create Table**.

![Captura de tela do Gerenciador de Servidores, com a opção Criar Tabela realçada](./media/hdinsight-hadoop-emulator-visual-studio/create-table.png)

Você pode criar tabela hello usando um formulário. Na parte inferior de saudação do hello captura de tela a seguir, você pode ver Olá HiveQL bruto que é usado toocreate Olá tabela.

![Captura de tela de formulário Olá usado toocreate uma tabela](./media/hdinsight-hadoop-emulator-visual-studio/create-table-form.png)

## <a name="next-steps"></a>Próximas etapas

* [Aprendizado ropes de saudação do hello Hortonworks seguro](http://hortonworks.com/hadoop-tutorial/learning-the-ropes-of-the-hortonworks-sandbox/)
* [Hadoop tutorial - Getting started with HDP](http://hortonworks.com/hadoop-tutorial/hello-world-an-introduction-to-hadoop-hcatalog-hive-and-pig/)
