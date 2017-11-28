---
title: "Python UDF com Apache Hive e Pig – HDInsight do Azure | Microsoft Docs"
description: "Saiba como usar UDFs (Funções Definidas pelo Usuário) do Python com o Hive e o Pig no HDInsight, a pilha de tecnologias do Hadoop no Azure."
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
ms.openlocfilehash: 9b67ded05a52f1e68580434667495cf6cf939871
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="406f2-103">Usar as UDF (Funções Definidas pelo Usuário) do Python com o Hive e o Pig no HDInsight</span><span class="sxs-lookup"><span data-stu-id="406f2-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="406f2-104">Saiba como usar funções definidas pelo usuário do Python (UDF) com o Apache Hive e o Pig no Hadoop no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="406f2-104">Learn how to use Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="406f2-105"><a name="python"></a>Python no HDInsight</span><span class="sxs-lookup"><span data-stu-id="406f2-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="406f2-106">O Python 2.7 é instalado por padrão no HDInsight 3.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="406f2-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="406f2-107">O Apache Hive pode ser usado com essa versão do Python para processamento de fluxo.</span><span class="sxs-lookup"><span data-stu-id="406f2-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="406f2-108">O processamento de fluxo usa STDOUT e STDIN para enviar dados entre o Hive e o UDF.</span><span class="sxs-lookup"><span data-stu-id="406f2-108">Stream processing uses STDOUT and STDIN to pass data between Hive and the UDF.</span></span>

<span data-ttu-id="406f2-109">O HDInsight também inclui o Jython, que é uma implementação do Python gravada em Java.</span><span class="sxs-lookup"><span data-stu-id="406f2-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="406f2-110">Jython é executado diretamente na Máquina Virtual Java e não usa streaming.</span><span class="sxs-lookup"><span data-stu-id="406f2-110">Jython runs directly on the Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="406f2-111">Jython é o interpretador do Python recomendado ao usar Python com Pig.</span><span class="sxs-lookup"><span data-stu-id="406f2-111">Jython is the recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="406f2-112">As etapas neste documento fazem as seguintes suposições:</span><span class="sxs-lookup"><span data-stu-id="406f2-112">The steps in this document make the following assumptions:</span></span> 
>
> * <span data-ttu-id="406f2-113">Você cria scripts Python em seu ambiente de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="406f2-113">You create the Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="406f2-114">Você carregar os scripts para o HDInsight usando o comando `scp` de uma sessão de Bash local ou o script do PowerShell fornecido.</span><span class="sxs-lookup"><span data-stu-id="406f2-114">You upload the scripts to HDInsight using either the `scp` command from a local Bash session or the provided PowerShell script.</span></span>
>
> <span data-ttu-id="406f2-115">Se você quiser usar a versão prévia do [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) para trabalhar com o HDInsight, você deverá:</span><span class="sxs-lookup"><span data-stu-id="406f2-115">If you want to use the [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview to work with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="406f2-116">Criar os scripts de dentro do ambiente do Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="406f2-116">Create the scripts inside the cloud shell environment.</span></span>
> * <span data-ttu-id="406f2-117">Usar `scp` para carregar os arquivos do Cloud Shell para o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="406f2-117">Use `scp` to upload the files from the cloud shell to HDInsight.</span></span>
> * <span data-ttu-id="406f2-118">Usar `ssh` do Cloud Shell para conectar-se ao HDInsight e executar os exemplos.</span><span class="sxs-lookup"><span data-stu-id="406f2-118">Use `ssh` from the cloud shell to connect to HDInsight and run the examples.</span></span>

## <span data-ttu-id="406f2-119"><a name="hivepython"></a>UDF do Hive</span><span class="sxs-lookup"><span data-stu-id="406f2-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="406f2-120">O Python pode ser utilizado como um UDF do Hive por meio da instrução HiveQL `TRANSFORM`.</span><span class="sxs-lookup"><span data-stu-id="406f2-120">Python can be used as a UDF from Hive through the HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="406f2-121">Por exemplo, o seguinte HiveQL invoca o arquivo `hiveudf.py` armazenado na conta de Armazenamento do Azure padrão para o cluster.</span><span class="sxs-lookup"><span data-stu-id="406f2-121">For example, the following HiveQL invokes the `hiveudf.py` file stored in the default Azure Storage account for the cluster.</span></span>

<span data-ttu-id="406f2-122">**HDInsight baseado em Linux**</span><span class="sxs-lookup"><span data-stu-id="406f2-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="406f2-123">**HDInsight baseado em Windows**</span><span class="sxs-lookup"><span data-stu-id="406f2-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="406f2-124">Em clusters de HDInsight baseados no Windows, a cláusula `USING` deve especificar o caminho completo para python.exe.</span><span class="sxs-lookup"><span data-stu-id="406f2-124">On Windows-based HDInsight clusters, the `USING` clause must specify the full path to python.exe.</span></span>

<span data-ttu-id="406f2-125">Aqui está o que este exemplo faz:</span><span class="sxs-lookup"><span data-stu-id="406f2-125">Here's what this example does:</span></span>

1. <span data-ttu-id="406f2-126">A instrução `add file` no início do arquivo adiciona o arquivo `hiveudf.py` ao cache distribuído, portanto, está acessível por todos os nós no cluster.</span><span class="sxs-lookup"><span data-stu-id="406f2-126">The `add file` statement at the beginning of the file adds the `hiveudf.py` file to the distributed cache, so it's accessible by all nodes in the cluster.</span></span>
2. <span data-ttu-id="406f2-127">A instrução `SELECT TRANSFORM ... USING` seleciona dados do `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="406f2-127">The `SELECT TRANSFORM ... USING` statement selects data from the `hivesampletable`.</span></span> <span data-ttu-id="406f2-128">Ela também passa os valores clientid, devicemake e devicemodel para o script `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="406f2-128">It also passes the clientid, devicemake, and devicemodel values to the `hiveudf.py` script.</span></span>
3. <span data-ttu-id="406f2-129">A cláusula `AS` descreve os campos retornados de `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="406f2-129">The `AS` clause describes the fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-the-hiveudfpy-file"></a><span data-ttu-id="406f2-130">Criar o arquivo hiveudf.py</span><span class="sxs-lookup"><span data-stu-id="406f2-130">Create the hiveudf.py file</span></span>


<span data-ttu-id="406f2-131">Em seu ambiente de desenvolvimento, crie um arquivo de texto chamado `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="406f2-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="406f2-132">Use o código a seguir como o conteúdo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="406f2-132">Use the following code as the contents of the file:</span></span>

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

<span data-ttu-id="406f2-133">O script executa as ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="406f2-133">This script performs the following actions:</span></span>

1. <span data-ttu-id="406f2-134">Ler uma linha de dados do STDIN.</span><span class="sxs-lookup"><span data-stu-id="406f2-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="406f2-135">O caractere de nova linha é removido usando `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="406f2-135">The trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="406f2-136">Ao realizar processamento de fluxo, uma única linha contém todos os valores com um caractere de tabulação entre cada par de valores.</span><span class="sxs-lookup"><span data-stu-id="406f2-136">When doing stream processing, a single line contains all the values with a tab character between each value.</span></span> <span data-ttu-id="406f2-137">Assim, `string.split(line, "\t")` pode ser usado para dividir a entrada em cada guia, retornando somente os campos.</span><span class="sxs-lookup"><span data-stu-id="406f2-137">So `string.split(line, "\t")` can be used to split the input at each tab, returning just the fields.</span></span>
4. <span data-ttu-id="406f2-138">Quando o processamento está concluído, a saída precisa ser gravada em STDOUT como uma linha única, com uma tabulação entre cada par de campos.</span><span class="sxs-lookup"><span data-stu-id="406f2-138">When processing is complete, the output must be written to STDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="406f2-139">Por exemplo: `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="406f2-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="406f2-140">O loop `while` é repetido até que nenhum `line` seja lido.</span><span class="sxs-lookup"><span data-stu-id="406f2-140">The `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="406f2-141">A saída do script é uma concatenação dos valores de entrada para `devicemake` e `devicemodel`, e um hash do valor concatenado.</span><span class="sxs-lookup"><span data-stu-id="406f2-141">The script output is a concatenation of the input values for `devicemake` and `devicemodel`, and a hash of the concatenated value.</span></span>

<span data-ttu-id="406f2-142">Consulte [Executando os exemplos](#running) para saber como executar este exemplo em seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="406f2-142">See [Running the examples](#running) for how to run this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="406f2-143"><a name="pigpython"></a>UDF do Pig</span><span class="sxs-lookup"><span data-stu-id="406f2-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="406f2-144">Um script Python pode ser utilizado como um UDF do Pig por meio da instrução `GENERATE`.</span><span class="sxs-lookup"><span data-stu-id="406f2-144">A Python script can be used as a UDF from Pig through the `GENERATE` statement.</span></span> <span data-ttu-id="406f2-145">Você pode executar o script usando o Jython ou o Python C.</span><span class="sxs-lookup"><span data-stu-id="406f2-145">You can run the script using either Jython or C Python.</span></span>

* <span data-ttu-id="406f2-146">Jython é executado em JVM e pode ser chamado nativamente do Pig.</span><span class="sxs-lookup"><span data-stu-id="406f2-146">Jython runs on the JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="406f2-147">O Python C é um processo externo para que os dados do Pig no JVM sejam enviados para o script executado em um processo do Python.</span><span class="sxs-lookup"><span data-stu-id="406f2-147">C Python is an external process, so the data from Pig on the JVM is sent out to the script running in a Python process.</span></span> <span data-ttu-id="406f2-148">A saída do script Python é enviada de volta ao Pig.</span><span class="sxs-lookup"><span data-stu-id="406f2-148">The output of the Python script is sent back into Pig.</span></span>

<span data-ttu-id="406f2-149">Para especificar o interpretador do Python, use `register` ao referenciar o script do Python.</span><span class="sxs-lookup"><span data-stu-id="406f2-149">To specify the Python interpreter, use `register` when referencing the Python script.</span></span> <span data-ttu-id="406f2-150">Os exemplos a seguir registram os scripts com o Pig como `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="406f2-150">The following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="406f2-151">**Para usar o Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="406f2-151">**To use Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="406f2-152">**Para usar o Python C**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="406f2-152">**To use C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="406f2-153">Ao usar o Jython, o caminho para o arquivo pig_jython pode ser um caminho local ou um caminho WASB://.</span><span class="sxs-lookup"><span data-stu-id="406f2-153">When using Jython, the path to the pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="406f2-154">No entanto, ao usar o Python C, você deve fazer referência a um arquivo no sistema de arquivos local do nó que está usando para enviar o trabalho de Pig.</span><span class="sxs-lookup"><span data-stu-id="406f2-154">However, when using C Python, you must reference a file on the local file system of the node that you are using to submit the Pig job.</span></span>

<span data-ttu-id="406f2-155">Depois do registro, o Pig Latin para o exemplo é o mesmo para ambos:</span><span class="sxs-lookup"><span data-stu-id="406f2-155">Once past registration, the Pig Latin for this example is the same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="406f2-156">Aqui está o que este exemplo faz:</span><span class="sxs-lookup"><span data-stu-id="406f2-156">Here's what this example does:</span></span>

1. <span data-ttu-id="406f2-157">A primeira linha carrega o arquivo de dados de exemplo, `sample.log` em `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="406f2-157">The first line loads the sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="406f2-158">Também define cada registro como `chararray`.</span><span class="sxs-lookup"><span data-stu-id="406f2-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="406f2-159">A próxima linha filtra e remove quaisquer valores nulos, armazenando o resultado da operação no `LOG`.</span><span class="sxs-lookup"><span data-stu-id="406f2-159">The next line filters out any null values, storing the result of the operation into `LOG`.</span></span>
3. <span data-ttu-id="406f2-160">Em seguida, itera nos registros em `LOG` e usa `GENERATE` para invocar o método `create_structure` contido no script de Python/Jython carregado como `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="406f2-160">Next, it iterates over the records in `LOG` and uses `GENERATE` to invoke the `create_structure` method contained in the Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="406f2-161">`LINE` é usado para passar o registro atual para a função.</span><span class="sxs-lookup"><span data-stu-id="406f2-161">`LINE` is used to pass the current record to the function.</span></span>
4. <span data-ttu-id="406f2-162">Por fim, as saídas são despejadas em STDOUT usando o comando `DUMP`.</span><span class="sxs-lookup"><span data-stu-id="406f2-162">Finally, the outputs are dumped to STDOUT using the `DUMP` command.</span></span> <span data-ttu-id="406f2-163">Esse comando exibe os resultados após a conclusão da operação.</span><span class="sxs-lookup"><span data-stu-id="406f2-163">This command displays the results after the operation completes.</span></span>

### <a name="create-the-pigudfpy-file"></a><span data-ttu-id="406f2-164">Criar o arquivo pigudf.py</span><span class="sxs-lookup"><span data-stu-id="406f2-164">Create the pigudf.py file</span></span>

<span data-ttu-id="406f2-165">Em seu ambiente de desenvolvimento, crie um arquivo de texto chamado `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="406f2-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="406f2-166">Use o código a seguir como o conteúdo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="406f2-166">Use the following code as the contents of the file:</span></span>

<a name="streamingpy"></a>

```python
# Uncomment the following if using C Python
#from pig_util import outputSchema

@outputSchema("log: {(date:chararray, time:chararray, classname:chararray, level:chararray, detail:chararray)}")
def create_structure(input):
    if (input.startswith('java.lang.Exception')):
        input = input[21:len(input)] + ' - java.lang.Exception'
    date, time, classname, level, detail = input.split(' ', 4)
    return date, time, classname, level, detail
```

<span data-ttu-id="406f2-167">No exemplo de Pig Latin, definimos a entrada `LINE` como um chararray porque não há nenhum esquema consistente para a entrada.</span><span class="sxs-lookup"><span data-stu-id="406f2-167">In the Pig Latin example, we defined the `LINE` input as a chararray because there is no consistent schema for the input.</span></span> <span data-ttu-id="406f2-168">O script Python transforma os dados em um esquema consistente para a saída.</span><span class="sxs-lookup"><span data-stu-id="406f2-168">The Python script transforms the data into a consistent schema for output.</span></span>

1. <span data-ttu-id="406f2-169">A instrução `@outputSchema` define o formato dos dados que são retornados ao Pig.</span><span class="sxs-lookup"><span data-stu-id="406f2-169">The `@outputSchema` statement defines the format of the data that is returned to Pig.</span></span> <span data-ttu-id="406f2-170">Nesse caso, é uma **mala de dados**, que é um tipo de dado do Pig.</span><span class="sxs-lookup"><span data-stu-id="406f2-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="406f2-171">A mala contém os campos a seguir, todos eles sendo matrizes de caracteres (cadeias de caracteres):</span><span class="sxs-lookup"><span data-stu-id="406f2-171">The bag contains the following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="406f2-172">date - a data em que a entrada de log foi criada</span><span class="sxs-lookup"><span data-stu-id="406f2-172">date - the date the log entry was created</span></span>
   * <span data-ttu-id="406f2-173">time - o horário em que a entrada de log foi criada</span><span class="sxs-lookup"><span data-stu-id="406f2-173">time - the time the log entry was created</span></span>
   * <span data-ttu-id="406f2-174">classname - o nome da classe para a qual a entrada foi criada</span><span class="sxs-lookup"><span data-stu-id="406f2-174">classname - the class name the entry was created for</span></span>
   * <span data-ttu-id="406f2-175">level - o nível do log</span><span class="sxs-lookup"><span data-stu-id="406f2-175">level - the log level</span></span>
   * <span data-ttu-id="406f2-176">detail - detalhes para a entrada de log</span><span class="sxs-lookup"><span data-stu-id="406f2-176">detail - verbose details for the log entry</span></span>

2. <span data-ttu-id="406f2-177">Em seguida, o `def create_structure(input)` define a função para a qual o Pig passa itens de linha.</span><span class="sxs-lookup"><span data-stu-id="406f2-177">Next, the `def create_structure(input)` defines the function that Pig passes line items to.</span></span>

3. <span data-ttu-id="406f2-178">Os dados de exemplo, `sample.log`, na maior parte das vezes estão em conformidade com o esquema de data, horário, nome de classe, nível e detalhe que desejamos retornar.</span><span class="sxs-lookup"><span data-stu-id="406f2-178">The example data, `sample.log`, mostly conforms to the date, time, classname, level, and detail schema we want to return.</span></span> <span data-ttu-id="406f2-179">No entanto, contêm algumas linhas que começam com `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="406f2-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="406f2-180">Essas linhas devem ser modificadas para que correspondam ao esquema.</span><span class="sxs-lookup"><span data-stu-id="406f2-180">These lines must be modified to match the schema.</span></span> <span data-ttu-id="406f2-181">A instrução `if` verifica essas linhas, então movimenta os dados de entrada para levar a cadeia de caracteres `*java.lang.Exception*` para o final, colocando os dados em linha com o nosso esquema de saída esperado.</span><span class="sxs-lookup"><span data-stu-id="406f2-181">The `if` statement checks for those, then massages the input data to move the `*java.lang.Exception*` string to the end, bringing the data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="406f2-182">Em seguida, o comando `split` é utilizado para dividir os dados nos quatro primeiros caracteres de espaço.</span><span class="sxs-lookup"><span data-stu-id="406f2-182">Next, the `split` command is used to split the data at the first four space characters.</span></span> <span data-ttu-id="406f2-183">A saída é atribuída a `date`, `time`, `classname`, `level` e `detail`.</span><span class="sxs-lookup"><span data-stu-id="406f2-183">The output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="406f2-184">Por fim, os valores são devolvidos ao Pig.</span><span class="sxs-lookup"><span data-stu-id="406f2-184">Finally, the values are returned to Pig.</span></span>

<span data-ttu-id="406f2-185">Quando os dados são devolvidos ao Pig, eles têm um esquema consistente conforme definido na instrução `@outputSchema`.</span><span class="sxs-lookup"><span data-stu-id="406f2-185">When the data is returned to Pig, it has a consistent schema as defined in the `@outputSchema` statement.</span></span>

## <span data-ttu-id="406f2-186"><a name="running"></a>Carregar e executar os exemplos</span><span class="sxs-lookup"><span data-stu-id="406f2-186"><a name="running"></a>Upload and run the examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="406f2-187">As etapas de **SSH** funcionam apenas com um cluster do HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="406f2-187">The **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="406f2-188">As etapas do **PowerShell** funcionam com um cluster do HDInsight baseado em Windows ou Linux, mas requer um cliente Windows.</span><span class="sxs-lookup"><span data-stu-id="406f2-188">The **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="406f2-189">SSH</span><span class="sxs-lookup"><span data-stu-id="406f2-189">SSH</span></span>

<span data-ttu-id="406f2-190">Para saber mais sobre como usar SSH, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="406f2-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="406f2-191">Use `scp` para copiar os arquivos para seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="406f2-191">Use `scp` to copy the files to your HDInsight cluster.</span></span> <span data-ttu-id="406f2-192">Por exemplo, o comando a seguir copia os arquivos para um cluster chamado **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="406f2-192">For example, the following command copies the files to a cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="406f2-193">Use SSH para conectar-se ao cluster.</span><span class="sxs-lookup"><span data-stu-id="406f2-193">Use SSH to connect to the cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="406f2-194">Na sessão de SSH, adicione ao cluster os arquivos de python carregados no armazenamento WASB anteriormente.</span><span class="sxs-lookup"><span data-stu-id="406f2-194">From the SSH session, add the python files uploaded previously to the WASB storage for the cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="406f2-195">Após carregar os arquivos, use as etapas a seguir para executar os trabalhos de Hive e Pig.</span><span class="sxs-lookup"><span data-stu-id="406f2-195">After uploading the files, use the following steps to run the Hive and Pig jobs.</span></span>

#### <a name="use-the-hive-udf"></a><span data-ttu-id="406f2-196">Usar UDF do Hive</span><span class="sxs-lookup"><span data-stu-id="406f2-196">Use the Hive UDF</span></span>

1. <span data-ttu-id="406f2-197">Use o comando `hive` para iniciar o shell do hive.</span><span class="sxs-lookup"><span data-stu-id="406f2-197">Use the `hive` command to start the hive shell.</span></span> <span data-ttu-id="406f2-198">Você deve ver um prompt `hive>` assim que o shell for carregado.</span><span class="sxs-lookup"><span data-stu-id="406f2-198">You should see a `hive>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="406f2-199">Insira a seguinte consulta no prompt `hive>`:</span><span class="sxs-lookup"><span data-stu-id="406f2-199">Enter the following query at the `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="406f2-200">Depois de inserir a última linha, o trabalho deve ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="406f2-200">After entering the last line, the job should start.</span></span> <span data-ttu-id="406f2-201">Quando o trabalho for concluído, ele retornará uma saída semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="406f2-201">Once the job completes, it returns output similar to the following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-the-pig-udf"></a><span data-ttu-id="406f2-202">Usar UDF do Pig</span><span class="sxs-lookup"><span data-stu-id="406f2-202">Use the Pig UDF</span></span>

1. <span data-ttu-id="406f2-203">Use o comando `pig` para iniciar o shell.</span><span class="sxs-lookup"><span data-stu-id="406f2-203">Use the `pig` command to start the shell.</span></span> <span data-ttu-id="406f2-204">Você vê um prompt `grunt>` quando o shell é carregado.</span><span class="sxs-lookup"><span data-stu-id="406f2-204">You see a `grunt>` prompt once the shell has loaded.</span></span>

2. <span data-ttu-id="406f2-205">No prompt `grunt>`, insira as seguintes instruções:</span><span class="sxs-lookup"><span data-stu-id="406f2-205">Enter the following statements at the `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="406f2-206">Depois de inserir a linha a seguir, o trabalho será iniciado.</span><span class="sxs-lookup"><span data-stu-id="406f2-206">After entering the following line, the job should start.</span></span> <span data-ttu-id="406f2-207">Quando o trabalho for concluído, ele retornará uma saída semelhante aos dados a seguir:</span><span class="sxs-lookup"><span data-stu-id="406f2-207">Once the job completes, it returns output similar to the following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="406f2-208">Use `quit` para sair do shell do Grunt e use o seguinte para editar o arquivo pigudf.py no sistema de arquivos local:</span><span class="sxs-lookup"><span data-stu-id="406f2-208">Use `quit` to exit the Grunt shell, and then use the following to edit the pigudf.py file on the local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="406f2-209">No editor, remova a seguinte linha removendo o caractere `#` do início da linha:</span><span class="sxs-lookup"><span data-stu-id="406f2-209">Once in the editor, uncomment the following line by removing the `#` character from the beginning of the line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="406f2-210">Depois que a alteração for feita, use Ctrl+X para sair do editor.</span><span class="sxs-lookup"><span data-stu-id="406f2-210">Once the change has been made, use Ctrl+X to exit the editor.</span></span> <span data-ttu-id="406f2-211">Selecione Y e Enter para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="406f2-211">Select Y, and then enter to save the changes.</span></span>

6. <span data-ttu-id="406f2-212">Use o comando `pig` para iniciar o shell novamente.</span><span class="sxs-lookup"><span data-stu-id="406f2-212">Use the `pig` command to start the shell again.</span></span> <span data-ttu-id="406f2-213">No prompt `grunt>` , use o que segue para executar o script de Python usando o interpretador de Python C.</span><span class="sxs-lookup"><span data-stu-id="406f2-213">Once you are at the `grunt>` prompt, use the following to run the Python script using the C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="406f2-214">Quando o trabalho for concluído, você verá a mesma saída de quando executou o script usando Jython.</span><span class="sxs-lookup"><span data-stu-id="406f2-214">Once this job completes, you should see the same output as when you previously ran the script using Jython.</span></span>

### <a name="powershell-upload-the-files"></a><span data-ttu-id="406f2-215">PowerShell: carregar os arquivos</span><span class="sxs-lookup"><span data-stu-id="406f2-215">PowerShell: Upload the files</span></span>

<span data-ttu-id="406f2-216">Você pode usar o PowerShell para carregar os arquivos para o servidor do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="406f2-216">You can use PowerShell to upload the files to the HDInsight server.</span></span> <span data-ttu-id="406f2-217">Use o script a seguir para carregar os arquivos do Python:</span><span class="sxs-lookup"><span data-stu-id="406f2-217">Use the following script to upload the Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="406f2-218">As etapas nesta seção usam o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="406f2-218">The steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="406f2-219">Para obter mais informações sobre como usar o Azure PowerShell, consulte [Como instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="406f2-219">For more information on using Azure PowerShell, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
# Change the path to match the file location on your system
$pathToStreamingFile = "C:\path\to\hiveudf.py"
$pathToJythonFile = "C:\path\to\pigudf.py"

$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName=$clusterInfo.DefaultStorageAccount.split('.')[0]
$container=$clusterInfo.DefaultStorageContainer
$storageAccountKey=(Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage content and upload the file
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
> <span data-ttu-id="406f2-220">Alterar o valor `C:\path\to` para o caminho para os arquivos no seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="406f2-220">Change the `C:\path\to` value to the path to the files on your development environment.</span></span>

<span data-ttu-id="406f2-221">Este script obtém informações a partir de seu cluster HDInsight, então, extrai a conta e a chave para a conta de armazenamento padrão, além de carregar os arquivos para a raiz do contêiner.</span><span class="sxs-lookup"><span data-stu-id="406f2-221">This script retrieves information for your HDInsight cluster, then extracts the account and key for the default storage account, and uploads the files to the root of the container.</span></span>

> [!NOTE]
> <span data-ttu-id="406f2-222">Para obter mais informações sobre como carregar arquivos, consulte o documento [Carregar dados para trabalhos do Hadoop no HDInsight](hdinsight-upload-data.md).</span><span class="sxs-lookup"><span data-stu-id="406f2-222">For more information on uploading files, see the [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-the-hive-udf"></a><span data-ttu-id="406f2-223">PowerShell: usar UDF do Hive</span><span class="sxs-lookup"><span data-stu-id="406f2-223">PowerShell: Use the Hive UDF</span></span>

<span data-ttu-id="406f2-224">O PowerShell também pode ser usado para executar remotamente consultas do Hive.</span><span class="sxs-lookup"><span data-stu-id="406f2-224">PowerShell can also be used to remotely run Hive queries.</span></span> <span data-ttu-id="406f2-225">Use o seguinte script do PowerShell para executar uma consulta do Hive que use o script **hiveudf.py**:</span><span class="sxs-lookup"><span data-stu-id="406f2-225">Use the following PowerShell script to run a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="406f2-226">Antes da execução, o script o solicita a fornecer as informações de HTTPs/conta do administrador do seu cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="406f2-226">Before running, the script prompts you for the HTTPs/Admin account information for your HDInsight cluster.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

# If using a Windows-based HDInsight cluster, change the USING statement to:
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
Write-Host "Wait for the Hive job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -JobId $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#   -Clustername $clusterName `
#   -JobId $job.JobId `
#   -HttpCredential $creds `
#   -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="406f2-227">A saída para o trabalho do **Hive** deve ser semelhante ao exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="406f2-227">The output for the **Hive** job should appear similar to the following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="406f2-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="406f2-228">Pig (Jython)</span></span>

<span data-ttu-id="406f2-229">O PowerShell também pode ser usado para executar trabalhos do Pig Latin.</span><span class="sxs-lookup"><span data-stu-id="406f2-229">PowerShell can also be used to run Pig Latin jobs.</span></span> <span data-ttu-id="406f2-230">Para executar um trabalho do Pig Latin que use o script **pigudf.py**, utilize o seguinte script do PowerShell:</span><span class="sxs-lookup"><span data-stu-id="406f2-230">To run a Pig Latin job that uses the **pigudf.py** script, use the following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="406f2-231">Ao enviar um trabalho remotamente usando o PowerShell, não é possível usar o Python C como interpretador.</span><span class="sxs-lookup"><span data-stu-id="406f2-231">When remotely submitting a job using PowerShell, it is not possible to use C Python as the interpreter.</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

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

Write-Host "Wait for the Pig job to complete ..." -ForegroundColor Green
Wait-AzureRmHDInsightJob `
    -Job $job.JobId `
    -ClusterName $clusterName `
    -HttpCredential $creds
# Uncomment the following to see stderr output
# Get-AzureRmHDInsightJobOutput `
#    -Clustername $clusterName `
#    -JobId $job.JobId `
#    -HttpCredential $creds `
#    -DisplayOutputType StandardError
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
    -Clustername $clusterName `
    -JobId $job.JobId `
    -HttpCredential $creds
```

<span data-ttu-id="406f2-232">A saída para o trabalho **Pig** deve ser parecida com os seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="406f2-232">The output for the **Pig** job should appear similar to the following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="406f2-233"><a name="troubleshooting"></a>Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="406f2-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="406f2-234">Erros durante a execução de trabalhos</span><span class="sxs-lookup"><span data-stu-id="406f2-234">Errors when running jobs</span></span>

<span data-ttu-id="406f2-235">Ao executar o trabalho do hive, você poderá encontrar um erro semelhante ao texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="406f2-235">When running the hive job, you may encounter an error similar to the following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing to your custom script. It may have crashed with an error.

<span data-ttu-id="406f2-236">Esse problema pode ser causado pelas terminações de linha no arquivo do Python.</span><span class="sxs-lookup"><span data-stu-id="406f2-236">This problem may be caused by the line endings in the Python file.</span></span> <span data-ttu-id="406f2-237">Muitos editores Windows usam CRLF como padrão como a terminação de linha, mas aplicativos Linux geralmente esperam LF.</span><span class="sxs-lookup"><span data-stu-id="406f2-237">Many Windows editors default to using CRLF as the line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="406f2-238">Você pode seguir as seguintes instruções do PowerShell para remover os caracteres CR antes de carregar o arquivo no HDInsight:</span><span class="sxs-lookup"><span data-stu-id="406f2-238">You can use the following PowerShell statements to remove the CR characters before uploading the file to HDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="406f2-239">Scripts do PowerShell</span><span class="sxs-lookup"><span data-stu-id="406f2-239">PowerShell scripts</span></span>

<span data-ttu-id="406f2-240">Ambos os scripts de exemplo do PowerShell usados para executar os exemplos contêm uma linha comentada que exibe a saída de erro do trabalho.</span><span class="sxs-lookup"><span data-stu-id="406f2-240">Both of the example PowerShell scripts used to run the examples contain a commented line that displays error output for the job.</span></span> <span data-ttu-id="406f2-241">Se você não estiver vendo a saída esperada para o trabalho, remova o comentário da linha a seguir e veja se as informações de erro indicam um problema.</span><span class="sxs-lookup"><span data-stu-id="406f2-241">If you are not seeing the expected output for the job, uncomment the following line and see if the error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="406f2-242">As informações de erro (STDERR) e o resultado do trabalho (STDOUT) também são registrados em seu armazenamento do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="406f2-242">The error information (STDERR) and the result of the job (STDOUT) are also logged to your HDInsight storage.</span></span>

| <span data-ttu-id="406f2-243">Para este trabalho…</span><span class="sxs-lookup"><span data-stu-id="406f2-243">For this job...</span></span> | <span data-ttu-id="406f2-244">Veja estes arquivos no contêiner blob</span><span class="sxs-lookup"><span data-stu-id="406f2-244">Look at these files in the blob container</span></span> |
| --- | --- |
| <span data-ttu-id="406f2-245">Hive</span><span class="sxs-lookup"><span data-stu-id="406f2-245">Hive</span></span> |<span data-ttu-id="406f2-246">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="406f2-246">/HivePython/stderr</span></span><p><span data-ttu-id="406f2-247">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="406f2-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="406f2-248">Pig</span><span class="sxs-lookup"><span data-stu-id="406f2-248">Pig</span></span> |<span data-ttu-id="406f2-249">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="406f2-249">/PigPython/stderr</span></span><p><span data-ttu-id="406f2-250">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="406f2-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="406f2-251"><a name="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="406f2-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="406f2-252">Se você precisar carregar módulos do Python que não são fornecidos por padrão, consulte [Como implantar um módulo para o HDInsight do Azure](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="406f2-252">If you need to load Python modules that aren't provided by default, see [How to deploy a module to Azure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="406f2-253">Para obter outras formas de usar o Pig e o Hive e para saber como usar o MapReduce, consulte os documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="406f2-253">For other ways to use Pig, Hive, and to learn about using MapReduce, see the following documents:</span></span>

* [<span data-ttu-id="406f2-254">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="406f2-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="406f2-255">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="406f2-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="406f2-256">Usar o MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="406f2-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
