---
title: aaaGet iniciada com o servidor do R no HDInsight - Azure | Microsoft Docs
description: Saiba como toocreate um Apache despertar no cluster HDInsight que inclui o R Server e enviar um script R no cluster hello.
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
ms.openlocfilehash: f7e418bbac48eee080a4b4cfbb33e246324ea5c9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-using-r-server-on-hdinsight"></a>Aprenda a usar o Servidor R no HDInsight

HDInsight inclui um toobe de opção R Server integrado ao seu cluster HDInsight. Essa opção permite que scripts R toouse Spark e MapReduce cálculos de toorun distribuído. Neste documento, você aprenderá como toocreate um R Server no cluster HDInsight e, em seguida, executar um R script que demonstra o uso do Spark para distribuídos cálculos de R.


## <a name="prerequisites"></a>Pré-requisitos

* **Uma assinatura do Azure**: antes de começar este tutorial, você deve ter uma assinatura do Azure. Artigo vá toohello [avaliação gratuita do Microsoft Azure obter](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/) para obter mais informações.
* **Um cliente do Secure Shell (SSH)**: um SSH cliente é usado tooremotely conectar o cluster do HDInsight toohello e executar comandos diretamente no cluster de saudação. Para obter mais informações, confira [Usar SSH com HDInsight.](hdinsight-hadoop-linux-use-ssh-unix.md)
* **As chaves de SSH (opcionais)**: você pode proteger a saudação SSH conta usada tooconnect toohello cluster usando uma senha ou uma chave pública. Usando uma senha é mais fácil e permite que você tooget iniciado sem toocreate um par de chaves pública/privada. No entanto, usar uma chave é mais seguro.

> [!NOTE]
> etapas de saudação neste documento pressupõem que você está usando uma senha.


## <a name="automated-cluster-creation"></a>Criação de cluster automatizada

Você pode automatizar a criação de saudação do HDInsight R Servers usando o Gerenciador de recursos do Azure modelos, Olá SDK e também PowerShell.

* toocreate um servidor de R usando um modelo de gerenciamento de recursos do Azure, consulte [implantar um cluster de HDInsight R server](https://azure.microsoft.com/resources/templates/101-hdinsight-rserver/).
* toocreate um servidor de R usando Olá .NET SDK, consulte [criar clusters baseados em Linux em HDInsight usando Olá .NET SDK.](hdinsight-hadoop-create-linux-clusters-dotnet-sdk.md)
* toodeploy R Server usando o powershell, consulte o artigo de saudação em [criação de um servidor de R no HDInsight com o PowerShell](hdinsight-hadoop-create-linux-clusters-azure-powershell.md).


<a name="create-hdi-custer-with-aure-portal"></a>
## <a name="create-hello-cluster-using-hello-azure-portal"></a>Criar cluster hello usando Olá portal do Azure

1. Entrar toohello [portal do Azure](https://portal.azure.com).

2. Selecione **NOVO** -> **Intelligence + Análises**, -> **HDInsight**.

    ![Imagem da criação de um novo cluster](./media/hdinsight-hadoop-r-server-get-started/newcluster.png)

3. Em Olá **criação rápida** experiência, insira um nome para o cluster de saudação em Olá **nome do Cluster** campo. Se você tiver várias assinaturas do Azure, use Olá **assinatura** entrada tooselect Olá um toouse desejado.

    ![Nome do cluster e seleções de assinatura](./media/hdinsight-hadoop-r-server-get-started/clustername.png)

4. Selecione **tipo de Cluster** tooopen Olá **configuração de Cluster** folha. Em Olá **configuração de Cluster** folha, selecione Olá as opções a seguir:

    * **Tipo de Cluster**: Servidor R
    * **Versão**: versão select Olá tooinstall R Server no cluster hello. Olá versão disponível no momento é ***R Server 9.1 (HDI 3.6)***. Notas de versão para versões disponíveis de saudação do servidor do R estão disponíveis [aqui](https://msdn.microsoft.com/microsoft-r/notes/r-server-notes).
    * **Edição de comunidade do estúdio R para R Server**: o IDE baseada em navegador é instalado por padrão no nó de borda hello. Se você preferir toonot que ele seja instalado, em seguida, desmarque a caixa de seleção de saudação. Se você escolher toohave-lo instalado, Olá URL para acessar Olá logon de servidor RStudio é encontrado em uma folha de aplicativo de portal para o cluster quando ela é criada.
    * Deixe Olá outras opções com valores padrão de saudação e usar Olá **selecione** toosave Olá cluster tipo de botão.

        ![Captura de tela do tipo de folha do cluster](./media/hdinsight-hadoop-r-server-get-started/clustertypeconfig.png)

5. Insira um **Nome de usuário de logon do cluster** e uma **Senha de logon do cluster**.

    Especifique um **Nome de Usuário SSH**. SSH é usado tooremotely conectar toohello cluster usando um **Secure Shell (SSH)** cliente. Você pode especificar usuário SSH Olá nesta caixa de diálogo ou após Olá cluster foi criado (na guia de configuração de saudação para cluster Olá). R Server está configurado tooexpect um **nome de usuário SSH** de "remoteuser".  **Se você usar um nome de usuário diferente, você deve executar uma etapa adicional após Olá cluster é criado.**

    Caixa de saudação deixe marcada para **usar a mesma senha de logon de cluster** toouse **senha** como hello tipo de autenticação, a menos que você preferir que o uso de uma chave pública.  Você precisa de um par de chaves pública/privada de tooaccess R Server no cluster Olá por meio de um cliente remoto como, por exemplo, RTVS, RStudio ou outro IDE de área de trabalho. Se você instalar Olá edição do servidor RStudio community, será necessário toochoose uma senha SSH.     

    toocreate e use um par de chaves pública/privada, desmarque **usar a mesma senha de logon de cluster** e, em seguida, selecione **chave pública** e faça o seguinte. Estas instruções pressupõem que você tenha o Cygwin com ssh-keygen ou equivalente instalado.

    * Gere um par de chaves pública/privada do prompt de comando de saudação em seu laptop:

        ssh-keygen -t rsa -b 2048

    * Siga Olá prompt tooname um arquivo de chave e, em seguida, insira uma frase secreta para aumentar a segurança. Sua tela deve ser semelhante a saudação a imagem a seguir:

        ![Linha de comando SSH no Windows](./media/hdinsight-hadoop-r-server-get-started/sshcmdline.png)

    * Este comando cria um arquivo de chave privada e um arquivo de chave pública em pub de nome < arquivo de chave privada > Olá, por exemplo, furiosa e furiosa.pub.

        ![Dir SSH](./media/hdinsight-hadoop-r-server-get-started/dir.png)

    * Em seguida, especifique o arquivo de chave pública de saudação (&#42;. pub) quando atribuir HDI credenciais de cluster e, por fim, confirme a grupo de recursos e região e selecione **próximo**.

        ![Folha Credenciais](./media/hdinsight-hadoop-r-server-get-started/publickeyfile.png)  

   * Alterar as permissões no arquivo de chave privada em seu laptop hello:

        chmod 600 <private-key-filename>

   * Use o arquivo de chave privada Olá com SSH para logon remoto:

        ssh –i <private-key-filename> remoteuser@<hostname public ip>

      Ou, como definição de saudação de parte de seu Hadoop Spark contexto de computação para o servidor do R no cliente de saudação. Consulte Olá **usando o Microsoft R Server como um cliente de Hadoop** subseção em [criar um contexto de computação para Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started#creating-a-compute-context-for-spark).

6. criação rápida de saudação faz transição toohello **armazenamento** conta de armazenamento blade tooselect Olá toobe configurações usado para local primário de saudação do hello usado pelo cluster Olá de sistema de arquivos do HDFS. Selecione uma conta nova ou existente do Armazenamento do Azure ou uma conta existente de armazenamento do Data Lake.

    - Se você selecionar uma conta de armazenamento do Azure, uma conta de armazenamento existente é selecionada, escolhendo **selecionar uma conta de armazenamento** e, em seguida, selecionando conta relevante hello. Criar uma nova conta usando Olá **criar novo** link no hello **selecionar uma conta de armazenamento** seção.

      > [!NOTE]
      > Se você selecionar **novo** você deve inserir um nome para a nova conta de armazenamento hello. Uma marca de seleção verde é exibida se o nome da saudação é aceito.

      Olá **contêiner padrão** nome de toohello padrões de cluster hello. Deixe o padrão como valor de saudação.

      Se uma nova opção de conta de armazenamento foi selecionada um prompt tooselect **local** é determinada tooselect toocreate qual região Olá conta de armazenamento.  

         ![Folha de fonte de dados](./media/hdinsight-getting-started-with-r/datastore.png)  

      > [!IMPORTANT]
      > Também selecionando Olá local para a fonte de dados padrão de saudação define o local de saudação do cluster do HDInsight hello. Olá fonte de dados padrão e de cluster deve estar no hello mesma região.

    - Se você quiser toouse um repositório do Data Lake existente, selecione Olá ADLS toouse de conta de armazenamento e adicionar cluster Olá *adicionar* identidade tooyour cluster tooallow acessar toohello o repositório. Para obter mais informações sobre este processo, consulte [Criar um cluster do HDInsight com o Data Lake Store usando o Portal do Azure](https://docs.microsoft.com/azure/data-lake-store/data-lake-store-hdinsight-hadoop-use-portal).

    Saudação de uso **selecione** configuração de fontes de dados do botão toosave hello.


7. Olá **resumo** folha, em seguida, exibe toovalidate todas as suas configurações. Aqui você pode alterar sua **tamanho do Cluster** toomodify Olá o número de servidores no cluster e também especificar qualquer **ações de Script** toorun desejado. A menos que você sabe que precisa de um cluster maior, deixe o número de saudação de nós de trabalho com o padrão de saudação do `4`. Olá estimativa de custo de cluster Olá é mostrado na folha de saudação.

    ![resumo do cluster](./media/hdinsight-hadoop-r-server-get-started/clustersummary.png)

   > [!NOTE]
   > Se necessário, você pode redimensionar o cluster mais tarde por meio de saudação Portal (**Cluster** -> **configurações** -> **Cluster de escala**) tooincrease ou Diminua o número de saudação de nós de trabalho.  Este redimensionamento pode ser útil para quando ocioso cluster hello quando não estiver em uso, ou para adicionar as necessidades de saudação do toomeet de capacidade de tarefas maior.
   >
   >

   Tookeep alguns fatores em mente ao dimensionar seu cluster, nós de dados hello e nó de borda Olá incluem:  

   * desempenho Olá de análises de R Server distribuídos no Spark é proporcional toohello número de nós de trabalho quando dados saudação forem grandes.  

   * desempenho de saudação de análises de R Server é linear no tamanho de saudação dos dados que está sendo analisados. Por exemplo:  

     * Para dados toomodest pequenos, o desempenho é melhor quando analisada em um contexto de computação local no nó de borda hello.  Para obter mais informações sobre cenários de saudação sob a qual hello local e o Spark contextos de computação funcionam melhor, consulte Opções de contexto de computação para o servidor do R no HDInsight.<br>
     * Se você fazer logon no nó de borda toohello e executa o script R, mas Olá funções de rx ScaleR são executadas <strong>localmente</strong> no nó de borda hello. Olá para memória e número de núcleos de nó de borda Olá sejam dimensionado adequadamente. Olá que mesmo se aplica se você usar R Server em HDI como um contexto de computação remota de seu laptop.

     ![Folha de camadas de preços de nó](./media/hdinsight-hadoop-r-server-get-started/pricingtier.png)

     Saudação de uso **selecione** nó de saudação do botão toosave preços de configuração.

   Também há um link para **Baixar modelo e parâmetros**. Clique em scripts de toodisplay esse link podem ser usado tooautomate Olá criação de um cluster com a configuração selecionada hello. Esses scripts também estão disponíveis no hello entrada portal do Azure para seu cluster quando ele tiver sido criado.

   > [!NOTE]
   > Levará algum tempo para Olá cluster toobe criado, normalmente em torno de 20 minutos. Use o bloco Olá Olá quadro inicial ou Olá **notificações** entrada hello à esquerda do hello página toocheck no processo de criação de saudação.
   >
   >

<a name="connect-to-rstudio-server"></a>
## <a name="connect-toorstudio-server"></a>Conecte-se tooRStudio Server

Se você tiver escolhido tooinclude edição do servidor RStudio community em sua instalação, você pode acessar o logon de RStudio Olá por meio de dois métodos diferentes.

1. Vá toohello URL a seguir (onde **CLUSTERNAME** é Olá nome do cluster de saudação que você criou):

    https://**CLUSTERNAME**.azurehdinsight.net/rstudio/

2. Abrir a entrada de Olá para seu cluster em Olá portal do Azure, selecione Olá **R Server painéis** link rápido e, em seguida, selecionando Olá **R Studio painel**:

     ![Painel de controle do acesso Olá R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard1.png)

     ![Painel de controle do acesso Olá R studio](./media/hdinsight-getting-started-with-r/rstudiodashboard2.png)

   > [!IMPORTANT]
   > Independentemente do método hello usado, hello primeira vez que você efetuar logon é necessário tooauthenticate duas vezes.  Na primeira autenticação de hello, fornecem Olá *ID de usuário do administrador de cluster* e *senha*. No prompt de segundo hello, fornecer Olá *SSH userid* e *senha*. Log subsequentes ins exigem apenas Olá *senha SSH* e *userid*.

<a name="connect-to-edge-node"></a>
## <a name="connect-toohello-r-server-edge-node"></a>Conecte-se o nó de borda de R Server toohello

Conecte-se tooR nó de borda do servidor do cluster do HDInsight hello usando o SSH com o comando hello:

   `ssh USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net`

> [!NOTE]
> Você pode encontrar hello `USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net` endereço no hello portal do Azure, selecionando o cluster, em seguida, **todas as configurações** -> **aplicativos** -> **RServer**. Isso exibe Olá informações de ponto de extremidade SSH para nó de borda de saudação.
>
> ![Imagem de saudação de ponto de extremidade SSH para o nó de borda Olá](./media/hdinsight-hadoop-r-server-get-started/sshendpoint.png)
>
>

Se você usou uma senha toosecure sua conta de usuário SSH, é solicitada tooentê-lo. Se você usou uma chave pública, você pode ter toouse Olá `-i` toospecify parâmetro hello chave privada correspondente. Por exemplo:

    ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Para obter mais informações, consulte [conectar tooHDInsight (Hadoop) usando o SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

Uma vez conectado, você chega em uma prompt toohello a seguir semelhante:

    sername@ed00-myrser:~$

<a name="enable-concurrent-users"></a>
## <a name="enable-multiple-concurrent-users"></a>Habilitar múltiplos usuário simultâneos

Você pode habilitar vários usuários simultâneos adicionando mais usuários para o nó de borda Olá no qual Olá comunidade RStudio versão é executado.

Quando você cria um cluster HDInsight, deve fornecer dois usuários, um usuário HTTP e um usuário SSH:

![Usuários simultâneos 1](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-1.png)

- **Nome de usuário de logon de cluster**: um usuário HTTP para autenticação por meio do gateway de HDInsight Olá que é usado tooprotect hello HDInsight clusters que você criou. Este usuário HTTP é usado tooaccess Olá Ambari UI, YARN da interface do usuário, bem como outros componentes de interface do usuário.
- **Nome de usuário de Shell (SSH) segura**: um cluster de saudação do SSH usuário tooaccess por meio do secure shell. Este usuário é um usuário em Olá sistema Linux para todos os nós de cabeçalho hello, nós de trabalho e nós de borda. Então você pode usar do secure shell tooaccess qualquer um de nós de saudação em um cluster remoto.

Olá R Studio Server Community na versão usada Olá Microsoft R Server no cluster do HDInsight tipo aceita apenas o nome de usuário do Linux e a senha como um mecanismo de logon. Ele não dá suporte a tokens de passagem. Portanto, se você tiver criado um novo cluster e deseja toouse Studio R tooaccess-lo, você precisa toolog em duas vezes.

- Primeiro, faça logon usando credenciais de usuário de saudação HTTP por meio de saudação HDInsight Gateway: 

    ![Usuário simultâneo 2a](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2a.png)

- Em seguida, use Olá toolog de credenciais de usuário SSH no tooRStudio:
  
    ![Usuário simultâneo 2b](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-2b.png)

Atualmente, apenas uma conta de usuário SSH pode ser criada durante o provisionamento de um cluster HDInsight. Para clusters de vários usuários tooaccess Microsoft R Server no HDInsight tooenable, precisamos toocreate mais usuários em Olá sistema Linux.

Como RStudio Server Community está em execução no nó de borda do cluster hello, há várias etapas aqui:

1. Usar toolog de usuário SSH Olá criada no nó de borda toohello
2. Adicionar mais usuários do Linux ao nó de borda
3. Use a versão de comunidade RStudio com usuário Olá criado

### <a name="step-1-use-hello-created-ssh-user-toolog-in-toohello-edge-node"></a>Etapa 1: Usar toolog de usuário SSH Olá criada no nó de borda toohello

Baixar qualquer ferramenta SSH (como o Putty) e usar o hello existente SSH usuário toolog no. Siga instruções Olá fornecidas no [conectar tooHDInsight (Hadoop) usando o SSH](hdinsight-hadoop-linux-use-ssh-unix.md) tooaccess Olá nó de borda. endereço de nó de borda Olá para R Server no cluster HDInsight é: *clustername-ed-ssh.azurehdinsight.net*


### <a name="step-2-add-more-linux-users-in-edge-node"></a>Etapa 2: adicionar mais usuários do Linux ao nó de borda

tooadd um nó de borda de toohello de usuário, execute os comandos de saudação:

    sudo useradd yournewusername -m
    sudo passwd yourusername

Você deve ver Olá itens retornados a seguir: 

![Usuários simultâneos 3](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-3.png)

Quando solicitado para "senha Kerberos atual:", basta pressionar **Enter** tooignore-lo. Olá `-m` opção `useradd` comando indica que o sistema Olá criará uma pasta base para usuário hello, que é necessário para a versão da comunidade de RStudio.


### <a name="step-3-use-rstudio-community-version-with-hello-user-created"></a>Etapa 3: Versão de uso RStudio comunidade com usuário Olá criado

Use Olá criado pelo usuário toolog tooRStudio:

![Usuários simultâneos 4](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-4.png)

Observe que RStudio indica que você está usando o novo usuário de saudação (aqui, por exemplo, *sshuser6*) toolog em cluster hello: 

![Usuários simultâneos 5](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-5.png)

Você também pode fazer logon usando credenciais de saudação original (por padrão, ele é *sshuser*) simultaneamente a partir de outra janela do navegador.

Você pode enviar um trabalho usando funções scaleR. Aqui está um exemplo de hello comandos usados toorun um trabalho:

    # Set hello HDFS (WASB) location of example data.
    bigDataDirRoot <- "/example/data"

    # Create a local folder for storaging data temporarily.
    source <- "/tmp/AirOnTimeCSV2012"
    dir.create(source)

    # Download data toohello tmp folder.
    remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
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

    # Set directory in bigDataDirRoot tooload hello data.
    inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

    # Create hello directory.
    rxHadoopMakeDir(inputDir)

    # Copy hello data from source tooinput.
    rxHadoopCopyFromLocal(source, bigDataDirRoot)

    # Define hello HDFS (WASB) file system.
    hdfsFS <- RxHdfsFileSystem()

    # Create info list for hello airline data.
    airlineColInfo <- list(
    DAY_OF_WEEK = list(type = "factor"),
    ORIGIN = list(type = "factor"),
    DEST = list(type = "factor"),
    DEP_TIME = list(type = "integer"),
    ARR_DEL15 = list(type = "logical"))

    # Get all hello column names.
    varNames <- names(airlineColInfo)

    # Define hello text data source in HDFS.
    airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

    # Define hello text data source in local system.
    airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

    # Specify hello formula toouse.
    formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

    # Define hello Spark compute context.
    mySparkCluster <- RxSpark()

    # Set hello compute context.
    rxSetComputeContext(mySparkCluster)

    # Run a logistic regression.
    system.time(
        modelSpark <- rxLogit(formula, data = airOnTimeData)
    )

    # Display a summary.
    summary(modelSpark)


Observe que os trabalhos de saudação enviados são em nomes de usuário diferente na interface do usuário do YARN:

![Usuários simultâneos 6](./media/hdinsight-hadoop-r-server-get-started/concurrent-users-6.png)

Observe também que Olá recém-adicionado usuários não têm privilégios de raiz no sistema Linux, mas eles têm Olá mesmo acessar arquivos de saudação do tooall no armazenamento remoto Olá HDFS e WASB.


<a name="use-r-console"></a>
## <a name="use-hello-r-console"></a>Use o console Olá R

1. Da sessão SSH hello, use Olá console do comando toostart Olá R a seguir:  

        R

2. Você deve ver o seguinte de toohello semelhante de saída:
    
    R versão 3.2.2 (2015-08-14) – "Segurança de incêndio" Copyright (C) 2015 hello R Foundation para a plataforma de computação de estatísticas: x86_64 pc linux-gnu (64 bits)

    R é um software livre e vem com ABSOLUTAMENTE NENHUMA GARANTIA.
    São boas-vinda tooredistribute sob determinadas condições.
    Digite 'license()' ou 'licence()' para obter detalhes de distribuição.

    Suporte de linguagem natural, mas em execução em uma localidade com idioma inglês

    R é um projeto de colaboração com muitos colaboradores.
    Digite 'contributors()' para obter mais informações e 'citation()' em como toocite R ou R pacotes em publicações.

    Digite 'demo()' para algumas demonstrações, help() para obter ajuda online ou help.start() para um toohelp de interface do navegador HTML.
    Digite 'chamar' tooquit R.

    Microsoft R Server versão 8.0: uma distribuição avançada de pacotes Microsoft R Copyright (C) 2016 Microsoft Corporation

    Digite readme() para notas de versão.
    >

3. De saudação `>` prompt, você pode inserir o código R. Servidor de R inclui pacotes que permitem que você tooeasily interagir com Hadoop e executar cálculos distribuídos. Por exemplo, use Olá raiz de saudação do comando tooview saudação padrão do sistema de arquivos para o cluster do HDInsight Olá a seguir:

    rxHadoopListFiles("/")

4. Você também pode usar o hello WASB estilo endereçamento.

    rxHadoopListFiles("wasb:///")


## <a name="using-r-server-on-hdi-from-a-remote-instance-of-microsoft-r-server-or-microsoft-r-client"></a>Usando o Servidor R no HDI de uma instância remota do Microsoft R Server ou Microsoft R Client

É possível tooset o contexto de computação do acesso toohello HDI Hadoop Spark de uma instância remota do Microsoft R Server ou o cliente do Microsoft R em execução em um desktop ou laptop. Consulte **usando o Microsoft R Server como um cliente de Hadoop** subseção Olá [criando um contexto de computação para Spark](https://msdn.microsoft.com/microsoft-r/scaler-spark-getting-started.md). toodo assim, você precisa toospecify Olá as opções a seguir ao definir o contexto de computação RxSpark Olá em seu laptop: hdfsShareDir, shareDir, sshUsername, sshHostname, sshSwitches e sshProfileScript. Por exemplo:


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

Um contexto de computação permite toocontrol se a computação é executada localmente no nó de borda de saudação ou distribuída entre nós Olá no cluster do HDInsight hello.

1. Servidor RStudio ou console Olá R (em uma sessão SSH), use Olá dados de exemplo de tooload de código a seguir no armazenamento padrão da saudação para HDInsight:

        # Set hello HDFS (WASB) location of example data
        bigDataDirRoot <- "/example/data"

        # create a local folder for storaging data temporarily
        source <- "/tmp/AirOnTimeCSV2012"
        dir.create(source)

        # Download data toohello tmp folder
        remoteDir <- "http://packages.revolutionanalytics.com/datasets/AirOnTimeCSV2012"
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

        # Set directory in bigDataDirRoot tooload hello data into
        inputDir <- file.path(bigDataDirRoot,"AirOnTimeCSV2012")

        # Make hello directory
        rxHadoopMakeDir(inputDir)

        # Copy hello data from source tooinput
        rxHadoopCopyFromLocal(source, bigDataDirRoot)

2. Em seguida, vamos criar algumas informações de dados e definir duas fontes de dados para que possamos trabalhar com dados de saudação.

        # Define hello HDFS (WASB) file system
        hdfsFS <- RxHdfsFileSystem()

        # Create info list for hello airline data
        airlineColInfo <- list(
             DAY_OF_WEEK = list(type = "factor"),
             ORIGIN = list(type = "factor"),
             DEST = list(type = "factor"),
             DEP_TIME = list(type = "integer"),
             ARR_DEL15 = list(type = "logical"))

        # get all hello column names
        varNames <- names(airlineColInfo)

        # Define hello text data source in hdfs
        airOnTimeData <- RxTextData(inputDir, colInfo = airlineColInfo, varsToKeep = varNames, fileSystem = hdfsFS)

        # Define hello text data source in local system
        airOnTimeDataLocal <- RxTextData(source, colInfo = airlineColInfo, varsToKeep = varNames)

        # formula toouse
        formula = "ARR_DEL15 ~ ORIGIN + DAY_OF_WEEK + DEP_TIME + DEST"

3. Vamos executar uma regressão logística em dados de saudação usando o contexto de computação local hello.

        # Set a local compute context
        rxSetComputeContext("local")

        # Run a logistic regression
        system.time(
           modelLocal <- rxLogit(formula, data = airOnTimeDataLocal)
        )

        # Display a summary
        summary(modelLocal)

    Você deve ver a saída que termina com linhas toohello semelhante a seguir:

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

4. Em seguida, vamos executar Olá mesmo Regressão logística usando Olá Spark contexto. contexto do Spark Olá distribui Olá processamento em todos os nós de trabalho Olá no cluster do HDInsight hello.

        # Define hello Spark compute context
        mySparkCluster <- RxSpark()

        # Set hello compute context
        rxSetComputeContext(mySparkCluster)

        # Run a logistic regression
        system.time(  
           modelSpark <- rxLogit(formula, data = airOnTimeData)
        )
        
        # Display a summary
        summary(modelSpark)


   > [!NOTE]
   > Você também pode usar o cálculo de toodistribute MapReduce em nós de cluster. Para saber mais sobre o contexto de computação, confira [Opções de contexto de computação para o Servidor R no HDInsight](hdinsight-hadoop-r-server-compute-contexts.md).


## <a name="distribute-r-code-toomultiple-nodes"></a>Distribuir nós de toomultiple código R

Com o servidor de R, você pode facilmente executar código R existente e executá-lo em vários nós no cluster hello usando `rxExec`. Essa função é útil ao fazer uma limpeza de parâmetro ou simulações. Olá, código a seguir é um exemplo de como toouse `rxExec`:

    rxExec( function() {Sys.info()["nodename"]}, timesToRun = 4 )

Se você ainda estiver usando Olá Spark ou contexto de MapReduce, esse comando retorna valor de nodename Olá para nós de trabalho Olá código Olá `(Sys.info()["nodename"])` é executado no. Por exemplo, em um cluster de quatro nós, você espera que tooreceive de saída a seguir toohello semelhante:

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


## <a name="accessing-data-in-hive-and-parquet"></a>Acessando dados no Hive e no Parquet

Um recurso disponível em R Server 9.1 permite toodata acesso direto no Hive e Parquet para uso por funções ScaleR no contexto de computação Olá Spark. Esses recursos estão disponíveis por meio de novos dados fonte funções ScaleR chamadas RxHiveData e RxParquetData que funcionam com o uso de dados do Spark SQL tooload diretamente em um DataFrame Spark para análise pelo ScaleR.  

saudação de código a seguir fornece um exemplo de código sobre o uso de novas funções de saudação:

    #Create a Spark compute context:
    myHadoopCluster <- rxSparkConnect(reset = TRUE)

    #Retrieve some sample data from Hive and run a model:
    hiveData <- RxHiveData("select * from hivesampletable",
                     colInfo = list(devicemake = list(type = "factor")))
    rxGetInfo(hiveData, getVarInfo = TRUE)

    rxLinMod(querydwelltime ~ devicemake, data=hiveData)

    #Retrieve some sample data from Parquet and run a model:
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

    #Check on Spark data objects, cleanup, and close hello Spark session:
    lsObj <- rxSparkListData() # two data objs are cached
    lsObj
    rxSparkRemoveData(lsObj)
    rxSparkListData() # it should show empty list
    rxSparkDisconnect(myHadoopCluster)


Para obter informações adicionais sobre o uso dessas novas funções consulte a Ajuda online Olá no R Server através do uso de saudação `?RxHivedata` e `?RxParquetData` comandos.  


## <a name="install-additional-r-packages-on-hello-edge-node"></a>Instalar pacotes R adicionais no nó de borda Olá

Se você quiser tooinstall pacotes de R adicionais no nó de borda hello, você pode usar `install.packages()` diretamente de dentro Olá console R quando conectado toohello borda nó por meio do SSH. No entanto, se você precisar tooinstall pacotes de R em nós de trabalho de saudação do cluster de saudação, você deve usar uma ação de Script.

Ações de script são scripts de Bash que são usadas toomake configuração alterações toohello HDInsight cluster ou tooinstall software adicional, como pacotes R adicionais. tooinstall pacotes adicionais usando uma ação de Script, use Olá etapas a seguir:

> [!IMPORTANT]
> Usar pacotes de R adicionais tooinstall ações de Script só pode ser usado depois Olá cluster foi criado. Não use esse procedimento durante a criação do cluster, como o script hello se baseia em R Server sendo completamente instalado e configurado.
>
>

1. De saudação [portal do Azure](https://portal.azure.com), selecione o servidor do R no cluster HDInsight.

2. De saudação **configurações** folha, selecione **ações de Script** e **Enviar nova** toosubmit uma nova ação de Script.

   ![Imagem da folha de ações do script](./media/hdinsight-hadoop-r-server-get-started/scriptaction.png)

3. De saudação **enviar ação de script** folha, fornecer Olá informações a seguir:

   * **Nome**: amigável para um nome tooidentify este script

   * **URI do script Bash**: `http://mrsactionscripts.blob.core.windows.net/rpackages-v01/InstallRPackages.sh`

   * **Cabeçalho**: esse item deve estar **desmarcado**

   * **Trabalho**: esse item deve estar **marcado**

   * **Nós de borda**: esse item deve estar **desmarcado**.

   * **Zookeeper**: esse item deve estar **desmarcado**

   * **Parâmetros**: Olá R pacotes toobe instalado. Por exemplo, `bitops stringr arules`

   * **Persistir esse script...**: esse item estar **marcado**  

   > [!NOTE]
   > 1. Por padrão, todos os pacotes de R são instalados de um instantâneo do repositório de MRAN Microsoft hello consistente com a versão de saudação do servidor de R que foi instalado. Se você quiser tooinstall de versões mais recentes dos pacotes, há alguns riscos de incompatibilidade. No entanto esse tipo de instalação é possível especificando `useCRAN` como Olá primeiro elemento do pacote de saudação de lista, por exemplo `useCRAN bitops, stringr, arules`.  
   > 2. Alguns pacotes R exigem outras bibliotecas do sistema Linux. Para sua conveniência, podemos ter pré-instalado dependências Olá necessárias por Olá top 100 pacotes R mais populares. No entanto, se precisam de pacotes de R Olá que instalar bibliotecas além esses, em seguida, você deve baixar Olá script base usado aqui e adicionar etapas tooinstall Olá sistema bibliotecas. Você deve carregar Olá modificado script tooa público blob contêiner no armazenamento do Azure e usar pacotes de saudação do hello modificado script tooinstall.
   >    Para saber mais sobre como desenvolver as Ações de Script, confira [Desenvolvimento de ação de script](hdinsight-hadoop-script-actions-linux.md).  
   >
   >

   ![Adicionando uma ação do script](./media/hdinsight-getting-started-with-r/submitscriptaction.png)

4. Selecione **criar** toorun script de saudação. Após a conclusão do script hello, pacotes de saudação R estão disponíveis em todos os nós de trabalho.


## <a name="using-microsoft-r-server-operationalization"></a>Usando a operacionalização do Microsoft R Server

Quando a modelagem de dados for concluída, você pode colocar previsões de toomake modelo Olá. tooconfigure para operacionalização do Microsoft R Server, execute Olá etapas a seguir:

Primeiro, ssh no nó de borda hello. Por exemplo, 

    ssh -L USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Depois de usar ssh, altere o diretório para versão relevantes hello e sudo Olá dotnet dll: 

- Para o Microsoft R Server 9.1:

    cd /usr/lib64/microsoft-r/rserver/o16n/9.1.0   sudo dotnet Microsoft.RServer.Utils.AdminUtil/Microsoft.RServer.Utils.AdminUtil.dll

- Para o Microsoft R Server 9.0:

    cd /usr/lib64/microsoft-deployr/9.0.1   sudo dotnet Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll

operacionalização do Microsoft R Server tooconfigure com uma configuração de uma caixa Olá a seguir:

1. Selecione “Configurar o R Server para operacionalização”
2. Selecione "A. Uma caixa (web + nós de computação)"
3. Digite uma senha para Olá **admin** usuário

![operações de uma caixa](./media/hdinsight-hadoop-r-server-get-started/admin-util-one-box-.png)

Como uma etapa opcional, você pode executar verificações de diagnóstico com um teste de diagnóstico da seguinte forma:

1. Selecione "6. Executar testes de diagnóstico”
2. Selecione "A. Configuração de teste”
3. Insira o nome de usuário = "admin" e a senha da etapa de configuração anterior
4. Confirme a integridade geral = aprovado
5. Utilitário de administração de saudação de saída
6. Sair do SSH

![Diagnóstico para operações](./media/hdinsight-hadoop-r-server-get-started/admin-util-diagnostics.png)


>[!NOTE]
>**Atrasos longos ao consumir um serviço web no Spark**
>
>Se você encontrar longos atrasos ao tentar tooconsume um serviço web criado com as funções de mrsdeploy em um contexto de computação Spark, talvez seja necessário tooadd algumas pastas ausentes. Olá aplicativo Spark pertence a usuário tooa chamado '*rserve2*' sempre que ele é chamado de um serviço web usando funções mrsdeploy. toowork esse problema:

    # Create these required folders for user 'rserve2' in local and hdfs:

    hadoop fs -mkdir /user/RevoShare/rserve2
    hadoop fs -chmod 777 /user/RevoShare/rserve2

    mkdir /var/RevoShare/rserve2
    chmod 777 /var/RevoShare/rserve2


    # Next, create a new Spark compute context:
 
    rxSparkConnect(reset = TRUE)


Neste estágio, a configuração de saudação para operacionalização foi concluída. Agora você pode usar o hello 'mrsdeploy' o pacote em seu toohello de tooconnect RClient operacionalização no nó de borda e começar a usar seus recursos, como [execução remota](https://msdn.microsoft.com/microsoft-r/operationalize/remote-execution) e [serviços web](https://msdn.microsoft.com/microsoft-r/mrsdeploy/mrsdeploy-websrv-vignette). Dependendo se o cluster é configurado em uma rede virtual ou não, talvez seja necessário tooset a porta direta túnel por meio de logon SSH. Olá seções a seguir explicam como tooset backup esse túnel.

### <a name="rserver-cluster-on-virtual-network"></a>Cluster do RServer em Rede Virtual

Verifique se que você permitir o tráfego por meio do nó de borda toohello 12800 de porta. Dessa forma, você pode usar o recurso do hello borda nó tooconnect toohello operacionalização.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://[your-cluster-name]-ed-ssh.azurehdinsight.net:12800",
        username = "admin",
        password = "xxxxxxx"
    )


Se hello `remoteLogin()` não é possível conectar-se o nó de borda toohello, mas é possível que o nó de borda toohello SSH, você precisará tooverify se o tráfego na porta 12800 tooallow de regra de saudação foi configurado corretamente ou não. Se você continuar problema de saudação tooface, você pode trabalhar ao redor dele com a configuração de porta direta túnel por meio do SSH. Para obter instruções, consulte Olá seção a seguir.

### <a name="rserver-cluster-not-set-up-on-virtual-network"></a>Cluster do RServer não configurado em rede virtual

Se o cluster não estiver configurado na rede virtual ou se você estiver tendo problemas com a conectividade por meio da rede virtual, use o túnel SSH de encaminhamento da porta:

    ssh -L localhost:12800:localhost:12800 USERNAME@CLUSTERNAME-ed-ssh.azurehdinsight.net

Você também pode configurá-la em Putty.

![conexão SSH em putty](./media/hdinsight-hadoop-r-server-get-started/putty.png)

Depois que sua sessão SSH está ativa, o tráfego de saudação da porta do computador 12800 é encaminhado porta do nó de borda toohello 12800 por meio de sessão SSH. Use `127.0.0.1:12800` no seu método `remoteLogin()`. Isso registra no operacionalização do nó de borda toohello por meio de encaminhamento de porta.


    library(mrsdeploy)

    remoteLogin(
        deployr_endpoint = "http://127.0.0.1:12800",
        username = "admin",
        password = "xxxxxxx"
    )


## <a name="how-tooscale-microsoft-r-server-operationalization-compute-nodes-on-hdinsight-worker-nodes"></a>Como o tooscale Microsoft R Server operacionalização nós em nós de trabalho HDInsight de computação

### <a name="decommission-hello-worker-nodes"></a>Encerrar Olá nó (s) de trabalho

Atualmente, o Microsoft R Server não é gerenciado por meio de Yarn. Se nós de trabalho Olá não estiverem encerrados, Olá Yarn Gerenciador de recursos não funcionará conforme esperado, pois ele não estar ciente recursos Olá consumidos pelo servidor de saudação. Em ordem tooavoid nessa situação, é recomendável encerramento nós de trabalho Olá antes de você expandir nós de computação hello.

Nós de trabalho toodecommissioning etapas:

* Faça logon no console do Ambari tooHDI do cluster e clique na guia "hosts"
* Selecione nós de trabalho (toobe encerrado), clique em "Ações" > "Hosts selecionados" > "Hosts" > clique em "Ativar o modo de manutenção ON". Por exemplo, Olá a imagem a seguir nós selecionamos toodecommission wn3 e wn4.  

   ![encerrar nós de trabalho](./media/hdinsight-hadoop-r-server-get-started/get-started-operationalization.png)  

* Selecione **Ações** > **Hosts Selecionados** > **DataNodes** > clique em **Desativar**
* Selecione **Ações** > **Hosts Selecionados** > **NodeManagers** > clique em **Desativar**
* Selecione **Ações** > **Hosts Selecionados** > **DataNodes** > clique em **Parar**
* Selecione **Ações** > **Hosts Selecionados** > **NodeManagers** > clique em **Parar**
* Selecione **Ações** > **Hosts Selecionados** > **Hosts** > clique em **Parar Todos os Componentes**
* Cancele a seleção de nós de trabalho hello e selecione nós de cabeçalho Olá
* Selecione **Ações** > **Hosts selecionados** > "**Hosts** > **Reiniciar Todos os Componentes**

### <a name="configure-compute-nodes-on-each-decommissioned-worker-nodes"></a>Configurar nós de computação em cada nó de trabalho encerrado

1. SSH em cada nó de trabalho desativado.
2. Executar o utilitário Administrador usando `dotnet /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Utils.AdminUtil/Microsoft.DeployR.Utils.AdminUtil.dll`.
3. Insira "1" tooselect opção "Configurar o servidor de R para operacionalização".
4. Insira a opção tooselect "c" "c. Nó de computação”. Isso configura o nó de computação Olá no nó do operador hello.
5. Utilitário de administração de saudação de saída.

### <a name="add-compute-nodes-details-on-web-node"></a>Adicionar detalhes de nós de computação no nó da Web

Depois que todos os nós de trabalho encerrado foram configurados toorun nó de computação, volte no nó de borda hello e adicionar endereços IP de nós de trabalho encerrado na configuração do nó de web do Microsoft R Server hello:

* SSH no nó de borda hello.
* Execute `vi /usr/lib64/microsoft-deployr/9.0.1/Microsoft.DeployR.Server.WebAPI/appsettings.json`.
* Procure Olá seção "URIs" e adicionar IP do nó do operador e detalhes de porta.

    ![encerrar nós de trabalho cmdline](./media/hdinsight-hadoop-r-server-get-started/get-started-op-cmd.png)


## <a name="troubleshoot"></a>Solucionar problemas

Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).


## <a name="next-steps"></a>Próximas etapas

Agora você deve entender como um novo cluster HDInsight que inclui as Noções básicas de R Server e hello de saudação do uso de toocreate Olá console de R em uma sessão SSH. Olá tópicos seguintes explicam outras maneiras de gerenciar e trabalhar com R Server no HDInsight:

* [Adicionar servidor RStudio tooHDInsight (se não é instalado durante a criação do cluster)](hdinsight-hadoop-r-server-install-r-studio.md)
* [Opções de contexto de computação para o Servidor R no HDInsight](hdinsight-hadoop-r-server-compute-contexts.md)
* [Opções de Armazenamento do Azure para o Servidor R no HDInsight](hdinsight-hadoop-r-server-storage.md)
