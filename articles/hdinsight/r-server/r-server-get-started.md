---
title: "Introdução ao R Server no HDInsight - Azure| Microsoft Docs"
description: Saiba como criar um Apache Spark no cluster HDInsight que inclui o R Server e enviar um script R no cluster.
services: HDInsight
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b5e111f3-c029-436c-ba22-c54a4a3016e3
ms.service: HDInsight
ms.custom: hdinsightactive
ms.devlang: R
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/14/2017
ms.author: bradsev
ms.openlocfilehash: e688068efb41cdccbeb23de3c8ad7a09021e5b3f
ms.sourcegitcommit: f1c1789f2f2502d683afaf5a2f46cc548c0dea50
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/18/2018
---
# <a name="get-started-with-r-server-on-hdinsight"></a>Introdução ao R Server no HDInsight

O Azure HDInsight inclui uma opção de R Server a ser integrada ao seu cluster HDInsight. Essa opção permite que scripts R usem o Spark e MapReduce para executar cálculos distribuídos. Neste artigo, você aprenderá como criar um Servidor R no cluster do HDInsight. Depois você aprende como executar um script R que demonstra o uso do Spark para cálculos de R distribuídos.


## <a name="prerequisites"></a>pré-requisitos

* **Uma assinatura do Azure**: antes de começar este tutorial, você deve ter uma assinatura do Azure. Para obter mais informações, consulte [Obter uma avaliação gratuita do Microsoft Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* **Um cliente Secure Shell (SSH)**: um cliente SSH é usado para se conectar ao cluster HDInsight remotamente e executar comandos diretamente no cluster. Para obter mais informações, confira [Usar SSH com HDInsight](../hdinsight-hadoop-linux-use-ssh-unix.md).
* **Chaves SSH (opcional)**: você pode proteger a conta SSH usada para se conectar ao cluster usando uma senha ou uma chave pública. Usar uma senha é mais fácil e permite que você comece sem precisar criar um par de chaves pública/privada. No entanto, usar uma chave é mais seguro.

  > [!NOTE]
  > As etapas neste artigo pressupõem que você esteja usando uma senha.


## <a name="automate-cluster-creation"></a>Automatizar a criação de cluster

Você pode automatizar a criação de R Servers para HDInsight usando modelos do Azure Resource Manager, do SDK e do PowerShell.

* Para criar uma instância do R Server usando um modelo do Azure Resource Manager, consulte [Implantar cluster HDInsight do R Server](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).
* Para criar uma instância do R Server usando o SDK do .NET, consulte [Criar clusters baseados em Linux no HDInsight usando o SDK do .NET](../hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md).
* Para implantar o R Server usando o PowerShell, consulte [Criar clusters baseados em Linux no HDInsight usando o Azure PowerShell](../hdinsight-hadoop-create-linux-clusters-azure-powershell.md).


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-a-cluster-by-using-the-azure-portal"></a>Criar um cluster usando o portal do Azure

1. Entre no [Portal do Azure](https://portal.azure.com).

2. Selecione **Novo** > **Intelligence + análises** > **HDInsight**.

    ![Imagem da criação de um novo cluster](./media/r-server-get-started/newcluster.png)

3. Na experiência **Criação rápida**, insira um nome para o cluster na caixa **Nome do cluster**. Se você tiver várias assinaturas do Azure, use a caixa **Assinatura** para selecionar aquela que deseja usar.

    ![Nome do cluster e seleções de assinatura](./media/r-server-get-started/clustername.png)

4. Selecione **Tipo de cluster** para abrir o painel **Configuração de cluster**. No painel **Configuração de cluster**, selecione as seguintes opções:

    * **Tipo de Cluster**: selecione **R Server**.
    * **Versão**: selecione a versão do R Server a ser instalada no cluster. A versão disponível no momento é **R Server 9.1 (HDI 3.6)**. As notas de versão para as versões disponíveis do R Server podem ser encontradas no [MSDN](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).
    * **Edição de comunidade R Studio para R Server**: esse IDE baseado em navegador é instalado por padrão no nó de borda. Se você preferir não instalá-lo, limpe a caixa de seleção. Caso opte por instalá-lo, a URL para acessar o logon do Servidor do RStudio estará em um painel de aplicativo do portal para o cluster depois de ele ter sido criado.
    * Deixe as outras opções com os valores padrão e use o botão **Selecionar** para salvar o tipo de cluster.

        ![Captura de tela do painel “Tipo do cluster”](./media/r-server-get-started/clustertypeconfig.png)

5. No painel **Básico**, nas caixas **Nome de usuário de logon de cluster** e **Senha de logon no cluster**, insira um nome de usuário e uma senha (respectivamente) para o cluster.

6. Na caixa **Nome de usuário do Secure Shell (SSH)**, especifique o nome de usuário SSH. O SSH é usado para se conectar remotamente ao cluster usando um cliente SSH. Você pode especificar o usuário SSH nesta caixa ou depois que o cluster for criado (na guia **Configuração** do cluster).
   
   > [!NOTE] 
   > O R Server está configurado para esperar um nome de usuário SSH de “remoteuser”. Se você usar um nome de usuário diferente, precisará executar uma etapa adicional após a criação do cluster.

7. Deixe a caixa de seleção **Usar a mesma senha como logon do cluster** marcada para usar a **SENHA** como o tipo de autenticação, a menos que você prefira o uso de uma chave pública. Você precisa de um par de chaves pública/privada para acessar o R Server no cluster por meio de um cliente remoto, como Ferramentas do R para Visual Studio, RStudio ou Desktop IDE. Se você instalar o RStudio Server Community Edition, precisará escolher uma senha SSH.     

   Para criar e usar um par de chaves pública/privada, limpe **Usar a mesma senha como logon do cluster**. Depois, selecione **CHAVE PÚBLICA** e faça o seguinte. Estas instruções pressupõem que você tenha o Cygwin com ssh-keygen ou equivalente instalado.

   a. Gere um par de chaves pública/privada do prompt de comando em seu laptop:

        ssh-keygen -t rsa -b 2048

   b. Siga os prompts para nomear um arquivo de chave e, em seguida, insira uma frase secreta para maior segurança. A tela deve ter uma aparência semelhante à seguinte imagem:

      ![Linha de comando SSH no Windows](./media/r-server-get-started/sshcmdline.png)

      Esse comando cria um arquivo de chave privada e um arquivo de chave pública com o nome <private-key-filename>.pub. Neste exemplo, os arquivos são furiosa e furiosa.pub:

      ![Resultado de exemplo do comando dir](./media/r-server-get-started/dir.png)

   c. Especifique o arquivo de chave pública (&#42;.pub) ao atribuir credenciais de cluster do HDI. Confirme seu grupo de recursos e sua região e selecione **Próximo**.

      ![Painel Credenciais](./media/r-server-get-started/publickeyfile.png)  

   d. Altere permissões no arquivo de chave privada em seu laptop:

        chmod 600 <private-key-filename>

   e. Usar o arquivo de chave privada com o SSH para logon remoto:

        ssh –i <private-key-filename> remoteuser@<hostname public ip>

      Ou use o arquivo de chave privada como parte da definição de seu contexto de computação Spark do Hadoop para o R Server no cliente. Para mais informações, consulte [Criar um Contexto de Computação para Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started).

8. A criação rápida faz sua transição para o painel **Armazenamento**. Lá, você seleciona as configurações de conta de armazenamento a serem usadas para a localização primária do sistema de arquivos HDFS usado pelo cluster. Selecione uma conta nova ou existente do armazenamento do Azure ou uma conta existente de armazenamento do Azure Data Lake Store.

    - Caso selecione uma conta de armazenamento do Azure, é possível escolher uma conta existente selecionando a opção **Selecionar conta de armazenamento** e depois a conta desejada. Crie uma nova conta usando o link **Criar nova** na seção **Selecionar uma conta de armazenamento**.

      > [!NOTE]
      > Se escolher **Novo**, você deverá digitar um nome para a nova conta de armazenamento. Uma marca de seleção verde é exibida se o nome é aceito.

      O **Contêiner padrão** usa o nome do cluster como padrão. Deixe o padrão como o valor.

      Caso tenha selecionado uma nova conta de armazenamento, use **Local** no prompt para selecionar uma região para ele.  

         ![Painel da fonte de dados](./media/r-server-get-started/datastore.png)  

      > [!IMPORTANT]
      > Selecionar o local para a fonte de dados padrão também define o local do cluster HDInsight. O cluster e a fonte de dados padrão devem estar na mesma região.

    - Caso queira usar uma conta existente do Data Lake Store, selecione a conta a ser usada. Depois, adicione a identidade *ADD* do cluster ao seu cluster para permitir o acesso ao armazenamento. Para obter mais informações sobre esse processo, consulte [Criar clusters HDInsight com o Data Lake Store usando o portal do Azure](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).

    Use o botão **Selecionar** para salvar a configuração da fonte de dados.


9. O painel **Resumo** é então exibido para que você possa validar todas as suas configurações. Aqui você pode alterar o tamanho do seu cluster para modificar o número de servidores nele. Também é possível especificar as ações de script que você deseja executar. A menos que você saiba que precisa de um cluster maior, deixe o número de nós de trabalho como o padrão de **4**. O painel também mostra o custo estimado do cluster.

    ![Resumo do cluster](./media/r-server-get-started/clustersummary.png)

   > [!NOTE]
   > Se necessário, redimensione o cluster posteriormente por meio do portal (**Cluster** > **Configurações** > **Dimensionar cluster**) para aumentar ou diminuir o número de nós de trabalho. Esse dimensionamento pode ser útil para deixar o cluster ocioso quando não estiver em uso ou para adicionar capacidade para atender às necessidades das tarefas maiores.
   >
   >

   Entre os fatores para se ter em mente ao dimensionar o cluster, os nós de dados e o nó de borda, estão:  

   * O desempenho da análise do Servidor R distribuída no Spark é proporcional ao número de nós de trabalho quando os dados são grandes.  

   * O desempenho da análise do Servidor R é linear ao tamanho dos dados que estão sendo analisados. Por exemplo:   

     * Para os tamanhos de dados pequenos e médios, o desempenho é melhor quando os dados são analisados em um contexto de computação local no nó de borda. Para saber mais sobre os cenários nos quais os contextos de computação local e Spark funcionam melhor, consulte [Opções de contexto de computação para R Server no HDInsight](r-server-compute-contexts.md).<br>
     * Se você entrar no nó de borda e executar o seu script R, todas as funções diferentes de rx ScaleR serão executadas *localmente* no nó de borda. Portanto, a memória e o número de núcleos no nó de borda devem ser dimensionados de acordo. O mesmo se aplica se você usar o Servidor R no HDI como contexto de computação remota do seu laptop.

   Use o botão **Selecionar** para salvar a configuração de preços do nó.

   ![Painel para tipos de preço do nó](./media/r-server-get-started/pricingtier.png)

   Também há um link para **Baixar modelo e parâmetros**. Selecione esse link para exibir scripts que podem ser usados para automatizar a criação de um cluster com a configuração selecionada. Esses scripts também estão disponíveis na entrada do portal do Azure para seu cluster depois de criados.

   > [!NOTE]
   > Levará algum tempo para que o cluster seja criado, geralmente, cerca de 20 minutos. Para verificar o processo de criação, use o bloco no Quadro inicial ou a entrada **Notificações** à esquerda da página.
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-to-rstudio-server"></a>Conectar-se ao RStudio Server

Caso tenha optado por incluir o RStudio Server Community Edition em sua instalação, você poderá acessar o logon do RStudio por dois métodos diferentes:

- Vá para a URL a seguir (em que *CLUSTERNAME* é o nome do cluster que você criou):

    https://*CLUSTERNAME*.azurehdinsight.net/rstudio/

- Abra a entrada para o cluster no portal do Azure, selecione o link rápido para os **Painéis do R Server** e selecione o **Painel do RStudio**:

  ![Acessar o painel do RStudio](./media/r-server-get-started/rstudiodashboard1.png)

  ![Acessar o painel do RStudio](./media/r-server-get-started/rstudiodashboard2.png)

> [!IMPORTANT]
> Não importa o método usado: na primeira vez que fizer logon, você precisará autenticar duas vezes. Na primeira autenticação, forneça a ID de usuário e a senha de administrador do cluster. Na segunda autenticação, forneça a ID de usuário e a senha do SSH. Os logons subsequentes exigirão apenas a ID de usuário e senha do SSH.

<a name="connect-to-edge-node"></a>
## <a name="connect-to-the-r-server-edge-node"></a>Conecte-se ao nó de borda do Servidor R

Conecte-se ao nó de borda do R Server do cluster HDInsight usando o SSH pelo comando:

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> Você pode encontrar o endereço `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` no portal do Azure. Selecione o cluster e depois **Todas as configurações** > **Aplicativos** > **RServer**. Isso exibe as informações do ponto de extremidade do SSH para o nó de borda.
>
> ![Imagem do ponto de extremidade do SSH para o nó de borda](./media/r-server-get-started/sshendpoint.png)
>
>

Caso tenha usado uma senha para ajudar a proteger sua conta de usuário do SSH, ela será solicitada. Caso tenha usado uma chave pública, talvez precise usar o parâmetro `-i` para especificar a chave privada correspondente. Por exemplo: 

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Para obter mais informações, consulte [Conectar ao HDInsight (Hadoop) usando SSH](../hdinsight-hadoop-linux-use-ssh-unix.md).

Depois de ficar conectado, você chegará em um prompt semelhante ao seguinte:

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a>Habilitar múltiplos usuário simultâneos

Você pode habilitar vários usuários simultâneos adicionando mais usuários ao nó de borda em que a versão da comunidade RStudio é executada.

Ao criar um cluster HDInsight, você deve fornecer dois usuários: um usuário HTTP e um usuário SSH.

![Inserir as credenciais de usuário do cluster e do usuário do SSH](./media/r-server-get-started/concurrent-users-1.png)

- **Nome de usuário de logon de cluster**: um usuário HTTP para autenticação por meio do gateway do HDInsight que é usado para proteger os clusters HDInsight criados por você. Esse usuário HTTP é usado para acessar a IU do Ambari, a IU do YARN e outros componentes de interface do usuário.
- **Nome de usuário SSH (Secure Shell)**: um usuário do SSH para acessar o cluster por meio do Secure Shell. Esse é um usuário no sistema Linux para todos os nós de cabeçalho, nós de trabalho e nós de borda. Portanto, você pode usar o SSH para acessar qualquer nó em um cluster remoto.

A versão do RStudio Server Community usada no Microsoft R Server no cluster do tipo HDInsight aceita apenas o nome de usuário e a senha do Linux como mecanismo de logon. Ele não dá suporte a tokens de passagem. Assim, se você criou um novo cluster e deseja usar o RStudio para acessá-lo, precisa fazer logon duas vezes.

1. Faça logon usando as credenciais de usuário HTTP por meio do gateway do HDInsight: 

    ![Inserir credenciais de usuário HTTP](./media/r-server-get-started/concurrent-users-2a.png)

2. Use as credenciais de usuário do SSH para entrar no RStudio:
  
    ![Inserir as credenciais de usuário SSH](./media/r-server-get-started/concurrent-users-2b.png)

Atualmente, é possível criar apenas uma conta de usuário SSH ao provisionar um cluster HDInsight. Para permitir que vários usuários acessem o Microsoft R Server em clusters HDInsight, você precisa criar usuários adicionais no sistema Linux.

Como a versão do RStudio Server Community está em execução no nó de borda do cluster, há três etapas a seguir:

1. Use o usuário SSH criado para fazer logon no nó de borda.
2. Adicione mais usuários do Linux ao nó de borda.
3. Use a versão do RStudio Community com o usuário criado.

### <a name="use-the-created-ssh-user-to-log-in-to-the-edge-node"></a>Use o usuário SSH criado para fazer logon no nó de borda

Baixe uma ferramenta SSH (como o PuTTY) e use o usuário SSH existente para fazer logon. Em seguida, siga as instruções fornecidas em [Conectar-se ao HDInsight (Hadoop) usando o SSH](../hdinsight-hadoop-linux-use-ssh-unix.md) para acessar o nó de borda. O endereço do nó de borda para o R Server no cluster HDInsight é: **clustername-ed-ssh.azurehdinsight.net**


### <a name="add-more-linux-users-to-the-edge-node"></a>Adicione mais usuários do Linux ao nó de borda

Para adicionar um usuário ao nó de borda, execute estes comandos:

    sudo useradd yournewusername -m
    sudo passwd yourusername

Você verá os seguintes itens retornados: 

![Saída dos comandos sudo](./media/r-server-get-started/concurrent-users-3.png)

Quando for solicitado a fornecer a senha atual do Kerberos, basta selecionar a tecla Enter para ignorá-lo. A opção `-m` no comando `useradd` indica que o sistema criará uma pasta base para o usuário. Essa pasta é necessária para a versão do RStudio Community.


### <a name="use-the-rstudio-community-version-with-the-created-user"></a>Use a versão do RStudio Community com o usuário criado

Use o usuário criado para entrar no RStudio:

![Página de entrada do RStudio](./media/r-server-get-started/concurrent-users-4.png)

Observe que RStudio indica que você está usando o novo usuário (aqui, por exemplo, **sshuser6**) para fazer logon no cluster: 

![Local do novo usuário na barra de comandos do RStudio](./media/r-server-get-started/concurrent-users-5.png)

Você também pode fazer logon usando as credenciais originais (por padrão, **sshuser**) simultaneamente em outra janela do navegador.

Você pode enviar um trabalho usando funções ScaleR. Aqui está um exemplo dos comandos para executar um trabalho:

    # Set the HDFS (Azure Blob storage) location of example data
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storing data temporarily
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data to the tmp folder
    remoteDir <- "https://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
    download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
    download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
    download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
    download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
    download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
    download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
    download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
    download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
    download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
    download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
    download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
    download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

    # Set the directory in bigDataDirRoot to load the data
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create the directory
    rxHadoopMakeDir(inputDir)

    # Copy the data from source to input
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define the HDFS (Blob storage) file system
    hdfsFS <- RxHdfsFileSystem()

    # Create an info list for the airline data
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all the column names
    varNames <- names(airlineColInfo)

    # Define the text data source in HDFS
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define the text data source in the local system
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify the formula to use
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define the Spark compute context
    mySparkCluster <- RxSpark()

    # Set the compute context
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary
    summary(modelSpark)


Observe que os trabalhos enviados estão com nomes de usuário diferentes na interface do usuário do YARN:

![Lista de usuários na interface do usuário do YARN](./media/r-server-get-started/concurrent-users-6.png)

Observe também que os usuários adicionados recentemente não têm privilégios de raiz no sistema Linux. Mas eles têm o mesmo acesso a todos os arquivos no sistema de arquivos remoto do HDFS e no armazenamento de Blob.


<a name="use-r-console"></a>
## <a name="use-the-r-console"></a>Use o console R

1. Na sessão de SSH, use o seguinte comando para iniciar o console R:  

        R

2. Você deverá ver uma saída semelhante ao seguinte:
    
        R version 3.2.2 (2015-08-14) -- "Fire Safety"
        Copyright (C) 2015 The R Foundation for Statistical Computing
        Platform: x86_64-pc-linux-gnu (64-bit)

        R is free software and comes with ABSOLUTELY NO WARRANTY.
        You are welcome to redistribute it under certain conditions.
        Type 'license()' or 'licence()' for distribution details.

        Natural language support but running in an English locale

        R is a collaborative project with many contributors.
        Type 'contributors()' for more information and
        'citation()' on how to cite R or R packages in publications.

        Type 'demo()' for some demos, 'help()' for on-line help, or
        'help.start()' for an HTML browser interface to help.
        Type 'q()' to quit R.

        Microsoft R Server version 8.0: an enhanced distribution of R
        Microsoft packages Copyright (C) 2016 Microsoft Corporation

        Type 'readme()' for release notes.
        >

3. No prompt `>` , você pode inserir o código R. O R Server inclui pacotes que você pode usar para interagir com o Hadoop e executar cálculos distribuídos com facilidade. Por exemplo, use o seguinte comando para exibir a raiz do sistema de arquivos padrão para o cluster HDInsight:

        rxHadoopListFiles("/")

4. Você também pode usar o estilo do armazenamento de Blob de endereçar:

        rxHadoopListFiles("wasb:///")


## <a name="use-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a>Use o R Server no HDI a partir de uma instância remota do Microsoft R Server ou Microsoft R Client

É possível configurar o acesso ao contexto de computação Spark HDI Hadoop a partir de uma instância remota do Microsoft R Server ou do Microsoft R Client em execução em um computador ou laptop. Para obter mais informações, consulte a seção “Usando o Microsoft R Server como um cliente Hadoop” em [Criando um contexto de computação para o Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md). Para isso, especifique as seguintes opções ao definir o contexto de computação RxSpark em seu laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches e sshProfileScript. Aqui está um exemplo:


    myNameNode <- "default"
    myPort <- 0

    mySshHostname  <- 'rkrrehdi1-ed-ssh.azurehdinsight.net'  # HDI secure shell hostname
    mySshUsername  <- 'remoteuser'# HDI SSH username
    mySshSwitches  <- '-i /cygdrive/c/Data/R/davec'   # HDI SSH private key

    myhdfsShareDir <- paste("/user/RevoShare", mySshUsername, sep="/")
    myShareDir <- paste("/var/RevoShare" , mySshUsername, sep="/")

    mySparkCluster <- RxSpark(
      hdfsShareDir = myhdfsShareDir,
      shareDir     = myShareDir,
      sshUsername  = mySshUsername,
      sshHostname  = mySshHostname,
      sshSwitches  = mySshSwitches,
      sshProfileScript = '/etc/profile',
      nameNode     = myNameNode,
      port         = myPort,
      consoleOutput= TRUE
    )


## <a name="use-a-compute-context"></a>Use um contexto de computação

É possível usar um contexto de computação para controlar se o cálculo é executado localmente no nó de borda ou distribuído entre os nós no cluster HDInsight.

1. No Servidor do RStudio ou no console R (em uma seção do SSH), use o seguinte código para carregar dados de exemplo no armazenamento padrão do HDInsight:

        # Set the HDFS (Blob storage) location of example data
        bigDataDirRoot <- "/example/data"

        # Create a local folder for storing data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data to the tmp folder
        remoteDir <- "https://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
        download.file(file.path(remoteDir, "airOT201201.csv"), file.path(source, "airOT201201.csv"))
        download.file(file.path(remoteDir, "airOT201202.csv"), file.path(source, "airOT201202.csv"))
        download.file(file.path(remoteDir, "airOT201203.csv"), file.path(source, "airOT201203.csv"))
        download.file(file.path(remoteDir, "airOT201204.csv"), file.path(source, "airOT201204.csv"))
        download.file(file.path(remoteDir, "airOT201205.csv"), file.path(source, "airOT201205.csv"))
        download.file(file.path(remoteDir, "airOT201206.csv"), file.path(source, "airOT201206.csv"))
        download.file(file.path(remoteDir, "airOT201207.csv"), file.path(source, "airOT201207.csv"))
        download.file(file.path(remoteDir, "airOT201208.csv"), file.path(source, "airOT201208.csv"))
        download.file(file.path(remoteDir, "airOT201209.csv"), file.path(source, "airOT201209.csv"))
        download.file(file.path(remoteDir, "airOT201210.csv"), file.path(source, "airOT201210.csv"))
        download.file(file.path(remoteDir, "airOT201211.csv"), file.path(source, "airOT201211.csv"))
        download.file(file.path(remoteDir, "airOT201212.csv"), file.path(source, "airOT201212.csv"))

        # Set the directory in bigDataDirRoot to load the data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make the directory
        rxHadoopMakeDir(inputDir)

        # Copy the data from source to input
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. Crie algumas informações de dados e defina duas fontes de dados para que você possa trabalhar com os dados:

        # Define the HDFS (Blob storage) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create an info list for the airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # Get all the column names
        varNames <- names(airlineColInfo)

        # Define the text data source in HDFS
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define the text data source in the local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # Formula to use
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. Execute uma regressão logística sobre os dados usando o contexto de computação local:

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    Você deve ver a saída que termina com linhas semelhantes à seguinte:

        Data: airOnTimeDataLocal (RxTextData Data Source)
        File name: /tmp/AirOnTimeCSV2012
        Dependent variable(s): ARR_DEL15
        Total independent variables: 634 (Including number dropped: 3)
        Number of valid observations: 6005381
        Number of missing observations: 91381
        -2*LogLikelihood: 5143814.1504 (Residual deviance on 6004750 degrees of freedom)

        Coefficients:
                         Estimate Std. Error z value Pr(>|z|)
         (Intercept)   -3.370e+00  1.051e+00  -3.208  0.00134 **
         ORIGIN=JFK     4.549e-01  7.915e-01   0.575  0.56548
         ORIGIN=LAX     5.265e-01  7.915e-01   0.665  0.50590
         ......
         DEST=SHD       5.975e-01  9.371e-01   0.638  0.52377
         DEST=TTN       4.563e-01  9.520e-01   0.479  0.63172
         DEST=LAR      -1.270e+00  7.575e-01  -1.676  0.09364 .
         DEST=BPT         Dropped    Dropped Dropped  Dropped

         ---

         Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1

         Condition number of final variance-covariance matrix: 11904202
         Number of iterations: 7

4. Execute a mesma regressão logística usando o contexto do Spark. O contexto do Spark distribui o processamento em todos os nós de trabalho no cluster HDInsight.

        # Define the Spark compute context
        mySparkCluster <- RxSpark()

        # Set the compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > Você também pode usar o MapReduce para distribuir a computação nos nós do cluster. Para saber mais sobre o contexto de computação, confira [Opções de contexto de computação para o Servidor R no HDInsight](r-server-compute-contexts.md).


## <a name="distribute-r-code-to-multiple-nodes"></a>Distribua o código R em vários nós

Com o R Server, você pode facilmente usar o código R existente e executá-lo em vários nós no cluster usando o `rxExec`. Essa função é útil ao fazer uma limpeza de parâmetro ou simulações. O código abaixo é um exemplo de como usar o `rxExec`:

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

Se você ainda estiver usando o contexto do Spark ou do MapReduce, esse comando retornará o valor `nodename` para os nós de trabalho nos quais o código `(Sys.info()["nodename"])` é executado. Por exemplo, em um cluster de quatro nós, você deve receber uma saída semelhante à seguinte:

    $rxElem1
        nodename
    "wn3-myrser"

    $rxElem2
        nodename
    "wn0-myrser"

    $rxElem3
        nodename
    "wn3-myrser"

    $rxElem4
        nodename
    "wn3-myrser"


## <a name="access-data-in-hive-and-parquet"></a>Acessar dados no Hive e no Parquet

Um recurso disponível no R Server 9.1 permite acesso direto a dados no Hive e no Parquet para serem usados pelas funções ScaleR no contexto de computação do Spark. Esses recursos estão disponíveis por meio de novas funções de fonte de dados do ScaleR chamadas RxHiveData e RxParquetData. Essas funções trabalham com o uso do Spark SQL para carregar dados diretamente em um DataFrame do Spark para análise pelo ScaleR.  

O código abaixo fornece alguns exemplos de como usar as novas funções:

    #Create a Spark compute context
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model
    rxHadoopMakeDir('/share')
    rxHadoopCopyFromLocal(file.path(rxGetOption('sampleDataDir'), 'claimsParquet/'), '/share/')
    pqData <- RxParquetData('/share/claimsParquet',
                     colInfo = list(
                age    = list(type = "factor"),
               car.age = list(type = "factor"),
                  type = list(type = "factor")
             ) )
    rxGetInfo(pqData, getVarInfo = TRUE)

    rxNaiveBayes(type ~ age + cost, data = pqData)

    #Check on Spark data objects, clean up, and close the Spark session
    lsObj <- rxSparkListData() #Two data objects are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() #It should show an empty list
    rxSparkDisconnect(myHadoopCluster)


Para obter mais informações sobre essas novas funções, consulte a ajuda online no R Server usando os comandos `?RxHivedata` e`?RxParquetData`.  


## <a name="install-additional-r-packages-on-the-edge-node"></a>Instalar pacotes R adicionais no nó de borda

Se desejar instalar pacotes R adicionais no nó de borda, você poderá usar o `install.packages()` diretamente do console R quando conectado ao nó de borda por meio do SSH. No entanto, se precisar instalar pacotes R em nós de trabalho do cluster, você deverá usar uma ação de script.

As ações de script são scripts de Bash usados para fazer alterações de configuração no cluster HDInsight ou para instalar um software adicional, como outros pacotes R. Para instalar pacotes adicionais usando uma ação de script, percorra as seguintes etapas.

> [!IMPORTANT]
> Só é possível usar ações de script para instalar pacotes R adicionais depois que o cluster tiver sido criado. Não use este procedimento durante a criação do cluster, porque o script precisa que o R Server esteja completamente instalado e configurado.
>
>

1. No [Portal do Azure](https://portal.azure.com), escolha o Servidor R no cluster HDInsight.

2. No painel **Configurações**, selecione **Ações de Script** > **Enviar Novo**.

   ![Imagem do painel Ações do script](./media/r-server-get-started/scriptaction.png)

3. No painel **Enviar ação de script**, forneça as seguintes informações:

   * **Nome**: um nome amigável para identificar esse script.

   * **URI do script Bash**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`

   * **Cabeçalho**: esse item deve estar limpo.

   * **Trabalho**: esse item deve estar limpo.

   * **Zookeeper**: esse item deve estar limpo.

   * **Nós de borda**: esse item deve estar selecionado.

   * **Parâmetros**: os pacotes R a serem instalados, por exemplo, `bitops stringr arules`.

   * **Persistir esse script**: esse item deve estar selecionado.  

   > [!NOTE]
   > Por padrão, todos os pacotes R são instalados por meio de um instantâneo do repositório do Microsoft R Application Network, que é consistente com a versão do R Server instalada. Se você quiser instalar versões mais recentes dos pacotes, há alguns riscos de incompatibilidade. No entanto, esse tipo de instalação é possível se você especificar `useCRAN` como o primeiro elemento do pacote de lista, por exemplo, `useCRAN bitops, stringr, arules`.  
   > 
   > Alguns pacotes R exigem outras bibliotecas do sistema Linux. Para sua conveniência, pré-instalamos as dependências de que os 100 pacotes R mais populares precisam. Se os pacotes R que você instalar exigirem bibliotecas além dessas, você deverá baixar o script base usado aqui e adicionar etapas para instalar as bibliotecas do sistema. Depois, você deverá carregar o script modificado em um contêiner de blob público no armazenamento do Azure e usar o script modificado para instalar os pacotes.
   >
   > Para saber mais sobre como desenvolver as ações de script, consulte [Desenvolvimento de ação de script](../hdinsight-hadoop-script-actions-linux.md).  
   >
   >

   ![Adicionando uma ação do script](./media/r-server-get-started/submitscriptaction.png)

4. Escolha **Criar** para executar o script. Depois de o script ter sido concluído, os pacotes R ficam disponíveis em todos os nós de trabalho.


## <a name="configure-microsoft-r-server-operationalization"></a>Configurar a operacionalização do Microsoft R Server

Quando sua modelagem de dados for concluída, você poderá operacionalizar o modelo para fazer previsões. Para configurar a operacionalização do Microsoft R Server, execute as seguintes etapas:

1. Use o comando `ssh` para o nó de borda – por exemplo: 

       ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

2. Altere o diretório para a versão relevante e use o comando `sudo dotnet` para o arquivo .dll. 

   Para o Microsoft R Server 9.1:

       cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0
       sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll

   Para o Microsoft R Server 9.0:

       cd /usr/lib64/microsoft-deployr/9.0.1
       sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll

3. Para configurar a operacionalização do Microsoft R Server com a configuração de uma caixa, faça o seguinte:

   a. Selecione `Configure R Server for Operationalization`.

   b. Selecione `A. One-box (web + compute nodes)`.

   c. Insira uma senha para o usuário `admin`.

   ![Operacionalização de uma caixa](./media/r-server-get-started/admin-util-one-box-.png)

4. Como uma etapa opcional, você pode executar um teste de diagnóstico da seguinte forma:

   a. Selecione `6. Run diagnostic tests`.

   b. Selecione `A. Test configuration`.

   c. Insira `admin` como o nome de usuário e insira a senha da etapa de configuração anterior.

   d. Confirme `Overall Health = pass`.

   e. Saia do utilitário do administrador.

   f. Saia do SSH.

   ![Diagnóstico para operacionalização](./media/r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
>Se você tiver longos atrasos ao tentar consumir um serviço Web criado com as funções mrsdeploy no contexto de computação do Spark, talvez seja necessário adicionar algumas pastas ausentes. O aplicativo Spark pertence a um usuário chamado *rserve2* sempre que ele é chamado de um serviço Web pelas funções mrsdeploy. Para resolver o problema:

    #Create these required folders for user rserve2 in local and HDFS
    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    #Create a new Spark compute context 
    rxSparkConnect(reset = TRUE)


Nesse estágio, a configuração de operacionalização foi concluída. Agora você pode usar o pacote mrsdeploy no cliente R para se conectar à operacionalização no nó de borda. Você pode iniciar usando seus recursos, como [execução remota](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) e [serviços Web](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette). Dependendo de se o cluster está configurado em uma rede virtual ou não, talvez você precise configurar o túnel de encaminhamento da porta por meio do logon de SSH.

### <a name="r-server-cluster-on-a-virtual-network"></a>Cluster do R Server em uma rede virtual

Lembre-se de permitir o tráfego pela porta 12800 para o nó de borda. Dessa forma, você pode usar o nó de borda para se conectar ao recurso de operacionalização.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


Se `remoteLogin()` não puder se conectar ao nó de borda, mas for possível usar o SSH para se conectar ao nó de borda, você precisará verificar se a regra que permite o tráfego na porta 12800 está configurada corretamente. Caso o problema persista, você pode usar uma solução alternativa configurando o túnel de encaminhamento da porta por meio de SSH. Para obter instruções, consulte a seção a seguir.

### <a name="r-server-cluster-not-set-up-on-a-virtual-network"></a>Cluster do R Server não configurado em uma rede virtual

Se o cluster não estiver configurado em uma rede virtual ou se você estiver tendo problemas com a conectividade por meio da rede virtual, é possível use o túnel SSH de encaminhamento da porta:

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Você também pode configurá-lo no PuTTY:

![Conexão SSH no PuTTY](./media/r-server-get-started/putty.png)

Depois que a sessão SSH estiver ativa, o tráfego da porta 12800 da máquina será encaminhado para a porta 12800 do nó de borda por meio da sessão SSH. Lembre-se de usar `127.0.0.1:12800` no seu método `remoteLogin()`. Esse método faz logon na operacionalização do nó de borda por meio do encaminhamento de porta.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="scale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a>Dimensionar nós de computação de operacionalização do Microsoft R Server em nós de trabalho do HDInsight

### <a name="decommission-the-worker-nodes"></a>Desativar os nós de trabalho

Atualmente, o Microsoft R Server não é gerenciado por meio de Yarn. Se os nós de trabalho não estiverem desativados, o ResourceManager Yarn não funcionará como esperado porque não estará ciente dos recursos sendo usados pelo servidor. Para evitar essa situação, recomendamos desativar os nós de trabalho antes de escalar horizontalmente os nós de computação.

Para desativar nós de trabalho:

1. Faça logon no console de Ambari do cluster HDI e selecione a guia **Hosts**.
2. Selecione os nós de trabalho a serem desativados e selecione **Ações** > **Hosts selecionados** > **Hosts** > **Ativar o modo de manutenção**. Por exemplo, na imagem a seguir, selecionamos wn3 e wn4 para desativar.  

   ![Captura de tela dos comandos para ativar o modo de manutenção](./media/r-server-get-started/get-started-operationalization.png)  

3. Selecione **Ações** > **Hosts Selecionados** > **DataNodes** > **Desativar**.
4. Selecione **Ações** > **Hosts Selecionados** > **NodeManagers** > **Desativar**.
5. Selecione **Ações** > **Hosts Selecionados** > **DataNodes** > **Parar**.
6. Selecione **Ações** > **Hosts Selecionados** > **NodeManagers** > **Parar**.
7. Selecione **Ações** > **Hosts Selecionados** > **Hosts** > **Parar Todos os Componentes**.
8. Desmarque os nós de trabalho e selecione os nós de cabeçalho.
9. Selecione **Ações** > **Hosts selecionados** > **Hosts** > **Reiniciar Todos os Componentes**.

### <a name="configure-compute-nodes-on-each-decommissioned-worker-node"></a>Configurar nós de computação em cada nó de trabalho desativado

1. Usar SSH para se conectar a cada nó de trabalho desativado.
2. Executar um utilitário de administrador usando `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.
3. Insira `1` para selecionar a opção `Configure R Server for Operationalization`.
4. Insira `c` para selecionar a opção `C. Compute node`. Essa etapa configura o nó de computação no nó de trabalho.
5. Saia do utilitário do administrador.

### <a name="add-compute-nodes-details-on-the-web-node"></a>Adicionar detalhes de nós de computação no nó da Web

Depois que todos os nós de trabalho encerrados estiverem configurados para serem executados no nó de computação, volte ao nó de borda e adicione os endereços IP dos nós de trabalho encerrados na configuração do nó de Web do Microsoft R Server:

1. Use SSH para conectar-se ao nó de borda.
2. Execute `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.
3. Procure a seção `URIs` e adicione o IP do nó de trabalho e detalhes de porta.

    ![Linha de comando do nó de borda](./media/r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a>Solucionar problemas

Se você tiver problemas com a criação de clusters HDInsight, confira os [Requisitos de controle de acesso](../hdinsight-administer-use-portal-linux.md#create-clusters).


## <a name="next-steps"></a>Próximas etapas

Agora você deve entender como criar um cluster HDInsight que inclui o R Server. Você também entende os fundamentos de uso do console R de uma sessão SSH. Os tópicos abaixo explicam outras maneiras de gerenciar e trabalhar com R Server no HDInsight:

* [Opções de contexto de computação para o Servidor R no HDInsight](r-server-compute-contexts.md)
* [Opções de Armazenamento do Azure para o Servidor R no HDInsight](r-server-storage.md)
