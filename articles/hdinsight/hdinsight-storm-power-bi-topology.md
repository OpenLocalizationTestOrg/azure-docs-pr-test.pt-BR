---
title: "Usar Apache Storm com Power BI – HDInsight do Azure | Microsoft Docs"
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
ms.openlocfilehash: 36487c0c34e5a4bb955bbc15c8c96b9e838aeb44
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-power-bi-to-visualize-data-from-an-apache-storm-topology"></a><span data-ttu-id="04cb3-103">Usar o Power BI para visualizar dados de uma topologia do Apache Storm</span><span class="sxs-lookup"><span data-stu-id="04cb3-103">Use Power BI to visualize data from an Apache Storm topology</span></span>

<span data-ttu-id="04cb3-104">O Power BI permite a exibição visual dos dados como relatórios.</span><span class="sxs-lookup"><span data-stu-id="04cb3-104">Power BI allows you to visually display data as reports.</span></span> <span data-ttu-id="04cb3-105">Este documento fornece um exemplo de como usar o Apache Storm no HDInsight para gerar dados para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="04cb3-105">This document provides an example of how to use Apache Storm on HDInsight to generate data for Power BI.</span></span>

> [!NOTE]
> <span data-ttu-id="04cb3-106">As etapas neste documento dependem de um ambiente de desenvolvimento do Windows com Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04cb3-106">The steps in this document rely on a Windows development environment with Visual Studio.</span></span> <span data-ttu-id="04cb3-107">O projeto compilado pode ser enviado para um cluster do HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="04cb3-107">The compiled project can be submitted to a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="04cb3-108">Somente os clusters baseados em Linux criados depois de 28/10/2016 são compatíveis com as topologias do SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="04cb3-108">Only Linux-based clusters created after 10/28/2016 support SCP.NET topologies.</span></span>
>
> <span data-ttu-id="04cb3-109">Para usar uma topologia do C# com um cluster baseado em Linux, atualize o pacote NuGet Microsoft.SCP.Net.SDK usado pelo seu projeto para a versão 0.10.0.6 ou superior.</span><span class="sxs-lookup"><span data-stu-id="04cb3-109">To use a C# topology with a Linux-based cluster, update the Microsoft.SCP.Net.SDK NuGet package used by your project to version 0.10.0.6 or higher.</span></span> <span data-ttu-id="04cb3-110">A versão do pacote também deve coincidir com a versão principal do Storm instalada no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04cb3-110">The version of the package must also match the major version of Storm installed on HDInsight.</span></span> <span data-ttu-id="04cb3-111">Por exemplo, o HDInsight versões 3.3 e 3.4 usam o Storm versão 0.10.x, enquanto o HDInsight 3.5 usa o Storm 1.0. x.</span><span class="sxs-lookup"><span data-stu-id="04cb3-111">For example, Storm on HDInsight versions 3.3 and 3.4 use Storm version 0.10.x, while HDInsight 3.5 uses Storm 1.0.x.</span></span>
>
> <span data-ttu-id="04cb3-112">As topologias C# em clusters baseados em Linux devem usar o .NET 4.5 e o Mono para execução no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04cb3-112">C# topologies on Linux-based clusters must use .NET 4.5, and use Mono to run on the HDInsight cluster.</span></span> <span data-ttu-id="04cb3-113">A maioria das coisas funciona.</span><span class="sxs-lookup"><span data-stu-id="04cb3-113">Most things work.</span></span> <span data-ttu-id="04cb3-114">No entanto, você deve verificar o documento [Compatibilidade do Mono](http://www.mono-project.com/docs/about-mono/compatibility/) em busca de possíveis incompatibilidades.</span><span class="sxs-lookup"><span data-stu-id="04cb3-114">However you should check the [Mono Compatibility](http://www.mono-project.com/docs/about-mono/compatibility/) document for potential incompatibilities.</span></span>
>
> <span data-ttu-id="04cb3-115">Para obter uma versão Java deste projeto, que funciona com HDInsight baseado em Windows ou Linux, confira [Processar eventos dos Hubs de Eventos do Azure com Storm no HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span><span class="sxs-lookup"><span data-stu-id="04cb3-115">For a Java version of this project, which works with Linux-based or Windows-based HDInsight, see [Process events from Azure Event Hubs with Storm on HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04cb3-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="04cb3-116">Prerequisites</span></span>

* <span data-ttu-id="04cb3-117">Um usuário do Azure Active Directory com acesso ao [Power BI](https://powerbi.com).</span><span class="sxs-lookup"><span data-stu-id="04cb3-117">An Azure Active Directory user with [Power BI](https://powerbi.com) access.</span></span>
* <span data-ttu-id="04cb3-118">Um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04cb3-118">An HDInsight cluster.</span></span> <span data-ttu-id="04cb3-119">Para obter mais informações, confira [Introdução ao Storm no HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="04cb3-119">For more information, see [Get started with Storm on HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="04cb3-120">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="04cb3-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="04cb3-121">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="04cb3-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="04cb3-122">Visual Studio (uma das seguintes versões a seguir)</span><span class="sxs-lookup"><span data-stu-id="04cb3-122">Visual Studio (one of the following versions)</span></span>

  * <span data-ttu-id="04cb3-123">Visual Studio 2012 com [atualização 4](http://www.microsoft.com/download/details.aspx?id=39305)</span><span class="sxs-lookup"><span data-stu-id="04cb3-123">Visual Studio 2012 with [update 4](http://www.microsoft.com/download/details.aspx?id=39305)</span></span>
  * <span data-ttu-id="04cb3-124">Visual Studio 2013 com [atualização 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="04cb3-124">Visual Studio 2013 with [update 4](http://www.microsoft.com/download/details.aspx?id=44921) or [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?linkid=517284&clcid=0x409)</span></span>
  * [<span data-ttu-id="04cb3-125">Visual Studio 2015</span><span class="sxs-lookup"><span data-stu-id="04cb3-125">Visual Studio 2015</span></span>](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
  * <span data-ttu-id="04cb3-126">Visual Studio 2017 (qualquer edição)</span><span class="sxs-lookup"><span data-stu-id="04cb3-126">Visual Studio 2017 (any edition)</span></span>

* <span data-ttu-id="04cb3-127">Ferramentas do HDInsight para o Visual Studio: consulte [Comece a usar as Ferramentas do HDInsight para o Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) para obter informações sobre a instalação.</span><span class="sxs-lookup"><span data-stu-id="04cb3-127">The HDInsight Tools for Visual Studio: See [Get started using the HDInsight Tools for Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) for information on installation information.</span></span>

## <a name="how-it-works"></a><span data-ttu-id="04cb3-128">Como ele funciona</span><span class="sxs-lookup"><span data-stu-id="04cb3-128">How it works</span></span>

<span data-ttu-id="04cb3-129">Este exemplo contém uma topologia do Storm em C# que gera aleatoriamente dados de log do IIS (Serviços de Informações da Internet).</span><span class="sxs-lookup"><span data-stu-id="04cb3-129">This example contains a C# Storm topology that randomly generates Internet Information Services (IIS) log data.</span></span> <span data-ttu-id="04cb3-130">Esses dados são gravados em um Banco de Dados SQL e, por meio dele, são usados para gerar relatórios no Power BI.</span><span class="sxs-lookup"><span data-stu-id="04cb3-130">This data is then written to a SQL Database, and from there it is used to generate reports in Power BI.</span></span>

<span data-ttu-id="04cb3-131">Os arquivos a seguir implementam a funcionalidade principal desse exemplo:</span><span class="sxs-lookup"><span data-stu-id="04cb3-131">The following files implement the main functionality of this example:</span></span>

* <span data-ttu-id="04cb3-132">**SqlAzureBolt.cs**: grava informações produzidas na topologia do Storm no Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="04cb3-132">**SqlAzureBolt.cs**: Writes information produced in the Storm topology to SQL Database.</span></span>
* <span data-ttu-id="04cb3-133">**IISLogsTable.sql**: as instruções Transact-SQL usadas para gerar o banco de dados no qual os dados são armazenados.</span><span class="sxs-lookup"><span data-stu-id="04cb3-133">**IISLogsTable.sql**: The Transact-SQL statements used to generate the database that the data is stored in.</span></span>

> [!WARNING]
> <span data-ttu-id="04cb3-134">Criar a tabela no Banco de Dados SQL antes de iniciar a topologia em seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04cb3-134">Create the table in SQL Database before starting the topology on your HDInsight cluster.</span></span>

## <a name="download-the-example"></a><span data-ttu-id="04cb3-135">Baixar o exemplo</span><span class="sxs-lookup"><span data-stu-id="04cb3-135">Download the example</span></span>

<span data-ttu-id="04cb3-136">Baixe o [exemplo do Power BI do Storm em C# do HDInsight](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span><span class="sxs-lookup"><span data-stu-id="04cb3-136">Download the [HDInsight C# Storm Power BI example](https://github.com/Azure-Samples/hdinsight-dotnet-storm-powerbi).</span></span> <span data-ttu-id="04cb3-137">Para baixá-lo, use uma bifurcação/clone-o usando [git](http://git-scm.com/)ou use o link de **Download** link para baixar um .zip do arquivo.</span><span class="sxs-lookup"><span data-stu-id="04cb3-137">To download it, either fork/clone it using [git](http://git-scm.com/), or use the **Download** link to download a .zip of the archive.</span></span>

## <a name="create-a-database"></a><span data-ttu-id="04cb3-138">Criar um banco de dados</span><span class="sxs-lookup"><span data-stu-id="04cb3-138">Create a database</span></span>

1. <span data-ttu-id="04cb3-139">Use as etapas no documento [Tutorial do Banco de Dados SQL](../sql-database/sql-database-get-started.md) para criar um novo banco de dados.</span><span class="sxs-lookup"><span data-stu-id="04cb3-139">To create a database, use the steps in the [SQL Database tutorial](../sql-database/sql-database-get-started.md) document.</span></span>

2. <span data-ttu-id="04cb3-140">Conecte-se ao banco de dados seguindo as etapas no documento [Conectar-se ao Banco de Dados SQL com o Visual Studio](../sql-database/sql-database-connect-query.md).</span><span class="sxs-lookup"><span data-stu-id="04cb3-140">Connect to the database by following the steps in the [Connect to a SQL Database with Visual Studio](../sql-database/sql-database-connect-query.md) document.</span></span>

3. <span data-ttu-id="04cb3-141">No Pesquisador de Objetos, clique com o botão direito do mouse no banco de dados e selecione **Nova Consulta**.</span><span class="sxs-lookup"><span data-stu-id="04cb3-141">In Object Explorer, right-click the database and select  **New Query**.</span></span> <span data-ttu-id="04cb3-142">Cole o conteúdo do arquivo **IISLogsTable.sql** incluído no projeto baixado na janela de consulta e use Ctrl + Shift + E para executar a consulta.</span><span class="sxs-lookup"><span data-stu-id="04cb3-142">Paste the contents of the **IISLogsTable.sql** file included in the downloaded project into the query window, and then use Ctrl + Shift + E to execute the query.</span></span> <span data-ttu-id="04cb3-143">Você deve receber uma mensagem de que os comandos foram concluídos com êxito.</span><span class="sxs-lookup"><span data-stu-id="04cb3-143">You should receive a message that the commands completed successfully.</span></span>

## <a name="configure-the-sample"></a><span data-ttu-id="04cb3-144">Configurar o exemplo</span><span class="sxs-lookup"><span data-stu-id="04cb3-144">Configure the sample</span></span>

1. <span data-ttu-id="04cb3-145">No [Portal do Azure](https://portal.azure.com), selecione seu Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="04cb3-145">From the [Azure portal](https://portal.azure.com), select your SQL database.</span></span> <span data-ttu-id="04cb3-146">Na seção **Fundamentos** da folha Banco de Dados SQL, selecione **Mostrar cadeias de conexão de banco de dados**.</span><span class="sxs-lookup"><span data-stu-id="04cb3-146">From the **Essentials** section of the SQL database blade, select **Show database connection strings**.</span></span> <span data-ttu-id="04cb3-147">Na lista exibida, copie as informações de **ADO.NET (autenticação do SQL)** .</span><span class="sxs-lookup"><span data-stu-id="04cb3-147">From the list that appears, copy the **ADO.NET (SQL authentication)** information.</span></span>

2. <span data-ttu-id="04cb3-148">Abra o exemplo no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="04cb3-148">Open the sample in Visual Studio.</span></span> <span data-ttu-id="04cb3-149">No **Gerenciador de Soluções**, abra o arquivo **App.config** e localize a seguinte entrada:</span><span class="sxs-lookup"><span data-stu-id="04cb3-149">From **Solution Explorer**, open the **App.config** file, and then find the following entry:</span></span>

        <add key="SqlAzureConnectionString" value="##TOBEFILLED##" />

    <span data-ttu-id="04cb3-150">Substitua o valor **##TOBEFILLED##** valor pela cadeia de conexão de banco de dados copiada na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="04cb3-150">Replace the **##TOBEFILLED##** value with the database connection string copied in the previous step.</span></span> <span data-ttu-id="04cb3-151">Substitua **{your\_username}** e **{your\_password}** pelo nome de usuário e pela senha do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="04cb3-151">Replace **{your\_username}** and **{your\_password}** with the username and password for the database.</span></span>

3. <span data-ttu-id="04cb3-152">Salve e feche os arquivos.</span><span class="sxs-lookup"><span data-stu-id="04cb3-152">Save and close the files.</span></span>

## <a name="deploy-the-sample"></a><span data-ttu-id="04cb3-153">Implantar o exemplo</span><span class="sxs-lookup"><span data-stu-id="04cb3-153">Deploy the sample</span></span>

1. <span data-ttu-id="04cb3-154">No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **StormToSQL** e selecione **Enviar para o Storm no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="04cb3-154">From **Solution Explorer**, right-click the **StormToSQL** project and select **Submit to Storm on HDInsight**.</span></span> <span data-ttu-id="04cb3-155">Selecione o cluster HDInsight no menu suspenso **Cluster Storm** .</span><span class="sxs-lookup"><span data-stu-id="04cb3-155">Select the HDInsight cluster from the **Storm Cluster** dropdown dialog.</span></span>

   > [!NOTE]
   > <span data-ttu-id="04cb3-156">Pode levar alguns segundos para a lista suspensa **Cluster Storm** ser populada com os nomes de servidor.</span><span class="sxs-lookup"><span data-stu-id="04cb3-156">It may take a few seconds for the **Storm Cluster** dropdown to populate with server names.</span></span>
   >
   > <span data-ttu-id="04cb3-157">Se solicitado, insira as credenciais de logon para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="04cb3-157">If prompted, enter the login credentials for your Azure subscription.</span></span> <span data-ttu-id="04cb3-158">Se você tiver mais de uma assinatura, faça o logon naquela que contém seu Storm no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04cb3-158">If you have more than one subscription, log in to the one that contains your Storm on HDInsight cluster.</span></span>

2. <span data-ttu-id="04cb3-159">Depois que a topologia é enviada, o __Visualizador de Topologia__ é exibido.</span><span class="sxs-lookup"><span data-stu-id="04cb3-159">When the topology has been submitted, the __Topology Viewer__ appears.</span></span> <span data-ttu-id="04cb3-160">Para exibir essa topologia, selecione a entrada SqlAzureWriterTopology na lista.</span><span class="sxs-lookup"><span data-stu-id="04cb3-160">To view this topology, select the SqlAzureWriterTopology entry from the list.</span></span>

    ![As topologias, com a topologia selecionada](./media/hdinsight-storm-power-bi-topology/topologyview.png)

    <span data-ttu-id="04cb3-162">Você pode usar esta exibição para ver informações sobre a topologia ou clicar duas vezes em uma entrada (como SqlAzureBolt) para ver as informações específicas de um componente na topologia.</span><span class="sxs-lookup"><span data-stu-id="04cb3-162">You can use this view to see information on the topology, or double-click an entry (such as the SqlAzureBolt) to see information specific to a component in the topology.</span></span>

3. <span data-ttu-id="04cb3-163">Depois que a topologia estiver executado por alguns minutos, volte para a janela de consulta do SQL usada para criar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="04cb3-163">After the topology has ran for a few minutes, return to the SQL query window you used to create the database.</span></span> <span data-ttu-id="04cb3-164">Substitua as instruções existentes pela seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="04cb3-164">Replace the existing statements with the following query:</span></span>

        select * from iislogs;

    <span data-ttu-id="04cb3-165">Use Ctrl + Shift + E para executar a consulta e deverá receber resultados semelhantes aos dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="04cb3-165">Use Ctrl + Shift + E to execute the query, and you should receive results similar to the following data:</span></span>

        1    2016-05-27 17:57:14.797    255.255.255.255    /bar    GET    200
        2    2016-05-27 17:57:14.843    127.0.0.1    /spam/eggs    POST    500
        3    2016-05-27 17:57:14.850    123.123.123.123    /eggs    DELETE    200
        4    2016-05-27 17:57:14.853    127.0.0.1    /foo    POST    404
        5    2016-05-27 17:57:14.853    10.9.8.7    /bar    GET    200
        6    2016-05-27 17:57:14.857    192.168.1.1    /spam    DELETE    200

    <span data-ttu-id="04cb3-166">Esses dados foram gravados da topologia do Storm.</span><span class="sxs-lookup"><span data-stu-id="04cb3-166">This data has been written from the Storm topology.</span></span>

## <a name="create-a-report"></a><span data-ttu-id="04cb3-167">Criar um relatório</span><span class="sxs-lookup"><span data-stu-id="04cb3-167">Create a report</span></span>

1. <span data-ttu-id="04cb3-168">Conecte-se ao [conector do Banco de Dados SQL do Azure](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="04cb3-168">Connect to the [Azure SQL Database connector](https://app.powerbi.com/getdata/bigdata/azure-sql-database-with-live-connect) for Power BI.</span></span> 

2. <span data-ttu-id="04cb3-169">Dentro de **Bancos de Dados**, selecione **Obter**.</span><span class="sxs-lookup"><span data-stu-id="04cb3-169">Within **Databases**, select **Get**.</span></span>

3. <span data-ttu-id="04cb3-170">Selecione **Banco de Dados SQL do Azure** e **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="04cb3-170">Select **Azure SQL Database**, and then select **Connect**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="04cb3-171">Você poderá ser solicitado a baixar o Power BI Desktop para continuar.</span><span class="sxs-lookup"><span data-stu-id="04cb3-171">You may be asked to download the Power BI Desktop to continue.</span></span> <span data-ttu-id="04cb3-172">Nesse caso, siga estas etapas para se conectar:</span><span class="sxs-lookup"><span data-stu-id="04cb3-172">If so, use the following steps to connect:</span></span>
    >
    > 1. <span data-ttu-id="04cb3-173">Abra o Power BI Desktop e selecione __Obter dados__.</span><span class="sxs-lookup"><span data-stu-id="04cb3-173">Open Power BI Desktop and select __Get Data__.</span></span>
    > <span data-ttu-id="04cb3-174">2 Selecione __Azure__ e, em seguida, __banco de dados SQL do Azure__.</span><span class="sxs-lookup"><span data-stu-id="04cb3-174">2  Select __Azure__, and then __Azure SQL database__.</span></span>

4. <span data-ttu-id="04cb3-175">Insira as informações para se conectar ao seu Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="04cb3-175">Enter the information to connect to your Azure SQL Database.</span></span> <span data-ttu-id="04cb3-176">Você pode encontrar essas informações visitando o [Portal do Azure](https://portal.azure.com) e selecionando o Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="04cb3-176">You can find this information by visiting the [Azure portal](https://portal.azure.com) and selecting your SQL database.</span></span>

   > [!NOTE]
   > <span data-ttu-id="04cb3-177">Você também pode definir o intervalo de atualização e filtros personalizados usando **Habilitar Opções Avançadas** na caixa de diálogo de conexão.</span><span class="sxs-lookup"><span data-stu-id="04cb3-177">You can also set the refresh interval and custom filters by using **Enable Advanced Options** from the connect dialog.</span></span>

5. <span data-ttu-id="04cb3-178">Depois de ter se conectado, você verá um novo conjunto de dados com o mesmo nome que o banco de dados ao qual está conectado.</span><span class="sxs-lookup"><span data-stu-id="04cb3-178">After you've connected, you will see a new dataset with the same name as the database you connected to.</span></span> <span data-ttu-id="04cb3-179">Selecione o conjunto de dados para começar a criar um relatório.</span><span class="sxs-lookup"><span data-stu-id="04cb3-179">Select the dataset to begin designing a report.</span></span>

6. <span data-ttu-id="04cb3-180">Em **Campos**, expanda a entrada **IISLOGS**.</span><span class="sxs-lookup"><span data-stu-id="04cb3-180">From **Fields**, expand the **IISLOGS** entry.</span></span> <span data-ttu-id="04cb3-181">Para criar um relatório que liste as derivações do URI, marque a caixa de seleção para **URISTEM**.</span><span class="sxs-lookup"><span data-stu-id="04cb3-181">To create a report that lists the URI stems, select the checkbox for **URISTEM**.</span></span>

    ![Criando um relatório](./media/hdinsight-storm-power-bi-topology/createreport.png)

7. <span data-ttu-id="04cb3-183">Em seguida, arraste **METHOD** para o relatório.</span><span class="sxs-lookup"><span data-stu-id="04cb3-183">Next, drag **METHOD** to the report.</span></span> <span data-ttu-id="04cb3-184">O relatório é atualizado para listar as derivações e o método HTTP correspondente usado para a solicitação HTTP.</span><span class="sxs-lookup"><span data-stu-id="04cb3-184">The report updates to list the stems and the corresponding HTTP method used for the HTTP request.</span></span>

    ![adicionando os dados de método](./media/hdinsight-storm-power-bi-topology/uristemandmethod.png)

8. <span data-ttu-id="04cb3-186">Na coluna **Visualizações**, selecione o ícone **Campos** e selecione a seta para baixo ao lado de **METHOD** na seção **Valores**.</span><span class="sxs-lookup"><span data-stu-id="04cb3-186">From the **Visualizations** column, select the **Fields** icon, and then select the down arrow next to **METHOD** in the **Values** section.</span></span> <span data-ttu-id="04cb3-187">Para exibir uma contagem de quantas vezes um URI pode ser acessado, selecione **Contagem**.</span><span class="sxs-lookup"><span data-stu-id="04cb3-187">To display a count of how many times a URI has been accessed, select **Count**.</span></span>

    ![Mudando para uma contagem de métodos](./media/hdinsight-storm-power-bi-topology/count.png)

9. <span data-ttu-id="04cb3-189">Em seguida, selecione o **Gráfico de colunas empilhadas** para alterar como as informações são exibidas.</span><span class="sxs-lookup"><span data-stu-id="04cb3-189">Next, select the **Stacked column chart** to change how the information is displayed.</span></span>

    ![Mudando para um gráfico empilhado](./media/hdinsight-storm-power-bi-topology/stackedcolumn.png)

10. <span data-ttu-id="04cb3-191">Para salvar o relatório, selecione **Salvar** e digite um nome para o relatório.</span><span class="sxs-lookup"><span data-stu-id="04cb3-191">To save the report, select **Save** and enter a name for the report.</span></span>

## <a name="stop-the-topology"></a><span data-ttu-id="04cb3-192">Parar a topologia</span><span class="sxs-lookup"><span data-stu-id="04cb3-192">Stop the topology</span></span>

<span data-ttu-id="04cb3-193">A topologia continuará sendo executada até você interrompê-la ou excluir o Storm no cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="04cb3-193">The topology continues to run until you stop it or delete the Storm on HDInsight cluster.</span></span> <span data-ttu-id="04cb3-194">Para interromper a topologia, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="04cb3-194">To stop the topology, perform the following steps:</span></span>

1. <span data-ttu-id="04cb3-195">No Visual Studio, volte ao visualizador de topologia e selecione a topologia.</span><span class="sxs-lookup"><span data-stu-id="04cb3-195">In Visual Studio, return to the topology viewer and select the topology.</span></span>

2. <span data-ttu-id="04cb3-196">Selecione o botão **Eliminar** para interromper a topologia.</span><span class="sxs-lookup"><span data-stu-id="04cb3-196">Select the **Kill** button to stop the topology.</span></span>

    ![Botão Eliminar no resumo da topologia](./media/hdinsight-storm-power-bi-topology/killtopology.png)

## <a name="delete-your-cluster"></a><span data-ttu-id="04cb3-198">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="04cb3-198">Delete your cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a><span data-ttu-id="04cb3-199">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04cb3-199">Next steps</span></span>

<span data-ttu-id="04cb3-200">Neste documento, você aprendeu como enviar dados de uma topologia do Storm para o Banco de Dados SQL e exibir os dados usando o Power BI.</span><span class="sxs-lookup"><span data-stu-id="04cb3-200">In this document, you learned how to send data from a Storm topology to SQL Database, then visualize the data using Power BI.</span></span> <span data-ttu-id="04cb3-201">Para obter informações sobre como trabalhar com outras tecnologias do Azure usando o Storm no HDInsight, consulte o seguinte documento:</span><span class="sxs-lookup"><span data-stu-id="04cb3-201">For information on how to work with other Azure technologies using Storm on HDInsight, see the following document:</span></span>

* [<span data-ttu-id="04cb3-202">Topologias de exemplo para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="04cb3-202">Example topologies for Storm on HDInsight</span></span>](hdinsight-storm-example-topology.md)
