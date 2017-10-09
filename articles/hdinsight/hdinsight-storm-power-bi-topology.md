---
title: aaaUse Apache Storm com o Power BI - HDInsight do Azure | Microsoft Docs
description: "Crie um relatório do Power BI usando dados de uma topologia C# em execução em um cluster do Apache Storm no HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 36fe3b9c-5232-4464-8d75-95403b6da7a1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/31/2017
ms.author: larryfr
ms.openlocfilehash: 194cd8220bd60475af1d64a110e4b23ef92e1bc8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-power-bi-toovisualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="8c0f8-103">Usar dados do Power BI toovisualize de uma topologia do Apache Storm</span><span class="sxs-lookup"><span data-stu-id="8c0f8-103">Use Power BI toovisualize data from an Apache Storm topology</span></span>

<span data-ttu-id="8c0f8-104">Power BI permite toovisually exibir dados de relatórios.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-104">Power BI allows you toovisually display data as reports.</span></span> <span data-ttu-id="8c0f8-105">Este documento fornece um exemplo de como toouse Apache Storm em HDInsight toogenerate dados para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-105">This document provides an example of how toouse Apache Storm on HDInsight toogenerate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="8c0f8-106">Olá etapas neste documento dependem de um ambiente de desenvolvimento do Windows com o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-106">hello steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="8c0f8-107">projeto compilado Olá pode ser enviado tooa cluster de HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-107">hello compiled project can be submitted tooa Linux-based HDInsight cluster.</span></span> <span data-ttu-id="8c0f8-108">Somente os clusters baseados em Linux criados depois de 28/10/2016 são compatíveis com as topologias do SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="8c0f8-109">toouse uma topologia c# com um cluster baseado em Linux, saudação de atualização de pacote do Microsoft.SCP.Net.SDK NuGet usado pelo seu projeto tooversion 0.10.0.6 ou superior.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-109">toouse a C# topology with a Linux-based cluster, update hello Microsoft.SCP.Net.SDK NuGet package used by your project tooversion 0.10.0.6 or higher.</span></span> <span data-ttu-id="8c0f8-110">versão de saudação do pacote de saudação também deve corresponder a versão principal de saudação do Storm instalado no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-110">hello version of hello package must also match hello major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="8c0f8-111">Por exemplo, o HDInsight versões 3.3 e 3.4 usam o Storm versão 0.10.x, enquanto o HDInsight 3.5 usa o Storm 1.0. x.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="8c0f8-112">C# topologias em clusters baseados em Linux devem usar o .NET 4.5 e use toorun Mono no cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono toorun on hello HDInsight cluster.</span></span> <span data-ttu-id="8c0f8-113">A maioria das coisas funciona.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-113">Most things work.</span></span> <span data-ttu-id="8c0f8-114">No entanto, você deve verificar Olá [Mono compatibilidade](http://www.mono-project.com/docs/about-mono/compatibility/) documento para incompatibilidades.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-114">However you should check hello [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="8c0f8-115">Para obter uma versão Java deste projeto, que funciona com HDInsight baseado em Windows ou Linux, confira [Processar eventos dos Hubs de Eventos do Azure com Storm no HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="8c0f8-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c0f8-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8c0f8-116">Prerequisites</span></span>

* <span data-ttu-id="8c0f8-117">Um usuário do Azure Active Directory com acesso ao [Power BI](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="8c0f8-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="8c0f8-118">Um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-118">An HDInsight cluster.</span></span> <span data-ttu-id="8c0f8-119">Para obter mais informações, confira [Introdução ao Storm no HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="8c0f8-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="8c0f8-120">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8c0f8-121">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8c0f8-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="8c0f8-122">O Visual Studio (um dos Olá versões a seguir)</span><span class="sxs-lookup"><span data-stu-id="8c0f8-122">Visual Studio (one of hello following versions)</span></span>

  * <span data-ttu-id="8c0f8-123">Visual Studio 2012 com [atualização 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="8c0f8-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="8c0f8-124">Visual Studio 2013 com [atualização 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="8c0f8-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="8c0f8-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="8c0f8-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="8c0f8-126">Visual Studio 2017 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="8c0f8-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="8c0f8-127">Olá ferramentas HDInsight para Visual Studio: consulte [começar a usar as ferramentas do HDInsight Olá para o Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) para obter informações sobre informações de instalação.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-127">hello HDInsight Tools for Visual Studio: See [Get started using hello HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="8c0f8-128">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="8c0f8-128">How it works</span></span>

<span data-ttu-id="8c0f8-129">Este exemplo contém uma topologia do Storm em C# que gera aleatoriamente dados de log do IIS (Serviços de Informações da Internet).</span><span class="sxs-lookup"><span data-stu-id="8c0f8-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="8c0f8-130">Esses dados são gravados tooa banco de dados SQL e de lá é usado toogenerate relatórios no Power BI.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-130">This data is then written tooa SQL Database, and from there it is used toogenerate reports in Power BI.</span></span>

<span data-ttu-id="8c0f8-131">Olá arquivos implementam Olá funcionalidade principal deste exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c0f8-131">hello following files implement hello main functionality of this example:</span></span>

* <span data-ttu-id="8c0f8-132">**SqlAzureBolt.cs**: grava informações produzidas no hello Storm topologia tooSQL banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-132">**SqlAzureBolt.cs**: Writes information produced in hello Storm topology tooSQL Database.</span></span>
* <span data-ttu-id="8c0f8-133">**IISLogsTable.sql**: Olá Transact-SQL instruções usadas toogenerate Olá banco de dados que Olá dados são armazenados em.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-133">**IISLogsTable.sql**: hello Transact-SQL statements used toogenerate hello database that hello data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="8c0f8-134">Crie tabela de saudação no banco de dados SQL antes de iniciar a topologia de saudação no seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-134">Create hello table in SQL Database before starting hello topology on your HDInsight cluster.</span></span>

## <a name="download-hello-example"></a><span data-ttu-id="8c0f8-135">Baixe o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="8c0f8-135">Download hello example</span></span>

<span data-ttu-id="8c0f8-136">Baixar Olá [exemplo HDInsight c# Storm Power BI](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="8c0f8-136">Download hello [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="8c0f8-137">toodownload, uma bifurcação/clone-o usando [git](http://git-scm.com/), ou use Olá **baixar** toodownload de link do arquivo hello. zip.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-137">toodownload it, either fork/clone it using [git](http://git-scm.com/), or use hello **Download** link toodownload a .zip of hello archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="8c0f8-138">Criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="8c0f8-138">Create a database</span></span>

1. <span data-ttu-id="8c0f8-139">toocreate um banco de dados, use as etapas de Olá Olá [tutorial do banco de dados SQL](../sql-database/sql-database-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-139">toocreate a database, use hello steps in hello [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="8c0f8-140">Conectar o banco de dados de toohello por Olá seguir as etapas em Olá [conectar tooa banco de dados SQL com o Visual Studio](../sql-database/sql-database-connect-query.md) documento.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-140">Connect toohello database by following hello steps in hello [Connect tooa SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="8c0f8-141">No Pesquisador de objetos, clique em banco de dados de saudação e selecione **nova consulta**.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-141">In Object Explorer, right-click hello database and select  **New Query**.</span></span> <span data-ttu-id="8c0f8-142">Cole o conteúdo Olá Olá **IISLogsTable.sql** arquivo incluído no hello baixou o projeto na janela de consulta hello e, em seguida, use Ctrl + Shift + a consulta de saudação tooexecute E.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-142">Paste hello contents of hello **IISLogsTable.sql** file included in hello downloaded project into hello query window, and then use Ctrl + Shift + E tooexecute hello query.</span></span> <span data-ttu-id="8c0f8-143">Você deve receber uma mensagem que Olá comandos foi concluídos com êxito.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-143">You should receive a message that hello commands completed successfully.</span></span>

## <a name="configure-hello-sample"></a><span data-ttu-id="8c0f8-144">Configurar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="8c0f8-144">Configure hello sample</span></span>

1. <span data-ttu-id="8c0f8-145">De saudação [portal do Azure](https://portal.azure.com), selecione o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-145">From hello [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="8c0f8-146">De saudação **Essentials** seção da folha de banco de dados SQL hello, selecione **Mostrar cadeias de conexão de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-146">From hello **Essentials** section of hello SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="8c0f8-147">Na lista de saudação que aparece, copie Olá **ADO.NET (autenticação do SQL)** informações.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-147">From hello list that appears, copy hello **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="8c0f8-148">Abra o exemplo hello no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-148">Open hello sample in Visual Studio.</span></span> <span data-ttu-id="8c0f8-149">De **Solution Explorer**, abra Olá **App. config** de arquivo e depois descobrir Olá a seguinte entrada:</span><span class="sxs-lookup"><span data-stu-id="8c0f8-149">From **Solution Explorer**, open hello **App.config** file, and then find hello following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="8c0f8-150">Substituir saudação **TOBEFILLED # # # #** valor com a cadeia de conexão de banco de dados de saudação copiado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-150">Replace hello **##TOBEFILLED##** value with hello database connection string copied in hello previous step.</span></span> <span data-ttu-id="8c0f8-151">Substituir **{sua\_nome de usuário}** e **{sua\_senha}** com hello nome de usuário e senha para o banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-151">Replace **{your\_username}** and **{your\_password}** with hello username and password for hello database.</span></span>

3. <span data-ttu-id="8c0f8-152">Salvar e fechar arquivos hello.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-152">Save and close hello files.</span></span>

## <a name="deploy-hello-sample"></a><span data-ttu-id="8c0f8-153">Implantar o exemplo hello</span><span class="sxs-lookup"><span data-stu-id="8c0f8-153">Deploy hello sample</span></span>

1. <span data-ttu-id="8c0f8-154">De **Solution Explorer**, Olá atalho **StormToSQL** do projeto e selecione **enviar tooStorm no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-154">From **Solution Explorer**, right-click hello **StormToSQL** project and select **Submit tooStorm on HDInsight**.</span></span> <span data-ttu-id="8c0f8-155">Cluster do HDInsight Olá Select de saudação **Cluster Storm** caixa de diálogo de lista suspensa.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-155">Select hello HDInsight cluster from hello **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8c0f8-156">Pode levar alguns segundos para Olá **Cluster Storm** toopopulate suspensa com nomes de servidor.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-156">It may take a few seconds for hello **Storm Cluster** dropdown toopopulate with server names.</span></span>
   >
   > <span data-ttu-id="8c0f8-157">Se solicitado, insira as credenciais de logon de saudação para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-157">If prompted, enter hello login credentials for your Azure subscription.</span></span> <span data-ttu-id="8c0f8-158">Se você tiver mais de uma assinatura, faça logon toohello que contém seu Storm no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-158">If you have more than one subscription, log in toohello one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="8c0f8-159">Quando a topologia de saudação tiver sido enviada, Olá __Visualizador de topologia__ é exibida.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-159">When hello topology has been submitted, hello __Topology Viewer__ appears.</span></span> <span data-ttu-id="8c0f8-160">tooview essa topologia, a entrada de SqlAzureWriterTopology Olá selecione da lista de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-160">tooview this topology, select hello SqlAzureWriterTopology entry from hello list.</span></span>

    ![topologias de Hello, com a topologia de saudação selecionado](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="8c0f8-162">Você pode usar essas informações de toosee de exibição na topologia hello, ou clique duas vezes um componente de tooa específico entrada (como Olá SqlAzureBolt) toosee informações na topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-162">You can use this view toosee information on hello topology, or double-click an entry (such as hello SqlAzureBolt) toosee information specific tooa component in hello topology.</span></span>

3. <span data-ttu-id="8c0f8-163">Após a saudação topologia tem executado por alguns minutos, janela de consulta SQL toohello retorno usado o banco de dados do toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-163">After hello topology has ran for a few minutes, return toohello SQL query window you used toocreate hello database.</span></span> <span data-ttu-id="8c0f8-164">Substitua instruções existentes Olá Olá consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c0f8-164">Replace hello existing statements with hello following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="8c0f8-165">Use Ctrl + Shift + E tooexecute Olá de consulta e você deve receber resultados toohello semelhante seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="8c0f8-165">Use Ctrl + Shift + E tooexecute hello query, and you should receive results similar toohello following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="8c0f8-166">Esses dados foi escritos da topologia de profusão de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-166">This data has been written from hello Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="8c0f8-167">Criar um relatório</span><span class="sxs-lookup"><span data-stu-id="8c0f8-167">Create a report</span></span>

1. <span data-ttu-id="8c0f8-168">Conecte-se toohello [conector do Azure SQL Database](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-168">Connect toohello [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="8c0f8-169">Dentro de **Bancos de Dados**, selecione **Obter**.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="8c0f8-170">Selecione **Banco de Dados SQL do Azure** e **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8c0f8-171">Talvez você seja solicitado toodownload Olá Power BI Desktop toocontinue.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-171">You may be asked toodownload hello Power BI Desktop toocontinue.</span></span> <span data-ttu-id="8c0f8-172">Nesse caso, use Olá tooconnect as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c0f8-172">If so, use hello following steps tooconnect:</span></span>
    >
    > 1. <span data-ttu-id="8c0f8-173">Abra o Power BI Desktop e selecione __Obter dados__.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="8c0f8-174">2 Selecione __Azure__ e, em seguida, __banco de dados SQL do Azure__.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="8c0f8-175">Digite hello informações tooconnect tooyour banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-175">Enter hello information tooconnect tooyour Azure SQL Database.</span></span> <span data-ttu-id="8c0f8-176">Você pode encontrar essas informações visitando Olá [portal do Azure](https://portal.azure.com) e selecionando o banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-176">You can find this information by visiting hello [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="8c0f8-177">Você também pode definir o intervalo de atualização de saudação e filtros personalizados usando **habilitar opções avançadas** de saudação caixa de diálogo de conexão.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-177">You can also set hello refresh interval and custom filters by using **Enable Advanced Options** from hello connect dialog.</span></span>

5. <span data-ttu-id="8c0f8-178">Depois de conectado, você verá um novo conjunto de dados com hello que mesmo nome como o banco de dados de saudação você se conectou.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-178">After you've connected, you will see a new dataset with hello same name as hello database you connected to.</span></span> <span data-ttu-id="8c0f8-179">Selecione Olá toobegin de conjunto de dados criando um relatório.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-179">Select hello dataset toobegin designing a report.</span></span>

6. <span data-ttu-id="8c0f8-180">De **campos**, expanda Olá **IISLOGS** entrada.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-180">From **Fields**, expand hello **IISLOGS** entry.</span></span> <span data-ttu-id="8c0f8-181">toocreate origina-se um relatório que lista Olá URI, marque a caixa de seleção de saudação para **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-181">toocreate a report that lists hello URI stems, select hello checkbox for **URISTEM**.</span></span>

    ![Criando um relatório](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="8c0f8-183">Em seguida, arraste **método** toohello relatório.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-183">Next, drag **METHOD** toohello report.</span></span> <span data-ttu-id="8c0f8-184">Olá Olá de toolist de atualizações de relatório originário e método HTTP correspondente Olá usado para Olá solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-184">hello report updates toolist hello stems and hello corresponding HTTP method used for hello HTTP request.</span></span>

    ![Adicionando dados de método hello](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="8c0f8-186">De saudação **visualizações** coluna, selecione Olá **campos** ícone e, em seguida, selecione Olá a seta para baixo próxima muito**método** em Olá **valores**seção.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-186">From hello **Visualizations** column, select hello **Fields** icon, and then select hello down arrow next too**METHOD** in hello **Values** section.</span></span> <span data-ttu-id="8c0f8-187">toodisplay uma contagem de quantas vezes um URI foi acessada, selecione **contagem**.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-187">toodisplay a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Alterar tooa contagem dos métodos](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="8c0f8-189">Em seguida, selecione Olá **gráfico de colunas empilhadas** toochange como Olá informações são exibidas.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-189">Next, select hello **Stacked column chart** toochange how hello information is displayed.</span></span>

    ![Gráfico de empilhado tooa alteração](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="8c0f8-191">relatório de saudação toosave, selecione **salvar** e digite um nome para o relatório de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-191">toosave hello report, select **Save** and enter a name for hello report.</span></span>

## <a name="stop-hello-topology"></a><span data-ttu-id="8c0f8-192">Parar a topologia de saudação</span><span class="sxs-lookup"><span data-stu-id="8c0f8-192">Stop hello topology</span></span>

<span data-ttu-id="8c0f8-193">topologia Olá continua toorun até você interrompê-lo ou excluir Olá Storm no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-193">hello topology continues toorun until you stop it or delete hello Storm on HDInsight cluster.</span></span> <span data-ttu-id="8c0f8-194">toostop Olá topologia, execute Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c0f8-194">toostop hello topology, perform hello following steps:</span></span>

1. <span data-ttu-id="8c0f8-195">No Visual Studio, retorne toohello Visualizador de topologia e selecione a topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-195">In Visual Studio, return toohello topology viewer and select hello topology.</span></span>

2. <span data-ttu-id="8c0f8-196">Selecione Olá **Kill** topologia de saudação do botão toostop.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-196">Select hello **Kill** button toostop hello topology.</span></span>

    ![Kill botão na topologia de saudação resumida](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="8c0f8-198">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="8c0f8-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="8c0f8-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8c0f8-199">Next steps</span></span>

<span data-ttu-id="8c0f8-200">Neste documento, você aprendeu como toosend dados de uma topologia de Storm tooSQL banco de dados, em seguida, visualizar dados hello usando o Power BI.</span><span class="sxs-lookup"><span data-stu-id="8c0f8-200">In this document, you learned how toosend data from a Storm topology tooSQL Database, then visualize hello data using Power BI.</span></span> <span data-ttu-id="8c0f8-201">Para obter informações sobre como toowork com outras tecnologias do Azure usando Storm no HDInsight, consulte Olá documento a seguir:</span><span class="sxs-lookup"><span data-stu-id="8c0f8-201">For information on how toowork with other Azure technologies using Storm on HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="8c0f8-202">Topologias de exemplo para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8c0f8-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
