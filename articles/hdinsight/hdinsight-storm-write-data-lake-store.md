---
title: "aaaApache Storm gravar tooStorage/Data Lake repositório - HDInsight do Azure | Microsoft Docs"
description: "Saiba como toouse hello o armazenamento do Apache Storm toowrite toohello compatível com o HDFS para HDInsight. Azure Storage ou repositório Azure Data Lake fornecem armazenamento de saudação comptabile HDFS para HDInsight. Esse documento e exemplo de associado hello, demonstram como o componente de HdfsBolt Olá pode ser usados toowrite toohello padrão armazenamento de uma profusão de cluster HDInsight."
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a>Gravar tooHDFS do Apache Storm no HDInsight

Saiba como toouse Storm toowrite dados toohello armazenamento compatível com o HDFS usada pelo Apache Storm no HDInsight. O HDInsight pode usar o Armazenamento do Azure e o Azure Data Lake Store como armazenamento compatível com HDFS. Tempestade fornece um [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) componente que grava dados tooHDFS. Este documento fornece informações sobre como escrever tooeither tipo de armazenamento de saudação HdfsBolt. 

> [!IMPORTANT]
> exemplo Hello topologia usada neste documento depende de componentes que estão incluídos com Storm no HDInsight. Ele pode exigir a modificação toowork com o repositório do Azure Data Lake quando usado com outros clusters Apache Storm.

## <a name="get-hello-code"></a>Obter o código de saudação

projeto de saudação que contém essa topologia está disponível como um download do [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).

toocompile este projeto, você precisa Olá seguinte configuração para o seu ambiente de desenvolvimento:

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) ou superior. HDInsight 3.5 ou superior exige Java 8.

* [Maven 3.x](https://maven.apache.org/download.cgi)

Olá seguintes variáveis de ambiente podem ser definidas quando você instala o Java e hello JDK em sua estação de trabalho de desenvolvimento. No entanto, você deve verificar se eles existem e que eles contêm valores de saudação corretos para seu sistema.

* `JAVA_HOME`-deve apontar toohello diretório onde hello JDK está instalado.
* `PATH`-deve conter Olá caminhos a seguir:
  
    * `JAVA_HOME`(ou caminho equivalente Olá).
    * `JAVA_HOME\bin`(ou caminho equivalente Olá).
    * diretório de saudação onde Maven está instalado.

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a>Como toouse Olá HdfsBolt com HDInsight

> [!IMPORTANT]
> Antes de usar o hello HdfsBolt com Storm no HDInsight, primeiro você deve usar um arquivos jar de toocopy necessário de ação de script em Olá `extpath` para Storm. Para obter mais informações, consulte Olá [cluster de saudação configurar](#configure) seção.

Olá HdfsBolt usa o esquema de arquivo hello que você forneça toounderstand como toowrite tooHDFS. Com HDInsight, use um dos seguintes esquemas de saudação:

* `wasb://`: usado com uma conta de Armazenamento do Azure.
* `adl://`: usado com o Azure Data Lake Store.

Olá tabela a seguir fornece exemplos de como usar o esquema de arquivo hello para cenários diferentes:

| Esquema | Observações |
| ----- | ----- |
| `wasb:///` | conta de armazenamento padrão de saudação é um contêiner de blob em uma conta de armazenamento do Azure |
| `adl:///` | conta de armazenamento padrão de saudação é um diretório do repositório Azure Data Lake. Durante a criação do cluster, você especifica o diretório de saudação no repositório Data Lake que é a raiz de saudação do HDFS do cluster Olá. Por exemplo, Olá `/clusters/myclustername/` directory. |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | Uma conta de armazenamento do Azure (adicionais) não padrão associada Olá cluster. |
| `adl://STORENAME/` | raiz de saudação do hello repositório Data Lake usados pelo cluster hello. Esse esquema permite que dados tooaccess localizado fora do diretório de saudação que contém o sistema de arquivos de cluster de saudação. |

Para obter mais informações, consulte Olá [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) referência em Apache.org.

### <a name="example-configuration"></a>Exemplo de configuração

Olá, YAML seguinte é um trecho da saudação `resources/writetohdfs.yaml` arquivo incluído no exemplo hello. Esse arquivo define a topologia de profusão de saudação usando Olá [fluxo](https://storm.apache.org/releases/1.1.0/flux.html) framework para o Apache Storm.

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

Este YAML define Olá itens a seguir:

* `syncPolicy`: Define quando arquivos são sincronizados/liberado toohello sistema de arquivos. Neste exemplo, a cada 1.000 tuplas.
* `fileNameFormat`: Define toouse de padrão de nome de arquivo e caminho de saudação ao gravar os arquivos. Neste exemplo, o caminho de saudação é fornecido em tempo de execução usando um filtro e extensão de arquivo hello é `.txt`.
* `recordFormat`: Define o formato interno de saudação do hello arquivos gravados. Neste exemplo, os campos são delimitados por Olá `|` caracteres.
* `rotationPolicy`: Define quando toorotate arquivos. Neste exemplo, nenhuma rotação é executada.
* `hdfs-bolt`: Usa Olá componentes anteriores como parâmetros de configuração para Olá `HdfsBolt` classe.

Para obter mais informações sobre a estrutura do fluxo de hello, consulte [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="configure-hello-cluster"></a>Configurar o cluster Olá

Por padrão, Storm no HDInsight não incluir componentes Olá HdfsBolt usa toocommunicate com armazenamento do Azure ou repositório Data Lake no classpath do Storm. Script a seguir do uso Olá ação tooadd toohello esses componentes `extlib` diretório para Storm no cluster:

| URI de script | Nós tooapply a | Parâmetros | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisor | Nenhum |

Para obter informações sobre como usar esse script com o cluster, consulte Olá [clusters de HDInsight personalizar usando ações de script](./hdinsight-hadoop-customize-cluster-linux.md) documento.

## <a name="build-and-package-hello-topology"></a>Compile e empacote topologia Olá

1. Baixe o projeto de exemplo hello de [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour ambiente de desenvolvimento.

2. Em um prompt de comando, terminal ou sessão do shell, alterar diretórios toohello raiz de saudação baixou o projeto. toobuild e pacote hello topologia, use Olá comando a seguir:
   
        mvn compile package
   
    Após a conclusão do build hello e empacotamento, há um novo diretório chamado `target`, que contém um arquivo chamado `StormToHdfs-1.0-SNAPSHOT.jar`. Este arquivo contém a topologia de saudação compilada.

## <a name="deploy-and-run-hello-topology"></a>Implantar e executar topologia Olá

1. Use Olá cluster HDInsight toohello de topologia do comando toocopy Olá a seguir. Substituir **usuário** com nome de usuário SSH Olá usados ao criar o cluster de saudação. Substituir **CLUSTERNAME** com o nome de saudação do cluster hello.
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    Quando solicitado, insira a senha Olá usada ao criar usuário SSH Olá para cluster hello. Se você usou uma chave pública em vez de uma senha, talvez seja necessário Olá toouse `-i` parâmetro toospecify Olá caminho toohello correspondência de chave privada.
   
   > [!NOTE]
   > Para saber mais sobre como usar o `scp` com HDInsight, confira [Usar SSH com HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md).

2. Após a conclusão do carregamento de hello, use Olá tooconnect toohello HDInsight cluster usando o SSH a seguir. Substituir **usuário** com nome de usuário SSH Olá usados ao criar o cluster de saudação. Substituir **CLUSTERNAME** com o nome de saudação do cluster hello.
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    Quando solicitado, insira a senha Olá usada ao criar usuário SSH Olá para cluster hello. Se você usou uma chave pública em vez de uma senha, talvez seja necessário Olá toouse `-i` parâmetro toospecify Olá caminho toohello correspondência de chave privada.
   
   Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Uma vez conectado, use Olá comando a seguir toocreate um arquivo chamado `dev.properties`:

        nano dev.properties

4. Saudação de uso após o texto como conteúdo de saudação do hello `dev.properties` arquivo:

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > Este exemplo presume que o cluster usa uma conta de armazenamento do Azure como armazenamento de padrão de saudação. Se o cluster usar o Azure Data Lake Store, use `hdfs.url: adl:///`.
    
    arquivo de saudação toosave, use __Ctrl + X__, em seguida, __Y__e, finalmente, __Enter__. valores Hello neste arquivo definir URL de repositório Data Lake hello e o nome do diretório de saudação que dados são gravados.

3. Use Olá topologia de saudação do toostart de comando a seguir:
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    Esse comando inicia a topologia hello usando a estrutura de fluxo de saudação enviando-o nó de Nimbus toohello de cluster hello. topologia de saudação é definida por Olá `writetohdfs.yaml` arquivo incluído no jar hello. Olá `dev.properties` arquivo é passado como um filtro e valores hello contidos no arquivo hello são lidas por topologia hello.

## <a name="view-output-data"></a>Exibir dados de saída

dados de saudação tooview, use Olá comando a seguir:

    hdfs dfs -ls /stormdata/

Uma lista de arquivos de saudação criados por essa topologia é exibida.

Olá lista a seguir é um exemplo de dados Olá reajustados por comandos anteriores hello:

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a>Parar a topologia de saudação

Topologias Storm executar até ser interrompido ou Olá cluster é excluído. toostop Olá topologia, use Olá comando a seguir:

    storm kill hdfswriter

## <a name="delete-your-cluster"></a>Excluir o cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Próximas etapas

Agora que você aprendeu como toouse Storm toowrite tooAzure armazenamento e repositório Azure Data Lake, descobrir outros [profusão de exemplos para HDInsight](hdinsight-storm-example-topology.md).

