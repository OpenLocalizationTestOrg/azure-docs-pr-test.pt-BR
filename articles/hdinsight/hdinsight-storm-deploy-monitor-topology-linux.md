---
title: aaaDeploy e gerenciar as topologias do Apache Storm no HDInsight baseados em Linux | Microsoft Docs
description: "Saiba como toodeploy, monitorar e gerenciar topologias Apache Storm usando Olá profusão de painel no HDInsight baseados em Linux. Use as ferramentas do Hadoop para Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a>Implantar e gerenciar topologias Apache Storm no HDInsight

Neste documento, conheça os fundamentos de saudação do gerenciamento e monitoramento topologias Storm em execução em Storm em clusters HDInsight.

> [!IMPORTANT]
> Olá etapas neste artigo exigem uma tempestade baseados em Linux no cluster HDInsight. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). 
>
> Para obter informações sobre as topologias de implantação e monitoramento em HDInsight baseado em Windows, consulte [Implantar e gerenciar topologias do Apache Storm no HDInsight baseado em Windows](hdinsight-storm-deploy-monitor-topology.md)


## <a name="prerequisites"></a>Pré-requisitos

* **Storm baseado em Linux no cluster HDInsight**: consulte [Introdução com o Apache Storm no HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) para etapas para criar um cluster

* (Opcional) **Familiaridade com SSH e SCP**: para saber mais, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* (Opcional) **Visual Studio**: SDK do Azure 2.5.1 ou mais recente e hello Data Lake Tools para Visual Studio. Para obter mais informações, consulte [Introdução ao uso das Ferramentas do Data Lake para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

    Um dos Olá seguintes versões do Visual Studio:

  * Visual Studio 2012 com [Atualização 4](http://www.microsoft.com/download/details.aspx?id=39305)

  * Visual Studio 2013 com [Atualização 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/)

  * Visual Studio 2015 (qualquer edição)

  * Visual Studio 2017 (qualquer edição). Data Lake Tools para Visual Studio de 2017 são instalados como parte da saudação carga de trabalho do Azure.

## <a name="submit-a-topology-visual-studio"></a>Enviar uma topologia: Visual Studio

Ferramentas do HDInsight Olá pode ser usado toosubmit c# ou híbrido topologias tooyour cluster Storm. Olá, as etapas a seguir usa um aplicativo de exemplo. Para obter informações sobre como criar seus próprio topologias usando ferramentas do HDInsight hello, consulte [desenvolver c# topologias usando ferramentas do HDInsight Olá para o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

1. Se já não tiver instalado a versão mais recente Olá das ferramentas de Data Lake Olá para o Visual Studio, consulte [começar a usar Data Lake Tools para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

    > [!NOTE]
    > Olá Data Lake Tools para Visual Studio foram anteriormente chamado hello ferramentas do HDInsight para Visual Studio.
    >
    > Data Lake Tools para Visual Studio são incluídos no hello __carga de trabalho do Azure__ para 2017 do Visual Studio.

2. Abra o Visual Studio, selecione **Arquivo** > **Novo** > **Projeto**.

3. Em Olá **novo projeto** caixa de diálogo caixa, expanda **instalado** > **modelos**e, em seguida, selecione **HDInsight**. Saudação de modelos, selecione lista **profusão de exemplo**. Na parte inferior do Olá Olá da caixa de diálogo, digite um nome para o aplicativo hello.

    ![imagem](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. Em **Solution Explorer**, clique com botão direito hello e selecione **enviar tooStorm no HDInsight**.

   > [!NOTE]
   > Se solicitado, insira as credenciais de logon de saudação para sua assinatura do Azure. Se você tiver mais de uma assinatura, faça logon toohello que contém seu Storm no cluster HDInsight.

5. Selecione seu Storm no cluster HDInsight Olá **Cluster Storm** lista suspensa e selecione **enviar**. Você pode monitorar se o envio de saudação foi bem-sucedida usando Olá **saída** janela.

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a>Enviar uma topologia: SSH e hello profusão de comando

1. Use SSH tooconnect toohello HDInsight cluster. Substituir **USERNAME** nome de saudação do seu logon SSH. Substitua o **CLUSTERNAME** pelo nome do seu cluster HDInsight:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Para obter mais informações sobre como usar SSH tooconnect tooyour HDInsight de cluster, consulte [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Use Olá comando toostart uma topologia de exemplo a seguir:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    Esse comando inicia a topologia de WordCount do exemplo hello no cluster hello. Essa topologia gerar aleatoriamente frases e a ocorrência de saudação de contagem de cada palavra em frases hello.

   > [!NOTE]
   > Ao enviar o cluster de toohello de topologia, primeiro você deve copiar o arquivo jar de saudação contendo cluster Olá antes de usar o hello `storm` comando. cluster do toocopy Olá arquivos toohello, você pode usar o hello `scp` comando. Por exemplo, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
   >
   > exemplo de WordCount Hello e obter outros exemplos de starter storm, já estão incluídos no cluster em `/usr/hdp/current/storm-client/contrib/storm-starter/`.

## <a name="submit-a-topology-programmatically"></a>Enviar uma topologia: de forma programática

Programaticamente, você pode implantar um tooStorm de topologia no HDInsight comunicando-se com hello serviço Nimbus hospedado no seu cluster. [https://GitHub.com/Azure-Samples/hdinsight-Java-Deploy-Storm-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) fornece um exemplo de aplicativo Java que demonstra como toodeploy e iniciar uma topologia através de Olá serviço Nimbus.

## <a name="monitor-and-manage-visual-studio"></a>Monitorar e gerenciar: Visual Studio

Quando uma topologia tiver sido enviada com êxito usando o Visual Studio, Olá **Storm topologias** exibir para Olá cluster aparece. Selecione topologia Olá Olá listar tooview informações sobre Olá executando topologia.

![monitor do visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> Você também pode exibir **Topologias Storm** no **Gerenciador de Servidores** expandindo **Azure** > **HDInsight** e clicando com o botão direito do mouse em um Storm no cluster do HDInsight e selecionando **Exibir Topologias Storm**.

Selecione a forma de Olá Olá spouts ou bolts tooview informações sobre esses componentes. Uma nova janela será aberta para cada item selecionado.

### <a name="deactivate-and-reactivate"></a>Desativar e reativar

A desativação de uma topologia pausa até que seja interrompido ou reativado. tooperform essas operações, use Olá __desativar__ e __reativar__ botões na parte superior de saudação do hello __Resumo da topologia__.

### <a name="rebalance"></a>Rebalanceamento

Rebalanceamento uma topologia permite Olá sistema toorevise Olá paralelismo topologia hello. Por exemplo, se você tiver redimensionado Olá cluster tooadd mais notas, rebalanceamento permite que uma topologia de toosee Olá novos nós.

toorebalance uma topologia, use Olá __reequilibrar__ botão na parte superior de saudação do hello __Resumo da topologia__.

> [!WARNING]
> Rebalanceamento uma topologia de primeiro desativa a topologia de saudação, redistribui os trabalhadores uniformemente em cluster hello e finalmente retorna Olá topologia toohello estado antes de rebalanceamento ocorrer. Então se topologia Olá estava ativa, ele fica ativo novamente. Se ela foi desativada, ela permanecerá desativada.

### <a name="kill-a-topology"></a>Encerrar uma topologia

Topologias Storm continuam em execução até que eles sejam interrompidos ou Olá cluster é excluído. toostop uma topologia, use Olá __Kill__ botão na parte superior de saudação do hello __Resumo da topologia__.

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a>Monitorar e gerenciar: SSH e hello profusão de comando

Olá `storm` utilitário permite que você toowork com a execução de topologias de linha de comando hello. Use `storm -h` para uma lista completa de comandos.

### <a name="list-topologies"></a>Topologias de lista

Use Olá toolist de comando a seguir todas as topologias em execução:

    storm list

Esse comando retorna informações toohello semelhante texto a seguir:

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a>Desativar e reativar

A desativação de uma topologia pausa até que seja interrompido ou reativado. Use Olá toodeactivate de comando a seguir e reativar:

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a>Eliminar uma topologia em execução

As topologias Storm, depois de iniciadas, continuarão em execução até serem interrompidas. toostop uma topologia, use Olá comando a seguir:

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a>Rebalanceamento

Rebalanceamento uma topologia permite Olá sistema toorevise Olá paralelismo topologia hello. Por exemplo, se você tiver redimensionado Olá cluster tooadd mais notas, rebalanceamento permite que uma topologia de toosee Olá novos nós.

> [!WARNING]
> Rebalanceamento uma topologia de primeiro desativa a topologia de saudação, redistribui os trabalhadores uniformemente em cluster hello e finalmente retorna Olá topologia toohello estado antes de rebalanceamento ocorrer. Então se topologia Olá estava ativa, ele fica ativo novamente. Se ela foi desativada, ela permanecerá desativada.

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a>Monitorar e gerenciar: interface do usuário do Storm

Olá profusão de interface do usuário fornece uma interface da web para trabalhar com a execução de topologias e está incluída no seu cluster HDInsight. Olá tooview Storm da interface do usuário, use um tooopen do navegador da web **https://CLUSTERNAME.azurehdinsight.net/stormui**, onde **CLUSTERNAME** é o nome de saudação do cluster.

> [!NOTE]
> Se for solicitado tooprovide um nome de usuário e senha, insira o administrador de cluster de saudação (administrador) e a senha que você usou quando criar cluster de saudação.

### <a name="main-page"></a>Página principal

página principal de saudação do hello profusão de interface do usuário fornece Olá informações a seguir:

* **Resumo do cluster**: informações básicas sobre cluster de Storm hello.
* **Resumo da topologia**: uma lista das topologias em execução. Use links Olá tooview esta seção obter mais informações sobre topologias específicas.
* **Resumo do Supervisor**: informações sobre o supervisor de profusão de saudação.
* **Configuração de Nimbus**: configuração Nimbus para cluster hello.

### <a name="topology-summary"></a>Resumo da topologia

Selecionar um link de saudação **Resumo da topologia** seção exibe Olá informações sobre topologia Olá a seguir:

* **Resumo de topologia**: informações básicas sobre a topologia de saudação.
* **Ações de topologia**: ações de gerenciamento que você pode executar para a topologia de saudação.

  * **Ativar**: retoma o processamento de uma topologia de desativada.
  * **Desativar**: pausa uma topologia em execução.
  * **Reequilibrar**: ajusta o paralelismo de saudação da topologia de saudação. Você deve reequilibrar topologias em execução depois que você tenha alterado Olá número de nós no cluster de saudação. Esta operação permite Olá topologia tooadjust paralelismo toocompensate para Olá aumentando ou diminuindo o número de nós no cluster de saudação.

    Para obter mais informações, consulte <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">Noções básicas sobre o paralelismo de saudação de uma topologia Storm</a>.
  * **Kill**: encerra uma topologia Storm depois Olá especificada de tempo limite.
* **Estatísticas de topologia**: estatísticas sobre a topologia de saudação. tooset Olá período de tempo para Olá restantes entradas na página de saudação, use os links de Olá Olá **janela** coluna.
* **Spouts**: Olá spouts usados pelo topologia hello. Use os links de saudação na tooview seção para obter mais informações sobre spouts específicos.
* **Bolts**: Olá parafusos usados pelo topologia hello. Use os links de saudação na tooview seção para obter mais informações sobre parafusos específicos.
* **Configuração de topologia**: configuração de saudação da topologia de saudação selecionada.

### <a name="spout-and-bolt-summary"></a>Resumo de Spout e Bolt

Selecionando um spout da saudação **Spouts** ou **Bolts** seções exibe Olá informações sobre o item de saudação selecionada a seguir:

* **Resumo de componente**: informações básicas sobre spout hello ou raio.
* **Estatísticas de spout/raio**: estatísticas sobre Olá spout ou parafuso. tooset Olá período de tempo para Olá restantes entradas na página de saudação, use os links de Olá Olá **janela** coluna.
* **Estatísticas de entrada** (incluem apenas): consumidos pelo raio de saudação de fluxos de entrada de informações sobre hello.
* **Estatísticas de saída**: informações sobre fluxos de saudação emitidos por essa spout ou parafuso.
* **Executores**: informações sobre instâncias de saudação do spout hello ou raio. Selecione Olá **porta** gerada de um log de informações de diagnóstico de entrada para tooview um executor específico para essa instância.
* **Erros**: qualquer informação de erro para este spout ou bolt.

## <a name="monitor-and-manage-rest-api"></a>Monitorar e gerenciar: API REST

Olá profusão de interface do usuário é criada sobre Olá API REST, para que você possa executar gerenciamento semelhantes e funcionalidade de monitoramento usando a API REST de saudação. Você pode usar ferramentas personalizadas do toocreate Olá API REST para gerenciar e monitorar as topologias Storm.

Para obter mais informações, veja [API REST da interface do usuário do Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html). Olá informações a seguir são específicos toousing Olá API de REST do Apache Storm no HDInsight.

> [!IMPORTANT]
> Olá profusão de REST API não está disponível publicamente em Olá internet e deve ser acessado usando um SSH túnel toohello HDInsight nó principal do cluster. Para obter informações sobre como criar e usar um túnel SSH, consulte [tooaccess Use SSH túnel Ambari web da interface do usuário, ResourceManager, JobHistory, NameNode, Oozie e outras interfaces do usuário da web](hdinsight-linux-ambari-ssh-tunnel.md).

### <a name="base-uri"></a>URI de base

Olá URI de base para a API REST de saudação em clusters HDInsight baseados em Linux está disponível no nó de cabeçalho de saudação em **https://HEADNODEFQDN:8744/api/v1/**. nome de domínio de saudação do nó principal Olá é gerado durante a criação do cluster e não é estático.

Você pode encontrar o nome de domínio totalmente qualificado (FQDN) Olá para o nó principal do cluster de saudação de várias maneiras diferentes:

* **Em uma sessão SSH**: usar o comando Olá `headnode -f` de um cluster de toohello sessão SSH.
* **Do Ambari Web**: selecione **serviços** da parte superior de saudação da página hello, em seguida, selecione **Storm**. De saudação **resumo** guia, selecione **profusão de interface do usuário servidor**. Olá FQDN do nó Olá Olá profusão de interface do usuário e a API REST está em execução é no início de saudação da página de saudação.
* **Na API de REST do Ambari**: usar o comando Olá `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` tooretrieve informações sobre o nó Olá Olá profusão de interface do usuário e a API REST estão em execução no. Substituir **senha** com a senha de administrador Olá para cluster hello. Substituir **CLUSTERNAME** com o nome do cluster hello. Em resposta hello, entrada de "host_name" hello contém Olá FQDN do nó de saudação.

### <a name="authentication"></a>Autenticação

Solicitações toohello devem usar a API REST **autenticação básica**, portanto, você usa o nome do administrador de cluster de HDInsight de saudação e a senha.

> [!NOTE]
> Porque a autenticação básica é enviada usando o texto não criptografado, você deve **sempre** usar comunicações toosecure HTTPS com cluster hello.

### <a name="return-values"></a>Valores de retorno

Informações que são retornadas da saudação REST API só pode ser usada em cluster hello ou máquinas virtuais em Olá mesma rede Virtual do Azure como cluster hello. Por exemplo, nome de domínio totalmente qualificado de saudação (FQDN) retornado para os servidores de Zookeeper não estará acessível de saudação à Internet.

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como topologias toodeploy e monitor usando Olá profusão de painel, saiba como muito[topologias em Java desenvolver usando Maven](hdinsight-storm-develop-java-topology.md).

Para obter mais topologias de exemplo, consulte [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md).
