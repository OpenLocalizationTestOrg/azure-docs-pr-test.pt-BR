---
title: "Configurar políticas do Hive no HDInsight associado ao domínio – Azure | Microsoft Docs"
description: Saiba como...
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 3fade1e5-c2e1-4ad5-b371-f95caea23f6d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: de537d5e39dd0d3f75ff802948c7372e4d65d127
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="b78f6-103">Configurar políticas do Hive no HDInsight associado ao domínio (Visualização)</span><span class="sxs-lookup"><span data-stu-id="b78f6-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="b78f6-104">Saiba como configurar políticas do Ranger Apache para o Hive.</span><span class="sxs-lookup"><span data-stu-id="b78f6-104">Learn how to configure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="b78f6-105">Neste artigo, você criará duas políticas do Ranger para restringir o acesso a hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="b78f6-105">In this article, you create two Ranger policies to restrict access to the hivesampletable.</span></span> <span data-ttu-id="b78f6-106">O hivesampletable fornecido com clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b78f6-106">The hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="b78f6-107">Depois de configurar as políticas, você usa o Excel e o driver ODBC para conectar-se a tabelas do Hive no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b78f6-107">After you have configured the policies, you use Excel and ODBC driver to connect to Hive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b78f6-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b78f6-108">Prerequisites</span></span>
* <span data-ttu-id="b78f6-109">Um cluster HDInsight associado a um domínio.</span><span class="sxs-lookup"><span data-stu-id="b78f6-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="b78f6-110">Confira [Configurar clusters HDInsight associados ao domínio](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b78f6-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="b78f6-111">Uma estação de trabalho com Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone ou Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="b78f6-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-to-apache-ranger-admin-ui"></a><span data-ttu-id="b78f6-112">Conectar-se à interface do usuário de Administração do Apache Ranger</span><span class="sxs-lookup"><span data-stu-id="b78f6-112">Connect to Apache Ranger Admin UI</span></span>
<span data-ttu-id="b78f6-113">**Para conectar-se à interface do usuário de Administrador do Ranger**</span><span class="sxs-lookup"><span data-stu-id="b78f6-113">**To connect to Ranger Admin UI**</span></span>

1. <span data-ttu-id="b78f6-114">Em um navegador, conecte-se à interface do usuário de Administrador do Ranger.</span><span class="sxs-lookup"><span data-stu-id="b78f6-114">From a browser, connect to Ranger Admin UI.</span></span> <span data-ttu-id="b78f6-115">A URL é https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span><span class="sxs-lookup"><span data-stu-id="b78f6-115">The URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="b78f6-116">O Ranger usa credenciais diferentes das do cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="b78f6-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="b78f6-117">Para evitar que os navegadores usem credenciais do Hadoop armazenadas em cache, use a nova janela de navegador inprivate para se conectar à interface do usuário de Administração do Ranger.</span><span class="sxs-lookup"><span data-stu-id="b78f6-117">To prevent browsers using cached Hadoop credentials, use new inprivate browser window to connect to the Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="b78f6-118">Faça logon usando o nome de usuário e a senha de domínio de administrador de cluster:</span><span class="sxs-lookup"><span data-stu-id="b78f6-118">Log in using the cluster administrator domain user name and password:</span></span>

    ![Home page do Ranger associado ao domínio do HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="b78f6-120">Atualmente, o Ranger só funciona com o Hive e o Yarn.</span><span class="sxs-lookup"><span data-stu-id="b78f6-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="b78f6-121">Criar usuários de Domínio</span><span class="sxs-lookup"><span data-stu-id="b78f6-121">Create Domain users</span></span>
<span data-ttu-id="b78f6-122">Em [Configurar clusters HDInsight associados ao domínio](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), você criou hiveruser1 e hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="b78f6-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="b78f6-123">Você usará a conta de usuário dois neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="b78f6-123">You will use the two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="b78f6-124">Criar políticas do Ranger</span><span class="sxs-lookup"><span data-stu-id="b78f6-124">Create Ranger policies</span></span>
<span data-ttu-id="b78f6-125">Nesta seção, você criará duas políticas do Ranger para acessar hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="b78f6-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="b78f6-126">Você pode dar permissão select em um conjunto diferente de colunas.</span><span class="sxs-lookup"><span data-stu-id="b78f6-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="b78f6-127">Ambos os usuários foram criados em [Configurar clusters HDInsight associados ao domínio](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="b78f6-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="b78f6-128">Na próxima seção, você testará as duas políticas no Excel.</span><span class="sxs-lookup"><span data-stu-id="b78f6-128">In the next section, you will test the two policies in Excel.</span></span>

<span data-ttu-id="b78f6-129">**Para criar políticas do Ranger**</span><span class="sxs-lookup"><span data-stu-id="b78f6-129">**To create Ranger policies**</span></span>

1. <span data-ttu-id="b78f6-130">Abrir a Interface de Usuário de Administração do Ranger.</span><span class="sxs-lookup"><span data-stu-id="b78f6-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="b78f6-131">Confira [Conectar-se à interface do usuário de Administração do Apache Ranger](#connect-to-apache-ranager-admin-ui).</span><span class="sxs-lookup"><span data-stu-id="b78f6-131">See [Connect to Apache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="b78f6-132">Clique em **&lt;ClusterName >_hive**, em **Hive**.</span><span class="sxs-lookup"><span data-stu-id="b78f6-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="b78f6-133">Você deverá ver duas políticas de pré-configuração.</span><span class="sxs-lookup"><span data-stu-id="b78f6-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="b78f6-134">Clique em **Adicionar Nova Política** e insira os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="b78f6-134">Click **Add New Policy**, and then enter the following values:</span></span>

   * <span data-ttu-id="b78f6-135">Nome da política: read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="b78f6-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="b78f6-136">Hive de Banco de Dados: padrão</span><span class="sxs-lookup"><span data-stu-id="b78f6-136">Hive Database: default</span></span>
   * <span data-ttu-id="b78f6-137">tabela: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="b78f6-137">table: hivesampletable</span></span>
   * <span data-ttu-id="b78f6-138">Coluna de hive: *</span><span class="sxs-lookup"><span data-stu-id="b78f6-138">Hive column: *</span></span>
   * <span data-ttu-id="b78f6-139">Selecione o usuário: hiveuser1</span><span class="sxs-lookup"><span data-stu-id="b78f6-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="b78f6-140">Permissões: selecionar</span><span class="sxs-lookup"><span data-stu-id="b78f6-140">Permissions: select</span></span>

     ![Configurar política do Hive do Ranger associada ao domínio do HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="b78f6-142">.</span><span class="sxs-lookup"><span data-stu-id="b78f6-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="b78f6-143">Se um usuário de domínio não estiver populado em Selecionar Usuário, aguarde alguns instantes para que o Ranger seja sincronizado com o AAD.</span><span class="sxs-lookup"><span data-stu-id="b78f6-143">If a domain user is not populated in Select User, wait a few moments for Ranger to sync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="b78f6-144">Clique em **Adicionar** para salvar a política.</span><span class="sxs-lookup"><span data-stu-id="b78f6-144">Click **Add** to save the policy.</span></span>
5. <span data-ttu-id="b78f6-145">Repita as duas últimas etapas para criar outra política com as seguintes propriedades:</span><span class="sxs-lookup"><span data-stu-id="b78f6-145">Repeat the last two steps to create another policy with the following properties:</span></span>

   * <span data-ttu-id="b78f6-146">Nome da política: read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="b78f6-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="b78f6-147">Hive de Banco de Dados: padrão</span><span class="sxs-lookup"><span data-stu-id="b78f6-147">Hive Database: default</span></span>
   * <span data-ttu-id="b78f6-148">tabela: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="b78f6-148">table: hivesampletable</span></span>
   * <span data-ttu-id="b78f6-149">Coluna do hive: clientid, devicemake</span><span class="sxs-lookup"><span data-stu-id="b78f6-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="b78f6-150">Selecione o usuário: hiveuser2</span><span class="sxs-lookup"><span data-stu-id="b78f6-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="b78f6-151">Permissões: selecionar</span><span class="sxs-lookup"><span data-stu-id="b78f6-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="b78f6-152">Criar uma fonte de dados ODBC do Hive</span><span class="sxs-lookup"><span data-stu-id="b78f6-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="b78f6-153">As instruções podem ser encontradas em [Criar fonte de dados ODBC do Hive](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="b78f6-153">The instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="b78f6-154">Propriedade</span><span class="sxs-lookup"><span data-stu-id="b78f6-154">Property</span></span>|<span data-ttu-id="b78f6-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="b78f6-155">Description</span></span>
    ---|---
    <span data-ttu-id="b78f6-156">Nome da fonte de dados</span><span class="sxs-lookup"><span data-stu-id="b78f6-156">Data Source Name</span></span>|<span data-ttu-id="b78f6-157">Forneça um nome para a sua fonte de dados</span><span class="sxs-lookup"><span data-stu-id="b78f6-157">Give a name to your data source</span></span>
    <span data-ttu-id="b78f6-158">Host</span><span class="sxs-lookup"><span data-stu-id="b78f6-158">Host</span></span>|<span data-ttu-id="b78f6-159">Digite &lt;HDInsightClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="b78f6-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="b78f6-160">Por exemplo, meu_Cluster_HDI.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="b78f6-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="b78f6-161">Port</span><span class="sxs-lookup"><span data-stu-id="b78f6-161">Port</span></span>|<span data-ttu-id="b78f6-162">Use <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="b78f6-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="b78f6-163">(Essa porta foi alterada de 563 para 443.)</span><span class="sxs-lookup"><span data-stu-id="b78f6-163">(This port has been changed from 563 to 443.)</span></span>
    <span data-ttu-id="b78f6-164">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="b78f6-164">Database</span></span>|<span data-ttu-id="b78f6-165">Use <strong>Padrão</strong>.</span><span class="sxs-lookup"><span data-stu-id="b78f6-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="b78f6-166">Tipo de servidor Hive</span><span class="sxs-lookup"><span data-stu-id="b78f6-166">Hive Server Type</span></span>|<span data-ttu-id="b78f6-167">Selecione <strong>Servidor Hive 2</strong></span><span class="sxs-lookup"><span data-stu-id="b78f6-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="b78f6-168">Mecanismo</span><span class="sxs-lookup"><span data-stu-id="b78f6-168">Mechanism</span></span>|<span data-ttu-id="b78f6-169">Selecione <strong>Serviço do Azure HDInsight</strong></span><span class="sxs-lookup"><span data-stu-id="b78f6-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="b78f6-170">Caminho HTTP</span><span class="sxs-lookup"><span data-stu-id="b78f6-170">HTTP Path</span></span>|<span data-ttu-id="b78f6-171">Deixe em branco.</span><span class="sxs-lookup"><span data-stu-id="b78f6-171">Leave it blank.</span></span>
    <span data-ttu-id="b78f6-172">Nome de usuário</span><span class="sxs-lookup"><span data-stu-id="b78f6-172">User Name</span></span>|<span data-ttu-id="b78f6-173">Digite hiveuser1@contoso158.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="b78f6-173">Enter hiveuser1@contoso158.onmicrosoft.com.</span></span> <span data-ttu-id="b78f6-174">Atualize o nome de domínio se ele for diferente.</span><span class="sxs-lookup"><span data-stu-id="b78f6-174">Update the domain name if it is different.</span></span>
    <span data-ttu-id="b78f6-175">Senha</span><span class="sxs-lookup"><span data-stu-id="b78f6-175">Password</span></span>|<span data-ttu-id="b78f6-176">Digite a senha para hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="b78f6-176">Enter the password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="b78f6-177">Clique em **Testar** antes de salvar a fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="b78f6-177">Make sure to click **Test** before saving the data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="b78f6-178">Importar dados do HDInsight para o Excel</span><span class="sxs-lookup"><span data-stu-id="b78f6-178">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="b78f6-179">Na última seção, você configurou duas políticas.</span><span class="sxs-lookup"><span data-stu-id="b78f6-179">In the last section, you have configured two policies.</span></span>  <span data-ttu-id="b78f6-180">hiveuser1 tem a permissão select em todas as colunas e hiveuser2 tem a permissão select em duas colunas.</span><span class="sxs-lookup"><span data-stu-id="b78f6-180">hiveuser1 has the select permission on all the columns, and hiveuser2 has the select permission on two columns.</span></span> <span data-ttu-id="b78f6-181">Nesta seção, você representa os dois usuários para importar dados para o Excel.</span><span class="sxs-lookup"><span data-stu-id="b78f6-181">In this section, you impersonate the two users to import data into Excel.</span></span>

1. <span data-ttu-id="b78f6-182">Abra uma pasta de trabalho nova ou existente no Excel.</span><span class="sxs-lookup"><span data-stu-id="b78f6-182">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="b78f6-183">Na guia **Dados**, clique em **De Outras Fontes de Dados** e clique em **Do Assistente de Conexão de Dados** para iniciar o **Assistente de Conexão de Dados**.</span><span class="sxs-lookup"><span data-stu-id="b78f6-183">From the **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** to launch the **Data Connection Wizard**.</span></span>

    <span data-ttu-id="b78f6-184">![Assistente de conexão de dados][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="b78f6-184">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="b78f6-185">Selecione **ODBC DSN** como a fonte de dados e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="b78f6-185">Select **ODBC DSN** as the data source, and then click **Next**.</span></span>
4. <span data-ttu-id="b78f6-186">Em Fontes de dados ODBC, selecione o nome da fonte de dados criada na etapa anterior e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="b78f6-186">From ODBC data sources, select the data source name that you created in the previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="b78f6-187">Digite novamente a senha para o cluster no assistente e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b78f6-187">Re-enter the password for the cluster in the wizard, and then click **OK**.</span></span> <span data-ttu-id="b78f6-188">Aguarde até que a caixa de diálogo **Selecionar Banco de Dados e Tabela** seja aberta.</span><span class="sxs-lookup"><span data-stu-id="b78f6-188">Wait for the **Select Database and Table** dialog to open.</span></span> <span data-ttu-id="b78f6-189">Isso pode levar alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="b78f6-189">This can take a few seconds.</span></span>
6. <span data-ttu-id="b78f6-190">Selecione **hivesampletable** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="b78f6-190">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="b78f6-191">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="b78f6-191">Click **Finish**.</span></span>
8. <span data-ttu-id="b78f6-192">No diálogo **Importar Dados** , você pode alterar ou especificar a consulta.</span><span class="sxs-lookup"><span data-stu-id="b78f6-192">In the **Import Data** dialog, you can change or specify the query.</span></span> <span data-ttu-id="b78f6-193">Para fazer isso, clique em **Propriedades**.</span><span class="sxs-lookup"><span data-stu-id="b78f6-193">To do so, click **Properties**.</span></span> <span data-ttu-id="b78f6-194">Isso pode levar alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="b78f6-194">This can take a few seconds.</span></span>
9. <span data-ttu-id="b78f6-195">Clique na guia **Definição**.</span><span class="sxs-lookup"><span data-stu-id="b78f6-195">Click the **Definition** tab.</span></span> <span data-ttu-id="b78f6-196">O texto do comando é:</span><span class="sxs-lookup"><span data-stu-id="b78f6-196">The command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="b78f6-197">De acordo com as políticas do Ranger definidas por você, hiveuser1 tem permissão select em todas as colunas.</span><span class="sxs-lookup"><span data-stu-id="b78f6-197">By the Ranger policies you defined,  hiveuser1 has select permission on all the columns.</span></span>  <span data-ttu-id="b78f6-198">Então, essa consulta funciona com as credenciais de hiveuser1, mas não funciona com as credenciais de hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="b78f6-198">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="b78f6-199">![Propriedades de conexão][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="b78f6-199">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="b78f6-200">Clique em **OK** para fechar o diálogo Propriedades da Conexão.</span><span class="sxs-lookup"><span data-stu-id="b78f6-200">Click **OK** to close the Connection Properties dialog.</span></span>
11. <span data-ttu-id="b78f6-201">Clique em **OK** para fechar a caixa de diálogo **Importar Dados**.</span><span class="sxs-lookup"><span data-stu-id="b78f6-201">Click **OK** to close the **Import Data** dialog.</span></span>  
12. <span data-ttu-id="b78f6-202">Digite novamente a senha para hiveuser1 e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="b78f6-202">Reenter the password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="b78f6-203">Leva alguns segundos para que os dados sejam importados para o Excel.</span><span class="sxs-lookup"><span data-stu-id="b78f6-203">It takes a few seconds before data gets imported to Excel.</span></span> <span data-ttu-id="b78f6-204">Quando estiver pronto, você deverá ver 11 colunas de dados.</span><span class="sxs-lookup"><span data-stu-id="b78f6-204">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="b78f6-205">Para testar a segunda política (read-hivesampletable-devicemake) que você criou na seção anterior</span><span class="sxs-lookup"><span data-stu-id="b78f6-205">To test the second policy (read-hivesampletable-devicemake) you created in the last section</span></span>

1. <span data-ttu-id="b78f6-206">Adicione uma nova planilha no Excel.</span><span class="sxs-lookup"><span data-stu-id="b78f6-206">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="b78f6-207">Siga o último procedimento para importar os dados.</span><span class="sxs-lookup"><span data-stu-id="b78f6-207">Follow the last procedure to import the data.</span></span>  <span data-ttu-id="b78f6-208">A única alteração que você fará é usar as credenciais de hiveuser2 em vez de hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="b78f6-208">The only change you will make is to use hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="b78f6-209">Isso falhará porque hiveuser2 só tem permissão para ver duas colunas.</span><span class="sxs-lookup"><span data-stu-id="b78f6-209">This will fail because hiveuser2 only has permission to see two columns.</span></span> <span data-ttu-id="b78f6-210">Você deverá receber o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="b78f6-210">You shall get the following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="b78f6-211">Siga o mesmo procedimento para importar dados.</span><span class="sxs-lookup"><span data-stu-id="b78f6-211">Follow the same procedure to import data.</span></span> <span data-ttu-id="b78f6-212">Desta vez, use as credenciais de hiveuser2 e também modifique a instrução select from:</span><span class="sxs-lookup"><span data-stu-id="b78f6-212">This time, use hiveuser2's credentials, and also modify the select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="b78f6-213">para:</span><span class="sxs-lookup"><span data-stu-id="b78f6-213">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="b78f6-214">Quando estiver pronto, você deverá ver duas colunas de dados importados.</span><span class="sxs-lookup"><span data-stu-id="b78f6-214">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b78f6-215">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b78f6-215">Next steps</span></span>
* <span data-ttu-id="b78f6-216">Para configurar um cluster HDInsight associado a um domínio, confira [Configurar clusters HDInsight associados a domínio](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="b78f6-216">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="b78f6-217">Para gerenciar um cluster HDInsight associado a um domínio, confira [Gerenciar clusters HDInsight associados a domínio](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="b78f6-217">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="b78f6-218">Para executar consultas Hive usando SSH em clusters HDInsight adicionados ao domínio, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="b78f6-218">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="b78f6-219">Para conectar o Hive usando o JDBC Hive, confira [Conectar ao Hive no Azure HDInsight usando o driver JDBC do Hive](hdinsight-connect-hive-jdbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="b78f6-219">For Connecting Hive using Hive JDBC, see [Connect to Hive on Azure HDInsight using the Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="b78f6-220">Para conectar o Excel ao Hadoop usando o ODBC do Hive, confira [Conectar o Excel ao Hadoop com a unidade ODBC do Microsoft Hive](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="b78f6-220">For connecting Excel to Hadoop using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="b78f6-221">Para conectar o Excel ao Hadoop usando o Power Query, confira [Conectar o Excel ao Hadoop usando o Power Query](hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="b78f6-221">For connecting Excel to Hadoop using Power Query, see [Connect Excel to Hadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
