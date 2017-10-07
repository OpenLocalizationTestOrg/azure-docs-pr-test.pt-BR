---
title: "aaaMonitor e gerenciar o HDInsight do Azure usando a interface do usuário do Ambari Web | Microsoft Docs"
description: "Saiba como toouse Ambari toomonitor e gerencie clusters HDInsight baseados em Linux. Neste documento, você aprenderá como clusters de saudação toouse Ambari da interface do usuário da Web incluídos no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a>Gerenciar clusters HDInsight usando Olá Ambari Web UI

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Apache Ambari simplifica o gerenciamento de saudação e monitoramento de um cluster de Hadoop, fornecendo a interface do usuário e REST API toouse fácil da web. Ambari é incluído em clusters HDInsight baseados em Linux e é Olá toomonitor usado cluster e faça alterações de configuração.

Neste documento, você aprenderá como toouse Olá Ambari Web UI com um cluster HDInsight.

## <a id="whatis"></a>O que é o Ambari?

O [Apache Ambari](http://ambari.apache.org) simplifica o gerenciamento do Hadoop, fornecendo uma interface do usuário da Web fácil de usar. Você pode usar o Ambari para criar, gerenciar e monitorar clusters do Hadoop. Os desenvolvedores podem integrar esses recursos em seus aplicativos usando Olá [APIs de REST do Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

Saudação da interface do usuário do Ambari Web é fornecida por padrão com clusters de HDInsight que usam o sistema de operacional Linux hello.

> [!IMPORTANT]
> Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). 

## <a name="connectivity"></a>Conectividade

Saudação da interface do usuário do Ambari Web está disponível no seu cluster HDInsight no HTTPS://CLUSTERNAME.azurehdidnsight.net, onde **CLUSTERNAME** é o nome de saudação do cluster.

> [!IMPORTANT]
> Conexão tooAmbari no HDInsight requer HTTPS. Quando solicitado para autenticação, use o nome de conta de administrador hello e senha que você forneceu quando Olá cluster foi criado.

## <a name="ssh-tunnel-proxy"></a>Túnel SSH (proxy)

Enquanto o Ambari para o cluster pode ser acessada diretamente pela Internet de hello, alguns links da saudação Ambari Web UI (como toohello JobTracker) não são expostos no hello da internet. tooaccess esses serviços, você deve criar um túnel SSH. Para obter mais informações, consulte [Usar túnel SSH com o HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).

## <a name="ambari-web-ui"></a>Interface do usuário da Ambari Web

Ao conectar-se toohello Ambari Web UI, será solicitado tooauthenticate toohello página. Use o usuário de administrador de cluster saudação (padrão de administrador) e a senha usada durante a criação do cluster.

Quando abre a página hello, observe barra Olá na parte superior da saudação. Essa barra contém seguinte Olá informações e controles:

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* **Logotipo do Ambari** -abre o painel hello, que pode ser usado toomonitor Olá cluster.

* **Operações de # nome de cluster** -exibe o número de saudação do Ambari as operações em andamento. Selecionar nome do cluster hello ou **ops #** exibe uma lista de operações em segundo plano.

* **alertas de #** -exibe avisos ou alertas críticos, se houver, para o cluster de saudação.

* **Painel** -painel de saudação exibe.

* **Serviços** -configurações de configuração e as informações para os serviços de saudação em cluster hello.

* **Hosts** -configurações de configuração e as informações de nós de saudação no cluster hello.

* **Alertas** : um log de informações, avisos e alertas críticos.

* **Administrador** -pilha/serviços de Software que estão instalados no cluster hello, informações de conta de serviço e segurança Kerberos.

* **Botão Admin** : gerenciamento, configurações de usuário e logoff do Ambari.

## <a name="monitoring"></a>Monitoramento

### <a name="alerts"></a>Alertas

Olá lista a seguir contém Olá comuns status usados pelo Ambari:

* **OK**
* **Aviso**
* **CRÍTICO**
* **DESCONHECIDO**

Alertas que **Okey** causar Olá **alertas #** entrada na parte superior de saudação do número da saudação toodisplay Olá página de alertas. Selecionar essa entrada exibe alertas hello e seus status.

Alertas são organizados em vários grupos padrão, que podem ser exibidos da saudação **alertas** página.

![página alertas](./media/hdinsight-hadoop-manage-ambari/alerts.png)

Você pode gerenciar grupos de saudação usando Olá **ações** menu e selecionando **gerenciar grupos de alerta**.

![diálogo gerenciar grupos de alerta](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

Você também pode gerenciar os métodos de alerta e criar notificações de alerta de saudação **ações** menu selecionando __gerenciar notificações de alerta__. Quaisquer notificações atuais são exibidas. Você também pode criar notificações daqui. As notificações podem ser enviadas por **EMAIL** ou **SNMP** quando ocorrerem combinações específicas de alerta/gravidade. Por exemplo, você pode enviar uma mensagem de email quando qualquer um dos alertas de saudação em Olá **YARN padrão** grupo está definido muito**crítico**.

![Diálogo Criar alerta](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

Por fim, selecionando __gerenciar configurações de alerta__ de saudação __ações__ menu permite tooset número de saudação de vezes que um alerta deve ocorrer antes que uma notificação é enviada. Essa configuração pode ser usado tooprevent notificações para erros transitórios.

### <a name="cluster"></a>HDInsight

Olá **métricas** Olá painel contém uma série de widgets que tornam mais fácil toomonitor status de saudação do cluster em um relance. Vários widgets, tais como **Uso de CPU**, fornecem informações adicionais quando são clicados.

![painel com metrics](./media/hdinsight-hadoop-manage-ambari/metrics.png)

Olá **Heatmaps** guia exibe as métricas como heatmaps colorida, indo de toored verde.

![painel com heatmaps](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

Para obter mais informações sobre nós Olá em cluster hello, selecione **Hosts**. Selecione Olá nó específico que lhe interessam.

![detalhes do host](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a>Serviços

Olá **serviços** barra lateral no painel de saudação fornece visão rápida do status de Olá dos serviços de saudação em execução no cluster de saudação. Vários ícones são usados tooindicate status ou ações que devem ser tomadas. Por exemplo, um símbolo de reciclagem amarelo é exibido se um serviço precisa toobe reciclado.

![barra lateral serviços](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> serviços Olá exibidos diferem entre as versões e tipos de cluster HDInsight. Serviços de saudação exibidos aqui podem ser diferentes Olá serviços exibidos para o cluster.

Selecionar um serviço exibe informações mais detalhadas no serviço de saudação.

![informações de resumo do serviço](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a>Links rápidos

Alguns serviços exibição um **Links rápidos** link na parte superior de saudação da página de saudação. Isso pode ser web específico do serviço de tooaccess usado interfaces do usuário, como:

* **Histórico de Trabalhos** : histórico de trabalhos do MapReduce.
* **Gerenciador de Recursos** : IU do gerenciador de recursos YARN RM.
* **NameNode** : IU NameNode no HDFS (Sistema de Arquivos Distribuído do Hadoop).
* **IU da Web do Oozie** : IU do Oozie.

Selecionar qualquer um desses links abre uma nova guia no seu navegador, que exibe a página selecionada hello.

> [!NOTE]
> Olá selecionando **Links rápidos** entrada para um serviço pode retornar um erro "servidor não encontrado". Se você encontrar esse erro, você deve usar um túnel SSH ao usar Olá **Links rápidos** entrada para este serviço. Para obter informações, consulte [Usar túnel SSH com o HDInsight](hdinsight-linux-ambari-ssh-tunnel.md)

## <a name="management"></a>Gerenciamento

### <a name="ambari-users-groups-and-permissions"></a>Usuários, grupos e permissões do Ambari

O trabalho com usuários, grupos e permissões tem suporte ao usar um cluster HDInsight [ingressado no domínio](hdinsight-domain-joined-introduction.md). Para obter informações sobre como usar o hello Ambari da interface do usuário de gerenciamento em um cluster de domínio, consulte [gerenciar clusters de HDInsight domínio](hdinsight-domain-joined-introduction.md).

> [!WARNING]
> Não altere a senha de saudação de watchdog de Ambari hello (hdinsightwatchdog) no seu cluster HDInsight baseados em Linux. Alteração quebras de senha Olá Olá ações de script toouse capacidade ou executam operações de dimensionamento com o cluster.

### <a name="hosts"></a>Hosts

Olá **Hosts** página lista todos os hosts no cluster hello. hosts de toomanage, siga estas etapas.

![página hosts](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> As ações de adicionar, encerrar e reativar um host não devem ser realizadas com clusters HDInsight.

1. Selecione host Olá que você deseja toomanage.

2. Saudação de uso **ações** ação de saudação do menu tooselect que você deseja tooperform:

   * **Iniciar todos os componentes** -iniciar todos os componentes no host de saudação.

   * **Parar todos os componentes** -parar todos os componentes no host de saudação.

   * **Reinicie todos os componentes** - parar e iniciar todos os componentes no host de saudação.

   * **Ativar o modo de manutenção** -suprime os alertas para o host de saudação. Esse modo deverá ser habilitado se você estiver realizando ações que geram alertas. Por exemplo, parar e iniciar um serviço.

   * **Desativar o modo de manutenção** -retorna Olá host toonormal alertas.

   * **Parar** -DataNode para ou NodeManagers no host de saudação.

   * **Iniciar** -DataNode inicia ou NodeManagers no host de saudação.

   * **Reiniciar** -interrompe e inicia DataNode ou NodeManagers no host de saudação.

   * **Encerrar** -remove um host de cluster de saudação.

     > [!NOTE]
     > Não use esta ação em clusters HDInsight.

   * **Recommission** -adiciona um cluster de toohello host encerrado anteriormente.

     > [!NOTE]
     > Não use esta ação em clusters HDInsight.

### <a id="service"></a>Serviços

De saudação **painel** ou **serviços** página, use Olá **ações** botão final Olá Olá lista de serviços toostop e iniciar todos os serviços.

![Ações de Serviço](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> Enquanto **Adicionar serviço** está listado no menu, não deve ser cluster do HDInsight usado tooadd serviços toohello. Novos serviços devem ser adicionados usando uma Ação de Script durante o provisionamento do cluster. Para saber mais sobre o uso de ações de script, consulte [Personalizar clusters HDInsight usando ações de script](hdinsight-hadoop-customize-cluster-linux.md).

Durante a saudação **ações** botão poderá reiniciar todos os serviços, geralmente você deseja toostart, parar ou reiniciar um serviço específico. Use Olá ações de tooperform as etapas a seguir em um serviço individual:

1. De saudação **painel** ou **serviços** , selecione um serviço.

2. Da parte superior de saudação do hello **resumo** guia, use Olá **ações de serviço** botão e selecione Olá ação tootake. Isso reinicia o serviço de saudação em todos os nós.

    ![ação de serviço](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > Reiniciar alguns serviços enquanto Olá cluster está em execução pode gerar alertas. tooavoid alertas, você pode usar o hello **ações de serviço** botão tooenable **modo de manutenção** para serviço de saudação antes de executar a reinicialização de saudação.

3. Quando uma ação tiver sido selecionada, Olá **op #** entrada na parte superior de saudação do hello tooshow de incrementos de página que está ocorrendo uma operação em segundo plano. Se configurado toodisplay, lista de saudação de operações em segundo plano é exibida.

   > [!NOTE]
   > Se você habilitou o **modo de manutenção** para serviço hello, lembre-se de toodisable usando Olá **ações de serviço** botão quando tiver terminado de operação de saudação.

tooconfigure um serviço, use Olá etapas a seguir:

1. De saudação **painel** ou **serviços** , selecione um serviço.

2. Selecione Olá **configurações** configuração atual de saudação de guia é exibida. Uma lista das configurações anteriores também é exibida.

    ![configurações](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. Usar configuração de Olá Olá campos exibidos toomodify e, em seguida, selecione **salvar**. Ou selecione uma configuração anterior e, em seguida, selecione **tornar atual** tooroll fazer configurações anteriores toohello.

## <a name="ambari-views"></a>Exibições do Ambari

Modos de exibição do Ambari permitem que os desenvolvedores tooplug elementos de interface do usuário em Olá Ambari Web UI usando Olá [Ambari exibições Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views). HDInsight fornece Olá exibições com tipos de cluster de Hadoop a seguir:

* Gerenciador de filas de yarn: Gerenciador de filas de saudação fornece uma interface do usuário simple para exibir e modificar as filas do YARN.

* Exibição de hive: Olá Hive exibição permite consultas de Hive toorun diretamente do seu navegador da web. Salvar consultas, exibir os resultados, salvar os resultados do armazenamento de cluster toohello ou baixar o sistema local do tooyour de resultados. Para obter mais informações sobre como usar Exibições do Hive, consulte [Usar Exibições do Hive com o HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).

* Exibição Tez: Olá Tez exibição permite que você toobetter entender e otimizar os trabalhos. Você pode exibir informações sobre como os trabalhos do Tez são executados e quais recursos são usados.
