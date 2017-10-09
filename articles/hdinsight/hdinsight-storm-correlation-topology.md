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
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="126a9-103">Correlacionar eventos que chegam em diferentes horários usando Storm e o HBase</span><span class="sxs-lookup"><span data-stu-id="126a9-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="126a9-104">Usando um armazenamento de dados persistentes com o Apache Storm, você pode correlacionar as entradas de dados que chegam em momentos diferentes.</span><span class="sxs-lookup"><span data-stu-id="126a9-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="126a9-105">Por exemplo, a vinculação de eventos de logon e logoff de um toocalculate de sessão de usuário como o tempo a sessão de saudação durou.</span><span class="sxs-lookup"><span data-stu-id="126a9-105">For example, linking login and logout events for a user session toocalculate how long hello session lasted.</span></span>

<span data-ttu-id="126a9-106">Neste documento, você aprenderá como toocreate uma topologia c# Storm básica que rastreia eventos de logon e logoff de sessões de usuário e calcula Olá duração da sessão de saudação.</span><span class="sxs-lookup"><span data-stu-id="126a9-106">In this document, you learn how toocreate a basic C# Storm topology that tracks login and logout events for user sessions, and calculates hello duration of hello session.</span></span> <span data-ttu-id="126a9-107">topologia de saudação usa HBase como um repositório de dados persistentes.</span><span class="sxs-lookup"><span data-stu-id="126a9-107">hello topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="126a9-108">HBase também permite que você consultas de lote tooperform informações adicionais do tooproduce Olá dados históricos.</span><span class="sxs-lookup"><span data-stu-id="126a9-108">HBase also allows you tooperform batch queries on hello historical data tooproduce additional insights.</span></span> <span data-ttu-id="126a9-109">Por exemplo, quantas sessões de usuário foram iniciadas ou encerradas durante um período de tempo específico.</span><span class="sxs-lookup"><span data-stu-id="126a9-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="126a9-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="126a9-110">Prerequisites</span></span>

* <span data-ttu-id="126a9-111">Visual Studio e hello ferramentas de HDInsight para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="126a9-111">Visual Studio and hello HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="126a9-112">Para obter mais informações, consulte [começar a usar as ferramentas do HDInsight Olá para o Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="126a9-112">For more information, see [Get started using hello HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="126a9-113">Apache Storm em cluster HDInsight (baseado em Windows).</span><span class="sxs-lookup"><span data-stu-id="126a9-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="126a9-114">Enquanto SCP.NET topologias têm suporte em clusters baseados em Linux Storm criados após 10/28/2016, Olá HBase SDK para o pacote .NET disponível a partir do 10/28/2016 não funciona corretamente no HDInsight baseados em Linux</span><span class="sxs-lookup"><span data-stu-id="126a9-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, hello HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="126a9-115">Apache HBase no cluster HDInsight (baseado em Linux ou Windows).</span><span class="sxs-lookup"><span data-stu-id="126a9-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="126a9-116">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="126a9-116">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="126a9-117">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="126a9-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="126a9-118">[Java](https://java.com) 1.7 ou posterior em seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="126a9-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="126a9-119">Java é usado toopackage Olá topologia quando é enviado toohello cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="126a9-119">Java is used toopackage hello topology when it is submitted toohello HDInsight cluster.</span></span>

  * <span data-ttu-id="126a9-120">Olá **JAVA_HOME** diretório de toohello de ponto de deve variável de ambiente que contém Java.</span><span class="sxs-lookup"><span data-stu-id="126a9-120">hello **JAVA_HOME** environment variable must point toohello directory that contains Java.</span></span>
  * <span data-ttu-id="126a9-121">Olá **%JAVA_HOME%/bin** diretório deve estar no caminho de saudação</span><span class="sxs-lookup"><span data-stu-id="126a9-121">hello **%JAVA_HOME%/bin** directory must be in hello path</span></span>

## <a name="architecture"></a><span data-ttu-id="126a9-122">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="126a9-122">Architecture</span></span>

![Diagrama de saudação do fluxo de dados por meio de topologia Olá](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="126a9-124">Correlacionar eventos exige um identificador comum para a origem do evento hello.</span><span class="sxs-lookup"><span data-stu-id="126a9-124">Correlating events requires a common identifier for hello event source.</span></span> <span data-ttu-id="126a9-125">Por exemplo, uma ID de usuário, ID de sessão ou outro conjunto de dados que é um) exclusivo e b) incluído no tooStorm de todos os dados enviados.</span><span class="sxs-lookup"><span data-stu-id="126a9-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent tooStorm.</span></span> <span data-ttu-id="126a9-126">Este exemplo usa um toorepresent de valor GUID de uma ID de sessão.</span><span class="sxs-lookup"><span data-stu-id="126a9-126">This example uses a GUID value toorepresent a session ID.</span></span>

<span data-ttu-id="126a9-127">Esse exemplo consiste em dois clusters HDInsight:</span><span class="sxs-lookup"><span data-stu-id="126a9-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="126a9-128">HBase: repositório de dados persistente dados históricos</span><span class="sxs-lookup"><span data-stu-id="126a9-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="126a9-129">Storm: usado tooingest os dados de entrada</span><span class="sxs-lookup"><span data-stu-id="126a9-129">Storm: used tooingest incoming data</span></span>

<span data-ttu-id="126a9-130">dados de saudação são gerados aleatoriamente, topologia de profusão de saudação e consiste em Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="126a9-130">hello data is randomly generated by hello Storm topology, and consists of hello following items:</span></span>

* <span data-ttu-id="126a9-131">ID da sessão: um GUID que identifica exclusivamente cada sessão</span><span class="sxs-lookup"><span data-stu-id="126a9-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="126a9-132">Evento: um evento INICIAR ou ENCERRAR.</span><span class="sxs-lookup"><span data-stu-id="126a9-132">Event: a START or END event.</span></span> <span data-ttu-id="126a9-133">Para este exemplo, INICIAR sempre ocorre antes do ENCERRAR</span><span class="sxs-lookup"><span data-stu-id="126a9-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="126a9-134">Tempo: tempo de saudação do evento hello.</span><span class="sxs-lookup"><span data-stu-id="126a9-134">Time: hello time of hello event.</span></span>

<span data-ttu-id="126a9-135">Esses dados são processados e armazenados no HBase.</span><span class="sxs-lookup"><span data-stu-id="126a9-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="126a9-136">Topologia Storm</span><span class="sxs-lookup"><span data-stu-id="126a9-136">Storm topology</span></span>

<span data-ttu-id="126a9-137">Quando uma sessão é iniciada, um **iniciar** evento é recebido por topologia hello e registrado tooHBase.</span><span class="sxs-lookup"><span data-stu-id="126a9-137">When a session starts, a **START** event is received by hello topology and logged tooHBase.</span></span> <span data-ttu-id="126a9-138">Quando um **final** evento é recebido, topologia Olá recupera Olá **iniciar** eventos e calcula o tempo de saudação entre eventos Olá dois.</span><span class="sxs-lookup"><span data-stu-id="126a9-138">When an **END** event is received, hello topology retrieves hello **START** event and calculates hello time between hello two events.</span></span> <span data-ttu-id="126a9-139">Isso **duração** valor é armazenado no HBase juntamente com hello **final** informações de evento.</span><span class="sxs-lookup"><span data-stu-id="126a9-139">This **Duration** value is then stored in HBase along with hello **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="126a9-140">Enquanto essa topologia demonstra o padrão básico hello, uma solução de produção precisará tootake design para Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="126a9-140">While this topology demonstrates hello basic pattern, a production solution would need tootake design for hello following scenarios:</span></span>
>
> * <span data-ttu-id="126a9-141">Eventos que chegam fora de ordem</span><span class="sxs-lookup"><span data-stu-id="126a9-141">Events arriving out of order</span></span>
> * <span data-ttu-id="126a9-142">Eventos duplicados</span><span class="sxs-lookup"><span data-stu-id="126a9-142">Duplicate events</span></span>
> * <span data-ttu-id="126a9-143">Eventos ignorados</span><span class="sxs-lookup"><span data-stu-id="126a9-143">Dropped events</span></span>

<span data-ttu-id="126a9-144">topologia de exemplo Hello é composta de saudação componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="126a9-144">hello sample topology is composed of hello following components:</span></span>

* <span data-ttu-id="126a9-145">Session.cs: simula uma sessão de usuário por meio da criação de uma ID de sessão aleatório, duração de sessão do início Olá tempo e por quanto tempo.</span><span class="sxs-lookup"><span data-stu-id="126a9-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long hello session lasts.</span></span>

* <span data-ttu-id="126a9-146">Spout.cs: cria 100 sessões, emite um evento de início, aguarda o tempo limite aleatória de saudação para cada sessão e, em seguida, emite um evento de término.</span><span class="sxs-lookup"><span data-stu-id="126a9-146">Spout.cs: creates 100 sessions, emits a START event, waits hello random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="126a9-147">Em seguida, recicla terminou toogenerate sessões novas.</span><span class="sxs-lookup"><span data-stu-id="126a9-147">Then recycles ended sessions toogenerate new ones.</span></span>

* <span data-ttu-id="126a9-148">HBaseLookupBolt.cs: usa toolook de ID de sessão Olá as informações de sessão do HBase.</span><span class="sxs-lookup"><span data-stu-id="126a9-148">HBaseLookupBolt.cs: uses hello session ID toolook up session information from HBase.</span></span> <span data-ttu-id="126a9-149">Quando um evento de término é processado, ele localiza um evento de início correspondente hello e calcula Olá duração da sessão de saudação.</span><span class="sxs-lookup"><span data-stu-id="126a9-149">When an END event is processed, it finds hello corresponding START event and calculates hello duration of hello session.</span></span>

* <span data-ttu-id="126a9-150">HBaseBolt.cs: Armazena informações no HBase.</span><span class="sxs-lookup"><span data-stu-id="126a9-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="126a9-151">TypeHelper.cs: Ajuda na conversão de tipo ao ler de / gravar tooHBase.</span><span class="sxs-lookup"><span data-stu-id="126a9-151">TypeHelper.cs: Helps with type conversion when reading from/writing tooHBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="126a9-152">Esquema do HBase</span><span class="sxs-lookup"><span data-stu-id="126a9-152">HBase schema</span></span>

<span data-ttu-id="126a9-153">No HBase, dados de saudação são armazenados em uma tabela com hello configurações do esquema a seguir:</span><span class="sxs-lookup"><span data-stu-id="126a9-153">In HBase, hello data is stored in a table with hello following schema/settings:</span></span>

* <span data-ttu-id="126a9-154">Chave de linha: Olá ID de sessão é usada como chave de saudação para linhas nessa tabela.</span><span class="sxs-lookup"><span data-stu-id="126a9-154">Row key: hello session ID is used as hello key for rows in this table.</span></span>

* <span data-ttu-id="126a9-155">Família de coluna: nome da família Olá é 'cf'.</span><span class="sxs-lookup"><span data-stu-id="126a9-155">Column family: hello family name is 'cf'.</span></span> <span data-ttu-id="126a9-156">As colunas armazenadas nesta família são:</span><span class="sxs-lookup"><span data-stu-id="126a9-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="126a9-157">evento: INICIAR ou ENCERRAR.</span><span class="sxs-lookup"><span data-stu-id="126a9-157">event: START or END.</span></span>

  * <span data-ttu-id="126a9-158">hora: tempo de saudação em milissegundos que Olá evento ocorreu.</span><span class="sxs-lookup"><span data-stu-id="126a9-158">time: hello time in milliseconds that hello event occurred.</span></span>

  * <span data-ttu-id="126a9-159">Duração: Olá comprimento entre eventos de início e término.</span><span class="sxs-lookup"><span data-stu-id="126a9-159">duration: hello length between START and END event.</span></span>

* <span data-ttu-id="126a9-160">VERSÕES: família de 'cf' hello é definida tooretain 5 versões de cada linha.</span><span class="sxs-lookup"><span data-stu-id="126a9-160">VERSIONS: hello 'cf' family is set tooretain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="126a9-161">As versões são um log dos valores anteriores armazenados para uma chave de linha específica.</span><span class="sxs-lookup"><span data-stu-id="126a9-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="126a9-162">Por padrão, HBase só retorna o valor Olá para a versão mais recente de saudação de uma linha.</span><span class="sxs-lookup"><span data-stu-id="126a9-162">By default, HBase only returns hello value for hello most recent version of a row.</span></span> <span data-ttu-id="126a9-163">Nesse caso, hello mesma linha é usada para todos os eventos (início, fim.) de que cada versão de uma linha é identificado pelo valor de carimbo de hora hello.</span><span class="sxs-lookup"><span data-stu-id="126a9-163">In this case, hello same row is used for all events (START, END.) each version of a row is identified by hello timestamp value.</span></span> <span data-ttu-id="126a9-164">As versões fornecem exibição do histórico de eventos registrados para uma ID específica.</span><span class="sxs-lookup"><span data-stu-id="126a9-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-hello-project"></a><span data-ttu-id="126a9-165">Baixe o projeto de saudação</span><span class="sxs-lookup"><span data-stu-id="126a9-165">Download hello project</span></span>

<span data-ttu-id="126a9-166">projeto de exemplo Hello pode ser baixado do [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span><span class="sxs-lookup"><span data-stu-id="126a9-166">hello sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="126a9-167">Este download contém Olá projetos c# a seguir:</span><span class="sxs-lookup"><span data-stu-id="126a9-167">This download contains hello following C# projects:</span></span>

* <span data-ttu-id="126a9-168">CorrelationTopology: topologia de Storm C# que emite aleatoriamente eventos de iniciar e encerrar para sessões de usuário.</span><span class="sxs-lookup"><span data-stu-id="126a9-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="126a9-169">Cada sessão dura entre 1 e 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="126a9-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="126a9-170">SessionInfo: Console aplicativo c# que cria a tabela do HBase hello e fornece exemplos de consultas tooreturn informações sobre os dados armazenados de sessão.</span><span class="sxs-lookup"><span data-stu-id="126a9-170">SessionInfo: C# console application that creates hello HBase table, and provides example queries tooreturn information about stored session data.</span></span>

## <a name="create-hello-table"></a><span data-ttu-id="126a9-171">Criar tabela Olá</span><span class="sxs-lookup"><span data-stu-id="126a9-171">Create hello table</span></span>

1. <span data-ttu-id="126a9-172">Olá abrir **SessionInfo** projeto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="126a9-172">Open hello **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="126a9-173">No **Solution Explorer**, Olá atalho **SessionInfo** do projeto e selecione **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="126a9-173">In **Solution Explorer**, right-click hello **SessionInfo** project and select **Properties**.</span></span>

    ![Captura de tela do menu com as propriedades selecionadas](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="126a9-175">Selecione **configurações**, então a saudação do conjunto de valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="126a9-175">Select **Settings**, then set hello following values:</span></span>

   * <span data-ttu-id="126a9-176">HBaseClusterURL: cluster Olá URL tooyour HBase.</span><span class="sxs-lookup"><span data-stu-id="126a9-176">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="126a9-177">Por exemplo, https://meuclusterhbase.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="126a9-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="126a9-178">HBaseClusterUserName: conta de usuário de administração/HTTP Olá para o cluster</span><span class="sxs-lookup"><span data-stu-id="126a9-178">HBaseClusterUserName: hello admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="126a9-179">HBaseClusterPassword: Olá senha Olá administrador/HTTP conta de usuário</span><span class="sxs-lookup"><span data-stu-id="126a9-179">HBaseClusterPassword: hello password for hello admin/HTTP user account</span></span>

   * <span data-ttu-id="126a9-180">HBaseTableName: nome de saudação do hello tabela toouse com este exemplo</span><span class="sxs-lookup"><span data-stu-id="126a9-180">HBaseTableName: hello name of hello table toouse with this example</span></span>

   * <span data-ttu-id="126a9-181">HBaseTableColumnFamily: nome da família Olá coluna</span><span class="sxs-lookup"><span data-stu-id="126a9-181">HBaseTableColumnFamily: hello column family name</span></span>

     ![Imagem da caixa de diálogo de configuração](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="126a9-183">Execute a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="126a9-183">Run hello solution.</span></span> <span data-ttu-id="126a9-184">Quando solicitado, selecione hello "c" toocreate chave Olá tabela cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="126a9-184">When prompted, select hello 'c' key toocreate hello table on your HBase cluster.</span></span>

## <a name="build-and-deploy-hello-storm-topology"></a><span data-ttu-id="126a9-185">Criar e implantar Olá Storm topologia</span><span class="sxs-lookup"><span data-stu-id="126a9-185">Build and deploy hello Storm topology</span></span>

1. <span data-ttu-id="126a9-186">Olá abrir **CorrelationTopology** solução no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="126a9-186">Open hello **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="126a9-187">Em **Solution Explorer**, Olá atalho **CorrelationTopology** do projeto e selecione Propriedades.</span><span class="sxs-lookup"><span data-stu-id="126a9-187">In **Solution Explorer**, right-click hello **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="126a9-188">Na janela de propriedades de saudação, selecione **configurações** e insira os valores de configuração de saudação para este projeto.</span><span class="sxs-lookup"><span data-stu-id="126a9-188">In hello properties window, select **Settings** and enter hello configuration values for this project.</span></span> <span data-ttu-id="126a9-189">5 primeiro Hello são Olá mesmos valores usados pelo Olá **SessionInfo** projeto:</span><span class="sxs-lookup"><span data-stu-id="126a9-189">hello first 5 are hello same values used by hello **SessionInfo** project:</span></span>

   * <span data-ttu-id="126a9-190">HBaseClusterURL: cluster Olá URL tooyour HBase.</span><span class="sxs-lookup"><span data-stu-id="126a9-190">HBaseClusterURL: hello URL tooyour HBase cluster.</span></span> <span data-ttu-id="126a9-191">Por exemplo, https://meuclusterhbase.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="126a9-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="126a9-192">HBaseClusterUserName: conta de usuário Olá administrador/HTTP para o cluster.</span><span class="sxs-lookup"><span data-stu-id="126a9-192">HBaseClusterUserName: hello admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="126a9-193">HBaseClusterPassword: Olá senha Olá administrador/HTTP conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="126a9-193">HBaseClusterPassword: hello password for hello admin/HTTP user account.</span></span>

   * <span data-ttu-id="126a9-194">HBaseTableName: o nome de saudação do hello tabela toouse com este exemplo.</span><span class="sxs-lookup"><span data-stu-id="126a9-194">HBaseTableName: hello name of hello table toouse with this example.</span></span> <span data-ttu-id="126a9-195">Esse valor é Olá mesmo nome de tabela como usado no projeto de SessionInfo hello.</span><span class="sxs-lookup"><span data-stu-id="126a9-195">This value is hello same table name as used in hello SessionInfo project.</span></span>

   * <span data-ttu-id="126a9-196">HBaseTableColumnFamily: nome de família da coluna Olá.</span><span class="sxs-lookup"><span data-stu-id="126a9-196">HBaseTableColumnFamily: hello column family name.</span></span> <span data-ttu-id="126a9-197">Esse valor é Olá a mesma coluna Nome da família como usado no projeto de SessionInfo hello.</span><span class="sxs-lookup"><span data-stu-id="126a9-197">This value is hello same column family name as used in hello SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="126a9-198">Não altere Olá HBaseTableColumnNames, como padrões de saudação são nomes Olá usados pelo **SessionInfo** tooretrieve dados.</span><span class="sxs-lookup"><span data-stu-id="126a9-198">Do not change hello HBaseTableColumnNames, as hello defaults are hello names used by **SessionInfo** tooretrieve data.</span></span>

4. <span data-ttu-id="126a9-199">Salvar as propriedades de saudação e compilar o projeto de saudação.</span><span class="sxs-lookup"><span data-stu-id="126a9-199">Save hello properties, then build hello project.</span></span>

5. <span data-ttu-id="126a9-200">Em **Solution Explorer**, clique com botão direito hello e selecione **enviar tooStorm no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="126a9-200">In **Solution Explorer**, right-click hello project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="126a9-201">Se solicitado, insira as credenciais de saudação para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="126a9-201">If prompted, enter hello credentials for your Azure subscription.</span></span>

   ![Imagem de saudação Enviar item de menu toostorm](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="126a9-203">Em Olá **topologia enviar** caixa de diálogo, o cluster Storm de saudação selecione deseja toodeploy essa topologia para.</span><span class="sxs-lookup"><span data-stu-id="126a9-203">In hello **Submit Topology** dialog, select hello Storm cluster you want toodeploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="126a9-204">Olá primeira vez que você enviar uma topologia, pode levar alguns segundos nome de saudação tooretrieve seus clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="126a9-204">hello first time you submit a topology, it may take a few seconds tooretrieve hello name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="126a9-205">Depois que a topologia Olá foi carregado e enviado toohello cluster, Olá **profusão de exibição de topologia** abre e exibe o saudação executando topologia.</span><span class="sxs-lookup"><span data-stu-id="126a9-205">Once hello topology has been uploaded and submitted toohello cluster, hello **Storm Topology View** opens and displays hello running topology.</span></span> <span data-ttu-id="126a9-206">dados de saudação toorefresh, selecione Olá **CorrelationTopology** e use o botão de atualização de saudação à saudação parte superior direita da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="126a9-206">toorefresh hello data, select hello **CorrelationTopology** and use hello refresh button at hello top right of hello page.</span></span>

   ![Imagem de exibição de topologia Olá](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="126a9-208">Quando a topologia Olá começa a geração de dados, Olá valor Olá **Emitted** incrementos de coluna.</span><span class="sxs-lookup"><span data-stu-id="126a9-208">When hello topology begins generating data, hello value in hello **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="126a9-209">Se hello **profusão de exibição de topologia** não abrir automaticamente, use Olá tooopen as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="126a9-209">If hello **Storm Topology View** does not open automatically, use hello following steps tooopen it:</span></span>
   >
   > 1. <span data-ttu-id="126a9-210">No **Gerenciador de Soluções**, expanda **Azure** e **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="126a9-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="126a9-211">Cluster Storm do botão direito do mouse Olá que Olá topologia está em execução no e, em seguida, selecione **topologias de profusão de exibição**</span><span class="sxs-lookup"><span data-stu-id="126a9-211">Right-click hello Storm cluster that hello topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-hello-data"></a><span data-ttu-id="126a9-212">Consultar dados Olá</span><span class="sxs-lookup"><span data-stu-id="126a9-212">Query hello data</span></span>

<span data-ttu-id="126a9-213">Depois de dados foi emitidos, use Olá seguintes etapas tooquery Olá dados.</span><span class="sxs-lookup"><span data-stu-id="126a9-213">Once data has been emitted, use hello following steps tooquery hello data.</span></span>

1. <span data-ttu-id="126a9-214">Retornar toohello **SessionInfo** projeto.</span><span class="sxs-lookup"><span data-stu-id="126a9-214">Return toohello **SessionInfo** project.</span></span> <span data-ttu-id="126a9-215">Se não estiver executando, inicie uma nova instância dele.</span><span class="sxs-lookup"><span data-stu-id="126a9-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="126a9-216">Quando solicitado, selecione **s** toosearch para o início do evento.</span><span class="sxs-lookup"><span data-stu-id="126a9-216">When prompted, select **s** toosearch for START event.</span></span> <span data-ttu-id="126a9-217">São solicitada tooenter um início e término tempo toodefine um intervalo de tempo - serão retornados somente eventos entre essas duas vezes.</span><span class="sxs-lookup"><span data-stu-id="126a9-217">You are prompted tooenter a start and end time toodefine a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="126a9-218">Ao inserir o início de saudação de formato e de término da seguinte de saudação de uso: hh: mm e 'm'' ou 'pm'.</span><span class="sxs-lookup"><span data-stu-id="126a9-218">Use hello following format when entering hello start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="126a9-219">Por exemplo, 11:20pm.</span><span class="sxs-lookup"><span data-stu-id="126a9-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="126a9-220">eventos tooreturn conectado, use uma hora de início do antes de saudação profusão de topologia foi implantada e uma hora de término da agora.</span><span class="sxs-lookup"><span data-stu-id="126a9-220">tooreturn logged events, use a start time from before hello Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="126a9-221">dados de retorno Olá contém entradas toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="126a9-221">hello return data contains entries similar toohello following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="126a9-222">Procurando saudação do fim eventos funciona mesmo como eventos de início.</span><span class="sxs-lookup"><span data-stu-id="126a9-222">Searching for END events works hello same as START events.</span></span> <span data-ttu-id="126a9-223">No entanto, eventos de término são gerados aleatoriamente entre 1 e 5 minutos após o início do evento hello.</span><span class="sxs-lookup"><span data-stu-id="126a9-223">However, END events are generated randomly between 1 and 5 minutes after hello START event.</span></span> <span data-ttu-id="126a9-224">Você pode ter tootry alguns intervalos toofind Olá final eventos.</span><span class="sxs-lookup"><span data-stu-id="126a9-224">You may have tootry a few time ranges toofind hello END events.</span></span> <span data-ttu-id="126a9-225">Eventos de término também contêm durante Olá Olá sessão - diferença Olá entre a hora de evento Olá início e término do evento.</span><span class="sxs-lookup"><span data-stu-id="126a9-225">END events also contain hello duration of hello session - hello difference between hello START event time and END event time.</span></span> <span data-ttu-id="126a9-226">Veja um exemplo de dados para eventos ENCERRAR:</span><span class="sxs-lookup"><span data-stu-id="126a9-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="126a9-227">Enquanto os valores de tempo de saudação que inserir estão no horário local, tempo de saudação retornado da consulta hello está em UTC.</span><span class="sxs-lookup"><span data-stu-id="126a9-227">While hello time values you enter are in local time, hello time returned from hello query is in UTC.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="126a9-228">Parar a topologia de saudação</span><span class="sxs-lookup"><span data-stu-id="126a9-228">Stop hello topology</span></span>

<span data-ttu-id="126a9-229">Quando você estiver pronto toostop topologia de hello, retornar toohello **CorrelationTopology** projeto no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="126a9-229">When you are ready toostop hello topology, return toohello **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="126a9-230">Em Olá **profusão de exibição de topologia**, selecione a topologia de saudação e, em seguida, use Olá **Kill** botão na parte superior de saudação do modo de exibição de topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="126a9-230">In hello **Storm Topology View**, select hello topology and then use hello **Kill** button at hello top of hello topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="126a9-231">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="126a9-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="126a9-232">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="126a9-232">Next steps</span></span>

<span data-ttu-id="126a9-233">Para obter mais exemplos de topologias Storm, consulte [Exemplo de topologias para Storm no HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="126a9-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
