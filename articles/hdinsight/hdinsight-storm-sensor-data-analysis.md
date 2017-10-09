---
title: dados de sensor aaaAnalyze com Apache Storm e HBase | Microsoft Docs
description: "Saiba como tooconnect tooApache Storm com uma rede virtual. Use Storm com dados de sensor do HBase tooprocess de um hub de eventos e visualizá-la com D3.js."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a><span data-ttu-id="4aa71-104">Analisar dados de sensor com o Apache Storm e com o HBase no HDInsight (Hadoop)</span><span class="sxs-lookup"><span data-stu-id="4aa71-104">Analyze sensor data with Apache Storm, Event Hub, and HBase in HDInsight (Hadoop)</span></span>

<span data-ttu-id="4aa71-105">Saiba como toouse Apache Storm no HDInsight tooprocess os dados do sensor de Hub de eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa71-105">Learn how toouse Apache Storm on HDInsight tooprocess sensor data from Azure Event Hub.</span></span> <span data-ttu-id="4aa71-106">Olá dados são armazenados no Apache HBase em HDInsight e visualizado usando D3.js.</span><span class="sxs-lookup"><span data-stu-id="4aa71-106">hello data is then stored into Apache HBase on HDInsight, and visualized using D3.js.</span></span>

<span data-ttu-id="4aa71-107">saudação do Azure Resource Manager modelo usada neste documento demonstra como toocreate vários recursos do Azure em um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4aa71-107">hello Azure Resource Manager template used in this document demonstrates how toocreate multiple Azure resources in a resource group.</span></span> <span data-ttu-id="4aa71-108">modelo de saudação cria uma rede Virtual do Azure, dois clusters de HDInsight (Storm e HBase) e um aplicativo Web do Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa71-108">hello template creates an Azure Virtual Network, two HDInsight clusters (Storm and HBase) and an Azure Web App.</span></span> <span data-ttu-id="4aa71-109">Uma implementação de Node. js de um painel da web em tempo real é implantado automaticamente toohello web app.</span><span class="sxs-lookup"><span data-stu-id="4aa71-109">A node.js implementation of a real-time web dashboard is automatically deployed toohello web app.</span></span>

> [!NOTE]
> <span data-ttu-id="4aa71-110">informações de saudação neste documento e o exemplo neste documento exigem HDInsight versão 3.6.</span><span class="sxs-lookup"><span data-stu-id="4aa71-110">hello information in this document and example in this document require HDInsight version 3.6.</span></span>
>
> <span data-ttu-id="4aa71-111">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="4aa71-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="4aa71-112">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="4aa71-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4aa71-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="4aa71-113">Prerequisites</span></span>

* <span data-ttu-id="4aa71-114">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="4aa71-114">An Azure subscription.</span></span>
* <span data-ttu-id="4aa71-115">[Node. js](http://nodejs.org/): painel de web hello toopreview usados localmente no seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="4aa71-115">[Node.js](http://nodejs.org/): Used toopreview hello web dashboard locally on your development environment.</span></span>
* <span data-ttu-id="4aa71-116">[Java e hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): usado toodevelop topologia de profusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aa71-116">[Java and hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): Used toodevelop hello Storm topology.</span></span>
* <span data-ttu-id="4aa71-117">[Maven](http://maven.apache.org/what-is-maven.html): projeto de saudação toobuild e compilação usado.</span><span class="sxs-lookup"><span data-stu-id="4aa71-117">[Maven](http://maven.apache.org/what-is-maven.html): Used toobuild and compile hello project.</span></span>
* <span data-ttu-id="4aa71-118">[Git](http://git-scm.com/): projeto de saudação toodownload usado do GitHub.</span><span class="sxs-lookup"><span data-stu-id="4aa71-118">[Git](http://git-scm.com/): Used toodownload hello project from GitHub.</span></span>
* <span data-ttu-id="4aa71-119">Um **SSH** cliente: clusters de HDInsight baseados em Linux toohello tooconnect usados.</span><span class="sxs-lookup"><span data-stu-id="4aa71-119">An **SSH** client: Used tooconnect toohello Linux-based HDInsight clusters.</span></span> <span data-ttu-id="4aa71-120">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4aa71-120">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>


> [!IMPORTANT]
> <span data-ttu-id="4aa71-121">Não é necessário um cluster HDInsight existente.</span><span class="sxs-lookup"><span data-stu-id="4aa71-121">You do not need an existing HDInsight cluster.</span></span> <span data-ttu-id="4aa71-122">Olá etapas neste documento para criar hello recursos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-122">hello steps in this document create hello following resources:</span></span>
> 
> * <span data-ttu-id="4aa71-123">Uma Rede virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="4aa71-123">An Azure Virtual Network</span></span>
> * <span data-ttu-id="4aa71-124">Um cluster Storm no HDInsight (baseado em Linux, dois nós de trabalho)</span><span class="sxs-lookup"><span data-stu-id="4aa71-124">A Storm on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="4aa71-125">Um cluster HBase no HDInsight (baseado em Linux, dois nós de trabalho)</span><span class="sxs-lookup"><span data-stu-id="4aa71-125">An HBase on HDInsight cluster (Linux-based, two worker nodes)</span></span>
> * <span data-ttu-id="4aa71-126">Um aplicativo Web do Azure que hospeda o painel da web de saudação</span><span class="sxs-lookup"><span data-stu-id="4aa71-126">An Azure Web App that hosts hello web dashboard</span></span>

## <a name="architecture"></a><span data-ttu-id="4aa71-127">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="4aa71-127">Architecture</span></span>

![diagrama da arquitetura](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

<span data-ttu-id="4aa71-129">Este exemplo consiste em Olá componentes a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-129">This example consists of hello following components:</span></span>

* <span data-ttu-id="4aa71-130">**Hub de Eventos do Azure**: contém os dados coletados dos sensores.</span><span class="sxs-lookup"><span data-stu-id="4aa71-130">**Azure Event Hubs**: Contains data that is collected from sensors.</span></span>
* <span data-ttu-id="4aa71-131">**Storm no HDInsight**: fornece processamento em tempo real dos dados do Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="4aa71-131">**Storm on HDInsight**: Provides real-time processing of data from Event Hub.</span></span>
* <span data-ttu-id="4aa71-132">**HBase no HDInsight**: fornece um armazenamento de dados NoSQL persistente para dados depois que eles são processados pelo Storm.</span><span class="sxs-lookup"><span data-stu-id="4aa71-132">**HBase on HDInsight**: Provides a persistent NoSQL data store for data after it has been processed by Storm.</span></span>
* <span data-ttu-id="4aa71-133">**Serviço de rede Virtual do Azure**: permite a comunicação segura entre hello Storm no HDInsight e HBase em clusters de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4aa71-133">**Azure Virtual Network service**: Enables secure communications between hello Storm on HDInsight and HBase on HDInsight clusters.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="4aa71-134">Uma rede virtual é necessária ao usar a API de cliente de Java HBase hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-134">A virtual network is required when using hello Java HBase client API.</span></span> <span data-ttu-id="4aa71-135">Ela não fica exposta por gateway de público Olá para clusters do HBase.</span><span class="sxs-lookup"><span data-stu-id="4aa71-135">It is not exposed over hello public gateway for HBase clusters.</span></span> <span data-ttu-id="4aa71-136">Clusters HBase instalar e Storm em Olá mesma rede virtual permite Olá cluster Storm (ou qualquer outro sistema na rede virtual Olá) toodirectly acessar HBase usando a API do cliente.</span><span class="sxs-lookup"><span data-stu-id="4aa71-136">Installing HBase and Storm clusters into hello same virtual network allows hello Storm cluster (or any other system on hello virtual network) toodirectly access HBase using client API.</span></span>

* <span data-ttu-id="4aa71-137">**Site do painel**: um painel de exemplo que traça gráficos de dados em tempo real.</span><span class="sxs-lookup"><span data-stu-id="4aa71-137">**Dashboard website**: An example dashboard that charts data in real time.</span></span>
  
  * <span data-ttu-id="4aa71-138">site de saudação é implementado em Node. js.</span><span class="sxs-lookup"><span data-stu-id="4aa71-138">hello website is implemented in Node.js.</span></span>
  * <span data-ttu-id="4aa71-139">[Socket.IO](http://socket.io/) é usado para comunicação em tempo real entre Olá site da Web e de topologia de profusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aa71-139">[Socket.io](http://socket.io/) is used for real-time communication between hello Storm topology and hello website.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="4aa71-140">O uso do Socket.io para a comunicação é um detalhe de implementação.</span><span class="sxs-lookup"><span data-stu-id="4aa71-140">Using Socket.io for communication is an implementation detail.</span></span> <span data-ttu-id="4aa71-141">Você pode usar qualquer estrutura de comunicação, como SignalR ou WebSockets brutos.</span><span class="sxs-lookup"><span data-stu-id="4aa71-141">You can use any communications framework, such as raw WebSockets or SignalR.</span></span>

  * <span data-ttu-id="4aa71-142">[D3.js](http://d3js.org/) toograph usado Olá dados enviados toohello site.</span><span class="sxs-lookup"><span data-stu-id="4aa71-142">[D3.js](http://d3js.org/) is used toograph hello data that is sent toohello website.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4aa71-143">Dois clusters são necessários, pois não há nenhum método com suporte toocreate um HDInsight cluster Storm e HBase.</span><span class="sxs-lookup"><span data-stu-id="4aa71-143">Two clusters are required, as there is no supported method toocreate one HDInsight cluster for both Storm and HBase.</span></span>

<span data-ttu-id="4aa71-144">Olá topologia lê dados de Hub de eventos usando Olá [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) classe e grava dados em HBase usando Olá [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) classe.</span><span class="sxs-lookup"><span data-stu-id="4aa71-144">hello topology reads data from Event Hub by using hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) class, and writes data into HBase using hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) class.</span></span> <span data-ttu-id="4aa71-145">Comunicação com o site de saudação é realizada usando [client.java socket.io](https://github.com/nkzawa/socket.io-client.java).</span><span class="sxs-lookup"><span data-stu-id="4aa71-145">Communication with hello website is accomplished by using [socket.io-client.java](https://github.com/nkzawa/socket.io-client.java).</span></span>

<span data-ttu-id="4aa71-146">Olá diagrama a seguir explica o layout de saudação da topologia de saudação:</span><span class="sxs-lookup"><span data-stu-id="4aa71-146">hello following diagram explains hello layout of hello topology:</span></span>

![diagrama de topologia](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> <span data-ttu-id="4aa71-148">Este diagrama é uma exibição simplificada de topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aa71-148">This diagram is a simplified view of hello topology.</span></span> <span data-ttu-id="4aa71-149">Uma instância de cada componente é criada para cada partição no Hub de Eventos.</span><span class="sxs-lookup"><span data-stu-id="4aa71-149">An instance of each component is created for each partition in your Event Hub.</span></span> <span data-ttu-id="4aa71-150">Essas instâncias são distribuídas entre os nós de saudação em cluster hello e dados são roteados entre eles, da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="4aa71-150">These instances are distributed across hello nodes in hello cluster, and data is routed between them as follows:</span></span>
> 
> * <span data-ttu-id="4aa71-151">Dados do analisador de toohello spout Olá são com balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="4aa71-151">Data from hello spout toohello parser is load balanced.</span></span>
> * <span data-ttu-id="4aa71-152">Dados de saudação analisador toohello painel e HBase são agrupados por ID do dispositivo, para que as mensagens de Olá mesmo dispositivo sempre fluxo toohello mesmo componente.</span><span class="sxs-lookup"><span data-stu-id="4aa71-152">Data from hello parser toohello Dashboard and HBase is grouped by Device ID, so that messages from hello same device always flow toohello same component.</span></span>

### <a name="topology-components"></a><span data-ttu-id="4aa71-153">Componentes da topologia</span><span class="sxs-lookup"><span data-stu-id="4aa71-153">Topology components</span></span>

* <span data-ttu-id="4aa71-154">**Evento Hub Spout**: spout Olá é fornecido como parte da versão do Apache Storm 0.10.0 e superior.</span><span class="sxs-lookup"><span data-stu-id="4aa71-154">**Event Hub Spout**: hello spout is provided as part of Apache Storm version 0.10.0 and higher.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="4aa71-155">spout do Hub de eventos Olá usado neste exemplo requer uma profusão de versão do cluster HDInsight 3.5 ou 3.6.</span><span class="sxs-lookup"><span data-stu-id="4aa71-155">hello Event Hub spout used in this example requires a Storm on HDInsight cluster version 3.5 or 3.6.</span></span>

* <span data-ttu-id="4aa71-156">**ParserBolt.java**: Olá dados emitida pelo spout Olá JSON bruto e, ocasionalmente, mais de um evento é emitido por vez.</span><span class="sxs-lookup"><span data-stu-id="4aa71-156">**ParserBolt.java**: hello data that is emitted by hello spout is raw JSON, and occasionally more than one event is emitted at a time.</span></span> <span data-ttu-id="4aa71-157">Este raio lê dados de saudação emitidos pelo Olá spout e analisa a mensagem de saudação do JSON.</span><span class="sxs-lookup"><span data-stu-id="4aa71-157">This bolt reads hello data emitted by hello spout and parses hello JSON message.</span></span> <span data-ttu-id="4aa71-158">raio Hello, em seguida, emite os dados de saudação como uma tupla que contém vários campos.</span><span class="sxs-lookup"><span data-stu-id="4aa71-158">hello bolt then emits hello data as a tuple that contains multiple fields.</span></span>
* <span data-ttu-id="4aa71-159">**DashboardBolt.java**: esse componente demonstra como toouse Olá Socket.io biblioteca de cliente para dados do Java toosend no painel da web toohello em tempo real.</span><span class="sxs-lookup"><span data-stu-id="4aa71-159">**DashboardBolt.java**: This component demonstrates how toouse hello Socket.io client library for Java toosend data in real time toohello web dashboard.</span></span>
* <span data-ttu-id="4aa71-160">**não hbase.yaml**: Olá definição de topologia usada durante a execução no modo local.</span><span class="sxs-lookup"><span data-stu-id="4aa71-160">**no-hbase.yaml**: hello topology definition used when running in local mode.</span></span> <span data-ttu-id="4aa71-161">Não usa componentes HBase.</span><span class="sxs-lookup"><span data-stu-id="4aa71-161">It does not use HBase components.</span></span>
* <span data-ttu-id="4aa71-162">**com hbase.yaml**: Olá definição de topologia usada ao executar topologia Olá no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-162">**with-hbase.yaml**: hello topology definition used when running hello topology on hello cluster.</span></span> <span data-ttu-id="4aa71-163">Usa componentes HBase.</span><span class="sxs-lookup"><span data-stu-id="4aa71-163">It does use HBase components.</span></span>
* <span data-ttu-id="4aa71-164">**dev.properties**: Olá informações de configuração para spout do Hub de eventos de saudação, HBase raio e os componentes do painel.</span><span class="sxs-lookup"><span data-stu-id="4aa71-164">**dev.properties**: hello configuration information for hello Event Hub spout, HBase bolt, and dashboard components.</span></span>

## <a name="prepare-your-environment"></a><span data-ttu-id="4aa71-165">Prepare o seu ambiente</span><span class="sxs-lookup"><span data-stu-id="4aa71-165">Prepare your environment</span></span>

<span data-ttu-id="4aa71-166">Antes de usar este exemplo, você deve criar um Hub de eventos do Azure, a topologia que Storm Olá lê do.</span><span class="sxs-lookup"><span data-stu-id="4aa71-166">Before you use this example, you must create an Azure Event Hub, which hello Storm topology reads from.</span></span>

### <a name="configure-event-hub"></a><span data-ttu-id="4aa71-167">Configurar o Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="4aa71-167">Configure Event Hub</span></span>

<span data-ttu-id="4aa71-168">Hub de eventos é a fonte de dados de saudação para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="4aa71-168">Event Hub is hello data source for this example.</span></span> <span data-ttu-id="4aa71-169">Use Olá etapas toocreate um Hub de eventos a seguir.</span><span class="sxs-lookup"><span data-stu-id="4aa71-169">Use hello following steps toocreate an Event Hub.</span></span>

1. <span data-ttu-id="4aa71-170">De saudação [portal do Azure](https://portal.azure.com), selecione **+ novo** -> **Internet das coisas** -> **Hubs de eventos**.</span><span class="sxs-lookup"><span data-stu-id="4aa71-170">From hello [Azure portal](https://portal.azure.com), select **+ New** -> **Internet of Things** -> **Event Hubs**.</span></span>
2. <span data-ttu-id="4aa71-171">Em Olá **criar Namespace** , execute as seguintes tarefas de saudação:</span><span class="sxs-lookup"><span data-stu-id="4aa71-171">In hello **Create Namespace** section, perform hello following tasks:</span></span>
   
   1. <span data-ttu-id="4aa71-172">Insira um **nome** Olá namespace.</span><span class="sxs-lookup"><span data-stu-id="4aa71-172">Enter a **Name** for hello namespace.</span></span>
   2. <span data-ttu-id="4aa71-173">Selecione um tipo de preço.</span><span class="sxs-lookup"><span data-stu-id="4aa71-173">Select a pricing tier.</span></span> <span data-ttu-id="4aa71-174">**Básico** é suficiente para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="4aa71-174">**Basic** is sufficient for this example.</span></span>
   3. <span data-ttu-id="4aa71-175">Selecione hello Azure **assinatura** toouse.</span><span class="sxs-lookup"><span data-stu-id="4aa71-175">Select hello Azure **Subscription** toouse.</span></span>
   4. <span data-ttu-id="4aa71-176">Selecione um grupo de recursos existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="4aa71-176">Either select an existing resource group or create a new one.</span></span>
   5. <span data-ttu-id="4aa71-177">Selecione Olá **local** para Olá Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="4aa71-177">Select hello **Location** for hello Event Hub.</span></span>
   6. <span data-ttu-id="4aa71-178">Selecione **Pin toodashboard**e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="4aa71-178">Select **Pin toodashboard**, and then click **Create**.</span></span>

3. <span data-ttu-id="4aa71-179">Quando o processo de criação de saudação for concluído, Olá informações de Hubs de eventos para o namespace é exibida.</span><span class="sxs-lookup"><span data-stu-id="4aa71-179">When hello creation process completes, hello Event Hubs information for your namespace is displayed.</span></span> <span data-ttu-id="4aa71-180">Desse local, selecione **+ Adicionar Hub de Eventos**.</span><span class="sxs-lookup"><span data-stu-id="4aa71-180">From here, select **+ Add Event Hub**.</span></span> <span data-ttu-id="4aa71-181">Em Olá **criar Hub de eventos** seção, insira um nome de **sensordata**e, em seguida, selecione **criar**.</span><span class="sxs-lookup"><span data-stu-id="4aa71-181">In hello **Create Event Hub** section, enter a name of **sensordata**, and then select **Create**.</span></span> <span data-ttu-id="4aa71-182">Deixe Olá outros campos com valores padrão de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aa71-182">Leave hello other fields at hello default values.</span></span>
4. <span data-ttu-id="4aa71-183">Olá dos Hubs de eventos Exibir para seu namespace, selecione **Hubs de eventos**.</span><span class="sxs-lookup"><span data-stu-id="4aa71-183">From hello Event Hubs view for your namespace, select **Event Hubs**.</span></span> <span data-ttu-id="4aa71-184">Selecione Olá **sensordata** entrada.</span><span class="sxs-lookup"><span data-stu-id="4aa71-184">Select hello **sensordata** entry.</span></span>
5. <span data-ttu-id="4aa71-185">Olá sensordata Hub de eventos, selecione **políticas de acesso compartilhado**.</span><span class="sxs-lookup"><span data-stu-id="4aa71-185">From hello sensordata Event Hub, select **Shared access policies**.</span></span> <span data-ttu-id="4aa71-186">Saudação de uso **+ adicionar** saudação do link tooadd políticas a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-186">Use hello **+ Add** link tooadd hello following policies:</span></span>

    | <span data-ttu-id="4aa71-187">Nome da política</span><span class="sxs-lookup"><span data-stu-id="4aa71-187">Policy name</span></span> | <span data-ttu-id="4aa71-188">Declarações</span><span class="sxs-lookup"><span data-stu-id="4aa71-188">Claims</span></span> |
    | ----- | ----- |
    | <span data-ttu-id="4aa71-189">dispositivos</span><span class="sxs-lookup"><span data-stu-id="4aa71-189">devices</span></span> | <span data-ttu-id="4aa71-190">Enviar</span><span class="sxs-lookup"><span data-stu-id="4aa71-190">Send</span></span> |
    | <span data-ttu-id="4aa71-191">storm</span><span class="sxs-lookup"><span data-stu-id="4aa71-191">storm</span></span> | <span data-ttu-id="4aa71-192">Escutar</span><span class="sxs-lookup"><span data-stu-id="4aa71-192">Listen</span></span> |

1. <span data-ttu-id="4aa71-193">Selecione ambas as políticas e anote Olá **chave primária** valor.</span><span class="sxs-lookup"><span data-stu-id="4aa71-193">Select both policies and make a note of hello **PRIMARY KEY** value.</span></span> <span data-ttu-id="4aa71-194">Você precisa valor Olá para ambas as políticas em etapas futuras.</span><span class="sxs-lookup"><span data-stu-id="4aa71-194">You need hello value for both policies in future steps.</span></span>

## <a name="download-and-configure-hello-project"></a><span data-ttu-id="4aa71-195">Baixar e configurar o projeto de saudação</span><span class="sxs-lookup"><span data-stu-id="4aa71-195">Download and configure hello project</span></span>

<span data-ttu-id="4aa71-196">Use Olá seguindo o projeto de saudação toodownload do GitHub.</span><span class="sxs-lookup"><span data-stu-id="4aa71-196">Use hello following toodownload hello project from GitHub.</span></span>

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

<span data-ttu-id="4aa71-197">Após a conclusão do comando hello, você tem Olá estrutura de diretórios a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-197">After hello command completes, you have hello following directory structure:</span></span>

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> <span data-ttu-id="4aa71-198">Este documento não entra nos detalhes de toofull de código Olá incluídos neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="4aa71-198">This document does not go in toofull details of hello code included in this example.</span></span> <span data-ttu-id="4aa71-199">No entanto, o código de saudação totalmente é comentado.</span><span class="sxs-lookup"><span data-stu-id="4aa71-199">However, hello code is fully commented.</span></span>

<span data-ttu-id="4aa71-200">tooconfigure tooread de projeto de saudação do Hub de eventos, abra Olá `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` e adicione seu toohello de informações de Hub de eventos linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="4aa71-200">tooconfigure hello project tooread from Event Hub, open hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file and add your Event Hub information toohello following lines:</span></span>

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a><span data-ttu-id="4aa71-201">Compile e teste localmente</span><span class="sxs-lookup"><span data-stu-id="4aa71-201">Compile and test locally</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4aa71-202">Usando a topologia de saudação localmente requer um ambiente de desenvolvimento profusão de trabalho.</span><span class="sxs-lookup"><span data-stu-id="4aa71-202">Using hello topology locally requires a working Storm development environment.</span></span> <span data-ttu-id="4aa71-203">Para saber mais, confira [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) (Configurando um ambiente de desenvolvimento Storm) em Apache.org.</span><span class="sxs-lookup"><span data-stu-id="4aa71-203">For more information, see [Setting up a Storm development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) at Apache.org.</span></span>

> [!WARNING]
> <span data-ttu-id="4aa71-204">Se você estiver usando um ambiente de desenvolvimento do Windows, você pode receber um `java.io.IOException` ao executar a topologia de saudação localmente.</span><span class="sxs-lookup"><span data-stu-id="4aa71-204">If you are using a Windows development environment, you may receive a `java.io.IOException` when running hello topology locally.</span></span> <span data-ttu-id="4aa71-205">Nesse caso, mova na topologia de saudação toorunning no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4aa71-205">If so, move on toorunning hello topology on HDInsight.</span></span>

<span data-ttu-id="4aa71-206">Antes de testar, você deve iniciar Olá painel tooview Olá saída de topologia hello e gerar dados toostore no Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="4aa71-206">Before testing, you must start hello dashboard tooview hello output of hello topology and generate data toostore in Event Hub.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4aa71-207">componente do HBase Olá dessa topologia não está ativo quando testar localmente.</span><span class="sxs-lookup"><span data-stu-id="4aa71-207">hello HBase component of this topology is not active when testing locally.</span></span> <span data-ttu-id="4aa71-208">Olá API Java para o cluster do HBase Olá não pode ser acessado de fora Olá rede Virtual do Azure que contém Olá clusters.</span><span class="sxs-lookup"><span data-stu-id="4aa71-208">hello Java API for hello HBase cluster cannot be accessed from outside hello Azure Virtual Network that contains hello clusters.</span></span>

### <a name="start-hello-web-application"></a><span data-ttu-id="4aa71-209">Iniciar o aplicativo da web hello</span><span class="sxs-lookup"><span data-stu-id="4aa71-209">Start hello web application</span></span>

1. <span data-ttu-id="4aa71-210">Abra um prompt de comando e altere os diretórios muito`hdinsight-eventhub-example/dashboard`.</span><span class="sxs-lookup"><span data-stu-id="4aa71-210">Open a command prompt and change directories too`hdinsight-eventhub-example/dashboard`.</span></span> <span data-ttu-id="4aa71-211">Use Olá dependências de saudação do comando tooinstall exigidas pelo aplicativo de web Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-211">Use hello following command tooinstall hello dependencies needed by hello web application:</span></span>
   
    ```bash
    npm install
    ```

2. <span data-ttu-id="4aa71-212">Use Olá aplicativo web do comando toostart hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-212">Use hello following command toostart hello web application:</span></span>
   
    ```bash
    node server.js
    ```
   
    <span data-ttu-id="4aa71-213">Você verá um toohello semelhante mensagem texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-213">You see a message similar toohello following text:</span></span>
   
        Server listening at port 3000

3. <span data-ttu-id="4aa71-214">Abra um navegador da web e digite `http://localhost:3000/` como endereço de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aa71-214">Open a web browser and enter `http://localhost:3000/` as hello address.</span></span> <span data-ttu-id="4aa71-215">Um toohello semelhante página imagem a seguir é exibida:</span><span class="sxs-lookup"><span data-stu-id="4aa71-215">A page similar toohello following image is displayed:</span></span>
   
    ![Painel da Web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    <span data-ttu-id="4aa71-217">Deixe esse prompt de comando aberto.</span><span class="sxs-lookup"><span data-stu-id="4aa71-217">Leave this command prompt open.</span></span> <span data-ttu-id="4aa71-218">Depois de testes, use servidor de web de saudação de toostop Ctrl-C.</span><span class="sxs-lookup"><span data-stu-id="4aa71-218">After testing, use Ctrl-C toostop hello web server.</span></span>

### <a name="generate-data"></a><span data-ttu-id="4aa71-219">Gerar dados</span><span class="sxs-lookup"><span data-stu-id="4aa71-219">Generate data</span></span>

> [!NOTE]
> <span data-ttu-id="4aa71-220">Hello etapas desta seção usam Node. js para que eles podem ser usados em qualquer plataforma.</span><span class="sxs-lookup"><span data-stu-id="4aa71-220">hello steps in this section use Node.js so that they can be used on any platform.</span></span> <span data-ttu-id="4aa71-221">Para obter outros exemplos de idioma, consulte Olá `SendEvents` directory.</span><span class="sxs-lookup"><span data-stu-id="4aa71-221">For other language examples, see hello `SendEvents` directory.</span></span>

1. <span data-ttu-id="4aa71-222">Abra um novo prompt, shell ou terminal e altere os diretórios muito`hdinsight-eventhub-example/SendEvents/nodejs`.</span><span class="sxs-lookup"><span data-stu-id="4aa71-222">Open a new prompt, shell, or terminal, and change directories too`hdinsight-eventhub-example/SendEvents/nodejs`.</span></span> <span data-ttu-id="4aa71-223">dependências de saudação tooinstall exigidas pelo aplicativo hello, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-223">tooinstall hello dependencies needed by hello application, use hello following command:</span></span>

    ```bash
    npm install
    ```

2. <span data-ttu-id="4aa71-224">Olá abrir `app.js` do arquivo em um editor de texto e adicione Olá informações de Hub de eventos obtidos anteriormente:</span><span class="sxs-lookup"><span data-stu-id="4aa71-224">Open hello `app.js` file in a text editor and add hello Event Hub information you obtained earlier:</span></span>
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > <span data-ttu-id="4aa71-225">Este exemplo supõe que você usou o `sensordata` como nome de saudação do seu Hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="4aa71-225">This example assumes that you have used `sensordata` as hello name of your Event Hub.</span></span> <span data-ttu-id="4aa71-226">E se `devices` como nome de saudação da política de saudação que tem um `Send` de declaração.</span><span class="sxs-lookup"><span data-stu-id="4aa71-226">And that `devices` as hello name of hello policy that has a `Send` claim.</span></span>

3. <span data-ttu-id="4aa71-227">Use Olá comando tooinsert novas entradas no Hub de eventos a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-227">Use hello following command tooinsert new entries in Event Hub:</span></span>
   
    ```bash
    node app.js
    ```
   
    <span data-ttu-id="4aa71-228">Você verá várias linhas de saída que contêm dados de saudação enviada tooEvent Hub:</span><span class="sxs-lookup"><span data-stu-id="4aa71-228">You see several lines of output that contain hello data sent tooEvent Hub:</span></span>
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a><span data-ttu-id="4aa71-229">Criar e iniciar a topologia de saudação</span><span class="sxs-lookup"><span data-stu-id="4aa71-229">Build and start hello topology</span></span>

1. <span data-ttu-id="4aa71-230">Abra um novo prompt de comando e altere os diretórios muito`hdinsight-eventhub-example/TemperatureMonitor`.</span><span class="sxs-lookup"><span data-stu-id="4aa71-230">Open a new command prompt and change directories too`hdinsight-eventhub-example/TemperatureMonitor`.</span></span> <span data-ttu-id="4aa71-231">toobuild e pacote hello topologia, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-231">toobuild and package hello topology, use hello following command:</span></span> 

    ```bash
    mvn clean package
    ```

2. <span data-ttu-id="4aa71-232">toostart Olá topologia em modo local, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-232">toostart hello topology in local mode, use hello following command:</span></span>

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * <span data-ttu-id="4aa71-233">`--local`topologia de saudação inicia no modo local.</span><span class="sxs-lookup"><span data-stu-id="4aa71-233">`--local` starts hello topology in local mode.</span></span>
    * <span data-ttu-id="4aa71-234">`--filter`Olá usa `dev.properties` toopopulate parâmetros na definição de topologia de saudação do arquivo.</span><span class="sxs-lookup"><span data-stu-id="4aa71-234">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="4aa71-235">`resources/no-hbase.yaml`Olá usa `no-hbase.yaml` definição de topologia.</span><span class="sxs-lookup"><span data-stu-id="4aa71-235">`resources/no-hbase.yaml` uses hello `no-hbase.yaml` topology definition.</span></span>
 
   <span data-ttu-id="4aa71-236">Depois de iniciado, topologia Olá lê as entradas do Hub de eventos e as envia toohello painel em execução no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="4aa71-236">Once started, hello topology reads entries from Event Hub, and sends them toohello dashboard running on your local machine.</span></span> <span data-ttu-id="4aa71-237">Você deverá ver linhas no painel da web hello, semelhante toohello imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-237">You should see lines appear in hello web dashboard, similar toohello following image:</span></span>
   
    ![Painel com dados](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. <span data-ttu-id="4aa71-239">Enquanto estiver executando o painel hello, use Olá `node app.js` tooEvent de dados novo toosend Hubs as etapas de comando de saudação anterior.</span><span class="sxs-lookup"><span data-stu-id="4aa71-239">While hello dashboard is running, use hello `node app.js` command from hello previous steps toosend new data tooEvent Hubs.</span></span> <span data-ttu-id="4aa71-240">Porque os valores de temperatura Olá gerados aleatoriamente, gráfico de saudação deve atualizar tooshow grandes alterações de temperatura.</span><span class="sxs-lookup"><span data-stu-id="4aa71-240">Because hello temperature values are randomly generated, hello graph should update tooshow large changes in temperature.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="4aa71-241">Você deve estar no hello **hdinsight-eventhub-exemplo/SendEvents/Nodejs** diretório ao usar Olá `node app.js` comando.</span><span class="sxs-lookup"><span data-stu-id="4aa71-241">You must be in hello **hdinsight-eventhub-example/SendEvents/Nodejs** directory when using hello `node app.js` command.</span></span>

3. <span data-ttu-id="4aa71-242">Depois de verificar atualizações de painel hello, parada Olá topologia usando Ctrl + C.</span><span class="sxs-lookup"><span data-stu-id="4aa71-242">After verifying that hello dashboard updates, stop hello topology using Ctrl+C.</span></span> <span data-ttu-id="4aa71-243">Você também pode usar servidor web local do Ctrl + C toostop hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-243">You can use Ctrl+C toostop hello local web server also.</span></span>

## <a name="create-a-storm-and-hbase-cluster"></a><span data-ttu-id="4aa71-244">Criar um cluster Storm e HBase</span><span class="sxs-lookup"><span data-stu-id="4aa71-244">Create a Storm and HBase cluster</span></span>

<span data-ttu-id="4aa71-245">Olá as etapas desta seção usam um [modelo do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) toocreate um cluster de rede Virtual do Azure e uma tempestade e HBase na rede virtual hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-245">hello steps in this section use an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md) toocreate an Azure Virtual Network and a Storm and HBase cluster on hello virtual network.</span></span> <span data-ttu-id="4aa71-246">modelo de saudação também cria um aplicativo Web do Azure e implanta uma cópia do painel Olá nele.</span><span class="sxs-lookup"><span data-stu-id="4aa71-246">hello template also creates an Azure Web App and deploys a copy of hello dashboard into it.</span></span>

> [!NOTE]
> <span data-ttu-id="4aa71-247">Uma rede virtual é usada para que a topologia de saudação em execução no cluster de profusão de saudação pode se comunicar diretamente com cluster do HBase hello usando Olá HBase Java API.</span><span class="sxs-lookup"><span data-stu-id="4aa71-247">A virtual network is used so that hello topology running on hello Storm cluster can directly communicate with hello HBase cluster using hello HBase Java API.</span></span>

<span data-ttu-id="4aa71-248">modelo do Gerenciador de recursos de saudação usado neste documento está localizado em um contêiner de blob público em **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span><span class="sxs-lookup"><span data-stu-id="4aa71-248">hello Resource Manager template used in this document is located in a public blob container at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.</span></span>

1. <span data-ttu-id="4aa71-249">Clique em Olá botão toosign em tooAzure e modelo do Gerenciador de recursos de saudação abrir no portal do Azure de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="4aa71-249">Click hello following button toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="4aa71-250">De saudação **implantação personalizada** seção, digite Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-250">From hello **Custom deployment** section, enter hello following values:</span></span>
   
    ![Parâmetros do HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * <span data-ttu-id="4aa71-252">**Nome do Cluster base**: esse valor é usado como nome de base Olá para clusters de saudação Storm e HBase.</span><span class="sxs-lookup"><span data-stu-id="4aa71-252">**Base Cluster Name**: This value is used as hello base name for hello Storm and HBase clusters.</span></span> <span data-ttu-id="4aa71-253">Por exemplo, a inserção de **abc** cria um cluster Storm chamado **storm-abc** e um cluster HBase chamado **hbase-abc**.</span><span class="sxs-lookup"><span data-stu-id="4aa71-253">For example, entering **abc** creates a Storm cluster named **storm-abc** and an HBase cluster named **hbase-abc**.</span></span>
   * <span data-ttu-id="4aa71-254">**Nome de usuário de logon de cluster**: nome de usuário de administrador Olá para clusters de saudação Storm e HBase.</span><span class="sxs-lookup"><span data-stu-id="4aa71-254">**Cluster Login User Name**: hello admin user name for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="4aa71-255">**Senha de logon de cluster**: senha do usuário administrador Olá para clusters de saudação Storm e HBase.</span><span class="sxs-lookup"><span data-stu-id="4aa71-255">**Cluster Login Password**: hello admin user password for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="4aa71-256">**Nome de usuário SSH**: Olá toocreate de usuário SSH para clusters de saudação Storm e HBase.</span><span class="sxs-lookup"><span data-stu-id="4aa71-256">**SSH User Name**: hello SSH user toocreate for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="4aa71-257">**Senha SSH**: senha Olá para usuário SSH Olá Olá Storm e HBase clusters.</span><span class="sxs-lookup"><span data-stu-id="4aa71-257">**SSH Password**: hello password for hello SSH user for hello Storm and HBase clusters.</span></span>
   * <span data-ttu-id="4aa71-258">**Local**: região Olá Olá clusters são criados no.</span><span class="sxs-lookup"><span data-stu-id="4aa71-258">**Location**: hello region that hello clusters are created in.</span></span>
     
     <span data-ttu-id="4aa71-259">Clique em **Okey** toosave parâmetros de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aa71-259">Click **OK** toosave hello parameters.</span></span>

3. <span data-ttu-id="4aa71-260">Saudação de uso **Noções básicas de** seção toocreate um grupo de recursos ou selecione um existente.</span><span class="sxs-lookup"><span data-stu-id="4aa71-260">Use hello **Basics** section toocreate a resource group or select an existing one.</span></span>
4. <span data-ttu-id="4aa71-261">Em Olá **local do grupo de recursos** menu suspenso, selecione Olá mesmo local que você selecionou para Olá **local** parâmetro hello **configurações** seção.</span><span class="sxs-lookup"><span data-stu-id="4aa71-261">In hello **Resource group location** dropdown menu, select hello same location as you selected for hello **Location** parameter in hello **Settings** section.</span></span>
5. <span data-ttu-id="4aa71-262">Ler Olá termos e condições e, em seguida, selecione **concordo toohello termos e condições declaradas acima**.</span><span class="sxs-lookup"><span data-stu-id="4aa71-262">Read hello terms and conditions, and then select **I agree toohello terms and conditions stated above**.</span></span>
6. <span data-ttu-id="4aa71-263">Finalmente, verifique **Pin toodashboard** e, em seguida, selecione **compra**.</span><span class="sxs-lookup"><span data-stu-id="4aa71-263">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="4aa71-264">Demora cerca de 20 minutos toocreate clusters hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-264">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="4aa71-265">Após a criação dos recursos de hello, informações sobre o grupo de recursos de saudação são exibidas.</span><span class="sxs-lookup"><span data-stu-id="4aa71-265">Once hello resources have been created, information about hello resource group is displayed.</span></span>

![Grupo de recursos para redes hello e clusters](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="4aa71-267">Observe que os nomes de saudação de clusters de HDInsight Olá ficam **profusão de nome de base** e **nome base do hbase**, onde nome base é o nome da saudação fornecido toohello modelo.</span><span class="sxs-lookup"><span data-stu-id="4aa71-267">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **hbase-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="4aa71-268">Você pode usar esses nomes em uma etapa posterior ao conectar-se toohello clusters.</span><span class="sxs-lookup"><span data-stu-id="4aa71-268">You use these names in a later step when connecting toohello clusters.</span></span> <span data-ttu-id="4aa71-269">Também Observe que Olá nome do site de painel Olá é **nome base painel**.</span><span class="sxs-lookup"><span data-stu-id="4aa71-269">Also note that hello name of hello dashboard site is **basename-dashboard**.</span></span> <span data-ttu-id="4aa71-270">Esse valor é usado posteriormente neste documento.</span><span class="sxs-lookup"><span data-stu-id="4aa71-270">This value is used later in this document.</span></span>

## <a name="configure-hello-dashboard-bolt"></a><span data-ttu-id="4aa71-271">Configurar o raio do painel Olá</span><span class="sxs-lookup"><span data-stu-id="4aa71-271">Configure hello Dashboard bolt</span></span>

<span data-ttu-id="4aa71-272">Painel de toohello de dados toosend implantado como um aplicativo web, você deve modificar Olá a seguinte linha no hello `dev.properties`arquivo:</span><span class="sxs-lookup"><span data-stu-id="4aa71-272">toosend data toohello dashboard deployed as a web app, you must modify hello following line in hello `dev.properties`file:</span></span>

```yaml
dashboard.uri: http://localhost:3000
```

<span data-ttu-id="4aa71-273">Alterar `http://localhost:3000` muito`http://BASENAME-dashboard.azurewebsites.net` e salve o arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-273">Change `http://localhost:3000` too`http://BASENAME-dashboard.azurewebsites.net` and save hello file.</span></span> <span data-ttu-id="4aa71-274">Substituir **nome base** com o nome de base Olá fornecido na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-274">Replace **BASENAME** with hello base name you provided in hello previous step.</span></span> <span data-ttu-id="4aa71-275">Você também pode usar o grupo de recursos de saudação criado anteriormente tooselect Olá painel e exibição Olá URL.</span><span class="sxs-lookup"><span data-stu-id="4aa71-275">You can also use hello resource group created previously tooselect hello dashboard and view hello URL.</span></span>

## <a name="create-hello-hbase-table"></a><span data-ttu-id="4aa71-276">Criar a tabela do HBase Olá</span><span class="sxs-lookup"><span data-stu-id="4aa71-276">Create hello HBase table</span></span>

<span data-ttu-id="4aa71-277">toostore dados em HBase, podemos deve primeiro criar uma tabela.</span><span class="sxs-lookup"><span data-stu-id="4aa71-277">toostore data in HBase, we must first create a table.</span></span> <span data-ttu-id="4aa71-278">Pré-criar recursos Storm precisa toowrite para, como tentar recursos toocreate, de dentro de uma topologia Storm podem resultar em várias instâncias tentar toocreate Olá mesmo recurso.</span><span class="sxs-lookup"><span data-stu-id="4aa71-278">Pre-create resources that Storm needs toowrite to, as trying toocreate resources from inside a Storm topology can result in multiple instances trying toocreate hello same resource.</span></span> <span data-ttu-id="4aa71-279">Criar recursos de Olá fora Olá topologia e usar profusão de leitura/gravação e análise.</span><span class="sxs-lookup"><span data-stu-id="4aa71-279">Create hello resources outside hello topology and use Storm for reading/writing and analytics.</span></span>

1. <span data-ttu-id="4aa71-280">Use o cluster do SSH tooconnect toohello HBase usando o usuário SSH hello e a senha fornecidos toohello modelo durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="4aa71-280">Use SSH tooconnect toohello HBase cluster using hello SSH user and password you supplied toohello template during cluster creation.</span></span> <span data-ttu-id="4aa71-281">Por exemplo, se estiver conectando usando Olá `ssh` de comando, você usaria Olá sintaxe a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-281">For example, if connecting using hello `ssh` command, you would use hello following syntax:</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    <span data-ttu-id="4aa71-282">Substituir `sshuser` com nome de usuário SSH Olá fornecida ao criar o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aa71-282">Replace `sshuser` with hello SSH user name you provided when creating hello cluster.</span></span> <span data-ttu-id="4aa71-283">Substituir `clustername` com o nome do cluster HBase hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-283">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="4aa71-284">Da sessão SSH hello, inicie o shell do HBase hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-284">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="4aa71-285">Quando o shell Olá tiver sido carregado, você ver um `hbase(main):001:0>` prompt.</span><span class="sxs-lookup"><span data-stu-id="4aa71-285">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="4aa71-286">Em Olá shell do HBase, digite Olá comando toocreate dados do sensor de saudação de toostore uma tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-286">From hello HBase shell, enter hello following command toocreate a table toostore hello sensor data:</span></span>
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. <span data-ttu-id="4aa71-287">Verifique se que essa tabela Olá foi criada usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="4aa71-287">Verify that hello table has been created by using hello following command:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="4aa71-288">Isso retorna informações o toohello semelhante exemplo a seguir, indicando que há 0 linhas na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aa71-288">This returns information similar toohello following example, indicating that there are 0 rows in hello table.</span></span>
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. <span data-ttu-id="4aa71-289">Digite `exit` tooexit Olá shell do HBase:</span><span class="sxs-lookup"><span data-stu-id="4aa71-289">Enter `exit` tooexit hello HBase shell:</span></span>

## <a name="configure-hello-hbase-bolt"></a><span data-ttu-id="4aa71-290">Configurar o raio do HBase Olá</span><span class="sxs-lookup"><span data-stu-id="4aa71-290">Configure hello HBase bolt</span></span>

<span data-ttu-id="4aa71-291">toowrite tooHBase do cluster de Storm hello, você deve fornecer raio do HBase Olá com detalhes de configuração de saudação do cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="4aa71-291">toowrite tooHBase from hello Storm cluster, you must provide hello HBase bolt with hello configuration details of your HBase cluster.</span></span>

1. <span data-ttu-id="4aa71-292">Use uma saudação quorum do exemplos tooretrieve Olá Zookeeper para seu cluster HBase a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-292">Use one of hello following examples tooretrieve hello Zookeeper quorum for your HBase cluster:</span></span>

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > <span data-ttu-id="4aa71-293">Substituir `your_HDInsight_cluster_name` com nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4aa71-293">Replace `your_HDInsight_cluster_name` with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="4aa71-294">Para obter mais informações sobre como instalar Olá `jq` utilitário, consulte [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span><span class="sxs-lookup"><span data-stu-id="4aa71-294">For more information on installing hello `jq` utility, see [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).</span></span>
    >
    > <span data-ttu-id="4aa71-295">Quando solicitado, insira a senha de saudação para logon de admin do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-295">When prompted, enter hello password for hello HDInsight admin login.</span></span>

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > <span data-ttu-id="4aa71-296">Substitua ' your_HDInsight_cluster_name com nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4aa71-296">Replace \`your_HDInsight_cluster_name with hello name of your HDInsight cluster.</span></span> <span data-ttu-id="4aa71-297">Quando solicitado, insira a senha de saudação para logon de admin do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-297">When prompted, enter hello password for hello HDInsight admin login.</span></span>
    >
    > <span data-ttu-id="4aa71-298">Este exemplo exige o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4aa71-298">This example requires Azure PowerShell.</span></span> <span data-ttu-id="4aa71-299">Para saber mais sobre como usar o Azure PowerShell, confira [Introdução ao Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span><span class="sxs-lookup"><span data-stu-id="4aa71-299">For more information on using Azure PowerShell, see [Get started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6)</span></span>

    <span data-ttu-id="4aa71-300">informações de Hello retornadas por esses exemplos são semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-300">hello information returned by these examples is similar toohello following text:</span></span>

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    <span data-ttu-id="4aa71-301">Essas informações são usadas pelo toocommunicate Storm com cluster HBase de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aa71-301">This information is used by Storm toocommunicate with hello HBase cluster.</span></span>

2. <span data-ttu-id="4aa71-302">Modificar Olá `dev.properties` e adicione Olá Zookeeper quorum informações toohello linha a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-302">Modify hello `dev.properties` file and add hello Zookeeper quorum information toohello following line:</span></span>

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a><span data-ttu-id="4aa71-303">Criar o pacote e implantar Olá solução tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="4aa71-303">Build, package, and deploy hello solution tooHDInsight</span></span>

<span data-ttu-id="4aa71-304">Em seu ambiente de desenvolvimento, use Olá cluster de storm etapas toodeploy Olá Storm topologia toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="4aa71-304">In your development environment, use hello following steps toodeploy hello Storm topology toohello storm cluster.</span></span>

1. <span data-ttu-id="4aa71-305">De saudação `TemperatureMonitor` diretório, use a seguir Olá comando tooperform uma nova compilação e crie um pacote JAR do seu projeto:</span><span class="sxs-lookup"><span data-stu-id="4aa71-305">From hello `TemperatureMonitor` directory, use hello following command tooperform a new build and create a JAR package from your project:</span></span>
   
        mvn clean package
   
    <span data-ttu-id="4aa71-306">Este comando cria um arquivo chamado `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `diretório de destino do projeto.</span><span class="sxs-lookup"><span data-stu-id="4aa71-306">This command creates a file named `TemperatureMonitor-1.0-SNAPSHOT.jar in hello `target\` directory of your project.</span></span>

2. <span data-ttu-id="4aa71-307">Saudação do uso scp tooupload `TemperatureMonitor-1.0-SNAPSHOT.jar` e `dev.properties` cluster de Storm tooyour arquivos.</span><span class="sxs-lookup"><span data-stu-id="4aa71-307">Use scp tooupload hello `TemperatureMonitor-1.0-SNAPSHOT.jar` and `dev.properties` files tooyour Storm cluster.</span></span> <span data-ttu-id="4aa71-308">Olá seguinte exemplo, substitua `sshuser` com você forneceu ao criar cluster hello, de usuário SSH hello e `clustername` com nome de saudação do cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="4aa71-308">In hello following example, replace `sshuser` with hello SSH user you provided when creating hello cluster, and `clustername` with hello name of your Storm cluster.</span></span> <span data-ttu-id="4aa71-309">Quando solicitado, insira a senha Olá para o usuário SSH hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-309">When prompted, enter hello password for hello SSH user.</span></span>
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > <span data-ttu-id="4aa71-310">Pode levar vários minutos arquivos de saudação tooupload.</span><span class="sxs-lookup"><span data-stu-id="4aa71-310">It may take several minutes tooupload hello files.</span></span>

    <span data-ttu-id="4aa71-311">Para obter mais informações sobre como usar o hello `scp` e `ssh` comandos com o HDInsight, consulte [usar SSH com HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span><span class="sxs-lookup"><span data-stu-id="4aa71-311">For more information on using hello `scp` and `ssh` commands with HDInsight, see [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)</span></span>

3. <span data-ttu-id="4aa71-312">Depois que o arquivo hello foi carregado, conecte o cluster de profusão de toohello usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="4aa71-312">Once hello file has been uploaded, connect toohello Storm cluster using SSH.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="4aa71-313">Substituir `sshuser` com nome de usuário SSH hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-313">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="4aa71-314">Substituir `clustername` com o nome do cluster Storm hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-314">Replace `clustername` with hello Storm cluster name.</span></span>

4. <span data-ttu-id="4aa71-315">toostart Olá topologia, use Olá comandos da sessão SSH Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="4aa71-315">toostart hello topology, use hello following command from hello SSH session:</span></span>
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * <span data-ttu-id="4aa71-316">`--remote`envia Olá topologia toohello serviço Nimbus, que distribui a ele toohello nós de supervisor em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-316">`--remote` submits hello topology toohello Nimbus service, which distributes it toohello supervisor nodes in hello cluster.</span></span>
    * <span data-ttu-id="4aa71-317">`--filter`Olá usa `dev.properties` toopopulate parâmetros na definição de topologia de saudação do arquivo.</span><span class="sxs-lookup"><span data-stu-id="4aa71-317">`--filter` uses hello `dev.properties` file toopopulate parameters in hello topology definition.</span></span>
    * <span data-ttu-id="4aa71-318">`-R /with-hbase.yaml`Olá usa `with-hbase.yaml` incluída no pacote de saudação de topologia.</span><span class="sxs-lookup"><span data-stu-id="4aa71-318">`-R /with-hbase.yaml` uses hello `with-hbase.yaml` topology included in hello package.</span></span>

5. <span data-ttu-id="4aa71-319">Depois de topologia Olá foi iniciado, abrir um site de toohello do navegador publicado no Azure, em seguida, use Olá `node app.js` comando toosend dados tooEvent Hub.</span><span class="sxs-lookup"><span data-stu-id="4aa71-319">After hello topology has started, open a browser toohello website you published on Azure, then use hello `node app.js` command toosend data tooEvent Hub.</span></span> <span data-ttu-id="4aa71-320">Você deve ver informações de Olá Olá web painel atualização toodisplay.</span><span class="sxs-lookup"><span data-stu-id="4aa71-320">You should see hello web dashboard update toodisplay hello information.</span></span>
   
    ![painel Transações da Web](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a><span data-ttu-id="4aa71-322">Exibir dados do HBase</span><span class="sxs-lookup"><span data-stu-id="4aa71-322">View HBase data</span></span>

<span data-ttu-id="4aa71-323">Use Olá tooHBase de tooconnect as etapas a seguir e verifique se que dados saudação foi gravados toohello tabela:</span><span class="sxs-lookup"><span data-stu-id="4aa71-323">Use hello following steps tooconnect tooHBase and verify that hello data has been written toohello table:</span></span>

1. <span data-ttu-id="4aa71-324">Use SSH tooconnect toohello HBase cluster.</span><span class="sxs-lookup"><span data-stu-id="4aa71-324">Use SSH tooconnect toohello HBase cluster.</span></span>
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="4aa71-325">Substituir `sshuser` com nome de usuário SSH hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-325">Replace `sshuser` with hello SSH user name.</span></span> <span data-ttu-id="4aa71-326">Substituir `clustername` com o nome do cluster HBase hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-326">Replace `clustername` with hello HBase cluster name.</span></span>

2. <span data-ttu-id="4aa71-327">Da sessão SSH hello, inicie o shell do HBase hello.</span><span class="sxs-lookup"><span data-stu-id="4aa71-327">From hello SSH session, start hello HBase shell.</span></span>
   
    ```bash
    hbase shell
    ```
   
    <span data-ttu-id="4aa71-328">Quando o shell Olá tiver sido carregado, você ver um `hbase(main):001:0>` prompt.</span><span class="sxs-lookup"><span data-stu-id="4aa71-328">Once hello shell has loaded, you see an `hbase(main):001:0>` prompt.</span></span>

3. <span data-ttu-id="4aa71-329">Exibir as linhas da tabela de saudação:</span><span class="sxs-lookup"><span data-stu-id="4aa71-329">View rows from hello table:</span></span>
   
    ```hbase
    scan 'SensorData'
    ```
   
    <span data-ttu-id="4aa71-330">Esse comando retorna informações o toohello semelhante texto a seguir, indicando que há dados na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aa71-330">This command returns information similar toohello following text, indicating that there is data in hello table.</span></span>
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > <span data-ttu-id="4aa71-331">Operação de varredura retorna um máximo de 10 linhas da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="4aa71-331">This scan operation returns a maximum of 10 rows from hello table.</span></span>

## <a name="delete-your-clusters"></a><span data-ttu-id="4aa71-332">Excluir os clusters</span><span class="sxs-lookup"><span data-stu-id="4aa71-332">Delete your clusters</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="4aa71-333">clusters de saudação toodelete, armazenamento e aplicativo web ao mesmo tempo, exclua o grupo de recursos de saudação que os contém.</span><span class="sxs-lookup"><span data-stu-id="4aa71-333">toodelete hello clusters, storage, and web app at one time, delete hello resource group that contains them.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4aa71-334">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4aa71-334">Next steps</span></span>

<span data-ttu-id="4aa71-335">Para obter mais exemplos de topologias Storm com o HDInsight, consulte [Topologias de exemplo para o Storm no HDInsight](hdinsight-storm-example-topology.md)</span><span class="sxs-lookup"><span data-stu-id="4aa71-335">For more examples of Storm topologies with HDInsight, see [Example topologies for Storm on HDInsight](hdinsight-storm-example-topology.md)</span></span>

<span data-ttu-id="4aa71-336">Para obter mais informações sobre o Apache Storm, consulte Olá [Apache Storm](https://storm.incubator.apache.org/) site.</span><span class="sxs-lookup"><span data-stu-id="4aa71-336">For more information about Apache Storm, see hello [Apache Storm](https://storm.incubator.apache.org/) site.</span></span>

<span data-ttu-id="4aa71-337">Para obter mais informações sobre HBase em HDInsight, consulte Olá [HBase visão geral de HDInsight](hdinsight-hbase-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4aa71-337">For more information about HBase on HDInsight, see hello [HBase with HDInsight Overview](hdinsight-hbase-overview.md).</span></span>

<span data-ttu-id="4aa71-338">Para obter mais informações sobre Socket.io, consulte Olá [socket.io](http://socket.io/) site.</span><span class="sxs-lookup"><span data-stu-id="4aa71-338">For more information about Socket.io, see hello [socket.io](http://socket.io/) site.</span></span>

<span data-ttu-id="4aa71-339">Para saber mais sobre D3.js, confira [D3.js - Documentos controlados por dados](http://d3js.org/)</span><span class="sxs-lookup"><span data-stu-id="4aa71-339">For more information about D3.js, see [D3.js - Data Driven Documents](http://d3js.org/).</span></span>

<span data-ttu-id="4aa71-340">Para saber mais sobre como criar topologias em Java, confira [Desenvolver topologias Java para Apache Storm no HDInsight](hdinsight-storm-develop-java-topology.md).</span><span class="sxs-lookup"><span data-stu-id="4aa71-340">For information about creating topologies in Java, see [Develop Java topologies for Apache Storm on HDInsight](hdinsight-storm-develop-java-topology.md).</span></span>

<span data-ttu-id="4aa71-341">Para saber mais sobre como se conectar ao cluster Storm, confira [Desenvolver topologias C# para Apache Storm no HDInsight usando o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="4aa71-341">For information about creating topologies in .NET, see [Develop C# topologies for Apache Storm on HDInsight using Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>

[azure-portal]: https://portal.azure.com
