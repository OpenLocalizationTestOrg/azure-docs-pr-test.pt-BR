---
title: aaaConnect Excel tooHadoop com hello Hive ODBC Driver - HDInsight do Azure | Microsoft Docs
description: "Saiba como tooset backup e use Olá Microsoft Hive ODBC driver para dados do Excel tooquery em clusters de HDInsight do Microsoft Excel."
keywords: hadoop excel,hive excel,hive odbc
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
tags: azure-portal
editor: cgronlun
ms.assetid: a7665a14-0211-4521-b3e7-3b26e8029cc0
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/22/2017
ms.author: jgao
ms.openlocfilehash: f01f89e7d4203c739d56079dc589fc11f4aa2174
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-excel-toohadoop-in-azure-hdinsight-with-hello-microsoft-hive-odbc-driver"></a><span data-ttu-id="1e09e-104">Conectar Excel tooHadoop no Azure HDInsight com hello Hive do Microsoft ODBC driver</span><span class="sxs-lookup"><span data-stu-id="1e09e-104">Connect Excel tooHadoop in Azure HDInsight with hello Microsoft Hive ODBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="1e09e-105">Solução de Big Data da Microsoft integra componentes do Microsoft Business Intelligence (BI) com clusters Apache Hadoop que foram implantados por hello Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e09e-105">Microsoft's Big Data solution integrates Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by hello Azure HDInsight.</span></span> <span data-ttu-id="1e09e-106">Um exemplo dessa integração é Olá capacidade tooconnect Excel toohello Hive do data warehouse de um cluster de Hadoop no HDInsight usando Olá Driver Microsoft Hive ODBC Open Database Connectivity ().</span><span class="sxs-lookup"><span data-stu-id="1e09e-106">An example of this integration is hello ability tooconnect Excel toohello Hive data warehouse of a Hadoop cluster in HDInsight using hello Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="1e09e-107">Também é possível tooconnect dados de Olá associados a um cluster HDInsight e outras fontes de dados, incluindo outra (não-HDInsight) Hadoop clusters do Excel usando Olá suplemento do Microsoft Power Query para Excel.</span><span class="sxs-lookup"><span data-stu-id="1e09e-107">It is also possible tooconnect hello data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using hello Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="1e09e-108">Para obter informações sobre como instalar e usar o Power Query, consulte [tooHDInsight Excel conectar-se com o Power Query][hdinsight-power-query].</span><span class="sxs-lookup"><span data-stu-id="1e09e-108">For information on installing and using Power Query, see [Connect Excel tooHDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="1e09e-109">Enquanto Olá etapas neste artigo pode ser usado com qualquer um Linux ou cluster HDInsight baseados no Windows, o Windows é necessária para a estação de trabalho de cliente hello.</span><span class="sxs-lookup"><span data-stu-id="1e09e-109">While hello steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for hello client workstation.</span></span>
> 
> 

<span data-ttu-id="1e09e-110">**Pré-requisitos**:</span><span class="sxs-lookup"><span data-stu-id="1e09e-110">**Prerequisites**:</span></span>

<span data-ttu-id="1e09e-111">Antes de começar este artigo, você deve ter Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="1e09e-111">Before you begin this article, you must have hello following items:</span></span>

* <span data-ttu-id="1e09e-112">**Um cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="1e09e-112">**An HDInsight cluster**.</span></span> <span data-ttu-id="1e09e-113">toocreate um, consulte [Introdução ao Azure HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="1e09e-113">toocreate one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="1e09e-114">**estação de trabalho** com Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone ou Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="1e09e-114">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="1e09e-115">Instalar o driver ODBC do Microsoft Hive</span><span class="sxs-lookup"><span data-stu-id="1e09e-115">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="1e09e-116">Baixe e instale o Microsoft ODBC Driver Hive da saudação [Centro de Download][hive-odbc-driver-download].</span><span class="sxs-lookup"><span data-stu-id="1e09e-116">Download and install Microsoft Hive ODBC Driver from hello [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="1e09e-117">Este driver pode ser instalado em versões de 32 ou 64 bits do Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 e Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="1e09e-117">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2, and Windows Server 2012.</span></span> <span data-ttu-id="1e09e-118">driver de saudação permite conexão tooAzure HDInsight (versão 1.6 e posterior) e o emulador de HDInsight do Azure (v.1.0.0.0 e posterior).</span><span class="sxs-lookup"><span data-stu-id="1e09e-118">hello driver allows connection tooAzure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="1e09e-119">Você deve instalar a versão de saudação que corresponde à versão de saudação do aplicativo hello onde você pode usar o driver ODBC hello.</span><span class="sxs-lookup"><span data-stu-id="1e09e-119">You shall install hello version that matches hello version of hello application where you use hello ODBC driver.</span></span> <span data-ttu-id="1e09e-120">Para este tutorial, o driver de saudação é usado do Office Excel.</span><span class="sxs-lookup"><span data-stu-id="1e09e-120">For this tutorial, hello driver is used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="1e09e-121">Criar uma fonte de dados ODBC do Hive</span><span class="sxs-lookup"><span data-stu-id="1e09e-121">Create Hive ODBC data source</span></span>
<span data-ttu-id="1e09e-122">Olá etapas a seguir mostram como toocreate uma fonte de dados ODBC Hive.</span><span class="sxs-lookup"><span data-stu-id="1e09e-122">hello following steps show you how toocreate a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="1e09e-123">Windows 8 ou Windows 10, pressione a tela inicial do hello Windows tooopen chave hello e, em seguida, digite **fontes de dados**.</span><span class="sxs-lookup"><span data-stu-id="1e09e-123">From Windows 8 or Windows 10, press hello Windows key tooopen hello Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="1e09e-124">Clique em **Configurar fontes de dados ODBC (32 bits)** ou **Configurar fontes de dados ODBC (64 bits)**, dependendo da sua versão do Office.</span><span class="sxs-lookup"><span data-stu-id="1e09e-124">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="1e09e-125">Se estiver usando o Windows 7, escolha **Fontes de Dados ODBC (32 bits)** ou **Fontes de Dados ODBC (64 bits)** em **Ferramentas Administrativas**.</span><span class="sxs-lookup"><span data-stu-id="1e09e-125">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="1e09e-126">Você deverá ver Olá **administrador de fonte de dados ODBC** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1e09e-126">You shall see hello **ODBC Data Source Administrator** dialog.</span></span>
   
    <span data-ttu-id="1e09e-127">![Administrador de fonte de dados ODBC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configurar um DSN usando o Administrador de Fonte de Dados ODBC")</span><span class="sxs-lookup"><span data-stu-id="1e09e-127">![OBDC data source administrator](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configure a DSN using ODBC Data Source Administrator")</span></span>

3. <span data-ttu-id="1e09e-128">Do DNS do usuário, clique em **adicionar** tooopen Olá **criar nova fonte de dados** assistente.</span><span class="sxs-lookup"><span data-stu-id="1e09e-128">From User DNS, click **Add** tooopen hello **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="1e09e-129">Selecione **Driver ODBC do Microsoft Hive** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="1e09e-129">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="1e09e-130">Você deverá ver Olá **Microsoft Hive ODBC Driver DNS instalação** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="1e09e-130">You shall see hello **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="1e09e-131">Digite ou selecione Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="1e09e-131">Type or select hello following values:</span></span>
   
   | <span data-ttu-id="1e09e-132">Propriedade</span><span class="sxs-lookup"><span data-stu-id="1e09e-132">Property</span></span> | <span data-ttu-id="1e09e-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="1e09e-133">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="1e09e-134">Nome da fonte de dados</span><span class="sxs-lookup"><span data-stu-id="1e09e-134">Data Source Name</span></span> |<span data-ttu-id="1e09e-135">Dê uma fonte de dados do nome tooyour</span><span class="sxs-lookup"><span data-stu-id="1e09e-135">Give a name tooyour data source</span></span> |
   |  <span data-ttu-id="1e09e-136">Host</span><span class="sxs-lookup"><span data-stu-id="1e09e-136">Host</span></span> |<span data-ttu-id="1e09e-137">Digite &lt;HDInsightClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="1e09e-137">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="1e09e-138">Por exemplo, meu_Cluster_HDI.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="1e09e-138">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="1e09e-139">Port</span><span class="sxs-lookup"><span data-stu-id="1e09e-139">Port</span></span> |<span data-ttu-id="1e09e-140">Use <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="1e09e-140">Use <strong>443</strong>.</span></span> <span data-ttu-id="1e09e-141">(Essa porta foi alterada de 563 too443.)</span><span class="sxs-lookup"><span data-stu-id="1e09e-141">(This port has been changed from 563 too443.)</span></span> |
   |  <span data-ttu-id="1e09e-142">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="1e09e-142">Database</span></span> |<span data-ttu-id="1e09e-143">Use <strong>Padrão</strong>.</span><span class="sxs-lookup"><span data-stu-id="1e09e-143">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="1e09e-144">Mecanismo</span><span class="sxs-lookup"><span data-stu-id="1e09e-144">Mechanism</span></span> |<span data-ttu-id="1e09e-145">Selecione <strong>Serviço do Azure HDInsight</strong></span><span class="sxs-lookup"><span data-stu-id="1e09e-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="1e09e-146">Nome de usuário</span><span class="sxs-lookup"><span data-stu-id="1e09e-146">User Name</span></span> |<span data-ttu-id="1e09e-147">Insira o nome de usuário HTTP do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e09e-147">Enter HDInsight cluster HTTP user username.</span></span> <span data-ttu-id="1e09e-148">é o nome de usuário do saudação padrão <strong>admin</strong>.</span><span class="sxs-lookup"><span data-stu-id="1e09e-148">hello default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="1e09e-149">Senha</span><span class="sxs-lookup"><span data-stu-id="1e09e-149">Password</span></span> |<span data-ttu-id="1e09e-150">Insira a senha do usuário do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1e09e-150">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="1e09e-151">Há alguns parâmetros importantes toobe ciente de quando você clica em **opções avançadas de**:</span><span class="sxs-lookup"><span data-stu-id="1e09e-151">There are some important parameters toobe aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="1e09e-152">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="1e09e-152">Parameter</span></span> | <span data-ttu-id="1e09e-153">Descrição</span><span class="sxs-lookup"><span data-stu-id="1e09e-153">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="1e09e-154">Use Consulta Nativa</span><span class="sxs-lookup"><span data-stu-id="1e09e-154">Use Native Query</span></span> |<span data-ttu-id="1e09e-155">Quando estiver selecionada, o driver ODBC Olá não tentará tooconvert TSQL em HiveQL.</span><span class="sxs-lookup"><span data-stu-id="1e09e-155">When it is selected, hello ODBC driver does NOT try tooconvert TSQL into HiveQL.</span></span> <span data-ttu-id="1e09e-156">Você deverá usar essa opção somente se estiver 100% certo de que está enviando instruções HiveQL puras.</span><span class="sxs-lookup"><span data-stu-id="1e09e-156">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="1e09e-157">Ao se conectar tooSQL servidor ou banco de dados do SQL Azure, deixe-a desmarcada.</span><span class="sxs-lookup"><span data-stu-id="1e09e-157">When connecting tooSQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="1e09e-158">Linhas buscadas por bloco</span><span class="sxs-lookup"><span data-stu-id="1e09e-158">Rows fetched per block</span></span> |<span data-ttu-id="1e09e-159">Ao buscar um grande número de registros, ajuste desse parâmetro pode ser o desempenho ideal de tooensure necessária.</span><span class="sxs-lookup"><span data-stu-id="1e09e-159">When fetching a large number of records, tuning this parameter may be required tooensure optimal performances.</span></span> |
   |  <span data-ttu-id="1e09e-160">Comprimento de coluna de cadeia de caracteres padrão, Comprimento da coluna binária e Escala da coluna decimal</span><span class="sxs-lookup"><span data-stu-id="1e09e-160">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="1e09e-161">tipo de dados de saudação comprimentos e precisões podem afetar como os dados são retornados.</span><span class="sxs-lookup"><span data-stu-id="1e09e-161">hello data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="1e09e-162">Que causem toobe informações incorretas retornado devido tooloss de precisão e/ou truncamento.</span><span class="sxs-lookup"><span data-stu-id="1e09e-162">They cause incorrect information toobe returned due tooloss of precision and/or truncation.</span></span> |

    <span data-ttu-id="1e09e-163">![Opções avançadas](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Opções de configuração de DSN avançadas")</span><span class="sxs-lookup"><span data-stu-id="1e09e-163">![Advanced options](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Advanced DSN configuration options")</span></span>

1. <span data-ttu-id="1e09e-164">Clique em **teste** tootest fonte de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e09e-164">Click **Test** tootest hello data source.</span></span> <span data-ttu-id="1e09e-165">Quando a fonte de dados hello está configurado corretamente, ele mostra *testes concluídos com êxito!*.</span><span class="sxs-lookup"><span data-stu-id="1e09e-165">When hello data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="1e09e-166">Clique em **Okey** caixa de diálogo de teste do tooclose hello.</span><span class="sxs-lookup"><span data-stu-id="1e09e-166">Click **OK** tooclose hello Test dialog.</span></span> <span data-ttu-id="1e09e-167">nova fonte de dados Olá deverá ser listado na Olá **administrador de fonte de dados ODBC**.</span><span class="sxs-lookup"><span data-stu-id="1e09e-167">hello new data source shall be listed on hello **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="1e09e-168">Clique em **Okey** tooexit Assistente de saudação.</span><span class="sxs-lookup"><span data-stu-id="1e09e-168">Click **OK** tooexit hello wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="1e09e-169">Importar dados do HDInsight para o Excel</span><span class="sxs-lookup"><span data-stu-id="1e09e-169">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="1e09e-170">Olá etapas a seguir descrevem Olá maneira tooimport dados de uma tabela de Hive em uma pasta de trabalho do Excel usando Olá fonte de dados ODBC que você criou na seção anterior hello.</span><span class="sxs-lookup"><span data-stu-id="1e09e-170">hello following steps describe hello way tooimport data from a Hive table into an Excel workbook using hello ODBC data source that you created in hello previous section.</span></span>

1. <span data-ttu-id="1e09e-171">Abra uma pasta de trabalho nova ou existente no Excel.</span><span class="sxs-lookup"><span data-stu-id="1e09e-171">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="1e09e-172">De saudação **dados** , clique em **obter dados**, clique em **de outras fontes**e, em seguida, clique em **do ODBC** toolaunch Olá  **Assistente de Conexão de dados**.</span><span class="sxs-lookup"><span data-stu-id="1e09e-172">From hello **Data** tab, click **Get Data**, click **From Other Sources**, and then click **From ODBC** toolaunch hello **Data Connection Wizard**.</span></span>
   
    <span data-ttu-id="1e09e-173">![Abrir assistente de conexão de dados](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Abrir assistente de conexão de dados")</span><span class="sxs-lookup"><span data-stu-id="1e09e-173">![Open data connection wizard](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Open data connection wizard")</span></span>
4. <span data-ttu-id="1e09e-174">Nome que você criou na seção última Olá de fonte de dados de Select hello e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="1e09e-174">Select hello data source name that you created in hello last section, and then click **OK**.</span></span>
5. <span data-ttu-id="1e09e-175">Insira o nome de usuário do Hadoop (nome da saudação padrão é admin) Olá senha e, em seguida, clique em **conectar**.</span><span class="sxs-lookup"><span data-stu-id="1e09e-175">Enter Hadoop user name (hello default name is admin) and hello password, and then click **Connect**.</span></span>
6. <span data-ttu-id="1e09e-176">No Navegador, expanda **HIVE**, expanda **padrão**, clique em **hivesampletable** e clique em **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="1e09e-176">On Navigator, expand **HIVE**, expand **default**, click **hivesampletable**, and then click **Load**.</span></span> <span data-ttu-id="1e09e-177">Levará alguns segundos antes de dados obtém tooExcel importado.</span><span class="sxs-lookup"><span data-stu-id="1e09e-177">It takes a few seconds before data gets imported tooExcel.</span></span>

    <span data-ttu-id="1e09e-178">![Navegador do ODBC Hive do HDInsight](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Assistente para conexão de dados aberto")</span><span class="sxs-lookup"><span data-stu-id="1e09e-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Open data connection wizard")</span></span>


## <a name="next-steps"></a><span data-ttu-id="1e09e-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1e09e-179">Next steps</span></span>
<span data-ttu-id="1e09e-180">Neste artigo, você aprendeu como toouse Olá dados do Hive do Microsoft ODBC driver tooretrieve de saudação HDInsight Service no Excel.</span><span class="sxs-lookup"><span data-stu-id="1e09e-180">In this article, you learned how toouse hello Microsoft Hive ODBC driver tooretrieve data from hello HDInsight Service into Excel.</span></span> <span data-ttu-id="1e09e-181">Da mesma forma, você pode recuperar dados de saudação HDInsight Service no banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="1e09e-181">Similarly, you can retrieve data from hello HDInsight Service into SQL Database.</span></span> <span data-ttu-id="1e09e-182">Também é dados tooupload possíveis em um HDInsight Service.</span><span class="sxs-lookup"><span data-stu-id="1e09e-182">It is also possible tooupload data into an HDInsight Service.</span></span> <span data-ttu-id="1e09e-183">toolearn mais, consulte:</span><span class="sxs-lookup"><span data-stu-id="1e09e-183">toolearn more, see:</span></span>

* <span data-ttu-id="1e09e-184">[Analisar dados de atraso de voo usando o HDInsight][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="1e09e-184">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="1e09e-185">[Carregar dados tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="1e09e-185">[Upload Data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="1e09e-186">[Use o Sqoop com o HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="1e09e-186">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


