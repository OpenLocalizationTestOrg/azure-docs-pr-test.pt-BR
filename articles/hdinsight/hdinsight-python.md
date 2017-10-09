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
# <a name="use-python-user-defined-functions-udf-with-hive-and-pig-in-hdinsight"></a><span data-ttu-id="49f53-103">Usar as UDF (Funções Definidas pelo Usuário) do Python com o Hive e o Pig no HDInsight</span><span class="sxs-lookup"><span data-stu-id="49f53-103">Use Python User Defined Functions (UDF) with Hive and Pig in HDInsight</span></span>

<span data-ttu-id="49f53-104">Saiba como toouse Python definido pelo usuário (UDF) de funções com o Apache Hive e Pig no Hadoop no HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="49f53-104">Learn how toouse Python user-defined functions (UDF) with Apache Hive and Pig in Hadoop on Azure HDInsight.</span></span>

## <span data-ttu-id="49f53-105"><a name="python"></a>Python no HDInsight</span><span class="sxs-lookup"><span data-stu-id="49f53-105"><a name="python"></a>Python on HDInsight</span></span>

<span data-ttu-id="49f53-106">O Python 2.7 é instalado por padrão no HDInsight 3.0 e posteriores.</span><span class="sxs-lookup"><span data-stu-id="49f53-106">Python2.7 is installed by default on HDInsight 3.0 and later.</span></span> <span data-ttu-id="49f53-107">O Apache Hive pode ser usado com essa versão do Python para processamento de fluxo.</span><span class="sxs-lookup"><span data-stu-id="49f53-107">Apache Hive can be used with this version of Python for stream processing.</span></span> <span data-ttu-id="49f53-108">Processamento de fluxo usa STDOUT e STDIN dados toopass entre Hive e hello UDF.</span><span class="sxs-lookup"><span data-stu-id="49f53-108">Stream processing uses STDOUT and STDIN toopass data between Hive and hello UDF.</span></span>

<span data-ttu-id="49f53-109">O HDInsight também inclui o Jython, que é uma implementação do Python gravada em Java.</span><span class="sxs-lookup"><span data-stu-id="49f53-109">HDInsight also includes Jython, which is a Python implementation written in Java.</span></span> <span data-ttu-id="49f53-110">Jython é executado diretamente na máquina Virtual Java de saudação e não usarem o fluxo.</span><span class="sxs-lookup"><span data-stu-id="49f53-110">Jython runs directly on hello Java Virtual Machine and does not use streaming.</span></span> <span data-ttu-id="49f53-111">Jython é Olá recomendada intérprete Python com Python Pig.</span><span class="sxs-lookup"><span data-stu-id="49f53-111">Jython is hello recommended Python interpreter when using Python with Pig.</span></span>

> [!WARNING]
> <span data-ttu-id="49f53-112">etapas de saudação neste documento fazem Olá seguintes suposições:</span><span class="sxs-lookup"><span data-stu-id="49f53-112">hello steps in this document make hello following assumptions:</span></span> 
>
> * <span data-ttu-id="49f53-113">Você cria Olá scripts Python em seu ambiente de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="49f53-113">You create hello Python scripts on your local development environment.</span></span>
> * <span data-ttu-id="49f53-114">Carregar Olá scripts tooHDInsight usando qualquer Olá `scp` comando de uma sessão de Bash local ou Olá fornecido script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="49f53-114">You upload hello scripts tooHDInsight using either hello `scp` command from a local Bash session or hello provided PowerShell script.</span></span>
>
> <span data-ttu-id="49f53-115">Se você quiser Olá toouse [Shell de nuvem do Azure (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) visualizar toowork com HDInsight, em seguida, você deve:</span><span class="sxs-lookup"><span data-stu-id="49f53-115">If you want toouse hello [Azure Cloud Shell (bash)](https://docs.microsoft.com/azure/cloud-shell/overview) preview toowork with HDInsight, then you must:</span></span>
>
> * <span data-ttu-id="49f53-116">Crie scripts de saudação dentro do ambiente de shell Olá nuvem.</span><span class="sxs-lookup"><span data-stu-id="49f53-116">Create hello scripts inside hello cloud shell environment.</span></span>
> * <span data-ttu-id="49f53-117">Use `scp` arquivos tooupload Olá Olá nuvem tooHDInsight de shell.</span><span class="sxs-lookup"><span data-stu-id="49f53-117">Use `scp` tooupload hello files from hello cloud shell tooHDInsight.</span></span>
> * <span data-ttu-id="49f53-118">Use `ssh` de saudação nuvem shell tooconnect tooHDInsight e exemplos de execução hello.</span><span class="sxs-lookup"><span data-stu-id="49f53-118">Use `ssh` from hello cloud shell tooconnect tooHDInsight and run hello examples.</span></span>

## <span data-ttu-id="49f53-119"><a name="hivepython"></a>UDF do Hive</span><span class="sxs-lookup"><span data-stu-id="49f53-119"><a name="hivepython"></a>Hive UDF</span></span>

<span data-ttu-id="49f53-120">Python pode ser usado como uma UDF de Hive por meio de saudação HiveQL `TRANSFORM` instrução.</span><span class="sxs-lookup"><span data-stu-id="49f53-120">Python can be used as a UDF from Hive through hello HiveQL `TRANSFORM` statement.</span></span> <span data-ttu-id="49f53-121">Por exemplo, Olá HiveQL a seguir invoca Olá `hiveudf.py` arquivo armazenado na conta de armazenamento do Azure saudação padrão para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="49f53-121">For example, hello following HiveQL invokes hello `hiveudf.py` file stored in hello default Azure Storage account for hello cluster.</span></span>

<span data-ttu-id="49f53-122">**HDInsight baseado em Linux**</span><span class="sxs-lookup"><span data-stu-id="49f53-122">**Linux-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'python hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

<span data-ttu-id="49f53-123">**HDInsight baseado em Windows**</span><span class="sxs-lookup"><span data-stu-id="49f53-123">**Windows-based HDInsight**</span></span>

```hiveql
add file wasb:///hiveudf.py;

SELECT TRANSFORM (clientid, devicemake, devicemodel)
    USING 'D:\Python27\python.exe hiveudf.py' AS
    (clientid string, phoneLable string, phoneHash string)
FROM hivesampletable
ORDER BY clientid LIMIT 50;
```

> [!NOTE]
> <span data-ttu-id="49f53-124">Em clusters HDInsight baseados no Windows, Olá `USING` cláusula deve especificar Olá caminho completo toopython.exe.</span><span class="sxs-lookup"><span data-stu-id="49f53-124">On Windows-based HDInsight clusters, hello `USING` clause must specify hello full path toopython.exe.</span></span>

<span data-ttu-id="49f53-125">Aqui está o que este exemplo faz:</span><span class="sxs-lookup"><span data-stu-id="49f53-125">Here's what this example does:</span></span>

1. <span data-ttu-id="49f53-126">Olá `add file` instrução no início de saudação do arquivo hello adiciona Olá `hiveudf.py` toohello de arquivo distribuído cache, para que ela é acessível por todos os nós no cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="49f53-126">hello `add file` statement at hello beginning of hello file adds hello `hiveudf.py` file toohello distributed cache, so it's accessible by all nodes in hello cluster.</span></span>
2. <span data-ttu-id="49f53-127">Olá `SELECT TRANSFORM ... USING` instrução seleciona dados da saudação `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="49f53-127">hello `SELECT TRANSFORM ... USING` statement selects data from hello `hivesampletable`.</span></span> <span data-ttu-id="49f53-128">Também passa clientid hello, devicemake e devicemodel valores toohello `hiveudf.py` script.</span><span class="sxs-lookup"><span data-stu-id="49f53-128">It also passes hello clientid, devicemake, and devicemodel values toohello `hiveudf.py` script.</span></span>
3. <span data-ttu-id="49f53-129">Olá `AS` cláusula descreve campos Olá retornados de `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="49f53-129">hello `AS` clause describes hello fields returned from `hiveudf.py`.</span></span>

<a name="streamingpy"></a>

### <a name="create-hello-hiveudfpy-file"></a><span data-ttu-id="49f53-130">Criar arquivo de hiveudf.py Olá</span><span class="sxs-lookup"><span data-stu-id="49f53-130">Create hello hiveudf.py file</span></span>


<span data-ttu-id="49f53-131">Em seu ambiente de desenvolvimento, crie um arquivo de texto chamado `hiveudf.py`.</span><span class="sxs-lookup"><span data-stu-id="49f53-131">On your development environment, create a text file named `hiveudf.py`.</span></span> <span data-ttu-id="49f53-132">Use Olá código a seguir como conteúdo de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="49f53-132">Use hello following code as hello contents of hello file:</span></span>

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

<span data-ttu-id="49f53-133">Esse script executa Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="49f53-133">This script performs hello following actions:</span></span>

1. <span data-ttu-id="49f53-134">Ler uma linha de dados do STDIN.</span><span class="sxs-lookup"><span data-stu-id="49f53-134">Read a line of data from STDIN.</span></span>
2. <span data-ttu-id="49f53-135">Olá caractere de nova linha à direita é removido usando `string.strip(line, "\n ")`.</span><span class="sxs-lookup"><span data-stu-id="49f53-135">hello trailing newline character is removed using `string.strip(line, "\n ")`.</span></span>
3. <span data-ttu-id="49f53-136">Ao fazer o processamento de fluxo, uma única linha contém todos os valores de saudação com um caractere de tabulação entre cada valor.</span><span class="sxs-lookup"><span data-stu-id="49f53-136">When doing stream processing, a single line contains all hello values with a tab character between each value.</span></span> <span data-ttu-id="49f53-137">Portanto `string.split(line, "\t")` pode ser usado toosplit Olá entrada em cada guia, retornando apenas campos de saudação.</span><span class="sxs-lookup"><span data-stu-id="49f53-137">So `string.split(line, "\t")` can be used toosplit hello input at each tab, returning just hello fields.</span></span>
4. <span data-ttu-id="49f53-138">Quando o processamento for concluído, saída de hello deve ser escrita tooSTDOUT como uma única linha, com uma guia entre cada campo.</span><span class="sxs-lookup"><span data-stu-id="49f53-138">When processing is complete, hello output must be written tooSTDOUT as a single line, with a tab between each field.</span></span> <span data-ttu-id="49f53-139">Por exemplo: `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span><span class="sxs-lookup"><span data-stu-id="49f53-139">For example, `print "\t".join([clientid, phone_label, hashlib.md5(phone_label).hexdigest()])`.</span></span>
5. <span data-ttu-id="49f53-140">Olá `while` loop é repetido até que não `line` é lido.</span><span class="sxs-lookup"><span data-stu-id="49f53-140">hello `while` loop repeats until no `line` is read.</span></span>

<span data-ttu-id="49f53-141">saída do script Hello é uma concatenação dos valores de entrada hello para `devicemake` e `devicemodel`, e o valor de hash de saudação concatenado.</span><span class="sxs-lookup"><span data-stu-id="49f53-141">hello script output is a concatenation of hello input values for `devicemake` and `devicemodel`, and a hash of hello concatenated value.</span></span>

<span data-ttu-id="49f53-142">Consulte [executando exemplos Olá](#running) como toorun Este exemplo em seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="49f53-142">See [Running hello examples](#running) for how toorun this example on your HDInsight cluster.</span></span>

## <span data-ttu-id="49f53-143"><a name="pigpython"></a>UDF do Pig</span><span class="sxs-lookup"><span data-stu-id="49f53-143"><a name="pigpython"></a>Pig UDF</span></span>

<span data-ttu-id="49f53-144">Um script Python pode ser usado como uma UDF de Pig por meio de saudação `GENERATE` instrução.</span><span class="sxs-lookup"><span data-stu-id="49f53-144">A Python script can be used as a UDF from Pig through hello `GENERATE` statement.</span></span> <span data-ttu-id="49f53-145">Você pode executar o script hello usando Jython ou Python C.</span><span class="sxs-lookup"><span data-stu-id="49f53-145">You can run hello script using either Jython or C Python.</span></span>

* <span data-ttu-id="49f53-146">Jython é executado em Olá da JVM e nativamente pode ser chamado do Pig.</span><span class="sxs-lookup"><span data-stu-id="49f53-146">Jython runs on hello JVM, and can natively be called from Pig.</span></span>
* <span data-ttu-id="49f53-147">Python C é um processo externo, para que dados de saudação do Pig em Olá JVM é enviada toohello script em execução em um processo de Python.</span><span class="sxs-lookup"><span data-stu-id="49f53-147">C Python is an external process, so hello data from Pig on hello JVM is sent out toohello script running in a Python process.</span></span> <span data-ttu-id="49f53-148">saída Olá Olá script Python é enviada para o Pig.</span><span class="sxs-lookup"><span data-stu-id="49f53-148">hello output of hello Python script is sent back into Pig.</span></span>

<span data-ttu-id="49f53-149">intérprete de Python Olá toospecify, use `register` ao referenciar o script de Python hello.</span><span class="sxs-lookup"><span data-stu-id="49f53-149">toospecify hello Python interpreter, use `register` when referencing hello Python script.</span></span> <span data-ttu-id="49f53-150">Olá exemplos a seguir registrar scripts com Pig como `myfuncs`:</span><span class="sxs-lookup"><span data-stu-id="49f53-150">hello following examples register scripts with Pig as `myfuncs`:</span></span>

* <span data-ttu-id="49f53-151">**toouse Jython**:`register '/path/to/pigudf.py' using jython as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="49f53-151">**toouse Jython**: `register '/path/to/pigudf.py' using jython as myfuncs;`</span></span>
* <span data-ttu-id="49f53-152">**toouse C Python**:`register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span><span class="sxs-lookup"><span data-stu-id="49f53-152">**toouse C Python**: `register '/path/to/pigudf.py' using streaming_python as myfuncs;`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49f53-153">Ao usar Jython, Olá caminho toohello pig_jython arquivo pode ser um caminho local ou um WASB: / / caminho.</span><span class="sxs-lookup"><span data-stu-id="49f53-153">When using Jython, hello path toohello pig_jython file can be either a local path or a WASB:// path.</span></span> <span data-ttu-id="49f53-154">No entanto, ao usar o Python C, você deve fazer referência a um arquivo no sistema de arquivos local de saudação do nó de saudação que você está usando o trabalho de Pig toosubmit hello.</span><span class="sxs-lookup"><span data-stu-id="49f53-154">However, when using C Python, you must reference a file on hello local file system of hello node that you are using toosubmit hello Pig job.</span></span>

<span data-ttu-id="49f53-155">Após após o registro, Olá latino Pig para este exemplo hello mesmo para ambos:</span><span class="sxs-lookup"><span data-stu-id="49f53-155">Once past registration, hello Pig Latin for this example is hello same for both:</span></span>

```pig
LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
LOG = FILTER LOGS by LINE is not null;
DETAILS = FOREACH LOG GENERATE myfuncs.create_structure(LINE);
DUMP DETAILS;
```

<span data-ttu-id="49f53-156">Aqui está o que este exemplo faz:</span><span class="sxs-lookup"><span data-stu-id="49f53-156">Here's what this example does:</span></span>

1. <span data-ttu-id="49f53-157">Olá primeira linha carrega o arquivo de dados de exemplo hello, `sample.log` em `LOGS`.</span><span class="sxs-lookup"><span data-stu-id="49f53-157">hello first line loads hello sample data file, `sample.log` into `LOGS`.</span></span> <span data-ttu-id="49f53-158">Também define cada registro como `chararray`.</span><span class="sxs-lookup"><span data-stu-id="49f53-158">It also defines each record as a `chararray`.</span></span>
2. <span data-ttu-id="49f53-159">linha seguinte Olá filtra quaisquer valores nulos, armazenando Olá resultado da operação de saudação em `LOG`.</span><span class="sxs-lookup"><span data-stu-id="49f53-159">hello next line filters out any null values, storing hello result of hello operation into `LOG`.</span></span>
3. <span data-ttu-id="49f53-160">Em seguida, ele é iterado sobre registros Olá `LOG` e usa `GENERATE` tooinvoke Olá `create_structure` método contido no script de Python/Jython Olá carregado como `myfuncs`.</span><span class="sxs-lookup"><span data-stu-id="49f53-160">Next, it iterates over hello records in `LOG` and uses `GENERATE` tooinvoke hello `create_structure` method contained in hello Python/Jython script loaded as `myfuncs`.</span></span> <span data-ttu-id="49f53-161">`LINE`é usado toopass função toohello registro atual de saudação.</span><span class="sxs-lookup"><span data-stu-id="49f53-161">`LINE` is used toopass hello current record toohello function.</span></span>
4. <span data-ttu-id="49f53-162">Por fim, Olá saídas são tooSTDOUT despejada usando Olá `DUMP` comando.</span><span class="sxs-lookup"><span data-stu-id="49f53-162">Finally, hello outputs are dumped tooSTDOUT using hello `DUMP` command.</span></span> <span data-ttu-id="49f53-163">Este comando exibe os resultados de saudação após a conclusão da operação de saudação.</span><span class="sxs-lookup"><span data-stu-id="49f53-163">This command displays hello results after hello operation completes.</span></span>

### <a name="create-hello-pigudfpy-file"></a><span data-ttu-id="49f53-164">Criar arquivo de pigudf.py Olá</span><span class="sxs-lookup"><span data-stu-id="49f53-164">Create hello pigudf.py file</span></span>

<span data-ttu-id="49f53-165">Em seu ambiente de desenvolvimento, crie um arquivo de texto chamado `pigudf.py`.</span><span class="sxs-lookup"><span data-stu-id="49f53-165">On your development environment, create a text file named `pigudf.py`.</span></span> <span data-ttu-id="49f53-166">Use Olá código a seguir como conteúdo de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="49f53-166">Use hello following code as hello contents of hello file:</span></span>

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

<span data-ttu-id="49f53-167">No exemplo de Pig latino hello, definimos Olá `LINE` de entrada como um chararray porque não há nenhum esquema consistente para entrada hello.</span><span class="sxs-lookup"><span data-stu-id="49f53-167">In hello Pig Latin example, we defined hello `LINE` input as a chararray because there is no consistent schema for hello input.</span></span> <span data-ttu-id="49f53-168">Olá script Python transforma dados de saudação em um esquema consistente para saída.</span><span class="sxs-lookup"><span data-stu-id="49f53-168">hello Python script transforms hello data into a consistent schema for output.</span></span>

1. <span data-ttu-id="49f53-169">Olá `@outputSchema` instrução define o formato de saudação de dados Olá tooPig retornado.</span><span class="sxs-lookup"><span data-stu-id="49f53-169">hello `@outputSchema` statement defines hello format of hello data that is returned tooPig.</span></span> <span data-ttu-id="49f53-170">Nesse caso, é uma **mala de dados**, que é um tipo de dado do Pig.</span><span class="sxs-lookup"><span data-stu-id="49f53-170">In this case, it's a **data bag**, which is a Pig data type.</span></span> <span data-ttu-id="49f53-171">recipiente Olá contém Olá campos, que são chararray (cadeias de caracteres) a seguir:</span><span class="sxs-lookup"><span data-stu-id="49f53-171">hello bag contains hello following fields, all of which are chararray (strings):</span></span>

   * <span data-ttu-id="49f53-172">Data - Olá data Olá entrada de log foi criada</span><span class="sxs-lookup"><span data-stu-id="49f53-172">date - hello date hello log entry was created</span></span>
   * <span data-ttu-id="49f53-173">hora - Olá Olá entrada de log foi criada</span><span class="sxs-lookup"><span data-stu-id="49f53-173">time - hello time hello log entry was created</span></span>
   * <span data-ttu-id="49f53-174">nome da classe - entrada de saudação do nome de classe Olá foi criado para</span><span class="sxs-lookup"><span data-stu-id="49f53-174">classname - hello class name hello entry was created for</span></span>
   * <span data-ttu-id="49f53-175">nível - Olá log</span><span class="sxs-lookup"><span data-stu-id="49f53-175">level - hello log level</span></span>
   * <span data-ttu-id="49f53-176">detalhe - entrada de log detalhado para Olá</span><span class="sxs-lookup"><span data-stu-id="49f53-176">detail - verbose details for hello log entry</span></span>

2. <span data-ttu-id="49f53-177">Em seguida, Olá `def create_structure(input)` define a função hello Pig passa itens de linha.</span><span class="sxs-lookup"><span data-stu-id="49f53-177">Next, hello `def create_structure(input)` defines hello function that Pig passes line items to.</span></span>

3. <span data-ttu-id="49f53-178">Olá dados de exemplo, `sample.log`, principalmente em conformidade toohello data, hora, classname, nível e detalhes de esquema que desejamos tooreturn.</span><span class="sxs-lookup"><span data-stu-id="49f53-178">hello example data, `sample.log`, mostly conforms toohello date, time, classname, level, and detail schema we want tooreturn.</span></span> <span data-ttu-id="49f53-179">No entanto, contêm algumas linhas que começam com `*java.lang.Exception*`.</span><span class="sxs-lookup"><span data-stu-id="49f53-179">However, it contains a few lines that begin with `*java.lang.Exception*`.</span></span> <span data-ttu-id="49f53-180">Essas linhas devem ter um esquema de saudação toomatch modificado.</span><span class="sxs-lookup"><span data-stu-id="49f53-180">These lines must be modified toomatch hello schema.</span></span> <span data-ttu-id="49f53-181">Olá `if` instrução verifica para aqueles que, em seguida, Massagens Olá Olá de toomove de dados de entrada `*java.lang.Exception*` final de toohello de cadeia de caracteres, colocando Olá em linha com nosso esquema de saída esperada.</span><span class="sxs-lookup"><span data-stu-id="49f53-181">hello `if` statement checks for those, then massages hello input data toomove hello `*java.lang.Exception*` string toohello end, bringing hello data in-line with our expected output schema.</span></span>

4. <span data-ttu-id="49f53-182">Em seguida, Olá `split` comando é toosplit usados dados Olá Olá primeiro quatro espaços.</span><span class="sxs-lookup"><span data-stu-id="49f53-182">Next, hello `split` command is used toosplit hello data at hello first four space characters.</span></span> <span data-ttu-id="49f53-183">saída de Hello é atribuída em `date`, `time`, `classname`, `level`, e `detail`.</span><span class="sxs-lookup"><span data-stu-id="49f53-183">hello output is assigned into `date`, `time`, `classname`, `level`, and `detail`.</span></span>

5. <span data-ttu-id="49f53-184">Por fim, os valores de saudação são retornados tooPig.</span><span class="sxs-lookup"><span data-stu-id="49f53-184">Finally, hello values are returned tooPig.</span></span>

<span data-ttu-id="49f53-185">Quando dados saudação são retornados tooPig, tem um esquema consistente conforme definido no hello `@outputSchema` instrução.</span><span class="sxs-lookup"><span data-stu-id="49f53-185">When hello data is returned tooPig, it has a consistent schema as defined in hello `@outputSchema` statement.</span></span>

## <span data-ttu-id="49f53-186"><a name="running"></a>Carregar e executar os exemplos de saudação</span><span class="sxs-lookup"><span data-stu-id="49f53-186"><a name="running"></a>Upload and run hello examples</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49f53-187">Olá **SSH** etapas funcionam apenas com um cluster HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="49f53-187">hello **SSH** steps only work with a Linux-based HDInsight cluster.</span></span> <span data-ttu-id="49f53-188">Olá **PowerShell** etapas funcionam com cluster um HDInsight baseados em Windows ou Linux, mas requer um cliente do Windows.</span><span class="sxs-lookup"><span data-stu-id="49f53-188">hello **PowerShell** steps work with either a Linux or Windows-based HDInsight cluster, but require a Windows client.</span></span>

### <a name="ssh"></a><span data-ttu-id="49f53-189">SSH</span><span class="sxs-lookup"><span data-stu-id="49f53-189">SSH</span></span>

<span data-ttu-id="49f53-190">Para saber mais sobre como usar SSH, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="49f53-190">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

1. <span data-ttu-id="49f53-191">Use `scp` cluster HDInsight do toocopy Olá arquivos tooyour.</span><span class="sxs-lookup"><span data-stu-id="49f53-191">Use `scp` toocopy hello files tooyour HDInsight cluster.</span></span> <span data-ttu-id="49f53-192">Por exemplo, Olá cópias Olá cluster tooa de arquivos chamado de comando a seguir **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="49f53-192">For example, hello following command copies hello files tooa cluster named **mycluster**.</span></span>

    ```bash
    scp hiveudf.py pigudf.py myuser@mycluster-ssh.azurehdinsight.net:
    ```

2. <span data-ttu-id="49f53-193">Use SSH tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="49f53-193">Use SSH tooconnect toohello cluster.</span></span>

    ```bash
    ssh myuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="49f53-194">Da sessão SSH hello, adicione arquivos de python Olá carregado anteriormente toohello armazenamento WASB cluster hello.</span><span class="sxs-lookup"><span data-stu-id="49f53-194">From hello SSH session, add hello python files uploaded previously toohello WASB storage for hello cluster.</span></span>

    ```bash
    hdfs dfs -put hiveudf.py /hiveudf.py
    hdfs dfs -put pigudf.py /pigudf.py
    ```

<span data-ttu-id="49f53-195">Depois de carregar arquivos hello, use Olá etapas a seguir toorun Olá Hive e trabalhos de Pig.</span><span class="sxs-lookup"><span data-stu-id="49f53-195">After uploading hello files, use hello following steps toorun hello Hive and Pig jobs.</span></span>

#### <a name="use-hello-hive-udf"></a><span data-ttu-id="49f53-196">Use Olá Hive UDF</span><span class="sxs-lookup"><span data-stu-id="49f53-196">Use hello Hive UDF</span></span>

1. <span data-ttu-id="49f53-197">Saudação de uso `hive` toostart Olá hive shell de comando.</span><span class="sxs-lookup"><span data-stu-id="49f53-197">Use hello `hive` command toostart hello hive shell.</span></span> <span data-ttu-id="49f53-198">Você deve ver uma `hive>` solicitar depois Olá shell foi carregado.</span><span class="sxs-lookup"><span data-stu-id="49f53-198">You should see a `hive>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="49f53-199">Digite Olá a seguinte consulta no hello `hive>` prompt:</span><span class="sxs-lookup"><span data-stu-id="49f53-199">Enter hello following query at hello `hive>` prompt:</span></span>

   ```hive
   add file wasb:///hiveudf.py;
   SELECT TRANSFORM (clientid, devicemake, devicemodel)
       USING 'python hiveudf.py' AS
       (clientid string, phoneLabel string, phoneHash string)
   FROM hivesampletable
   ORDER BY clientid LIMIT 50;
   ```

3. <span data-ttu-id="49f53-200">Depois de inserir a última linha do hello, trabalho Olá deve começar.</span><span class="sxs-lookup"><span data-stu-id="49f53-200">After entering hello last line, hello job should start.</span></span> <span data-ttu-id="49f53-201">Após a conclusão do trabalho Olá, ele retorna a saída toohello semelhante exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="49f53-201">Once hello job completes, it returns output similar toohello following example:</span></span>

        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100041    RIM 9650    d476f3687700442549a83fac4560c51c
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
        100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="use-hello-pig-udf"></a><span data-ttu-id="49f53-202">Use Olá UDF Pig</span><span class="sxs-lookup"><span data-stu-id="49f53-202">Use hello Pig UDF</span></span>

1. <span data-ttu-id="49f53-203">Saudação de uso `pig` toostart Olá shell de comando.</span><span class="sxs-lookup"><span data-stu-id="49f53-203">Use hello `pig` command toostart hello shell.</span></span> <span data-ttu-id="49f53-204">Você verá um `grunt>` solicitar depois Olá shell foi carregado.</span><span class="sxs-lookup"><span data-stu-id="49f53-204">You see a `grunt>` prompt once hello shell has loaded.</span></span>

2. <span data-ttu-id="49f53-205">Digite hello seguindo as instruções no hello `grunt>` prompt:</span><span class="sxs-lookup"><span data-stu-id="49f53-205">Enter hello following statements at hello `grunt>` prompt:</span></span>

   ```pig
   Register wasb:///pigudf.py using jython as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

3. <span data-ttu-id="49f53-206">Depois de inserir Olá linha a seguir, o trabalho de saudação deve começar.</span><span class="sxs-lookup"><span data-stu-id="49f53-206">After entering hello following line, hello job should start.</span></span> <span data-ttu-id="49f53-207">Após a conclusão do trabalho hello, ele retorna toohello semelhante de saída seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="49f53-207">Once hello job completes, it returns output similar toohello following data:</span></span>

        ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
        ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
        ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
        ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
        ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

4. <span data-ttu-id="49f53-208">Use `quit` tooexit Olá shell pesado e use Olá seguir tooedit Olá pigudf.py arquivo no sistema de arquivos local hello:</span><span class="sxs-lookup"><span data-stu-id="49f53-208">Use `quit` tooexit hello Grunt shell, and then use hello following tooedit hello pigudf.py file on hello local file system:</span></span>

    ```bash
    nano pigudf.py
    ```

5. <span data-ttu-id="49f53-209">Uma vez no editor de hello, remova os comentários Olá seguinte linha removendo Olá `#` caracteres do início de saudação da linha de saudação:</span><span class="sxs-lookup"><span data-stu-id="49f53-209">Once in hello editor, uncomment hello following line by removing hello `#` character from hello beginning of hello line:</span></span>

    ```bash
    #from pig_util import outputSchema
    ```

    <span data-ttu-id="49f53-210">Depois de alterar Olá, use o editor de saudação de tooexit de Ctrl + X.</span><span class="sxs-lookup"><span data-stu-id="49f53-210">Once hello change has been made, use Ctrl+X tooexit hello editor.</span></span> <span data-ttu-id="49f53-211">Selecione Y e, em seguida, insira as alterações de saudação toosave.</span><span class="sxs-lookup"><span data-stu-id="49f53-211">Select Y, and then enter toosave hello changes.</span></span>

6. <span data-ttu-id="49f53-212">Saudação de uso `pig` comando shell de saudação toostart novamente.</span><span class="sxs-lookup"><span data-stu-id="49f53-212">Use hello `pig` command toostart hello shell again.</span></span> <span data-ttu-id="49f53-213">Quando você chega a saudação `grunt>` prompt, use Olá script em Python usando o interpretador do Python C Olá Olá toorun a seguir.</span><span class="sxs-lookup"><span data-stu-id="49f53-213">Once you are at hello `grunt>` prompt, use hello following toorun hello Python script using hello C Python interpreter.</span></span>

   ```pig
   Register 'pigudf.py' using streaming_python as myfuncs;
   LOGS = LOAD 'wasb:///example/data/sample.log' as (LINE:chararray);
   LOG = FILTER LOGS by LINE is not null;
   DETAILS = foreach LOG generate myfuncs.create_structure(LINE);
   DUMP DETAILS;
   ```

    <span data-ttu-id="49f53-214">Quando esta tarefa for concluída, você deverá ver Olá mesmo saído como quando você executou anteriormente script hello usando Jython.</span><span class="sxs-lookup"><span data-stu-id="49f53-214">Once this job completes, you should see hello same output as when you previously ran hello script using Jython.</span></span>

### <a name="powershell-upload-hello-files"></a><span data-ttu-id="49f53-215">PowerShell: Arquivos de saudação de carregamento</span><span class="sxs-lookup"><span data-stu-id="49f53-215">PowerShell: Upload hello files</span></span>

<span data-ttu-id="49f53-216">Você pode usar o servidor do PowerShell tooupload Olá arquivos toohello HDInsight.</span><span class="sxs-lookup"><span data-stu-id="49f53-216">You can use PowerShell tooupload hello files toohello HDInsight server.</span></span> <span data-ttu-id="49f53-217">Use Olá arquivos de script de tooupload Olá Python a seguir:</span><span class="sxs-lookup"><span data-stu-id="49f53-217">Use hello following script tooupload hello Python files:</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="49f53-218">Olá etapas desta seção usam PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="49f53-218">hello steps in this section use Azure PowerShell.</span></span> <span data-ttu-id="49f53-219">Para obter mais informações sobre como usar o PowerShell do Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="49f53-219">For more information on using Azure PowerShell, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

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
> <span data-ttu-id="49f53-220">Saudação de alteração `C:\path\to` valor toohello arquivos de toohello de caminho em seu ambiente de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="49f53-220">Change hello `C:\path\to` value toohello path toohello files on your development environment.</span></span>

<span data-ttu-id="49f53-221">Este script recupera as informações de seu cluster HDInsight, em seguida, extrai conta hello e chave de conta de armazenamento padrão hello e carregamentos Olá raiz toohello de arquivos do contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="49f53-221">This script retrieves information for your HDInsight cluster, then extracts hello account and key for hello default storage account, and uploads hello files toohello root of hello container.</span></span>

> [!NOTE]
> <span data-ttu-id="49f53-222">Para obter mais informações sobre como carregar arquivos, consulte Olá [carregar dados para trabalhos de Hadoop no HDInsight](hdinsight-upload-data.md) documento.</span><span class="sxs-lookup"><span data-stu-id="49f53-222">For more information on uploading files, see hello [Upload data for Hadoop jobs in HDInsight](hdinsight-upload-data.md) document.</span></span>

#### <a name="powershell-use-hello-hive-udf"></a><span data-ttu-id="49f53-223">PowerShell: Saudação de uso Hive UDF</span><span class="sxs-lookup"><span data-stu-id="49f53-223">PowerShell: Use hello Hive UDF</span></span>

<span data-ttu-id="49f53-224">PowerShell também pode ser usado tooremotely executar consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="49f53-224">PowerShell can also be used tooremotely run Hive queries.</span></span> <span data-ttu-id="49f53-225">Saudação de uso toorun de script do PowerShell uma consulta de Hive que usa a seguir **hiveudf.py** script:</span><span class="sxs-lookup"><span data-stu-id="49f53-225">Use hello following PowerShell script toorun a Hive query that uses **hiveudf.py** script:</span></span>

> [!IMPORTANT]
> <span data-ttu-id="49f53-226">Antes de executar, script hello solicita Olá HTTPs/Admin informações da conta para seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="49f53-226">Before running, hello script prompts you for hello HTTPs/Admin account information for your HDInsight cluster.</span></span>

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

<span data-ttu-id="49f53-227">Olá saída Olá **Hive** trabalho deve aparecer semelhante toohello exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="49f53-227">hello output for hello **Hive** job should appear similar toohello following example:</span></span>

    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100041    RIM 9650    d476f3687700442549a83fac4560c51c
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9
    100042    Apple iPhone 4.2.x    375ad9a0ddc4351536804f1d5d0ea9b9

#### <a name="pig-jython"></a><span data-ttu-id="49f53-228">Pig (Jython)</span><span class="sxs-lookup"><span data-stu-id="49f53-228">Pig (Jython)</span></span>

<span data-ttu-id="49f53-229">PowerShell também pode ser usado toorun Pig latino trabalhos.</span><span class="sxs-lookup"><span data-stu-id="49f53-229">PowerShell can also be used toorun Pig Latin jobs.</span></span> <span data-ttu-id="49f53-230">toorun um trabalho de Pig latino que usa Olá **pigudf.py** de script, use Olá script do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="49f53-230">toorun a Pig Latin job that uses hello **pigudf.py** script, use hello following PowerShell script:</span></span>

> [!NOTE]
> <span data-ttu-id="49f53-231">Durante o envio de um trabalho usando o PowerShell remotamente, não é possível toouse Python C como interpretador hello.</span><span class="sxs-lookup"><span data-stu-id="49f53-231">When remotely submitting a job using PowerShell, it is not possible toouse C Python as hello interpreter.</span></span>

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

<span data-ttu-id="49f53-232">Olá saída Olá **Pig** trabalho deve aparecer semelhante toohello seguintes dados:</span><span class="sxs-lookup"><span data-stu-id="49f53-232">hello output for hello **Pig** job should appear similar toohello following data:</span></span>

    ((2012-02-03,20:11:56,SampleClass5,[TRACE],verbose detail for id 990982084))
    ((2012-02-03,20:11:56,SampleClass7,[TRACE],verbose detail for id 1560323914))
    ((2012-02-03,20:11:56,SampleClass8,[DEBUG],detail for id 2083681507))
    ((2012-02-03,20:11:56,SampleClass3,[TRACE],verbose detail for id 1718828806))
    ((2012-02-03,20:11:56,SampleClass3,[INFO],everything normal for id 530537821))

## <span data-ttu-id="49f53-233"><a name="troubleshooting"></a>Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="49f53-233"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="errors-when-running-jobs"></a><span data-ttu-id="49f53-234">Erros durante a execução de trabalhos</span><span class="sxs-lookup"><span data-stu-id="49f53-234">Errors when running jobs</span></span>

<span data-ttu-id="49f53-235">Ao executar o trabalho de hive hello, você pode encontrar um toohello semelhante erro texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="49f53-235">When running hello hive job, you may encounter an error similar toohello following text:</span></span>

    Caused by: org.apache.hadoop.hive.ql.metadata.HiveException: [Error 20001]: An error occurred while reading or writing tooyour custom script. It may have crashed with an error.

<span data-ttu-id="49f53-236">Esse problema pode ser causado por terminações de linha de saudação no arquivo de Python hello.</span><span class="sxs-lookup"><span data-stu-id="49f53-236">This problem may be caused by hello line endings in hello Python file.</span></span> <span data-ttu-id="49f53-237">Muitos editores de Windows padrão toousing CRLF como linha hello final, mas aplicativos Linux normalmente esperam LF.</span><span class="sxs-lookup"><span data-stu-id="49f53-237">Many Windows editors default toousing CRLF as hello line ending, but Linux applications usually expect LF.</span></span>

<span data-ttu-id="49f53-238">Você pode usar o hello PowerShell instruções tooremove Olá CR caracteres à direita antes de carregar Olá arquivo tooHDInsight:</span><span class="sxs-lookup"><span data-stu-id="49f53-238">You can use hello following PowerShell statements tooremove hello CR characters before uploading hello file tooHDInsight:</span></span>

```powershell
$original_file ='c:\path\to\hiveudf.py'
$text = [IO.File]::ReadAllText($original_file) -replace "`r`n", "`n"
[IO.File]::WriteAllText($original_file, $text)
```

### <a name="powershell-scripts"></a><span data-ttu-id="49f53-239">Scripts do PowerShell</span><span class="sxs-lookup"><span data-stu-id="49f53-239">PowerShell scripts</span></span>

<span data-ttu-id="49f53-240">Exemplo hello scripts do PowerShell usados toorun exemplos de saudação conter uma linha comentada que exibe a saída de erro para o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="49f53-240">Both of hello example PowerShell scripts used toorun hello examples contain a commented line that displays error output for hello job.</span></span> <span data-ttu-id="49f53-241">Se você não estiver vendo saída Olá esperado para o trabalho de hello, remova os comentários a seguir Olá linha e ver se as informações de erro de saudação indicam um problema.</span><span class="sxs-lookup"><span data-stu-id="49f53-241">If you are not seeing hello expected output for hello job, uncomment hello following line and see if hello error information indicates a problem.</span></span>

```powershell
# Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="49f53-242">informações de erro da saudação (STDERR) e o resultado de saudação do trabalho de saudação (STDOUT) também são registrados tooyour HDInsight armazenamento.</span><span class="sxs-lookup"><span data-stu-id="49f53-242">hello error information (STDERR) and hello result of hello job (STDOUT) are also logged tooyour HDInsight storage.</span></span>

| <span data-ttu-id="49f53-243">Para este trabalho…</span><span class="sxs-lookup"><span data-stu-id="49f53-243">For this job...</span></span> | <span data-ttu-id="49f53-244">Examinar esses arquivos no contêiner de blob Olá</span><span class="sxs-lookup"><span data-stu-id="49f53-244">Look at these files in hello blob container</span></span> |
| --- | --- |
| <span data-ttu-id="49f53-245">Hive</span><span class="sxs-lookup"><span data-stu-id="49f53-245">Hive</span></span> |<span data-ttu-id="49f53-246">/HivePython/stderr</span><span class="sxs-lookup"><span data-stu-id="49f53-246">/HivePython/stderr</span></span><p><span data-ttu-id="49f53-247">/HivePython/stdout</span><span class="sxs-lookup"><span data-stu-id="49f53-247">/HivePython/stdout</span></span> |
| <span data-ttu-id="49f53-248">Pig</span><span class="sxs-lookup"><span data-stu-id="49f53-248">Pig</span></span> |<span data-ttu-id="49f53-249">/PigPython/stderr</span><span class="sxs-lookup"><span data-stu-id="49f53-249">/PigPython/stderr</span></span><p><span data-ttu-id="49f53-250">/PigPython/stdout</span><span class="sxs-lookup"><span data-stu-id="49f53-250">/PigPython/stdout</span></span> |

## <span data-ttu-id="49f53-251"><a name="next"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="49f53-251"><a name="next"></a>Next steps</span></span>

<span data-ttu-id="49f53-252">Se você precisar de módulos de Python tooload que não são fornecidos por padrão, consulte [como toodeploy tooAzure um módulo HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span><span class="sxs-lookup"><span data-stu-id="49f53-252">If you need tooload Python modules that aren't provided by default, see [How toodeploy a module tooAzure HDInsight](http://blogs.msdn.com/b/benjguin/archive/2014/03/03/how-to-deploy-a-python-module-to-windows-azure-hdinsight.aspx).</span></span>

<span data-ttu-id="49f53-253">Para outras maneiras toouse Pig, Hive e toolearn sobre o uso de MapReduce, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="49f53-253">For other ways toouse Pig, Hive, and toolearn about using MapReduce, see hello following documents:</span></span>

* [<span data-ttu-id="49f53-254">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="49f53-254">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="49f53-255">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="49f53-255">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="49f53-256">Usar o MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="49f53-256">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)
