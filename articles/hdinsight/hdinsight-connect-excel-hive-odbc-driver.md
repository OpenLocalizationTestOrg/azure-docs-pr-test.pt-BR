---
title: "Conectar o Excel ao Hadoop com o driver ODBC do Hive – Azure HDInsight | Microsoft Docs"
description: Saiba como configurar e usar o driver ODBC do Microsoft Hive para Excel para consultar dados em clusters HDInsight no Microsoft Excel.
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
ms.openlocfilehash: 7818093e42c34ee671a035cde783a6622fb2a798
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-excel-to-hadoop-in-azure-hdinsight-with-the-microsoft-hive-odbc-driver"></a><span data-ttu-id="a204b-104">Conectar o Excel ao Hadoop no Azure HDInsight com o driver ODBC do Microsoft Hive</span><span class="sxs-lookup"><span data-stu-id="a204b-104">Connect Excel to Hadoop in Azure HDInsight with the Microsoft Hive ODBC driver</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="a204b-105">A solução de Big Data da Microsoft integra componentes do Microsoft Business Intelligence (BI) com os clusters do Apache Hadoop que foram implantados pelo Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a204b-105">Microsoft's Big Data solution integrates Microsoft Business Intelligence (BI) components with Apache Hadoop clusters that have been deployed by the Azure HDInsight.</span></span> <span data-ttu-id="a204b-106">Um exemplo dessa integração é a capacidade de conectar o Excel ao data warehouse do Hive de um cluster Hadoop no HDInsight usando o driver ODBC do Microsoft Hive.</span><span class="sxs-lookup"><span data-stu-id="a204b-106">An example of this integration is the ability to connect Excel to the Hive data warehouse of a Hadoop cluster in HDInsight using the Microsoft Hive Open Database Connectivity (ODBC) Driver.</span></span>

<span data-ttu-id="a204b-107">Também é possível conectar os dados associados a um cluster HDInsight e outras fontes de dados, incluindo outros clusters Hadoop (não HDInsight), do Excel usando o suplemento Microsoft Power Query para Excel.</span><span class="sxs-lookup"><span data-stu-id="a204b-107">It is also possible to connect the data associated with an HDInsight cluster and other data sources, including other (non-HDInsight) Hadoop clusters, from Excel using the Microsoft Power Query add-in for Excel.</span></span> <span data-ttu-id="a204b-108">Para obter informações sobre como instalar e usar o Power Query, confira [Conectar o Excel ao HDInsight com o Power Query][hdinsight-power-query].</span><span class="sxs-lookup"><span data-stu-id="a204b-108">For information on installing and using Power Query, see [Connect Excel to HDInsight with Power Query][hdinsight-power-query].</span></span>

> [!NOTE]
> <span data-ttu-id="a204b-109">Embora as etapas deste artigo possam ser usadas com um cluster HDInsight com base no Linux ou Windows, é preciso ter o Windows para a estação de trabalho cliente.</span><span class="sxs-lookup"><span data-stu-id="a204b-109">While the steps in this article can be used with either a Linux or Windows-based HDInsight cluster, Windows is required for the client workstation.</span></span>
> 
> 

<span data-ttu-id="a204b-110">**Pré-requisitos**:</span><span class="sxs-lookup"><span data-stu-id="a204b-110">**Prerequisites**:</span></span>

<span data-ttu-id="a204b-111">Antes de começar este artigo, você deve ter os seguintes itens:</span><span class="sxs-lookup"><span data-stu-id="a204b-111">Before you begin this article, you must have the following items:</span></span>

* <span data-ttu-id="a204b-112">**Um cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a204b-112">**An HDInsight cluster**.</span></span> <span data-ttu-id="a204b-113">Para criar um, confira [Introdução ao Azure HDInsight][hdinsight-get-started].</span><span class="sxs-lookup"><span data-stu-id="a204b-113">To create one, see [Get started with Azure HDInsight][hdinsight-get-started].</span></span>
* <span data-ttu-id="a204b-114">**estação de trabalho** com Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone ou Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="a204b-114">**A workstation** with Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="install-microsoft-hive-odbc-driver"></a><span data-ttu-id="a204b-115">Instalar o driver ODBC do Microsoft Hive</span><span class="sxs-lookup"><span data-stu-id="a204b-115">Install Microsoft Hive ODBC driver</span></span>
<span data-ttu-id="a204b-116">Baixe e instale o driver ODBC do Microsoft Hive no [Centro de download][hive-odbc-driver-download].</span><span class="sxs-lookup"><span data-stu-id="a204b-116">Download and install Microsoft Hive ODBC Driver from the [Download Center][hive-odbc-driver-download].</span></span>

<span data-ttu-id="a204b-117">Este driver pode ser instalado em versões de 32 ou 64 bits do Windows 7, Windows 8, Windows 10, Windows Server 2008 R2 e Windows Server 2012.</span><span class="sxs-lookup"><span data-stu-id="a204b-117">This driver can be installed on 32-bit or 64-bit versions of Windows 7, Windows 8, Windows 10, Windows Server 2008 R2, and Windows Server 2012.</span></span> <span data-ttu-id="a204b-118">O driver permite a conexão com o Azure HDInsight (versão 1.6 ou posterior) e o Emulador do Azure HDInsight (1.0.0.0 e posterior).</span><span class="sxs-lookup"><span data-stu-id="a204b-118">The driver allows connection to Azure HDInsight (version 1.6 and later) and Azure HDInsight Emulator (v.1.0.0.0 and later).</span></span> <span data-ttu-id="a204b-119">Você deve instalar a versão que corresponda à versão do aplicativo onde você usa o driver ODBC.</span><span class="sxs-lookup"><span data-stu-id="a204b-119">You shall install the version that matches the version of the application where you use the ODBC driver.</span></span> <span data-ttu-id="a204b-120">Para este tutorial, o driver é usado do Office Excel.</span><span class="sxs-lookup"><span data-stu-id="a204b-120">For this tutorial, the driver is used from Office Excel.</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="a204b-121">Criar uma fonte de dados ODBC do Hive</span><span class="sxs-lookup"><span data-stu-id="a204b-121">Create Hive ODBC data source</span></span>
<span data-ttu-id="a204b-122">As etapas a seguir mostram como criar uma fonte de dados ODBC do Hive.</span><span class="sxs-lookup"><span data-stu-id="a204b-122">The following steps show you how to create a Hive ODBC Data Source.</span></span>

1. <span data-ttu-id="a204b-123">No Windows 8 ou no Windows 10, pressione a tecla Windows para abrir a tela Iniciar e digite **fontes de dados**.</span><span class="sxs-lookup"><span data-stu-id="a204b-123">From Windows 8 or Windows 10, press the Windows key to open the Start screen, and then type **data sources**.</span></span>
2. <span data-ttu-id="a204b-124">Clique em **Configurar fontes de dados ODBC (32 bits)** ou **Configurar fontes de dados ODBC (64 bits)**, dependendo da sua versão do Office.</span><span class="sxs-lookup"><span data-stu-id="a204b-124">Click **Set up ODBC Data sources (32-bit)** or **Set up ODBC Data Sources (64-bit)** depending on your Office version.</span></span> <span data-ttu-id="a204b-125">Se estiver usando o Windows 7, escolha **Fontes de Dados ODBC (32 bits)** ou **Fontes de Dados ODBC (64 bits)** em **Ferramentas Administrativas**.</span><span class="sxs-lookup"><span data-stu-id="a204b-125">If you are using Windows 7, choose **ODBC Data Sources (32 bit)** or **ODBC Data Sources (64 bit)** from **Administrative Tools**.</span></span> <span data-ttu-id="a204b-126">Você deverá ver a caixa de diálogo **Administrador de Fonte de Dados ODBC**.</span><span class="sxs-lookup"><span data-stu-id="a204b-126">You shall see the **ODBC Data Source Administrator** dialog.</span></span>
   
    <span data-ttu-id="a204b-127">![Administrador de fonte de dados ODBC](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configurar um DSN usando o Administrador de Fonte de Dados ODBC")</span><span class="sxs-lookup"><span data-stu-id="a204b-127">![OBDC data source administrator](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.DataSourceAdmin1.png "Configure a DSN using ODBC Data Source Administrator")</span></span>

3. <span data-ttu-id="a204b-128">No DNS do Usuário, clique em **Adicionar** para abrir o assistente **Criar Nova Fonte de Dados**.</span><span class="sxs-lookup"><span data-stu-id="a204b-128">From User DNS, click **Add** to open the **Create New Data Source** wizard.</span></span>
4. <span data-ttu-id="a204b-129">Selecione **Driver ODBC do Microsoft Hive** e clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="a204b-129">Select **Microsoft Hive ODBC Driver**, and then click **Finish**.</span></span> <span data-ttu-id="a204b-130">Você deverá ver a caixa de diálogo **Configuração DNS do Driver ODBC do Microsoft Hive**.</span><span class="sxs-lookup"><span data-stu-id="a204b-130">You shall see the **Microsoft Hive ODBC Driver DNS Setup** dialog.</span></span>
5. <span data-ttu-id="a204b-131">Digite ou selecione os valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="a204b-131">Type or select the following values:</span></span>
   
   | <span data-ttu-id="a204b-132">Propriedade</span><span class="sxs-lookup"><span data-stu-id="a204b-132">Property</span></span> | <span data-ttu-id="a204b-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="a204b-133">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="a204b-134">Nome da fonte de dados</span><span class="sxs-lookup"><span data-stu-id="a204b-134">Data Source Name</span></span> |<span data-ttu-id="a204b-135">Forneça um nome para a sua fonte de dados</span><span class="sxs-lookup"><span data-stu-id="a204b-135">Give a name to your data source</span></span> |
   |  <span data-ttu-id="a204b-136">Host</span><span class="sxs-lookup"><span data-stu-id="a204b-136">Host</span></span> |<span data-ttu-id="a204b-137">Digite &lt;HDInsightClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="a204b-137">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="a204b-138">Por exemplo, meu_Cluster_HDI.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="a204b-138">For example, myHDICluster.azurehdinsight.net</span></span> |
   |  <span data-ttu-id="a204b-139">Port</span><span class="sxs-lookup"><span data-stu-id="a204b-139">Port</span></span> |<span data-ttu-id="a204b-140">Use <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="a204b-140">Use <strong>443</strong>.</span></span> <span data-ttu-id="a204b-141">(Essa porta foi alterada de 563 para 443.)</span><span class="sxs-lookup"><span data-stu-id="a204b-141">(This port has been changed from 563 to 443.)</span></span> |
   |  <span data-ttu-id="a204b-142">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="a204b-142">Database</span></span> |<span data-ttu-id="a204b-143">Use <strong>Padrão</strong>.</span><span class="sxs-lookup"><span data-stu-id="a204b-143">Use <strong>Default</strong>.</span></span> |
   |  <span data-ttu-id="a204b-144">Mecanismo</span><span class="sxs-lookup"><span data-stu-id="a204b-144">Mechanism</span></span> |<span data-ttu-id="a204b-145">Selecione <strong>Serviço do Azure HDInsight</strong></span><span class="sxs-lookup"><span data-stu-id="a204b-145">Select <strong>Azure HDInsight Service</strong></span></span> |
   |  <span data-ttu-id="a204b-146">Nome de usuário</span><span class="sxs-lookup"><span data-stu-id="a204b-146">User Name</span></span> |<span data-ttu-id="a204b-147">Insira o nome de usuário HTTP do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a204b-147">Enter HDInsight cluster HTTP user username.</span></span> <span data-ttu-id="a204b-148">O nome de usuário padrão é <strong>admin</strong>.</span><span class="sxs-lookup"><span data-stu-id="a204b-148">The default username is <strong>admin</strong>.</span></span> |
   |  <span data-ttu-id="a204b-149">Senha</span><span class="sxs-lookup"><span data-stu-id="a204b-149">Password</span></span> |<span data-ttu-id="a204b-150">Insira a senha do usuário do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a204b-150">Enter HDInsight cluster user password.</span></span> |
   
    </table>
   
    <span data-ttu-id="a204b-151">Há alguns parâmetros importantes a serem lembrados ao clicar em **Opções Avançadas**.</span><span class="sxs-lookup"><span data-stu-id="a204b-151">There are some important parameters to be aware of when you click **Advanced Options**:</span></span>
   
   | <span data-ttu-id="a204b-152">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="a204b-152">Parameter</span></span> | <span data-ttu-id="a204b-153">Descrição</span><span class="sxs-lookup"><span data-stu-id="a204b-153">Description</span></span> |
   | --- | --- |
   |  <span data-ttu-id="a204b-154">Use Consulta Nativa</span><span class="sxs-lookup"><span data-stu-id="a204b-154">Use Native Query</span></span> |<span data-ttu-id="a204b-155">Quando selecionado, o driver ODBC NÃO tenta converter TSQL em HiveQL.</span><span class="sxs-lookup"><span data-stu-id="a204b-155">When it is selected, the ODBC driver does NOT try to convert TSQL into HiveQL.</span></span> <span data-ttu-id="a204b-156">Você deverá usar essa opção somente se estiver 100% certo de que está enviando instruções HiveQL puras.</span><span class="sxs-lookup"><span data-stu-id="a204b-156">You shall use it only if you are 100% sure you are submitting pure HiveQL statements.</span></span> <span data-ttu-id="a204b-157">Ao conectar-se ao SQL Server ou ao Banco de Dados SQL do Azure, deixe-a desmarcada.</span><span class="sxs-lookup"><span data-stu-id="a204b-157">When connecting to SQL Server or Azure SQL Database, you should leave it unchecked.</span></span> |
   |  <span data-ttu-id="a204b-158">Linhas buscadas por bloco</span><span class="sxs-lookup"><span data-stu-id="a204b-158">Rows fetched per block</span></span> |<span data-ttu-id="a204b-159">Ao buscar uma grande quantidade de registros, o ajuste desse parâmetro poderá ser necessário para garantir o desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="a204b-159">When fetching a large number of records, tuning this parameter may be required to ensure optimal performances.</span></span> |
   |  <span data-ttu-id="a204b-160">Comprimento de coluna de cadeia de caracteres padrão, Comprimento da coluna binária e Escala da coluna decimal</span><span class="sxs-lookup"><span data-stu-id="a204b-160">Default string column length, Binary column length, Decimal column scale</span></span> |<span data-ttu-id="a204b-161">Os tamanhos e as precisões dos tipos de dados podem afetar a maneira como os dados são retornados.</span><span class="sxs-lookup"><span data-stu-id="a204b-161">The data type lengths and precisions may affect how data is returned.</span></span> <span data-ttu-id="a204b-162">Eles farão com que informações incorretas sejam retornadas devido à perda de precisão e/ou truncamento.</span><span class="sxs-lookup"><span data-stu-id="a204b-162">They cause incorrect information to be returned due to loss of precision and/or truncation.</span></span> |

    <span data-ttu-id="a204b-163">![Opções avançadas](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Opções de configuração de DSN avançadas")</span><span class="sxs-lookup"><span data-stu-id="a204b-163">![Advanced options](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.HiveOdbc.DataSource.AdvancedOptions1.png "Advanced DSN configuration options")</span></span>

1. <span data-ttu-id="a204b-164">Clique em **Testar** para testar a fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="a204b-164">Click **Test** to test the data source.</span></span> <span data-ttu-id="a204b-165">Quando a fonte de dados estiver configurada corretamente, será mostrado *TESTES CONCLUÍDOS COM ÊXITO!*.</span><span class="sxs-lookup"><span data-stu-id="a204b-165">When the data source is configured correctly, it shows *TESTS COMPLETED SUCCESSFULLY!*.</span></span>
2. <span data-ttu-id="a204b-166">Clique em **OK** para fechar o diálogo Testar.</span><span class="sxs-lookup"><span data-stu-id="a204b-166">Click **OK** to close the Test dialog.</span></span> <span data-ttu-id="a204b-167">A nova fonte de dados deve estar listada no **Administrador de Fonte de Dados ODBC**.</span><span class="sxs-lookup"><span data-stu-id="a204b-167">The new data source shall be listed on the **ODBC Data Source Administrator**.</span></span>
3. <span data-ttu-id="a204b-168">Clique em **OK** para sair do assistente.</span><span class="sxs-lookup"><span data-stu-id="a204b-168">Click **OK** to exit the wizard.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="a204b-169">Importar dados do HDInsight para o Excel</span><span class="sxs-lookup"><span data-stu-id="a204b-169">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="a204b-170">As etapas a seguir descrevem a maneira de importar dados de uma tabela Hive em uma pasta de trabalho do Excel usando a fonte de dados ODBC que você criou na seção anterior.</span><span class="sxs-lookup"><span data-stu-id="a204b-170">The following steps describe the way to import data from a Hive table into an Excel workbook using the ODBC data source that you created in the previous section.</span></span>

1. <span data-ttu-id="a204b-171">Abra uma pasta de trabalho nova ou existente no Excel.</span><span class="sxs-lookup"><span data-stu-id="a204b-171">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="a204b-172">Na guia **Dados**, clique em **Obter Dados**, em **De Outras Fontes** e em **Do ODBC** para iniciar o **Assistente para Conexão de Dados**.</span><span class="sxs-lookup"><span data-stu-id="a204b-172">From the **Data** tab, click **Get Data**, click **From Other Sources**, and then click **From ODBC** to launch the **Data Connection Wizard**.</span></span>
   
    <span data-ttu-id="a204b-173">![Abrir assistente de conexão de dados](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Abrir assistente de conexão de dados")</span><span class="sxs-lookup"><span data-stu-id="a204b-173">![Open data connection wizard](./media/hdinsight-connect-excel-hive-ODBC-driver/HDI.SimbaHiveOdbc.Excel.DataConnection1.png "Open data connection wizard")</span></span>
4. <span data-ttu-id="a204b-174">Selecione o nome da fonte de dados que você criou na última seção e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a204b-174">Select the data source name that you created in the last section, and then click **OK**.</span></span>
5. <span data-ttu-id="a204b-175">Insira o nome de usuário do Hadoop (o nome padrão é admin) e a senha e, em seguida, clique em **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="a204b-175">Enter Hadoop user name (the default name is admin) and the password, and then click **Connect**.</span></span>
6. <span data-ttu-id="a204b-176">No Navegador, expanda **HIVE**, expanda **padrão**, clique em **hivesampletable** e clique em **Carregar**.</span><span class="sxs-lookup"><span data-stu-id="a204b-176">On Navigator, expand **HIVE**, expand **default**, click **hivesampletable**, and then click **Load**.</span></span> <span data-ttu-id="a204b-177">Leva alguns segundos para que os dados sejam importados para o Excel.</span><span class="sxs-lookup"><span data-stu-id="a204b-177">It takes a few seconds before data gets imported to Excel.</span></span>

    <span data-ttu-id="a204b-178">![Navegador do ODBC Hive do HDInsight](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Assistente para conexão de dados aberto")</span><span class="sxs-lookup"><span data-stu-id="a204b-178">![HDInsight Hive ODBC navigator](./media/hdinsight-connect-excel-hive-ODBC-driver/hdinsight.hive.odbc.navigator.png "Open data connection wizard")</span></span>


## <a name="next-steps"></a><span data-ttu-id="a204b-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a204b-179">Next steps</span></span>
<span data-ttu-id="a204b-180">Neste artigo você aprendeu a usar o driver ODBC do Microsoft Hive para recuperar dados do Serviço do HDInsight no Excel.</span><span class="sxs-lookup"><span data-stu-id="a204b-180">In this article, you learned how to use the Microsoft Hive ODBC driver to retrieve data from the HDInsight Service into Excel.</span></span> <span data-ttu-id="a204b-181">Da mesma forma, você pode recuperar dados do Serviço do HDInsight no Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="a204b-181">Similarly, you can retrieve data from the HDInsight Service into SQL Database.</span></span> <span data-ttu-id="a204b-182">Também é possível carregar dados em um Serviço do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a204b-182">It is also possible to upload data into an HDInsight Service.</span></span> <span data-ttu-id="a204b-183">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="a204b-183">To learn more, see:</span></span>

* <span data-ttu-id="a204b-184">[Analisar dados de atraso de voo usando o HDInsight][hdinsight-analyze-flight-data]</span><span class="sxs-lookup"><span data-stu-id="a204b-184">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]</span></span>
* <span data-ttu-id="a204b-185">[Carregar Dados no HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="a204b-185">[Upload Data to HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="a204b-186">[Use o Sqoop com o HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="a204b-186">[Use Sqoop with HDInsight][hdinsight-use-sqoop]</span></span>

[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-get-started]: hdinsight-hadoop-tutorial-get-started-windows.md

[hive-odbc-driver-download]: http://go.microsoft.com/fwlink/?LinkID=286698


