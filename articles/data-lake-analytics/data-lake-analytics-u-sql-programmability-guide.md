---
title: "Guia de programação aaaU-SQL para o Azure Data Lake | Microsoft Docs"
description: "Saiba mais sobre o conjunto de saudação de serviços do Azure Data Lake que permitem que você toocreate uma plataforma de dados grande baseado em nuvem."
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
ms.assetid: 63be271e-7c44-4d19-9897-c2913ee9599d
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/30/2017
ms.author: saveenr
ms.openlocfilehash: cc8f126234c6106a0dc633ce85a1d9ab1e634e30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="f9942-103">Guia de programação do U-SQL</span><span class="sxs-lookup"><span data-stu-id="f9942-103">U-SQL programmability guide</span></span>

<span data-ttu-id="f9942-104">O U-SQL é uma linguagem de consulta projetada para o tipo big data de cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f9942-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="f9942-105">Um dos recursos exclusivos de saudação do U-SQL é a combinação de saudação de linguagem declarativa do tipo SQL Olá com extensibilidade hello e programação que é fornecida pelo c#.</span><span class="sxs-lookup"><span data-stu-id="f9942-105">One of hello unique features of U-SQL is hello combination of hello SQL-like declarative language with hello extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="f9942-106">Neste guia, nos concentraremos nas extensibilidade hello e programação da linguagem de U-SQL Olá habilitado por c#.</span><span class="sxs-lookup"><span data-stu-id="f9942-106">In this guide, we concentrate on hello extensibility and programmability of hello U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="f9942-107">Requisitos</span><span class="sxs-lookup"><span data-stu-id="f9942-107">Requirements</span></span>

<span data-ttu-id="f9942-108">Baixe e instale as [Ferramentas do Azure Data Lake para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="f9942-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="f9942-109">Introdução ao U-SQL</span><span class="sxs-lookup"><span data-stu-id="f9942-109">Get started with U-SQL</span></span>  

<span data-ttu-id="f9942-110">Vejamos Olá script U-SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9942-110">Let’s look at hello following U-SQL script:</span></span>

```
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso",   1500.0, "2017-03-39"),
            ("Woodgrove", 2700.0, "2017-04-10")
        ) AS 
              D( customer, amount );
@results =
    SELECT
        customer,
    amount,
    date
    FROM @a;    
```

<span data-ttu-id="f9942-111">Ele define um conjunto de linhas chamado @a e cria um conjunto de linhas chamado @results de @a.</span><span class="sxs-lookup"><span data-stu-id="f9942-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="f9942-112">Tipos e expressões de C# no script U-SQL</span><span class="sxs-lookup"><span data-stu-id="f9942-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="f9942-113">Uma expressão de U-SQL é uma expressão de C# combinada com operações lógicas U-SQL como `AND`, `OR` e `NOT`.</span><span class="sxs-lookup"><span data-stu-id="f9942-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="f9942-114">Expressões U-SQL podem ser usadas com SELECT, EXTRACT, WHERE, HAVING, GROUP BY e DECLARE.</span><span class="sxs-lookup"><span data-stu-id="f9942-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="f9942-115">Por exemplo, Olá script a seguir analisa uma cadeia de um valor DateTime na cláusula SELECT hello.</span><span class="sxs-lookup"><span data-stu-id="f9942-115">For example, hello following script parses a string a DateTime value in hello SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="f9942-116">Olá script a seguir analisa uma cadeia de caracteres de um valor de data e hora em uma instrução DECLARE.</span><span class="sxs-lookup"><span data-stu-id="f9942-116">hello following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="f9942-117">Usar expressões C# para conversões de tipo de dados</span><span class="sxs-lookup"><span data-stu-id="f9942-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="f9942-118">saudação de exemplo a seguir demonstra como você pode fazer uma conversão de dados de data e hora usando expressões de c#.</span><span class="sxs-lookup"><span data-stu-id="f9942-118">hello following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="f9942-119">Neste cenário específico, dados de data e hora da cadeia de caracteres são convertida toostandard datetime com notação de hora 00:00:00 meia-noite.</span><span class="sxs-lookup"><span data-stu-id="f9942-119">In this particular scenario, string datetime data is converted toostandard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="f9942-120">Usar expressões C# para a data de hoje</span><span class="sxs-lookup"><span data-stu-id="f9942-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="f9942-121">toopull a data de hoje, podemos usar Olá expressão c# a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9942-121">toopull today’s date, we can use hello following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="f9942-122">Aqui está um exemplo de como toouse essa expressão em um script:</span><span class="sxs-lookup"><span data-stu-id="f9942-122">Here's an example of how toouse this expression in a script:</span></span>

```
@rs1 =
    SELECT
        MAX(guid) AS start_id,
        MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        user,
        des
    FROM @rs0
    GROUP BY user, des;
```



## <a name="using-net-assemblies"></a><span data-ttu-id="f9942-123">Usando assemblies .NET</span><span class="sxs-lookup"><span data-stu-id="f9942-123">Using .NET assemblies</span></span>
<span data-ttu-id="f9942-124">Modelo de extensibilidade do U-SQL se baseia no código personalizado do hello capacidade tooadd.</span><span class="sxs-lookup"><span data-stu-id="f9942-124">U-SQL’s extensibility model relies heavily on hello ability tooadd custom code.</span></span> <span data-ttu-id="f9942-125">Atualmente, U-SQL fornece maneiras fáceis tooadd sua própria Microsoft. Código de rede (em especial, c#).</span><span class="sxs-lookup"><span data-stu-id="f9942-125">Currently, U-SQL provides you with easy ways tooadd your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="f9942-126">No entanto, você também pode adicionar código personalizado escrito em outras linguagens .NET, como VB.NET ou F#.</span><span class="sxs-lookup"><span data-stu-id="f9942-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="f9942-127">Registrar um assembly .NET</span><span class="sxs-lookup"><span data-stu-id="f9942-127">Register a .NET assembly</span></span>

<span data-ttu-id="f9942-128">Use tooplace de instrução de CREATE ASSEMBLY hello um assembly do .NET em um banco de dados de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f9942-128">Use hello CREATE ASSEMBLY statement tooplace a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="f9942-129">Quando um assembly é um banco de dados, scripts U-SQL podem usar esses assemblies usando a instrução de referência de ASSEMBLY hello.</span><span class="sxs-lookup"><span data-stu-id="f9942-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using hello REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="f9942-130">Olá mostrado no código a seguir como tooregister um assembly:</span><span class="sxs-lookup"><span data-stu-id="f9942-130">hello following code shows how tooregister an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="f9942-131">Olá mostrado no código a seguir como tooreference um assembly:</span><span class="sxs-lookup"><span data-stu-id="f9942-131">hello following code shows how tooreference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="f9942-132">Consulte Olá [instruções de registro do assembly](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) que abrange a este tópico mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="f9942-132">Consult hello [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="f9942-133">Usar o controle de versão do assembly</span><span class="sxs-lookup"><span data-stu-id="f9942-133">Use assembly versioning</span></span>
<span data-ttu-id="f9942-134">Atualmente, U-SQL usa saudação do .NET Framework versão 4.5.</span><span class="sxs-lookup"><span data-stu-id="f9942-134">Currently, U-SQL uses hello .NET Framework version 4.5.</span></span> <span data-ttu-id="f9942-135">Portanto, certifique-se de que seus próprios assemblies são compatíveis com essa versão do tempo de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9942-135">So ensure that your own assemblies are compatible with that version of hello runtime.</span></span>

<span data-ttu-id="f9942-136">Conforme mencionado anteriormente, o U-SQL executa código em um formato de 64 bits (x64).</span><span class="sxs-lookup"><span data-stu-id="f9942-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="f9942-137">Portanto, certifique-se de que seu código seja compilado toorun em x64.</span><span class="sxs-lookup"><span data-stu-id="f9942-137">So make sure that your code is compiled toorun on x64.</span></span> <span data-ttu-id="f9942-138">Caso contrário, você obterá o erro de formato incorreto de saudação mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f9942-138">Otherwise you get hello incorrect format error shown earlier.</span></span>

<span data-ttu-id="f9942-139">Cada arquivo de recurso e DLL de assembly carregado, como um tempo de execução diferente, um assembly nativo ou um arquivo config, pode ter no máximo 400 MB.</span><span class="sxs-lookup"><span data-stu-id="f9942-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="f9942-140">tamanho total de saudação de recursos implantados, por meio do recurso de IMPLANTAR ou por meio de referências tooassemblies e seus arquivos adicionais, não pode exceder 3 GB.</span><span class="sxs-lookup"><span data-stu-id="f9942-140">hello total size of deployed resources, either via DEPLOY RESOURCE or via references tooassemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="f9942-141">Por fim, observe que cada banco de dados U-SQL pode conter apenas uma versão de qualquer determinado assembly.</span><span class="sxs-lookup"><span data-stu-id="f9942-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="f9942-142">Por exemplo, se você precisar tanto versão 7 e 8 do hello NewtonSoft Json.Net biblioteca, você precisa tooregistê-los em dois bancos de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="f9942-142">For example, if you need both version 7 and version 8 of hello NewtonSoft Json.Net library, you need tooregister them in two different databases.</span></span> <span data-ttu-id="f9942-143">Além disso, cada script só pode fazer referência a versão de tooone de um determinado assembly DLL.</span><span class="sxs-lookup"><span data-stu-id="f9942-143">Furthermore, each script can only refer tooone version of a given assembly DLL.</span></span> <span data-ttu-id="f9942-144">Nesse sentido, U-SQL segue Olá c# assembly gerenciamento e controle de versão de semântica.</span><span class="sxs-lookup"><span data-stu-id="f9942-144">In this respect, U-SQL follows hello C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="f9942-145">Funções definidas pelo usuário: UDF</span><span class="sxs-lookup"><span data-stu-id="f9942-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="f9942-146">Funções definidas pelo usuário U-SQL ou UDF, estiver programando rotinas que aceitam parâmetros, executam uma ação (como um cálculo complexo) e retornam Olá resultado dessa ação como um valor.</span><span class="sxs-lookup"><span data-stu-id="f9942-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return hello result of that action as a value.</span></span> <span data-ttu-id="f9942-147">Olá retornar o valor de UDF só pode ser um único valor escalar.</span><span class="sxs-lookup"><span data-stu-id="f9942-147">hello return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="f9942-148">A UDF do U-SQL pode ser chamado no script base U-SQL como qualquer outra função escalar C#.</span><span class="sxs-lookup"><span data-stu-id="f9942-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="f9942-149">Recomendamos que você inicialize as funções do U-SQL definidas pelo usuário como **públicas** e **estáticas**.</span><span class="sxs-lookup"><span data-stu-id="f9942-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="f9942-150">Primeiro vamos examinar Olá o exemplo simples de criação de um UDF.</span><span class="sxs-lookup"><span data-stu-id="f9942-150">First let’s look at hello simple example of creating a UDF.</span></span>

<span data-ttu-id="f9942-151">Neste cenário de caso de uso, é preciso toodetermine Olá período fiscal, incluindo o trimestre fiscal hello e mês fiscal do hello entrar pela primeira vez para usuário específico hello.</span><span class="sxs-lookup"><span data-stu-id="f9942-151">In this use-case scenario, we need toodetermine hello fiscal period, including hello fiscal quarter and fiscal month of hello first sign-in for hello specific user.</span></span> <span data-ttu-id="f9942-152">Olá primeiro mês fiscal do ano de saudação em nosso cenário é junho.</span><span class="sxs-lookup"><span data-stu-id="f9942-152">hello first fiscal month of hello year in our scenario is June.</span></span>

<span data-ttu-id="f9942-153">período de toocalculate, apresentamos Olá função c# a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9942-153">toocalculate fiscal period, we introduce hello following C# function:</span></span>

```
public static string GetFiscalPeriod(DateTime dt)
{
    int FiscalMonth=0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter=0;
    if (FiscalMonth >=1 && FiscalMonth<=3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return "Q" + FiscalQuarter.ToString() + ":P" + FiscalMonth.ToString();
}
```

<span data-ttu-id="f9942-154">Ela simplesmente calcula o mês e o trimestre fiscal e retorna um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="f9942-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="f9942-155">Junho, Olá primeiro mês do hello primeiro trimestre fiscal, usamos "Q1:P1".</span><span class="sxs-lookup"><span data-stu-id="f9942-155">For June, hello first month of hello first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="f9942-156">No caso de julho, usamos "Q1:P2" e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="f9942-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="f9942-157">Essa é uma regular c# função que estamos toouse contínuo em nosso projeto U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f9942-157">This is a regular C# function that we are going toouse in our U-SQL project.</span></span>

<span data-ttu-id="f9942-158">Aqui está a aparência da seção de código por trás de saudação neste cenário:</span><span class="sxs-lookup"><span data-stu-id="f9942-158">Here is how hello code-behind section looks in this scenario:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        public static string GetFiscalPeriod(DateTime dt)
        {
            int FiscalMonth=0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter=0;
            if (FiscalMonth >=1 && FiscalMonth<=3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return "Q" + FiscalQuarter.ToString() + ":" + FiscalMonth.ToString();
        }

    }

}
```

<span data-ttu-id="f9942-159">Agora, vamos toocall essa função de script U-SQL de base de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9942-159">Now we are going toocall this function from hello base U-SQL script.</span></span> <span data-ttu-id="f9942-160">toodo isso, temos tooprovide um nome totalmente qualificado para a função hello, incluindo o namespace de saudação, que nesse caso é NameSpace.Class.Function(parameter).</span><span class="sxs-lookup"><span data-stu-id="f9942-160">toodo this, we have tooprovide a fully qualified name for hello function, including hello namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="f9942-161">O seguinte é script base do hello real U-SQL:</span><span class="sxs-lookup"><span data-stu-id="f9942-161">Following is hello actual U-SQL base script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt DateTime,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

DECLARE @default_dt DateTime = Convert.ToDateTime("06/01/2016");

@rs1 =
    SELECT
        MAX(guid) AS start_id,
    MIN(dt) AS start_time,
        MIN(Convert.ToDateTime(Convert.ToDateTime(dt<@default_dt?@default_dt:dt).ToString("yyyy-MM-dd"))) AS start_zero_time,
        MIN(USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)) AS start_fiscalperiod,
        user,
        des
    FROM @rs0
    GROUP BY user, des;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="f9942-162">O seguinte é um arquivo de saída Olá Olá da execução do script:</span><span class="sxs-lookup"><span data-stu-id="f9942-162">Following is hello output file of hello script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="f9942-163">Esse exemplo demonstra um uso simples de UDF embutida no U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f9942-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="f9942-164">Manter o estado entre invocações da UDF</span><span class="sxs-lookup"><span data-stu-id="f9942-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="f9942-165">Objetos de programação c# U-SQL podem ser mais sofisticados, utilizando a interatividade por meio de variáveis globais do hello por trás do código.</span><span class="sxs-lookup"><span data-stu-id="f9942-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through hello code-behind global variables.</span></span> <span data-ttu-id="f9942-166">Vamos examinar Olá seguindo o cenário de caso de uso de negócios.</span><span class="sxs-lookup"><span data-stu-id="f9942-166">Let’s look at hello following business use-case scenario.</span></span>

<span data-ttu-id="f9942-167">Em grandes organizações, os usuários podem alternar entre diversos aplicativos internos.</span><span class="sxs-lookup"><span data-stu-id="f9942-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="f9942-168">Eles podem incluir o Microsoft Dynamics CRM, o PowerBI e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="f9942-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="f9942-169">Os clientes talvez queira tooapply uma análise de telemetria de como os usuários alternam entre diferentes aplicativos, o uso de saudação mostra as tendências são e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="f9942-169">Customers might want tooapply a telemetry analysis of how users switch between different applications, what hello usage trends are, and so on.</span></span> <span data-ttu-id="f9942-170">meta de Hello para empresas Olá é toooptimize o uso do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9942-170">hello goal for hello business is toooptimize application usage.</span></span> <span data-ttu-id="f9942-171">Eles também seja toocombine diferentes aplicativos ou as rotinas de logon específicas.</span><span class="sxs-lookup"><span data-stu-id="f9942-171">They also might want toocombine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="f9942-172">tooachieve essa meta, temos toodetermine IDs de sessão e o tempo de atraso entre hello última sessão que ocorreu.</span><span class="sxs-lookup"><span data-stu-id="f9942-172">tooachieve this goal, we have toodetermine session IDs and lag time between hello last session that occurred.</span></span>

<span data-ttu-id="f9942-173">Precisamos toofind uma entrada anterior e, em seguida, atribuir esse sessões de entrada tooall que estão sendo gerado toohello mesmo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f9942-173">We need toofind a previous sign-in and then assign this sign-in tooall sessions that are being generated toohello same application.</span></span> <span data-ttu-id="f9942-174">Olá primeiro desafio é que script base U-SQL não permite nos cálculos de tooapply colunas já calculado com a função LAG.</span><span class="sxs-lookup"><span data-stu-id="f9942-174">hello first challenge is that U-SQL base script doesn't allow us tooapply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="f9942-175">Olá segundo desafio é que temos de sessão específica do tookeep Olá para todas as sessões em Olá mesmo período de tempo.</span><span class="sxs-lookup"><span data-stu-id="f9942-175">hello second challenge is that we have tookeep hello specific session for all sessions within hello same time period.</span></span>

<span data-ttu-id="f9942-176">toosolve esse problema, usamos uma variável global dentro de uma seção de lógica: `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="f9942-176">toosolve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="f9942-177">Essa variável global é aplicado toohello todo conjunto de linhas durante a execução do nosso script.</span><span class="sxs-lookup"><span data-stu-id="f9942-177">This global variable is applied toohello entire rowset during our script execution.</span></span>

<span data-ttu-id="f9942-178">Aqui é Olá por trás do código da seção de nosso programa U-SQL:</span><span class="sxs-lookup"><span data-stu-id="f9942-178">Here is hello code-behind section of our U-SQL program:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;

namespace USQLApplication21
{
    public class UserSession
    {
        static public string globalSession;
        static public string StampUserSession(string eventTime, string PreviousRow, string Session)
        {

            if (!string.IsNullOrEmpty(PreviousRow))
            {
                double timeGap = Convert.ToDateTime(eventTime).Subtract(Convert.ToDateTime(PreviousRow)).TotalMinutes;
                if (timeGap <= 60) {return Session;}
                else {return Guid.NewGuid().ToString();}
            }
            else {return Guid.NewGuid().ToString();}

        }

        static public string getStampUserSession(string Session)
        {
            if (Session != globalSession && !string.IsNullOrEmpty(Session)) { globalSession = Session; }
            return globalSession;
        }

    }
}
```

<span data-ttu-id="f9942-179">Este exemplo mostra Olá variável global `static public string globalSession;` usada dentro de saudação `getStampUserSession` função e Obtendo reinicializada cada sessão de parâmetro for alterado de saudação do tempo.</span><span class="sxs-lookup"><span data-stu-id="f9942-179">This example shows hello global variable `static public string globalSession;` used inside hello `getStampUserSession` function and getting reinitialized each time hello Session parameter is changed.</span></span>

<span data-ttu-id="f9942-180">Olá U-SQL script base é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f9942-180">hello U-SQL base script is as follows:</span></span>

```
DECLARE @in string = @"\UserSession\test1.tsv";
DECLARE @out1 string = @"\UserSession\Out1.csv";
DECLARE @out2 string = @"\UserSession\Out2.csv";
DECLARE @out3 string = @"\UserSession\Out3.csv";

@records =
    EXTRACT DataId string,
            EventDateTime string,           
            UserName string,
            UserSessionTimestamp string

    FROM @in
    USING Extractors.Tsv();

@rs1 =
    SELECT 
        EventDateTime,
        UserName,
    LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,          
        string.IsNullOrEmpty(LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,           
        USQLApplication21.UserSession.StampUserSession
           (
            EventDateTime,
            LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC),
            LAG(UserSessionTimestamp, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)
           ) AS UserSessionTimestamp
    FROM @records;

@rs2 =
    SELECT 
        EventDateTime,
        UserName,
        LAG(EventDateTime, 1) 
        OVER(PARTITION BY UserName ORDER BY EventDateTime ASC) AS prevDateTime,
        string.IsNullOrEmpty( LAG(EventDateTime, 1) OVER(PARTITION BY UserName ORDER BY EventDateTime ASC)) AS Flag,
        USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp) AS UserSessionTimestamp
    FROM @rs1
    WHERE UserName != "UserName";

OUTPUT @rs2
    too@out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="f9942-181">Função `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` é chamado aqui durante o cálculo de conjunto de linhas de memória segundo hello.</span><span class="sxs-lookup"><span data-stu-id="f9942-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during hello second memory rowset calculation.</span></span> <span data-ttu-id="f9942-182">Ele passa Olá `UserSessionTimestamp` Olá valor até que a coluna e retorna `UserSessionTimestamp` foi alterado.</span><span class="sxs-lookup"><span data-stu-id="f9942-182">It passes hello `UserSessionTimestamp` column and returns hello value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="f9942-183">arquivo de saída de saudação é da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f9942-183">hello output file is as follows:</span></span>

```
"2016-02-19T07:32:36.8420000-08:00","User1",,True,"72a0660e-22df-428e-b672-e0977007177f"
"2016-02-17T11:52:43.6350000-08:00","User2",,True,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-17T11:59:08.8320000-08:00","User2","2016-02-17T11:52:43.6350000-08:00",False,"4a0cd19a-6e67-4d95-a119-4eda590226ba"
"2016-02-11T07:04:17.2630000-08:00","User3",,True,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-11T07:10:33.9720000-08:00","User3","2016-02-11T07:04:17.2630000-08:00",False,"51860a7a-1610-4f74-a9ea-69d5eef7cd9c"
"2016-02-15T21:27:41.8210000-08:00","User3","2016-02-11T07:10:33.9720000-08:00",False,"4d2bc48d-bdf3-4591-a9c1-7b15ceb8e074"
"2016-02-16T05:48:49.6360000-08:00","User3","2016-02-15T21:27:41.8210000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-16T06:22:43.6390000-08:00","User3","2016-02-16T05:48:49.6360000-08:00",False,"dd3006d0-2dcd-42d0-b3a2-bc03dd77c8b9"
"2016-02-17T16:29:53.2280000-08:00","User3","2016-02-16T06:22:43.6390000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T16:39:07.2430000-08:00","User3","2016-02-17T16:29:53.2280000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-17T17:20:39.3220000-08:00","User3","2016-02-17T16:39:07.2430000-08:00",False,"2fa899c7-eecf-4b1b-a8cd-30c5357b4f3a"
"2016-02-19T05:23:54.5710000-08:00","User3","2016-02-17T17:20:39.3220000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T05:48:37.7510000-08:00","User3","2016-02-19T05:23:54.5710000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T06:40:27.4830000-08:00","User3","2016-02-19T05:48:37.7510000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T07:27:37.7550000-08:00","User3","2016-02-19T06:40:27.4830000-08:00",False,"6ca7ed80-c149-4c22-b24b-94ff5b0d824d"
"2016-02-19T19:35:40.9450000-08:00","User3","2016-02-19T07:27:37.7550000-08:00",False,"3f385f0b-3e68-4456-ac74-ff6cef093674"
"2016-02-20T00:07:37.8250000-08:00","User3","2016-02-19T19:35:40.9450000-08:00",False,"685f76d5-ca48-4c58-b77d-bd3a9ddb33da"
"2016-02-11T09:01:33.9720000-08:00","User4",,True,"9f0cf696-c8ba-449a-8d5f-1ca6ed8f2ee8"
"2016-02-17T06:30:38.6210000-08:00","User4","2016-02-11T09:01:33.9720000-08:00",False,"8b11fd2a-01bf-4a5e-a9af-3c92c4e4382a"
"2016-02-17T22:15:26.4020000-08:00","User4","2016-02-17T06:30:38.6210000-08:00",False,"4e1cb707-3b5f-49c1-90c7-9b33b86ca1f4"
"2016-02-18T14:37:27.6560000-08:00","User4","2016-02-17T22:15:26.4020000-08:00",False,"f4e44400-e837-40ed-8dfd-2ea264d4e338"
"2016-02-19T01:20:31.4800000-08:00","User4","2016-02-18T14:37:27.6560000-08:00",False,"2136f4cf-7c7d-43c1-8ae2-08f4ad6a6e08"
```

<span data-ttu-id="f9942-184">Este exemplo demonstra um cenário de caso de uso mais complicado que usamos uma variável global dentro de uma seção de lógica que é o conjunto de linhas do toohello aplicada memória inteira.</span><span class="sxs-lookup"><span data-stu-id="f9942-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied toohello entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="f9942-185">Tipos de CLR definidos pelo usuário: UDT</span><span class="sxs-lookup"><span data-stu-id="f9942-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="f9942-186">Os tipos definidos pelo usuário, ou UDT, são outro recurso de programação do U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f9942-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="f9942-187">O UDT do U-SQL atua como um tipo definido pelo usuário regular de C#.</span><span class="sxs-lookup"><span data-stu-id="f9942-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="f9942-188">C# é uma linguagem fortemente tipada que permite o uso de saudação de tipos internos e personalizados definidos pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-188">C# is a strongly typed language that allows hello use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="f9942-189">U-SQL implicitamente não é possível serializar ou desserializar UDTs arbitrários quando Olá UDT é transmitido entre vértices em conjuntos de linhas.</span><span class="sxs-lookup"><span data-stu-id="f9942-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when hello UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="f9942-190">Isso significa que o usuário Olá tem tooprovide um formatador explícita usando Olá IFormatter interface.</span><span class="sxs-lookup"><span data-stu-id="f9942-190">This means that hello user has tooprovide an explicit formatter by using hello IFormatter interface.</span></span> <span data-ttu-id="f9942-191">Isso fornece U-SQL com hello serializar e desserializar métodos para Olá UDT.</span><span class="sxs-lookup"><span data-stu-id="f9942-191">This provides U-SQL with hello serialize and de-serialize methods for hello UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="f9942-192">U-SQL Extratores internos e outputters atualmente não é possível serializar ou desserializar tooor de dados UDT de arquivos mesmo com hello IFormatter conjunto.</span><span class="sxs-lookup"><span data-stu-id="f9942-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data tooor from files even with hello IFormatter set.</span></span> <span data-ttu-id="f9942-193">Portanto, quando você está escrevendo o arquivo de tooa dados UDT com hello declaração de saída ou lê-lo com um extrator, você tem toopass-lo como uma cadeia de caracteres ou matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="f9942-193">So when you're writing UDT data tooa file with hello OUTPUT statement, or reading it with an extractor, you have toopass it as a string or byte array.</span></span> <span data-ttu-id="f9942-194">Em seguida, você chamar serialização hello e a desserialização de código (ou seja, o método ToString () de saudação do UDT) explicitamente.</span><span class="sxs-lookup"><span data-stu-id="f9942-194">Then you call hello serialization and deserialization code (that is, hello UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="f9942-195">Extratores definidas pelo usuário e outputters em outros Olá mão, podem ler e gravar UDTs.</span><span class="sxs-lookup"><span data-stu-id="f9942-195">User-defined extractors and outputters, on hello other hand, can read and write UDTs.</span></span>

<span data-ttu-id="f9942-196">Se tentarmos toouse UDT EXTRATOR ou OUTPUTTER (fora da seleção anterior), conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="f9942-196">If we try toouse UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="f9942-197">Recebemos Olá erro a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9942-197">We receive hello following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used toooutput column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how tooserialize this type, or call a serialization method on hello type in
hello preceding SELECT. C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="f9942-198">toowork com UDT no outputter, podemos ter tooserialize-toostring com hello método ToString () ou criar um outputter personalizado.</span><span class="sxs-lookup"><span data-stu-id="f9942-198">toowork with UDT in outputter, we either have tooserialize it toostring with hello ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="f9942-199">Atualmente, os UDTs não podem ser usados em GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="f9942-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="f9942-200">Se o UDT é usado em GROUP BY, Olá erro a seguir é gerada:</span><span class="sxs-lookup"><span data-stu-id="f9942-200">If UDT is used in GROUP BY, hello following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want toouse with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="f9942-201">toodefine um UDT, temos:</span><span class="sxs-lookup"><span data-stu-id="f9942-201">toodefine a UDT, we have to:</span></span>

* <span data-ttu-id="f9942-202">Adicione Olá namespaces a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9942-202">Add hello following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="f9942-203">Adicionar `Microsoft.Analytics.Interfaces`, que é necessário para as interfaces UDT de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9942-203">Add `Microsoft.Analytics.Interfaces`, which is required for hello UDT interfaces.</span></span> <span data-ttu-id="f9942-204">Além disso, `System.IO` pode ser a interface de IFormatter Olá toodefine necessários.</span><span class="sxs-lookup"><span data-stu-id="f9942-204">In addition, `System.IO` might be needed toodefine hello IFormatter interface.</span></span>

* <span data-ttu-id="f9942-205">Defina o tipo definido usado com o atributo SqlUserDefinedType.</span><span class="sxs-lookup"><span data-stu-id="f9942-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="f9942-206">**SqlUserDefinedType** é toomark usada uma definição de tipo em um assembly como um tipo definido pelo usuário (UDT) em U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f9942-206">**SqlUserDefinedType** is used toomark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="f9942-207">Propriedades de saudação no atributo Olá refletem características físicas de saudação do hello UDT.</span><span class="sxs-lookup"><span data-stu-id="f9942-207">hello properties on hello attribute reflect hello physical characteristics of hello UDT.</span></span> <span data-ttu-id="f9942-208">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="f9942-208">This class cannot be inherited.</span></span>

<span data-ttu-id="f9942-209">SqlUserDefinedType é um atributo necessário para a definição de UDT.</span><span class="sxs-lookup"><span data-stu-id="f9942-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="f9942-210">Construtor de saudação da classe hello:</span><span class="sxs-lookup"><span data-stu-id="f9942-210">hello constructor of hello class:</span></span>  

* <span data-ttu-id="f9942-211">SqlUserDefinedTypeAttribute(type formatter)</span><span class="sxs-lookup"><span data-stu-id="f9942-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="f9942-212">Formatador do tipo: necessário parâmetro toodefine um formatador UDT — especificamente, o tipo de saudação da saudação `IFormatter` interface deve ser passada aqui.</span><span class="sxs-lookup"><span data-stu-id="f9942-212">Type formatter: Required parameter toodefine an UDT formatter--specifically, hello type of hello `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="f9942-213">UDT típico também requer a definição da interface de IFormatter hello, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f9942-213">Typical UDT also requires definition of hello IFormatter interface, as shown in hello following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="f9942-214">Olá `IFormatter` interface serializa e desfaz a serialização de um gráfico de objeto com tipo de raiz de saudação do \<typeparamref name = "T" >.</span><span class="sxs-lookup"><span data-stu-id="f9942-214">hello `IFormatter` interface serializes and de-serializes an object graph with hello root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="f9942-215">\<typeparam name = "T" > Olá tipo raiz para Olá objeto gráfico tooserialize e desserializar.</span><span class="sxs-lookup"><span data-stu-id="f9942-215">\<typeparam name="T">hello root type for hello object graph tooserialize and de-serialize.</span></span>

* <span data-ttu-id="f9942-216">**Desserializar**: desfaz a serialização de dados Olá fluxo Olá fornecido e reconstitui gráfico Olá de objetos.</span><span class="sxs-lookup"><span data-stu-id="f9942-216">**Deserialize**: De-serializes hello data on hello provided stream and reconstitutes hello graph of objects.</span></span>

* <span data-ttu-id="f9942-217">**Serializar**: serializa um objeto ou o gráfico de objetos, com hello recebe o fluxo de toohello fornecido de raiz.</span><span class="sxs-lookup"><span data-stu-id="f9942-217">**Serialize**: Serializes an object, or graph of objects, with hello given root toohello provided stream.</span></span>

<span data-ttu-id="f9942-218">`MyType`instância: instância de tipo hello.</span><span class="sxs-lookup"><span data-stu-id="f9942-218">`MyType` instance: Instance of hello type.</span></span>  
<span data-ttu-id="f9942-219">`IColumnWriter`Gravador / `IColumnReader` leitor: Olá subjacente de fluxo de coluna.</span><span class="sxs-lookup"><span data-stu-id="f9942-219">`IColumnWriter` writer / `IColumnReader` reader: hello underlying column stream.</span></span>  
<span data-ttu-id="f9942-220">`ISerializationContext`contexto: Enum que define um conjunto de sinalizadores que especifica o contexto de origem ou destino de saudação de fluxo Olá durante a serialização.</span><span class="sxs-lookup"><span data-stu-id="f9942-220">`ISerializationContext` context: Enum that defines a set of flags that specifies hello source or destination context for hello stream during serialization.</span></span>

* <span data-ttu-id="f9942-221">**Intermediário**: Especifica o contexto Olá origem ou destino não é um armazenamento persistente.</span><span class="sxs-lookup"><span data-stu-id="f9942-221">**Intermediate**: Specifies that hello source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="f9942-222">**Persistência**: Especifica o contexto Olá origem ou destino é um armazenamento persistente.</span><span class="sxs-lookup"><span data-stu-id="f9942-222">**Persistence**: Specifies that hello source or destination context is a persisted store.</span></span>

<span data-ttu-id="f9942-223">Como um tipo C# regular, uma definição de UDT do U-SQL pode incluir substituições para operadores como +/==/!=.</span><span class="sxs-lookup"><span data-stu-id="f9942-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="f9942-224">Ele também pode incluir métodos estáticos.</span><span class="sxs-lookup"><span data-stu-id="f9942-224">It can also include static methods.</span></span> <span data-ttu-id="f9942-225">Por exemplo, se formos toouse desse UDT como uma função de agregação MIN U-SQL de tooa do parâmetro, temos toodefine < substituição de operador.</span><span class="sxs-lookup"><span data-stu-id="f9942-225">For example, if we are going toouse this UDT as a parameter tooa U-SQL MIN aggregate function, we have toodefine < operator override.</span></span>

<span data-ttu-id="f9942-226">Neste guia, demonstramos um exemplo de identificação do período fiscal de data de saudação específica no formato Olá Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="f9942-226">Earlier in this guide, we demonstrated an example for fiscal period identification from hello specific date in hello format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="f9942-227">saudação de exemplo a seguir mostra como toodefine um tipo personalizado para os valores do período fiscais.</span><span class="sxs-lookup"><span data-stu-id="f9942-227">hello following example shows how toodefine a custom type for fiscal period values.</span></span>

<span data-ttu-id="f9942-228">Abaixo temos um exemplo de uma seção code-behind com interface IFormatter e UDT personalizado:</span><span class="sxs-lookup"><span data-stu-id="f9942-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

```
[SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
public struct FiscalPeriod
{
    public int Quarter { get; private set; }

    public int Month { get; private set; }

    public FiscalPeriod(int quarter, int month):this()
    {
    this.Quarter = quarter;
    this.Month = month;
    }

    public override bool Equals(object obj)
    {
    if (ReferenceEquals(null, obj))
    {
        return false;
    }

    return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
    }

    public bool Equals(FiscalPeriod other)
    {
return this.Quarter.Equals(other.Quarter) && this.Month.Equals(other.Month);
    }

    public bool GreaterThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
    }

    public bool LessThan(FiscalPeriod other)
    {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
    }

    public override int GetHashCode()
    {
    unchecked
    {
        return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
    }
    }

    public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
    {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
    }

    public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.Equals(c2);
    }

    public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
    {
    return !c1.Equals(c2);
    }
    public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.GreaterThan(c2);
    }
    public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
    {
    return c1.LessThan(c2);
    }
    public override string ToString()
    {
    return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
    }

}

public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
{
    public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
    {
    using (var binaryWriter = new BinaryWriter(writer.BaseStream))
    {
        binaryWriter.Write(instance.Quarter);
        binaryWriter.Write(instance.Month);
        binaryWriter.Flush();
    }
    }

    public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
    {
    using (var binaryReader = new BinaryReader(reader.BaseStream))
    {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
        return result;
    }
    }
}
```

<span data-ttu-id="f9942-229">tipo definido Hello inclui dois números: trimestre e mês.</span><span class="sxs-lookup"><span data-stu-id="f9942-229">hello defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="f9942-230">Os operadores ==/!=/>/< e o método estático ToString() são definidos aqui.</span><span class="sxs-lookup"><span data-stu-id="f9942-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="f9942-231">Como mencionado anteriormente, o UDT pode ser usado nas expressões SELECT, mas não pode ser usado em OUTPUTTER/EXTRACTOR sem serialização personalizada.</span><span class="sxs-lookup"><span data-stu-id="f9942-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="f9942-232">Ele tem toobe serializado como uma cadeia de caracteres com ToString () ou usados com um OUTPUTTER/EXTRATOR personalizado.</span><span class="sxs-lookup"><span data-stu-id="f9942-232">It either has toobe serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="f9942-233">Agora, vamos falar sobre o uso do UDT.</span><span class="sxs-lookup"><span data-stu-id="f9942-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="f9942-234">Em uma seção de lógica, alteramos nossas seguinte de toohello GetFiscalPeriod função:</span><span class="sxs-lookup"><span data-stu-id="f9942-234">In a code-behind section, we changed our GetFiscalPeriod function toohello following:</span></span>

```
public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
{
    int FiscalMonth = 0;
    if (dt.Month < 7)
    {
    FiscalMonth = dt.Month + 6;
    }
    else
    {
    FiscalMonth = dt.Month - 6;
    }

    int FiscalQuarter = 0;
    if (FiscalMonth >= 1 && FiscalMonth <= 3)
    {
    FiscalQuarter = 1;
    }
    if (FiscalMonth >= 4 && FiscalMonth <= 6)
    {
    FiscalQuarter = 2;
    }
    if (FiscalMonth >= 7 && FiscalMonth <= 9)
    {
    FiscalQuarter = 3;
    }
    if (FiscalMonth >= 10 && FiscalMonth <= 12)
    {
    FiscalQuarter = 4;
    }

    return new FiscalPeriod(FiscalQuarter, FiscalMonth);
}
```

<span data-ttu-id="f9942-235">Como você pode ver, ele retorna o valor de saudação do nosso tipo FiscalPeriod.</span><span class="sxs-lookup"><span data-stu-id="f9942-235">As you can see, it returns hello value of our FiscalPeriod type.</span></span>

<span data-ttu-id="f9942-236">Aqui, fornecemos um exemplo de como a toouse-lo posteriormente no script base U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f9942-236">Here we provide an example of how toouse it further in U-SQL base script.</span></span> <span data-ttu-id="f9942-237">Este exemplo demonstra as diferentes formas de invocação do UDT no script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f9942-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

```
DECLARE @input_file string = @"c:\work\cosmos\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"c:\work\cosmos\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        guid string,
        dt DateTime,
        user String,
        des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT 
        guid AS start_id,
        dt,
        DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Quarter AS fiscalquarter,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).Month AS fiscalmonth,
        USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt) + new USQL_Programmability.CustomFunctions.FiscalPeriod(1,7) AS fiscalperiod_adjusted,
        user,
        des
    FROM @rs0;

@rs2 =
    SELECT 
           start_id,
           dt,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           fiscalquarter,
           fiscalmonth,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS fiscalperiod,

       // This user-defined type was created in hello prior SELECT.  Passing hello UDT toothis subsequent SELECT would have failed if hello UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```

<span data-ttu-id="f9942-238">Veja um exemplo de uma seção completa code-behind:</span><span class="sxs-lookup"><span data-stu-id="f9942-238">Here's an example of a full code-behind section:</span></span>

```
using Microsoft.Analytics.Interfaces;
using Microsoft.Analytics.Types.Sql;
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.IO;

namespace USQL_Programmability
{
    public class CustomFunctions
    {
        static public DateTime? ToDateTime(string dt)
        {
            DateTime dtValue;

            if (!DateTime.TryParse(dt, out dtValue))
                return Convert.ToDateTime(dt);
            else
                return null;
        }

        public static FiscalPeriod GetFiscalPeriodWithCustomType(DateTime dt)
        {
            int FiscalMonth = 0;
            if (dt.Month < 7)
            {
                FiscalMonth = dt.Month + 6;
            }
            else
            {
                FiscalMonth = dt.Month - 6;
            }

            int FiscalQuarter = 0;
            if (FiscalMonth >= 1 && FiscalMonth <= 3)
            {
                FiscalQuarter = 1;
            }
            if (FiscalMonth >= 4 && FiscalMonth <= 6)
            {
                FiscalQuarter = 2;
            }
            if (FiscalMonth >= 7 && FiscalMonth <= 9)
            {
                FiscalQuarter = 3;
            }
            if (FiscalMonth >= 10 && FiscalMonth <= 12)
            {
                FiscalQuarter = 4;
            }

            return new FiscalPeriod(FiscalQuarter, FiscalMonth);
        }



        [SqlUserDefinedType(typeof(FiscalPeriodFormatter))]
        public struct FiscalPeriod
        {
            public int Quarter { get; private set; }

            public int Month { get; private set; }

            public FiscalPeriod(int quarter, int month):this()
            {
                this.Quarter = quarter;
                this.Month = month;
            }

            public override bool Equals(object obj)
            {
                if (ReferenceEquals(null, obj))
                {
                    return false;
                }

                return obj is FiscalPeriod && Equals((FiscalPeriod)obj);
            }

            public bool Equals(FiscalPeriod other)
            {
return this.Quarter.Equals(other.Quarter) &&    this.Month.Equals(other.Month);
            }

            public bool GreaterThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) > 0 || this.Month.CompareTo(other.Month) > 0;
            }

            public bool LessThan(FiscalPeriod other)
            {
return this.Quarter.CompareTo(other.Quarter) < 0 || this.Month.CompareTo(other.Month) < 0;
            }

            public override int GetHashCode()
            {
                unchecked
                {
                    return (this.Quarter.GetHashCode() * 397) ^ this.Month.GetHashCode();
                }
            }

            public static FiscalPeriod operator +(FiscalPeriod c1, FiscalPeriod c2)
            {
return new FiscalPeriod((c1.Quarter + c2.Quarter) > 4 ? (c1.Quarter + c2.Quarter)-4 : (c1.Quarter + c2.Quarter), (c1.Month + c2.Month) > 12 ? (c1.Month + c2.Month) - 12 : (c1.Month + c2.Month));
            }

            public static bool operator ==(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.Equals(c2);
            }

            public static bool operator !=(FiscalPeriod c1, FiscalPeriod c2)
            {
                return !c1.Equals(c2);
            }
            public static bool operator >(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.GreaterThan(c2);
            }
            public static bool operator <(FiscalPeriod c1, FiscalPeriod c2)
            {
                return c1.LessThan(c2);
            }
            public override string ToString()
            {
                return (String.Format("Q{0}:P{1}", this.Quarter, this.Month));
            }

        }

        public class FiscalPeriodFormatter : IFormatter<FiscalPeriod>
        {
public void Serialize(FiscalPeriod instance, IColumnWriter writer, ISerializationContext context)
            {
                using (var binaryWriter = new BinaryWriter(writer.BaseStream))
                {
                    binaryWriter.Write(instance.Quarter);
                    binaryWriter.Write(instance.Month);
                    binaryWriter.Flush();
                }
            }

public FiscalPeriod Deserialize(IColumnReader reader, ISerializationContext context)
            {
                using (var binaryReader = new BinaryReader(reader.BaseStream))
                {
var result = new FiscalPeriod(binaryReader.ReadInt16(), binaryReader.ReadInt16());
                    return result;
                }
            }
        }
    }
}
```

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="f9942-239">Use agregações definidas pelo usuário: UDAGG</span><span class="sxs-lookup"><span data-stu-id="f9942-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="f9942-240">As agregações definidas pelo usuário são funções relacionadas à agregação que não são enviadas para uso imediato com o U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f9942-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="f9942-241">exemplo Hello pode ser uma agregação tooperform matemáticas personalizadas cálculos concatenações, manipulações de cadeias de caracteres e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="f9942-241">hello example can be an aggregate tooperform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="f9942-242">a definição de classe base de agregação definida pelo usuário Olá é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f9942-242">hello user-defined aggregate base class definition is as follows:</span></span>

```c#
    [SqlUserDefinedAggregate]
    public abstract class IAggregate<T1, T2, TResult> : IAggregate
    {
        protected IAggregate();

        public abstract void Accumulate(T1 t1, T2 t2);
        public abstract void Init();
        public abstract TResult Terminate();
    }
```

<span data-ttu-id="f9942-243">**SqlUserDefinedAggregate** indica que o tipo de saudação deve ser registrado como uma agregação definida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-243">**SqlUserDefinedAggregate** indicates that hello type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="f9942-244">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="f9942-244">This class cannot be inherited.</span></span>

<span data-ttu-id="f9942-245">O atributo SqlUserDefinedType é **opcional** para a definição de UDAGG.</span><span class="sxs-lookup"><span data-stu-id="f9942-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="f9942-246">Olá classe base permite que você toopass três parâmetros de abstrata: dois como parâmetros de entrada e outra como resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9942-246">hello base class allows you toopass three abstract parameters: two as input parameters and one as hello result.</span></span> <span data-ttu-id="f9942-247">tipos de dados de saudação são variáveis e devem ser definidos durante a herança de classe.</span><span class="sxs-lookup"><span data-stu-id="f9942-247">hello data types are variable and should be defined during class inheritance.</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    { … }

    public override void Accumulate(string guid, string user)
    { … }

    public override string Terminate()
    { … }
}
```

* <span data-ttu-id="f9942-248">**Init** é invocado uma vez para cada grupo durante o cálculo.</span><span class="sxs-lookup"><span data-stu-id="f9942-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="f9942-249">Ele fornece uma rotina de inicialização para cada grupo de agregação.</span><span class="sxs-lookup"><span data-stu-id="f9942-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="f9942-250">**Accumulate** é executado uma vez para cada valor.</span><span class="sxs-lookup"><span data-stu-id="f9942-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="f9942-251">Ele fornece funcionalidade principal Olá para o algoritmo de agregação de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9942-251">It provides hello main functionality for hello aggregation algorithm.</span></span> <span data-ttu-id="f9942-252">Pode ser usado tooaggregate valores com vários tipos de dados que são definidos durante a herança de classe.</span><span class="sxs-lookup"><span data-stu-id="f9942-252">It can be used tooaggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="f9942-253">Ele pode aceitar dois parâmetros de tipos de dados variáveis.</span><span class="sxs-lookup"><span data-stu-id="f9942-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="f9942-254">**Encerrar** é executada uma vez por grupo de agregação no final de saudação do processamento toooutput Olá resultado para cada grupo.</span><span class="sxs-lookup"><span data-stu-id="f9942-254">**Terminate** is executed once per aggregation group at hello end of processing toooutput hello result for each group.</span></span>

<span data-ttu-id="f9942-255">entrada correta toodeclare e tipos de dados de saída, use a definição de classe hello como segue:</span><span class="sxs-lookup"><span data-stu-id="f9942-255">toodeclare correct input and output data types, use hello class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="f9942-256">T1: Primeiro parâmetro tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="f9942-256">T1: First parameter tooaccumulate</span></span>
* <span data-ttu-id="f9942-257">T2: Primeiro parâmetro tooaccumulate</span><span class="sxs-lookup"><span data-stu-id="f9942-257">T2: First parameter tooaccumulate</span></span>
* <span data-ttu-id="f9942-258">TResult: tipo de retorno de terminate</span><span class="sxs-lookup"><span data-stu-id="f9942-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="f9942-259">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f9942-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="f9942-260">ou o</span><span class="sxs-lookup"><span data-stu-id="f9942-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="f9942-261">Usar UDAGG no U-SQL</span><span class="sxs-lookup"><span data-stu-id="f9942-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="f9942-262">primeiro, toouse UDAGG, defini-lo no code-behind ou fazer referência de programação existente de saudação DLL conforme discutido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="f9942-262">toouse UDAGG, first define it in code-behind or reference it from hello existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="f9942-263">Em seguida, use Olá sintaxe a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9942-263">Then use hello following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="f9942-264">Veja um exemplo de UDAGG:</span><span class="sxs-lookup"><span data-stu-id="f9942-264">Here is an example of UDAGG:</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
{
    string guid_agg;

    public override void Init()
    {
        guid_agg = "";
    }

    public override void Accumulate(string guid, string user)
    {
        if (user.ToUpper()== "USER1")
        {
        guid_agg += "{" + guid + "}";
        }
    }

    public override string Terminate()
    {
        return guid_agg;
    }

}
```

<span data-ttu-id="f9942-265">E o script base U-SQL:</span><span class="sxs-lookup"><span data-stu-id="f9942-265">And base U-SQL script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @" \usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    SELECT
        user,
        AGG<USQL_Programmability.GuidAggregate>(guid,user) AS guid_list
    FROM @rs0
    GROUP BY user;

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

<span data-ttu-id="f9942-266">Neste cenário de caso de uso, podemos concatenar GUIDs de classe para usuários específicos hello.</span><span class="sxs-lookup"><span data-stu-id="f9942-266">In this use-case scenario, we concatenate class GUIDs for hello specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="f9942-267">Usar objetos definidos pelo usuário: UDO</span><span class="sxs-lookup"><span data-stu-id="f9942-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="f9942-268">U-SQL permite que objetos de programação personalizada toodefine, que são chamados objetos definidos pelo usuário ou do UDO.</span><span class="sxs-lookup"><span data-stu-id="f9942-268">U-SQL enables you toodefine custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="f9942-269">a seguir Olá é uma lista de UDO em U-SQL:</span><span class="sxs-lookup"><span data-stu-id="f9942-269">hello following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="f9942-270">Extratores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="f9942-270">User-defined extractors</span></span>
    * <span data-ttu-id="f9942-271">Extrair linha por linha</span><span class="sxs-lookup"><span data-stu-id="f9942-271">Extract row by row</span></span>
    * <span data-ttu-id="f9942-272">Usado tooimplement extração de dados de arquivos estruturados personalizados</span><span class="sxs-lookup"><span data-stu-id="f9942-272">Used tooimplement data extraction from custom structured files</span></span>

* <span data-ttu-id="f9942-273">Outputters definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="f9942-273">User-defined outputters</span></span>
    * <span data-ttu-id="f9942-274">Gerar linha por linha</span><span class="sxs-lookup"><span data-stu-id="f9942-274">Output row by row</span></span>
    * <span data-ttu-id="f9942-275">Usado toooutput tipos de dados personalizados ou formatos de arquivo personalizados</span><span class="sxs-lookup"><span data-stu-id="f9942-275">Used toooutput custom data types or custom file formats</span></span>

* <span data-ttu-id="f9942-276">Processadores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="f9942-276">User-defined processors</span></span>
    * <span data-ttu-id="f9942-277">Usar uma linha e gerar uma linha</span><span class="sxs-lookup"><span data-stu-id="f9942-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="f9942-278">Tooreduce usado Olá o número de colunas ou produzir novas colunas com valores que são derivados de um conjunto de coluna existente</span><span class="sxs-lookup"><span data-stu-id="f9942-278">Used tooreduce hello number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="f9942-279">Aplicadores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="f9942-279">User-defined appliers</span></span>
    * <span data-ttu-id="f9942-280">Coloque uma linha e produzir 0 linhas toon</span><span class="sxs-lookup"><span data-stu-id="f9942-280">Take one row and produce 0 toon rows</span></span>
    * <span data-ttu-id="f9942-281">Usado com OUTER/CROSS APPLY</span><span class="sxs-lookup"><span data-stu-id="f9942-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="f9942-282">Combinadores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="f9942-282">User-defined combiners</span></span>
    * <span data-ttu-id="f9942-283">Combina conjuntos de linhas — JOINs definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="f9942-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="f9942-284">Redutores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="f9942-284">User-defined reducers</span></span>
    * <span data-ttu-id="f9942-285">Usar n linhas e gerar uma linha</span><span class="sxs-lookup"><span data-stu-id="f9942-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="f9942-286">Usado tooreduce Olá número de linhas</span><span class="sxs-lookup"><span data-stu-id="f9942-286">Used tooreduce hello number of rows</span></span>

<span data-ttu-id="f9942-287">UDO é geralmente chamado explicitamente no script U-SQL como parte da saudação instruções U-SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9942-287">UDO is typically called explicitly in U-SQL script as part of hello following U-SQL statements:</span></span>

* <span data-ttu-id="f9942-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="f9942-288">EXTRACT</span></span>
* <span data-ttu-id="f9942-289">OUTPUT</span><span class="sxs-lookup"><span data-stu-id="f9942-289">OUTPUT</span></span>
* <span data-ttu-id="f9942-290">PROCESS</span><span class="sxs-lookup"><span data-stu-id="f9942-290">PROCESS</span></span>
* <span data-ttu-id="f9942-291">COMBINE</span><span class="sxs-lookup"><span data-stu-id="f9942-291">COMBINE</span></span>
* <span data-ttu-id="f9942-292">REDUCE</span><span class="sxs-lookup"><span data-stu-id="f9942-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="f9942-293">UDO é limitados tooconsume 0,5 Gb memória.</span><span class="sxs-lookup"><span data-stu-id="f9942-293">UDO’s are limited tooconsume 0.5Gb memory.</span></span>  <span data-ttu-id="f9942-294">Essa limitação de memória não se aplica a toolocal execuções.</span><span class="sxs-lookup"><span data-stu-id="f9942-294">This memory limitation does not apply toolocal executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="f9942-295">Usar extratores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="f9942-295">Use user-defined extractors</span></span>
<span data-ttu-id="f9942-296">U-SQL permite que dados externos tooimport usando uma instrução de EXTRAÇÃO.</span><span class="sxs-lookup"><span data-stu-id="f9942-296">U-SQL allows you tooimport external data by using an EXTRACT statement.</span></span> <span data-ttu-id="f9942-297">Uma instrução EXTRACT pode usar extratores de UDO internos:</span><span class="sxs-lookup"><span data-stu-id="f9942-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="f9942-298">*Extractors.Text()*: fornece extração dos arquivos de texto delimitados de diferentes codificações.</span><span class="sxs-lookup"><span data-stu-id="f9942-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="f9942-299">*Extractors.Csv()*: fornece extração de arquivos CSV (valores separados por vírgula) de diferentes codificações.</span><span class="sxs-lookup"><span data-stu-id="f9942-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="f9942-300">*Extractors.Tsv()*: fornece extração de arquivos TSV (valores separados por tabulação) de diferentes codificações.</span><span class="sxs-lookup"><span data-stu-id="f9942-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="f9942-301">Ele pode ser útil toodevelop um extrator personalizado.</span><span class="sxs-lookup"><span data-stu-id="f9942-301">It can be useful toodevelop a custom extractor.</span></span> <span data-ttu-id="f9942-302">Isso pode ser útil durante a importação de dados se quisermos toodo qualquer uma das seguintes tarefas de saudação:</span><span class="sxs-lookup"><span data-stu-id="f9942-302">This can be helpful during data import if we want toodo any of hello following tasks:</span></span>

* <span data-ttu-id="f9942-303">Modificar dados de entrada ao dividir colunas e modificar os valores individuais.</span><span class="sxs-lookup"><span data-stu-id="f9942-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="f9942-304">Olá funcionalidade do processador é melhor para a combinação de colunas.</span><span class="sxs-lookup"><span data-stu-id="f9942-304">hello PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="f9942-305">Analisar dados não estruturados, como páginas da Web e emails, ou semiestruturados, como XML/JSON.</span><span class="sxs-lookup"><span data-stu-id="f9942-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="f9942-306">Analisar dados na codificação sem suporte.</span><span class="sxs-lookup"><span data-stu-id="f9942-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="f9942-307">toodefine extrator de definida pelo usuário, ou excluir, precisamos toocreate um `IExtractor` interface.</span><span class="sxs-lookup"><span data-stu-id="f9942-307">toodefine a user-defined extractor, or UDE, we need toocreate an `IExtractor` interface.</span></span> <span data-ttu-id="f9942-308">Todas as entrada extrator de toohello parâmetros, como delimitadores de coluna/linha e a codificação, precisam toobe definida no construtor de saudação da classe de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9942-308">All input parameters toohello extractor, such as column/row delimiters, and encoding, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="f9942-309">Olá `IExtractor` interface também deve conter uma definição para Olá `IEnumerable<IRow>` substituir da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f9942-309">hello `IExtractor`  interface should also contain a definition for hello `IEnumerable<IRow>` override as follows:</span></span>

```
[SqlUserDefinedExtractor]
public class SampleExtractor : IExtractor
{
     public SampleExtractor(string row_delimiter, char col_delimiter)
     { … }

     public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
     { … }
}
```

<span data-ttu-id="f9942-310">Olá **SqlUserDefinedExtractor** atributo indica que tipo de saudação deve ser registrado como um extrator definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-310">hello **SqlUserDefinedExtractor** attribute indicates that hello type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="f9942-311">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="f9942-311">This class cannot be inherited.</span></span>

<span data-ttu-id="f9942-312">SqlUserDefinedExtractor é um atributo opcional para a definição de UDE.</span><span class="sxs-lookup"><span data-stu-id="f9942-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="f9942-313">Ele usado toodefine AtomicFileProcessing propriedade para o objeto de uir hello.</span><span class="sxs-lookup"><span data-stu-id="f9942-313">It used toodefine AtomicFileProcessing property for hello UDE object.</span></span>

* <span data-ttu-id="f9942-314">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="f9942-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="f9942-315">**true** = indica que esse extrator exige arquivos de entrada atômicos (JSON, XML, ...)</span><span class="sxs-lookup"><span data-stu-id="f9942-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="f9942-316">**false** = indica que esse extrator pode lidar com arquivos divididos/distribuídos (CSV, SEQ, ...)</span><span class="sxs-lookup"><span data-stu-id="f9942-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="f9942-317">os objetos de programação uir principais Olá são **entrada** e **saída**.</span><span class="sxs-lookup"><span data-stu-id="f9942-317">hello main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="f9942-318">objeto de entrada Hello está dados de entrada usado tooenumerate como `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="f9942-318">hello input object is used tooenumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="f9942-319">saudação do objeto de saída é usada tooset dados de saída como resultado da atividade de extrator de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9942-319">hello output object is used tooset output data as a result of hello extractor activity.</span></span>

<span data-ttu-id="f9942-320">dados de entrada Hello são acessados por meio de `System.IO.Stream` e `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="f9942-320">hello input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="f9942-321">Para a enumeração de colunas de entrada do primeiro dividiremos fluxo de entrada hello usando um delimitador de linha.</span><span class="sxs-lookup"><span data-stu-id="f9942-321">For input columns enumeration, we first split hello input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="f9942-322">Em seguida, dividimos ainda mais a linha de entrada em partes de coluna.</span><span class="sxs-lookup"><span data-stu-id="f9942-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="f9942-323">dados de saída tooset, usamos Olá `output.Set` método.</span><span class="sxs-lookup"><span data-stu-id="f9942-323">tooset output data, we use hello `output.Set` method.</span></span>

<span data-ttu-id="f9942-324">É importante toounderstand que Olá extrator personalizado produz somente colunas e valores que são definidos com saída de hello.</span><span class="sxs-lookup"><span data-stu-id="f9942-324">It's important toounderstand that hello custom extractor only outputs columns and values that are defined with hello output.</span></span> <span data-ttu-id="f9942-325">Defina a chamada do método.</span><span class="sxs-lookup"><span data-stu-id="f9942-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="f9942-326">saída do Hello extrator real é disparada pela chamada `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="f9942-326">hello actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="f9942-327">O seguinte é um exemplo extrator de hello:</span><span class="sxs-lookup"><span data-stu-id="f9942-327">Following is hello extractor example:</span></span>

```
[SqlUserDefinedExtractor(AtomicFileProcessing = true)]
public class FullDescriptionExtractor : IExtractor
{
     private Encoding _encoding;
     private byte[] _row_delim;
     private char _col_delim;

    public FullDescriptionExtractor(Encoding encoding, string row_delim = "\r\n", char col_delim = '\t')
    {
         this._encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
         this._row_delim = this._encoding.GetBytes(row_delim);
         this._col_delim = col_delim;

    }

    public override IEnumerable<IRow> Extract(IUnstructuredReader input, IUpdatableRow output)
    {
         string line;
         //Read hello input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split hello input by hello column delimiter
             string[] parts = line.Split(this._col_delim);
             int count = 0; // start with first column
             foreach (string part in parts)
             {
    if (count == 0)
             {  // for column “guid”, re-generated guid
                 Guid new_guid = Guid.NewGuid();
                 output.Set<Guid>(count, new_guid);
             }
             else if (count == 2)
             {
                 // for column “user”, convert tooUPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep hello rest of hello columns as-is
                 output.Set<string>(count, part);
             }
             count += 1;
             }

         }
         yield return output.AsReadOnly();
         }
         yield break;
     }
}
```

<span data-ttu-id="f9942-328">Neste cenário de caso de uso, extrator de saudação regenera Olá GUID para a coluna "guid" e converte os valores de saudação do caso de tooupper de coluna de "usuário".</span><span class="sxs-lookup"><span data-stu-id="f9942-328">In this use-case scenario, hello extractor regenerates hello GUID for “guid” column and converts hello values of “user” column tooupper case.</span></span> <span data-ttu-id="f9942-329">Os extratores personalizados podem produzir resultados mais complicados ao analisar dados de entrada e manipulá-los.</span><span class="sxs-lookup"><span data-stu-id="f9942-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="f9942-330">Script base U-SQL que usa um extrator personalizado:</span><span class="sxs-lookup"><span data-stu-id="f9942-330">Following is base U-SQL script that uses a custom extractor:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file
        USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="f9942-331">Usar outputters definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="f9942-331">Use user-defined outputters</span></span>
<span data-ttu-id="f9942-332">Outputter definida pelo usuário é outro UDO U-SQL que permite a você uma funcionalidade interna tooextend U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f9942-332">User-defined outputter is another U-SQL UDO that allows you tooextend built-in U-SQL functionality.</span></span> <span data-ttu-id="f9942-333">Extrator de toohello semelhante, há vários outputters internos.</span><span class="sxs-lookup"><span data-stu-id="f9942-333">Similar toohello extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="f9942-334">*Outputters.Text()*: grava dados toodelimited arquivos de texto de codificações diferentes.</span><span class="sxs-lookup"><span data-stu-id="f9942-334">*Outputters.Text()*: Writes data toodelimited text files of different encodings.</span></span>
* <span data-ttu-id="f9942-335">*Outputters.Csv()*: grava arquivos de (CSV) de diferentes codificações de valor toocomma separada dos dados.</span><span class="sxs-lookup"><span data-stu-id="f9942-335">*Outputters.Csv()*: Writes data toocomma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="f9942-336">*Outputters.Tsv()*: grava arquivos de (TSV) diferentes codificações de valor tootab separada dos dados.</span><span class="sxs-lookup"><span data-stu-id="f9942-336">*Outputters.Tsv()*: Writes data tootab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="f9942-337">Outputter personalizada permite que você toowrite dados em um formato definido personalizado.</span><span class="sxs-lookup"><span data-stu-id="f9942-337">Custom outputter allows you toowrite data in a custom defined format.</span></span> <span data-ttu-id="f9942-338">Isso pode ser útil para Olá tarefas a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9942-338">This can be useful for hello following tasks:</span></span>

* <span data-ttu-id="f9942-339">Gravando arquivos de dados estruturados toosemi ou não estruturados.</span><span class="sxs-lookup"><span data-stu-id="f9942-339">Writing data toosemi-structured or unstructured files.</span></span>
* <span data-ttu-id="f9942-340">Gravar dados em codificações sem suporte.</span><span class="sxs-lookup"><span data-stu-id="f9942-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="f9942-341">Modificar dados de saída ou adicionar atributos personalizados.</span><span class="sxs-lookup"><span data-stu-id="f9942-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="f9942-342">toodefine definido pelo usuário outputter, precisamos Olá toocreate `IOutputter` interface.</span><span class="sxs-lookup"><span data-stu-id="f9942-342">toodefine user-defined outputter, we need toocreate hello `IOutputter` interface.</span></span>

<span data-ttu-id="f9942-343">A seguir é hello base `IOutputter` implementação da classe:</span><span class="sxs-lookup"><span data-stu-id="f9942-343">Following is hello base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="f9942-344">Todas as entrada parâmetros toohello outputter, como delimitadores de coluna/linha, codificação e assim por diante, precisam toobe definida no construtor de saudação da classe de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9942-344">All input parameters toohello outputter, such as column/row delimiters, encoding, and so on, need toobe defined in hello constructor of hello class.</span></span> <span data-ttu-id="f9942-345">Olá `IOutputter` interface também deve conter uma definição para `void Output` substituir.</span><span class="sxs-lookup"><span data-stu-id="f9942-345">hello `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="f9942-346">atributo Olá `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` opcionalmente pode ser definido para o processamento de arquivos atômicas.</span><span class="sxs-lookup"><span data-stu-id="f9942-346">hello attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="f9942-347">Para obter mais informações, consulte Olá detalhes a seguir.</span><span class="sxs-lookup"><span data-stu-id="f9942-347">For more information, see hello following details.</span></span>

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class MyOutputter : IOutputter
{

    public MyOutputter(myparam1, myparam2)
    {
      …
    }

    public override void Close()
    {
      …
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
      …
    }
}
```

* <span data-ttu-id="f9942-348">`Output` é chamado para cada linha de entrada.</span><span class="sxs-lookup"><span data-stu-id="f9942-348">`Output` is called for each input row.</span></span> <span data-ttu-id="f9942-349">Ele retorna Olá `IUnstructuredWriter output` conjunto de linhas.</span><span class="sxs-lookup"><span data-stu-id="f9942-349">It returns hello `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="f9942-350">Olá classe construtor é usado ao definido pelo usuário outputter de toohello de parâmetros toopass.</span><span class="sxs-lookup"><span data-stu-id="f9942-350">hello Constructor class is used toopass parameters toohello user-defined outputter.</span></span>
* <span data-ttu-id="f9942-351">`Close`é usado toooptionally substituição do estado caro toorelease ou determinar quando a última linha de saudação foi gravada.</span><span class="sxs-lookup"><span data-stu-id="f9942-351">`Close` is used toooptionally override toorelease expensive state or determine when hello last row was written.</span></span>

<span data-ttu-id="f9942-352">**SqlUserDefinedOutputter** atributo indica que o tipo de saudação deve ser registrado como um outputter definida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-352">**SqlUserDefinedOutputter** attribute indicates that hello type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="f9942-353">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="f9942-353">This class cannot be inherited.</span></span>

<span data-ttu-id="f9942-354">SqlUserDefinedOutputter é um atributo opcional para a definição de um outputter definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="f9942-355">Ele tenha usado a propriedade de AtomicFileProcessing Olá toodefine.</span><span class="sxs-lookup"><span data-stu-id="f9942-355">It's used toodefine hello AtomicFileProcessing property.</span></span>

* <span data-ttu-id="f9942-356">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="f9942-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="f9942-357">**true** = indica que esse outputter exige arquivos de saída atômicos (JSON, XML, ...)</span><span class="sxs-lookup"><span data-stu-id="f9942-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="f9942-358">**false** = indica que esse outputter pode lidar com arquivos divididos/distribuídos (CSV, SEQ, ...)</span><span class="sxs-lookup"><span data-stu-id="f9942-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="f9942-359">objetos de programação principal Olá são **linha** e **saída**.</span><span class="sxs-lookup"><span data-stu-id="f9942-359">hello main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="f9942-360">Olá **linha** objeto é usado tooenumerate dados de saída como `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="f9942-360">hello **row** object is used tooenumerate output data as `IRow` interface.</span></span> <span data-ttu-id="f9942-361">**Saída** é usado tooset arquivo de destino de toohello de dados de saída.</span><span class="sxs-lookup"><span data-stu-id="f9942-361">**Output** is used tooset output data toohello target file.</span></span>

<span data-ttu-id="f9942-362">Olá dados de saída são acessados por meio de saudação `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="f9942-362">hello output data is accessed through hello `IRow` interface.</span></span> <span data-ttu-id="f9942-363">Os dados de saída são passados em uma linha por vez.</span><span class="sxs-lookup"><span data-stu-id="f9942-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="f9942-364">valores individuais de saudação são enumerados chamando Olá Get método da interface de IRow hello:</span><span class="sxs-lookup"><span data-stu-id="f9942-364">hello individual values are enumerated by calling hello Get method of hello IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="f9942-365">Os nomes de coluna individuais podem ser determinados chamando `row.Schema`:</span><span class="sxs-lookup"><span data-stu-id="f9942-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="f9942-366">Essa abordagem permite que você toobuild um outputter flexível para qualquer esquema de metadados.</span><span class="sxs-lookup"><span data-stu-id="f9942-366">This approach enables you toobuild a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="f9942-367">Olá dados de saída são gravados toofile usando `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="f9942-367">hello output data is written toofile by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="f9942-368">parâmetro de fluxo de saudação está definido muito`output.BaseStrea` como parte do `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="f9942-368">hello stream parameter is set too`output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="f9942-369">Observe que é importante tooflush Olá dados buffer toohello arquivo depois de cada iteração de linha.</span><span class="sxs-lookup"><span data-stu-id="f9942-369">Note that it's important tooflush hello data buffer toohello file after each row iteration.</span></span> <span data-ttu-id="f9942-370">Além disso, Olá `StreamWriter` objeto deve ser usado com hello descartáveis atributo habilitado (padrão) e Olá **usando** palavra-chave:</span><span class="sxs-lookup"><span data-stu-id="f9942-370">In addition, hello `StreamWriter` object must be used with hello Disposable attribute enabled (default) and with hello **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="f9942-371">Caso contrário, chame o método Flush() explicitamente depois de cada iteração.</span><span class="sxs-lookup"><span data-stu-id="f9942-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="f9942-372">Vamos mostrar isso em Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="f9942-372">We show this in hello following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="f9942-373">Definir cabeçalhos e rodapés para outputter definido pelo usuário</span><span class="sxs-lookup"><span data-stu-id="f9942-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="f9942-374">tooset um cabeçalho, use o fluxo de execução única iteração.</span><span class="sxs-lookup"><span data-stu-id="f9942-374">tooset a header, use single iteration execution flow.</span></span>

```
public override void Output(IRow row, IUnstructuredWriter output)
{
 …
if (isHeaderRow)
{
    …                
}

 …
if (isHeaderRow)
{
    isHeaderRow = false;
}
 …
}
}
```

<span data-ttu-id="f9942-375">Olá Olá código primeiro `if (isHeaderRow)` bloco é executado apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="f9942-375">hello code in hello first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="f9942-376">Rodapé Olá, usar a instância de toohello de referência de saudação do `System.IO.Stream` objeto (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="f9942-376">For hello footer, use hello reference toohello instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="f9942-377">Gravar rodapé Olá no hello método Close () do hello `IOutputter` interface.</span><span class="sxs-lookup"><span data-stu-id="f9942-377">Write hello footer in hello Close() method of hello `IOutputter` interface.</span></span>  <span data-ttu-id="f9942-378">(Para obter mais informações, consulte Olá exemplo a seguir).</span><span class="sxs-lookup"><span data-stu-id="f9942-378">(For more information, see hello following example.)</span></span>

<span data-ttu-id="f9942-379">Veja um exemplo de um outputter definido pelo usuário:</span><span class="sxs-lookup"><span data-stu-id="f9942-379">Following is an example of a user-defined outputter:</span></span>

```
[SqlUserDefinedOutputter(AtomicFileProcessing = true)]
public class HTMLOutputter : IOutputter
{
    // Local variables initialization
    private string row_delimiter;
    private char col_delimiter;
    private bool isHeaderRow;
    private Encoding encoding;
    private bool IsTableHeader = true;
    private Stream g_writer;

    // Parameters definition            
    public HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    this.isHeaderRow = isHeader;
    this.encoding = ((encoding == null) ? Encoding.UTF8 : encoding);
    }

    // hello Close method is used toowrite hello footer toohello file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference tooIO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization tooenumerate column names
    ISchema schema = row.Schema;

    // This is a data-independent header--HTML table definition
    if (IsTableHeader)
    {
        streamWriter.Write("<table border=1>");
        IsTableHeader = false;
    }

    // HTML table attributes
    string header_wrapper_on = "<th>";
    string header_wrapper_off = "</th>";
    string data_wrapper_on = "<td>";
    string data_wrapper_off = "</td>";

    // Header row output--runs only once
    if (isHeaderRow)
    {
        streamWriter.Write("<tr>");
        for (int i = 0; i < schema.Count(); i++)
        {
        var col = schema[i];
        streamWriter.Write(header_wrapper_on + col.Name + header_wrapper_off);
        }
        streamWriter.Write("</tr>");
    }

    // Data row output
    streamWriter.Write("<tr>");                
    for (int i = 0; i < schema.Count(); i++)
    {
        var col = schema[i];
        string val = "";
        try
        {
        // Data type enumeration--required toomatch hello distinct list of types from OUTPUT statement
        switch (col.Type.Name.ToString().ToLower())
        {
            case "string": val = row.Get<string>(col.Name).ToString(); break;
            case "guid": val = row.Get<Guid>(col.Name).ToString(); break;
            default: break;
        }
        }
        // Handling NULL values--keeping them empty
        catch (System.NullReferenceException)
        {
        }
        streamWriter.Write(data_wrapper_on + val + data_wrapper_off);
    }
    streamWriter.Write("</tr>");

    if (isHeaderRow)
    {
        isHeaderRow = false;
    }
    // Reference toohello instance of hello IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define hello factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="f9942-380">E o script base U-SQL:</span><span class="sxs-lookup"><span data-stu-id="f9942-380">And U-SQL base script:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.html";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
         FROM @input_file
         USING new USQL_Programmability.FullDescriptionExtractor(Encoding.UTF8);

OUTPUT @rs0 
    too@output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="f9942-381">Esse é um outputter HTML, que cria um arquivo HTML com dados da tabela.</span><span class="sxs-lookup"><span data-stu-id="f9942-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="f9942-382">Chamando outputter do script base U-SQL</span><span class="sxs-lookup"><span data-stu-id="f9942-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="f9942-383">toocall um outputter personalizado do script U-SQL da base hello, nova instância de saudação do objeto de outputter Olá tem toobe criado.</span><span class="sxs-lookup"><span data-stu-id="f9942-383">toocall a custom outputter from hello base U-SQL script, hello new instance of hello outputter object has toobe created.</span></span>

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="f9942-384">tooavoid criando uma instância de saudação do objeto no script base, podemos criar um wrapper de função, conforme mostrado no exemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="f9942-384">tooavoid creating an instance of hello object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define hello factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="f9942-385">Nesse caso, chamada original Olá Olá seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="f9942-385">In this case, hello original call looks like hello following:</span></span>

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="f9942-386">Usar processadores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="f9942-386">Use user-defined processors</span></span>
<span data-ttu-id="f9942-387">Processador definida pelo usuário ou UDP, é um tipo de UDO U-SQL que permite que você tooprocess linhas de entrada hello aplicando recursos de programação.</span><span class="sxs-lookup"><span data-stu-id="f9942-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you tooprocess hello incoming rows by applying programmability features.</span></span> <span data-ttu-id="f9942-388">UDP permite toocombine colunas, modifique os valores e adicionar novas colunas, se necessário.</span><span class="sxs-lookup"><span data-stu-id="f9942-388">UDP enables you toocombine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="f9942-389">Basicamente, ele ajuda a tooprocess elementos de dados de tooproduce necessário um conjunto de linhas.</span><span class="sxs-lookup"><span data-stu-id="f9942-389">Basically, it helps tooprocess a rowset tooproduce required data elements.</span></span>

<span data-ttu-id="f9942-390">toodefine um UDP, precisamos toocreate um `IProcessor` interface com hello `SqlUserDefinedProcessor` atributo, que é opcional para UDP.</span><span class="sxs-lookup"><span data-stu-id="f9942-390">toodefine a UDP, we need toocreate an `IProcessor` interface with hello `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="f9942-391">Esta interface deve conter a definição de saudação para Olá `IRow` substituir o conjunto de linhas de interface, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="f9942-391">This interface should contain hello definition for hello `IRow` interface rowset override, as shown in hello following example:</span></span>

```
[SqlUserDefinedProcessor]
public class MyProcessor: IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
        …
 }
}
```

<span data-ttu-id="f9942-392">**SqlUserDefinedProcessor** indica que tipo de saudação deve ser registrado como um processador definida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-392">**SqlUserDefinedProcessor** indicates that hello type should be registered as a user-defined processor.</span></span> <span data-ttu-id="f9942-393">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="f9942-393">This class cannot be inherited.</span></span>

<span data-ttu-id="f9942-394">Olá SqlUserDefinedProcessor atributo é **opcional** para definição de UDP.</span><span class="sxs-lookup"><span data-stu-id="f9942-394">hello SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="f9942-395">objetos de programação principal Olá são **entrada** e **saída**.</span><span class="sxs-lookup"><span data-stu-id="f9942-395">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="f9942-396">objeto de entrada Hello está tooenumerate usado colunas de entrada e saída e tooset dados de saída como resultado da atividade do processador hello.</span><span class="sxs-lookup"><span data-stu-id="f9942-396">hello input object is used tooenumerate input columns and output, and tooset output data as a result of hello processor activity.</span></span>

<span data-ttu-id="f9942-397">Enumeração de colunas de entrada, usamos Olá `input.Get` método.</span><span class="sxs-lookup"><span data-stu-id="f9942-397">For input columns enumeration, we use hello `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="f9942-398">Olá parâmetro `input.Get` método é uma coluna que é passada como parte da saudação `PRODUCE` cláusula da saudação `PROCESS` instrução do script base Olá U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f9942-398">hello parameter for `input.Get` method is a column that's passed as part of hello `PRODUCE` clause of hello `PROCESS` statement of hello U-SQL base script.</span></span> <span data-ttu-id="f9942-399">Precisamos toouse aqui, o tipo de dados correto do hello.</span><span class="sxs-lookup"><span data-stu-id="f9942-399">We need toouse hello correct data type here.</span></span>

<span data-ttu-id="f9942-400">Saída, use Olá `output.Set` método.</span><span class="sxs-lookup"><span data-stu-id="f9942-400">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="f9942-401">É importante toonote que produtor personalizado gera apenas colunas e valores que são definidos com hello `output.Set` chamada de método.</span><span class="sxs-lookup"><span data-stu-id="f9942-401">It's important toonote that custom producer only outputs columns and values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="f9942-402">saída de processador real Hello é disparada pela chamada `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="f9942-402">hello actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="f9942-403">Veja abaixo um exemplo de processador:</span><span class="sxs-lookup"><span data-stu-id="f9942-403">Following is a processor example:</span></span>

```
[SqlUserDefinedProcessor]
public class FullDescriptionProcessor : IProcessor
{
public override IRow Process(IRow input, IUpdatableRow output)
 {
     string user = input.Get<string>("user");
     string des = input.Get<string>("des");
     string full_description = user.ToUpper() + "=>" + des;
     output.Set<string>("dt", input.Get<string>("dt"));
     output.Set<string>("full_description", full_description);
     output.Set<Guid>("new_guid", Guid.NewGuid());
     output.Set<Guid>("guid", input.Get<Guid>("guid"));
     return output.AsReadOnly();
 }
}
```

<span data-ttu-id="f9942-404">Neste cenário de caso de uso, o processador hello está gerando uma nova coluna chamada "full_description" combinando Olá colunas existentes – nesse caso, "usuário" em letras maiusculas e "des".</span><span class="sxs-lookup"><span data-stu-id="f9942-404">In this use-case scenario, hello processor is generating a new column called “full_description” by combining hello existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="f9942-405">Ele também gera um GUID e retorna Olá originais e novos valores GUID.</span><span class="sxs-lookup"><span data-stu-id="f9942-405">It also regenerates a GUID and returns hello original and new GUID values.</span></span>

<span data-ttu-id="f9942-406">Como você pode ver do exemplo anterior hello, você pode chamar métodos c# durante `output.Set` chamada de método.</span><span class="sxs-lookup"><span data-stu-id="f9942-406">As you can see from hello previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="f9942-407">Abaixo temos um exemplo de script base U-SQL que usa um processador personalizado:</span><span class="sxs-lookup"><span data-stu-id="f9942-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid Guid,
        dt String,
            user String,
            des String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
     PROCESS @rs0
     PRODUCE dt String,
             full_description String,
             guid Guid,
             new_guid Guid
     USING new USQL_Programmability.FullDescriptionProcessor();

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="f9942-408">Usar aplicadores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="f9942-408">Use user-defined appliers</span></span>
<span data-ttu-id="f9942-409">Um aplicador de U-SQL definida pelo usuário permite que você tooinvoke personalizado c# função para cada linha que é retornada pela expressão da tabela externa saudação de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="f9942-409">A U-SQL user-defined applier enables you tooinvoke a custom C# function for each row that's returned by hello outer table expression of a query.</span></span> <span data-ttu-id="f9942-410">entrada de saudação à direita é avaliada para cada linha da entrada esquerda hello e linhas de saudação que são produzidas são combinadas para saída final hello.</span><span class="sxs-lookup"><span data-stu-id="f9942-410">hello right input is evaluated for each row from hello left input, and hello rows that are produced are combined for hello final output.</span></span> <span data-ttu-id="f9942-411">lista de saudação de colunas que são produzidas pelo operador APPLY de saudação são a combinação de saudação de conjunto de saudação de colunas da esquerda hello e hello entrada à direita.</span><span class="sxs-lookup"><span data-stu-id="f9942-411">hello list of columns that are produced by hello APPLY operator are hello combination of hello set of columns in hello left and hello right input.</span></span>

<span data-ttu-id="f9942-412">Aplicador definido pelo usuário está sendo invocado como parte da saudação USQL selecione expressão.</span><span class="sxs-lookup"><span data-stu-id="f9942-412">User-defined applier is being invoked as part of hello USQL SELECT expression.</span></span>

<span data-ttu-id="f9942-413">Olá típica chamada toohello definida pelo usuário aplicador de alterações é semelhante Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9942-413">hello typical call toohello user-defined applier looks like hello following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="f9942-414">Para saber mais sobre como usar aplicadores na expressão SELECT., veja [U-SQL SELECT selecionando de CROSS APPLY e OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9942-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="f9942-415">definição Hello, definido pelo usuário aplicador de alterações classe base é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="f9942-415">hello user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="f9942-416">toodefine um aplicador definida pelo usuário, precisamos Olá toocreate `IApplier` interface com hello [`SqlUserDefinedApplier`] atributo, que é opcional para uma definição de aplicador de alterações definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-416">toodefine a user-defined applier, we need toocreate hello `IApplier` interface with hello [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
    public ParserApplier()
    {
        …
    }

    public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
    {
        …
    }
}
```

* <span data-ttu-id="f9942-417">Aplicar é chamado para cada linha da tabela externa hello.</span><span class="sxs-lookup"><span data-stu-id="f9942-417">Apply is called for each row of hello outer table.</span></span> <span data-ttu-id="f9942-418">Ele retorna Olá `IUpdatableRow` conjunto de linhas de saída.</span><span class="sxs-lookup"><span data-stu-id="f9942-418">It returns hello `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="f9942-419">classe de construtor Olá é toopass usados parâmetros toohello definida pelo usuário aplicador.</span><span class="sxs-lookup"><span data-stu-id="f9942-419">hello Constructor class is used toopass parameters toohello user-defined applier.</span></span>

<span data-ttu-id="f9942-420">**SqlUserDefinedApplier** indica que o tipo de saudação deve ser registrado como um aplicador definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-420">**SqlUserDefinedApplier** indicates that hello type should be registered as a user-defined applier.</span></span> <span data-ttu-id="f9942-421">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="f9942-421">This class cannot be inherited.</span></span>

<span data-ttu-id="f9942-422">O atributo **SqlUserDefinedApplier** é **opcional** para a definição do aplicador definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="f9942-423">objetos de programação principal Olá são da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="f9942-423">hello main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="f9942-424">Os conjuntos de linhas de entrada são passados como entrada `IRow`.</span><span class="sxs-lookup"><span data-stu-id="f9942-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="f9942-425">Olá linhas de saída são geradas como `IUpdatableRow` interface de saída.</span><span class="sxs-lookup"><span data-stu-id="f9942-425">hello output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="f9942-426">Nomes de coluna individuais podem ser determinados por chamada hello `IRow` método de esquema.</span><span class="sxs-lookup"><span data-stu-id="f9942-426">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="f9942-427">valores de dados reais de saudação tooget de saudação entrada `IRow`, usamos o método Get () Olá `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="f9942-427">tooget hello actual data values from hello incoming `IRow`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="f9942-428">Ou podemos usar o nome da coluna de esquema hello:</span><span class="sxs-lookup"><span data-stu-id="f9942-428">Or we use hello schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="f9942-429">Olá valores de saída devem ser definidos com `IUpdatableRow` saída:</span><span class="sxs-lookup"><span data-stu-id="f9942-429">hello output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="f9942-430">É importante toounderstand que aplicadores personalizados saída somente colunas e valores que são definidos com `output.Set` chamada de método.</span><span class="sxs-lookup"><span data-stu-id="f9942-430">It is important toounderstand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="f9942-431">saída real Olá é disparada pela chamada `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="f9942-431">hello actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="f9942-432">parâmetros aplicador de alterações da saudação definidos pelo usuário podem ser passados toohello construtor.</span><span class="sxs-lookup"><span data-stu-id="f9942-432">hello user-defined applier parameters can be passed toohello constructor.</span></span> <span data-ttu-id="f9942-433">Aplicador pode retornar um número variável de colunas que precisa toobe definida durante a chamada de saudação aplicador de alterações no Script U-SQL base.</span><span class="sxs-lookup"><span data-stu-id="f9942-433">Applier can return a variable number of columns that need toobe defined during hello applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="f9942-434">Aqui está o exemplo de aplicador de alterações definido pelo usuário hello:</span><span class="sxs-lookup"><span data-stu-id="f9942-434">Here is hello user-defined applier example:</span></span>

```
[SqlUserDefinedApplier]
public class ParserApplier : IApplier
{
private string parsingPart;

public ParserApplier(string parsingPart)
{
    if (parsingPart.ToUpper().Contains("ALL")
    || parsingPart.ToUpper().Contains("MAKE")
    || parsingPart.ToUpper().Contains("MODEL")
    || parsingPart.ToUpper().Contains("YEAR")
    || parsingPart.ToUpper().Contains("TYPE")
    || parsingPart.ToUpper().Contains("MILLAGE")
    )
    {
    this.parsingPart = parsingPart;
    }
    else
    {
    throw new ArgumentException("Incorrect parameter. Please use: 'ALL[MAKE|MODEL|TYPE|MILLAGE]'");
    }
}

public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
{

    string[] properties = input.Get<string>("properties").Split(',');

    //  only process with correct number of properties
    if (properties.Count() == 5)
    {

    string make = properties[0];
    string model = properties[1];
    string year = properties[2];
    string type = properties[3];
    int millage = -1;

    // Only return millage if it is number, otherwise, -1
    if (!int.TryParse(properties[4], out millage))
    {
        millage = -1;
    }

    if (parsingPart.ToUpper().Contains("MAKE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("make", make);
    if (parsingPart.ToUpper().Contains("MODEL") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("model", model);
    if (parsingPart.ToUpper().Contains("YEAR") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("year", year);
    if (parsingPart.ToUpper().Contains("TYPE") || parsingPart.ToUpper().Contains("ALL")) output.Set<string>("type", type);
    if (parsingPart.ToUpper().Contains("MILLAGE") || parsingPart.ToUpper().Contains("ALL")) output.Set<int>("millage", millage);
    }
    yield return output.AsReadOnly();            
}
}
```

<span data-ttu-id="f9942-435">O seguinte é script U-SQL base de saudação para este aplicador definido pelo usuário:</span><span class="sxs-lookup"><span data-stu-id="f9942-435">Following is hello base U-SQL script for this user-defined applier:</span></span>

```
DECLARE @input_file string = @"c:\usql-programmability\car_fleet.tsv";
DECLARE @output_file string = @"c:\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
        stocknumber int,
        vin String,
        properties String
    FROM @input_file USING Extractors.Tsv();

@rs1 =
    SELECT
        r.stocknumber,
        r.vin,
        properties.make,
        properties.model,
        properties.year,
        properties.type,
        properties.millage
    FROM @rs0 AS r
    CROSS APPLY
    new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);

OUTPUT @rs1 too@output_file USING Outputters.Text();
```

<span data-ttu-id="f9942-436">Neste cenário de caso de uso, definido pelo usuário aplicador de alterações funciona como um analisador de valor separado por vírgulas para carro Olá frota propriedades.</span><span class="sxs-lookup"><span data-stu-id="f9942-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for hello car fleet properties.</span></span> <span data-ttu-id="f9942-437">linhas do arquivo de entrada Hello aparência Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9942-437">hello input file rows look like hello following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="f9942-438">Trata-se de um típico arquivo TSV delimitado por tab com a coluna de propriedades contendo propriedades do carro, como fabricante e modelo.</span><span class="sxs-lookup"><span data-stu-id="f9942-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="f9942-439">Essas propriedades devem ser analisado toohello colunas da tabela.</span><span class="sxs-lookup"><span data-stu-id="f9942-439">Those properties must be parsed toohello table columns.</span></span> <span data-ttu-id="f9942-440">aplicador de saudação que é fornecido também permite que você toogenerate dinâmica várias propriedades em Olá resultam de linhas, com base no parâmetro de saudação que é passado.</span><span class="sxs-lookup"><span data-stu-id="f9942-440">hello applier that's provided also enables you toogenerate a dynamic number of properties in hello result rowset, based on hello parameter that's passed.</span></span> <span data-ttu-id="f9942-441">Você pode gerar todas as propriedades ou somente um conjunto específico de propriedades.</span><span class="sxs-lookup"><span data-stu-id="f9942-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="f9942-442">aplicador de saudação definido pelo usuário pode ser chamado como uma nova instância do objeto aplicador de alterações:</span><span class="sxs-lookup"><span data-stu-id="f9942-442">hello user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="f9942-443">Ou com a invocação de saudação de um método de fábrica de wrapper:</span><span class="sxs-lookup"><span data-stu-id="f9942-443">Or with hello invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="f9942-444">Usar combinadores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="f9942-444">Use user-defined combiners</span></span>
<span data-ttu-id="f9942-445">Combinação definida pelo usuário ou UDC, permite que você toocombine linhas conjuntos de linhas à esquerda e direita, com base em lógica personalizada.</span><span class="sxs-lookup"><span data-stu-id="f9942-445">User-defined combiner, or UDC, enables you toocombine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="f9942-446">O Combinador Definido pelo Usuário é usado com a expressão COMBINE.</span><span class="sxs-lookup"><span data-stu-id="f9942-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="f9942-447">Uma combinação está sendo invocada com a expressão de COMBINAR Olá que fornece informações necessárias de saudação sobre ambos os conjuntos de linhas de entrada hello, Olá agrupamento de colunas, hello esperado esquema de resultados e informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="f9942-447">A combiner is being invoked with hello COMBINE expression that provides hello necessary information about both hello input rowsets, hello grouping columns, hello expected result schema, and additional information.</span></span>

<span data-ttu-id="f9942-448">toocall uma combinação de um script U-SQL base, usamos Olá sintaxe a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9942-448">toocall a combiner in a base U-SQL script, we use hello following syntax:</span></span>

```
Combine_Expression :=
    'COMBINE' Combine_Input
    'WITH' Combine_Input
    Join_On_Clause
    Produce_Clause
    [Readonly_Clause]
    [Required_Clause]
    USING_Clause.
```

<span data-ttu-id="f9942-449">Para saber mais, veja [Expressão COMBINE (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span><span class="sxs-lookup"><span data-stu-id="f9942-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="f9942-450">toodefine uma combinação definida pelo usuário, precisamos Olá toocreate `ICombiner` interface com hello [`SqlUserDefinedCombiner`] atributo, que é opcional para uma definição de combinação definida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-450">toodefine a user-defined combiner, we need toocreate hello `ICombiner` interface with hello [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="f9942-451">Definição da classe `ICombiner` base:</span><span class="sxs-lookup"><span data-stu-id="f9942-451">Base `ICombiner` class definition:</span></span>

```
public abstract class ICombiner : IUserDefinedOperator
{
protected ICombiner();
public virtual IEnumerable<IRow> Combine(List<IRowset> inputs,
       IUpdatableRow output);
public abstract IEnumerable<IRow> Combine(IRowset left, IRowset right,
       IUpdatableRow output);
}
```

<span data-ttu-id="f9942-452">Olá implementação personalizada de um `ICombiner` interface deve conter a definição de saudação para um `IEnumerable<IRow>` combinar a substituição.</span><span class="sxs-lookup"><span data-stu-id="f9942-452">hello custom implementation of an `ICombiner` interface should contain hello definition for an `IEnumerable<IRow>` Combine override.</span></span>

```
[SqlUserDefinedCombiner]
public class MyCombiner : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    …
}
}
```

<span data-ttu-id="f9942-453">Olá **SqlUserDefinedCombiner** atributo indica que o tipo de saudação deve ser registrado como uma combinação definida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-453">hello **SqlUserDefinedCombiner** attribute indicates that hello type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="f9942-454">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="f9942-454">This class cannot be inherited.</span></span>

<span data-ttu-id="f9942-455">**SqlUserDefinedCombiner** é propriedade de modo de combinação de saudação toodefine usado.</span><span class="sxs-lookup"><span data-stu-id="f9942-455">**SqlUserDefinedCombiner** is used toodefine hello Combiner mode property.</span></span> <span data-ttu-id="f9942-456">É um atributo opcional para a definição do combinador definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="f9942-457">Modo CombinerMode</span><span class="sxs-lookup"><span data-stu-id="f9942-457">CombinerMode     Mode</span></span>

<span data-ttu-id="f9942-458">Enumeração CombinerMode pode assumir Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="f9942-458">CombinerMode enum can take hello following values:</span></span>

* <span data-ttu-id="f9942-459">Completo (0), que cada linha de saída depende de todas as linhas de entrada hello, da esquerda e direita com hello mesmo valor de chave.</span><span class="sxs-lookup"><span data-stu-id="f9942-459">Full  (0) Every output row potentially depends on all hello input rows from left and right       with hello same key value.</span></span>

* <span data-ttu-id="f9942-460">Esquerda (1) depende de cada linha de saída em uma única linha de entrada da esquerda da saudação (e potencialmente todas as linhas a partir de saudação à direita com hello mesmo valor de chave).</span><span class="sxs-lookup"><span data-stu-id="f9942-460">Left  (1) Every output row depends on a single input row from hello left (and potentially all rows       from hello right with hello same key value).</span></span>

* <span data-ttu-id="f9942-461">Right (2) depende de cada linha de saída em uma única linha de entrada da saudação à direita (e potencialmente todas as linhas da esquerda Olá com hello que mesmo valor de chave).</span><span class="sxs-lookup"><span data-stu-id="f9942-461">Right (2)     Every output row depends on a single input row from hello right (and potentially all rows       from hello left with hello same key value).</span></span>

* <span data-ttu-id="f9942-462">Interno (3) depende de cada linha de saída em uma única entrada de linha da esquerda e direita com hello mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="f9942-462">Inner (3) Every output row depends on a single input row from left and right with hello same value.</span></span>

<span data-ttu-id="f9942-463">Exemplo:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="f9942-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="f9942-464">objetos de programação principal Olá são:</span><span class="sxs-lookup"><span data-stu-id="f9942-464">hello main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="f9942-465">Os conjuntos de linhas de entrada são passados como tipo `IRowset` **esquerdo** e **direito** da interface.</span><span class="sxs-lookup"><span data-stu-id="f9942-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="f9942-466">Ambos os conjuntos de linhas precisam ser enumerados para processamento.</span><span class="sxs-lookup"><span data-stu-id="f9942-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="f9942-467">Só é possível enumerar cada interface de uma vez, podemos ter tooenumerate e armazene em cache se necessário.</span><span class="sxs-lookup"><span data-stu-id="f9942-467">You can only enumerate each interface once, so we have tooenumerate and cache it if necessary.</span></span>

<span data-ttu-id="f9942-468">Para fins de caching, podemos criar um tipo List\<T\> de estrutura de memória como resultado de uma execução da consulta LINQ, especificamente List<`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="f9942-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="f9942-469">tipo de dados anônimos Olá pode ser usado durante a enumeração também.</span><span class="sxs-lookup"><span data-stu-id="f9942-469">hello anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="f9942-470">Consulte [Introdução tooLINQ consultas (c#)](https://msdn.microsoft.com/library/bb397906.aspx) para obter mais informações sobre consultas LINQ e [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) para obter mais informações sobre o IEnumerable\<T\> interface.</span><span class="sxs-lookup"><span data-stu-id="f9942-470">See [Introduction tooLINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="f9942-471">valores de dados reais de saudação tooget de saudação entrada `IRowset`, usamos o método Get () Olá `IRow` interface.</span><span class="sxs-lookup"><span data-stu-id="f9942-471">tooget hello actual data values from hello incoming `IRowset`, we use hello Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="f9942-472">Nomes de coluna individuais podem ser determinados por chamada hello `IRow` método de esquema.</span><span class="sxs-lookup"><span data-stu-id="f9942-472">Individual column names can be determined by calling hello `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="f9942-473">Ou usando o nome da coluna de esquema hello:</span><span class="sxs-lookup"><span data-stu-id="f9942-473">Or by using hello schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="f9942-474">a enumeração geral Olá com LINQ semelhante ao seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="f9942-474">hello general enumeration with LINQ looks like hello following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="f9942-475">Depois de enumerar os dois conjuntos de linhas, vamos tooloop por todas as linhas.</span><span class="sxs-lookup"><span data-stu-id="f9942-475">After enumerating both rowsets, we are going tooloop through all rows.</span></span> <span data-ttu-id="f9942-476">Para cada linha no conjunto de linhas à esquerda Olá, vamos toofind todas as linhas que satisfazem a condição de saudação do nosso combinação.</span><span class="sxs-lookup"><span data-stu-id="f9942-476">For each row in hello left rowset, we are going toofind all rows that satisfy hello condition of our combiner.</span></span>

<span data-ttu-id="f9942-477">Olá valores de saída devem ser definidos com `IUpdatableRow` saída.</span><span class="sxs-lookup"><span data-stu-id="f9942-477">hello output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="f9942-478">saída real Olá é disparada pela chamada muito`yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="f9942-478">hello actual output is triggered by calling too`yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="f9942-479">Veja abaixo um exemplo do combinador:</span><span class="sxs-lookup"><span data-stu-id="f9942-479">Following is a combiner example:</span></span>

```
[SqlUserDefinedCombiner]
public class CombineSales : ICombiner
{

public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
    IUpdatableRow output)
{
    var internetSales =
    (from row in left.Rows
          select new
          {
              ProductKey = row.Get<int>("ProductKey"),
              OrderDateKey = row.Get<int>("OrderDateKey"),
              SalesAmount = row.Get<decimal>("SalesAmount"),
              TaxAmt = row.Get<decimal>("TaxAmt")
          }).ToList();

    var resellerSales =
    (from row in right.Rows
     select new
     {
     ProductKey = row.Get<int>("ProductKey"),
     OrderDateKey = row.Get<int>("OrderDateKey"),
     SalesAmount = row.Get<decimal>("SalesAmount"),
     TaxAmt = row.Get<decimal>("TaxAmt")
     }).ToList();

    foreach (var row_i in internetSales)
    {
    foreach (var row_r in resellerSales)
    {

        if (
        row_i.OrderDateKey > 0
        && row_i.OrderDateKey < row_r.OrderDateKey
        && row_i.OrderDateKey == 20010701
        && (row_r.SalesAmount + row_r.TaxAmt) > 20000)
        {
        output.Set<int>("OrderDateKey", row_i.OrderDateKey);
        output.Set<int>("ProductKey", row_i.ProductKey);
        output.Set<decimal>("Internet_Sales_Amount", row_i.SalesAmount + row_i.TaxAmt);
        output.Set<decimal>("Reseller_Sales_Amount", row_r.SalesAmount + row_r.TaxAmt);
        }

    }
    }
    yield return output.AsReadOnly();
}
}
```

<span data-ttu-id="f9942-480">Neste cenário de caso de uso, estamos criando um relatório de análise de revendedor de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9942-480">In this use-case scenario, we are building an analytics report for hello retailer.</span></span> <span data-ttu-id="f9942-481">meta de saudação é toofind todos os produtos que custam mais de US $20.000 e que vendem através do site de hello mais rapidamente do que através de revendedor de saudação normal em um determinado intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="f9942-481">hello goal is toofind all products that cost more than $20,000 and that sell through hello website faster than through hello regular retailer within a certain time frame.</span></span>

<span data-ttu-id="f9942-482">Aqui está o script U-SQL de base de saudação.</span><span class="sxs-lookup"><span data-stu-id="f9942-482">Here is hello base U-SQL script.</span></span> <span data-ttu-id="f9942-483">Você pode comparar a lógica de saudação entre uma junção comum e uma combinação:</span><span class="sxs-lookup"><span data-stu-id="f9942-483">You can compare hello logic between a regular JOIN and a combiner:</span></span>

```sql
DECLARE @LocalURI string = @"\usql-programmability\";

DECLARE @input_file_internet_sales string = @LocalURI+"FactInternetSales.txt";
DECLARE @input_file_reseller_sales string = @LocalURI+"FactResellerSales.txt";
DECLARE @output_file1 string = @LocalURI+"output_file1.tsv";
DECLARE @output_file2 string = @LocalURI+"output_file2.tsv";

@fact_internet_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    CustomerKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_internet_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@fact_reseller_sales =
EXTRACT
    ProductKey int ,
    OrderDateKey int ,
    DueDateKey int ,
    ShipDateKey int ,
    ResellerKey int ,
    EmployeeKey int ,
    PromotionKey int ,
    CurrencyKey int ,
    SalesTerritoryKey int ,
    SalesOrderNumber String ,
    SalesOrderLineNumber  int ,
    RevisionNumber int ,
    OrderQuantity int ,
    UnitPrice decimal ,
    ExtendedAmount decimal,
    UnitPriceDiscountPct float ,
    DiscountAmount float ,
    ProductStandardCost decimal ,
    TotalProductCost decimal ,
    SalesAmount decimal ,
    TaxAmt decimal ,
    Freight decimal ,
    CarrierTrackingNumber String,
    CustomerPONumber String
FROM @input_file_reseller_sales
USING Extractors.Text(delimiter:'|', encoding: Encoding.Unicode);

@rs1 =
SELECT
    fis.OrderDateKey,
    fis.ProductKey,
    fis.SalesAmount+fis.TaxAmt AS Internet_Sales_Amount,
    frs.SalesAmount+frs.TaxAmt AS Reseller_Sales_Amount
FROM @fact_internet_sales AS fis
     INNER JOIN @fact_reseller_sales AS frs
     ON fis.ProductKey == frs.ProductKey
WHERE
    fis.OrderDateKey < frs.OrderDateKey
    AND fis.OrderDateKey == 20010701
    AND frs.SalesAmount+frs.TaxAmt > 20000;

@rs2 =
COMBINE @fact_internet_sales AS fis
WITH @fact_reseller_sales AS frs
ON fis.ProductKey == frs.ProductKey
PRODUCE OrderDateKey int,
        ProductKey int,
        Internet_Sales_Amount decimal,
        Reseller_Sales_Amount decimal
USING new USQL_Programmability.CombineSales();

OUTPUT @rs1 too@output_file1 USING Outputters.Tsv();
OUTPUT @rs2 too@output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="f9942-484">Uma combinação definida pelo usuário pode ser chamada como uma nova instância do objeto de saudação aplicador de alterações:</span><span class="sxs-lookup"><span data-stu-id="f9942-484">A user-defined combiner can be called as a new instance of hello applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="f9942-485">Ou com a invocação de saudação de um método de fábrica de wrapper:</span><span class="sxs-lookup"><span data-stu-id="f9942-485">Or with hello invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="f9942-486">Usar redutores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="f9942-486">Use user-defined reducers</span></span>

<span data-ttu-id="f9942-487">U-SQL permite que você toowrite reducers de conjunto de linhas personalizadas em c# usando a estrutura de extensibilidade do operador definido pelo usuário hello e implementando uma interface IReducer.</span><span class="sxs-lookup"><span data-stu-id="f9942-487">U-SQL enables you toowrite custom rowset reducers in C# by using hello user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="f9942-488">Redutor definido pelo usuário ou UDR, pode ser linhas desnecessárias tooeliminate usado durante a extração de dados (importação).</span><span class="sxs-lookup"><span data-stu-id="f9942-488">User-defined reducer, or UDR, can be used tooeliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="f9942-489">Também pode ser usado toomanipulate e avaliar as linhas e colunas.</span><span class="sxs-lookup"><span data-stu-id="f9942-489">It also can be used toomanipulate and evaluate rows and columns.</span></span> <span data-ttu-id="f9942-490">Com base na lógica de programação, ele também pode definir quais linhas necessário toobe extraído.</span><span class="sxs-lookup"><span data-stu-id="f9942-490">Based on programmability logic, it can also define which rows need toobe extracted.</span></span>

<span data-ttu-id="f9942-491">toodefine uma classe UDR, precisamos toocreate um `IReducer` interface com um recurso opcional `SqlUserDefinedReducer` atributo.</span><span class="sxs-lookup"><span data-stu-id="f9942-491">toodefine a UDR class, we need toocreate an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="f9942-492">Essa interface de classe deve conter uma definição para Olá `IEnumerable` substituir o conjunto de linhas de interface.</span><span class="sxs-lookup"><span data-stu-id="f9942-492">This class interface should contain a definition for hello `IEnumerable` interface rowset override.</span></span>

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
        …
    }

}
```

<span data-ttu-id="f9942-493">Olá **SqlUserDefinedReducer** atributo indica que o tipo de saudação deve ser registrado como um redutor definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-493">hello **SqlUserDefinedReducer** attribute indicates that hello type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="f9942-494">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="f9942-494">This class cannot be inherited.</span></span>
<span data-ttu-id="f9942-495">**SqlUserDefinedReducer** é um atributo opcional para a definição do redutor definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="f9942-496">Ele usou toodefine IsRecursive propriedade.</span><span class="sxs-lookup"><span data-stu-id="f9942-496">It's used toodefine IsRecursive property.</span></span>

* <span data-ttu-id="f9942-497">bool     IsRecursive</span><span class="sxs-lookup"><span data-stu-id="f9942-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="f9942-498">**true**  = indica se esse Redutor é idempotente</span><span class="sxs-lookup"><span data-stu-id="f9942-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="f9942-499">objetos de programação principal Olá são **entrada** e **saída**.</span><span class="sxs-lookup"><span data-stu-id="f9942-499">hello main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="f9942-500">objeto de entrada Hello está tooenumerate usado linhas de entrada.</span><span class="sxs-lookup"><span data-stu-id="f9942-500">hello input object is used tooenumerate input rows.</span></span> <span data-ttu-id="f9942-501">A saída é usada tooset linhas de saída como resultado de reduzir a atividade.</span><span class="sxs-lookup"><span data-stu-id="f9942-501">Output is used tooset output rows as a result of reducing activity.</span></span>

<span data-ttu-id="f9942-502">Enumeração de linhas de entrada, usamos Olá `Row.Get` método.</span><span class="sxs-lookup"><span data-stu-id="f9942-502">For input rows enumeration, we use hello `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="f9942-503">Olá parâmetro hello `Row.Get` método é uma coluna que é passada como parte da saudação `PRODUCE` classe de saudação `REDUCE` instrução do script base Olá U-SQL.</span><span class="sxs-lookup"><span data-stu-id="f9942-503">hello parameter for hello `Row.Get` method is a column that's passed as part of hello `PRODUCE` class of hello `REDUCE` statement of hello U-SQL base script.</span></span> <span data-ttu-id="f9942-504">Precisamos toouse Olá tipo de dados correto aqui também.</span><span class="sxs-lookup"><span data-stu-id="f9942-504">We need toouse hello correct data type here as well.</span></span>

<span data-ttu-id="f9942-505">Saída, use Olá `output.Set` método.</span><span class="sxs-lookup"><span data-stu-id="f9942-505">For output, use hello `output.Set` method.</span></span>

<span data-ttu-id="f9942-506">É importante toounderstand que Redutor personalizado somente saídas os valores que são definidos com hello `output.Set` chamada de método.</span><span class="sxs-lookup"><span data-stu-id="f9942-506">It is important toounderstand that custom reducer only outputs values that are defined with hello `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="f9942-507">saída do Hello Redutor real é disparada pela chamada `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="f9942-507">hello actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="f9942-508">Abaixo temos um exemplo de redutor:</span><span class="sxs-lookup"><span data-stu-id="f9942-508">Following is a reducer example:</span></span>

```
[SqlUserDefinedReducer]
public class EmptyUserReducer : IReducer
{

    public override IEnumerable<IRow> Reduce(IRowset input, IUpdatableRow output)
    {
    string guid;
    DateTime dt;
    string user;
    string des;

    foreach (IRow row in input.Rows)
    {
        guid = row.Get<string>("guid");
        dt = row.Get<DateTime>("dt");
        user = row.Get<string>("user");
        des = row.Get<string>("des");

        if (user.Length > 0)
        {
        output.Set<string>("guid", guid);
        output.Set<DateTime>("dt", dt);
        output.Set<string>("user", user);
        output.Set<string>("des", des);

        yield return output.AsReadOnly();
        }
    }
    }

}
```

<span data-ttu-id="f9942-509">Neste cenário de caso de uso, Redutor hello está ignorando linhas com um nome de usuário vazio.</span><span class="sxs-lookup"><span data-stu-id="f9942-509">In this use-case scenario, hello reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="f9942-510">Para cada linha no conjunto de linhas, lê cada coluna necessária, em seguida, avalia o comprimento de Olá Olá do nome de usuário.</span><span class="sxs-lookup"><span data-stu-id="f9942-510">For each row in rowset, it reads each required column, then evaluates hello length of hello user name.</span></span> <span data-ttu-id="f9942-511">Ele produz real da linha hello somente se o comprimento do valor de nome de usuário é maior que 0.</span><span class="sxs-lookup"><span data-stu-id="f9942-511">It outputs hello actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="f9942-512">Abaixo temos um script base U-SQL que usa um redutor personalizado:</span><span class="sxs-lookup"><span data-stu-id="f9942-512">Following is base U-SQL script that uses a custom reducer:</span></span>

```
DECLARE @input_file string = @"\usql-programmability\input_file_reducer.tsv";
DECLARE @output_file string = @"\usql-programmability\output_file.tsv";

@rs0 =
    EXTRACT
            guid string,
        dt DateTime,
            user String,
            des String
    FROM @input_file 
    USING Extractors.Tsv();

@rs1 =
    REDUCE @rs0 PRESORT guid
    ON guid  
    PRODUCE guid string, dt DateTime, user String, des String
    USING new USQL_Programmability.EmptyUserReducer();

@rs2 =
    SELECT guid AS start_id,
           dt AS start_time,
           DateTime.Now.ToString("M/d/yyyy") AS Nowdate,
           USQL_Programmability.CustomFunctions.GetFiscalPeriodWithCustomType(dt).ToString() AS start_fiscalperiod,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    too@output_file 
    USING Outputters.Text();
```
