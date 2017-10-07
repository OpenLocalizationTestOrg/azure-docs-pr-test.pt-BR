---
title: aaaDeploy e gerenciar as topologias do Apache Storm no HDInsight | Microsoft Docs
description: "Saiba como toodeploy, monitorar e gerenciar topologias Apache Storm usando Olá profusão de painel no HDInsight. Use as ferramentas do Hadoop para Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a>Implantar e gerenciar topologias Apache Storm no HDInsight baseado no Windows

Olá profusão de painel permite que você tooeasily implantar e executar o cluster HDInsight do Apache Storm topologias tooyour usando seu navegador da web. Você também pode usar o hello painel toomonitor e gerenciar topologias em execução. Se você usar o Visual Studio, ferramentas do HDInsight Olá para o Visual Studio fornecem recursos semelhantes no Visual Studio.

Olá profusão de painel e recursos Storm Olá Olá ferramentas HDInsight dependem Olá profusão de REST API, que pode ser usado toocreate suas próprias soluções de monitoramento e gerenciamento.

> [!IMPORTANT]
> etapas de saudação neste documento exigem uma tempestade no cluster HDInsight que usa o Windows como sistema operacional de saudação. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Para obter informações sobre como implantar e gerenciar topologias Storm com um cluster HDInsight que usa Linux, veja [Implantar e gerenciar topologias Apache Storm no HDInsight baseado em Linux](hdinsight-storm-deploy-monitor-topology-linux.md)

## <a name="prerequisites"></a>Pré-requisitos

* **Apache Storm no HDInsight** - veja [Introdução ao Apache Storm no HDInsight](hdinsight-apache-storm-tutorial-get-started.md) para obter as etapas de criação de um cluster.

* Para Olá **Storm painel**: um navegador da web modernos que dá suporte a HTML5.

* Para **Visual Studio** -2.5.1 do SDK do Azure ou mais recente e hello ferramentas HDInsight para Visual Studio. Consulte [começar a usar as ferramentas do HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall e configurar as ferramentas do HDInsight Olá para o Visual Studio.

    Um dos Olá seguintes versões do Visual Studio:

  * Visual Studio 2012 com Atualização 4

  * Visual Studio 2013 com Atualização 4 ou Visual Studio 2013 Community

  * Visual Studio 2015 (qualquer edição)

  * Visual Studio 2017 (qualquer edição)

## <a name="storm-dashboard"></a>Painel Storm

Olá profusão de painel é uma página da web disponível no seu cluster Storm. Olá URL é **https://&lt;clustername >.azurehdinsight.net/**, onde **clustername** é nome de saudação do seu Storm no cluster HDInsight.

Na parte superior do hello da saudação profusão de painel, selecione **topologia enviar**. Siga as instruções de saudação em Olá página toorun uma topologia de amostra ou tooupload e execute uma topologia que você criou.

![Olá Enviar página topologia][storm-dashboard-submit]

### <a name="storm-ui"></a>Interface do Usuário do Storm

Olá profusão de painel, selecione Olá **profusão de interface do usuário** link. Isso exibe informações sobre o cluster Olá, em adição tooany executando topologias.

![Olá storm ui][storm-dashboard-ui]

> [!NOTE]
> Com algumas versões do Internet Explorer, você pode descobrir que Olá que profusão de interface do usuário não são atualizados depois que você visitou primeiro-lo. Por exemplo, ele não pode mostrar novas topologias de saudação enviada por você, ou pode exibir uma topologia como ativo quando você o desativada anteriormente. A Microsoft está ciente desse problema e está trabalhando em uma solução.

#### <a name="main-page"></a>Página principal

página principal de saudação do hello profusão de interface do usuário fornece Olá informações a seguir:

* **Resumo do cluster**: informações básicas sobre cluster de Storm hello.

* **Resumo da topologia**: uma lista das topologias em execução. Use links Olá tooview esta seção obter mais informações sobre topologias específicas.

* **Resumo do Supervisor**: informações sobre o supervisor de profusão de saudação.

* **Configuração de Nimbus**: configuração Nimbus para cluster hello.

#### <a name="topology-summary"></a>Resumo da topologia

Selecionar um link de saudação **Resumo da topologia** seção exibe Olá informações sobre topologia Olá a seguir:

* **Resumo de topologia**: informações básicas sobre a topologia de saudação.

* **Ações de topologia**: ações de gerenciamento que você pode executar para a topologia de saudação.

  * **Ativar**: retoma o processamento de uma topologia de desativada.

  * **Desativar**: pausa uma topologia em execução.

  * **Reequilibrar**: ajusta o paralelismo de saudação da topologia de saudação. Você deve reequilibrar topologias em execução depois que você tenha alterado Olá número de nós no cluster de saudação. Isso permite Olá topologia tooadjust paralelismo toocompensate para Olá aumentando ou diminuindo o número de nós no cluster de saudação.

      Para obter mais informações, consulte [Noções básicas sobre o paralelismo de saudação de uma topologia de Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

  * **Kill**: encerra uma topologia Storm depois Olá especificada de tempo limite.

* **Estatísticas de topologia**: estatísticas sobre a topologia de saudação. Use os links de Olá Olá **janela** coluna tooset Olá período para Olá restantes entradas na página de saudação.

* **Spouts**: Olá spouts usados pelo topologia hello. Use os links de saudação na tooview seção para obter mais informações sobre spouts específicos.

* **Bolts**: Olá parafusos usados pelo topologia hello. Use os links de saudação na tooview seção para obter mais informações sobre parafusos específicos.

* **Configuração de topologia**: configuração de saudação da topologia de saudação selecionada.

#### <a name="spout-and-bolt-summary"></a>Resumo de Spout e Bolt

Selecionando um spout da saudação **Spouts** ou **Bolts** seções exibe Olá informações sobre o item de saudação selecionada a seguir:

* **Resumo de componente**: informações básicas sobre spout hello ou raio.

* **Estatísticas de spout/raio**: estatísticas sobre Olá spout ou parafuso. Use os links de Olá Olá **janela** coluna tooset Olá período para Olá restantes entradas na página de saudação.

* **Estatísticas de entrada** (incluem apenas): consumidos pelo raio de saudação de fluxos de entrada de informações sobre hello.

* **Estatísticas de saída**: informações sobre fluxos de saudação emitidos por essa spout ou parafuso.

* **Executores**: informações sobre instâncias de saudação do spout hello ou raio. Selecione Olá **porta** gerada de um log de informações de diagnóstico de entrada para tooview um executor específico para essa instância.

* **Erros**: qualquer informação de erro para este spout ou bolt.

## <a name="hdinsight-tools-for-visual-studio"></a>Ferramentas do HDInsight para Visual Studio

Ferramentas do HDInsight Olá pode ser usado toosubmit c# ou híbrido topologias tooyour cluster Storm. Olá, as etapas a seguir usa um aplicativo de exemplo. Para obter informações sobre como criar seus próprio topologias usando ferramentas do HDInsight hello, consulte [desenvolver c# topologias usando ferramentas do HDInsight Olá para o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Usar Olá etapas toodeploy uma profusão de tooyour do exemplo a seguir no cluster HDInsight, exibir e gerenciar a topologia de saudação.

1. Se já não tiver instalado a versão mais recente Olá de saudação ferramentas HDInsight para Visual Studio, consulte [começar a usar as ferramentas do HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Abra o Visual Studio, selecione **Arquivo** > **Novo** > **Projeto**.

3. Em Olá **novo projeto** caixa de diálogo caixa, expanda **instalado** > **modelos**e, em seguida, selecione **HDInsight**. Saudação de modelos, selecione lista **profusão de exemplo**. Na parte inferior do Olá Olá da caixa de diálogo, digite um nome para o aplicativo hello.

    ![imagem](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. Em **Solution Explorer**, clique com botão direito hello e selecione **enviar tooStorm no HDInsight**.

   > [!NOTE]
   > Se solicitado, insira as credenciais de logon de saudação para sua assinatura do Azure. Se você tiver mais de uma assinatura, faça logon toohello que contém seu Storm no cluster HDInsight.

5. Selecione seu Storm no cluster HDInsight Olá **Cluster Storm** lista suspensa e selecione **enviar**. Você pode monitorar se o envio de saudação foi bem-sucedida usando Olá **saída** janela.

6. Quando a topologia de saudação foi enviada com êxito, Olá **Storm topologias** para cluster Olá deve aparecer. Selecione topologia Olá Olá listar tooview informações sobre Olá executando topologia.

    ![monitor do visual studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > Você também pode exibir **Topologias Storm** no **Gerenciador de Servidores** expandindo **Azure** > **HDInsight** e clicando com o botão direito do mouse em um Storm no cluster do HDInsight e selecionando **Exibir Topologias Storm**.

    Selecione a forma de Olá Olá spouts ou bolts tooview informações sobre esses componentes. Uma nova janela será aberta para cada item selecionado.

   > [!NOTE]
   > nome de saudação da topologia de saudação é o nome de classe de Olá da topologia de saudação (nesse caso, `HelloWord`,) com um carimbo de hora anexado.

7. De saudação **Resumo da topologia** exibição, selecione **Kill** toostop topologia de saudação.

   > [!NOTE]
   > Topologias Storm continuam em execução até que eles sejam interrompidos ou Olá cluster é excluído.


## <a name="rest-api"></a>API REST

Olá profusão de interface do usuário é criada sobre Olá API REST, para que você possa executar gerenciamento semelhantes e funcionalidade de monitoramento usando a API REST de saudação. Você pode usar ferramentas personalizadas do toocreate Olá API REST para gerenciar e monitorar as topologias Storm.

Para obter mais informações, veja [API REST da interface do usuário do Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md). Olá informações a seguir são específicos toousing Olá API de REST do Apache Storm no HDInsight.

### <a name="base-uri"></a>URI de base

Olá URI base para Olá API REST em clusters de HDInsight é **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, onde **clustername** é o nome de saudação do seu Storm em Cluster HDInsight.

### <a name="authentication"></a>Autenticação

Solicitações toohello devem usar a API REST **autenticação básica**, portanto, você usa o nome do administrador de cluster de HDInsight de saudação e a senha.

> [!NOTE]
> Porque a autenticação básica é enviada usando o texto não criptografado, você deve **sempre** usar comunicações toosecure HTTPS com cluster hello.

### <a name="return-values"></a>Valores de retorno

Informações que são retornadas da saudação REST API só pode ser usada em cluster hello ou máquinas virtuais em Olá mesma rede Virtual do Azure como cluster hello. Por exemplo, nome de domínio totalmente qualificado de saudação (FQDN) retornado para os servidores de Zookeeper não ser acessível de saudação à Internet.

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como topologias toodeploy e monitor usando Olá profusão de painel, saiba como:

* [Desenvolver c# topologias usando ferramentas do HDInsight Olá para Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [Desenvolver topologias baseadas em Java usando Maven](hdinsight-storm-develop-java-topology.md)

Para obter mais topologias de exemplo, consulte [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md).

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
