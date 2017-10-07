---
title: "desenvolvimento de ação aaaScript com HDInsight baseados em Linux - Azure | Microsoft Docs"
description: "Saiba como toouse Bash scripts toocustomize clusters de HDInsight baseados em Linux. recurso de ação de script de saudação do HDInsight permite que você toorun scripts durante ou após a criação do cluster. Scripts podem ser usado toochange definições de configuração de cluster ou instalar software adicional."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: cf4c89cd-f7da-4a10-857f-838004965d3e
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 1f504b00365df5f4cfb3ae19ad55ff7630342650
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="script-action-development-with-hdinsight"></a>Desenvolvimento de ação de script com o HDInsight

Saiba como toocustomize seu cluster HDInsight usando Bash scripts. Ações de script são uma maneira toocustomize HDInsight durante ou após a criação do cluster.

> [!IMPORTANT]
> etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux. Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior. Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="what-are-script-actions"></a>O que são ações de script

Ações de script são scripts de Bash Azure é executado em alterações de configuração toomake de nós de cluster hello ou instalam o software. Uma ação de script é executada como raiz e fornece nós de cluster toohello direitos de acesso completo.

Ações de script podem ser aplicadas por meio de saudação métodos a seguir:

| Use esse método tooapply um script... | Durante a criação do cluster... | Em um cluster em execução... |
| --- |:---:|:---:|
| Portal do Azure |✓  |✓ |
| Azure PowerShell |✓ |✓ |
| CLI do Azure |&nbsp; |✓ |
| SDK do .NET do HDInsight |✓ |✓ |
| Modelo do Azure Resource Manager |✓  |&nbsp; |

Para obter mais informações sobre como usar essas ações de script tooapply métodos, consulte [clusters de HDInsight personalizar usando ações de script](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="bestPracticeScripting"></a>Práticas recomendadas para o desenvolvimento de scripts

Quando você desenvolve um script personalizado para um cluster HDInsight, há vários tookeep práticas recomendadas em mente:

* [Versão do Hadoop de saudação de destino](#bPS1)
* [Olá, versão do sistema operacional de destino](#bps10)
* [Fornecer estável links tooscript recursos](#bPS2)
* [Usar os recursos pré-compilados](#bPS4)
* [Certifique-se de que o script de personalização de cluster Olá é idempotente](#bPS3)
* [Garantir a alta disponibilidade da arquitetura de cluster Olá](#bPS5)
* [Configurar o armazenamento de BLOBs do Azure em toouse Olá componentes personalizados](#bPS6)
* [Gravar informações tooSTDOUT e STDERR](#bPS7)
* [Salvar arquivos como ASCII com terminações de linha LF](#bps8)
* [Usar toorecover de lógica de repetição de erros transitórios](#bps9)

> [!IMPORTANT]
> Ações de script devem ser concluído dentro de 60 minutos ou Olá processo falhar. Durante o provisionamento de nó, o script hello é executado simultaneamente com outros processos de instalação e configuração. Competição por recursos, como largura de banda rede ou tempo de CPU pode provocar Olá script tootake mais toofinish do que no ambiente de desenvolvimento.

### <a name="bPS1"></a>Versão do Hadoop de saudação de destino

Diferentes versões do HDInsight têm diferentes versões de componentes e serviços do Hadoop instaladas. Se seu script espera uma versão específica de um serviço ou componente, você deve usar somente script hello com versão de saudação do HDInsight que inclui componentes de saudação necessária. Você pode encontrar informações sobre versões de componentes incluídos no HDInsight usando Olá [o controle de versão do HDInsight componente](hdinsight-component-versioning.md) documento.

### <a name="bps10"></a>Versão de hello sistema operacional de destino

HDInsight baseados em Linux baseia-se em Olá distribuição Ubuntu Linux. Versões diferentes do HDInsight contam com versões diferentes do Ubuntu, o que pode afetar o comportamento do seu script. Por exemplo, HDInsight 3.4 e versões mais recentes são baseados em versões do Ubuntu que usam o Upstart. A versão 3.5 baseia-se no Ubuntu 16.04, que usa Systemd. Systemd e Upstart dependem comandos diferentes, para que o script deve ser gravado toowork com ambos.

Outra diferença importante entre HDInsight 3.4 e 3.5 é que `JAVA_HOME` agora aponta tooJava 8.

Você pode verificar a versão de hello SO usando `lsb_release`. Olá código a seguir demonstra como toodetermine se hello script está em execução no Ubuntu 14 ou 16:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
...
if [[ $OS_VERSION == 16* ]]; then
    echo "Using systemd configuration"
    systemctl daemon-reload
    systemctl stop webwasb.service    
    systemctl start webwasb.service
else
    echo "Using upstart configuration"
    initctl reload-configuration
    stop webwasb
    start webwasb
fi
...
if [[ $OS_VERSION == 14* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-7-openjdk-amd64
elif [[ $OS_VERSION == 16* ]]; then
    export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
fi
```

Você pode encontrar o script hello completo contém estes trechos de código em https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh.

Para a versão de saudação do Ubuntu que é usado pelo HDInsight, consulte Olá [HDInsight a versão do componente](hdinsight-component-versioning.md) documento.

diferenças de saudação toounderstand entre Systemd e Upstart, consulte [Systemd para usuários Upstart](https://wiki.ubuntu.com/SystemdForUpstartUsers).

### <a name="bPS2"></a>Fornecer estável links tooscript recursos

Olá script e os recursos associados devem permanecer disponíveis durante o tempo de vida de saudação do cluster hello. Esses recursos são necessários se novos nós forem adicionados toohello cluster durante as operações de dimensionamento.

prática recomendada Olá é toodownload e arquivar tudo em uma conta de armazenamento do Azure em sua assinatura.

> [!IMPORTANT]
> conta de armazenamento Olá usada deve ser uma conta de armazenamento de padrão Olá para cluster de saudação ou um contêiner público, somente leitura em qualquer outra conta de armazenamento.

Por exemplo, os exemplos de saudação fornecidos pela Microsoft são armazenados em Olá [https://hdiconfigactions.blob.core.windows.net/](https://hdiconfigactions.blob.core.windows.net/) conta de armazenamento. Isso é um contêiner de público, somente leitura mantido pela equipe de HDInsight hello.

### <a name="bPS4"></a>Usar os recursos pré-compilados

Olá tooreduce tempo que demora toorun Olá script, evite operações que são compilados recursos do código-fonte. Por exemplo, pré-compilar recursos e armazená-las em um blob da conta de armazenamento do Azure no hello mesmo data center que HDInsight.

### <a name="bPS3"></a>Certifique-se de que o script de personalização de cluster Olá é idempotente

Os scripts devem ser idempotentes. Se o script hello será executado várias vezes, ele deverá retornar Olá toohello cluster mesmo estado de cada vez.

Por exemplo, um script que modifica os arquivos de configuração não deve adicionar entradas duplicadas se executado várias vezes.

### <a name="bPS5"></a>Garantir a alta disponibilidade da arquitetura de cluster Olá

Clusters de HDInsight baseados em Linux fornecem dois nós de cabeçalho que estão ativo no cluster hello e executar ações de script em ambos os nós. Se a instalação de componentes de saudação esperam apenas um nó principal, não instale os componentes de saudação em ambos os nós principal.

> [!IMPORTANT]
> Os serviços fornecidos como parte do HDInsight são toofail projetado através entre dois nós de cabeça Olá conforme necessário. Essa funcionalidade não é estendida toocustom componentes instalados por meio de ações de script. Se você precisar de alta disponibilidade para componentes personalizados, você deverá implementar seu próprio mecanismo de failover.

### <a name="bPS6"></a>Configurar o armazenamento de BLOBs do Azure em toouse Olá componentes personalizados

Componentes que você instalar no cluster Olá podem ter uma configuração padrão que usa o armazenamento do sistema de arquivos distribuído da Hadoop (HDFS). HDInsight usa o armazenamento do Azure ou repositório Data Lake como armazenamento de padrão de saudação. Oferecem um sistema de arquivos compatíveis do HDFS que persiste dados mesmo que o cluster Olá é excluído. Talvez seja necessário tooconfigure componentes instalar toouse WASB ou publicitário em vez de HDFS.

Para a maioria das operações, não é necessário toospecify sistema de arquivos de saudação. Por exemplo, seguinte Olá copia o arquivo de giraph examples.jar de saudação do armazenamento de toocluster do sistema de arquivos local hello:

```bash
hdfs dfs -put /usr/hdp/current/giraph/giraph-examples.jar /example/jars/
```

Neste exemplo, Olá `hdfs` comando transparentemente usa armazenamento de cluster saudação padrão. Para algumas operações, talvez seja necessário toospecify Olá URI. Por exemplo, `adl:///example/jars` para Data Lake Store ou `wasb:///example/jars` para o Armazenamento do Azure.

### <a name="bPS7"></a>Gravar informações tooSTDOUT e STDERR

HDInsight registra a saída do script é escrito tooSTDOUT e STDERR. Você pode exibir essas informações usando a interface da web hello Ambari.

> [!NOTE]
> Ambari só estará disponível se o cluster de saudação é criado com êxito. Se você usar uma ação de script durante a criação do cluster e falha de criação, consulte seção de solução de problemas de saudação [HDInsight personalizar clusters usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting) para outras maneiras de acessar as informações registradas.

A maioria dos pacotes de instalação e utilitários já gravam informações tooSTDOUT e STDERR, no entanto, convém tooadd adicionais de log. toosend texto tooSTDOUT, use `echo`. Por exemplo:

```bash
echo "Getting ready tooinstall Foo"
```

Por padrão, `echo` envia Olá tooSTDOUT de cadeia de caracteres. toodirect-tooSTDERR, adicionar `>&2` antes de `echo`. Por exemplo:

```bash
>&2 echo "An error occurred installing Foo"
```

Isso redirecionará informações gravadas tooSTDOUT tooSTDERR (2) em vez disso. Para obter mais informações sobre redirecionamento de E/S, consulte [http://www.tldp.org/LDP/abs/html/io-redirection.html](http://www.tldp.org/LDP/abs/html/io-redirection.html).

Para saber mais sobre exibição de informações registradas em log por ações de script, confira [Personalizar clusters HDInsight usando ação de script](hdinsight-hadoop-customize-cluster-linux.md#troubleshooting)

### <a name="bps8"></a> Salvar arquivos como ASCII com terminações de linha LF

Scripts de Bash devem ser armazenados com formato ASCII, com linhas terminadas em LF. Arquivos que são armazenados como UTF-8, ou usam CRLF como final de linha hello podem falhar com hello erro a seguir:

```
$'\r': command not found
line 1: #!/usr/bin/env: No such file or directory
```

### <a name="bps9"></a>Usar toorecover de lógica de repetição de erros transitórios

Ao fazer o download de arquivos, instalando os pacotes usando apt get ou outras ações que transmitem dados sobre Olá da internet, ação Olá pode falhar devido a erros de rede tootransient. Por exemplo, o recurso remoto hello, com que você está se comunicando pode ser no processo de saudação da falha ao nó de backup tooa.

toomake os erros do script tootransient resiliente, você pode implementar a lógica de repetição. saudação de função a seguir demonstra como tooimplement lógica de repetição. Tentar novamente a operação Olá três vezes antes de falhar.

```bash
#retry
MAXATTEMPTS=3

retry() {
    local -r CMD="$@"
    local -i ATTMEPTNUM=1
    local -i RETRYINTERVAL=2

    until $CMD
    do
        if (( ATTMEPTNUM == MAXATTEMPTS ))
        then
                echo "Attempt $ATTMEPTNUM failed. no more attempts left."
                return 1
        else
                echo "Attempt $ATTMEPTNUM failed! Retrying in $RETRYINTERVAL seconds..."
                sleep $(( RETRYINTERVAL ))
                ATTMEPTNUM=$ATTMEPTNUM+1
        fi
    done
}
```

Olá exemplos a seguir demonstram como toouse essa função.

```bash
retry ls -ltr foo

retry wget -O ./tmpfile.sh https://hdiconfigactions.blob.core.windows.net/linuxhueconfigactionv02/install-hue-uber-v02.sh
```

## <a name="helpermethods"></a>Métodos auxiliares para scripts personalizados

Os métodos auxiliares da Ação de Script são utilitários que podem ser usados durante a gravação de scripts personalizados. Esses métodos estão contidos no script [https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh](https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh). Use Olá toodownload a seguir e usá-los como parte do script:

```bash
# Import hello helper method module.
wget -O /tmp/HDInsightUtilities-v01.sh -q https://hdiconfigactions.blob.core.windows.net/linuxconfigactionmodulev01/HDInsightUtilities-v01.sh && source /tmp/HDInsightUtilities-v01.sh && rm -f /tmp/HDInsightUtilities-v01.sh
```

Olá auxiliares disponíveis para uso em seu script a seguir:

| Uso do auxiliar | Descrição |
| --- | --- |
| `download_file SOURCEURL DESTFILEPATH [OVERWRITE]` |Baixa um arquivo do caminho de arquivo especificado toohello do URI de origem hello. Por padrão, ele não substitui um arquivo existente. |
| `untar_file TARFILE DESTDIR` |Extrai um arquivo tar (usando `-xf`) toohello diretório de destino. |
| `test_is_headnode` |Se executado em um nó de cabeçalho do cluster, retorna 1. Caso contrário, 0. |
| `test_is_datanode` |Se o nó atual Olá for um nó de dados (trabalho), retornar um 1; Caso contrário, 0. |
| `test_is_first_datanode` |Se Olá atual é dados primeiro saudação (trabalho) nó (chamado workernode0) retornará 1; Caso contrário, 0. |
| `get_headnodes` |Retorne o nome de domínio totalmente qualificado de saudação do hello headnodes no cluster de saudação. Os nomes são delimitados por vírgula. Uma cadeia de caracteres vazia retorna em caso de erro. |
| `get_primary_headnode` |Obtém o nome de domínio totalmente qualificado de saudação do nó primário principal de saudação. Uma cadeia de caracteres vazia retorna em caso de erro. |
| `get_secondary_headnode` |Obtém o nome de domínio totalmente qualificado de saudação do nó secundário principal de saudação. Uma cadeia de caracteres vazia retorna em caso de erro. |
| `get_primary_headnode_number` |Obtém o sufixo numérico de saudação do nó primário principal de saudação. Uma cadeia de caracteres vazia retorna em caso de erro. |
| `get_secondary_headnode_number` |Obtém o sufixo numérico de saudação do nó secundário principal de saudação. Uma cadeia de caracteres vazia retorna em caso de erro. |

## <a name="commonusage"></a>Padrões comuns de uso

Esta seção fornece orientação sobre como implementar alguns Olá padrões comuns de uso que você pode encontrar ao gravar seu próprio script personalizado.

### <a name="passing-parameters-tooa-script"></a>Passando parâmetros de script tooa

Em alguns casos, seu script pode exigir parâmetros. Por exemplo, talvez seja necessário senha do administrador Olá para cluster Olá ao usar Olá API REST do Ambari.

Parâmetros passados toohello script são conhecidos como *parâmetros posicionais*e são atribuídos muito`$1` para o primeiro parâmetro de hello, `$2` para Olá segundo e portanto no. `$0`contém o nome de saudação do próprio script hello.

Os valores passados toohello script como parâmetros devem ser fechados por aspas simples ('). Isso garante que Olá passado valor é tratado como um literal.

### <a name="setting-environment-variables"></a>Configurando variáveis de ambiente

Definir uma variável de ambiente é executada por Olá instrução a seguir:

    VARIABLENAME=value

Onde o VARIABLENAME é o nome de saudação da variável de saudação. uso da variável, Olá tooaccess `$VARIABLENAME`. Por exemplo, tooassign um valor fornecido por um parâmetro posicional como uma variável de ambiente denominada senha, você usaria Olá instrução a seguir:

    PASSWORD=$1

Informações de toohello acesso subsequente podem usar `$PASSWORD`.

Variáveis de ambiente definida no script hello existem somente no escopo de saudação do script hello. Em alguns casos, talvez seja necessário variáveis de ambiente de todo o sistema de tooadd que serão mantido depois que o script hello terminou. variáveis de ambiente de todo o sistema tooadd, adicione a variável de saudação muito`/etc/environment`. Por exemplo, a saudação instrução a seguir adiciona `HADOOP_CONF_DIR`:

```bash
echo "HADOOP_CONF_DIR=/etc/hadoop/conf" | sudo tee -a /etc/environment
```

### <a name="access-toolocations-where-hello-custom-scripts-are-stored"></a>Acesso toolocations onde são armazenados os scripts personalizados Olá

Scripts usados toocustomize um cluster precisa toobe armazenado em uma saudação locais a seguir:

* Um __conta de armazenamento do Azure__ que está associado ao cluster hello.

* Um __conta de armazenamento adicional__ associada Olá cluster.

* Um URI __que pode ser lido publicamente__. Por exemplo, uma URL toodata armazenado no OneDrive, Dropbox ou outro arquivo de serviço de hospedagem.

* Um __conta do repositório Azure Data Lake__ que está associado ao cluster do HDInsight hello. Para obter mais informações sobre o uso do Azure Data Lake Store com o HDInsight, veja [Criar um cluster HDInsight com o Repositório Data Lake](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md).

    > [!NOTE]
    > Olá serviço principal HDInsight usa tooaccess repositório Data Lake deve ter acesso de leitura toohello script.

Recursos usados pelo script hello também devem estar publicamente disponíveis.

Armazenar arquivos de saudação em uma conta de armazenamento do Azure ou um repositório Azure Data Lake fornece acesso rápido, como ambos em Olá rede do Azure.

> [!NOTE]
> Olá URI formato usado tooreference Olá script difere dependendo de serviço hello está sendo usado. Para contas de armazenamento associadas com o cluster do HDInsight hello, use `wasb://` ou `wasbs://`. Para URIs lidas publicamente, use `http://` ou `https://`. Para Data Lake Store, use `adl://`.

### <a name="checking-hello-operating-system-version"></a>Verificando a versão do sistema operacional Olá

Versões diferentes do HDInsight contam com versões específicas do Ubuntu. Pode haver diferenças entre as versões de sistema operacional, que você deve verificar em seu script. Por exemplo, talvez seja necessário tooinstall um binário de versão associado toohello do Ubuntu.

toocheck Olá SO a versão `lsb_release`. Por exemplo, a saudação script a seguir demonstra como tooreference um tar específico de arquivo dependendo Olá versão do sistema operacional:

```bash
OS_VERSION=$(lsb_release -sr)
if [[ $OS_VERSION == 14* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-14-04."
    HUE_TARFILE=hue-binaries-14-04.tgz
elif [[ $OS_VERSION == 16* ]]; then
    echo "OS verion is $OS_VERSION. Using hue-binaries-16-04."
    HUE_TARFILE=hue-binaries-16-04.tgz
fi
```

## <a name="deployScript"></a>Lista de verificação para implantação de uma ação de script

Aqui estão as etapas Olá que demos ao preparar toodeploy esses scripts:

* Coloca os arquivos de saudação que contêm scripts personalizados de saudação em um local que seja acessível por nós de cluster Olá durante a implantação. Por exemplo, Olá armazenamento padrão para o cluster de saudação. Arquivos também podem ser armazenados nos serviços de hospedagem legíveis publicamente.
* Verifique se o script hello é impotent. Isso permite Olá script toobe executada várias vezes em Olá mesmo nó.
* Use uma saudação do arquivo temporário diretório /tmp tookeep baixado os arquivos usados pelos scripts de saudação e depois limpá-los depois de scripts foram executadas.
* Se as configurações de nível de sistema operacional ou arquivos de configuração do serviço de Hadoop forem alterados, convém toorestart HDInsight serviços.

## <a name="runScriptAction"></a>Como toorun uma ação de script

Você pode usar clusters de HDInsight do script ações toocustomize usando Olá métodos a seguir:

* Portal do Azure
* PowerShell do Azure
* Modelos do Gerenciador de Recursos do Azure
* Olá HDInsight .NET SDK.

Para obter mais informações sobre como usar cada método, consulte [como toouse scripts de ação](hdinsight-hadoop-customize-cluster-linux.md).

## <a name="sampleScripts"></a>Exemplos de script personalizado

Microsoft fornece scripts de exemplo tooinstall componentes em um cluster HDInsight. Consulte Olá links para mais ações de script de exemplo a seguir.

* [Instalar e usar o Hue em clusters HDInsight](hdinsight-hadoop-hue-linux.md)
* [Instalar e usar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install-linux.md)
* [Instalar e usar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md)
* [Instalar ou atualizar o Mono em clusters HDInsight](hdinsight-hadoop-install-mono.md)

## <a name="troubleshooting"></a>Solucionar problemas

Olá seguem erros que você pode encontrar ao usar scripts que você desenvolveu:

**Erro**: `$'\r': command not found`. Às vezes, seguido por `syntax error: unexpected end of file`.

*Causa*: este erro é causado quando terminam de linhas de saudação em um script com CRLF. Sistemas UNIX esperam LF apenas como final de linha de saudação.

Esse problema geralmente ocorre quando o script hello é criado em um ambiente do Windows, como CRLF é uma linha comum final para muitos editores de texto no Windows.

*Resolução*: se ela é uma opção em seu editor de texto, selecione o formato Unix ou LF para terminação de linha de saudação. Você também pode usar os comandos a seguir em uma instalação do Unix sistema toochange Olá CRLF tooan LF de saudação:

> [!NOTE]
> Olá comandos a seguir são equivalentes em que eles devem alterar tooLF de terminações de linha hello CRLF. Selecione uma opção com base em utilitários de saudação disponíveis no sistema.

| Command | Observações |
| --- | --- |
| `unix2dos -b INFILE` |arquivo original Olá é feito com um. Extensão BAK |
| `tr -d '\r' < INFILE > OUTFILE` |OUTFILE contém uma versão apenas com terminações LF |
| `perl -pi -e 's/\r\n/\n/g' INFILE` | Modifica o arquivo hello diretamente |
| ```sed 's/$'"/`echo \\\r`/" INFILE > OUTFILE``` |OUTFILE contém uma versão apenas com terminações LF. |

**Erro**: `line 1: #!/usr/bin/env: No such file or directory`.

*Causa*: este erro ocorre quando hello script foi salvo como UTF-8 com marca de ordem de um Byte (BOM).

*Resolução*: Olá de salvar arquivo como ASCII ou UTF-8 sem um BOM. Você também pode usar o hello comando a seguir em um toocreate de sistema Linux ou Unix um arquivo sem Olá BOM:

    awk 'NR==1{sub(/^\xef\xbb\xbf/,"")}{print}' INFILE > OUTFILE

Substituir `INFILE` com arquivo hello contendo Olá BOM. `OUTFILE`deve ser um novo nome de arquivo que contém o script hello sem Olá BOM.

## <a name="seeAlso"></a>Próximas etapas

* Saiba como muito[clusters de HDInsight personalizar usando a ação de script](hdinsight-hadoop-customize-cluster-linux.md)
* Saudação de uso [referência do HDInsight .NET SDK](https://msdn.microsoft.com/library/mt271028.aspx) toolearn mais sobre a criação de aplicativos .NET que gerenciar o HDInsight
* Saudação de uso [API REST do HDInsight](https://msdn.microsoft.com/library/azure/mt622197.aspx) toolearn como clusters de ações de gerenciamento de tooperform toouse REST no HDInsight.
