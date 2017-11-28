---
title: aaaRun um Hadoop de trabalho usando o banco de dados do Azure Cosmos e HDInsight | Microsoft Docs
description: Saiba como toorun um simple Hive, Pig e MapReduce trabalho com o banco de dados do Azure Cosmos e HDInsight do Azure.
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
ms.openlocfilehash: 2e27499f2c4ba951af9a1ade1bcc9c1b6d298fcd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <span data-ttu-id="b0375-103"><a name="Azure Cosmos DB-HDInsight"></a>Executar um trabalho do Apache Hive, Pig ou Hadoop usando o Azure Cosmos DB e o HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0375-103"><a name="Azure Cosmos DB-HDInsight"></a>Run an Apache Hive, Pig, or Hadoop job using Azure Cosmos DB and HDInsight</span></span>
<span data-ttu-id="b0375-104">Este tutorial mostra como toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], e [Apache Hadoop] [ apache-hadoop] Trabalhos MapReduce no Azure HDInsight com o conector para Hadoop do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0375-104">This tutorial shows you how toorun [Apache Hive][apache-hive], [Apache Pig][apache-pig], and [Apache Hadoop][apache-hadoop] MapReduce jobs on Azure HDInsight with Cosmos DB's Hadoop connector.</span></span> <span data-ttu-id="b0375-105">Conector para Hadoop do cosmos do banco de dados permite tooact DB Cosmos como uma origem e um coletor para trabalhos Hive, Pig e MapReduce.</span><span class="sxs-lookup"><span data-stu-id="b0375-105">Cosmos DB's Hadoop connector allows Cosmos DB tooact as both a source and sink for Hive, Pig, and MapReduce jobs.</span></span> <span data-ttu-id="b0375-106">Este tutorial usará DB Cosmos como fonte de dados de saudação e de destino para trabalhos de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b0375-106">This tutorial will use Cosmos DB as both hello data source and destination for Hadoop jobs.</span></span>

<span data-ttu-id="b0375-107">Após concluir este tutorial, você será capaz de tooanswer Olá perguntas a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0375-107">After completing this tutorial, you'll be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="b0375-108">Como fazer para carregar dados do Cosmos DB usando um trabalho do Hive, Pig ou MapReduce?</span><span class="sxs-lookup"><span data-stu-id="b0375-108">How do I load data from Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>
* <span data-ttu-id="b0375-109">Como fazer para armazenar dados no Cosmos DB usando um trabalho do Hive, Pig ou MapReduce?</span><span class="sxs-lookup"><span data-stu-id="b0375-109">How do I store data in Cosmos DB using a Hive, Pig, or MapReduce job?</span></span>

<span data-ttu-id="b0375-110">É recomendável que guia de Introdução observando Olá seguindo o vídeo, onde é executado por meio de um trabalho de Hive usando o banco de dados do Cosmos e HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0375-110">We recommend getting started by watching hello following video, where we run through a Hive job using Cosmos DB and HDInsight.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Use-Azure-DocumentDB-Hadoop-Connector-with-Azure-HDInsight/player]
>
>

<span data-ttu-id="b0375-111">Em seguida, retorne toothis artigo, onde você receberá detalhes completos de saudação em como você pode executar trabalhos de análise em seus dados de banco de dados do Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b0375-111">Then, return toothis article, where you'll receive hello full details on how you can run analytics jobs on your Cosmos DB data.</span></span>

> [!TIP]
> <span data-ttu-id="b0375-112">Este tutorial presume que você tenha experiência anterior com o uso do Apache Hadoop, Hive e/ou Pig.</span><span class="sxs-lookup"><span data-stu-id="b0375-112">This tutorial assumes that you have prior experience using Apache Hadoop, Hive, and/or Pig.</span></span> <span data-ttu-id="b0375-113">Se você for novo tooApache Hadoop, Hive e Pig, recomendamos que você visite Olá [documentação do Apache Hadoop][apache-hadoop-doc].</span><span class="sxs-lookup"><span data-stu-id="b0375-113">If you are new tooApache Hadoop, Hive, and Pig, we recommend visiting hello [Apache Hadoop documentation][apache-hadoop-doc].</span></span> <span data-ttu-id="b0375-114">Este tutorial também pressupõe que você tenha experiência anterior com o Cosmos DB e tenha uma conta do Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0375-114">This tutorial also assumes that you have prior experience with Cosmos DB and have a Cosmos DB account.</span></span> <span data-ttu-id="b0375-115">Se você estiver tooCosmos novo banco de dados ou você não tem uma conta de banco de dados do Cosmos, Confira nosso [Introdução] [ getting-started] página.</span><span class="sxs-lookup"><span data-stu-id="b0375-115">If you are new tooCosmos DB or you do not have a Cosmos DB account, please check out our [Getting Started][getting-started] page.</span></span>
>
>

<span data-ttu-id="b0375-116">Você não tem tempo toocomplete Olá tutorial e deseja apenas scripts do PowerShell de exemplo completo tooget Olá para Hive, Pig e MapReduce?</span><span class="sxs-lookup"><span data-stu-id="b0375-116">Don't have time toocomplete hello tutorial and just want tooget hello full sample PowerShell scripts for Hive, Pig, and MapReduce?</span></span> <span data-ttu-id="b0375-117">Sem problemas, elas estão [aqui][hdinsight-samples].</span><span class="sxs-lookup"><span data-stu-id="b0375-117">Not a problem, get them [here][hdinsight-samples].</span></span> <span data-ttu-id="b0375-118">download de saudação também contém arquivos hql, pig e java Olá esses exemplos.</span><span class="sxs-lookup"><span data-stu-id="b0375-118">hello download also contains hello hql, pig, and java files for these samples.</span></span>

## <span data-ttu-id="b0375-119"><a name="NewestVersion"></a>Versão Mais Recente</span><span class="sxs-lookup"><span data-stu-id="b0375-119"><a name="NewestVersion"></a>Newest Version</span></span>
<table border='1'>
    <tr><th><span data-ttu-id="b0375-120">Versão do Conector para Hadoop</span><span class="sxs-lookup"><span data-stu-id="b0375-120">Hadoop Connector Version</span></span></th>
        <td><span data-ttu-id="b0375-121">1.2.0</span><span class="sxs-lookup"><span data-stu-id="b0375-121">1.2.0</span></span></td></tr>
    <tr><th><span data-ttu-id="b0375-122">URI do script</span><span class="sxs-lookup"><span data-stu-id="b0375-122">Script Uri</span></span></th>
        <td><span data-ttu-id="b0375-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span><span class="sxs-lookup"><span data-stu-id="b0375-123">https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</span></span></td></tr>
    <tr><th><span data-ttu-id="b0375-124">Data da Modificação</span><span class="sxs-lookup"><span data-stu-id="b0375-124">Date Modified</span></span></th>
        <td><span data-ttu-id="b0375-125">26/04/2016</span><span class="sxs-lookup"><span data-stu-id="b0375-125">04/26/2016</span></span></td></tr>
    <tr><th><span data-ttu-id="b0375-126">Versões do HDInsight para as quais há suporte</span><span class="sxs-lookup"><span data-stu-id="b0375-126">Supported HDInsight Versions</span></span></th>
        <td><span data-ttu-id="b0375-127">3.1, 3.2</span><span class="sxs-lookup"><span data-stu-id="b0375-127">3.1, 3.2</span></span></td></tr>
    <tr><th><span data-ttu-id="b0375-128">Log de alterações</span><span class="sxs-lookup"><span data-stu-id="b0375-128">Change Log</span></span></th>
        <td><span data-ttu-id="b0375-129">Cosmos atualizada do Azure DB Java SDK too1.6.0</span><span class="sxs-lookup"><span data-stu-id="b0375-129">Updated Azure Cosmos DB Java SDK too1.6.0</span></span></br>
            <span data-ttu-id="b0375-130">Suporte adicionado para coleções particionadas como uma fonte e coletor</span><span class="sxs-lookup"><span data-stu-id="b0375-130">Added support for partitioned collections as both a source and sink</span></span></br>
        </td></tr>
</table>

## <span data-ttu-id="b0375-131"><a name="Prerequisites"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b0375-131"><a name="Prerequisites"></a>Prerequisites</span></span>
<span data-ttu-id="b0375-132">Antes de seguir as instruções de saudação neste tutorial, certifique-se de que você tenha a seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="b0375-132">Before following hello instructions in this tutorial, ensure that you have hello following:</span></span>

* <span data-ttu-id="b0375-133">Uma conta do Cosmos DB, um banco de dados e uma coleção com documentos.</span><span class="sxs-lookup"><span data-stu-id="b0375-133">A Cosmos DB account, a database, and a collection with documents inside.</span></span> <span data-ttu-id="b0375-134">Para obter mais informações, consulte [Introdução ao Cosmos DB][getting-started].</span><span class="sxs-lookup"><span data-stu-id="b0375-134">For more information, see [Getting Started with Cosmos DB][getting-started].</span></span> <span data-ttu-id="b0375-135">Importar dados de exemplo para a conta de banco de dados do Cosmos com hello [ferramenta de importação de banco de dados do Cosmos][import-data].</span><span class="sxs-lookup"><span data-stu-id="b0375-135">Import sample data into your Cosmos DB account with hello [Cosmos DB import tool][import-data].</span></span>
* <span data-ttu-id="b0375-136">Produtividade.</span><span class="sxs-lookup"><span data-stu-id="b0375-136">Throughput.</span></span> <span data-ttu-id="b0375-137">Leituras e gravações do HDInsight serão contabilizadas de acordo com suas unidades de solicitação alocadas para suas coleções.</span><span class="sxs-lookup"><span data-stu-id="b0375-137">Reads and writes from HDInsight will be counted towards your allotted request units for your collections.</span></span>
* <span data-ttu-id="b0375-138">Capacidade para um procedimento armazenado adicional dentro de cada coleção de saída.</span><span class="sxs-lookup"><span data-stu-id="b0375-138">Capacity for an additional stored procedure within each output collection.</span></span> <span data-ttu-id="b0375-139">procedimentos armazenado de Hello são usados para a transferência de documentos resultantes.</span><span class="sxs-lookup"><span data-stu-id="b0375-139">hello stored procedures are used for transferring resulting documents.</span></span>
* <span data-ttu-id="b0375-140">Capacidade para documentos resultantes de saudação de trabalhos de Hive, Pig e MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="b0375-140">Capacity for hello resulting documents from hello Hive, Pig, or MapReduce jobs.</span></span>
* <span data-ttu-id="b0375-141">[*Opcional*] Capacidade para uma coleção adicional.</span><span class="sxs-lookup"><span data-stu-id="b0375-141">[*Optional*] Capacity for an additional collection.</span></span>

> [!WARNING]
> <span data-ttu-id="b0375-142">Em ordem tooavoid Olá a criação de uma nova coleção durante qualquer um dos trabalhos hello, você pode imprimir Olá resultados toostdout, salvar o contêiner do hello saída tooyour WASB ou especifique uma coleção já existente.</span><span class="sxs-lookup"><span data-stu-id="b0375-142">In order tooavoid hello creation of a new collection during any of hello jobs, you can either print hello results toostdout, save hello output tooyour WASB container, or specify an already existing collection.</span></span> <span data-ttu-id="b0375-143">No caso de saudação da especificação de uma coleção existente, novos documentos serão criados dentro da coleção de saudação e documentos já existentes serão afetados apenas se houver um conflito na *ids*.</span><span class="sxs-lookup"><span data-stu-id="b0375-143">In hello case of specifying an existing collection, new documents will be created inside hello collection and already existing documents will only be affected if there is a conflict in *ids*.</span></span> <span data-ttu-id="b0375-144">**conector de saudação substituirá automaticamente os documentos existentes com conflitos de id**.</span><span class="sxs-lookup"><span data-stu-id="b0375-144">**hello connector will automatically overwrite existing documents with id conflicts**.</span></span> <span data-ttu-id="b0375-145">Você pode desativar esse recurso definindo Olá upsert opção toofalse.</span><span class="sxs-lookup"><span data-stu-id="b0375-145">You can turn off this feature by setting hello upsert option toofalse.</span></span> <span data-ttu-id="b0375-146">Se upsert é falso e um conflito ocorre, o trabalho do Hadoop Olá falhará; relatar um erro de conflito de id.</span><span class="sxs-lookup"><span data-stu-id="b0375-146">If upsert is false and a conflict occurs, hello Hadoop job will fail; reporting an id conflict error.</span></span>
>
>

## <span data-ttu-id="b0375-147"><a name="ProvisionHDInsight"></a>Etapa 1: criar um novo cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0375-147"><a name="ProvisionHDInsight"></a>Step 1: Create a new HDInsight cluster</span></span>
<span data-ttu-id="b0375-148">Este tutorial usa o Script de ação de saudação do Portal Azure toocustomize seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0375-148">This tutorial uses Script Action from hello Azure Portal toocustomize your HDInsight cluster.</span></span> <span data-ttu-id="b0375-149">Neste tutorial, usaremos hello Azure Portal toocreate seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0375-149">In this tutorial, we will use hello Azure Portal toocreate your HDInsight cluster.</span></span> <span data-ttu-id="b0375-150">Para obter instruções sobre como os cmdlets do PowerShell toouse ou hello HDInsight .NET SDK, check-out de [HDInsight personalizar clusters usando a ação de Script] [ hdinsight-custom-provision] artigo.</span><span class="sxs-lookup"><span data-stu-id="b0375-150">For instructions on how toouse PowerShell cmdlets or hello HDInsight .NET SDK, check out the [Customize HDInsight clusters using Script Action][hdinsight-custom-provision] article.</span></span>

1. <span data-ttu-id="b0375-151">Entrar toohello [Portal do Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="b0375-151">Sign in toohello [Azure Portal][azure-portal].</span></span>
2. <span data-ttu-id="b0375-152">Clique em **+ novo** na parte superior de saudação do hello barra de navegação esquerda, procure por **HDInsight** na barra de pesquisa de saudação na nova folha de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0375-152">Click **+ New** on hello top of hello left navigation, search for **HDInsight** in hello top search bar on hello New blade.</span></span>
3. <span data-ttu-id="b0375-153">**HDInsight** publicado por **Microsoft** aparecerá na parte superior de saudação do hello resultados.</span><span class="sxs-lookup"><span data-stu-id="b0375-153">**HDInsight** published by **Microsoft** will appear at hello top of hello Results.</span></span> <span data-ttu-id="b0375-154">Clique nele, em seguida, clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="b0375-154">Click on it and then click **Create**.</span></span>
4. <span data-ttu-id="b0375-155">No novo HDInsight Cluster de saudação criar folha, insira seu **nome do Cluster** e selecione hello **assinatura** deseja tooprovision esse recurso em.</span><span class="sxs-lookup"><span data-stu-id="b0375-155">On hello New HDInsight Cluster create blade, enter your **Cluster Name** and select hello **Subscription** you want tooprovision this resource under.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="b0375-156">Nome do cluster</span><span class="sxs-lookup"><span data-stu-id="b0375-156">Cluster name</span></span></td><td><span data-ttu-id="b0375-157">Cluster de saudação do nome.</span><span class="sxs-lookup"><span data-stu-id="b0375-157">Name hello cluster.</span></span><br/>
<span data-ttu-id="b0375-158">O nome DNS deve começar e terminar com um número alfanumérico e pode conter traços.</span><span class="sxs-lookup"><span data-stu-id="b0375-158">DNS name must start and end with an alpha numeric character, and may contain dashes.</span></span><br/>
<span data-ttu-id="b0375-159">campo de saudação deve ser uma cadeia de caracteres entre 3 e 63 caracteres.</span><span class="sxs-lookup"><span data-stu-id="b0375-159">hello field must be a string between 3 and 63 characters.</span></span></td></tr>
        <tr><td><span data-ttu-id="b0375-160">Nome da assinatura</span><span class="sxs-lookup"><span data-stu-id="b0375-160">Subscription Name</span></span></td>
            <td><span data-ttu-id="b0375-161">Se você tiver mais de uma assinatura do Azure, selecione a assinatura de saudação que irá hospedar o seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0375-161">If you have more than one Azure Subscription, select hello subscription that will host your HDInsight cluster.</span></span> </td></tr>
    </table><span data-ttu-id="b0375-162">
5.Clique em **Selecionar tipo de Cluster** e valores especificados de saudação do conjunto de propriedades toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="b0375-162">
5. Click **Select Cluster Type** and set hello following properties toohello specified values.</span></span>

    <table border='1'>
        <tr><td><span data-ttu-id="b0375-163">Tipo de cluster</span><span class="sxs-lookup"><span data-stu-id="b0375-163">Cluster type</span></span></td><td><span data-ttu-id="b0375-164"><strong>Hadoop</strong></span><span class="sxs-lookup"><span data-stu-id="b0375-164"><strong>Hadoop</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="b0375-165">Nível do cluster</span><span class="sxs-lookup"><span data-stu-id="b0375-165">Cluster tier</span></span></td><td><span data-ttu-id="b0375-166"><strong>Standard</strong></span><span class="sxs-lookup"><span data-stu-id="b0375-166"><strong>Standard</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="b0375-167">Sistema operacional</span><span class="sxs-lookup"><span data-stu-id="b0375-167">Operating System</span></span></td><td><span data-ttu-id="b0375-168"><strong>Windows</strong></span><span class="sxs-lookup"><span data-stu-id="b0375-168"><strong>Windows</strong></span></span></td></tr>
        <tr><td><span data-ttu-id="b0375-169">Versão</span><span class="sxs-lookup"><span data-stu-id="b0375-169">Version</span></span></td><td><span data-ttu-id="b0375-170">última versão</span><span class="sxs-lookup"><span data-stu-id="b0375-170">latest version</span></span></td></tr>
    </table>

    <span data-ttu-id="b0375-171">Agora, clique em **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="b0375-171">Now, click **SELECT**.</span></span>

    ![Fornecer detalhes do cluster HDInsight inicial do Hadoop][image-customprovision-page1]
6. <span data-ttu-id="b0375-173">Clique em **credenciais** tooset seu logon e credenciais de acesso remoto.</span><span class="sxs-lookup"><span data-stu-id="b0375-173">Click on **Credentials** tooset your login and remote access credentials.</span></span> <span data-ttu-id="b0375-174">Escolha o **Nome de Usuário de Logon do Cluster** e a **Senha de Logon do Cluster**.</span><span class="sxs-lookup"><span data-stu-id="b0375-174">Choose your **Cluster Login Username** and **Cluster Login Password**.</span></span>

    <span data-ttu-id="b0375-175">Se você desejar tooremote em seu cluster, selecione *Sim* na parte inferior da saudação da folha de saudação e forneça um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="b0375-175">If you want tooremote into your cluster, select *yes* at hello bottom of hello blade and provide a username and password.</span></span>
7. <span data-ttu-id="b0375-176">Clique em **fonte de dados** tooset acessar o local para os dados.</span><span class="sxs-lookup"><span data-stu-id="b0375-176">Click on **Data Source** tooset your primary location for data access.</span></span> <span data-ttu-id="b0375-177">Escolha Olá **método de seleção** e especificar uma conta de armazenamento já existente ou crie um novo.</span><span class="sxs-lookup"><span data-stu-id="b0375-177">Choose hello **Selection Method** and specify an already existing storage account or create a new one.</span></span>
8. <span data-ttu-id="b0375-178">Olá folha mesmo em, especifique um **contêiner padrão** e um **local**.</span><span class="sxs-lookup"><span data-stu-id="b0375-178">On hello same blade, specify a **Default Container** and a **Location**.</span></span> <span data-ttu-id="b0375-179">Clique em **SELECT**.</span><span class="sxs-lookup"><span data-stu-id="b0375-179">And, click **SELECT**.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b0375-180">Selecione tooyour de fechar um local DB Cosmos região da conta para melhorar o desempenho</span><span class="sxs-lookup"><span data-stu-id="b0375-180">Select a location close tooyour Cosmos DB account region for better performance</span></span>
   >
   >
9. <span data-ttu-id="b0375-181">Clique em **preços** tooselect Olá número e tipo de nós.</span><span class="sxs-lookup"><span data-stu-id="b0375-181">Click on **Pricing** tooselect hello number and type of nodes.</span></span> <span data-ttu-id="b0375-182">Você pode manter configuração padrão de saudação e Olá aumenta o número de nós de trabalho mais tarde.</span><span class="sxs-lookup"><span data-stu-id="b0375-182">You can keep hello default configuration and scale hello number of Worker nodes later on.</span></span>
10. <span data-ttu-id="b0375-183">Clique em **configuração opcional**, em seguida, **ações de Script** no hello folha de configuração opcional.</span><span class="sxs-lookup"><span data-stu-id="b0375-183">Click **Optional Configuration**, then **Script Actions** in hello Optional Configuration Blade.</span></span>

     <span data-ttu-id="b0375-184">Em ações de Script, digite Olá toocustomize informações a seguir seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0375-184">In Script Actions, enter hello following information toocustomize your HDInsight cluster.</span></span>

     <table border='1'>
         <tr><th><span data-ttu-id="b0375-185">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b0375-185">Property</span></span></th><th><span data-ttu-id="b0375-186">Valor</span><span class="sxs-lookup"><span data-stu-id="b0375-186">Value</span></span></th></tr>
         <tr><td><span data-ttu-id="b0375-187">Nome</span><span class="sxs-lookup"><span data-stu-id="b0375-187">Name</span></span></td>
             <td><span data-ttu-id="b0375-188">Especifique um nome para a ação de script hello.</span><span class="sxs-lookup"><span data-stu-id="b0375-188">Specify a name for hello script action.</span></span></td></tr>
         <tr><td><span data-ttu-id="b0375-189">URI do script</span><span class="sxs-lookup"><span data-stu-id="b0375-189">Script URI</span></span></td>
             <td><span data-ttu-id="b0375-190">Especifique Olá URI toohello script que é invocado toocustomize Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="b0375-190">Specify hello URI toohello script that is invoked toocustomize hello cluster.</span></span></br></br>
<span data-ttu-id="b0375-191">Insira:</span><span class="sxs-lookup"><span data-stu-id="b0375-191">Please enter:</span></span> </br> <span data-ttu-id="b0375-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span><span class="sxs-lookup"><span data-stu-id="b0375-192"><strong>https://portalcontent.blob.core.windows.net/scriptaction/documentdb-hadoop-installer-v04.ps1</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="b0375-193">Principal</span><span class="sxs-lookup"><span data-stu-id="b0375-193">Head</span></span></td>
             <td><span data-ttu-id="b0375-194">Clique em Olá toorun da caixa de seleção Olá script do PowerShell para o nó de cabeçalho hello.</span><span class="sxs-lookup"><span data-stu-id="b0375-194">Click hello checkbox toorun hello PowerShell script onto hello Head node.</span></span></br></br><span data-ttu-id="b0375-195">
             <strong>Marque essa caixa de seleção</strong>.</span><span class="sxs-lookup"><span data-stu-id="b0375-195">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="b0375-196">Trabalho</span><span class="sxs-lookup"><span data-stu-id="b0375-196">Worker</span></span></td>
             <td><span data-ttu-id="b0375-197">Clique em Olá caixa de seleção toorun Olá PowerShell script no nó de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="b0375-197">Click hello checkbox toorun hello PowerShell script onto hello Worker node.</span></span></br></br><span data-ttu-id="b0375-198">
             <strong>Marque essa caixa de seleção</strong>.</span><span class="sxs-lookup"><span data-stu-id="b0375-198">
             <strong>Check this checkbox</strong>.</span></span></td></tr>
         <tr><td><span data-ttu-id="b0375-199">Zookeeper</span><span class="sxs-lookup"><span data-stu-id="b0375-199">Zookeeper</span></span></td>
             <td><span data-ttu-id="b0375-200">Clique em script do PowerShell Olá caixa de seleção toorun Olá para Olá Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="b0375-200">Click hello checkbox toorun hello PowerShell script onto hello Zookeeper.</span></span></br></br><span data-ttu-id="b0375-201">
             <strong>Não é necessário</strong>.</span><span class="sxs-lookup"><span data-stu-id="b0375-201">
             <strong>Not needed</strong>.</span></span>
             </td></tr>
         <tr><td><span data-ttu-id="b0375-202">parâmetros</span><span class="sxs-lookup"><span data-stu-id="b0375-202">Parameters</span></span></td>
             <td><span data-ttu-id="b0375-203">Especifica parâmetros de hello, se exigido pelo script hello.</span><span class="sxs-lookup"><span data-stu-id="b0375-203">Specify hello parameters, if required by hello script.</span></span></br></br><span data-ttu-id="b0375-204">
             <strong>Nenhum parâmetro necessário</strong>.</span><span class="sxs-lookup"><span data-stu-id="b0375-204">
             <strong>No Parameters needed</strong>.</span></span></td></tr>
     </table><span data-ttu-id="b0375-205">
11. Criar um novo **Grupo de Recursos** ou use um Grupo de Recursos existente em sua Assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0375-205">
11. Create either a new **Resource Group** or use an existing Resource Group under your Azure Subscription.</span></span>
<span data-ttu-id="b0375-206">12.</span><span class="sxs-lookup"><span data-stu-id="b0375-206">12.</span></span> <span data-ttu-id="b0375-207">Agora, verifique **Pin toodashboard** tootrack sua implantação e clique em **criar**!</span><span class="sxs-lookup"><span data-stu-id="b0375-207">Now, check **Pin toodashboard** tootrack its deployment and click **Create**!</span></span>

## <span data-ttu-id="b0375-208"><a name="InstallCmdlets"></a>Etapa 2: instalar e configurar o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b0375-208"><a name="InstallCmdlets"></a>Step 2: Install and configure Azure PowerShell</span></span>
1. <span data-ttu-id="b0375-209">Instale o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0375-209">Install Azure PowerShell.</span></span> <span data-ttu-id="b0375-210">As instruções podem ser encontradas [aqui][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="b0375-210">Instructions can be found [here][powershell-install-configure].</span></span>

   > [!NOTE]
   > <span data-ttu-id="b0375-211">Como alternativa, só para consultas Hive, você pode usar o Editor de Hive online do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0375-211">Alternatively, just for Hive queries, you can use HDInsight's online Hive Editor.</span></span> <span data-ttu-id="b0375-212">toodo assim, entrar toohello [Portal do Azure][azure-portal], clique em **HDInsight** tooview de painel esquerdo Olá em uma lista de seus clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0375-212">toodo so, sign in toohello [Azure Portal][azure-portal], click **HDInsight** on hello left pane tooview a list of your HDInsight clusters.</span></span> <span data-ttu-id="b0375-213">Clique em cluster Olá você deseja que as consultas de Hive toorun em e, em seguida, clique em **Console de consulta**.</span><span class="sxs-lookup"><span data-stu-id="b0375-213">Click hello cluster you want toorun Hive queries on, and then click **Query Console**.</span></span>
   >
   >
2. <span data-ttu-id="b0375-214">Abra hello Azure PowerShell ambiente de script integrado:</span><span class="sxs-lookup"><span data-stu-id="b0375-214">Open hello Azure PowerShell Integrated Scripting Environment:</span></span>

   * <span data-ttu-id="b0375-215">Em um computador executando o Windows 8 ou o Windows Server 2012 ou posterior, você pode usar internas Olá pesquisa.</span><span class="sxs-lookup"><span data-stu-id="b0375-215">On a computer running Windows 8 or Windows Server 2012 or higher, you can use hello built-in Search.</span></span> <span data-ttu-id="b0375-216">Na tela de início do hello, digite **powershell ise** e clique em **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b0375-216">From hello Start screen, type **powershell ise** and click **Enter**.</span></span>
   * <span data-ttu-id="b0375-217">Em um computador executando uma versão anterior ao Windows 8 ou Windows Server 2012, use o menu de início de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0375-217">On a computer running a version earlier than Windows 8 or Windows Server 2012, use hello Start menu.</span></span> <span data-ttu-id="b0375-218">Saudação do menu de início, digite **Prompt de comando** na caixa de pesquisa hello e, na lista de saudação de resultados, clique em **Prompt de comando**.</span><span class="sxs-lookup"><span data-stu-id="b0375-218">From hello Start menu, type **Command Prompt** in hello search box, then in hello list of results, click **Command Prompt**.</span></span> <span data-ttu-id="b0375-219">No Prompt de comando do hello, digite **powershell_ise** e clique em **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b0375-219">In hello Command Prompt, type **powershell_ise** and click **Enter**.</span></span>
3. <span data-ttu-id="b0375-220">Adicione sua conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0375-220">Add your Azure Account.</span></span>

   1. <span data-ttu-id="b0375-221">Em Olá painel de Console, digite **Add-AzureAccount** e clique em **Enter**.</span><span class="sxs-lookup"><span data-stu-id="b0375-221">In hello Console Pane, type **Add-AzureAccount** and click **Enter**.</span></span>
   2. <span data-ttu-id="b0375-222">Digite hello endereço de email associado à sua assinatura do Azure e clique em **continuar**.</span><span class="sxs-lookup"><span data-stu-id="b0375-222">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span>
   3. <span data-ttu-id="b0375-223">Digite a senha Olá para sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0375-223">Type in hello password for your Azure subscription.</span></span>
   4. <span data-ttu-id="b0375-224">Clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="b0375-224">Click **Sign in**.</span></span>
4. <span data-ttu-id="b0375-225">Olá diagrama a seguir identifica as partes importantes de saudação do seu ambiente de script de PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="b0375-225">hello following diagram identifies hello important parts of your Azure PowerShell Scripting Environment.</span></span>

    ![Diagrama do PowerShell do Azure][azure-powershell-diagram]

## <span data-ttu-id="b0375-227"><a name="RunHive"></a>Etapa 3: Executar um trabalho do Hive usando o Cosmos DB e o HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0375-227"><a name="RunHive"></a>Step 3: Run a Hive job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b0375-228">Todas as variáveis indicadas entre < > devem ser preenchidas usando suas configurações.</span><span class="sxs-lookup"><span data-stu-id="b0375-228">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="b0375-229">Saudação de conjunto de variáveis no seu painel de Script do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="b0375-229">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name, hello Azure Storage account and container that is used for hello default HDInsight file system.
        $subscriptionName = "<SubscriptionName>"
        $storageAccountName = "<AzureStorageAccountName>"
        $containerName = "<AzureStorageContainerName>"

        # Provide hello HDInsight cluster name where you want toorun hello Hive job.
        $clusterName = "<HDInsightClusterName>"
2. <p><span data-ttu-id="b0375-230">Vamos começar pela cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="b0375-230">Let's begin constructing your query string.</span></span> <span data-ttu-id="b0375-231">Vamos gravar uma consulta de Hive que leva os carimbos de hora gerada pelo sistema ( TS) e identificações exclusivas ( RID) de uma coleção de banco de dados do Azure Cosmos todos os documentos, também incluirá todos os documentos em um minuto hello e, em seguida, armazena os resultados de saudação volta para uma nova coleção de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b0375-231">We'll write a Hive query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>

    <p><span data-ttu-id="b0375-232">Primeiro, vamos criar uma tabela Hive por meio da coleção do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="b0375-232">First, let's create a Hive table from our Azure Cosmos DB collection.</span></span> <span data-ttu-id="b0375-233">Adicionar Olá toohello de trecho de código painel de Script do PowerShell a seguir <strong>depois</strong> trecho de código de saudação do #1.</span><span class="sxs-lookup"><span data-stu-id="b0375-233">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="b0375-234">Certifique-se de que incluir Olá opcional DocumentDB.query parâmetro t trim nossos TS toojust de documentos e RID.</span><span class="sxs-lookup"><span data-stu-id="b0375-234">Make sure you include hello optional DocumentDB.query parameter t trim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="b0375-235">**Ter nomeado o DocumentDB.inputCollections não foi um erro.**</span><span class="sxs-lookup"><span data-stu-id="b0375-235">**Naming DocumentDB.inputCollections was not a mistake.**</span></span> <span data-ttu-id="b0375-236">Sim, nós podemos adicionar várias coleções como entrada:</span><span class="sxs-lookup"><span data-stu-id="b0375-236">Yes, we allow adding multiple collections as an input:</span></span> </br>
   >
   >

        '*DocumentDB.inputCollections*' = '*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*' A1A</br> hello collection names are separated without spaces, using only a single comma.

        # Create a Hive table using data from DocumentDB. Pass DocumentDB hello query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "drop table DocumentDB_timestamps; "  +
                            "create external table DocumentDB_timestamps(id string, ts BIGINT) "  +
                            "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' "  +
                            "tblproperties ( " +
                                "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                "'DocumentDB.key' = '<DocumentDB Primary Key>', " +
                                "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                "'DocumentDB.inputCollections' = '<DocumentDB Input Collection Name>', " +
                                "'DocumentDB.query' = 'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "

1. <span data-ttu-id="b0375-237">Em seguida, vamos criar uma tabela de Hive para a coleção de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="b0375-237">Next, let's create a Hive table for hello output collection.</span></span> <span data-ttu-id="b0375-238">Propriedades de documento de saída Olá será mês hello, dia, hora, minuto e número total de saudação de ocorrências.</span><span class="sxs-lookup"><span data-stu-id="b0375-238">hello output document properties will be hello month, day, hour, minute, and hello total number of occurrences.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b0375-239">**Mais uma vez, ter nomeado o DocumentDB.outputCollections não foi um erro.**</span><span class="sxs-lookup"><span data-stu-id="b0375-239">**Yet again, naming DocumentDB.outputCollections was not a mistake.**</span></span> <span data-ttu-id="b0375-240">Sim, nós podemos adicionar várias coleções como saída:</span><span class="sxs-lookup"><span data-stu-id="b0375-240">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="b0375-241">'*DocumentDB.outputCollections*' = '*\<Nome da Coleção de Saída do DocumentDB 1\>*,*\<Nome da Coleção de Saída do DocumentDB 2\>*'</span><span class="sxs-lookup"><span data-stu-id="b0375-241">'*DocumentDB.outputCollections*' = '*\<DocumentDB Output Collection Name 1\>*,*\<DocumentDB Output Collection Name 2\>*'</span></span> </br> <span data-ttu-id="b0375-242">nomes de coleção de saudação são separados sem espaços, usando apenas uma única vírgula.</span><span class="sxs-lookup"><span data-stu-id="b0375-242">hello collection names are separated without spaces, using only a single comma.</span></span> </br></br>
   > <span data-ttu-id="b0375-243">Os documentos são distribuídos por round robin entre várias coleções.</span><span class="sxs-lookup"><span data-stu-id="b0375-243">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="b0375-244">Um lote de documentos será armazenado em uma coleção e, em seguida, um segundo lote de documentos será armazenado na coleção de Avançar de Olá e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="b0375-244">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

       # Create a Hive table for hello output data tooDocumentDB.
       $queryStringPart2 = "drop table DocumentDB_analytics; " +
                             "create external table DocumentDB_analytics(Month INT, Day INT, Hour INT, Minute INT, Total INT) " +
                             "stored by 'com.microsoft.azure.documentdb.hive.DocumentDBStorageHandler' " +
                             "tblproperties ( " +
                                 "'DocumentDB.endpoint' = '<DocumentDB Endpoint>', " +
                                 "'DocumentDB.key' = '<DocumentDB Primary Key>', " +  
                                 "'DocumentDB.db' = '<DocumentDB Database Name>', " +
                                 "'DocumentDB.outputCollections' = '<DocumentDB Output Collection Name>' ); "
2. <span data-ttu-id="b0375-245">Por fim, vamos contagem Olá documentos por mês, dia, hora e minuto e inserir resultados Olá Olá no Hive tabela de saída.</span><span class="sxs-lookup"><span data-stu-id="b0375-245">Finally, let's tally hello documents by month, day, hour, and minute and insert hello results back into hello output Hive table.</span></span>

        # GROUP BY minute, COUNT entries for each, INSERT INTO output Hive table.
        $queryStringPart3 = "INSERT INTO table DocumentDB_analytics " +
                              "SELECT month(from_unixtime(ts)) as Month, day(from_unixtime(ts)) as Day, " +
                              "hour(from_unixtime(ts)) as Hour, minute(from_unixtime(ts)) as Minute, " +
                              "COUNT(*) AS Total " +
                              "FROM DocumentDB_timestamps " +
                              "GROUP BY month(from_unixtime(ts)), day(from_unixtime(ts)), " +
                              "hour(from_unixtime(ts)) , minute(from_unixtime(ts)); "
3. <span data-ttu-id="b0375-246">Adicione Olá toocreate de trecho de código de script uma definição de trabalho de Hive a seguir da consulta anterior hello.</span><span class="sxs-lookup"><span data-stu-id="b0375-246">Add hello following script snippet toocreate a Hive job definition from hello previous query.</span></span>

        # Create a Hive job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $hiveJobDefinition = New-AzureHDInsightHiveJobDefinition -Query $queryString

    <span data-ttu-id="b0375-247">Você também pode usar hello - arquivo alternar toospecify um arquivo de script HiveQL no HDFS.</span><span class="sxs-lookup"><span data-stu-id="b0375-247">You can also use hello -File switch toospecify a HiveQL script file on HDFS.</span></span>
4. <span data-ttu-id="b0375-248">Adicione Olá após a hora de início do trecho toosave hello e enviar o trabalho de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="b0375-248">Add hello following snippet toosave hello start time and submit hello Hive job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $hiveJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $hiveJobDefinition
5. <span data-ttu-id="b0375-249">Adicione Olá toowait para toocomplete de trabalho de Hive Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="b0375-249">Add hello following toowait for hello Hive job toocomplete.</span></span>

        # Wait for hello Hive job toocomplete.
        Wait-AzureHDInsightJob -Job $hiveJob -WaitTimeoutInSeconds 3600
6. <span data-ttu-id="b0375-250">Adicionar Olá após tooprint saudação padrão hello e saída de início e término.</span><span class="sxs-lookup"><span data-stu-id="b0375-250">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $hiveJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
7. <span data-ttu-id="b0375-251">**Execute** seu novo script!</span><span class="sxs-lookup"><span data-stu-id="b0375-251">**Run** your new script!</span></span> <span data-ttu-id="b0375-252">**Clique em** verde Olá executar botão.</span><span class="sxs-lookup"><span data-stu-id="b0375-252">**Click** hello green execute button.</span></span>
8. <span data-ttu-id="b0375-253">Verifique os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0375-253">Check hello results.</span></span> <span data-ttu-id="b0375-254">O logon no hello [Portal do Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="b0375-254">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="b0375-255">Clique em <strong>procurar</strong> no painel do lado esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0375-255">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
   2. <span data-ttu-id="b0375-256">Clique em <strong>tudo</strong> na saudação de superior direita do painel de navegação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0375-256">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
   3. <span data-ttu-id="b0375-257">Localize e clique em <strong>Contas do Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="b0375-257">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
   4. <span data-ttu-id="b0375-258">Em seguida, localizar seu <strong>conta de banco de dados do Azure Cosmos</strong>, em seguida, <strong>banco de dados do banco de dados do Azure Cosmos</strong> e sua <strong>coleção de banco de dados do Azure Cosmos</strong> associado a coleção de saída Olá especificada em a consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="b0375-258">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Hive query.</span></span></br>
   5. <span data-ttu-id="b0375-259">Por fim, clique em <strong>Gerenciador de Documentos</strong> abaixo de <strong>Ferramentas de Desenvolvedor</strong>.</span><span class="sxs-lookup"><span data-stu-id="b0375-259">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

   <span data-ttu-id="b0375-260">Você verá os resultados de saudação de sua consulta de Hive.</span><span class="sxs-lookup"><span data-stu-id="b0375-260">You will see hello results of your Hive query.</span></span>

   ![Resultados da consulta de Hive][image-hive-query-results]

## <span data-ttu-id="b0375-262"><a name="RunPig"></a>Etapa 4: Executar um trabalho do Pig usando o Cosmos DB e o HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0375-262"><a name="RunPig"></a>Step 4: Run a Pig job using Cosmos DB and HDInsight</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b0375-263">Todas as variáveis indicadas entre < > devem ser preenchidas usando suas configurações.</span><span class="sxs-lookup"><span data-stu-id="b0375-263">All variables indicated by < > must be filled in using your configuration settings.</span></span>
>
>

1. <span data-ttu-id="b0375-264">Saudação de conjunto de variáveis no seu painel de Script do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="b0375-264">Set hello following variables in your PowerShell Script pane.</span></span>

        # Provide Azure subscription name.
        $subscriptionName = "Azure Subscription Name"

        # Provide HDInsight cluster name where you want toorun hello Pig job.
        $clusterName = "Azure HDInsight Cluster Name"
2. <p><span data-ttu-id="b0375-265">Vamos começar pela cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="b0375-265">Let's begin constructing your query string.</span></span> <span data-ttu-id="b0375-266">Vamos gravar uma consulta de Pig que usa todos os documentos gerada pelo sistema carimbos de hora ( TS) e identificações exclusivas ( RID) de uma coleção de banco de dados do Azure Cosmos, também incluirá todos os documentos em um minuto hello e, em seguida, armazena os resultados de saudação volta para uma nova coleção de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b0375-266">We'll write a Pig query that takes all documents' system generated timestamps (_ts) and unique ids (_rid) from an Azure Cosmos DB collection, tallies all documents by hello minute, and then stores hello results back into a new Azure Cosmos DB collection.</span></span></p>
    <p><span data-ttu-id="b0375-267">Primeiro, carregue documentos do Cosmos DB no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0375-267">First, load documents from Cosmos DB into HDInsight.</span></span> <span data-ttu-id="b0375-268">Adicionar Olá toohello de trecho de código painel de Script do PowerShell a seguir <strong>depois</strong> trecho de código de saudação do #1.</span><span class="sxs-lookup"><span data-stu-id="b0375-268">Add hello following code snippet toohello PowerShell Script pane <strong>after</strong> hello code snippet from #1.</span></span> <span data-ttu-id="b0375-269">Certifique-se de tooadd um DocumentDB de consulta toohello tootrim de parâmetro de consulta opcional DocumentDB nossos TS toojust de documentos e RID.</span><span class="sxs-lookup"><span data-stu-id="b0375-269">Make sure tooadd a DocumentDB query toohello optional DocumentDB query parameter tootrim our documents toojust _ts and _rid.</span></span></p>

   > [!NOTE]
   > <span data-ttu-id="b0375-270">Sim, nós podemos adicionar várias coleções como entrada:</span><span class="sxs-lookup"><span data-stu-id="b0375-270">Yes, we allow adding multiple collections as an input:</span></span> </br>
   > <span data-ttu-id="b0375-271">'*\<Nome da Coleção de Entrada do DocumentDB 1\>*,*\<Nome da Coleção de Entrada do DocumentDB 2\>*'</span><span class="sxs-lookup"><span data-stu-id="b0375-271">'*\<DocumentDB Input Collection Name 1\>*,*\<DocumentDB Input Collection Name 2\>*'</span></span></br> <span data-ttu-id="b0375-272">nomes de coleção de saudação são separados sem espaços, usando apenas uma única vírgula.</span><span class="sxs-lookup"><span data-stu-id="b0375-272">hello collection names are separated without spaces, using only a single comma.</span></span> </b>
   >
   >

    <span data-ttu-id="b0375-273">Os documentos são distribuídos por round robin entre várias coleções.</span><span class="sxs-lookup"><span data-stu-id="b0375-273">Documents will be distributed round-robin across multiple collections.</span></span> <span data-ttu-id="b0375-274">Um lote de documentos será armazenado em uma coleção e, em seguida, um segundo lote de documentos será armazenado na coleção de Avançar de Olá e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="b0375-274">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>

        # Load data from Cosmos DB. Pass DocumentDB query toofilter transferred data too_rid and _ts.
        $queryStringPart1 = "DocumentDB_timestamps = LOAD '<DocumentDB Endpoint>' USING com.microsoft.azure.documentdb.pig.DocumentDBLoader( " +
                                                        "'<DocumentDB Primary Key>', " +
                                                        "'<DocumentDB Database Name>', " +
                                                        "'<DocumentDB Input Collection Name>', " +
                                                        "'SELECT r._rid AS id, r._ts AS ts FROM root r' ); "
3. <span data-ttu-id="b0375-275">Em seguida, vamos contar documentos Olá por mês hello, dia, hora, minuto e número total de saudação de ocorrências.</span><span class="sxs-lookup"><span data-stu-id="b0375-275">Next, let's tally hello documents by hello month, day, hour, minute, and hello total number of occurrences.</span></span>

       # GROUP BY minute and COUNT entries for each.
       $queryStringPart2 = "timestamp_record = FOREACH DocumentDB_timestamps GENERATE `$0#'id' as id:int, ToDate((long)(`$0#'ts') * 1000) as timestamp:datetime; " +
                           "by_minute = GROUP timestamp_record BY (GetYear(timestamp), GetMonth(timestamp), GetDay(timestamp), GetHour(timestamp), GetMinute(timestamp)); " +
                           "by_minute_count = FOREACH by_minute GENERATE FLATTEN(group) as (Year:int, Month:int, Day:int, Hour:int, Minute:int), COUNT(timestamp_record) as Total:int; "
4. <span data-ttu-id="b0375-276">Por fim, vamos armazenar resultados Olá em nossa nova coleção de saída.</span><span class="sxs-lookup"><span data-stu-id="b0375-276">Finally, let's store hello results into our new output collection.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b0375-277">Sim, nós podemos adicionar várias coleções como saída:</span><span class="sxs-lookup"><span data-stu-id="b0375-277">Yes, we allow adding multiple collections as an output:</span></span> </br>
   > <span data-ttu-id="b0375-278">'\<Nome da Coleção de Saída do DocumentDB 1\>, \<Nome da Coleção de Saída do DocumentDB 2\>'</span><span class="sxs-lookup"><span data-stu-id="b0375-278">'\<DocumentDB Output Collection Name 1\>,\<DocumentDB Output Collection Name 2\>'</span></span></br> <span data-ttu-id="b0375-279">nomes de coleção de saudação são separados sem espaços, usando apenas uma única vírgula.</span><span class="sxs-lookup"><span data-stu-id="b0375-279">hello collection names are separated without spaces, using only a single comma.</span></span></br>
   > <span data-ttu-id="b0375-280">Documenta vai ser distribuído round robin em Olá várias coleções.</span><span class="sxs-lookup"><span data-stu-id="b0375-280">Documents will be distributed round-robin across hello multiple collections.</span></span> <span data-ttu-id="b0375-281">Um lote de documentos será armazenado em uma coleção e, em seguida, um segundo lote de documentos será armazenado na coleção de Avançar de Olá e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="b0375-281">A batch of documents will be stored in one collection, then a second batch of documents will be stored in hello next collection, and so forth.</span></span>
   >
   >

        # Store output data tooCosmos DB.
        $queryStringPart3 = "STORE by_minute_count INTO '<DocumentDB Endpoint>' " +
                            "USING com.microsoft.azure.documentdb.pig.DocumentDBStorage( " +
                                "'<DocumentDB Primary Key>', " +
                                "'<DocumentDB Database Name>', " +
                                "'<DocumentDB Output Collection Name>'); "
5. <span data-ttu-id="b0375-282">Adicione Olá seguir toocreate de trecho de código de script uma definição de trabalho de Pig de consulta anterior hello.</span><span class="sxs-lookup"><span data-stu-id="b0375-282">Add hello following script snippet toocreate a Pig job definition from hello previous query.</span></span>

        # Create a Pig job definition.
        $queryString = $queryStringPart1 + $queryStringPart2 + $queryStringPart3
        $pigJobDefinition = New-AzureHDInsightPigJobDefinition -Query $queryString -StatusFolder $statusFolder

    <span data-ttu-id="b0375-283">Você também pode usar hello - arquivo alternar toospecify um arquivo de script Pig no HDFS.</span><span class="sxs-lookup"><span data-stu-id="b0375-283">You can also use hello -File switch toospecify a Pig script file on HDFS.</span></span>
6. <span data-ttu-id="b0375-284">Adicione Olá após a hora de início do trecho toosave hello e enviar o trabalho de Pig hello.</span><span class="sxs-lookup"><span data-stu-id="b0375-284">Add hello following snippet toosave hello start time and submit hello Pig job.</span></span>

        # Save hello start time and submit hello job toohello cluster.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $pigJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $pigJobDefinition
7. <span data-ttu-id="b0375-285">Adicione Olá toowait para toocomplete de trabalho de Pig Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="b0375-285">Add hello following toowait for hello Pig job toocomplete.</span></span>

        # Wait for hello Pig job toocomplete.
        Wait-AzureHDInsightJob -Job $pigJob -WaitTimeoutInSeconds 3600
8. <span data-ttu-id="b0375-286">Adicionar Olá após tooprint saudação padrão hello e saída de início e término.</span><span class="sxs-lookup"><span data-stu-id="b0375-286">Add hello following tooprint hello standard output and hello start and end times.</span></span>

        # Print hello standard error, hello standard output of hello Hive job, and hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $pigJob.JobId -StandardOutput
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
9. <span data-ttu-id="b0375-287">**Execute** seu novo script!</span><span class="sxs-lookup"><span data-stu-id="b0375-287">**Run** your new script!</span></span> <span data-ttu-id="b0375-288">**Clique em** verde Olá executar botão.</span><span class="sxs-lookup"><span data-stu-id="b0375-288">**Click** hello green execute button.</span></span>
10. <span data-ttu-id="b0375-289">Verifique os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0375-289">Check hello results.</span></span> <span data-ttu-id="b0375-290">O logon no hello [Portal do Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="b0375-290">Sign into hello [Azure Portal][azure-portal].</span></span>

    1. <span data-ttu-id="b0375-291">Clique em <strong>procurar</strong> no painel do lado esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0375-291">Click <strong>Browse</strong> on hello left-side panel.</span></span> </br>
    2. <span data-ttu-id="b0375-292">Clique em <strong>tudo</strong> na saudação de superior direita do painel de navegação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0375-292">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span> </br>
    3. <span data-ttu-id="b0375-293">Localize e clique em <strong>Contas do Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="b0375-293">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span> </br>
    4. <span data-ttu-id="b0375-294">Em seguida, localizar seu <strong>conta de banco de dados do Azure Cosmos</strong>, em seguida, <strong>banco de dados do banco de dados do Azure Cosmos</strong> e sua <strong>coleção de banco de dados do Azure Cosmos</strong> associado a coleção de saída Olá especificada em a consulta de Pig.</span><span class="sxs-lookup"><span data-stu-id="b0375-294">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your Pig query.</span></span></br>
    5. <span data-ttu-id="b0375-295">Por fim, clique em <strong>Gerenciador de Documentos</strong> abaixo de <strong>Ferramentas de Desenvolvedor</strong>.</span><span class="sxs-lookup"><span data-stu-id="b0375-295">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span></br></p>

    <span data-ttu-id="b0375-296">Você verá os resultados de saudação de sua consulta de Pig.</span><span class="sxs-lookup"><span data-stu-id="b0375-296">You will see hello results of your Pig query.</span></span>

    ![Resultados da consulta de Pig][image-pig-query-results]

## <span data-ttu-id="b0375-298"><a name="RunMapReduce"></a>Etapa 5: executar um trabalho MapReduce usando o Azure Cosmos DB e o HDInsight</span><span class="sxs-lookup"><span data-stu-id="b0375-298"><a name="RunMapReduce"></a>Step 5: Run a MapReduce job using Azure Cosmos DB and HDInsight</span></span>
1. <span data-ttu-id="b0375-299">Saudação de conjunto de variáveis no seu painel de Script do PowerShell a seguir.</span><span class="sxs-lookup"><span data-stu-id="b0375-299">Set hello following variables in your PowerShell Script pane.</span></span>

        $subscriptionName = "<SubscriptionName>"   # Azure subscription name
        $clusterName = "<ClusterName>"             # HDInsight cluster name
2. <span data-ttu-id="b0375-300">Executaremos um trabalho MapReduce que calcula o número de saudação de ocorrências para cada propriedade de documento da coleção de banco de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="b0375-300">We'll execute a MapReduce job that tallies hello number of occurrences for each Document property from your Azure Cosmos DB collection.</span></span> <span data-ttu-id="b0375-301">Adicionar este trecho de código de script **depois** trecho de saudação acima.</span><span class="sxs-lookup"><span data-stu-id="b0375-301">Add this script snippet **after** hello snippet above.</span></span>

        # Define hello MapReduce job.
        $TallyPropertiesJobDefinition = New-AzureHDInsightMapReduceJobDefinition -JarFile "wasb:///example/jars/TallyProperties-v01.jar" -ClassName "TallyProperties" -Arguments "<DocumentDB Endpoint>","<DocumentDB Primary Key>", "<DocumentDB Database Name>","<DocumentDB Input Collection Name>","<DocumentDB Output Collection Name>","<[Optional] DocumentDB Query>"

   > [!NOTE]
   > <span data-ttu-id="b0375-302">TallyProperties v01.jar vem com instalação personalizada de saudação do hello Cosmos conector para Hadoop do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="b0375-302">TallyProperties-v01.jar comes with hello custom installation of hello Cosmos DB Hadoop Connector.</span></span>
   >
   >
3. <span data-ttu-id="b0375-303">Adicione Olá trabalho MapReduce do comando toosubmit Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="b0375-303">Add hello following command toosubmit hello MapReduce job.</span></span>

        # Save hello start time and submit hello job.
        $startTime = Get-Date
        Select-AzureSubscription $subscriptionName
        $TallyPropertiesJob = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $TallyPropertiesJobDefinition | Wait-AzureHDInsightJob -WaitTimeoutInSeconds 3600  

    <span data-ttu-id="b0375-304">Além disso toohello definição de trabalho MapReduce, você também fornecer nome do cluster HDInsight Olá onde você deseja o trabalho de MapReduce toorun hello e credenciais de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0375-304">In addition toohello MapReduce job definition, you also provide hello HDInsight cluster name where you want toorun hello MapReduce job, and hello credentials.</span></span> <span data-ttu-id="b0375-305">Olá Start-AzureHDInsightJob é uma chamada assíncrona.</span><span class="sxs-lookup"><span data-stu-id="b0375-305">hello Start-AzureHDInsightJob is an asynchronized call.</span></span> <span data-ttu-id="b0375-306">conclusão de Olá toocheck de trabalho hello, use Olá *Wait-AzureHDInsightJob* cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b0375-306">toocheck hello completion of hello job, use hello *Wait-AzureHDInsightJob* cmdlet.</span></span>
4. <span data-ttu-id="b0375-307">Adicione Olá toocheck de comando a seguir erros com a execução do trabalho MapReduce hello.</span><span class="sxs-lookup"><span data-stu-id="b0375-307">Add hello following command toocheck any errors with running hello MapReduce job.</span></span>

        # Get hello job output and print hello start and end time.
        $endTime = Get-Date
        Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $TallyPropertiesJob.JobId -StandardError
        Write-Host "Start: " $startTime ", End: " $endTime -ForegroundColor Green
5. <span data-ttu-id="b0375-308">**Execute** seu novo script!</span><span class="sxs-lookup"><span data-stu-id="b0375-308">**Run** your new script!</span></span> <span data-ttu-id="b0375-309">**Clique em** verde Olá executar botão.</span><span class="sxs-lookup"><span data-stu-id="b0375-309">**Click** hello green execute button.</span></span>
6. <span data-ttu-id="b0375-310">Verifique os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0375-310">Check hello results.</span></span> <span data-ttu-id="b0375-311">O logon no hello [Portal do Azure][azure-portal].</span><span class="sxs-lookup"><span data-stu-id="b0375-311">Sign into hello [Azure Portal][azure-portal].</span></span>

   1. <span data-ttu-id="b0375-312">Clique em <strong>procurar</strong> no painel do lado esquerdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0375-312">Click <strong>Browse</strong> on hello left-side panel.</span></span>
   2. <span data-ttu-id="b0375-313">Clique em <strong>tudo</strong> na saudação de superior direita do painel de navegação de saudação.</span><span class="sxs-lookup"><span data-stu-id="b0375-313">Click <strong>everything</strong> at hello top-right of hello browse panel.</span></span>
   3. <span data-ttu-id="b0375-314">Localize e clique em <strong>Contas do Azure Cosmos DB</strong>.</span><span class="sxs-lookup"><span data-stu-id="b0375-314">Find and click <strong>Azure Cosmos DB Accounts</strong>.</span></span>
   4. <span data-ttu-id="b0375-315">Em seguida, localizar seu <strong>conta de banco de dados do Azure Cosmos</strong>, em seguida, <strong>banco de dados do banco de dados do Azure Cosmos</strong> e sua <strong>coleção de banco de dados do Azure Cosmos</strong> associado a coleção de saída Olá especificada em o trabalho de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="b0375-315">Next, find your <strong>Azure Cosmos DB Account</strong>, then <strong>Azure Cosmos DB Database</strong> and your <strong>Azure Cosmos DB Collection</strong> associated with hello output collection specified in your MapReduce job.</span></span>
   5. <span data-ttu-id="b0375-316">Por fim, clique em <strong>Gerenciador de Documentos</strong> abaixo de <strong>Ferramentas de Desenvolvedor</strong>.</span><span class="sxs-lookup"><span data-stu-id="b0375-316">Finally, click <strong>Document Explorer</strong> underneath <strong>Developer Tools</strong>.</span></span>

      <span data-ttu-id="b0375-317">Você verá os resultados de saudação do seu trabalho de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="b0375-317">You will see hello results of your MapReduce job.</span></span>

      ![Resultados da consulta de MapReduce][image-mapreduce-query-results]

## <span data-ttu-id="b0375-319"><a name="NextSteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b0375-319"><a name="NextSteps"></a>Next Steps</span></span>
<span data-ttu-id="b0375-320">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="b0375-320">Congratulations!</span></span> <span data-ttu-id="b0375-321">Você acaba de executar seus primeiros trabalhos do Hive, Pig e MapReduce usando o Azure Cosmos DB e o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b0375-321">You just ran your first Hive, Pig, and MapReduce jobs using Azure Cosmos DB and HDInsight.</span></span>

<span data-ttu-id="b0375-322">Nós abrimos o código-fonte do nosso Conector do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b0375-322">We have open sourced our Hadoop Connector.</span></span> <span data-ttu-id="b0375-323">Se estiver interessado, você poderá contribuir com o [GitHub][github].</span><span class="sxs-lookup"><span data-stu-id="b0375-323">If you're interested, you can contribute on [GitHub][github].</span></span>

<span data-ttu-id="b0375-324">toolearn mais, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="b0375-324">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="b0375-325">[Desenvolver um aplicativo Java com o DocumentDB][documentdb-java-application]</span><span class="sxs-lookup"><span data-stu-id="b0375-325">[Develop a Java application with Documentdb][documentdb-java-application]</span></span>
* <span data-ttu-id="b0375-326">[Desenvolver programas Java MapReduce para Hadoop no HDInsight][hdinsight-develop-deploy-java-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="b0375-326">[Develop Java MapReduce programs for Hadoop in HDInsight][hdinsight-develop-deploy-java-mapreduce]</span></span>
* <span data-ttu-id="b0375-327">[Começar a usar Hadoop com Hive no uso de celular tooanalyze HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="b0375-327">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="b0375-328">[Usar o MapReduce com o HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="b0375-328">[Use MapReduce with HDInsight][hdinsight-use-mapreduce]</span></span>
* <span data-ttu-id="b0375-329">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="b0375-329">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="b0375-330">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="b0375-330">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="b0375-331">[Personalizar os clusters HDInsight usando a Ação de Script][hdinsight-hadoop-customize-cluster]</span><span class="sxs-lookup"><span data-stu-id="b0375-331">[Customize HDInsight clusters using Script Action][hdinsight-hadoop-customize-cluster]</span></span>

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
