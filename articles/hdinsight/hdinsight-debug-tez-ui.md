---
title: aaaUse Tez UI com HDInsight baseados em Windows - Azure | Microsoft Docs
description: "Saiba como Olá toouse Tez UI toodebug Tez trabalhos no HDInsight de HDInsight baseados no Windows."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a55bccb9-7c32-4ff2-b654-213a2354bd5c
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 7ae21242ee1f8dc34a8501bed1ca995480885540
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-tez-ui-toodebug-tez-jobs-on-windows-based-hdinsight"></a>Use Olá Tez UI toodebug Tez trabalhos no HDInsight baseados no Windows
Olá Tez UI é uma página da web que pode ser usado toounderstand e depurar os trabalhos que usam Tez como mecanismo de execução de saudação em clusters HDInsight baseados no Windows. Olá Tez UI permite toovisualize trabalho de saudação como um gráfico de itens conectados, detalhar cada item e recuperar estatísticas e informações de registro em log.

> [!IMPORTANT]
> etapas de saudação neste documento exigem um cluster HDInsight que usa o Windows. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Pré-requisitos
* Um cluster HDInsight baseado no Windows. Para obter as etapas de criação de um novo cluster, confira [Introdução ao uso do HDInsight baseado no Windows](hdinsight-hadoop-tutorial-get-started-windows.md).

  > [!IMPORTANT]
  > Olá Tez UI só está disponível em clusters HDInsight baseados no Windows criados após 8 de fevereiro de 2016.
  >
  >
* Um cliente da Área de Trabalho Remota baseado no Windows.

## <a name="understanding-tez"></a>Noções básicas sobre o Tez
Tez é uma estrutura extensível para processamento de dados no Hadoop que fornece maior velocidade de processamento do que o MapReduce tradicional. Para clusters HDInsight baseados no Windows, é um mecanismo opcional que você pode habilitar para o Hive usando o comando a seguir como parte de sua consulta de Hive de saudação:

    set hive.execution.engine=tez;

Quando o trabalho é enviado tooTez, ele cria um direcionado acíclico Graph (DAG) que descreve a ordem de saudação de execução das ações de saudação exigidos pelo trabalho de saudação. Ações individuais são chamadas de vértices e executar um pedaço de saudação trabalho geral. a execução real Olá Olá trabalho descrita por um vértice é chamada de uma tarefa e pode ser distribuída em vários nós no cluster de saudação.

### <a name="understanding-hello-tez-ui"></a>Saudação de compreensão Tez UI
Olá Tez UI é que uma página da web fornece informações sobre os processos que estão em execução, ou tenha executaram anteriormente usando Tez. Ele permite tooview Olá DAG gerado pelo Tez, como ele é distribuído entre clusters, os contadores como a memória usada por tarefas e vértices e informações de erro. Ele pode oferecer informações úteis no hello os seguintes cenários:

* Monitorando processos de longa execução, exibindo Olá progresso de mapa e reduzir as tarefas.
* Analisar dados históricos para toolearn processos com êxito ou falha, como o processamento pode ser aprimorado ou razão da falha.

## <a name="generate-a-dag"></a>Gerar um DAG
Olá Tez UI conterá apenas dados se um trabalho que usa Olá Tez mecanismo está em execução ou tem foi executado no hello anterior. Normalmente, as consultas simples do Hive podem ser resolvidas sem usar o Tez. Porém, as consultas mais complexas que realizam filtragem, agrupamento, ordenação, associações etc. normalmente exigirão o Tez.

Use Olá etapas toorun uma consulta de Hive que será executado usando Tez a seguir.

1. Em um navegador da web, navegar toohttps://CLUSTERNAME.azurehdinsight.net, onde **CLUSTERNAME** é o nome de saudação do cluster HDInsight.
2. No menu de saudação na parte superior de saudação da página hello, selecione Olá **Editor Hive**. Isso exibirá uma página com hello consulta de exemplo a seguir.

        Select * from hivesampletable

    Apagar a consulta de exemplo hello e substitua-o pelo seguinte hello.

        set hive.execution.engine=tez;
        select market, state, country from hivesampletable where deviceplatform='Android' group by market, country, state;
3. Selecione Olá **enviar** botão. Olá **sessão de trabalho** seção final Olá Olá página exibirá o status de saudação de consulta de saudação. Uma vez Olá alterações de status muito**concluído**, selecione Olá **exibir detalhes** link tooview resultados de saudação. Olá **saída de trabalho** deve ser a seguir toohello semelhante:

        en-GB   Hessen      Germany
        en-GB   Kingston    Jamaica
        en-GB   Nairobi Area    Kenya

## <a name="use-hello-tez-ui"></a>Use Olá Tez UI
> [!NOTE]
> Olá Tez UI só está disponível na área de trabalho Olá Olá principal de nós de cluster, você deve usar nós de cabeçalho de toohello de tooconnect de área de trabalho remota.
>
>

1. De saudação [portal do Azure](https://portal.azure.com), selecione o cluster HDInsight. Da parte superior de saudação da folha de HDInsight hello, selecione Olá **área de trabalho remota** ícone. Isso exibirá a folha de área de trabalho remota Olá

    ![Ícone da área de trabalho remota](./media/hdinsight-debug-tez-ui/remotedesktopicon.png)
2. Na folha de área de trabalho remota hello, selecione **conectar** nó principal do cluster tooconnect toohello. Quando solicitado, use Olá cluster área de trabalho remota usuário nome e senha tooauthenticate Olá conexão.

    ![Ícone de conexão da área de trabalho remota](./media/hdinsight-debug-tez-ui/remotedesktopconnect.png)

   > [!NOTE]
   > Se você não tiver habilitado a conectividade de área de trabalho remota, forneça um nome de usuário, senha e data de validade, e selecione **habilitar** tooenable área de trabalho remota. Depois que ele tiver sido habilitado, use Olá tooconnect de etapas anteriores.
   >
   >
3. Uma vez conectado, abra o Internet Explorer na área de trabalho de remota do hello, ícone de engrenagem Olá select no superior Olá direita do navegador Olá e, em seguida, selecione **configurações de exibição de compatibilidade**.
4. Na parte inferior de saudação do **configurações de exibição de compatibilidade**, desmarque Olá a caixa de seleção para **exibir sites da intranet na exibição de compatibilidade** e **listas de compatibilidade de usar o Microsoft**, e, em seguida, selecione **fechar**.
5. No Internet Explorer, navegue toohttp://headnodehost:8188/tezui / #/. Isso exibirá Olá Tez UI

    ![Interface de usuário do Tez](./media/hdinsight-debug-tez-ui/tezui.png)

    Quando carregado Olá Tez UI, você verá uma lista de DAGs que estão sendo executados, ou ter sido executado no cluster hello. exibição padrão de saudação inclui Olá Dag Name, Id, emissor, Status, hora de início, hora de término, duração, ID do aplicativo e fila. Mais colunas podem ser adicionadas usando o ícone de engrenagem Olá na saudação à direita da página de saudação.

    Se você tiver apenas uma entrada, ele será usado para consulta Olá que você executou na seção anterior Olá. Se você tiver várias entradas, você pode pesquisar inserindo critérios de pesquisa nos campos de saudação acima Olá DAGs e ocorrências **Enter**.
6. Selecione Olá **Dag Name** para a entrada mais recente DAG hello. Isso exibirá informações sobre Olá DAG, bem como toodownload de opção Olá um zip dos arquivos JSON que contêm informações sobre Olá DAG.

    ![Detalhes do DAG](./media/hdinsight-debug-tez-ui/dagdetails.png)
7. Acima Olá **DAG detalhes** são vários links que podem ser usados toodisplay informações sobre Olá DAG.

   * **Contadores de DAG** exibe informações de contadores do DAG em questão.
   * **Modo de Exibição Gráfico** exibe uma representação gráfica deste DAG.
   * **Todos os vértices** exibe uma lista dos vértices de saudação neste DAG.
   * **Todas as tarefas** exibe uma lista de tarefas Olá para todos os vértices neste DAG.
   * **Todos os TaskAttempts** exibe informações sobre Olá tentativas toorun tarefas para esta DAG.

     > [!NOTE]
     > Se você rolar a exibição da coluna Olá vértices, tarefas e TaskAttempts, observe que há links tooview **contadores** e **exibir ou baixar os logs** para cada linha.
     >
     >

     Se houver uma falha com o trabalho Olá, Olá DAG detalhes exibirá um status de falha, junto com links tooinformation sobre Olá tarefa que falhou. Informações de diagnóstico serão exibidas abaixo detalhes Olá DAG.
8. Escolha **Modo de Exibição Gráfico**. Isso exibe uma representação gráfica da saudação DAG. Você pode colocar o mouse Olá sobre cada vértice no hello exibir toodisplay informações sobre ele.

    ![Modo de Exibição Gráfico](./media/hdinsight-debug-tez-ui/dagdiagram.png)
9. Clicar em um vértice carregará Olá **detalhes de vértice** para aquele item. Clique em Olá **mapa 1** detalhes de toodisplay de vértice para este item. Selecione **confirmar** tooconfirm navegação de saudação.

    ![Detalhes do Vértice](./media/hdinsight-debug-tez-ui/vertexdetails.png)
10. Observe que agora tem links na parte superior de saudação da página de saudação que são as tarefas e toovertices relacionados.

    > [!NOTE]
    > Você também pode chegar a essa página voltando muito**DAG detalhes**, selecionando **detalhes de vértice**e, em seguida, selecionando Olá **mapa 1** vértice.
    >
    >

    * **Contadores de Vértice** exibe informações de contadores do vértice em questão.
    * **Tarefas** exibe tarefas do vértice em questão.
    * **Tentativas de tarefas** exibe informações sobre tentativas toorun tarefas para esta vértice.
    * **Fontes e Coletores** exibe fontes de dados e coletores do vértice em questão.

      > [!NOTE]
      > Como com menu anterior do hello, você pode rolar a exibição da coluna Olá para tarefas, tentativas de tarefa e fontes & Sinks__ toodisplay vincula toomore informações para cada item.
      >
      >
11. Selecione **tarefas**, e, em seguida, o item de saudação selecione chamado **00_000000**. Isso exibirá os **Detalhes da Tarefa** desta tarefa. Nessa tela, você pode exibir **Contadores de Tarefa** e **Tentativas de Tarefa**.

    ![Detalhes de tarefa](./media/hdinsight-debug-tez-ui/taskdetails.png)

## <a name="next-steps"></a>Próximas etapas
Agora que você aprendeu como exibir hello toouse Tez, saiba mais sobre [usando Hive no HDInsight](hdinsight-use-hive.md).

Para obter mais informações técnicas sobre Tez, consulte Olá [Tez página no Hortonworks](http://hortonworks.com/hadoop/tez/).
