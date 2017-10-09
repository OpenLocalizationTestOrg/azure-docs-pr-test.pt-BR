---
title: aaaPython UDF com o Apache Hive e Pig - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse Python definida pelo usuário funções (UDF) de Hive e Pig no HDInsight, Olá Hadoop tecnologia de pilha no Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: c44d6606-28cd-429b-b535-235e8f34a664
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 07/17/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 26d8160cc6ed7fc22c3f06f7c1c9954c224b2366
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a>Usar as UDF (Funções Definidas pelo Usuário) do Python com o Hive e o Pig no HDInsight

Saiba como toouse Python definido pelo usuário (UDF) de funções com o Apache Hive e Pig no Hadoop no HDInsight do Azure.

## <a name="python"></a>Python no HDInsight

O Python 2.7 é instalado por padrão no HDInsight 3.0 e posteriores. O Apache Hive pode ser usado com essa versão do Python para processamento de fluxo. Processamento de fluxo usa STDOUT e STDIN dados toopass entre Hive e hello UDF.

O HDInsight também inclui o Jython, que é uma implementação do Python gravada em Java. Jython é executado diretamente na máquina Virtual Java de saudação e não usarem o fluxo. Jython é Olá recomendada intérprete Python com Python Pig.

> [!WARNING]
> etapas de saudação neste documento fazem Olá seguintes suposições: 
>
> * Você cria Olá scripts Python em seu ambiente de desenvolvimento local.
> * Carregar Olá scripts tooHDInsight usando qualquer Olá `scp` comando de uma sessão de Bash local ou Olá fornecido script do PowerShell.
>
> Se você quiser Olá toouse [Shell de nuvem do Azure (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) visualizar toowork com HDInsight, em seguida, você deve:
>
> * Crie scripts de saudação dentro do ambiente de shell Olá nuvem.
> * Use `scp` arquivos tooupload Olá Olá nuvem tooHDInsight de shell.
> * Use `ssh` de saudação nuvem shell tooconnect tooHDInsight e exemplos de execução hello.

## <a name="hivepython"></a>UDF do Hive

Python pode ser usado como uma UDF de Hive por meio de saudação HiveQL `TRANSFORM` instrução. Por exemplo, Olá HiveQL a seguir invoca Olá `hiveudf.py` arquivo armazenado na conta de armazenamento do Azure saudação padrão para o cluster de saudação.

**HDInsight baseado em Linux**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

**HDInsight baseado em Windows**

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> Em clusters HDInsight baseados no Windows, Olá `USING` cláusula deve especificar Olá caminho completo toopython.exe.

Aqui está o que este exemplo faz:

1. Olá `add file` instrução no início de saudação do arquivo hello adiciona Olá `hiveudf.py` toohello de arquivo distribuído cache, para que ela é acessível por todos os nós no cluster de saudação.
2. Olá `SELECT TRANSFORM ... USING` instrução seleciona dados da saudação `hivesampletable`. Também passa clientid hello, devicemake e devicemodel valores toohello `hiveudf.py` script.
3. Olá `AS` cláusula descreve campos Olá retornados de `hiveudf.py`.

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a>Criar arquivo de hiveudf.py Olá


Em seu ambiente de desenvolvimento, crie um arquivo de texto chamado `hiveudf.py`. Use Olá código a seguir como conteúdo de saudação do arquivo hello:

```python
#!/usr/bin/env python
import sys
import string
import hashlib

while True:
    line = sys.stdin.readline()
    if not line:
        break

    line = string.strip(line, "\n ")
    clientid, devicemake, devicemodel = string.split(line, "\t")
    phone_label = devicemake + ' ' + devicemodel
    print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])
```

Esse script executa Olá ações a seguir:

1. Ler uma linha de dados do STDIN.
2. Olá caractere de nova linha à direita é removido usando `string.strip(line, "\n ")`.
3. Ao fazer o processamento de fluxo, uma única linha contém todos os valores de saudação com um caractere de tabulação entre cada valor. Portanto `string.split(line, "\t")` pode ser usado toosplit Olá entrada em cada guia, retornando apenas campos de saudação.
4. Quando o processamento for concluído, saída de hello deve ser escrita tooSTDOUT como uma única linha, com uma guia entre cada campo. Por exemplo: `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.
5. Olá `while` loop é repetido até que não `line` é lido.

saída do script Hello é uma concatenação dos valores de entrada hello para `devicemake` e `devicemodel`, e o valor de hash de saudação concatenado.

Consulte [executando exemplos Olá](#running) como toorun Este exemplo em seu cluster HDInsight.

## <a name="pigpython"></a>UDF do Pig

Um script Python pode ser usado como uma UDF de Pig por meio de saudação `GENERATE` instrução. Você pode executar o script hello usando Jython ou Python C.

* Jython é executado em Olá da JVM e nativamente pode ser chamado do Pig.
* Python C é um processo externo, para que dados de saudação do Pig em Olá JVM é enviada toohello script em execução em um processo de Python. saída Olá Olá script Python é enviada para o Pig.

intérprete de Python Olá toospecify, use `register` ao referenciar o script de Python hello. Olá exemplos a seguir registrar scripts com Pig como `myfuncs`:

* **toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`
* **toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`

> [!IMPORTANT]
> Ao usar Jython, Olá caminho toohello pig_jython arquivo pode ser um caminho local ou um WASB: / / caminho. No entanto, ao usar o Python C, você deve fazer referência a um arquivo no sistema de arquivos local de saudação do nó de saudação que você está usando o trabalho de Pig toosubmit hello.

Após após o registro, Olá latino Pig para este exemplo hello mesmo para ambos:

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

Aqui está o que este exemplo faz:

1. Olá primeira linha carrega o arquivo de dados de exemplo hello, `sample.log` em `LOGS`. Também define cada registro como `chararray`.
2. linha seguinte Olá filtra quaisquer valores nulos, armazenando Olá resultado da operação de saudação em `LOG`.
3. Em seguida, ele é iterado sobre registros Olá `LOG` e usa `GENERATE` tooinvoke Olá `create_structure` método contido no script de Python/Jython Olá carregado como `myfuncs`. `LINE`é usado toopass função toohello registro atual de saudação.
4. Por fim, Olá saídas são tooSTDOUT despejada usando Olá `DUMP` comando. Este comando exibe os resultados de saudação após a conclusão da operação de saudação.

### <a name="create-hello-pigudfpy-file"></a>Criar arquivo de pigudf.py Olá

Em seu ambiente de desenvolvimento, crie um arquivo de texto chamado `pigudf.py`. Use Olá código a seguir como conteúdo de saudação do arquivo hello:

<a name="streamingpy"></a>

```python
# Uncomment hello following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

No exemplo de Pig latino hello, definimos Olá `LINE` de entrada como um chararray porque não há nenhum esquema consistente para entrada hello. Olá script Python transforma dados de saudação em um esquema consistente para saída.

1. Olá `@outputSchema` instrução define o formato de saudação de dados Olá tooPig retornado. Nesse caso, é uma **mala de dados**, que é um tipo de dado do Pig. recipiente Olá contém Olá campos, que são chararray (cadeias de caracteres) a seguir:

   * Data - Olá data Olá entrada de log foi criada
   * hora - Olá Olá entrada de log foi criada
   * nome da classe - entrada de saudação do nome de classe Olá foi criado para
   * nível - Olá log
   * detalhe - entrada de log detalhado para Olá

2. Em seguida, Olá `def create_structure(input)` define a função hello Pig passa itens de linha.

3. Olá dados de exemplo, `sample.log`, principalmente em conformidade toohello data, hora, classname, nível e detalhes de esquema que desejamos tooreturn. No entanto, contêm algumas linhas que começam com `*java.lang.Exception*`. Essas linhas devem ter um esquema de saudação toomatch modificado. Olá `if` instrução verifica para aqueles que, em seguida, Massagens Olá Olá de toomove de dados de entrada `*java.lang.Exception*` final de toohello de cadeia de caracteres, colocando Olá em linha com nosso esquema de saída esperada.

4. Em seguida, Olá `split` comando é toosplit usados dados Olá Olá primeiro quatro espaços. saída de Hello é atribuída em `date`, `time`, `classname`, `level`, e `detail`.

5. Por fim, os valores de saudação são retornados tooPig.

Quando dados saudação são retornados tooPig, tem um esquema consistente conforme definido no hello `@outputSchema` instrução.

## <a name="running"></a>Carregar e executar os exemplos de saudação

> [!IMPORTANT]
> Olá **SSH** etapas funcionam apenas com um cluster HDInsight baseados em Linux. Olá **PowerShell** etapas funcionam com cluster um HDInsight baseados em Windows ou Linux, mas requer um cliente do Windows.

### <a name="ssh"></a>SSH

Para saber mais sobre como usar SSH, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

1. Use `scp` cluster HDInsight do toocopy Olá arquivos tooyour. Por exemplo, Olá cópias Olá cluster tooa de arquivos chamado de comando a seguir **mycluster**.

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. Use SSH tooconnect toohello cluster.

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. Da sessão SSH hello, adicione arquivos de python Olá carregado anteriormente toohello armazenamento WASB cluster hello.

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

Depois de carregar arquivos hello, use Olá etapas a seguir toorun Olá Hive e trabalhos de Pig.

#### <a name="use-hello-hive-udf"></a>Use Olá Hive UDF

1. Saudação de uso `hive` toostart Olá hive shell de comando. Você deve ver uma `hive>` solicitar depois Olá shell foi carregado.

2. Digite Olá a seguinte consulta no hello `hive>` prompt:

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. Depois de inserir a última linha do hello, trabalho Olá deve começar. Após a conclusão do trabalho Olá, ele retorna a saída toohello semelhante exemplo a seguir:

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a>Use Olá UDF Pig

1. Saudação de uso `pig` toostart Olá shell de comando. Você verá um `grunt>` solicitar depois Olá shell foi carregado.

2. Digite hello seguindo as instruções no hello `grunt>` prompt:

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. Depois de inserir Olá linha a seguir, o trabalho de saudação deve começar. Após a conclusão do trabalho hello, ele retorna toohello semelhante de saída seguintes dados:

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. Use `quit` tooexit Olá shell pesado e use Olá seguir tooedit Olá pigudf.py arquivo no sistema de arquivos local hello:

    ```bash
    nano pigudf.py
    ```

5. Uma vez no editor de hello, remova os comentários Olá seguinte linha removendo Olá `#` caracteres do início de saudação da linha de saudação:

    ```bash
    #from pig_util import outputSchema
    ```

    Depois de alterar Olá, use o editor de saudação de tooexit de Ctrl + X. Selecione Y e, em seguida, insira as alterações de saudação toosave.

6. Saudação de uso `pig` comando shell de saudação toostart novamente. Quando você chega a saudação `grunt>` prompt, use Olá script em Python usando o interpretador do Python C Olá Olá toorun a seguir.

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    Quando esta tarefa for concluída, você deverá ver Olá mesmo saído como quando você executou anteriormente script hello usando Jython.

### <a name="powershell-upload-hello-files"></a>PowerShell: Arquivos de saudação de carregamento

Você pode usar o servidor do PowerShell tooupload Olá arquivos toohello HDInsight. Use Olá arquivos de script de tooupload Olá Python a seguir:

> [!IMPORTANT] 
> Olá etapas desta seção usam PowerShell do Azure. Para obter mais informações sobre como usar o PowerShell do Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
# Change hello path toomatch hello file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

Set-AzureStorageBlobContent `
    -File $pathToStreamingFile `
    -Blob "hiveudf.py" `
    -Container $container `
    -Context $context

Set-AzureStorageBlobContent `
    -File $pathToJythonFile `
    -Blob "pigudf.py" `
    -Container $container `
    -Context $context
```
> [!IMPORTANT]
> Saudação de alteração `C:\path\to` valor toohello arquivos de toohello de caminho em seu ambiente de desenvolvimento.

Este script recupera as informações de seu cluster HDInsight, em seguida, extrai conta hello e chave de conta de armazenamento padrão hello e carregamentos Olá raiz toohello de arquivos do contêiner de saudação.

> [!NOTE]
> Para obter mais informações sobre como carregar arquivos, consulte Olá [carregar dados para trabalhos de Hadoop no HDInsight](hdinsight-upload-data.md) documento.

#### <a name="powershell-use-hello-hive-udf"></a>PowerShell: Saudação de uso Hive UDF

PowerShell também pode ser usado tooremotely executar consultas de Hive. Saudação de uso toorun de script do PowerShell uma consulta de Hive que usa a seguir **hiveudf.py** script:

> [!IMPORTANT]
> Antes de executar, script hello solicita Olá HTTPs/Admin informações da conta para seu cluster HDInsight.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

# If using a Windows-based HDInsight cluster, change hello USING statement to:
# "USING 'D:\Python27\python.exe hiveudf.py' AS " +
$HiveQuery = "add file wasb:///hiveudf.py;" +
                "SELECT TRANSFORM (clientid, devicemake, devicemodel) " +
                "USING 'python hiveudf.py' AS " +
                "(clientid string, phoneLabel string, phoneHash string) " +
                "FROM hivesampletable " +
                "ORDER BY clientid LIMIT 50;"

$jobDefinition = New-AzureRmHDInsightHiveJobDefinition `
    -Query $HiveQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds
Write-Host "Wait for hello Hive job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

Olá saída Olá **Hive** trabalho deve aparecer semelhante toohello exemplo a seguir:

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a>Pig (Jython)

PowerShell também pode ser usado toorun Pig latino trabalhos. toorun um trabalho de Pig latino que usa Olá **pigudf.py** de script, use Olá script do PowerShell a seguir:

> [!NOTE]
> Durante o envio de um trabalho usando o PowerShell remotamente, não é possível toouse Python C como interpretador hello.

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

$PigQuery = "Register wasb:///pigudf.py using jython as myfuncs;" +
            "LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);" +
            "LOG = FILTER LOGS by LINE is not null;" +
            "DETAILS = foreach LOG generate myfuncs.create_structure(LINE);" +
            "DUMP DETAILS;"

$jobDefinition = New-AzureRmHDInsightPigJobDefinition -Query $PigQuery

$job = Start-AzureRmHDInsightJob `
    -ClusterName $clusterName `
    -JobDefinition $jobDefinition `
    -HttpCredential $creds

Write-Host "Wait for hello Pig job toocomplete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment hello following toosee stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

Olá saída Olá **Pig** trabalho deve aparecer semelhante toohello seguintes dados:

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <a name="troubleshooting"></a>Solucionar problemas

### <a name="errors-when-running-jobs"></a>Erros durante a execução de trabalhos

Ao executar o trabalho de hive hello, você pode encontrar um toohello semelhante erro texto a seguir:

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

Esse problema pode ser causado por terminações de linha de saudação no arquivo de Python hello. Muitos editores de Windows padrão toousing CRLF como linha hello final, mas aplicativos Linux normalmente esperam LF.

Você pode usar o hello PowerShell instruções tooremove Olá CR caracteres à direita antes de carregar Olá arquivo tooHDInsight:

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a>Scripts do PowerShell

Exemplo hello scripts do PowerShell usados toorun exemplos de saudação conter uma linha comentada que exibe a saída de erro para o trabalho de saudação. Se você não estiver vendo saída Olá esperado para o trabalho de hello, remova os comentários a seguir Olá linha e ver se as informações de erro de saudação indicam um problema.

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

informações de erro da saudação (STDERR) e o resultado de saudação do trabalho de saudação (STDOUT) também são registrados tooyour HDInsight armazenamento.

| Para este trabalho… | Examinar esses arquivos no contêiner de blob Olá |
| --- | --- |
| Hive |/HivePython/stderr<p>/HivePython/stdout |
| Pig |/PigPython/stderr<p>/PigPython/stdout |

## <a name="next"></a>Próximas etapas

Se você precisar de módulos de Python tooload que não são fornecidos por padrão, consulte [como toodeploy tooAzure um módulo HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).

Para outras maneiras toouse Pig, Hive e toolearn sobre o uso de MapReduce, consulte Olá documentos a seguir:

* [Usar o Hive com o HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com o HDInsight](hdinsight-use-pig.md)
* [Usar o MapReduce com o HDInsight](hdinsight-use-mapreduce.md)
