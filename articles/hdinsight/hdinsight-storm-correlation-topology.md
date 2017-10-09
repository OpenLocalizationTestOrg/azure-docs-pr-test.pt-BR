---
title: eventos de aaaCorrelate ao longo do tempo com Storm e HBase em HDInsight
description: Saiba como toocorrelate eventos que chegam em momentos diferentes usando Storm e HBase em HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a>Correlacionar eventos que chegam em diferentes horários usando Storm e o HBase

Usando um armazenamento de dados persistentes com o Apache Storm, você pode correlacionar as entradas de dados que chegam em momentos diferentes. Por exemplo, a vinculação de eventos de logon e logoff de um toocalculate de sessão de usuário como o tempo a sessão de saudação durou.

Neste documento, você aprenderá como toocreate uma topologia c# Storm básica que rastreia eventos de logon e logoff de sessões de usuário e calcula Olá duração da sessão de saudação. topologia de saudação usa HBase como um repositório de dados persistentes. HBase também permite que você consultas de lote tooperform informações adicionais do tooproduce Olá dados históricos. Por exemplo, quantas sessões de usuário foram iniciadas ou encerradas durante um período de tempo específico.

## <a name="prerequisites"></a>Pré-requisitos

* Visual Studio e hello ferramentas de HDInsight para Visual Studio. Para obter mais informações, consulte [começar a usar as ferramentas do HDInsight Olá para o Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Apache Storm em cluster HDInsight (baseado em Windows).

  > [!WARNING]
  > Enquanto SCP.NET topologias têm suporte em clusters baseados em Linux Storm criados após 10/28/2016, Olá HBase SDK para o pacote .NET disponível a partir do 10/28/2016 não funciona corretamente no HDInsight baseados em Linux

* Apache HBase no cluster HDInsight (baseado em Linux ou Windows).

  > [!IMPORTANT]
  > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Java](https://java.com) 1.7 ou posterior em seu ambiente de desenvolvimento. Java é usado toopackage Olá topologia quando é enviado toohello cluster do HDInsight.

  * Olá **JAVA_HOME** diretório de toohello de ponto de deve variável de ambiente que contém Java.
  * Olá **%JAVA_HOME%/bin** diretório deve estar no caminho de saudação

## <a name="architecture"></a>Arquitetura

![Diagrama de saudação do fluxo de dados por meio de topologia Olá](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

Correlacionar eventos exige um identificador comum para a origem do evento hello. Por exemplo, uma ID de usuário, ID de sessão ou outro conjunto de dados que é um) exclusivo e b) incluído no tooStorm de todos os dados enviados. Este exemplo usa um toorepresent de valor GUID de uma ID de sessão.

Esse exemplo consiste em dois clusters HDInsight:

* HBase: repositório de dados persistente dados históricos
* Storm: usado tooingest os dados de entrada

dados de saudação são gerados aleatoriamente, topologia de profusão de saudação e consiste em Olá itens a seguir:

* ID da sessão: um GUID que identifica exclusivamente cada sessão
* Evento: um evento INICIAR ou ENCERRAR. Para este exemplo, INICIAR sempre ocorre antes do ENCERRAR
* Tempo: tempo de saudação do evento hello.

Esses dados são processados e armazenados no HBase.

### <a name="storm-topology"></a>Topologia Storm

Quando uma sessão é iniciada, um **iniciar** evento é recebido por topologia hello e registrado tooHBase. Quando um **final** evento é recebido, topologia Olá recupera Olá **iniciar** eventos e calcula o tempo de saudação entre eventos Olá dois. Isso **duração** valor é armazenado no HBase juntamente com hello **final** informações de evento.

> [!IMPORTANT]
> Enquanto essa topologia demonstra o padrão básico hello, uma solução de produção precisará tootake design para Olá os seguintes cenários:
>
> * Eventos que chegam fora de ordem
> * Eventos duplicados
> * Eventos ignorados

topologia de exemplo Hello é composta de saudação componentes a seguir:

* Session.cs: simula uma sessão de usuário por meio da criação de uma ID de sessão aleatório, duração de sessão do início Olá tempo e por quanto tempo.

* Spout.cs: cria 100 sessões, emite um evento de início, aguarda o tempo limite aleatória de saudação para cada sessão e, em seguida, emite um evento de término. Em seguida, recicla terminou toogenerate sessões novas.

* HBaseLookupBolt.cs: usa toolook de ID de sessão Olá as informações de sessão do HBase. Quando um evento de término é processado, ele localiza um evento de início correspondente hello e calcula Olá duração da sessão de saudação.

* HBaseBolt.cs: Armazena informações no HBase.

* TypeHelper.cs: Ajuda na conversão de tipo ao ler de / gravar tooHBase.

### <a name="hbase-schema"></a>Esquema do HBase

No HBase, dados de saudação são armazenados em uma tabela com hello configurações do esquema a seguir:

* Chave de linha: Olá ID de sessão é usada como chave de saudação para linhas nessa tabela.

* Família de coluna: nome da família Olá é 'cf'. As colunas armazenadas nesta família são:

  * evento: INICIAR ou ENCERRAR.

  * hora: tempo de saudação em milissegundos que Olá evento ocorreu.

  * Duração: Olá comprimento entre eventos de início e término.

* VERSÕES: família de 'cf' hello é definida tooretain 5 versões de cada linha.

  > [!NOTE]
  > As versões são um log dos valores anteriores armazenados para uma chave de linha específica. Por padrão, HBase só retorna o valor Olá para a versão mais recente de saudação de uma linha. Nesse caso, hello mesma linha é usada para todos os eventos (início, fim.) de que cada versão de uma linha é identificado pelo valor de carimbo de hora hello. As versões fornecem exibição do histórico de eventos registrados para uma ID específica.

## <a name="download-hello-project"></a>Baixe o projeto de saudação

projeto de exemplo Hello pode ser baixado do [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).

Este download contém Olá projetos c# a seguir:

* CorrelationTopology: topologia de Storm C# que emite aleatoriamente eventos de iniciar e encerrar para sessões de usuário. Cada sessão dura entre 1 e 5 minutos.

* SessionInfo: Console aplicativo c# que cria a tabela do HBase hello e fornece exemplos de consultas tooreturn informações sobre os dados armazenados de sessão.

## <a name="create-hello-table"></a>Criar tabela Olá

1. Olá abrir **SessionInfo** projeto no Visual Studio.

2. No **Solution Explorer**, Olá atalho **SessionInfo** do projeto e selecione **propriedades**.

    ![Captura de tela do menu com as propriedades selecionadas](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. Selecione **configurações**, então a saudação do conjunto de valores a seguir:

   * HBaseClusterURL: cluster Olá URL tooyour HBase. Por exemplo, https://meuclusterhbase.azurehdinsight.net.

   * HBaseClusterUserName: conta de usuário de administração/HTTP Olá para o cluster

   * HBaseClusterPassword: Olá senha Olá administrador/HTTP conta de usuário

   * HBaseTableName: nome de saudação do hello tabela toouse com este exemplo

   * HBaseTableColumnFamily: nome da família Olá coluna

     ![Imagem da caixa de diálogo de configuração](./media/hdinsight-storm-correlation-topology/settings.png)

4. Execute a solução de saudação. Quando solicitado, selecione hello "c" toocreate chave Olá tabela cluster HBase.

## <a name="build-and-deploy-hello-storm-topology"></a>Criar e implantar Olá Storm topologia

1. Olá abrir **CorrelationTopology** solução no Visual Studio.

2. Em **Solution Explorer**, Olá atalho **CorrelationTopology** do projeto e selecione Propriedades.

3. Na janela de propriedades de saudação, selecione **configurações** e insira os valores de configuração de saudação para este projeto. 5 primeiro Hello são Olá mesmos valores usados pelo Olá **SessionInfo** projeto:

   * HBaseClusterURL: cluster Olá URL tooyour HBase. Por exemplo, https://meuclusterhbase.azurehdinsight.net.

   * HBaseClusterUserName: conta de usuário Olá administrador/HTTP para o cluster.

   * HBaseClusterPassword: Olá senha Olá administrador/HTTP conta de usuário.

   * HBaseTableName: o nome de saudação do hello tabela toouse com este exemplo. Esse valor é Olá mesmo nome de tabela como usado no projeto de SessionInfo hello.

   * HBaseTableColumnFamily: nome de família da coluna Olá. Esse valor é Olá a mesma coluna Nome da família como usado no projeto de SessionInfo hello.

   > [!IMPORTANT]
   > Não altere Olá HBaseTableColumnNames, como padrões de saudação são nomes Olá usados pelo **SessionInfo** tooretrieve dados.

4. Salvar as propriedades de saudação e compilar o projeto de saudação.

5. Em **Solution Explorer**, clique com botão direito hello e selecione **enviar tooStorm no HDInsight**. Se solicitado, insira as credenciais de saudação para sua assinatura do Azure.

   ![Imagem de saudação Enviar item de menu toostorm](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. Em Olá **topologia enviar** caixa de diálogo, o cluster Storm de saudação selecione deseja toodeploy essa topologia para.

   > [!NOTE]
   > Olá primeira vez que você enviar uma topologia, pode levar alguns segundos nome de saudação tooretrieve seus clusters HDInsight.

7. Depois que a topologia Olá foi carregado e enviado toohello cluster, Olá **profusão de exibição de topologia** abre e exibe o saudação executando topologia. dados de saudação toorefresh, selecione Olá **CorrelationTopology** e use o botão de atualização de saudação à saudação parte superior direita da página de saudação.

   ![Imagem de exibição de topologia Olá](./media/hdinsight-storm-correlation-topology/topologyview.png)

   Quando a topologia Olá começa a geração de dados, Olá valor Olá **Emitted** incrementos de coluna.

   > [!NOTE]
   > Se hello **profusão de exibição de topologia** não abrir automaticamente, use Olá tooopen as etapas a seguir:
   >
   > 1. No **Gerenciador de Soluções**, expanda **Azure** e **HDInsight**.
   > 2. Cluster Storm do botão direito do mouse Olá que Olá topologia está em execução no e, em seguida, selecione **topologias de profusão de exibição**

## <a name="query-hello-data"></a>Consultar dados Olá

Depois de dados foi emitidos, use Olá seguintes etapas tooquery Olá dados.

1. Retornar toohello **SessionInfo** projeto. Se não estiver executando, inicie uma nova instância dele.

2. Quando solicitado, selecione **s** toosearch para o início do evento. São solicitada tooenter um início e término tempo toodefine um intervalo de tempo - serão retornados somente eventos entre essas duas vezes.

    Ao inserir o início de saudação de formato e de término da seguinte de saudação de uso: hh: mm e 'm'' ou 'pm'. Por exemplo, 11:20pm.

    eventos tooreturn conectado, use uma hora de início do antes de saudação profusão de topologia foi implantada e uma hora de término da agora. dados de retorno Olá contém entradas toohello semelhante texto a seguir:

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

Procurando saudação do fim eventos funciona mesmo como eventos de início. No entanto, eventos de término são gerados aleatoriamente entre 1 e 5 minutos após o início do evento hello. Você pode ter tootry alguns intervalos toofind Olá final eventos. Eventos de término também contêm durante Olá Olá sessão - diferença Olá entre a hora de evento Olá início e término do evento. Veja um exemplo de dados para eventos ENCERRAR:

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> Enquanto os valores de tempo de saudação que inserir estão no horário local, tempo de saudação retornado da consulta hello está em UTC.

## <a name="stop-hello-topology"></a>Parar a topologia de saudação

Quando você estiver pronto toostop topologia de hello, retornar toohello **CorrelationTopology** projeto no Visual Studio. Em Olá **profusão de exibição de topologia**, selecione a topologia de saudação e, em seguida, use Olá **Kill** botão na parte superior de saudação do modo de exibição de topologia de saudação.

## <a name="delete-your-cluster"></a>Excluir o cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Próximas etapas

Para obter mais exemplos de topologias Storm, consulte [Exemplo de topologias para Storm no HDInsight](hdinsight-storm-example-topology.md).
