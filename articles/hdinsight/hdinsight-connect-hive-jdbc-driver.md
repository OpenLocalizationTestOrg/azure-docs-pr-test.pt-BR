---
title: "aaaQuery Hive por meio do driver JDBC Olá - HDInsight do Azure | Microsoft Docs"
description: "Use o driver JDBC de saudação de um tooHadoop de consultas de Hive do Java aplicativo toosubmit no HDInsight. Conecte-se por meio de programação e do cliente de SQL esquilo hello."
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
ms.openlocfilehash: 93178da3b8d497faa4c788e91dba89c4e45d3fff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a><span data-ttu-id="ac850-104">Consulta de Hive por meio do driver JDBC Olá no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ac850-104">Query Hive through hello JDBC driver in HDInsight</span></span>

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

<span data-ttu-id="ac850-105">Saiba como o JDBC driver toouse Olá de um aplicativo de Java toosubmit Hive consultas tooHadoop no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac850-105">Learn how toouse hello JDBC driver from a Java application toosubmit Hive queries tooHadoop in Azure HDInsight.</span></span> <span data-ttu-id="ac850-106">informações de saudação neste documento demonstra como tooconnect programaticamente e da saudação esquilo SQL client.</span><span class="sxs-lookup"><span data-stu-id="ac850-106">hello information in this document demonstrates how tooconnect programmatically and from hello SQuirrel SQL client.</span></span>

<span data-ttu-id="ac850-107">Para obter mais informações sobre Olá Hive JDBC Interface, consulte [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span><span class="sxs-lookup"><span data-stu-id="ac850-107">For more information on hello Hive JDBC Interface, see [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ac850-108">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ac850-108">Prerequisites</span></span>

* <span data-ttu-id="ac850-109">Um Hadoop no cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac850-109">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="ac850-110">Tanto clusters baseados em Linux quanto em Windows funcionarão.</span><span class="sxs-lookup"><span data-stu-id="ac850-110">Either Linux-based or Windows-based clusters work.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="ac850-111">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ac850-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="ac850-112">Para obter mais informações, confira [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight 3.3).</span><span class="sxs-lookup"><span data-stu-id="ac850-112">For more information, see [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="ac850-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span><span class="sxs-lookup"><span data-stu-id="ac850-113">[SQuirreL SQL](http://squirrel-sql.sourceforge.net/).</span></span> <span data-ttu-id="ac850-114">O SQuirreL é um aplicativo cliente JDBC.</span><span class="sxs-lookup"><span data-stu-id="ac850-114">SQuirreL is a JDBC client application.</span></span>

* <span data-ttu-id="ac850-115">Olá [Java Developer Kit (JDK) versão 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior.</span><span class="sxs-lookup"><span data-stu-id="ac850-115">hello [Java Developer Kit (JDK) version 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span>

* <span data-ttu-id="ac850-116">[Apache Maven](https://maven.apache.org).</span><span class="sxs-lookup"><span data-stu-id="ac850-116">[Apache Maven](https://maven.apache.org).</span></span> <span data-ttu-id="ac850-117">Maven é um projeto de criar o sistema para projetos Java que é usado pelo projeto Olá associado a este artigo.</span><span class="sxs-lookup"><span data-stu-id="ac850-117">Maven is a project build system for Java projects that is used by hello project associated with this article.</span></span>

## <a name="jdbc-connection-string"></a><span data-ttu-id="ac850-118">Cadeia de conexão JDBC</span><span class="sxs-lookup"><span data-stu-id="ac850-118">JDBC connection string</span></span>

<span data-ttu-id="ac850-119">Cluster do HDInsight tooan JDBC conexões no Azure são feitas em 443 e tráfego de saudação é protegido usando SSL.</span><span class="sxs-lookup"><span data-stu-id="ac850-119">JDBC connections tooan HDInsight cluster on Azure are made over 443, and hello traffic is secured using SSL.</span></span> <span data-ttu-id="ac850-120">gateway Olá pública clusters Olá ficam atrás redireciona toohello porta Olá tráfego HiveServer2 realmente está escutando.</span><span class="sxs-lookup"><span data-stu-id="ac850-120">hello public gateway that hello clusters sit behind redirects hello traffic toohello port that HiveServer2 is actually listening on.</span></span> <span data-ttu-id="ac850-121">a seguir Olá é uma cadeia de caracteres de conexão de exemplo:</span><span class="sxs-lookup"><span data-stu-id="ac850-121">hello following is an example connection string:</span></span>

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

<span data-ttu-id="ac850-122">Substituir `CLUSTERNAME` com nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac850-122">Replace `CLUSTERNAME` with hello name of your HDInsight cluster.</span></span>

## <a name="authentication"></a><span data-ttu-id="ac850-123">Autenticação</span><span class="sxs-lookup"><span data-stu-id="ac850-123">Authentication</span></span>

<span data-ttu-id="ac850-124">Ao estabelecer conexão hello, você deve usar o hello HDInsight cluster admin nome e senha tooauthenticate toohello cluster gateway.</span><span class="sxs-lookup"><span data-stu-id="ac850-124">When establishing hello connection, you must use hello HDInsight cluster admin name and password tooauthenticate toohello cluster gateway.</span></span> <span data-ttu-id="ac850-125">Durante a conexão de clientes do JDBC, como esquilo SQL, você deve inserir nome de saudação do administrador e a senha nas configurações do cliente.</span><span class="sxs-lookup"><span data-stu-id="ac850-125">When connecting from JDBC clients such as SQuirreL SQL, you must enter hello admin name and password in client settings.</span></span>

<span data-ttu-id="ac850-126">Em um aplicativo Java, você deve usar o hello nome e senha ao estabelecer uma conexão.</span><span class="sxs-lookup"><span data-stu-id="ac850-126">From a Java application, you must use hello name and password when establishing a connection.</span></span> <span data-ttu-id="ac850-127">Por exemplo, hello código Java a seguir abre uma nova conexão usando a cadeia de caracteres de conexão Olá, nome do administrador e senha:</span><span class="sxs-lookup"><span data-stu-id="ac850-127">For example, hello following Java code opens a new connection using hello connection string, admin name, and password:</span></span>

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a><span data-ttu-id="ac850-128">Conectar-se ao cliente do SQuirreL SQL</span><span class="sxs-lookup"><span data-stu-id="ac850-128">Connect with SQuirreL SQL client</span></span>

<span data-ttu-id="ac850-129">Esquilo SQL é um cliente JDBC que pode ser usados tooremotely executar consultas de Hive com seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac850-129">SQuirreL SQL is a JDBC client that can be used tooremotely run Hive queries with your HDInsight cluster.</span></span> <span data-ttu-id="ac850-130">Olá etapas a seguir pressupõem que você já instalou esquilo SQL.</span><span class="sxs-lookup"><span data-stu-id="ac850-130">hello following steps assume that you have already installed SQuirreL SQL.</span></span>

1. <span data-ttu-id="ac850-131">Copie os drivers de JDBC Hive de saudação do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac850-131">Copy hello Hive JDBC drivers from your HDInsight cluster.</span></span>

    * <span data-ttu-id="ac850-132">Para **HDInsight baseados em Linux**, arquivos jar da saudação necessário toodownload as etapas a seguir do uso hello.</span><span class="sxs-lookup"><span data-stu-id="ac850-132">For **Linux-based HDInsight**, use hello following steps toodownload hello required jar files.</span></span>

        1. <span data-ttu-id="ac850-133">Crie um diretório que contém arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac850-133">Create a directory that contains hello files.</span></span> <span data-ttu-id="ac850-134">Por exemplo: `mkdir hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="ac850-134">For example, `mkdir hivedriver`.</span></span>

        2. <span data-ttu-id="ac850-135">Em uma linha de comando, use a seguir Olá comandos toocopy arquivos de saudação do cluster do HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="ac850-135">From a command line, use hello following commands toocopy hello files from hello HDInsight cluster:</span></span>

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            <span data-ttu-id="ac850-136">Substituir `USERNAME` com o nome da conta de usuário Olá SSH para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ac850-136">Replace `USERNAME` with hello SSH user account name for hello cluster.</span></span> <span data-ttu-id="ac850-137">Substituir `CLUSTERNAME` com o nome do cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="ac850-137">Replace `CLUSTERNAME` with hello HDInsight cluster name.</span></span>

    * <span data-ttu-id="ac850-138">Para **HDInsight baseados em Windows**, arquivos jar do toodownload Olá as etapas a seguir de saudação do uso.</span><span class="sxs-lookup"><span data-stu-id="ac850-138">For **Windows-based HDInsight**, use hello following steps toodownload hello jar files.</span></span>

        1. <span data-ttu-id="ac850-139">De Olá portal do Azure, selecione seu cluster HDInsight e selecione Olá **área de trabalho remota** ícone.</span><span class="sxs-lookup"><span data-stu-id="ac850-139">From hello Azure portal, select your HDInsight cluster, and then select hello **Remote Desktop** icon.</span></span>

            ![Ícone da Área de Trabalho Remota](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. <span data-ttu-id="ac850-141">Na folha de área de trabalho remota hello, use Olá **conectar** cluster do botão tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="ac850-141">On hello Remote Desktop blade, use hello **Connect** button tooconnect toohello cluster.</span></span> <span data-ttu-id="ac850-142">Se Olá área de trabalho remota não está habilitado, use Olá formulário tooprovide um nome de usuário e senha e selecione **habilitar** tooenable área de trabalho remota para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac850-142">If hello Remote Desktop is not enabled, use hello form tooprovide a user name and password, then select **Enable** tooenable Remote Desktop for hello cluster.</span></span>

            ![Folha Área de Trabalho Remota](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            <span data-ttu-id="ac850-144">Depois de selecionar **Conectar**, um arquivo .rdp será baixado.</span><span class="sxs-lookup"><span data-stu-id="ac850-144">After selecting **Connect**, a .rdp file is downloaded.</span></span> <span data-ttu-id="ac850-145">Use esse cliente de área de trabalho remota do arquivo toolaunch hello.</span><span class="sxs-lookup"><span data-stu-id="ac850-145">Use this file toolaunch hello Remote Desktop client.</span></span> <span data-ttu-id="ac850-146">Quando solicitado, use o nome de usuário de saudação e senha que você digitou para o acesso de área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="ac850-146">When prompted, use hello user name and password you entered for Remote Desktop access.</span></span>

        3. <span data-ttu-id="ac850-147">Uma vez conectado, copie Olá seguintes arquivos da máquina local de tooyour Olá de sessão área de trabalho remota.</span><span class="sxs-lookup"><span data-stu-id="ac850-147">Once connected, copy hello following files from hello Remote Desktop session tooyour local machine.</span></span> <span data-ttu-id="ac850-148">Coloque-os em um diretório local chamado `hivedriver`.</span><span class="sxs-lookup"><span data-stu-id="ac850-148">Put them in a local directory named `hivedriver`.</span></span>

            * <span data-ttu-id="ac850-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span><span class="sxs-lookup"><span data-stu-id="ac850-149">C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar</span></span>
            * <span data-ttu-id="ac850-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="ac850-150">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar</span></span>
            * <span data-ttu-id="ac850-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span><span class="sxs-lookup"><span data-stu-id="ac850-151">C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar</span></span>

            > [!NOTE]
            > <span data-ttu-id="ac850-152">versão de Hello números incluídos nos nomes de arquivo e caminhos de saudação podem ser diferentes para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="ac850-152">hello version numbers included in hello paths and file names may be different for your cluster.</span></span>

        4. <span data-ttu-id="ac850-153">Desconecte a sessão de área de trabalho remota Olá depois de terminar de copiar arquivos de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac850-153">Disconnect hello Remote Desktop session once you have finished copying hello files.</span></span>

2. <span data-ttu-id="ac850-154">Inicie aplicativo do SQL esquilo hello.</span><span class="sxs-lookup"><span data-stu-id="ac850-154">Start hello SQuirreL SQL application.</span></span> <span data-ttu-id="ac850-155">Da esquerda de saudação da janela hello, selecione **Drivers**.</span><span class="sxs-lookup"><span data-stu-id="ac850-155">From hello left of hello window, select **Drivers**.</span></span>

    ![Guia drivers saudação à esquerda da janela de saudação](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. <span data-ttu-id="ac850-157">Dos demais ícones na parte superior de saudação do Olá Olá **Drivers** caixa de diálogo, selecione Olá  **+**  toocreate ícone um driver.</span><span class="sxs-lookup"><span data-stu-id="ac850-157">From hello icons at hello top of hello **Drivers** dialog, select hello **+** icon toocreate a driver.</span></span>

    ![Ícones de Drivers](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. <span data-ttu-id="ac850-159">Na caixa de diálogo de Adicionar Driver hello, adicione Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="ac850-159">In hello Add Driver dialog, add hello following information:</span></span>

    * <span data-ttu-id="ac850-160">**Nome**: Hive</span><span class="sxs-lookup"><span data-stu-id="ac850-160">**Name**: Hive</span></span>
    * <span data-ttu-id="ac850-161">**Exemplo de URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span><span class="sxs-lookup"><span data-stu-id="ac850-161">**Example URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`</span></span>
    * <span data-ttu-id="ac850-162">**Caminho de classe extra**: usar Olá adicionar botão tooadd Olá jar arquivos baixados anteriormente</span><span class="sxs-lookup"><span data-stu-id="ac850-162">**Extra Class Path**: Use hello Add button tooadd hello jar files downloaded earlier</span></span>
    * <span data-ttu-id="ac850-163">**Nome de Classe**: org.apache.hive.jdbc.HiveDriver</span><span class="sxs-lookup"><span data-stu-id="ac850-163">**Class Name**: org.apache.hive.jdbc.HiveDriver</span></span>

   ![diálogo adicionar driver](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   <span data-ttu-id="ac850-165">Clique em **Okey** toosave essas configurações.</span><span class="sxs-lookup"><span data-stu-id="ac850-165">Click **OK** toosave these settings.</span></span>

5. <span data-ttu-id="ac850-166">Esquerda de saudação da janela de SQL esquilo hello, selecione **Aliases**.</span><span class="sxs-lookup"><span data-stu-id="ac850-166">On hello left of hello SQuirreL SQL window, select **Aliases**.</span></span> <span data-ttu-id="ac850-167">Em seguida, clique em Olá  **+**  toocreate ícone um alias de conexão.</span><span class="sxs-lookup"><span data-stu-id="ac850-167">Then click hello **+** icon toocreate a connection alias.</span></span>

    ![adicionar novo alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. <span data-ttu-id="ac850-169">A seguir Olá Use valores de saudação **adicionar Alias** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ac850-169">Use hello following values for hello **Add Alias** dialog.</span></span>

    * <span data-ttu-id="ac850-170">**Nome**: Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ac850-170">**Name**: Hive on HDInsight</span></span>

    * <span data-ttu-id="ac850-171">**Driver**: Use Olá suspensa tooselect Olá **Hive** driver</span><span class="sxs-lookup"><span data-stu-id="ac850-171">**Driver**: Use hello dropdown tooselect hello **Hive** driver</span></span>

    * <span data-ttu-id="ac850-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span><span class="sxs-lookup"><span data-stu-id="ac850-172">**URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2</span></span>

        <span data-ttu-id="ac850-173">Substituir **CLUSTERNAME** com nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac850-173">Replace **CLUSTERNAME** with hello name of your HDInsight cluster.</span></span>

    * <span data-ttu-id="ac850-174">**Nome de usuário**: nome da conta de logon Olá cluster para seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac850-174">**User Name**: hello cluster login account name for your HDInsight cluster.</span></span> <span data-ttu-id="ac850-175">saudação padrão é `admin`.</span><span class="sxs-lookup"><span data-stu-id="ac850-175">hello default is `admin`.</span></span>

    * <span data-ttu-id="ac850-176">**Senha**: senha Olá Olá cluster conta de logon.</span><span class="sxs-lookup"><span data-stu-id="ac850-176">**Password**: hello password for hello cluster login account.</span></span>

 ![diálogo adicionar alias](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    <span data-ttu-id="ac850-178">Saudação de uso **teste** tooverify botão que Olá conexão funciona.</span><span class="sxs-lookup"><span data-stu-id="ac850-178">Use hello **Test** button tooverify that hello connection works.</span></span> <span data-ttu-id="ac850-179">Quando **conectem: Hive no HDInsight** caixa de diálogo é exibida, selecione **conectar** tooperform teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac850-179">When **Connect to: Hive on HDInsight** dialog appears, select **Connect** tooperform hello test.</span></span> <span data-ttu-id="ac850-180">Se o teste de saudação for bem-sucedida, você verá um **Conexão bem-sucedida** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ac850-180">If hello test succeeds, you see a **Connection successful** dialog.</span></span>

    <span data-ttu-id="ac850-181">conexão de saudação toosave alias, use Olá **Okey** botão na parte inferior de saudação do hello **adicionar Alias** caixa de diálogo.</span><span class="sxs-lookup"><span data-stu-id="ac850-181">toosave hello connection alias, use hello **Ok** button at hello bottom of hello **Add Alias** dialog.</span></span>

7. <span data-ttu-id="ac850-182">De saudação **se conectem** selecione da lista suspensa na parte superior de saudação do SQL esquilo, **Hive no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="ac850-182">From hello **Connect to** dropdown at hello top of SQuirreL SQL, select **Hive on HDInsight**.</span></span> <span data-ttu-id="ac850-183">Quando solicitado, selecione **Conectar**.</span><span class="sxs-lookup"><span data-stu-id="ac850-183">When prompted, select **Connect**.</span></span>

    ![diálogo conexão](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. <span data-ttu-id="ac850-185">Uma vez conectado, digite Olá seguinte consulta na caixa de diálogo de consulta SQL hello e selecione Olá **executar** ícone.</span><span class="sxs-lookup"><span data-stu-id="ac850-185">Once connected, enter hello following query into hello SQL query dialog, and then select hello **Run** icon.</span></span> <span data-ttu-id="ac850-186">Olá resultados área deve mostrar resultados de saudação de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="ac850-186">hello results area should show hello results of hello query.</span></span>

        select * from hivesampletable limit 10;

    ![diálogo consulta sql, incluindo os resultados](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a><span data-ttu-id="ac850-188">Conectar-se de um aplicativo Java de exemplo</span><span class="sxs-lookup"><span data-stu-id="ac850-188">Connect from an example Java application</span></span>

<span data-ttu-id="ac850-189">Um exemplo de como usar um cliente de Java tooquery Hive no HDInsight está disponível em [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span><span class="sxs-lookup"><span data-stu-id="ac850-189">An example of using a Java client tooquery Hive on HDInsight is available at [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc).</span></span> <span data-ttu-id="ac850-190">Siga as instruções de Olá Olá repositório toobuild e executar o exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="ac850-190">Follow hello instructions in hello repository toobuild and run hello sample.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="ac850-191">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="ac850-191">Troubleshooting</span></span>

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a><span data-ttu-id="ac850-192">Erro inesperado ocorreu tooopen tentando uma conexão de SQL</span><span class="sxs-lookup"><span data-stu-id="ac850-192">Unexpected Error occurred attempting tooopen an SQL connection</span></span>

<span data-ttu-id="ac850-193">**Sintomas**: ao conectar o cluster HDInsight tooan versão 3.3 ou 3.4, você poderá receber um erro que ocorreu um erro inesperado.</span><span class="sxs-lookup"><span data-stu-id="ac850-193">**Symptoms**: When connecting tooan HDInsight cluster that is version 3.3 or 3.4, you may receive an error that an unexpected error occurred.</span></span> <span data-ttu-id="ac850-194">rastreamento de pilha Olá para esse erro começa com hello linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="ac850-194">hello stack trace for this error begins with hello following lines:</span></span>

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

<span data-ttu-id="ac850-195">**Causa**: este erro é causado por uma incompatibilidade de versão de saudação do hello commons codec.jar arquivo usado pelo esquilo e hello exigido pelos componentes do Hive JDBC hello.</span><span class="sxs-lookup"><span data-stu-id="ac850-195">**Cause**: This error is caused by a mismatch in hello version of hello commons-codec.jar file used by SQuirreL and hello one required by hello Hive JDBC components.</span></span>

<span data-ttu-id="ac850-196">**Resolução**: toofix esse erro, use Olá seguindo as etapas:</span><span class="sxs-lookup"><span data-stu-id="ac850-196">**Resolution**: toofix this error, use hello following steps:</span></span>

1. <span data-ttu-id="ac850-197">Baixe o arquivo de jar de codec commons de saudação do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac850-197">Download hello commons-codec jar file from your HDInsight cluster.</span></span>

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. <span data-ttu-id="ac850-198">Sair esquilo e, em seguida, vá toohello diretório onde esquilo está instalado no seu sistema.</span><span class="sxs-lookup"><span data-stu-id="ac850-198">Exit SQuirreL, and then go toohello directory where SQuirreL is installed on your system.</span></span> <span data-ttu-id="ac850-199">No diretório de esquilo hello, sob Olá `lib` diretório, substituir Olá existente commons-codec.jar com hello um baixado do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="ac850-199">In hello SquirreL directory, under hello `lib` directory, replace hello existing commons-codec.jar with hello one downloaded from hello HDInsight cluster.</span></span>

3. <span data-ttu-id="ac850-200">Reinicie o SQuirreL.</span><span class="sxs-lookup"><span data-stu-id="ac850-200">Restart SQuirreL.</span></span> <span data-ttu-id="ac850-201">Erro de saudação não deve ocorrer durante a conexão tooHive no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ac850-201">hello error should no longer occur when connecting tooHive on HDInsight.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac850-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac850-202">Next steps</span></span>

<span data-ttu-id="ac850-203">Agora que você aprendeu como toouse JDBC toowork com Hive, Olá uso a seguir vincula tooexplore toowork outras formas ao HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac850-203">Now that you have learned how toouse JDBC toowork with Hive, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* [<span data-ttu-id="ac850-204">Carregar dados tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="ac850-204">Upload data tooHDInsight</span></span>](hdinsight-upload-data.md)
* [<span data-ttu-id="ac850-205">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="ac850-205">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ac850-206">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="ac850-206">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ac850-207">Usar trabalhos do MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="ac850-207">Use MapReduce jobs with HDInsight</span></span>](hdinsight-use-mapreduce.md)
