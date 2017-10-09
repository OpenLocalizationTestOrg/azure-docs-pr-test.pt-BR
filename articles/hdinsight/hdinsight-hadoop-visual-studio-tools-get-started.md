---
title: aaaConnect tooAzure HDInsight usando Data Lake Tools para Visual Studio | Microsoft Docs
description: Saiba como tooinstall e usar ferramentas de Lake de dados para o Visual Studio tooconnect tooHadoop clusters de HDInsight do Azure e executadas consultas de Hive.
keywords: ferramentas do hadoop, consulta hive, visual studio, hadoop do visual studio
services: HDInsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: ce9c572a-1e98-46bf-9581-13a9767f1fa5
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/23/2017
ms.author: jgao
ms.openlocfilehash: ff5819a64bebe5f4ab3cf763ce6c45c81aa34b19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooazure-hdinsight-and-run-hive-queries-using-data-lake-tools-for-visual-studio"></a>Conecte-se tooAzure HDInsight e executar consultas do Hive usando Data Lake Tools para Visual Studio

Saiba como clusters de toouse Data Lake Tools para Visual Studio tooconnect tooHadoop [HDInsight do Azure](hdinsight-hadoop-introduction.md) e enviar consultas Hive. Para obter mais informações sobre como usar o HDInsight, consulte [Introdução tooHDInsight](hdinsight-hadoop-introduction.md) e [Introdução ao HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md). Para obter mais informações sobre o cluster de Storm tooa conexão, consulte [desenvolver c# topologias para Apache Storm no HDInsight usando o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Data Lake Tools para Visual Studio pode ser usado tooaccess análise Data Lake e HDInsight.  Para obter informações sobre o Data Lake Tools Olá, consulte [Tutorial: desenvolver scripts de U-SQL usando o Data Lake Tools para Visual Studio](../data-lake-analytics/data-lake-analytics-data-lake-tools-get-started.md).

**Pré-requisitos**

toocomplete este tutorial e use Olá Data Lake ferramentas no Visual Studio, você precisará seguir hello:

* Um cluster Azure HDInsight: um consulte toocreate [começar a usar o HDInsight baseados em Linux](hdinsight-hadoop-linux-tutorial-get-started.md)
* Uma estação de trabalho com hello software a seguir:
  
  * Windows 10, Windows 8.1, Windows 8, ou Windows 7.
  * Visual Studio 2013/2015/2017.
    
    > [!NOTE]
    > Atualmente, Olá Data Lake Tools para Visual Studio são fornecidos apenas com versão em inglês do hello.
    > 
    > 

## <a name="install-data-lake-tools-for-visual-studio"></a>Instalar Ferramentas do Data Lake para Visual Studio

As Ferramentas do Data Lake estão instaladas por padrão no Visual Studio 2017. Para versões mais antigas, você pode instalá-lo usando Olá [Web Platform Installer](https://www.microsoft.com/web/downloads/). Você deve escolher Olá que corresponde à sua versão do Visual Studio. Se você não tiver instalado o Visual Studio, você pode instalar Olá comunidade do Visual Studio e SDK do Azure mais recentes usando Olá [Web Platform Installer](https://www.microsoft.com/web/downloads/):

![Data Lake Tools para o instalador do Visual Studio Web Platform. ] (./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.wpi.png "Tooinstall de usar o Web Platform Installer Data Lake Tools para Visual Studio")

## <a name="connect-tooazure-subscriptions"></a>Conecte-se tooAzure assinaturas
Data Lake Tools para Visual Studio permite que você tooconnect clusters de HDInsight tooyour, executar algumas operações básicas de gerenciamento e executar consultas de Hive.

> [!NOTE]
> Para obter informações sobre o cluster de Hadoop genérico tooa conexão, consulte [escrever e enviar consultas Hive usando o Visual Studio](http://blogs.msdn.com/b/xiaoyong/archive/2015/05/04/how-to-write-and-submit-hive-queries-using-visual-studio.aspx).
> 
> 

**tooconnect tooyour assinatura do Azure**

1. Abra o Visual Studio.
2. De saudação **exibição** menu, clique em **Server Explorer** tooopen janela do Gerenciador de servidor de saudação.
3. Expanda **Azure** e expanda **HDInsight**.
   
   > [!NOTE]
   > Saudação de aviso **lista de tarefas do HDInsight** janela deve ser aberta. Se você não estiver visível, clique em **outras janelas** de saudação **exibição** menu e clique **janela de lista de tarefas do HDInsight**.  
   > 
   > 
4. Insira as credenciais de assinatura do Azure e clique em **Entrar**. Isso só é necessário se você nunca se conectou toohello assinatura do Azure do Visual Studio nesta estação de trabalho.
5. No Gerenciador de Servidores, você verá uma lista de clusters existentes do HDInsight. Se você não tiver qualquer clusters, você pode criar uma usando Olá portal do Azure, Azure PowerShell ou Olá HDInsight SDK. Para saber mais, veja [Criar clusters HDInsight](hdinsight-hadoop-provision-linux-clusters.md).
   
   ![Lista de clusters do Gerenciador de Servidores das Ferramentas do Data Lake para Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.server.explorer.png "Gerenciador de Servidores das Ferramentas do Data Lake para Visual Studio")
6. Expanda um cluster do HDInsight. Você verá **Bancos de Dados do Hive**, uma conta de armazenamento padrão, contas de armazenamento vinculadas e o **Log de Serviço do Hadoop**. Ainda mais, você pode expandir entidades hello.

Depois de conectado tooyour assinatura do Azure, você será capaz de toodo seguinte de saudação:

**tooconnect toohello portal do Azure do Visual Studio**

* No Gerenciador de Servidores, expanda **Azure** > **HDInsight**, clique com o botão direito do mouse em um cluster do HDInsight e clique em **Gerenciar Cluster no Portal do Azure**.

**tooask perguntas e fornecer comentários do Visual Studio**

* De saudação **ferramentas** menu, clique em **HDInsight**e, em seguida, clique em **Fórum do MSDN** tooask perguntas, ou clique em **fornecer Feedback**.

## <a name="navigate-hello-linked-resources"></a>Navegue Olá vinculado recursos
Do Gerenciador de servidores, você pode ver a conta de armazenamento saudação padrão e as contas de armazenamento vinculada. Se você expandir a conta de armazenamento padrão Olá, você pode ver contêineres Olá na conta de armazenamento hello. conta de armazenamento saudação padrão e o contêiner padrão de saudação estão marcadas. Você pode também clique qualquer conteúdo de Olá Olá contêineres tooview.

![Recursos vinculados à lista do gerenciador de servidores para Ferramentas do Data Lake para Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.linked.resources.png "recursos vinculados")

Depois de abrir um contêiner, você pode usar o hello tooupload botões, delete e blobs de download a seguir:

![Operações de blob do gerenciador de servidores das Ferramentas do Data Lake para Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.blob.operations.png "carregar, excluir e baixar blobs")

## <a name="run-a-hive-query"></a>Executar um trabalho do Hive
O [Apache Hive](http://hive.apache.org) é uma infraestrutura de data warehouse de dados criado com base no Hadoop para fornecer resumo de dados, consultas e análises. As ferramentas do Data Lake para o Visual Studio dão suporte às consultas Hive em execução do Visual Studio. Para obter mais informações sobre o Hive, consulte [Usar o Hive com o HDInsight](hdinsight-use-hive.md).

É demorado tootest script do Hive em um cluster HDInsight. Pode levar vários minutos ou mais. Data Lake Tools para Visual Studio é capaz de validar o script do Hive localmente sem cluster ao vivo de tooa conexão.

Data Lake Tools para Visual Studio também permite que os usuários toosee o que está dentro de trabalho de Hive Olá coletando e adicionar logs YARN Olá de determinados trabalhos Hive.

### <a name="view-hello-hivesampletable"></a>Saudação de exibição **hivesampletable**
Todos os clusters HDInsight são fornecidos com uma tabela Hive de exemplo chamada *hivesampletable*. Vamos usar essa tooshow tabela você como tabelas de Hive toolist, confira os esquemas de tabela hello e liste as linhas de saudação da Olá Hive tabela.

**tabelas de Hive toolist e exibição de esquema da tabela de Hive**

1. De **Server Explorer**, expanda **Azure** > **HDInsight** > cluster Olá de sua escolha > **bancos de dados de Hive**  >  **Padrão** > **hivesampletable** toosee esquema da tabela hello.
2. Clique com botão direito **hivesampletable**e, em seguida, clique em **exibição Top 100 linhas** linhas de saudação toolist. É equivalente toorunning Olá consulta de Hive, usando o driver ODBC da seção a seguir:
   
     SELECT * FROM hivesampletable LIMIT 100
   
   Você pode personalizar a contagem de linhas de saudação.
   
   ![Ferramentas do Data Lake: consulta de esquema do Hive do HDInsight para Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.hive.schema.png "Resultados da consulta Hive")

### <a name="create-hive-tables"></a>Criar tabelas Hive
Você pode usar o hello GUI toocreate uma tabela Hive ou usar consultas de Hive. Para obter informações sobre como usar consultas de Hive, consulte [Executar consultas Hive](#run.queries).

**toocreate uma tabela de Hive**

1. No **Gerenciador de Servidores**, expanda **Azure** > **Clusters HDInsight**, um cluster do HDInsight > **Bancos de dados Hive**, clique com o botão direito do mouse em **Padrão** e clique em **Criar Tabela**.
2. Configure a tabela de saudação.
3. Clique em **Create Table** toosubmit Olá trabalho toocreate Olá nova tabela Hive.
   
    ![Ferramentas do Data Lake: criar tabela hive das Ferramentas do HDInsight para Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.create.hive.table.png "Criar tabela Hive")

### <a name="run.queries"></a>Validar e executar consultas do Hive
Há duas maneiras toocreate e executadas consultas de Hive:

* Criar consultas locais
* Criar um aplicativo Hive

**toocreate, validar e executar consultas ad hoc**

1. No **Gerenciador de Servidores**, expanda **Azure** e expanda **Clusters HDInsight**.
2. Cluster de saudação com o botão direito em que deseja toorun Olá consulta e, em seguida, clique em **escrever uma consulta de Hive**.
3. Insira as consultas de Hive hello. Editor de Hive do aviso Olá dá suporte a IntelliSense. Data Lake Tools para Visual Studio dá suporte ao carregamento Olá metadados remota quando você estiver editando o script do Hive. Por exemplo, quando você digitar "SELECT * FROM", Olá IntelliSense listará todos os Olá nomes de tabela sugeridas. Quando for especificado um nome de tabela, nomes de coluna de saudação são listados por Olá IntelliSense. ferramentas de saudação oferece suporte a quase todas as instruções de DML Hive, subconsultas e Olá UDFs internos.
   
    ![Ferramentas Data Lake: Ferramentas do Visual Studio IntelliSense para HDInsight](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.table.names.png "U-SQL IntelliSense")
   
    ![Ferramentas Data Lake: Ferramentas do Visual Studio IntelliSense para HDInsight](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.intellisense.column.names.png "U-SQL IntelliSense")
   
   > [!NOTE]
   > Serão sugerido apenas Olá metadados de clusters Olá selecionado na barra de ferramentas do HDInsight.
   > 
   > 
4. (Opcional): clique em **Script validar** erros de sintaxe de script toocheck hello.
   
    ![Data Lake: Ferramentas do Data Lake para validação de local do Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.validate.hive.script.png "Validar script")
5. Clique em **Enviar** ou **Enviar (Avançado)**. Com hello Enviar opções avançadas, você vai configurar **nome do trabalho**, **argumentos**, **configurações adicionais**, e **Status diretório**para script hello:
   
    ![Consulta de hive do Hadoop do HDInsight](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.submit.jobs.advanced.png "Enviar consultas")
   
    Depois de enviar o trabalho de saudação, você verá um **resumo do trabalho de Hive** janela.
   
    ![Resumo de uma consulta de Hive do HDInsight Hadoop](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.run.hive.job.summary.png "Resumo de trabalho do Hive")
6. Saudação de uso **atualizar** botão status de saudação tooupdate até que as alterações de status do trabalho Olá muito**concluído**.
7. Clicar em links de saudação na seguinte de Olá Olá inferior toosee: **consulta de trabalho**, **saída de trabalho**, **log trabalho**, ou **log Yarn**.

**toocreate e executar uma solução de Hive**

1. De saudação **arquivo** menu, clique em **novo**e, em seguida, clique em **projeto**.
2. Selecione **HDInsight** no painel esquerdo do hello, selecione **aplicativo Hive** no painel do meio hello, insira as propriedades de saudação e, em seguida, clique em **Okey**.
   
    ![Ferramentas do Data Lake: novo projeto hive das Ferramentas do HDInsight para Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.new.hive.project.png "Criar aplicativos Hive do Visual Studio")
3. De **Solution Explorer**, clique duas vezes em **Script.hql** tooopen-lo.
4. script do Hive Olá toovalidate, você pode clicar em Olá **validar Script** botão, ou clique script hello no editor de Hive hello e, em seguida, clique em **Script validar** Olá no menu de contexto.

### <a name="view-hive-jobs"></a>Exibir trabalhos Hive
Você pode exibir consultas de trabalho, saída do trabalho, logs de trabalho e logs do Yarn para trabalhos do Hive. Para obter mais informações, consulte a captura de tela de saudação anterior.

a versão mais recente Olá das ferramentas de saudação permite que você toosee o que está dentro de seus trabalhos Hive coletando e adicionar YARN logs. Um log do YARN pode ajudar você investigar problemas de desempenho. Para obter mais informações sobre como o HDInsight coleta logs do YARN, veja [Acessar Logs de Aplicativo do HDInsight Programaticamente](hdinsight-hadoop-access-yarn-app-logs.md).

**trabalhos de Hive tooview**

1. No **Gerenciador de Servidores**, expanda**Azure** e expanda **HDInsight**.
2. Clique com o botão direito do mouse em um cluster HDInsight e em **Exibir Trabalhos**. Você verá uma lista de saudação Hive trabalhos executados no cluster hello.
3. Clique em um trabalho em Olá tooselect de lista de trabalho e, em seguida, use Olá **resumo do trabalho de Hive** janela tooopen **consulta de trabalho**, **saída de trabalho**, **Log trabalho**, ou **log Yarn**.
   
    ![Ferramentas do Data Lake: exibir projetos hive das ferramentas do HDInsight para o Visual Studio](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.view.hive.jobs.png "Exibir trabalhos do Hive")

### <a name="faster-path-hive-execution-via-hiveserver2"></a>Execução do Hive de caminho mais rápido via HiveServer2
> [!NOTE]
> Este tutorial funciona com o cluster HDInsight versão 3.2 e mais recentes.
> 
> 

Olá Data Lake Tools usado toosubmit Hive trabalhos por meio de [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (também conhecido como Templeton). Levou um tempo longo tooreturn detalhes do trabalho e informações de erro.
Em ordem toosolve esse problema de desempenho, Olá Data Lake Tools executa Hive trabalhos diretamente no cluster Olá por meio de HiveServer2, para que ela ignora RDP/SSH.
Desempenho de toobetter de adição, os usuários também podem ver Hive em gráficos Tez e Olá detalhes da tarefa.

Para o cluster HDInsight versão 3.2 ou posterior, você pode ver um botão **Executar via HiveServer2**:

![Ferramentas do Data Lake para Visual Studio, executar via hiveserver2](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.execute.via.hiveserver2.png "Executar consultas Hive usando o HiveServer2")

E você pode consulte Olá logs de streaming em tempo real e visualizar gráficos de trabalho de saudação se a consulta de Hive Olá é executada em Tez.

![Ferramentas do Data Lake para Visual Studio, execução por caminho rápido de fast](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.fast.path.hive.execution.png "Exibir gráficos do trabalho")

**Diferença entre executar consultas por meio do HiveServer2 e enviar consultas por meio do WebHCat**

Embora a execução de consultas por meio do HiveServer2 traga muitos benefícios de desempenho, ela tem várias limitações. Algumas das limitações de saudação não são adequadas para uso de produção. Olá tabela a seguir mostra as diferenças de saudação:

|  | Execução por meio do HiveServer2 | Envio  por meio do WebHCat |
| --- | --- | --- |
| Executar consultas |Elimina a sobrecarga de saudação em WebHCat (que inicia um MapReduce Job denominado "TempletonControllerJob"). |Desde que uma consulta seja executada por meio do WebHCat, o WebHCat iniciará um trabalho MapReduce que introduz latência adicional. |
| Transmitir os logs |Quase em tempo real. |Olá logs de execução de trabalho estão disponíveis somente quando Olá trabalho é concluído. |
| Exibir histórico de trabalho |Se uma consulta for executada por meio do HiveServer2, seu histórico de trabalho dela (log de trabalho, saída do trabalho) não será preservado. aplicativo Hello pode ser exibido na interface do usuário do YARN com informações limitadas. |Se uma consulta for executada por meio do WebHCat, o histórico de trabalho dela (log de trabalho, saída de trabalho) será preservado e poderá ser exibido usando o Visual Studio/SDK do HDInsight/PowerShell. |
| Fechar janela |Executar via HiveServer2 é uma forma de "síncrona", para que você deve manter Olá janelas são abertas; Se o windows hello são fechados, em seguida, a execução da consulta Olá será cancelada. |Enviando via WebHCat é uma forma de "assíncrona" para que possa enviar consulta Olá via WebHCat e feche o Visual Studio. Você pode voltar e ver os resultados de saudação a qualquer momento. |

### <a name="tez-hive-job-performance-graph"></a>Gráfico de desempenho do trabalho do Tez Hive
suporte de Data Lake Tools Olá mostrando os gráficos de desempenho para Olá trabalhos Hive executado pelo mecanismo de execução Tez hello. Para saber mais sobre como habilitar o Tez, consulte [Usar o Hive no HDInsight](hdinsight-use-hive.md). Depois de enviar uma ramificação de trabalho no Visual Studio, o Visual Studio mostra Olá gráfico quando Olá trabalho seja concluído.  Talvez seja necessário Olá tooclick **atualização** botão status do trabalho tooget hello mais recente.

> [!NOTE]
> Esse recurso só está disponível para o cluster HDInsight em versões posteriores a 3.2.4.593 e funciona somente para trabalhos concluídos (Se você enviar seu trabalho por meio do WebHCat. Esse gráfico mostra quando você executa a consulta por meio de HiveServer2). Isso funciona para clusters baseados em Windows e Linux.
> 
> 

![gráfico de desempenho do hive tez do hadoop](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.hive.tez.performance.graph.png "Status do trabalho")

toohelp você entender o Hive de consulta melhor, ferramentas de saudação adicionam exibição de operador Hive Olá nesta versão. Você precisa apenas toodouble, clique em vértices Olá Olá do gráfico de trabalho e você pode ver todos os operadores de saudação dentro Olá vértice. Você também pode passar em um operador específico tooview mais detalhes deste operador.

### <a name="task-execution-view-for-hive-on-tez-jobs"></a>Exibição de execução de tarefa para o Hive em trabalhos do Tez
Olá modo de execução de tarefa para Hive Tez trabalhos pode ser usado tooget estruturado e visualizar informações sobre trabalhos de Hive e obter mais detalhes do trabalho. Quando há problemas de desempenho, você pode usar o hello exibir tooget mais detalhes. Por exemplo, como cada tarefa opera e Olá informações detalhadas sobre cada tarefa (leitura/gravação de dados, agendamento/início/término, etc.), para que você pode ajustar as configurações de trabalho ou a arquitetura do sistema com base nas informações de saudação visualizada.

![Ferramentas do Data Lake para Visual Studio, exibir execução de tarefa](./media/hdinsight-hadoop-visual-studio-tools-get-started/hdinsight.visual.studio.tools.task.execution.view.png "Modo de exibição de tarefa")

## <a name="run-pig-scripts"></a>Executar scripts do Pig
Data Lake Tools para Visual Studio oferece suporte à criação e enviar clusters de tooHDInsight de scripts do Pig. Os usuários podem criar um projeto de Pig de modelo e envie clusters de tooHDInsight script hello.

## <a name="feedbacks--known-issues"></a>Comentários e problemas conhecidos
* Atualmente, os resultados do HiveServer2 são exibidos na forma de texto simples, o que não é ideal. Estamos trabalhando para corrigir isso.
* Se os resultados de saudação forem iniciados com valores nulos, atualmente Olá resultados não são mostrados. Podemos corrigir esse problema e se você está bloqueado para esse problema, sinta-se livre toodrop em um email ou entre em contato com a equipe de suporte.
* script HQL Olá criado pelo Visual Studio está codificado dependendo da configuração de região local do usuário. Ele pode não ser executada corretamente se o usuário carrega Olá script toocluster como binário.

## <a name="next-steps"></a>Próximas etapas
Neste artigo, você aprendeu como tooconnect tooHDInsight clusters do Visual Studio, Olá Data Lake (HDInsight) usando o pacote de ferramentas e como toorun uma consulta de Hive. Para obter mais informações, consulte:

* [Usar o Hive do Hadoop no HDInsight](hdinsight-use-hive.md)
* [Introdução ao uso do Hadoop no HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md)
* [Enviar trabalhos Hadoop no HDInsight](hdinsight-submit-hadoop-jobs-programmatically.md)
* [Analisar dados do Twitter com Hadoop no HDInsight](hdinsight-analyze-twitter-data.md)

