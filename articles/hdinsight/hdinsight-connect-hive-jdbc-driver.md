---
title: "Consultar o Hive por meio do driver JDBC – Azure HDInsight | Microsoft Docs"
description: "Use o driver JDBC de um aplicativo Java para enviar consultas do Hive ao Hadoop no HDInsight. Conecte-se de forma programática e do cliente SQL SQuirrel."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 928f8d2a-684d-48cb-894c-11c59a5599ae
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: f2de58c2763b2ddd0926336164738929c477c4ae
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="query-hive-through-the-jdbc-driver-in-hdinsight"></a><span data-ttu-id="dee5c-104">Consultar o Hive por meio do driver JDBC no HDInsight</span><span class="sxs-lookup"><span data-stu-id="dee5c-104">Query Hive through the JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="dee5c-105">Saiba como usar o driver JDBC de um aplicativo Java para enviar consultas do Hive para Hadoop no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dee5c-105">Learn how to use the JDBC driver from a Java application to submit Hive queries to Hadoop in Azure HDInsight.</span></span> <span data-ttu-id="dee5c-106">As informações neste documento mostram como se conectar programaticamente e do cliente SQL SQuirrel.</span><span class="sxs-lookup"><span data-stu-id="dee5c-106">The information in this document demonstrates how to connect programmatically and from the SQuirrel SQL client.</span></span>

<span data-ttu-id="dee5c-107">Para obter mais informações sobre a Interface JDBC do Hive, consulte [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span><span class="sxs-lookup"><span data-stu-id="dee5c-107">For more information on the Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dee5c-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="dee5c-108">Prerequisites</span></span>

* <span data-ttu-id="dee5c-109">Um Hadoop no cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dee5c-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="dee5c-110">Tanto clusters baseados em Linux quanto em Windows funcionarão.</span><span class="sxs-lookup"><span data-stu-id="dee5c-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="dee5c-111">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="dee5c-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="dee5c-112">Para obter mais informações, confira [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight 3.3).</span><span class="sxs-lookup"><span data-stu-id="dee5c-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="dee5c-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="dee5c-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="dee5c-114">O SQuirreL é um aplicativo cliente JDBC.</span><span class="sxs-lookup"><span data-stu-id="dee5c-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="dee5c-115">O [Java Developer Kit (JDK) versão 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior.</span><span class="sxs-lookup"><span data-stu-id="dee5c-115">The [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="dee5c-116">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="dee5c-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="dee5c-117">Maven é um sistema de criação de projeto para projetos Java que é usado pelo projeto associado a este artigo.</span><span class="sxs-lookup"><span data-stu-id="dee5c-117">Maven is a project build system for Java projects that is used by the project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="dee5c-118">Cadeia de conexão JDBC</span><span class="sxs-lookup"><span data-stu-id="dee5c-118">JDBC connection string</span></span>

<span data-ttu-id="dee5c-119">Conexões JDBC para um cluster HDInsight no Azure são feitas em 443, e o tráfego é protegido usando SSL.</span><span class="sxs-lookup"><span data-stu-id="dee5c-119">JDBC connections to an HDInsight cluster on Azure are made over 443, and the traffic is secured using SSL.</span></span> <span data-ttu-id="dee5c-120">O gateway público atrás dos quais ficam os clusters redireciona o tráfego para a porta que o HiveServer2 de fato está escutando.</span><span class="sxs-lookup"><span data-stu-id="dee5c-120">The public gateway that the clusters sit behind redirects the traffic to the port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="dee5c-121">A seguir, há um exemplo de cadeia de conexão:</span><span class="sxs-lookup"><span data-stu-id="dee5c-121">The following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="dee5c-122">Substitua `CLUSTERNAME` pelo nome do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dee5c-122">Replace `CLUSTERNAME` with the name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="dee5c-123">Autenticação</span><span class="sxs-lookup"><span data-stu-id="dee5c-123">Authentication</span></span>

<span data-ttu-id="dee5c-124">Ao estabelecer a conexão, você deverá usar o nome e a senha do administrador do cluster HDInsight para se autenticar no gateway do cluster.</span><span class="sxs-lookup"><span data-stu-id="dee5c-124">When establishing the connection, you must use the HDInsight cluster admin name and password to authenticate to the cluster gateway.</span></span> <span data-ttu-id="dee5c-125">Durante a conexão de clientes JDBC como o SQuirreL SQL, você deve inserir o nome e a senha do administrador nas configurações do cliente.</span><span class="sxs-lookup"><span data-stu-id="dee5c-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter the admin name and password in client settings.</span></span>

<span data-ttu-id="dee5c-126">De um aplicativo Java, use o nome e a senha ao estabelecer uma conexão.</span><span class="sxs-lookup"><span data-stu-id="dee5c-126">From a Java application, you must use the name and password when establishing a connection.</span></span> <span data-ttu-id="dee5c-127">Por exemplo, o código Java a seguir abre uma nova conexão usando a cadeia de conexão, o nome do administrador e a senha:</span><span class="sxs-lookup"><span data-stu-id="dee5c-127">For example, the following Java code opens a new connection using the connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="dee5c-128">Conectar-se ao cliente do SQuirreL SQL</span><span class="sxs-lookup"><span data-stu-id="dee5c-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="dee5c-129">O SQuirreL SQL é um cliente JDBC que pode ser usado para executar remotamente as consultas do Hive com o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dee5c-129">SQuirreL SQL is a JDBC client that can be used to remotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="dee5c-130">As etapas a seguir pressupõem que você já tenha instalado o SQuirreL SQL.</span><span class="sxs-lookup"><span data-stu-id="dee5c-130">The following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="dee5c-131">Copie os drivers JDBC do Hive do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dee5c-131">Copy the Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="dee5c-132">Para o **HDInsight baseado em Linux**, use as etapas a seguir para baixar os arquivos jar necessários.</span><span class="sxs-lookup"><span data-stu-id="dee5c-132">For **Linux-based HDInsight**, use the following steps to download the required jar files.</span></span>

        1. <span data-ttu-id="dee5c-133">Crie um diretório que contenha os arquivos.</span><span class="sxs-lookup"><span data-stu-id="dee5c-133">Create a directory that contains the files.</span></span> <span data-ttu-id="dee5c-134">Por exemplo: `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="dee5c-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="dee5c-135">Em uma linha de comando, use os seguintes comandos para copiar os arquivos do cluster do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="dee5c-135">From a command line, use the following commands to copy the files from the HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="dee5c-136">Substitua `USERNAME` pelo nome da conta de usuário SSH para o cluster.</span><span class="sxs-lookup"><span data-stu-id="dee5c-136">Replace `USERNAME` with the SSH user account name for the cluster.</span></span> <span data-ttu-id="dee5c-137">Substitua `CLUSTERNAME` pelo nome do cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dee5c-137">Replace `CLUSTERNAME` with the HDInsight cluster name.</span></span>

    * <span data-ttu-id="dee5c-138">Para o **HDInsight baseado no Windows**, use as etapas a seguir para baixar os arquivos jar necessários.</span><span class="sxs-lookup"><span data-stu-id="dee5c-138">For **Windows-based HDInsight**, use the following steps to download the jar files.</span></span>

        1. <span data-ttu-id="dee5c-139">No portal do Azure, selecione o cluster HDInsight e selecione o ícone da **Área de Trabalho Remota**.</span><span class="sxs-lookup"><span data-stu-id="dee5c-139">From the Azure portal, select your HDInsight cluster, and then select the **Remote Desktop** icon.</span></span>

            ![Ícone da Área de Trabalho Remota](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="dee5c-141">Na folha Área de Trabalho Remota, selecione **Conectar** para se conectar ao cluster.</span><span class="sxs-lookup"><span data-stu-id="dee5c-141">On the Remote Desktop blade, use the **Connect** button to connect to the cluster.</span></span> <span data-ttu-id="dee5c-142">Se a Área de Trabalho Remota não estiver habilitada, use o formulário para fornecer um nome de usuário e uma senha e selecione **Habilitar** para habilitar a Área de Trabalho Remota para o cluster.</span><span class="sxs-lookup"><span data-stu-id="dee5c-142">If the Remote Desktop is not enabled, use the form to provide a user name and password, then select **Enable** to enable Remote Desktop for the cluster.</span></span>

            ![Folha Área de Trabalho Remota](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="dee5c-144">Depois de selecionar **Conectar**, um arquivo .rdp será baixado.</span><span class="sxs-lookup"><span data-stu-id="dee5c-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="dee5c-145">Use esse arquivo para iniciar o cliente da Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="dee5c-145">Use this file to launch the Remote Desktop client.</span></span> <span data-ttu-id="dee5c-146">Quando solicitado, use o nome de usuário e a senha inseridos para o acesso à Área de Trabalho Remota.</span><span class="sxs-lookup"><span data-stu-id="dee5c-146">When prompted, use the user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="dee5c-147">Uma vez conectado, copie os seguintes arquivos da sessão da Área de Trabalho Remota para o seu computador local.</span><span class="sxs-lookup"><span data-stu-id="dee5c-147">Once connected, copy the following files from the Remote Desktop session to your local machine.</span></span> <span data-ttu-id="dee5c-148">Coloque-os em um diretório local chamado `hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="dee5c-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="dee5c-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span><span class="sxs-lookup"><span data-stu-id="dee5c-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="dee5c-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="dee5c-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="dee5c-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="dee5c-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="dee5c-152">Os números da versão incluídos nos caminhos e os nomes de arquivo podem ser diferentes para o seu cluster.</span><span class="sxs-lookup"><span data-stu-id="dee5c-152">The version numbers included in the paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="dee5c-153">Desconecte a sessão da Área de Trabalho Remota quando terminar de copiar os arquivos.</span><span class="sxs-lookup"><span data-stu-id="dee5c-153">Disconnect the Remote Desktop session once you have finished copying the files.</span></span>

2. <span data-ttu-id="dee5c-154">Inicie o aplicativo SQuirreL SQL.</span><span class="sxs-lookup"><span data-stu-id="dee5c-154">Start the SQuirreL SQL application.</span></span> <span data-ttu-id="dee5c-155">Na parte esquerda da janela, selecione **Drivers**.</span><span class="sxs-lookup"><span data-stu-id="dee5c-155">From the left of the window, select **Drivers**.</span></span>

    ![Guia Drivers à esquerda da janela](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="dee5c-157">Nos ícones na parte superior do diálogo **Drivers**, selecione o ícone **+** para criar um driver.</span><span class="sxs-lookup"><span data-stu-id="dee5c-157">From the icons at the top of the **Drivers** dialog, select the **+** icon to create a driver.</span></span>

    ![Ícones de Drivers](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="dee5c-159">No diálogo Adicionar Driver, adicione as informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="dee5c-159">In the Add Driver dialog, add the following information:</span></span>

    * <span data-ttu-id="dee5c-160">**Nome**: Hive</span><span class="sxs-lookup"><span data-stu-id="dee5c-160">**Name**: Hive</span></span>
    * <span data-ttu-id="dee5c-161">**Exemplo de URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="dee5c-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="dee5c-162">**Caminho de Classe Adicional**: use o botão Adicionar para adicionar os arquivos jar baixados anteriormente</span><span class="sxs-lookup"><span data-stu-id="dee5c-162">**Extra Class Path**: Use the Add button to add the jar files downloaded earlier</span></span>
    * <span data-ttu-id="dee5c-163">**Nome de Classe**: org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="dee5c-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![diálogo adicionar driver](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="dee5c-165">Clique em **OK** para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="dee5c-165">Click **OK** to save these settings.</span></span>

5. <span data-ttu-id="dee5c-166">À esquerda da janela do SQuirreL SQL, selecione **Aliases**.</span><span class="sxs-lookup"><span data-stu-id="dee5c-166">On the left of the SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="dee5c-167">Em seguida, clique no ícone **+** para criar um alias de conexão.</span><span class="sxs-lookup"><span data-stu-id="dee5c-167">Then click the **+** icon to create a connection alias.</span></span>

    ![adicionar novo alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="dee5c-169">Use os valores a seguir para o diálogo **Adicionar Alias**.</span><span class="sxs-lookup"><span data-stu-id="dee5c-169">Use the following values for the **Add Alias** dialog.</span></span>

    * <span data-ttu-id="dee5c-170">**Nome**: Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="dee5c-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="dee5c-171">**Driver**: use o menu suspenso para selecionar o driver do **Hive**</span><span class="sxs-lookup"><span data-stu-id="dee5c-171">**Driver**: Use the dropdown to select the **Hive** driver</span></span>

    * <span data-ttu-id="dee5c-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="dee5c-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="dee5c-173">Substitua **CLUSTERNAME** pelo nome do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dee5c-173">Replace **CLUSTERNAME** with the name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="dee5c-174">**Nome de Usuário**: o nome de conta de logon do cluster para o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dee5c-174">**User Name**: The cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="dee5c-175">O padrão é `admin`.</span><span class="sxs-lookup"><span data-stu-id="dee5c-175">The default is `admin`.</span></span>

    * <span data-ttu-id="dee5c-176">**Senha**: a senha da conta de logon do cluster.</span><span class="sxs-lookup"><span data-stu-id="dee5c-176">**Password**: The password for the cluster login account.</span></span>

 ![diálogo adicionar alias](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="dee5c-178">Use o botão **Testar** para verificar se a conexão funciona.</span><span class="sxs-lookup"><span data-stu-id="dee5c-178">Use the **Test** button to verify that the connection works.</span></span> <span data-ttu-id="dee5c-179">Quando o diálogo **Conectar a: Hive no HDInsight** for exibido, selecione **Conectar** para executar o teste.</span><span class="sxs-lookup"><span data-stu-id="dee5c-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** to perform the test.</span></span> <span data-ttu-id="dee5c-180">Se o teste tiver êxito, você verá um diálogo **Conexão bem-sucedida**.</span><span class="sxs-lookup"><span data-stu-id="dee5c-180">If the test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="dee5c-181">Use o botão **Ok** na parte inferior do diálogo **Adicionar Alias** para salvar o alias de conexão.</span><span class="sxs-lookup"><span data-stu-id="dee5c-181">To save the connection alias, use the **Ok** button at the bottom of the **Add Alias** dialog.</span></span>

7. <span data-ttu-id="dee5c-182">Na lista suspensa **Conectar a**, na parte superior do SQuirreL SQL, selecione **Hive no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="dee5c-182">From the **Connect to** dropdown at the top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="dee5c-183">Quando solicitado, selecione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="dee5c-183">When prompted, select **Connect**.</span></span>

    ![diálogo conexão](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="dee5c-185">Uma vez conectado, insira a consulta a seguir no diálogo Consulta SQL e selecione o ícone **Executar**.</span><span class="sxs-lookup"><span data-stu-id="dee5c-185">Once connected, enter the following query into the SQL query dialog, and then select the **Run** icon.</span></span> <span data-ttu-id="dee5c-186">A área de resultados deve mostrar os resultados da consulta.</span><span class="sxs-lookup"><span data-stu-id="dee5c-186">The results area should show the results of the query.</span></span>

        select * from hivesampletable limit 10;

    ![diálogo consulta sql, incluindo os resultados](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="dee5c-188">Conectar-se de um aplicativo Java de exemplo</span><span class="sxs-lookup"><span data-stu-id="dee5c-188">Connect from an example Java application</span></span>

<span data-ttu-id="dee5c-189">Um exemplo de como usar um cliente Java para consultar o Hive no HDInsight está disponível em [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span><span class="sxs-lookup"><span data-stu-id="dee5c-189">An example of using a Java client to query Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="dee5c-190">Siga as instruções no repositório para compilar e executar o exemplo.</span><span class="sxs-lookup"><span data-stu-id="dee5c-190">Follow the instructions in the repository to build and run the sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="dee5c-191">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="dee5c-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-to-open-an-sql-connection"></a><span data-ttu-id="dee5c-192">Ocorreu um erro inesperado ao tentar abrir uma conexão SQL</span><span class="sxs-lookup"><span data-stu-id="dee5c-192">Unexpected Error occurred attempting to open an SQL connection</span></span>

<span data-ttu-id="dee5c-193">**Sintomas**: ao se conectar a um cluster HDInsight versão 3.3 ou 3.4, você poderá receber uma mensagem indicando que ocorreu um erro inesperado.</span><span class="sxs-lookup"><span data-stu-id="dee5c-193">**Symptoms**: When connecting to an HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="dee5c-194">O rastreamento de pilha para esse erro começa com as seguintes linhas:</span><span class="sxs-lookup"><span data-stu-id="dee5c-194">The stack trace for this error begins with the following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="dee5c-195">**Causa**: este erro é causado por uma incompatibilidade na versão do arquivo commons-codec.jar usada pelo SQuirreL e aquela exigida pelos componentes JDBC do Hive.</span><span class="sxs-lookup"><span data-stu-id="dee5c-195">**Cause**: This error is caused by a mismatch in the version of the commons-codec.jar file used by SQuirreL and the one required by the Hive JDBC components.</span></span>

<span data-ttu-id="dee5c-196">**Resolução**: para corrigir esse erro, use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="dee5c-196">**Resolution**: To fix this error, use the following steps:</span></span>

1. <span data-ttu-id="dee5c-197">Baixe o arquivo commons-codec.jar por meio do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dee5c-197">Download the commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="dee5c-198">Saia do SQuirreL e vá para o diretório em que o SQuirreL está instalado em seu sistema.</span><span class="sxs-lookup"><span data-stu-id="dee5c-198">Exit SQuirreL, and then go to the directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="dee5c-199">No diretório do SquirreL, sob o diretório `lib` , substitua o commons-codec.jar existente pelo baixado por meio do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dee5c-199">In the SquirreL directory, under the `lib` directory, replace the existing commons-codec.jar with the one downloaded from the HDInsight cluster.</span></span>

3. <span data-ttu-id="dee5c-200">Reinicie o SQuirreL.</span><span class="sxs-lookup"><span data-stu-id="dee5c-200">Restart SQuirreL.</span></span> <span data-ttu-id="dee5c-201">O erro não deverá ocorrer mais nas próximas conexões ao Hive no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dee5c-201">The error should no longer occur when connecting to Hive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dee5c-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dee5c-202">Next steps</span></span>

<span data-ttu-id="dee5c-203">Agora que você aprendeu a usar o JDBC para trabalhar com Hive, use os links abaixo para explorar outras maneiras de trabalhar com o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="dee5c-203">Now that you have learned how to use JDBC to work with Hive, use the following links to explore other ways to work with Azure HDInsight.</span></span>

* [<span data-ttu-id="dee5c-204">Carregar dados no HDInsight</span><span class="sxs-lookup"><span data-stu-id="dee5c-204">Upload data to HDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="dee5c-205">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="dee5c-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="dee5c-206">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="dee5c-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="dee5c-207">Usar trabalhos do MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="dee5c-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
