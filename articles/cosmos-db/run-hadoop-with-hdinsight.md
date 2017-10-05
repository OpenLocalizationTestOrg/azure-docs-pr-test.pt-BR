---
title: Executar um trabalho do Hadoop usando o Azure Cosmos DB e o HDInsight | Microsoft Docs
description: Saiba como executar um trabalho simples do Hive, Pig e MapReduce com o Azure Cosmos DB e o Azure HDInsight.
services: cosmos-db
author: dennyglee
manager: jhubbard
editor: mimig
documentationcenter: 
ms.assetid: 06f0ea9d-07cb-4593-a9c5-ab912b62ac42
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 06/08/2017
ms.author: denlee
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 427864fc4e494c19fcda4cfd454a9923499f6337
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <span data-ttu-id="86b88-103"><a name="Azure Cosmos DB-HDInsight"></a>Executar um trabalho do Apache Hive, Pig ou Hadoop usando o Azure Cosmos DB e o HDInsight</span><span class="sxs-lookup"><span data-stu-id="86b88-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="86b88-104">Este tutorial mostra como executar trabalhos do [Apache Hive][apache-hive], [Apache Pig][apache-pig] e [Apache Hadoop][apache-hadoop] MapReduce no Azure HDInsight com o conector para Hadoop do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="86b88-104">This tutorial shows you how to run [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="86b88-105">O conector para Hadoop do Cosmos DB permite que o Cosmos DB atue como uma fonte e um coletor para trabalhos do Hive, Pig e MapReduce.</span><span class="sxs-lookup"><span data-stu-id="86b88-105">Cosmos DB's Hadoop connector allows Cosmos DB to act as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="86b88-106">Este tutorial usará o Cosmos DB como a fonte de dados e o destino para trabalhos do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="86b88-106">This tutorial will use Cosmos DB as both the data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="86b88-107">Depois de concluir este tutorial, você poderá responder às seguintes perguntas:</span><span class="sxs-lookup"><span data-stu-id="86b88-107">After completing this tutorial, you'll be able to answer the following questions:</span></span>

* <span data-ttu-id="86b88-108">Como fazer para carregar dados do Cosmos DB usando um trabalho do Hive, Pig ou MapReduce?</span><span class="sxs-lookup"><span data-stu-id="86b88-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="86b88-109">Como fazer para armazenar dados no Cosmos DB usando um trabalho do Hive, Pig ou MapReduce?</span><span class="sxs-lookup"><span data-stu-id="86b88-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="86b88-110">Recomendamos começar assistindo ao vídeo a seguir, no qual executamos um trabalho do Hive usando o Cosmos DB e o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86b88-110">We recommend getting started by watching the following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="86b88-111">Depois, volte a este artigo, no qual você receberá todos os detalhes de como executar trabalhos analíticos nos dados do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="86b88-111">Then, return to this article, where you'll receive the full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="86b88-112">Este tutorial presume que você tenha experiência anterior com o uso do Apache Hadoop, Hive e/ou Pig.</span><span class="sxs-lookup"><span data-stu-id="86b88-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="86b88-113">Se você estiver começando a usar o Apache Hadoop, Hive e Pig, recomendamos visitar a [Documentação do Apache Hadoop][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="86b88-113">If you are new to Apache Hadoop, Hive, and Pig, we recommend visiting the [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="86b88-114">Este tutorial também pressupõe que você tenha experiência anterior com o Cosmos DB e tenha uma conta do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="86b88-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="86b88-115">Se estiver conhecendo o Cosmos DB agora ou ainda não tiver uma conta do Cosmos DB, confira nossa página [Introdução][getting-started].</span><span class="sxs-lookup"><span data-stu-id="86b88-115">If you are new to Cosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="86b88-116">Não tem tempo para fazer o tutorial e quer apenas a amostra completa de scripts do PowerShell para Hive, Pig e MapReduce?</span><span class="sxs-lookup"><span data-stu-id="86b88-116">Don't have time to complete the tutorial and just want to get the full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="86b88-117">Sem problemas, elas estão [aqui][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="86b88-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="86b88-118">O download contém também arquivos hql, pig e java para essas amostras.</span><span class="sxs-lookup"><span data-stu-id="86b88-118">The download also contains the hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="86b88-119"><a name="NewestVersion"></a>Versão Mais Recente</span><span class="sxs-lookup"><span data-stu-id="86b88-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="86b88-120">Versão do Conector para Hadoop</span><span class="sxs-lookup"><span data-stu-id="86b88-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="86b88-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="86b88-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="86b88-122">URI do script</span><span class="sxs-lookup"><span data-stu-id="86b88-122">Script Uri</span></span></th>
        <td><span data-ttu-id="86b88-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="86b88-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="86b88-124">Data da Modificação</span><span class="sxs-lookup"><span data-stu-id="86b88-124">Date Modified</span></span></th>
        <td><span data-ttu-id="86b88-125">26/04/2016</span><span class="sxs-lookup"><span data-stu-id="86b88-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="86b88-126">Versões do HDInsight para as quais há suporte</span><span class="sxs-lookup"><span data-stu-id="86b88-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="86b88-127">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="86b88-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="86b88-128">Log de alterações</span><span class="sxs-lookup"><span data-stu-id="86b88-128">Change Log</span></span></th>
        <td><span data-ttu-id="86b88-129">Azure Cosmos DB Java SDK atualizado para 1.6.0</span><span class="sxs-lookup"><span data-stu-id="86b88-129">Updated Azure Cosmos DB Java SDK to 1.6.0</span></span></br>
            <span data-ttu-id="86b88-130">Suporte adicionado para coleções particionadas como uma fonte e coletor</span><span class="sxs-lookup"><span data-stu-id="86b88-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="86b88-131"><a name="Prerequisites"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="86b88-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="86b88-132">Antes de seguir as instruções neste tutorial, certifique-se de ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="86b88-132">Before following the instructions in this tutorial, ensure that you have the following:</span></span>

* <span data-ttu-id="86b88-133">Uma conta do Cosmos DB, um banco de dados e uma coleção com documentos.</span><span class="sxs-lookup"><span data-stu-id="86b88-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="86b88-134">Para obter mais informações, consulte [Introdução ao Cosmos DB][getting-started].</span><span class="sxs-lookup"><span data-stu-id="86b88-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="86b88-135">Importe dados de exemplo para sua conta do Cosmos DB com a [ferramenta de importação do Cosmos DB][import-data].</span><span class="sxs-lookup"><span data-stu-id="86b88-135">Import sample data into your Cosmos DB account with the [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="86b88-136">Produtividade.</span><span class="sxs-lookup"><span data-stu-id="86b88-136">Throughput.</span></span> <span data-ttu-id="86b88-137">Leituras e gravações do HDInsight serão contabilizadas de acordo com suas unidades de solicitação alocadas para suas coleções.</span><span class="sxs-lookup"><span data-stu-id="86b88-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="86b88-138">Capacidade para um procedimento armazenado adicional dentro de cada coleção de saída.</span><span class="sxs-lookup"><span data-stu-id="86b88-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="86b88-139">Os procedimentos armazenados são usados para transferir os documentos resultantes.</span><span class="sxs-lookup"><span data-stu-id="86b88-139">The stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="86b88-140">Capacidade para os documentos resultantes dos trabalhos de Hive, Pig ou MapReduce.</span><span class="sxs-lookup"><span data-stu-id="86b88-140">Capacity for the resulting documents from the Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="86b88-141">[*Opcional*] Capacidade para uma coleção adicional.</span><span class="sxs-lookup"><span data-stu-id="86b88-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="86b88-142">Para evitar a criação de uma nova coleção durante um dos trabalhos, você pode imprimir os resultados no StdOut, salvar a saída no seu contêiner WASB ou especificar um coleção que já existe.</span><span class="sxs-lookup"><span data-stu-id="86b88-142">In order to avoid the creation of a new collection during any of the jobs, you can either print the results to stdout, save the output to your WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="86b88-143">Caso você especifique uma coleção existente, novos documentos serão criados dentro da coleção e os documentos existentes serão afetados somente se houver conflitos entre as *IDs*.</span><span class="sxs-lookup"><span data-stu-id="86b88-143">In the case of specifying an existing collection, new documents will be created inside the collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="86b88-144">**O conector substitui automaticamente documentos existentes com conflitos de ID**.</span><span class="sxs-lookup"><span data-stu-id="86b88-144">**The connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="86b88-145">Você pode desativar esse recurso definindo a opção de upsert como falsa.</span><span class="sxs-lookup"><span data-stu-id="86b88-145">You can turn off this feature by setting the upsert option to false.</span></span> <span data-ttu-id="86b88-146">Se upsert estiver definido como falso e houver um conflito, o trabalho do Hadoop falhará, retornando um erro de conflito de ID.</span><span class="sxs-lookup"><span data-stu-id="86b88-146">If upsert is false and a conflict occurs, the Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="86b88-147"><a name="ProvisionHDInsight"></a>Etapa 1: criar um novo cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="86b88-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="86b88-148">Este tutorial usa a Ação de Script do Portal do Azure para personalizar o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86b88-148">This tutorial uses Script Action from the Azure Portal to customize your HDInsight cluster.</span></span> <span data-ttu-id="86b88-149">Nesse tutorial, usaremos o Portal do Azure para criar o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86b88-149">In this tutorial, we will use the Azure Portal to create your HDInsight cluster.</span></span> <span data-ttu-id="86b88-150">Para sabe como usar cmdlets do PowerShell ou o SDK do .NET do HDInsight, veja o artigo [Personalizar clusters HDInsight usando Ação de Script][hdinsight-custom-provision].</span><span class="sxs-lookup"><span data-stu-id="86b88-150">For instructions on how to use PowerShell cmdlets or the HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="86b88-151">Entre no [Portal do Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="86b88-151">Sign in to the [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="86b88-152">Clique em **+Novo** na parte superior do painel de navegação esquerdo e procure por **HDInsight** na barra de pesquisa na folha Novo.</span><span class="sxs-lookup"><span data-stu-id="86b88-152">Click **+ New** on the top of the left navigation, search for **HDInsight** in the top search bar on the New blade.</span></span>
3. <span data-ttu-id="86b88-153">O **HDInsight** publicado pela **Microsoft** aparecerá na parte superior dos Resultados.</span><span class="sxs-lookup"><span data-stu-id="86b88-153">**HDInsight** published by **Microsoft** will appear at the top of the Results.</span></span> <span data-ttu-id="86b88-154">Clique nele, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="86b88-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="86b88-155">Na folha Criar Novo Cluster do HDInsight, insira seu **Nome do Cluster** e selecione a **Assinatura** com a qual você deseja provisionar o recurso.</span><span class="sxs-lookup"><span data-stu-id="86b88-155">On the New HDInsight Cluster create blade, enter your **Cluster Name** and select the **Subscription** you want to provision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="86b88-156">Nome do cluster</span><span class="sxs-lookup"><span data-stu-id="86b88-156">Cluster name</span></span></td><td><span data-ttu-id="86b88-157">Nome do cluster.</span><span class="sxs-lookup"><span data-stu-id="86b88-157">Name the cluster.</span></span><br/>
<span data-ttu-id="86b88-158">O nome DNS deve começar e terminar com um número alfanumérico e pode conter traços.</span><span class="sxs-lookup"><span data-stu-id="86b88-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="86b88-159">O campo deve ser uma cadeia com 3 a 63 caracteres.</span><span class="sxs-lookup"><span data-stu-id="86b88-159">The field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="86b88-160">Nome da assinatura</span><span class="sxs-lookup"><span data-stu-id="86b88-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="86b88-161">Se você tiver mais de uma Assinatura do Azure, selecione a assinatura que hospedará seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86b88-161">If you have more than one Azure Subscription, select the subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="86b88-162">
5. Clique em **Selecionar Tipo de Cluster** e defina as seguintes propriedades para os valores especificados.</span><span class="sxs-lookup"><span data-stu-id="86b88-162">
5. Click **Select Cluster Type** and set the following properties to the specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="86b88-163">Tipo de cluster</span><span class="sxs-lookup"><span data-stu-id="86b88-163">Cluster type</span></span></td><td><span data-ttu-id="86b88-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="86b88-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="86b88-165">Nível do cluster</span><span class="sxs-lookup"><span data-stu-id="86b88-165">Cluster tier</span></span></td><td><span data-ttu-id="86b88-166"><strong>Standard</strong></span><span class="sxs-lookup"><span data-stu-id="86b88-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="86b88-167">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="86b88-167">Operating System</span></span></td><td><span data-ttu-id="86b88-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="86b88-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="86b88-169">Versão</span><span class="sxs-lookup"><span data-stu-id="86b88-169">Version</span></span></td><td><span data-ttu-id="86b88-170">última versão</span><span class="sxs-lookup"><span data-stu-id="86b88-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="86b88-171">Agora, clique em **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="86b88-171">Now, click **SELECT**.</span></span>

    ![Fornecer detalhes do cluster HDInsight inicial do Hadoop][image-customprovision-page1]
6. <span data-ttu-id="86b88-173">Clique em **Credenciais** para definir seu logon e credenciais de acesso remoto.</span><span class="sxs-lookup"><span data-stu-id="86b88-173">Click on **Credentials** to set your login and remote access credentials.</span></span> <span data-ttu-id="86b88-174">Escolha o **Nome de Usuário de Logon do Cluster** e a **Senha de Logon do Cluster**.</span><span class="sxs-lookup"><span data-stu-id="86b88-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="86b88-175">Se você quiser ter um acesso remoto em seu cluster, selecione *sim* na parte inferior da folha e forneça um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="86b88-175">If you want to remote into your cluster, select *yes* at the bottom of the blade and provide a username and password.</span></span>
7. <span data-ttu-id="86b88-176">Clique em **Fonte de Dados** para definir o local principal para o acesso a dados.</span><span class="sxs-lookup"><span data-stu-id="86b88-176">Click on **Data Source** to set your primary location for data access.</span></span> <span data-ttu-id="86b88-177">Escolha o **Método de Seleção** e especifique uma conta de armazenamento já existente ou crie uma nova.</span><span class="sxs-lookup"><span data-stu-id="86b88-177">Choose the **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="86b88-178">Na mesma folha, especifique um **Contêiner Padrão** e um **Local**.</span><span class="sxs-lookup"><span data-stu-id="86b88-178">On the same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="86b88-179">Clique em **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="86b88-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="86b88-180">Selecione um local próximo à região da conta do Cosmos DB para ter um melhor desempenho</span><span class="sxs-lookup"><span data-stu-id="86b88-180">Select a location close to your Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="86b88-181">Clique em **Preços** para selecionar o número e o tipo de nós.</span><span class="sxs-lookup"><span data-stu-id="86b88-181">Click on **Pricing** to select the number and type of nodes.</span></span> <span data-ttu-id="86b88-182">Você poderá manter a configuração padrão e dimensionar o número de nós de Trabalho mais tarde.</span><span class="sxs-lookup"><span data-stu-id="86b88-182">You can keep the default configuration and scale the number of Worker nodes later on.</span></span>
10. <span data-ttu-id="86b88-183">Clique em **Configuração Opcional** e, em seguida, em **Ações de Script** na folha Configuração Opcional.</span><span class="sxs-lookup"><span data-stu-id="86b88-183">Click **Optional Configuration**, then **Script Actions** in the Optional Configuration Blade.</span></span>

     <span data-ttu-id="86b88-184">Nas Ações de Script, digite as informações a seguir para personalizar o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86b88-184">In Script Actions, enter the following information to customize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="86b88-185">Propriedade</span><span class="sxs-lookup"><span data-stu-id="86b88-185">Property</span></span></th><th><span data-ttu-id="86b88-186">Valor</span><span class="sxs-lookup"><span data-stu-id="86b88-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="86b88-187">Nome</span><span class="sxs-lookup"><span data-stu-id="86b88-187">Name</span></span></td>
             <td><span data-ttu-id="86b88-188">Especifique um nome para a ação de script.</span><span class="sxs-lookup"><span data-stu-id="86b88-188">Specify a name for the script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="86b88-189">URI do script</span><span class="sxs-lookup"><span data-stu-id="86b88-189">Script URI</span></span></td>
             <td><span data-ttu-id="86b88-190">Especifique o URI para o script que é chamado para personalizar o cluster.</span><span class="sxs-lookup"><span data-stu-id="86b88-190">Specify the URI to the script that is invoked to customize the cluster.</span></span></br></br>
<span data-ttu-id="86b88-191">Insira:</span><span class="sxs-lookup"><span data-stu-id="86b88-191">Please enter:</span></span> </br> <span data-ttu-id="86b88-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="86b88-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="86b88-193">Principal</span><span class="sxs-lookup"><span data-stu-id="86b88-193">Head</span></span></td>
             <td><span data-ttu-id="86b88-194">Clique na caixa de seleção para executar o script do PowerShell no nó Principal.</span><span class="sxs-lookup"><span data-stu-id="86b88-194">Click the checkbox to run the PowerShell script onto the Head node.</span></span></br></br><span data-ttu-id="86b88-195">
             <strong>Marque essa caixa de seleção</strong>.</span><span class="sxs-lookup"><span data-stu-id="86b88-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="86b88-196">Trabalho</span><span class="sxs-lookup"><span data-stu-id="86b88-196">Worker</span></span></td>
             <td><span data-ttu-id="86b88-197">Clique na caixa de seleção para executar o script do PowerShell no nó Trabalho.</span><span class="sxs-lookup"><span data-stu-id="86b88-197">Click the checkbox to run the PowerShell script onto the Worker node.</span></span></br></br><span data-ttu-id="86b88-198">
             <strong>Marque essa caixa de seleção</strong>.</span><span class="sxs-lookup"><span data-stu-id="86b88-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="86b88-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="86b88-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="86b88-200">Clique na caixa de seleção para executar o script do PowerShell no nó Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="86b88-200">Click the checkbox to run the PowerShell script onto the Zookeeper.</span></span></br></br><span data-ttu-id="86b88-201">
             <strong>Não é necessário</strong>.</span><span class="sxs-lookup"><span data-stu-id="86b88-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="86b88-202">parâmetros</span><span class="sxs-lookup"><span data-stu-id="86b88-202">Parameters</span></span></td>
             <td><span data-ttu-id="86b88-203">Especifique os parâmetros, se exigido pelo script.</span><span class="sxs-lookup"><span data-stu-id="86b88-203">Specify the parameters, if required by the script.</span></span></br></br><span data-ttu-id="86b88-204">
             <strong>Nenhum parâmetro necessário</strong>.</span><span class="sxs-lookup"><span data-stu-id="86b88-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="86b88-205">
11. Criar um novo **Grupo de Recursos** ou use um Grupo de Recursos existente em sua Assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="86b88-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="86b88-206">12.</span><span class="sxs-lookup"><span data-stu-id="86b88-206">12.</span></span> <span data-ttu-id="86b88-207">Agora, marque **Fixar no painel** para controlar sua implantação e clique em **Criar**!</span><span class="sxs-lookup"><span data-stu-id="86b88-207">Now, check **Pin to dashboard** to track its deployment and click **Create**!</span></span>

## <span data-ttu-id="86b88-208"><a name="InstallCmdlets"></a>Etapa 2: instalar e configurar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="86b88-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="86b88-209">Instale o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="86b88-209">Install Azure PowerShell.</span></span> <span data-ttu-id="86b88-210">As instruções podem ser encontradas [aqui][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="86b88-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="86b88-211">Como alternativa, só para consultas Hive, você pode usar o Editor de Hive online do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86b88-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="86b88-212">Para fazer isso, entre no [Portal do Azure][azure-portal] e clique em **HDInsight** no painel esquerdo para exibir uma lista dos clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86b88-212">To do so, sign in to the [Azure Portal][azure-portal], click **HDInsight** on the left pane to view a list of your HDInsight clusters.</span></span> <span data-ttu-id="86b88-213">Clique no cluster no qual deseja executar consultas Hive e clique em **Console de Consulta**.</span><span class="sxs-lookup"><span data-stu-id="86b88-213">Click the cluster you want to run Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="86b88-214">Abra o Ambiente de Script Integrado do PowerShell do Azure:</span><span class="sxs-lookup"><span data-stu-id="86b88-214">Open the Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="86b88-215">Em um computador com Windows 8 ou Windows Server 2012 ou posterior, você pode usar a Pesquisa interna.</span><span class="sxs-lookup"><span data-stu-id="86b88-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use the built-in Search.</span></span> <span data-ttu-id="86b88-216">Na tela Inicial, digite **powershell ise** e clique em **Inserir**.</span><span class="sxs-lookup"><span data-stu-id="86b88-216">From the Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="86b88-217">Em um computador com uma versão anterior ao Windows 8 ou ao Windows Server 2012, use o menu Iniciar.</span><span class="sxs-lookup"><span data-stu-id="86b88-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use the Start menu.</span></span> <span data-ttu-id="86b88-218">No menu Iniciar, digite **Prompt de Comando** na caixa de pesquisa e, na lista de resultados, clique em **Prompt de Comando**.</span><span class="sxs-lookup"><span data-stu-id="86b88-218">From the Start menu, type **Command Prompt** in the search box, then in the list of results, click **Command Prompt**.</span></span> <span data-ttu-id="86b88-219">No Prompt de Comando, digite **powershell_ise** e clique em **Inserir**.</span><span class="sxs-lookup"><span data-stu-id="86b88-219">In the Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="86b88-220">Adicione sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="86b88-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="86b88-221">No Painel do Console, digite **Add-AzureAccount** e clique em **Inserir**.</span><span class="sxs-lookup"><span data-stu-id="86b88-221">In the Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="86b88-222">Digite o endereço de email associado à sua assinatura do Azure e clique em **Continuar**.</span><span class="sxs-lookup"><span data-stu-id="86b88-222">Type in the email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="86b88-223">Digite a senha de sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="86b88-223">Type in the password for your Azure subscription.</span></span>
   4. <span data-ttu-id="86b88-224">Clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="86b88-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="86b88-225">O diagrama a seguir identifica as partes importantes do seu Ambiente de Script de PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="86b88-225">The following diagram identifies the important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Diagrama do PowerShell do Azure][azure-powershell-diagram]

## <span data-ttu-id="86b88-227"><a name="RunHive"></a>Etapa 3: Executar um trabalho do Hive usando o Cosmos DB e o HDInsight</span><span class="sxs-lookup"><span data-stu-id="86b88-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="86b88-228">Todas as variáveis indicadas entre < > devem ser preenchidas usando suas configurações.</span><span class="sxs-lookup"><span data-stu-id="86b88-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="86b88-229">Defina as seguintes variáveis no seu Painel de Script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86b88-229">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, the Azure Storage account and container that is used for the default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide the HDInsight cluster name where you want to run the Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="86b88-230">Vamos começar pela cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="86b88-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="86b88-231">Vamos escrever uma consulta do Hive que usa todas as IDs exclusivas (_rid) e os carimbos de data/hora (_ts) gerados pelo sistema de documentos de uma coleção do Azure Cosmos DB, registra todos os documentos por minuto e armazena os resultados em uma nova coleção do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="86b88-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="86b88-232">Primeiro, vamos criar uma tabela Hive por meio da coleção do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="86b88-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="86b88-233">Adicione o seguinte trecho de código ao painel de Script do PowerShell <strong>após</strong> o trecho de código do n.º 1.</span><span class="sxs-lookup"><span data-stu-id="86b88-233">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="86b88-234">Inclua o parâmetro opcional DocumentDB.query para limitar os documentos a somente _ts e _rid.</span><span class="sxs-lookup"><span data-stu-id="86b88-234">Make sure you include the optional DocumentDB.query parameter t trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="86b88-235">**Ter nomeado o DocumentDB.inputCollections não foi um erro.**</span><span class="sxs-lookup"><span data-stu-id="86b88-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="86b88-236">Sim, nós podemos adicionar várias coleções como entrada:</span><span class="sxs-lookup"><span data-stu-id="86b88-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> The collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB the query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="86b88-237">Em seguida, vamos criar uma tabela Hive para a coleção de saída.</span><span class="sxs-lookup"><span data-stu-id="86b88-237">Next, let's create a Hive table for the output collection.</span></span> <span data-ttu-id="86b88-238">As propriedades do documento de saída serão o mês, dia, hora, minuto e o número total de ocorrências.</span><span class="sxs-lookup"><span data-stu-id="86b88-238">The output document properties will be the month, day, hour, minute, and the total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="86b88-239">**Mais uma vez, ter nomeado o DocumentDB.outputCollections não foi um erro.**</span><span class="sxs-lookup"><span data-stu-id="86b88-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="86b88-240">Sim, nós podemos adicionar várias coleções como saída:</span><span class="sxs-lookup"><span data-stu-id="86b88-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="86b88-241">'*DocumentDB.outputCollections*' = '*\<Nome da Coleção de Saída do DocumentDB 1\>*,*\<Nome da Coleção de Saída do DocumentDB 2\>*'</span><span class="sxs-lookup"><span data-stu-id="86b88-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="86b88-242">Os nomes de coleção são separados sem espaços, usando apenas uma única vírgula.</span><span class="sxs-lookup"><span data-stu-id="86b88-242">The collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="86b88-243">Os documentos são distribuídos por round robin entre várias coleções.</span><span class="sxs-lookup"><span data-stu-id="86b88-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="86b88-244">Um lote de documentos será armazenado em uma coleção, um segundo lote de documentos será armazenado na coleção seguinte e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="86b88-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for the output data to DocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="86b88-245">Por fim, vamos classificar os documentos por mês, dia, hora e minuto e inserir os resultados na tabela Hive de saída.</span><span class="sxs-lookup"><span data-stu-id="86b88-245">Finally, let's tally the documents by month, day, hour, and minute and insert the results back into the output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="86b88-246">Adicione o trecho de script a seguir para criar uma definição de trabalho Hive por meio da consulta anterior.</span><span class="sxs-lookup"><span data-stu-id="86b88-246">Add the following script snippet to create a Hive job definition from the previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="86b88-247">Você também pode usar a opção -File para especificar um arquivo de script HiveQL no HDFS.</span><span class="sxs-lookup"><span data-stu-id="86b88-247">You can also use the -File switch to specify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="86b88-248">Adicione o trecho a seguir para salvar a hora de início e enviar o trabalho Hive.</span><span class="sxs-lookup"><span data-stu-id="86b88-248">Add the following snippet to save the start time and submit the Hive job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="86b88-249">Adicione o seguinte para aguardar a conclusão do trabalho Hive.</span><span class="sxs-lookup"><span data-stu-id="86b88-249">Add the following to wait for the Hive job to complete.</span></span>

        # Wait for the Hive job to complete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="86b88-250">Adicione o seguinte para imprimir a saída padrão e os horários de início e fim.</span><span class="sxs-lookup"><span data-stu-id="86b88-250">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="86b88-251">**Execute** seu novo script!</span><span class="sxs-lookup"><span data-stu-id="86b88-251">**Run** your new script!</span></span> <span data-ttu-id="86b88-252">**Clique** no botão de execução verde.</span><span class="sxs-lookup"><span data-stu-id="86b88-252">**Click** the green execute button.</span></span>
8. <span data-ttu-id="86b88-253">Confira os resultados.</span><span class="sxs-lookup"><span data-stu-id="86b88-253">Check the results.</span></span> <span data-ttu-id="86b88-254">Faça logon no [Portal do Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="86b88-254">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="86b88-255">Clique em <strong>Procurar</strong> no painel do lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="86b88-255">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
   2. <span data-ttu-id="86b88-256">Clique em <strong>tudo</strong> na parte superior direita no painel de navegação.</span><span class="sxs-lookup"><span data-stu-id="86b88-256">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
   3. <span data-ttu-id="86b88-257">Localize e clique em <strong>Contas do Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="86b88-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="86b88-258">Em seguida, encontre sua <strong>Conta do Azure Cosmos DB</strong>, depois o <strong>Banco de dados do Azure Cosmos DB</strong> e sua <strong>Coleção do Azure Cosmos DB</strong> associada à coleção de saída especificada no trabalho na consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="86b88-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="86b88-259">Por fim, clique em <strong>Gerenciador de Documentos</strong> abaixo de <strong>Ferramentas de Desenvolvedor</strong>.</span><span class="sxs-lookup"><span data-stu-id="86b88-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="86b88-260">Você verá os resultados da consulta Hive.</span><span class="sxs-lookup"><span data-stu-id="86b88-260">You will see the results of your Hive query.</span></span>

   ![Resultados da consulta de Hive][image-hive-query-results]

## <span data-ttu-id="86b88-262"><a name="RunPig"></a>Etapa 4: Executar um trabalho do Pig usando o Cosmos DB e o HDInsight</span><span class="sxs-lookup"><span data-stu-id="86b88-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="86b88-263">Todas as variáveis indicadas entre < > devem ser preenchidas usando suas configurações.</span><span class="sxs-lookup"><span data-stu-id="86b88-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="86b88-264">Defina as seguintes variáveis no seu Painel de Script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86b88-264">Set the following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want to run the Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="86b88-265">Vamos começar pela cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="86b88-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="86b88-266">Vamos escrever uma consulta Pig que usa todas as IDs exclusivas (_rid) e os carimbos de data/hora (_ts) gerados pelo sistema de documentos de uma coleção do Azure Cosmos DB, registra todos os documentos por minuto e armazena os resultados em uma nova coleção do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="86b88-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by the minute, and then stores the results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="86b88-267">Primeiro, carregue documentos do Cosmos DB no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86b88-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="86b88-268">Adicione o seguinte trecho de código ao painel de Script do PowerShell <strong>após</strong> o trecho de código do n.º 1.</span><span class="sxs-lookup"><span data-stu-id="86b88-268">Add the following code snippet to the PowerShell Script pane <strong>after</strong> the code snippet from #1.</span></span> <span data-ttu-id="86b88-269">Adicione uma consulta do DocumentDB ao parâmetro de consulta opcional do DocumentDB para limitar os documentos a somente _ts e _rid.</span><span class="sxs-lookup"><span data-stu-id="86b88-269">Make sure to add a DocumentDB query to the optional DocumentDB query parameter to trim our documents to just _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="86b88-270">Sim, nós podemos adicionar várias coleções como entrada:</span><span class="sxs-lookup"><span data-stu-id="86b88-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="86b88-271">'*\<Nome da Coleção de Entrada do DocumentDB 1\>*,*\<Nome da Coleção de Entrada do DocumentDB 2\>*'</span><span class="sxs-lookup"><span data-stu-id="86b88-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="86b88-272">Os nomes de coleção são separados sem espaços, usando apenas uma única vírgula.</span><span class="sxs-lookup"><span data-stu-id="86b88-272">The collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="86b88-273">Os documentos são distribuídos por round robin entre várias coleções.</span><span class="sxs-lookup"><span data-stu-id="86b88-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="86b88-274">Um lote de documentos será armazenado em uma coleção, um segundo lote de documentos será armazenado na coleção seguinte e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="86b88-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query to filter transferred data to _rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="86b88-275">Em seguida, vamos classificar os documentos por mês, dia, hora, minuto e o número total de ocorrências.</span><span class="sxs-lookup"><span data-stu-id="86b88-275">Next, let's tally the documents by the month, day, hour, minute, and the total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="86b88-276">Por fim, vamos armazenar os resultados em nossa nova coleção de saída.</span><span class="sxs-lookup"><span data-stu-id="86b88-276">Finally, let's store the results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="86b88-277">Sim, nós podemos adicionar várias coleções como saída:</span><span class="sxs-lookup"><span data-stu-id="86b88-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="86b88-278">'\<Nome da Coleção de Saída do DocumentDB 1\>, \<Nome da Coleção de Saída do DocumentDB 2\>'</span><span class="sxs-lookup"><span data-stu-id="86b88-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="86b88-279">Os nomes de coleção são separados sem espaços, usando apenas uma única vírgula.</span><span class="sxs-lookup"><span data-stu-id="86b88-279">The collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="86b88-280">Os documentos serão distribuídos em round robin entre os vários documentos.</span><span class="sxs-lookup"><span data-stu-id="86b88-280">Documents will be distributed round-robin across the multiple collections.</span></span> <span data-ttu-id="86b88-281">Um lote de documentos será armazenado em uma coleção, um segundo lote de documentos será armazenado na coleção seguinte e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="86b88-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in the next collection, and so forth.</span></span>
   >
   >

        # Store output data to Cosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="86b88-282">Adicione o trecho de script a seguir para criar uma definição de trabalho Pig por meio da consulta anterior.</span><span class="sxs-lookup"><span data-stu-id="86b88-282">Add the following script snippet to create a Pig job definition from the previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="86b88-283">Você também pode usar a opção -File para especificar um arquivo script Pig no HDFS.</span><span class="sxs-lookup"><span data-stu-id="86b88-283">You can also use the -File switch to specify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="86b88-284">Adicione o trecho a seguir para salvar a hora de início e enviar o trabalho Pig.</span><span class="sxs-lookup"><span data-stu-id="86b88-284">Add the following snippet to save the start time and submit the Pig job.</span></span>

        # Save the start time and submit the job to the cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="86b88-285">Adicione o seguinte para aguardar a conclusão do trabalho Pig.</span><span class="sxs-lookup"><span data-stu-id="86b88-285">Add the following to wait for the Pig job to complete.</span></span>

        # Wait for the Pig job to complete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="86b88-286">Adicione o seguinte para imprimir a saída padrão e os horários de início e fim.</span><span class="sxs-lookup"><span data-stu-id="86b88-286">Add the following to print the standard output and the start and end times.</span></span>

        # Print the standard error, the standard output of the Hive job, and the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="86b88-287">**Execute** seu novo script!</span><span class="sxs-lookup"><span data-stu-id="86b88-287">**Run** your new script!</span></span> <span data-ttu-id="86b88-288">**Clique** no botão de execução verde.</span><span class="sxs-lookup"><span data-stu-id="86b88-288">**Click** the green execute button.</span></span>
10. <span data-ttu-id="86b88-289">Confira os resultados.</span><span class="sxs-lookup"><span data-stu-id="86b88-289">Check the results.</span></span> <span data-ttu-id="86b88-290">Faça logon no [Portal do Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="86b88-290">Sign into the [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="86b88-291">Clique em <strong>Procurar</strong> no painel do lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="86b88-291">Click <strong>Browse</strong> on the left-side panel.</span></span> </br>
    2. <span data-ttu-id="86b88-292">Clique em <strong>tudo</strong> na parte superior direita no painel de navegação.</span><span class="sxs-lookup"><span data-stu-id="86b88-292">Click <strong>everything</strong> at the top-right of the browse panel.</span></span> </br>
    3. <span data-ttu-id="86b88-293">Localize e clique em <strong>Contas do Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="86b88-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="86b88-294">Em seguida, localizar seu <strong>Conta do Azure Cosmos DB</strong>, depois, <strong>banco de dados do Azure Cosmos DB</strong> e sua <strong>coleção do Azure Cosmos DB</strong> associados à coleção de saída especificada na consulta de Pig.</span><span class="sxs-lookup"><span data-stu-id="86b88-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="86b88-295">Por fim, clique em <strong>Gerenciador de Documentos</strong> abaixo de <strong>Ferramentas de Desenvolvedor</strong>.</span><span class="sxs-lookup"><span data-stu-id="86b88-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="86b88-296">Você verá os resultados da consulta Pig.</span><span class="sxs-lookup"><span data-stu-id="86b88-296">You will see the results of your Pig query.</span></span>

    ![Resultados da consulta de Pig][image-pig-query-results]

## <span data-ttu-id="86b88-298"><a name="RunMapReduce"></a>Etapa 5: executar um trabalho MapReduce usando o Azure Cosmos DB e o HDInsight</span><span class="sxs-lookup"><span data-stu-id="86b88-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="86b88-299">Defina as seguintes variáveis no seu Painel de Script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86b88-299">Set the following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="86b88-300">Executaremos um trabalho MapReduce que computa o número de ocorrências para cada propriedade do Documento por meio de sua coleção do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="86b88-300">We'll execute a MapReduce job that tallies the number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="86b88-301">Adicione este trecho de script **após** o trecho acima.</span><span class="sxs-lookup"><span data-stu-id="86b88-301">Add this script snippet **after** the snippet above.</span></span>

        # Define the MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="86b88-302">TallyProperties-v01.jar é fornecido com a instalação personalizada do Conector para Hadoop do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="86b88-302">TallyProperties-v01.jar comes with the custom installation of the Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="86b88-303">Adicione o comando a seguir para enviar o trabalho MapReduce.</span><span class="sxs-lookup"><span data-stu-id="86b88-303">Add the following command to submit the MapReduce job.</span></span>

        # Save the start time and submit the job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="86b88-304">Além da definição do trabalho MapReduce, você também deve fornecer o nome do cluster HDInsight onde você deseja executar o trabalho MapReduce e as credenciais.</span><span class="sxs-lookup"><span data-stu-id="86b88-304">In addition to the MapReduce job definition, you also provide the HDInsight cluster name where you want to run the MapReduce job, and the credentials.</span></span> <span data-ttu-id="86b88-305">O Start-AzureHDInsightJob é uma chamada assincronizada.</span><span class="sxs-lookup"><span data-stu-id="86b88-305">The Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="86b88-306">Para verificar a conclusão do trabalho, use o cmdlet *AzureHDInsightJob de espera* .</span><span class="sxs-lookup"><span data-stu-id="86b88-306">To check the completion of the job, use the *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="86b88-307">Adicione o seguinte comando para verificar se há erros na execução do trabalho MapReduce.</span><span class="sxs-lookup"><span data-stu-id="86b88-307">Add the following command to check any errors with running the MapReduce job.</span></span>

        # Get the job output and print the start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="86b88-308">**Execute** seu novo script!</span><span class="sxs-lookup"><span data-stu-id="86b88-308">**Run** your new script!</span></span> <span data-ttu-id="86b88-309">**Clique** no botão de execução verde.</span><span class="sxs-lookup"><span data-stu-id="86b88-309">**Click** the green execute button.</span></span>
6. <span data-ttu-id="86b88-310">Confira os resultados.</span><span class="sxs-lookup"><span data-stu-id="86b88-310">Check the results.</span></span> <span data-ttu-id="86b88-311">Faça logon no [Portal do Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="86b88-311">Sign into the [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="86b88-312">Clique em <strong>Procurar</strong> no painel do lado esquerdo.</span><span class="sxs-lookup"><span data-stu-id="86b88-312">Click <strong>Browse</strong> on the left-side panel.</span></span>
   2. <span data-ttu-id="86b88-313">Clique em <strong>tudo</strong> na parte superior direita no painel de navegação.</span><span class="sxs-lookup"><span data-stu-id="86b88-313">Click <strong>everything</strong> at the top-right of the browse panel.</span></span>
   3. <span data-ttu-id="86b88-314">Localize e clique em <strong>Contas do Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="86b88-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="86b88-315">Em seguida, localizar seu <strong>Conta do Azure Cosmos DB</strong>, depois, <strong>banco de dados do Azure Cosmos DB</strong> e sua <strong>coleção do Azure Cosmos DB</strong> associados à coleção de saída especificada no trabalho do MapReduce.</span><span class="sxs-lookup"><span data-stu-id="86b88-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with the output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="86b88-316">Por fim, clique em <strong>Gerenciador de Documentos</strong> abaixo de <strong>Ferramentas de Desenvolvedor</strong>.</span><span class="sxs-lookup"><span data-stu-id="86b88-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="86b88-317">Você verá os resultados do trabalho MapReduce.</span><span class="sxs-lookup"><span data-stu-id="86b88-317">You will see the results of your MapReduce job.</span></span>

      ![Resultados da consulta de MapReduce][image-mapreduce-query-results]

## <span data-ttu-id="86b88-319"><a name="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="86b88-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="86b88-320">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="86b88-320">Congratulations!</span></span> <span data-ttu-id="86b88-321">Você acaba de executar seus primeiros trabalhos do Hive, Pig e MapReduce usando o Azure Cosmos DB e o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86b88-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="86b88-322">Nós abrimos o código-fonte do nosso Conector do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="86b88-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="86b88-323">Se estiver interessado, você poderá contribuir com o [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="86b88-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="86b88-324">Para saber mais, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="86b88-324">To learn more, see the following articles:</span></span>

* <span data-ttu-id="86b88-325">[Desenvolver um aplicativo Java com o DocumentDB][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="86b88-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="86b88-326">[Desenvolver programas Java MapReduce para Hadoop no HDInsight][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="86b88-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="86b88-327">[Introdução ao uso do Hadoop com o Hive no HDInsight para analisar o uso de fone de celular][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="86b88-327">[Get started using Hadoop with Hive in HDInsight to analyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="86b88-328">[Usar o MapReduce com o HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="86b88-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="86b88-329">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="86b88-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="86b88-330">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="86b88-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="86b88-331">[Personalizar os clusters HDInsight usando a Ação de Script][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="86b88-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

[apache-hadoop]: http://hadoop.apache.org/
[apache-hadoop-doc]: http://hadoop.apache.org/docs/current/
[apache-hive]: http://hive.apache.org/
[apache-pig]: http://pig.apache.org/
[getting-started]: documentdb-get-started.md

[azure-portal]: https://portal.azure.com/
[azure-powershell-diagram]: ./media/run-hadoop-with-hdinsight/azurepowershell-diagram-med.png

[hdinsight-samples]: http://portalcontent.blob.core.windows.net/samples/documentdb-hdinsight-samples.zip
[github]: https://github.com/Azure/azure-documentdb-hadoop
[documentdb-java-application]: documentdb-java-application.md
[import-data]: import-data.md

[hdinsight-custom-provision]: ../hdinsight/hdinsight-provision-clusters.md
[hdinsight-develop-deploy-java-mapreduce]: ../hdinsight/hdinsight-develop-deploy-java-mapreduce-linux.md
[hdinsight-hadoop-customize-cluster]: ../hdinsight/hdinsight-hadoop-customize-cluster.md
[hdinsight-get-started]: ../hdinsight/hdinsight-hadoop-tutorial-get-started-windows.md
[hdinsight-storage]: ../hdinsight/hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-hive]: ../hdinsight/hdinsight-use-hive.md
[hdinsight-use-mapreduce]: ../hdinsight/hdinsight-use-mapreduce.md
[hdinsight-use-pig]: ../hdinsight/hdinsight-use-pig.md

[image-customprovision-page1]: ./media/run-hadoop-with-hdinsight/customprovision-page1.png
[image-hive-query-results]: ./media/run-hadoop-with-hdinsight/hivequeryresults.PNG
[image-mapreduce-query-results]: ./media/run-hadoop-with-hdinsight/mapreducequeryresults.PNG
[image-pig-query-results]: ./media/run-hadoop-with-hdinsight/pigqueryresults.PNG

[powershell-install-configure]: https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0
