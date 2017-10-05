---
title: Correlacionar eventos ao longo do tempo com o Storm e o HBase no HDInsight
description: Saiba como correlacionar eventos que chegam em momentos diferentes usando o Storm e HBase no HDInsight.
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
ms.openlocfilehash: 06630096383601e48e8f69f8553314cee42f5f3e
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a><span data-ttu-id="0ef8c-103">Correlacionar eventos que chegam em diferentes horários usando Storm e o HBase</span><span class="sxs-lookup"><span data-stu-id="0ef8c-103">Correlate events that arrive at different times using Storm and HBase</span></span>

<span data-ttu-id="0ef8c-104">Usando um armazenamento de dados persistentes com o Apache Storm, você pode correlacionar as entradas de dados que chegam em momentos diferentes.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-104">By using a persistent data store with Apache Storm, you can correlate data entries that arrive at different times.</span></span> <span data-ttu-id="0ef8c-105">Por exemplo, vincular eventos de logon e logoff de uma sessão de usuário para calcular quanto tempo durou a sessão.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-105">For example, linking login and logout events for a user session to calculate how long the session lasted.</span></span>

<span data-ttu-id="0ef8c-106">Neste documento, você aprenderá como criar uma topologia Storm C# básica que rastreie eventos de logon e logoff de sessões de usuário e calcule a duração da sessão.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-106">In this document, you learn how to create a basic C# Storm topology that tracks login and logout events for user sessions, and calculates the duration of the session.</span></span> <span data-ttu-id="0ef8c-107">A topologia usa HBase como um repositório de dados persistentes.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-107">The topology uses HBase as a persistent data store.</span></span> <span data-ttu-id="0ef8c-108">O HBase também permite que você execute consultas de lote nos dados históricos para produzir informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-108">HBase also allows you to perform batch queries on the historical data to produce additional insights.</span></span> <span data-ttu-id="0ef8c-109">Por exemplo, quantas sessões de usuário foram iniciadas ou encerradas durante um período de tempo específico.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-109">For example, how many user sessions were started or ended during a specific time period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0ef8c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0ef8c-110">Prerequisites</span></span>

* <span data-ttu-id="0ef8c-111">O Visual Studio e as ferramentas do HDInsight para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-111">Visual Studio and the HDInsight tools for Visual Studio.</span></span> <span data-ttu-id="0ef8c-112">Para obter mais informações, consulte [Introdução ao uso das ferramentas do HDInsight para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0ef8c-112">For more information, see [Get started using the HDInsight tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

* <span data-ttu-id="0ef8c-113">Apache Storm em cluster HDInsight (baseado em Windows).</span><span class="sxs-lookup"><span data-stu-id="0ef8c-113">Apache Storm on HDInsight cluster (Windows-based).</span></span>

  > [!WARNING]
  > <span data-ttu-id="0ef8c-114">Embora as topologias SCP.NET tenham suporte em clusters Storm baseados em Linux criados após 28/10/2016, o pacote SDK do HBase para .NET disponível a partir de 28/10/2016 não funciona corretamente no HDInsight baseado em Linux</span><span class="sxs-lookup"><span data-stu-id="0ef8c-114">While SCP.NET topologies are supported on Linux-based Storm clusters created after 10/28/2016, the HBase SDK for .NET package available as of 10/28/2016 does not work correctly on Linux-based HDInsight</span></span>

* <span data-ttu-id="0ef8c-115">Apache HBase no cluster HDInsight (baseado em Linux ou Windows).</span><span class="sxs-lookup"><span data-stu-id="0ef8c-115">Apache HBase on HDInsight cluster (Linux or Windows-based).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="0ef8c-116">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-116">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="0ef8c-117">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="0ef8c-117">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="0ef8c-118">[Java](https://java.com) 1.7 ou posterior em seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-118">[Java](https://java.com) 1.7 or greater on your development environment.</span></span> <span data-ttu-id="0ef8c-119">O Java é usado para o pacote da topologia quando ela é enviada ao cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-119">Java is used to package the topology when it is submitted to the HDInsight cluster.</span></span>

  * <span data-ttu-id="0ef8c-120">A variável de ambiente **JAVA_HOME** deve apontar ao diretório que contém o Java.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-120">The **JAVA_HOME** environment variable must point to the directory that contains Java.</span></span>
  * <span data-ttu-id="0ef8c-121">O diretório **%JAVA_HOME%/bin** deve estar no caminho</span><span class="sxs-lookup"><span data-stu-id="0ef8c-121">The **%JAVA_HOME%/bin** directory must be in the path</span></span>

## <a name="architecture"></a><span data-ttu-id="0ef8c-122">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="0ef8c-122">Architecture</span></span>

![Diagrama do fluxo de dados por meio da topologia](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

<span data-ttu-id="0ef8c-124">A correlação de eventos requer um identificador comum para a origem do evento.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-124">Correlating events requires a common identifier for the event source.</span></span> <span data-ttu-id="0ef8c-125">Por exemplo, uma ID de usuário, ID de sessão ou outra parte dos dados que seja a) exclusiva e b) incluída em todos os dados enviados ao Storm.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-125">For example, a user ID, session ID, or other piece of data that is a) unique and b) included in all data sent to Storm.</span></span> <span data-ttu-id="0ef8c-126">Este exemplo usa um valor de GUID para representar uma ID de sessão.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-126">This example uses a GUID value to represent a session ID.</span></span>

<span data-ttu-id="0ef8c-127">Esse exemplo consiste em dois clusters HDInsight:</span><span class="sxs-lookup"><span data-stu-id="0ef8c-127">This example consists of two HDInsight clusters:</span></span>

* <span data-ttu-id="0ef8c-128">HBase: repositório de dados persistente dados históricos</span><span class="sxs-lookup"><span data-stu-id="0ef8c-128">HBase: persistent data store for historical data</span></span>
* <span data-ttu-id="0ef8c-129">Storm: usado para incluir dados de entrada</span><span class="sxs-lookup"><span data-stu-id="0ef8c-129">Storm: used to ingest incoming data</span></span>

<span data-ttu-id="0ef8c-130">Os dados são gerados aleatoriamente, pelo Storm e contém dos seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="0ef8c-130">The data is randomly generated by the Storm topology, and consists of the following items:</span></span>

* <span data-ttu-id="0ef8c-131">ID da sessão: um GUID que identifica exclusivamente cada sessão</span><span class="sxs-lookup"><span data-stu-id="0ef8c-131">Session ID: a GUID that uniquely identifies each session</span></span>
* <span data-ttu-id="0ef8c-132">Evento: um evento INICIAR ou ENCERRAR.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-132">Event: a START or END event.</span></span> <span data-ttu-id="0ef8c-133">Para este exemplo, INICIAR sempre ocorre antes do ENCERRAR</span><span class="sxs-lookup"><span data-stu-id="0ef8c-133">For this example, START always occurs before END</span></span>
* <span data-ttu-id="0ef8c-134">Hora: a hora do evento.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-134">Time: the time of the event.</span></span>

<span data-ttu-id="0ef8c-135">Esses dados são processados e armazenados no HBase.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-135">This data is processed and stored in HBase.</span></span>

### <a name="storm-topology"></a><span data-ttu-id="0ef8c-136">Topologia Storm</span><span class="sxs-lookup"><span data-stu-id="0ef8c-136">Storm topology</span></span>

<span data-ttu-id="0ef8c-137">Quando uma sessão é iniciada, um evento **INICIAR** é recebido pela topologia e registrado no HBase.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-137">When a session starts, a **START** event is received by the topology and logged to HBase.</span></span> <span data-ttu-id="0ef8c-138">Quando um evento **ENCERRAR** é recebido, a topologia recupera o evento **INICIAR** e calcula o tempo entre os dois eventos.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-138">When an **END** event is received, the topology retrieves the **START** event and calculates the time between the two events.</span></span> <span data-ttu-id="0ef8c-139">Esse valor **Duração** é armazenado no HBase com as informações do evento **ENCERRAR**.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-139">This **Duration** value is then stored in HBase along with the **END** event information.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0ef8c-140">Enquanto essa topologia demonstra o padrão básico, uma solução de produção precisaria fazer o design para os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="0ef8c-140">While this topology demonstrates the basic pattern, a production solution would need to take design for the following scenarios:</span></span>
>
> * <span data-ttu-id="0ef8c-141">Eventos que chegam fora de ordem</span><span class="sxs-lookup"><span data-stu-id="0ef8c-141">Events arriving out of order</span></span>
> * <span data-ttu-id="0ef8c-142">Eventos duplicados</span><span class="sxs-lookup"><span data-stu-id="0ef8c-142">Duplicate events</span></span>
> * <span data-ttu-id="0ef8c-143">Eventos ignorados</span><span class="sxs-lookup"><span data-stu-id="0ef8c-143">Dropped events</span></span>

<span data-ttu-id="0ef8c-144">A topologia de exemplo é composta dos seguintes componentes:</span><span class="sxs-lookup"><span data-stu-id="0ef8c-144">The sample topology is composed of the following components:</span></span>

* <span data-ttu-id="0ef8c-145">Session.cs: simula uma sessão de usuário criando uma ID de sessão aleatória, hora de início e por quanto tempo durará a sessão.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-145">Session.cs: simulates a user session by creating a random session ID, start time, and how long the session lasts.</span></span>

* <span data-ttu-id="0ef8c-146">Spout.cs: cria 100 sessões, emite um evento START, aguarda o tempo limite aleatório para cada sessão e emite um evento END.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-146">Spout.cs: creates 100 sessions, emits a START event, waits the random timeout for each session, and then emits an END event.</span></span> <span data-ttu-id="0ef8c-147">Em seguida, recicla as sessões encerradas para gerar novas.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-147">Then recycles ended sessions to generate new ones.</span></span>

* <span data-ttu-id="0ef8c-148">HBaseLookupBolt.cs: usa a ID de sessão para pesquisar informações de sessão do HBase.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-148">HBaseLookupBolt.cs: uses the session ID to look up session information from HBase.</span></span> <span data-ttu-id="0ef8c-149">Quando um evento ENCERRAR é processado, ele localiza o evento INICIAR correspondente e calcula a duração da sessão.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-149">When an END event is processed, it finds the corresponding START event and calculates the duration of the session.</span></span>

* <span data-ttu-id="0ef8c-150">HBaseBolt.cs: Armazena informações no HBase.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-150">HBaseBolt.cs: Stores information into HBase.</span></span>

* <span data-ttu-id="0ef8c-151">TypeHelper.cs: ajuda na conversão de tipo ao ler/gravar no HBase.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-151">TypeHelper.cs: Helps with type conversion when reading from/writing to HBase.</span></span>

### <a name="hbase-schema"></a><span data-ttu-id="0ef8c-152">Esquema do HBase</span><span class="sxs-lookup"><span data-stu-id="0ef8c-152">HBase schema</span></span>

<span data-ttu-id="0ef8c-153">No HBase, os dados são armazenados em uma tabela com os seguintes esquema/configurações:</span><span class="sxs-lookup"><span data-stu-id="0ef8c-153">In HBase, the data is stored in a table with the following schema/settings:</span></span>

* <span data-ttu-id="0ef8c-154">Chave de linha: a ID da sessão é usada como a chave para linhas nesta tabela.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-154">Row key: the session ID is used as the key for rows in this table.</span></span>

* <span data-ttu-id="0ef8c-155">Família de coluna: o nome da família é “cf”.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-155">Column family: the family name is 'cf'.</span></span> <span data-ttu-id="0ef8c-156">As colunas armazenadas nesta família são:</span><span class="sxs-lookup"><span data-stu-id="0ef8c-156">Columns stored in this family are:</span></span>

  * <span data-ttu-id="0ef8c-157">evento: INICIAR ou ENCERRAR.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-157">event: START or END.</span></span>

  * <span data-ttu-id="0ef8c-158">tempo: o tempo em milissegundos durante o qual o evento ocorreu.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-158">time: the time in milliseconds that the event occurred.</span></span>

  * <span data-ttu-id="0ef8c-159">duração: o comprimento entre eventos INICIAR e ENCERRAR.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-159">duration: the length between START and END event.</span></span>

* <span data-ttu-id="0ef8c-160">VERSÕES: a família 'cf' é definida para reter cinco versões de cada linha.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-160">VERSIONS: the 'cf' family is set to retain 5 versions of each row.</span></span>

  > [!NOTE]
  > <span data-ttu-id="0ef8c-161">As versões são um log dos valores anteriores armazenados para uma chave de linha específica.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-161">Versions are a log of previous values stored for a specific row key.</span></span> <span data-ttu-id="0ef8c-162">Por padrão, o HBase retorna apenas o valor para a versão mais recente de uma linha.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-162">By default, HBase only returns the value for the most recent version of a row.</span></span> <span data-ttu-id="0ef8c-163">Nesse caso, a mesma linha é usada para todos os eventos (INICIAR, ENCERRAR) por que cada versão de uma linha é identificada pelo valor de carimbo de data e hora.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-163">In this case, the same row is used for all events (START, END.) each version of a row is identified by the timestamp value.</span></span> <span data-ttu-id="0ef8c-164">As versões fornecem exibição do histórico de eventos registrados para uma ID específica.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-164">Versions provide a historical view of events logged for a specific ID.</span></span>

## <a name="download-the-project"></a><span data-ttu-id="0ef8c-165">Baixe o projeto</span><span class="sxs-lookup"><span data-stu-id="0ef8c-165">Download the project</span></span>

<span data-ttu-id="0ef8c-166">O projeto de exemplo pode ser baixado de [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span><span class="sxs-lookup"><span data-stu-id="0ef8c-166">The sample project can be downloaded from [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).</span></span>

<span data-ttu-id="0ef8c-167">Este download contém os seguintes projetos C#:</span><span class="sxs-lookup"><span data-stu-id="0ef8c-167">This download contains the following C# projects:</span></span>

* <span data-ttu-id="0ef8c-168">CorrelationTopology: topologia de Storm C# que emite aleatoriamente eventos de iniciar e encerrar para sessões de usuário.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-168">CorrelationTopology: C# Storm topology that randomly emits start and end events for user sessions.</span></span> <span data-ttu-id="0ef8c-169">Cada sessão dura entre 1 e 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-169">Each session lasts between 1 and 5 minutes.</span></span>

* <span data-ttu-id="0ef8c-170">SessionInfo: aplicativo do console C# que cria a tabela de HBase e fornece consultas de exemplo para retornar informações sobre dados de sessão armazenados.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-170">SessionInfo: C# console application that creates the HBase table, and provides example queries to return information about stored session data.</span></span>

## <a name="create-the-table"></a><span data-ttu-id="0ef8c-171">Criar a tabela.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-171">Create the table</span></span>

1. <span data-ttu-id="0ef8c-172">Abra o projeto **SessionInfo** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-172">Open the **SessionInfo** project in Visual Studio.</span></span>

2. <span data-ttu-id="0ef8c-173">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **SessionInfo** e selecione **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-173">In **Solution Explorer**, right-click the **SessionInfo** project and select **Properties**.</span></span>

    ![Captura de tela do menu com as propriedades selecionadas](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. <span data-ttu-id="0ef8c-175">Selecione **configurações**e defina os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="0ef8c-175">Select **Settings**, then set the following values:</span></span>

   * <span data-ttu-id="0ef8c-176">HBaseClusterURL: a URL para o cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-176">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="0ef8c-177">Por exemplo, https://meuclusterhbase.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-177">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="0ef8c-178">HBaseClusterUserName: a conta de usuário de admin/HTTP para o cluster</span><span class="sxs-lookup"><span data-stu-id="0ef8c-178">HBaseClusterUserName: the admin/HTTP user account for your cluster</span></span>

   * <span data-ttu-id="0ef8c-179">HBaseClusterPassword: a senha para a conta de usuário admin/HTTP</span><span class="sxs-lookup"><span data-stu-id="0ef8c-179">HBaseClusterPassword: the password for the admin/HTTP user account</span></span>

   * <span data-ttu-id="0ef8c-180">HBaseTableName: o nome da tabela a ser usada com este exemplo</span><span class="sxs-lookup"><span data-stu-id="0ef8c-180">HBaseTableName: the name of the table to use with this example</span></span>

   * <span data-ttu-id="0ef8c-181">HBaseTableColumnFamily: o nome da família de coluna</span><span class="sxs-lookup"><span data-stu-id="0ef8c-181">HBaseTableColumnFamily: The column family name</span></span>

     ![Imagem da caixa de diálogo de configuração](./media/hdinsight-storm-correlation-topology/settings.png)

4. <span data-ttu-id="0ef8c-183">Execute a solução.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-183">Run the solution.</span></span> <span data-ttu-id="0ef8c-184">Quando solicitado, selecione a chave "c" para criar a tabela no cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-184">When prompted, select the 'c' key to create the table on your HBase cluster.</span></span>

## <a name="build-and-deploy-the-storm-topology"></a><span data-ttu-id="0ef8c-185">Criar e implantar a topologia Storm</span><span class="sxs-lookup"><span data-stu-id="0ef8c-185">Build and deploy the Storm topology</span></span>

1. <span data-ttu-id="0ef8c-186">Abra a solução **CorrelationTopology** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-186">Open the **CorrelationTopology** solution in Visual Studio.</span></span>

2. <span data-ttu-id="0ef8c-187">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **CorrelationTopology** e selecione Propriedades.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-187">In **Solution Explorer**, right-click the **CorrelationTopology** project and select properties.</span></span>

3. <span data-ttu-id="0ef8c-188">Na janela Propriedades, selecione **Configurações** e insira os valores de configuração para este projeto.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-188">In the properties window, select **Settings** and enter the configuration values for this project.</span></span> <span data-ttu-id="0ef8c-189">Os cinco primeiros são os mesmos valores usados pelo projeto **SessionInfo**:</span><span class="sxs-lookup"><span data-stu-id="0ef8c-189">The first 5 are the same values used by the **SessionInfo** project:</span></span>

   * <span data-ttu-id="0ef8c-190">HBaseClusterURL: a URL para o cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-190">HBaseClusterURL: the URL to your HBase cluster.</span></span> <span data-ttu-id="0ef8c-191">Por exemplo, https://meuclusterhbase.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-191">For example, https://myhbasecluster.azurehdinsight.net.</span></span>

   * <span data-ttu-id="0ef8c-192">HBaseClusterUserName: a conta de usuário de admin/HTTP para o cluster.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-192">HBaseClusterUserName: the admin/HTTP user account for your cluster.</span></span>

   * <span data-ttu-id="0ef8c-193">HBaseClusterPassword: a senha para a conta de usuário admin/HTTP.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-193">HBaseClusterPassword: the password for the admin/HTTP user account.</span></span>

   * <span data-ttu-id="0ef8c-194">HBaseTableName: o nome da tabela a ser usada com este exemplo.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-194">HBaseTableName: the name of the table to use with this example.</span></span> <span data-ttu-id="0ef8c-195">Esse valor deve conter o mesmo nome de tabela usado no projeto SessionInfo.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-195">This value is the same table name as used in the SessionInfo project.</span></span>

   * <span data-ttu-id="0ef8c-196">HBaseTableColumnFamily: o nome da família de coluna.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-196">HBaseTableColumnFamily: The column family name.</span></span> <span data-ttu-id="0ef8c-197">Esse valor deve conter o mesmo nome de família de colunas usado no projeto SessionInfo.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-197">This value is the same column family name as used in the SessionInfo project.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0ef8c-198">Não altere HBaseTableColumnNames, pois os padrões são os nomes usados por **SessionInfo** para recuperar dados.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-198">Do not change the HBaseTableColumnNames, as the defaults are the names used by **SessionInfo** to retrieve data.</span></span>

4. <span data-ttu-id="0ef8c-199">Salvar as propriedades e compilar o projeto.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-199">Save the properties, then build the project.</span></span>

5. <span data-ttu-id="0ef8c-200">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto e selecione **Enviar para o Storm no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-200">In **Solution Explorer**, right-click the project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="0ef8c-201">Se solicitado, insira as credenciais de logon para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-201">If prompted, enter the credentials for your Azure subscription.</span></span>

   ![Imagem do item de menu enviar para o storm](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. <span data-ttu-id="0ef8c-203">Na caixa de diálogo **Enviar Topologia**, selecione o cluster Storm no qual você deseja implantar essa topologia.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-203">In the **Submit Topology** dialog, select the Storm cluster you want to deploy this topology to.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0ef8c-204">Na primeira vez que você enviar uma topologia, pode levar alguns segundos para recuperar o nome do seus clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-204">The first time you submit a topology, it may take a few seconds to retrieve the name of your HDInsight clusters.</span></span>

7. <span data-ttu-id="0ef8c-205">Depois que a topologia for carregada e enviada para o cluster, a **Visualização da Topologia Storm** será aberta e exibirá a topologia em execução.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-205">Once the topology has been uploaded and submitted to the cluster, the **Storm Topology View** opens and displays the running topology.</span></span> <span data-ttu-id="0ef8c-206">Para atualizar os dados, selecione o **CorrelationTopology** e use o botão Atualizar na parte superior direita da página.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-206">To refresh the data, select the **CorrelationTopology** and use the refresh button at the top right of the page.</span></span>

   ![Imagem da visualização da topologia](./media/hdinsight-storm-correlation-topology/topologyview.png)

   <span data-ttu-id="0ef8c-208">Quando a topologia começar a gerar dados, o valor da coluna **Emitido** será incrementado.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-208">When the topology begins generating data, the value in the **Emitted** column increments.</span></span>

   > [!NOTE]
   > <span data-ttu-id="0ef8c-209">Se a **Visualização da topologia Storm** não abrir automaticamente, use as seguintes etapas para abri-la:</span><span class="sxs-lookup"><span data-stu-id="0ef8c-209">If the **Storm Topology View** does not open automatically, use the following steps to open it:</span></span>
   >
   > 1. <span data-ttu-id="0ef8c-210">No **Gerenciador de Soluções**, expanda **Azure** e **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-210">In **Solution Explorer**, expand **Azure**, and then expand **HDInsight**.</span></span>
   > 2. <span data-ttu-id="0ef8c-211">Clique com o botão direito do mouse no cluster Storm em que a topologia está em execução e selecione **Exibir topologias Storm**</span><span class="sxs-lookup"><span data-stu-id="0ef8c-211">Right-click the Storm cluster that the topology is running on, and then select **View Storm Topologies**</span></span>

## <a name="query-the-data"></a><span data-ttu-id="0ef8c-212">Consultar os dados</span><span class="sxs-lookup"><span data-stu-id="0ef8c-212">Query the data</span></span>

<span data-ttu-id="0ef8c-213">Depois que os dados forem emitidos, use as seguintes etapas para consultar os dados.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-213">Once data has been emitted, use the following steps to query the data.</span></span>

1. <span data-ttu-id="0ef8c-214">Volte para o projeto **SessionInfo** .</span><span class="sxs-lookup"><span data-stu-id="0ef8c-214">Return to the **SessionInfo** project.</span></span> <span data-ttu-id="0ef8c-215">Se não estiver executando, inicie uma nova instância dele.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-215">If not running, start a new instance of it.</span></span>

2. <span data-ttu-id="0ef8c-216">Quando solicitado, selecione **s** para pesquisar pelo evento INICIAR.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-216">When prompted, select **s** to search for START event.</span></span> <span data-ttu-id="0ef8c-217">Você será solicitado a inserir uma hora de início e encerramento para definir um intervalo de tempo; apenas os eventos entre essas duas horas serão retornados.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-217">You are prompted to enter a start and end time to define a time range - only events between these two times are returned.</span></span>

    <span data-ttu-id="0ef8c-218">Use o seguinte formato ao inserir as horas de início e encerramento: HH:MM e “am” ou “pm”.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-218">Use the following format when entering the start and end times: HH:MM and 'am' or 'pm'.</span></span> <span data-ttu-id="0ef8c-219">Por exemplo, 11:20pm.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-219">For example, 11:20pm.</span></span>

    <span data-ttu-id="0ef8c-220">Para retornar eventos registrados em log, use uma hora de início anterior à implantação da topologia do Storm e uma hora de encerramento equivalente ao horário atual.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-220">To return logged events, use a start time from before the Storm topology was deployed, and an end time of now.</span></span> <span data-ttu-id="0ef8c-221">Os dados retornados contêm entradas semelhantes ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="0ef8c-221">The return data contains entries similar to the following text:</span></span>

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

<span data-ttu-id="0ef8c-222">A busca por eventos ENCERRAR funciona da mesma maneira que os eventos INICIAR.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-222">Searching for END events works the same as START events.</span></span> <span data-ttu-id="0ef8c-223">No entanto, os eventos ENCERRAR são gerados aleatoriamente entre 1 e 5 minutos após o evento INICIAR.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-223">However, END events are generated randomly between 1 and 5 minutes after the START event.</span></span> <span data-ttu-id="0ef8c-224">Você terá que experimentar alguns intervalos de tempo para encontrar os eventos ENCERRAR.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-224">You may have to try a few time ranges to find the END events.</span></span> <span data-ttu-id="0ef8c-225">Os eventos ENCERRAR também contêm a duração da sessão; a diferença entre a hora do evento INICIAR e do evento ENCERRAR.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-225">END events also contain the duration of the session - the difference between the START event time and END event time.</span></span> <span data-ttu-id="0ef8c-226">Veja um exemplo de dados para eventos ENCERRAR:</span><span class="sxs-lookup"><span data-stu-id="0ef8c-226">Here is an example of data for END events:</span></span>

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> <span data-ttu-id="0ef8c-227">Embora os valores de hora que você insere estão na hora local, a hora retornada da consulta será em UTC.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-227">While the time values you enter are in local time, the time returned from the query is in UTC.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="0ef8c-228">Parar a topologia</span><span class="sxs-lookup"><span data-stu-id="0ef8c-228">Stop the topology</span></span>

<span data-ttu-id="0ef8c-229">Quando você estiver pronto para parar a topologia, volte para o projeto **CorrelationTopology** no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-229">When you are ready to stop the topology, return to the **CorrelationTopology** project in Visual Studio.</span></span> <span data-ttu-id="0ef8c-230">Na **Exibição da Topologia Storm**, selecione a topologia e use o botão **Eliminar** na parte superior da exibição da topologia.</span><span class="sxs-lookup"><span data-stu-id="0ef8c-230">In the **Storm Topology View**, select the topology and then use the **Kill** button at the top of the topology view.</span></span>

## <a name="delete-your-cluster"></a><span data-ttu-id="0ef8c-231">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="0ef8c-231">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="0ef8c-232">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0ef8c-232">Next steps</span></span>

<span data-ttu-id="0ef8c-233">Para obter mais exemplos de topologias Storm, consulte [Exemplo de topologias para Storm no HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="0ef8c-233">For more Storm examples, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md).</span></span>
