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
# <a name="query-hive-through-hello-jdbc-driver-in-hdinsight"></a>Consulta de Hive por meio do driver JDBC Olá no HDInsight

[!INCLUDE [ODBC-JDBC-selector](../../includes/hdinsight-selector-odbc-jdbc.md)]

Saiba como o JDBC driver toouse Olá de um aplicativo de Java toosubmit Hive consultas tooHadoop no Azure HDInsight. informações de saudação neste documento demonstra como tooconnect programaticamente e da saudação esquilo SQL client.

Para obter mais informações sobre Olá Hive JDBC Interface, consulte [HiveJDBCInterface](https://cwiki.apache.org/confluence/display/Hive/HiveJDBCInterface).

## <a name="prerequisites"></a>Pré-requisitos

* Um Hadoop no cluster do HDInsight. Tanto clusters baseados em Linux quanto em Windows funcionarão.

  > [!IMPORTANT]
  > Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [HDInsight 3.3 retirement](hdinsight-component-versioning.md#hdinsight-windows-retirement) (Desativação do HDInsight 3.3).

* [SQuirreL SQL](http://squirrel-sql.sourceforge.net/). O SQuirreL é um aplicativo cliente JDBC.

* Olá [Java Developer Kit (JDK) versão 7](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior.

* [Apache Maven](https://maven.apache.org). Maven é um projeto de criar o sistema para projetos Java que é usado pelo projeto Olá associado a este artigo.

## <a name="jdbc-connection-string"></a>Cadeia de conexão JDBC

Cluster do HDInsight tooan JDBC conexões no Azure são feitas em 443 e tráfego de saudação é protegido usando SSL. gateway Olá pública clusters Olá ficam atrás redireciona toohello porta Olá tráfego HiveServer2 realmente está escutando. a seguir Olá é uma cadeia de caracteres de conexão de exemplo:

    jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

Substituir `CLUSTERNAME` com nome de saudação do cluster HDInsight.

## <a name="authentication"></a>Autenticação

Ao estabelecer conexão hello, você deve usar o hello HDInsight cluster admin nome e senha tooauthenticate toohello cluster gateway. Durante a conexão de clientes do JDBC, como esquilo SQL, você deve inserir nome de saudação do administrador e a senha nas configurações do cliente.

Em um aplicativo Java, você deve usar o hello nome e senha ao estabelecer uma conexão. Por exemplo, hello código Java a seguir abre uma nova conexão usando a cadeia de caracteres de conexão Olá, nome do administrador e senha:

```java
DriverManager.getConnection(connectionString,clusterAdmin,clusterPassword);
```

## <a name="connect-with-squirrel-sql-client"></a>Conectar-se ao cliente do SQuirreL SQL

Esquilo SQL é um cliente JDBC que pode ser usados tooremotely executar consultas de Hive com seu cluster HDInsight. Olá etapas a seguir pressupõem que você já instalou esquilo SQL.

1. Copie os drivers de JDBC Hive de saudação do seu cluster HDInsight.

    * Para **HDInsight baseados em Linux**, arquivos jar da saudação necessário toodownload as etapas a seguir do uso hello.

        1. Crie um diretório que contém arquivos de saudação. Por exemplo: `mkdir hivedriver`.

        2. Em uma linha de comando, use a seguir Olá comandos toocopy arquivos de saudação do cluster do HDInsight hello:

            ```bash
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/hive-jdbc*standalone.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-common.jar .
            scp USERNAME@CLUSTERNAME:/usr/hdp/current/hadoop-client/hadoop-auth.jar .
            ```

            Substituir `USERNAME` com o nome da conta de usuário Olá SSH para cluster hello. Substituir `CLUSTERNAME` com o nome do cluster HDInsight hello.

    * Para **HDInsight baseados em Windows**, arquivos jar do toodownload Olá as etapas a seguir de saudação do uso.

        1. De Olá portal do Azure, selecione seu cluster HDInsight e selecione Olá **área de trabalho remota** ícone.

            ![Ícone da Área de Trabalho Remota](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopicon.png)

        2. Na folha de área de trabalho remota hello, use Olá **conectar** cluster do botão tooconnect toohello. Se Olá área de trabalho remota não está habilitado, use Olá formulário tooprovide um nome de usuário e senha e selecione **habilitar** tooenable área de trabalho remota para o cluster de saudação.

            ![Folha Área de Trabalho Remota](./media/hdinsight-connect-hive-jdbc-driver/remotedesktopblade.png)

            Depois de selecionar **Conectar**, um arquivo .rdp será baixado. Use esse cliente de área de trabalho remota do arquivo toolaunch hello. Quando solicitado, use o nome de usuário de saudação e senha que você digitou para o acesso de área de trabalho remota.

        3. Uma vez conectado, copie Olá seguintes arquivos da máquina local de tooyour Olá de sessão área de trabalho remota. Coloque-os em um diretório local chamado `hivedriver`.

            * C:\apps\dist\hive-0.14.0.2.2.9.1-7\lib\hive-jdbc-0.14.0.2.2.9.1-7-standalone.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\hadoop-common-2.6.0.2.2.9.1-7.jar
            * C:\apps\dist\hadoop-2.6.0.2.2.9.1-7\share\hadoop\common\lib\hadoop-auth-2.6.0.2.2.9.1-7.jar

            > [!NOTE]
            > versão de Hello números incluídos nos nomes de arquivo e caminhos de saudação podem ser diferentes para seu cluster.

        4. Desconecte a sessão de área de trabalho remota Olá depois de terminar de copiar arquivos de saudação.

2. Inicie aplicativo do SQL esquilo hello. Da esquerda de saudação da janela hello, selecione **Drivers**.

    ![Guia drivers saudação à esquerda da janela de saudação](./media/hdinsight-connect-hive-jdbc-driver/squirreldrivers.png)

3. Dos demais ícones na parte superior de saudação do Olá Olá **Drivers** caixa de diálogo, selecione Olá  **+**  toocreate ícone um driver.

    ![Ícones de Drivers](./media/hdinsight-connect-hive-jdbc-driver/driversicons.png)

4. Na caixa de diálogo de Adicionar Driver hello, adicione Olá informações a seguir:

    * **Nome**: Hive
    * **Exemplo de URL**: `jdbc:hive2://localhost:443/default;transportMode=http;ssl=true;httpPath=/hive2`
    * **Caminho de classe extra**: usar Olá adicionar botão tooadd Olá jar arquivos baixados anteriormente
    * **Nome de Classe**: org.apache.hive.jdbc.HiveDriver

   ![diálogo adicionar driver](./media/hdinsight-connect-hive-jdbc-driver/adddriver.png)

   Clique em **Okey** toosave essas configurações.

5. Esquerda de saudação da janela de SQL esquilo hello, selecione **Aliases**. Em seguida, clique em Olá  **+**  toocreate ícone um alias de conexão.

    ![adicionar novo alias](./media/hdinsight-connect-hive-jdbc-driver/aliases.png)

6. A seguir Olá Use valores de saudação **adicionar Alias** caixa de diálogo.

    * **Nome**: Hive no HDInsight

    * **Driver**: Use Olá suspensa tooselect Olá **Hive** driver

    * **URL**: jdbc:hive2://CLUSTERNAME.azurehdinsight.net:443/default;transportMode=http;ssl=true;httpPath=/hive2

        Substituir **CLUSTERNAME** com nome de saudação do cluster HDInsight.

    * **Nome de usuário**: nome da conta de logon Olá cluster para seu cluster HDInsight. saudação padrão é `admin`.

    * **Senha**: senha Olá Olá cluster conta de logon.

 ![diálogo adicionar alias](./media/hdinsight-connect-hive-jdbc-driver/addalias.png)

    Saudação de uso **teste** tooverify botão que Olá conexão funciona. Quando **conectem: Hive no HDInsight** caixa de diálogo é exibida, selecione **conectar** tooperform teste de saudação. Se o teste de saudação for bem-sucedida, você verá um **Conexão bem-sucedida** caixa de diálogo.

    conexão de saudação toosave alias, use Olá **Okey** botão na parte inferior de saudação do hello **adicionar Alias** caixa de diálogo.

7. De saudação **se conectem** selecione da lista suspensa na parte superior de saudação do SQL esquilo, **Hive no HDInsight**. Quando solicitado, selecione **Conectar**.

    ![diálogo conexão](./media/hdinsight-connect-hive-jdbc-driver/connect.png)

8. Uma vez conectado, digite Olá seguinte consulta na caixa de diálogo de consulta SQL hello e selecione Olá **executar** ícone. Olá resultados área deve mostrar resultados de saudação de consulta de saudação.

        select * from hivesampletable limit 10;

    ![diálogo consulta sql, incluindo os resultados](./media/hdinsight-connect-hive-jdbc-driver/sqlquery.png)

## <a name="connect-from-an-example-java-application"></a>Conectar-se de um aplicativo Java de exemplo

Um exemplo de como usar um cliente de Java tooquery Hive no HDInsight está disponível em [https://github.com/Azure-Samples/hdinsight-java-hive-jdbc](https://github.com/Azure-Samples/hdinsight-java-hive-jdbc). Siga as instruções de Olá Olá repositório toobuild e executar o exemplo hello.

## <a name="troubleshooting"></a>Solucionar problemas

### <a name="unexpected-error-occurred-attempting-tooopen-an-sql-connection"></a>Erro inesperado ocorreu tooopen tentando uma conexão de SQL

**Sintomas**: ao conectar o cluster HDInsight tooan versão 3.3 ou 3.4, você poderá receber um erro que ocorreu um erro inesperado. rastreamento de pilha Olá para esse erro começa com hello linhas seguintes:

```java
java.util.concurrent.ExecutionException: java.lang.RuntimeException: java.lang.NoSuchMethodError: org.apache.commons.codec.binary.Base64.<init>(I)V
at java.util.concurrent.FutureTas...(FutureTask.java:122)
at java.util.concurrent.FutureTask.get(FutureTask.java:206)
```

**Causa**: este erro é causado por uma incompatibilidade de versão de saudação do hello commons codec.jar arquivo usado pelo esquilo e hello exigido pelos componentes do Hive JDBC hello.

**Resolução**: toofix esse erro, use Olá seguindo as etapas:

1. Baixe o arquivo de jar de codec commons de saudação do seu cluster HDInsight.

        scp USERNAME@CLUSTERNAME:/usr/hdp/current/hive-client/lib/commons-codec*.jar ./commons-codec.jar

2. Sair esquilo e, em seguida, vá toohello diretório onde esquilo está instalado no seu sistema. No diretório de esquilo hello, sob Olá `lib` diretório, substituir Olá existente commons-codec.jar com hello um baixado do cluster do HDInsight hello.

3. Reinicie o SQuirreL. Erro de saudação não deve ocorrer durante a conexão tooHive no HDInsight.

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como toouse JDBC toowork com Hive, Olá uso a seguir vincula tooexplore toowork outras formas ao HDInsight do Azure.

* [Carregar dados tooHDInsight](hdinsight-upload-data.md)
* [Usar o Hive com o HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com o HDInsight](hdinsight-use-pig.md)
* [Usar trabalhos do MapReduce com o HDInsight](hdinsight-use-mapreduce.md)
