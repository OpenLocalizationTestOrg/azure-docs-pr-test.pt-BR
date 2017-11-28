---
title: "aaaConfigure políticas de Hive no HDInsight domínio - Azure | Microsoft Docs"
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
ms.openlocfilehash: 56f2bf9d872abc5f772b886fcf91c2e2422092f4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hive-policies-in-domain-joined-hdinsight-preview"></a><span data-ttu-id="05f52-103">Configurar políticas do Hive no HDInsight associado ao domínio (Visualização)</span><span class="sxs-lookup"><span data-stu-id="05f52-103">Configure Hive policies in Domain-joined HDInsight (Preview)</span></span>
<span data-ttu-id="05f52-104">Saiba como as políticas de Ranger Apache tooconfigure para o Hive.</span><span class="sxs-lookup"><span data-stu-id="05f52-104">Learn how tooconfigure Apache Ranger policies for Hive.</span></span> <span data-ttu-id="05f52-105">Neste artigo, você deve criar dois Ranger políticas toorestrict acesso toohello hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="05f52-105">In this article, you create two Ranger policies toorestrict access toohello hivesampletable.</span></span> <span data-ttu-id="05f52-106">Olá hivesampletable vem com clusters HDInsight.</span><span class="sxs-lookup"><span data-stu-id="05f52-106">hello hivesampletable comes with HDInsight clusters.</span></span> <span data-ttu-id="05f52-107">Depois que você configurou políticas hello, você usar tabelas de tooHive do Excel e ODBC driver tooconnect no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="05f52-107">After you have configured hello policies, you use Excel and ODBC driver tooconnect tooHive tables in HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="05f52-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="05f52-108">Prerequisites</span></span>
* <span data-ttu-id="05f52-109">Um cluster HDInsight associado a um domínio.</span><span class="sxs-lookup"><span data-stu-id="05f52-109">A Domain-joined HDInsight cluster.</span></span> <span data-ttu-id="05f52-110">Confira [Configurar clusters HDInsight associados ao domínio](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="05f52-110">See [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="05f52-111">Uma estação de trabalho com Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone ou Office 2010 Professional Plus.</span><span class="sxs-lookup"><span data-stu-id="05f52-111">A workstation with Office 2016, Office 2013 Professional Plus, Office 365 Pro Plus, Excel 2013 Standalone, or Office 2010 Professional Plus.</span></span>

## <a name="connect-tooapache-ranger-admin-ui"></a><span data-ttu-id="05f52-112">Conecte-se tooApache Ranger da interface do usuário de administrador</span><span class="sxs-lookup"><span data-stu-id="05f52-112">Connect tooApache Ranger Admin UI</span></span>
<span data-ttu-id="05f52-113">**tooconnect tooRanger Admin UI**</span><span class="sxs-lookup"><span data-stu-id="05f52-113">**tooconnect tooRanger Admin UI**</span></span>

1. <span data-ttu-id="05f52-114">Em um navegador, conecte-se tooRanger Admin UI.</span><span class="sxs-lookup"><span data-stu-id="05f52-114">From a browser, connect tooRanger Admin UI.</span></span> <span data-ttu-id="05f52-115">Olá URL é https://&lt;ClusterName >.azurehdinsight.net/Ranger/.</span><span class="sxs-lookup"><span data-stu-id="05f52-115">hello URL is https://&lt;ClusterName>.azurehdinsight.net/Ranger/.</span></span>

   > [!NOTE]
   > <span data-ttu-id="05f52-116">O Ranger usa credenciais diferentes das do cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="05f52-116">Ranger uses different credentials than Hadoop cluster.</span></span> <span data-ttu-id="05f52-117">navegadores tooprevent usando credenciais armazenadas em cache do Hadoop, use toohello de tooconnect nova janela de navegador inprivate Ranger da interface do usuário de administrador.</span><span class="sxs-lookup"><span data-stu-id="05f52-117">tooprevent browsers using cached Hadoop credentials, use new inprivate browser window tooconnect toohello Ranger Admin UI.</span></span>
   >
   >
2. <span data-ttu-id="05f52-118">Faça logon usando a senha e nome de usuário de domínio do administrador de cluster hello:</span><span class="sxs-lookup"><span data-stu-id="05f52-118">Log in using hello cluster administrator domain user name and password:</span></span>

    ![Home page do Ranger associado ao domínio do HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-ranger-home-page.png)

    <span data-ttu-id="05f52-120">Atualmente, o Ranger só funciona com o Hive e o Yarn.</span><span class="sxs-lookup"><span data-stu-id="05f52-120">Currently, Ranger only works with Yarn and Hive.</span></span>

## <a name="create-domain-users"></a><span data-ttu-id="05f52-121">Criar usuários de Domínio</span><span class="sxs-lookup"><span data-stu-id="05f52-121">Create Domain users</span></span>
<span data-ttu-id="05f52-122">Em [Configurar clusters HDInsight associados ao domínio](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), você criou hiveruser1 e hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="05f52-122">In [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad), you have created hiveruser1 and hiveuser2.</span></span> <span data-ttu-id="05f52-123">Você usará a conta de usuário de dois Olá neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="05f52-123">You will use hello two user account in this tutorial.</span></span>

## <a name="create-ranger-policies"></a><span data-ttu-id="05f52-124">Criar políticas do Ranger</span><span class="sxs-lookup"><span data-stu-id="05f52-124">Create Ranger policies</span></span>
<span data-ttu-id="05f52-125">Nesta seção, você criará duas políticas do Ranger para acessar hivesampletable.</span><span class="sxs-lookup"><span data-stu-id="05f52-125">In this section, you will create two Ranger policies for accessing hivesampletable.</span></span> <span data-ttu-id="05f52-126">Você pode dar permissão select em um conjunto diferente de colunas.</span><span class="sxs-lookup"><span data-stu-id="05f52-126">You give select permission on different set of columns.</span></span> <span data-ttu-id="05f52-127">Ambos os usuários foram criados em [Configurar clusters HDInsight associados ao domínio](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span><span class="sxs-lookup"><span data-stu-id="05f52-127">Both users were created in [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md#create-and-configure-azure-ad-ds-for-your-azure-ad).</span></span>  <span data-ttu-id="05f52-128">Na próxima seção, Olá, você testará duas políticas Olá no Excel.</span><span class="sxs-lookup"><span data-stu-id="05f52-128">In hello next section, you will test hello two policies in Excel.</span></span>

<span data-ttu-id="05f52-129">**políticas de Ranger toocreate**</span><span class="sxs-lookup"><span data-stu-id="05f52-129">**toocreate Ranger policies**</span></span>

1. <span data-ttu-id="05f52-130">Abrir a Interface de Usuário de Administração do Ranger.</span><span class="sxs-lookup"><span data-stu-id="05f52-130">Open Ranger Admin UI.</span></span> <span data-ttu-id="05f52-131">Consulte [conectar tooApache Ranger da interface do usuário de administrador](#connect-to-apache-ranager-admin-ui).</span><span class="sxs-lookup"><span data-stu-id="05f52-131">See [Connect tooApache Ranger Admin UI](#connect-to-apache-ranager-admin-ui).</span></span>
2. <span data-ttu-id="05f52-132">Clique em **&lt;ClusterName >_hive**, em **Hive**.</span><span class="sxs-lookup"><span data-stu-id="05f52-132">Click **&lt;ClusterName>_hive**, under **Hive**.</span></span> <span data-ttu-id="05f52-133">Você deverá ver duas políticas de pré-configuração.</span><span class="sxs-lookup"><span data-stu-id="05f52-133">You shall see two pre-configure policies.</span></span>
3. <span data-ttu-id="05f52-134">Clique em **adicionar nova política**e, em seguida, digite Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="05f52-134">Click **Add New Policy**, and then enter hello following values:</span></span>

   * <span data-ttu-id="05f52-135">Nome da política: read-hivesampletable-all</span><span class="sxs-lookup"><span data-stu-id="05f52-135">Policy name: read-hivesampletable-all</span></span>
   * <span data-ttu-id="05f52-136">Hive de Banco de Dados: padrão</span><span class="sxs-lookup"><span data-stu-id="05f52-136">Hive Database: default</span></span>
   * <span data-ttu-id="05f52-137">tabela: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="05f52-137">table: hivesampletable</span></span>
   * <span data-ttu-id="05f52-138">Coluna de hive: *</span><span class="sxs-lookup"><span data-stu-id="05f52-138">Hive column: *</span></span>
   * <span data-ttu-id="05f52-139">Selecione o usuário: hiveuser1</span><span class="sxs-lookup"><span data-stu-id="05f52-139">Select User: hiveuser1</span></span>
   * <span data-ttu-id="05f52-140">Permissões: selecionar</span><span class="sxs-lookup"><span data-stu-id="05f52-140">Permissions: select</span></span>

     ![Configurar política do Hive do Ranger associada ao domínio do HDInsight](./media/hdinsight-domain-joined-run-hive/hdinsight-domain-joined-configure-ranger-policy.png)<span data-ttu-id="05f52-142">.</span><span class="sxs-lookup"><span data-stu-id="05f52-142">.</span></span>

     > [!NOTE]
     > <span data-ttu-id="05f52-143">Se um usuário de domínio não é populado em Selecionar usuário, aguarde alguns instantes para toosync Ranger com o AAD.</span><span class="sxs-lookup"><span data-stu-id="05f52-143">If a domain user is not populated in Select User, wait a few moments for Ranger toosync with AAD.</span></span>
     >
     >
4. <span data-ttu-id="05f52-144">Clique em **adicionar** toosave política de saudação.</span><span class="sxs-lookup"><span data-stu-id="05f52-144">Click **Add** toosave hello policy.</span></span>
5. <span data-ttu-id="05f52-145">Repita Olá duas últimas etapas toocreate outra política com hello propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="05f52-145">Repeat hello last two steps toocreate another policy with hello following properties:</span></span>

   * <span data-ttu-id="05f52-146">Nome da política: read-hivesampletable-devicemake</span><span class="sxs-lookup"><span data-stu-id="05f52-146">Policy name: read-hivesampletable-devicemake</span></span>
   * <span data-ttu-id="05f52-147">Hive de Banco de Dados: padrão</span><span class="sxs-lookup"><span data-stu-id="05f52-147">Hive Database: default</span></span>
   * <span data-ttu-id="05f52-148">tabela: hivesampletable</span><span class="sxs-lookup"><span data-stu-id="05f52-148">table: hivesampletable</span></span>
   * <span data-ttu-id="05f52-149">Coluna do hive: clientid, devicemake</span><span class="sxs-lookup"><span data-stu-id="05f52-149">Hive column: clientid, devicemake</span></span>
   * <span data-ttu-id="05f52-150">Selecione o usuário: hiveuser2</span><span class="sxs-lookup"><span data-stu-id="05f52-150">Select User: hiveuser2</span></span>
   * <span data-ttu-id="05f52-151">Permissões: selecionar</span><span class="sxs-lookup"><span data-stu-id="05f52-151">Permissions: select</span></span>

## <a name="create-hive-odbc-data-source"></a><span data-ttu-id="05f52-152">Criar uma fonte de dados ODBC do Hive</span><span class="sxs-lookup"><span data-stu-id="05f52-152">Create Hive ODBC data source</span></span>
<span data-ttu-id="05f52-153">Olá instruções podem ser encontradas no [fonte de dados ODBC de Hive criar](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="05f52-153">hello instructions can be found in [Create Hive ODBC data source](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>  

    <span data-ttu-id="05f52-154">Propriedade</span><span class="sxs-lookup"><span data-stu-id="05f52-154">Property</span></span>|<span data-ttu-id="05f52-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="05f52-155">Description</span></span>
    ---|---
    <span data-ttu-id="05f52-156">Nome da fonte de dados</span><span class="sxs-lookup"><span data-stu-id="05f52-156">Data Source Name</span></span>|<span data-ttu-id="05f52-157">Dê uma fonte de dados do nome tooyour</span><span class="sxs-lookup"><span data-stu-id="05f52-157">Give a name tooyour data source</span></span>
    <span data-ttu-id="05f52-158">Host</span><span class="sxs-lookup"><span data-stu-id="05f52-158">Host</span></span>|<span data-ttu-id="05f52-159">Digite &lt;HDInsightClusterName>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="05f52-159">Enter &lt;HDInsightClusterName>.azurehdinsight.net.</span></span> <span data-ttu-id="05f52-160">Por exemplo, meu_Cluster_HDI.azurehdinsight.net</span><span class="sxs-lookup"><span data-stu-id="05f52-160">For example, myHDICluster.azurehdinsight.net</span></span>
    <span data-ttu-id="05f52-161">Port</span><span class="sxs-lookup"><span data-stu-id="05f52-161">Port</span></span>|<span data-ttu-id="05f52-162">Use <strong>443</strong>.</span><span class="sxs-lookup"><span data-stu-id="05f52-162">Use <strong>443</strong>.</span></span> <span data-ttu-id="05f52-163">(Essa porta foi alterada de 563 too443.)</span><span class="sxs-lookup"><span data-stu-id="05f52-163">(This port has been changed from 563 too443.)</span></span>
    <span data-ttu-id="05f52-164">Banco de dados</span><span class="sxs-lookup"><span data-stu-id="05f52-164">Database</span></span>|<span data-ttu-id="05f52-165">Use <strong>Padrão</strong>.</span><span class="sxs-lookup"><span data-stu-id="05f52-165">Use <strong>Default</strong>.</span></span>
    <span data-ttu-id="05f52-166">Tipo de servidor Hive</span><span class="sxs-lookup"><span data-stu-id="05f52-166">Hive Server Type</span></span>|<span data-ttu-id="05f52-167">Selecione <strong>Servidor Hive 2</strong></span><span class="sxs-lookup"><span data-stu-id="05f52-167">Select <strong>Hive Server 2</strong></span></span>
    <span data-ttu-id="05f52-168">Mecanismo</span><span class="sxs-lookup"><span data-stu-id="05f52-168">Mechanism</span></span>|<span data-ttu-id="05f52-169">Selecione <strong>Serviço do Azure HDInsight</strong></span><span class="sxs-lookup"><span data-stu-id="05f52-169">Select <strong>Azure HDInsight Service</strong></span></span>
    <span data-ttu-id="05f52-170">Caminho HTTP</span><span class="sxs-lookup"><span data-stu-id="05f52-170">HTTP Path</span></span>|<span data-ttu-id="05f52-171">Deixe em branco.</span><span class="sxs-lookup"><span data-stu-id="05f52-171">Leave it blank.</span></span>
    <span data-ttu-id="05f52-172">Nome de usuário</span><span class="sxs-lookup"><span data-stu-id="05f52-172">User Name</span></span>|<span data-ttu-id="05f52-173">Digite hiveuser1@contoso158.onmicrosoft.com. Atualize o nome de domínio de saudação se ele for diferente.</span><span class="sxs-lookup"><span data-stu-id="05f52-173">Enter hiveuser1@contoso158.onmicrosoft.com. Update hello domain name if it is different.</span></span>
    <span data-ttu-id="05f52-174">Senha</span><span class="sxs-lookup"><span data-stu-id="05f52-174">Password</span></span>|<span data-ttu-id="05f52-175">Insira a senha de saudação para hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="05f52-175">Enter hello password for hiveuser1.</span></span>
    </table>

<span data-ttu-id="05f52-176">Certifique-se de que tooclick **teste** antes de salvar a fonte de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="05f52-176">Make sure tooclick **Test** before saving hello data source.</span></span>

## <a name="import-data-into-excel-from-hdinsight"></a><span data-ttu-id="05f52-177">Importar dados do HDInsight para o Excel</span><span class="sxs-lookup"><span data-stu-id="05f52-177">Import data into Excel from HDInsight</span></span>
<span data-ttu-id="05f52-178">Na seção de última hello, você configurou duas políticas.</span><span class="sxs-lookup"><span data-stu-id="05f52-178">In hello last section, you have configured two policies.</span></span>  <span data-ttu-id="05f52-179">hiveuser1 tem Olá permissão em todas as colunas de saudação select e hiveuser2 tem Olá permissão select na duas colunas.</span><span class="sxs-lookup"><span data-stu-id="05f52-179">hiveuser1 has hello select permission on all hello columns, and hiveuser2 has hello select permission on two columns.</span></span> <span data-ttu-id="05f52-180">Nesta seção, você pode representar Olá dois usuários tooimport dados no Excel.</span><span class="sxs-lookup"><span data-stu-id="05f52-180">In this section, you impersonate hello two users tooimport data into Excel.</span></span>

1. <span data-ttu-id="05f52-181">Abra uma pasta de trabalho nova ou existente no Excel.</span><span class="sxs-lookup"><span data-stu-id="05f52-181">Open a new or existing workbook in Excel.</span></span>
2. <span data-ttu-id="05f52-182">De saudação **dados** , clique em **de outras fontes de dados**e, em seguida, clique em **do Assistente de Conexão de dados** toolaunch Olá **,AssistentedeConexãodedados**.</span><span class="sxs-lookup"><span data-stu-id="05f52-182">From hello **Data** tab, click **From Other Data Sources**, and then click **From Data Connection Wizard** toolaunch hello **Data Connection Wizard**.</span></span>

    <span data-ttu-id="05f52-183">![Assistente de conexão de dados][img-hdi-simbahiveodbc.excel.dataconnection]</span><span class="sxs-lookup"><span data-stu-id="05f52-183">![Open data connection wizard][img-hdi-simbahiveodbc.excel.dataconnection]</span></span>
3. <span data-ttu-id="05f52-184">Selecione **DSN ODBC** como fonte de dados hello e clique **próximo**.</span><span class="sxs-lookup"><span data-stu-id="05f52-184">Select **ODBC DSN** as hello data source, and then click **Next**.</span></span>
4. <span data-ttu-id="05f52-185">De fontes de dados ODBC, Olá Selecionar fonte de dados nome que você criou na etapa anterior hello e, em seguida, clique em **próximo**.</span><span class="sxs-lookup"><span data-stu-id="05f52-185">From ODBC data sources, select hello data source name that you created in hello previous step, and then  click **Next**.</span></span>
5. <span data-ttu-id="05f52-186">Digite novamente a senha Olá para cluster Olá no Assistente de saudação e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="05f52-186">Re-enter hello password for hello cluster in hello wizard, and then click **OK**.</span></span> <span data-ttu-id="05f52-187">Aguarde a saudação **Selecionar banco de dados e tabela** tooopen da caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="05f52-187">Wait for hello **Select Database and Table** dialog tooopen.</span></span> <span data-ttu-id="05f52-188">Isso pode levar alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="05f52-188">This can take a few seconds.</span></span>
6. <span data-ttu-id="05f52-189">Selecione **hivesampletable** e clique em **Avançar**.</span><span class="sxs-lookup"><span data-stu-id="05f52-189">Select **hivesampletable**, and then click **Next**.</span></span>
7. <span data-ttu-id="05f52-190">Clique em **Concluir**.</span><span class="sxs-lookup"><span data-stu-id="05f52-190">Click **Finish**.</span></span>
8. <span data-ttu-id="05f52-191">Em Olá **importar dados** caixa de diálogo, você pode alterar ou especificar Olá consulta.</span><span class="sxs-lookup"><span data-stu-id="05f52-191">In hello **Import Data** dialog, you can change or specify hello query.</span></span> <span data-ttu-id="05f52-192">toodo, clique em **propriedades**.</span><span class="sxs-lookup"><span data-stu-id="05f52-192">toodo so, click **Properties**.</span></span> <span data-ttu-id="05f52-193">Isso pode levar alguns segundos.</span><span class="sxs-lookup"><span data-stu-id="05f52-193">This can take a few seconds.</span></span>
9. <span data-ttu-id="05f52-194">Clique em Olá **definição** na guia texto do comando de saudação é:</span><span class="sxs-lookup"><span data-stu-id="05f52-194">Click hello **Definition** tab. hello command text is:</span></span>

       SELECT * FROM "HIVE"."default"."hivesampletable"

   <span data-ttu-id="05f52-195">Por políticas de Ranger Olá definidos, hiveuser1 tem permissão select em todas as colunas de saudação.</span><span class="sxs-lookup"><span data-stu-id="05f52-195">By hello Ranger policies you defined,  hiveuser1 has select permission on all hello columns.</span></span>  <span data-ttu-id="05f52-196">Então, essa consulta funciona com as credenciais de hiveuser1, mas não funciona com as credenciais de hiveuser2.</span><span class="sxs-lookup"><span data-stu-id="05f52-196">So this query works with hiveuser1's credentials, but this query does not not work with hiveuser2's credentials.</span></span>

   <span data-ttu-id="05f52-197">![Propriedades de conexão][img-hdi-simbahiveodbc-excel-connectionproperties]</span><span class="sxs-lookup"><span data-stu-id="05f52-197">![Connection Properties][img-hdi-simbahiveodbc-excel-connectionproperties]</span></span>
10. <span data-ttu-id="05f52-198">Clique em **Okey** caixa de diálogo de propriedades de Conexão de saudação tooclose.</span><span class="sxs-lookup"><span data-stu-id="05f52-198">Click **OK** tooclose hello Connection Properties dialog.</span></span>
11. <span data-ttu-id="05f52-199">Clique em **Okey** tooclose Olá **importar dados** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="05f52-199">Click **OK** tooclose hello **Import Data** dialog.</span></span>  
12. <span data-ttu-id="05f52-200">Redigite a senha de saudação para hiveuser1 e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="05f52-200">Reenter hello password for hiveuser1, and then click **OK**.</span></span> <span data-ttu-id="05f52-201">Levará alguns segundos antes de dados obtém tooExcel importado.</span><span class="sxs-lookup"><span data-stu-id="05f52-201">It takes a few seconds before data gets imported tooExcel.</span></span> <span data-ttu-id="05f52-202">Quando estiver pronto, você deverá ver 11 colunas de dados.</span><span class="sxs-lookup"><span data-stu-id="05f52-202">When it is done, you shall see 11 columns of data.</span></span>

<span data-ttu-id="05f52-203">política do tootest Olá segundo (leitura-hivesampletable-devicemake) que você criou na seção de última Olá</span><span class="sxs-lookup"><span data-stu-id="05f52-203">tootest hello second policy (read-hivesampletable-devicemake) you created in hello last section</span></span>

1. <span data-ttu-id="05f52-204">Adicione uma nova planilha no Excel.</span><span class="sxs-lookup"><span data-stu-id="05f52-204">Add a new sheet in Excel.</span></span>
2. <span data-ttu-id="05f52-205">Siga a dados do hello último procedimento tooimport Olá.</span><span class="sxs-lookup"><span data-stu-id="05f52-205">Follow hello last procedure tooimport hello data.</span></span>  <span data-ttu-id="05f52-206">alteração somente Hello, que você fará é credenciais do toouse hiveuser2 em vez do hiveuser1.</span><span class="sxs-lookup"><span data-stu-id="05f52-206">hello only change you will make is toouse hiveuser2's credentials instead of hiveuser1's.</span></span> <span data-ttu-id="05f52-207">Isso irá falhar porque hiveuser2 tem apenas duas colunas de toosee de permissão.</span><span class="sxs-lookup"><span data-stu-id="05f52-207">This will fail because hiveuser2 only has permission toosee two columns.</span></span> <span data-ttu-id="05f52-208">Você deve obter Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="05f52-208">You shall get hello following error:</span></span>

        [Microsoft][HiveODBC] (35) Error from Hive: error code: '40000' error message: 'Error while compiling statement: FAILED: HiveAccessControlException Permission denied: user [hiveuser2] does not have [SELECT] privilege on [default/hivesampletable/clientid,country ...]'.
3. <span data-ttu-id="05f52-209">Siga Olá mesmo dados de tooimport de procedimento.</span><span class="sxs-lookup"><span data-stu-id="05f52-209">Follow hello same procedure tooimport data.</span></span> <span data-ttu-id="05f52-210">Neste momento, usar credenciais do hiveuser2 e também modificar a instrução select hello from:</span><span class="sxs-lookup"><span data-stu-id="05f52-210">This time, use hiveuser2's credentials, and also modify hello select statement from:</span></span>

        SELECT * FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="05f52-211">para:</span><span class="sxs-lookup"><span data-stu-id="05f52-211">to:</span></span>

        SELECT clientid, devicemake FROM "HIVE"."default"."hivesampletable"

    <span data-ttu-id="05f52-212">Quando estiver pronto, você deverá ver duas colunas de dados importados.</span><span class="sxs-lookup"><span data-stu-id="05f52-212">When it is done, you shall see two columns of data imported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="05f52-213">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="05f52-213">Next steps</span></span>
* <span data-ttu-id="05f52-214">Para configurar um cluster HDInsight associado a um domínio, confira [Configurar clusters HDInsight associados a domínio](hdinsight-domain-joined-configure.md).</span><span class="sxs-lookup"><span data-stu-id="05f52-214">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="05f52-215">Para gerenciar um cluster HDInsight associado a um domínio, confira [Gerenciar clusters HDInsight associados a domínio](hdinsight-domain-joined-manage.md).</span><span class="sxs-lookup"><span data-stu-id="05f52-215">For managing a Domain-joined HDInsight clusters, see [Manage Domain-joined HDInsight clusters](hdinsight-domain-joined-manage.md).</span></span>
* <span data-ttu-id="05f52-216">Para executar consultas Hive usando SSH em clusters HDInsight adicionados ao domínio, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span><span class="sxs-lookup"><span data-stu-id="05f52-216">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
* <span data-ttu-id="05f52-217">Para conectar-se de Hive usando JDBC Hive, consulte [conectar tooHive no Azure HDInsight usando Olá Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="05f52-217">For Connecting Hive using Hive JDBC, see [Connect tooHive on Azure HDInsight using hello Hive JDBC driver](hdinsight-connect-hive-jdbc-driver.md)</span></span>
* <span data-ttu-id="05f52-218">Para conectar tooHadoop do Excel usando o ODBC Hive, consulte [tooHadoop Excel conectar-se com hello unidade Microsoft Hive ODBC](hdinsight-connect-excel-hive-odbc-driver.md)</span><span class="sxs-lookup"><span data-stu-id="05f52-218">For connecting Excel tooHadoop using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC drive](hdinsight-connect-excel-hive-odbc-driver.md)</span></span>
* <span data-ttu-id="05f52-219">Para conectar usando o Power Query do Excel tooHadoop, consulte [tooHadoop Excel se conectar usando o Power Query](hdinsight-connect-excel-power-query.md)</span><span class="sxs-lookup"><span data-stu-id="05f52-219">For connecting Excel tooHadoop using Power Query, see [Connect Excel tooHadoop by using Power Query](hdinsight-connect-excel-power-query.md)</span></span>
