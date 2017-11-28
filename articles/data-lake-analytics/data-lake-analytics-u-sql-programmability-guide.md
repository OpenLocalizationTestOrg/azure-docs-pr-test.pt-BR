---
title: "Guia de programação do U-SQL para o Azure Data Lake | Microsoft Docs"
description: "Saiba mais sobre o conjunto de serviços do Azure Data Lake que permite criar uma plataforma de big data baseada em nuvem."
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
ms.openlocfilehash: e4e298475d7be7d51c8bd55be498371ed6ce77a9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="u-sql-programmability-guide"></a><span data-ttu-id="143be-103">Guia de programação do U-SQL</span><span class="sxs-lookup"><span data-stu-id="143be-103">U-SQL programmability guide</span></span>

<span data-ttu-id="143be-104">O U-SQL é uma linguagem de consulta projetada para o tipo big data de cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="143be-104">U-SQL is a query language that's designed for big data-type of workloads.</span></span> <span data-ttu-id="143be-105">Um dos recursos exclusivos do U-SQL é a combinação da linguagem declarativa semelhante ao SQL com a extensibilidade e a programação fornecidas por C#.</span><span class="sxs-lookup"><span data-stu-id="143be-105">One of the unique features of U-SQL is the combination of the SQL-like declarative language with the extensibility and programmability that's provided by C#.</span></span> <span data-ttu-id="143be-106">Neste guia, nosso foco é a extensibilidade e a programação da linguagem U-SQL habilitadas por C#.</span><span class="sxs-lookup"><span data-stu-id="143be-106">In this guide, we concentrate on the extensibility and programmability of the U-SQL language that's enabled by C#.</span></span>

## <a name="requirements"></a><span data-ttu-id="143be-107">Requisitos</span><span class="sxs-lookup"><span data-stu-id="143be-107">Requirements</span></span>

<span data-ttu-id="143be-108">Baixe e instale as [Ferramentas do Azure Data Lake para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span><span class="sxs-lookup"><span data-stu-id="143be-108">Download and install [Azure Data Lake Tools for Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).</span></span>

## <a name="get-started-with-u-sql"></a><span data-ttu-id="143be-109">Introdução ao U-SQL</span><span class="sxs-lookup"><span data-stu-id="143be-109">Get started with U-SQL</span></span>  

<span data-ttu-id="143be-110">Examinaremos o script U-SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="143be-110">Let’s look at the following U-SQL script:</span></span>

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

<span data-ttu-id="143be-111">Ele define um conjunto de linhas chamado @a e cria um conjunto de linhas chamado @results de @a.</span><span class="sxs-lookup"><span data-stu-id="143be-111">It defines a RowSet called @a and creates a RowSet called @results from @a.</span></span>

## <a name="c-types-and-expressions-in-u-sql-script"></a><span data-ttu-id="143be-112">Tipos e expressões de C# no script U-SQL</span><span class="sxs-lookup"><span data-stu-id="143be-112">C# types and expressions in U-SQL script</span></span>

<span data-ttu-id="143be-113">Uma expressão de U-SQL é uma expressão de C# combinada com operações lógicas U-SQL como `AND`, `OR` e `NOT`.</span><span class="sxs-lookup"><span data-stu-id="143be-113">A U-SQL Expression is a C# expression combined with U-SQL logical operations such `AND`, `OR`, and `NOT`.</span></span> <span data-ttu-id="143be-114">Expressões U-SQL podem ser usadas com SELECT, EXTRACT, WHERE, HAVING, GROUP BY e DECLARE.</span><span class="sxs-lookup"><span data-stu-id="143be-114">U-SQL Expressions can be used with SELECT, EXTRACT, WHERE, HAVING, GROUP BY and DECLARE.</span></span>

<span data-ttu-id="143be-115">Por exemplo, o script a seguir analisa uma cadeia de caracteres de um valor DateTime na cláusula SELECT.</span><span class="sxs-lookup"><span data-stu-id="143be-115">For example, the following script parses a string a DateTime value in the SELECT clause.</span></span>

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

<span data-ttu-id="143be-116">O script a seguir analisa uma cadeia de caracteres de um valor DateTime em uma instrução DECLARE.</span><span class="sxs-lookup"><span data-stu-id="143be-116">The following script parses a string a DateTime value in a DECLARE statement.</span></span>

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a><span data-ttu-id="143be-117">Usar expressões C# para conversões de tipo de dados</span><span class="sxs-lookup"><span data-stu-id="143be-117">Use C# expressions for data type conversions</span></span>
<span data-ttu-id="143be-118">O exemplo a seguir demonstra como você pode fazer uma conversão de dados de data e hora usando expressões C#.</span><span class="sxs-lookup"><span data-stu-id="143be-118">The following example demonstrates how you can do a datetime data conversion by using C# expressions.</span></span> <span data-ttu-id="143be-119">Nesse cenário específico, os dados de datetime da cadeia de caracteres são convertidos em datetime padrão com a notação de hora 00:00:00 meia-noite.</span><span class="sxs-lookup"><span data-stu-id="143be-119">In this particular scenario, string datetime data is converted to standard datetime with midnight 00:00:00 time notation.</span></span>

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a><span data-ttu-id="143be-120">Usar expressões C# para a data de hoje</span><span class="sxs-lookup"><span data-stu-id="143be-120">Use C# expressions for today’s date</span></span>
<span data-ttu-id="143be-121">Para efetuar pull da data de hoje, podemos usar a seguinte expressão C#:</span><span class="sxs-lookup"><span data-stu-id="143be-121">To pull today’s date, we can use the following C# expression:</span></span>

```
DateTime.Now.ToString("M/d/yyyy")
```

<span data-ttu-id="143be-122">Aqui está um exemplo de como usar essa expressão em um script:</span><span class="sxs-lookup"><span data-stu-id="143be-122">Here's an example of how to use this expression in a script:</span></span>

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



## <a name="using-net-assemblies"></a><span data-ttu-id="143be-123">Usando assemblies .NET</span><span class="sxs-lookup"><span data-stu-id="143be-123">Using .NET assemblies</span></span>
<span data-ttu-id="143be-124">O modelo de extensibilidade do U-SQL depende em grande parte da capacidade de adicionar código personalizado.</span><span class="sxs-lookup"><span data-stu-id="143be-124">U-SQL’s extensibility model relies heavily on the ability to add custom code.</span></span> <span data-ttu-id="143be-125">Atualmente, o U-SQL fornece maneiras fáceis de adicionar seu próprio código baseado em Microsoft .NET (em especial, C#).</span><span class="sxs-lookup"><span data-stu-id="143be-125">Currently, U-SQL provides you with easy ways to add your own Microsoft .NET-based code (in particular, C#).</span></span> <span data-ttu-id="143be-126">No entanto, você também pode adicionar código personalizado escrito em outras linguagens .NET, como VB.NET ou F#.</span><span class="sxs-lookup"><span data-stu-id="143be-126">However, you can also add custom code that's written in other .NET languages, such as VB.NET or F#.</span></span> 

### <a name="register-a-net-assembly"></a><span data-ttu-id="143be-127">Registrar um assembly .NET</span><span class="sxs-lookup"><span data-stu-id="143be-127">Register a .NET assembly</span></span>

<span data-ttu-id="143be-128">Use a instrução CREATE ASSEMBLY para colocar um assembly do .NET em um banco de dados U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-128">Use the CREATE ASSEMBLY statement to place a .NET assembly into a U-SQL Database.</span></span> <span data-ttu-id="143be-129">Quando um assembly está em um banco de dados, scripts U-SQL podem usar esses assemblies usando a instrução REFERENCE ASSEMBLY.</span><span class="sxs-lookup"><span data-stu-id="143be-129">Once an assembly is in a database, U-SQL scripts can use those assemblies by using the REFERENCE ASSEMBLY statement.</span></span> 

<span data-ttu-id="143be-130">O código a seguir mostra como registrar um assembly:</span><span class="sxs-lookup"><span data-stu-id="143be-130">The following code shows how to register an assembly:</span></span>

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

<span data-ttu-id="143be-131">O código a seguir mostra como referenciar um assembly:</span><span class="sxs-lookup"><span data-stu-id="143be-131">The following code shows how to reference an assembly:</span></span>

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

<span data-ttu-id="143be-132">Consulte as [instruções de registro do assembly](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/), que abrangem este tópico mais detalhadamente.</span><span class="sxs-lookup"><span data-stu-id="143be-132">Consult the [assembly registration instructions](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) that covers this topic in greater detail.</span></span>


### <a name="use-assembly-versioning"></a><span data-ttu-id="143be-133">Usar o controle de versão do assembly</span><span class="sxs-lookup"><span data-stu-id="143be-133">Use assembly versioning</span></span>
<span data-ttu-id="143be-134">Atualmente, o U-SQL usa o .NET Framework versão 4.5.</span><span class="sxs-lookup"><span data-stu-id="143be-134">Currently, U-SQL uses the .NET Framework version 4.5.</span></span> <span data-ttu-id="143be-135">Portanto, faça com que seus próprios assemblies sejam compatíveis com essa versão do tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="143be-135">So ensure that your own assemblies are compatible with that version of the runtime.</span></span>

<span data-ttu-id="143be-136">Conforme mencionado anteriormente, o U-SQL executa código em um formato de 64 bits (x64).</span><span class="sxs-lookup"><span data-stu-id="143be-136">As mentioned earlier, U-SQL runs code in a 64-bit (x64) format.</span></span> <span data-ttu-id="143be-137">Portanto, faça com que seu código seja compilado para execução em x64.</span><span class="sxs-lookup"><span data-stu-id="143be-137">So make sure that your code is compiled to run on x64.</span></span> <span data-ttu-id="143be-138">Caso contrário, você obterá o erro de formato incorreto mostrado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="143be-138">Otherwise you get the incorrect format error shown earlier.</span></span>

<span data-ttu-id="143be-139">Cada arquivo de recurso e DLL de assembly carregado, como um tempo de execução diferente, um assembly nativo ou um arquivo config, pode ter no máximo 400 MB.</span><span class="sxs-lookup"><span data-stu-id="143be-139">Each uploaded assembly DLL and resource file, such as a different runtime, a native assembly, or a config file, can be at most 400 MB.</span></span> <span data-ttu-id="143be-140">O tamanho total dos recursos implantados, seja por meio de DEPLOY RESOURCE ou por meio de referências a assemblies e a seus arquivos adicionais, não pode exceder 3 GB.</span><span class="sxs-lookup"><span data-stu-id="143be-140">The total size of deployed resources, either via DEPLOY RESOURCE or via references to assemblies and their additional files, cannot exceed 3 GB.</span></span>

<span data-ttu-id="143be-141">Por fim, observe que cada banco de dados U-SQL pode conter apenas uma versão de qualquer determinado assembly.</span><span class="sxs-lookup"><span data-stu-id="143be-141">Finally, note that each U-SQL database can only contain one version of any given assembly.</span></span> <span data-ttu-id="143be-142">Por exemplo, se você precisar da versão 7 e da versão 8 da biblioteca NewtonSoft Json.Net, será preciso registrá-las em dois bancos de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="143be-142">For example, if you need both version 7 and version 8 of the NewtonSoft Json.Net library, you need to register them in two different databases.</span></span> <span data-ttu-id="143be-143">Além disso, cada script pode fazer referência apenas a uma versão da DLL de um determinado assembly.</span><span class="sxs-lookup"><span data-stu-id="143be-143">Furthermore, each script can only refer to one version of a given assembly DLL.</span></span> <span data-ttu-id="143be-144">Nesse sentido, o U-SQL segue a semântica de controle de versão e gerenciamento do assembly de C#.</span><span class="sxs-lookup"><span data-stu-id="143be-144">In this respect, U-SQL follows the C# assembly management and versioning semantics.</span></span>


## <a name="use-user-defined-functions-udf"></a><span data-ttu-id="143be-145">Funções definidas pelo usuário: UDF</span><span class="sxs-lookup"><span data-stu-id="143be-145">Use user-defined functions: UDF</span></span>
<span data-ttu-id="143be-146">As funções definidas pelo usuário ou UDF do U-SQL são rotinas de programação que aceitam parâmetros, executam uma ação (mo um cálculo complexo)e retornam o resultado dessa ação como um valor.</span><span class="sxs-lookup"><span data-stu-id="143be-146">U-SQL user-defined functions, or UDF, are programming routines that accept parameters, perform an action (such as a complex calculation), and return the result of that action as a value.</span></span> <span data-ttu-id="143be-147">O valor de retorno da UDF pode ser apenas um único escalar.</span><span class="sxs-lookup"><span data-stu-id="143be-147">The return value of UDF can only be a single scalar.</span></span> <span data-ttu-id="143be-148">A UDF do U-SQL pode ser chamado no script base U-SQL como qualquer outra função escalar C#.</span><span class="sxs-lookup"><span data-stu-id="143be-148">U-SQL UDF can be called in U-SQL base script like any other C# scalar function.</span></span>

<span data-ttu-id="143be-149">Recomendamos que você inicialize as funções do U-SQL definidas pelo usuário como **públicas** e **estáticas**.</span><span class="sxs-lookup"><span data-stu-id="143be-149">We recommend that you initialize U-SQL user-defined functions as **public** and **static**.</span></span>

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

<span data-ttu-id="143be-150">Primeiro, vamos ver um exemplo simples de como criar uma UDF.</span><span class="sxs-lookup"><span data-stu-id="143be-150">First let’s look at the simple example of creating a UDF.</span></span>

<span data-ttu-id="143be-151">Nesse cenário de caso de uso, precisamos determinar o período fiscal, inclusive o trimestre fiscal e o mês fiscal do primeiro logon para o usuário específico.</span><span class="sxs-lookup"><span data-stu-id="143be-151">In this use-case scenario, we need to determine the fiscal period, including the fiscal quarter and fiscal month of the first sign-in for the specific user.</span></span> <span data-ttu-id="143be-152">O primeiro mês fiscal do ano em nosso cenário é junho.</span><span class="sxs-lookup"><span data-stu-id="143be-152">The first fiscal month of the year in our scenario is June.</span></span>

<span data-ttu-id="143be-153">Para calcular o período fiscal, introduzimos a seguinte função C#:</span><span class="sxs-lookup"><span data-stu-id="143be-153">To calculate fiscal period, we introduce the following C# function:</span></span>

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

<span data-ttu-id="143be-154">Ela simplesmente calcula o mês e o trimestre fiscal e retorna um valor de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="143be-154">It simply calculates fiscal month and quarter and returns a string value.</span></span> <span data-ttu-id="143be-155">No caso de junho, o primeiro mês do primeiro trimestre fiscal, usamos "Q1:P1".</span><span class="sxs-lookup"><span data-stu-id="143be-155">For June, the first month of the first fiscal quarter, we use "Q1:P1".</span></span> <span data-ttu-id="143be-156">No caso de julho, usamos "Q1:P2" e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="143be-156">For July, we use "Q1:P2", and so on.</span></span>

<span data-ttu-id="143be-157">Essa é uma função C# regular que vamos usar em nosso projeto U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-157">This is a regular C# function that we are going to use in our U-SQL project.</span></span>

<span data-ttu-id="143be-158">Veja como é a seção code-behind nesse cenário:</span><span class="sxs-lookup"><span data-stu-id="143be-158">Here is how the code-behind section looks in this scenario:</span></span>

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

<span data-ttu-id="143be-159">Agora, vamos chamar essa função do script base U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-159">Now we are going to call this function from the base U-SQL script.</span></span> <span data-ttu-id="143be-160">Para fazer isso, precisamos fornecer um nome totalmente qualificado para a função, incluindo o namespace, que nesse caso é NameSpace.Class.Function(parameter).</span><span class="sxs-lookup"><span data-stu-id="143be-160">To do this, we have to provide a fully qualified name for the function, including the namespace, which in this case is NameSpace.Class.Function(parameter).</span></span>

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

<span data-ttu-id="143be-161">Veja abaixo o script base U-SQL real:</span><span class="sxs-lookup"><span data-stu-id="143be-161">Following is the actual U-SQL base script:</span></span>

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
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="143be-162">Veja abaixo o arquivo de saída da execução do script:</span><span class="sxs-lookup"><span data-stu-id="143be-162">Following is the output file of the script execution:</span></span>

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

<span data-ttu-id="143be-163">Esse exemplo demonstra um uso simples de UDF embutida no U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-163">This example demonstrates a simple usage of inline UDF in U-SQL.</span></span>

### <a name="keep-state-between-udf-invocations"></a><span data-ttu-id="143be-164">Manter o estado entre invocações da UDF</span><span class="sxs-lookup"><span data-stu-id="143be-164">Keep state between UDF invocations</span></span>
<span data-ttu-id="143be-165">Os objetos de programação C# do U-SQL podem ser mais sofisticados ao utilizar interatividade por meio de variáveis globais de code-behind.</span><span class="sxs-lookup"><span data-stu-id="143be-165">U-SQL C# programmability objects can be more sophisticated, utilizing interactivity through the code-behind global variables.</span></span> <span data-ttu-id="143be-166">Vejamos o cenário de caso de uso comercial a seguir.</span><span class="sxs-lookup"><span data-stu-id="143be-166">Let’s look at the following business use-case scenario.</span></span>

<span data-ttu-id="143be-167">Em grandes organizações, os usuários podem alternar entre diversos aplicativos internos.</span><span class="sxs-lookup"><span data-stu-id="143be-167">In large organizations, users can switch between varieties of internal applications.</span></span> <span data-ttu-id="143be-168">Eles podem incluir o Microsoft Dynamics CRM, o PowerBI e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="143be-168">These can include Microsoft Dynamics CRM, PowerBI, and so on.</span></span> <span data-ttu-id="143be-169">O cliente pode querer aplicar uma análise de telemetria de como os usuários alternam entre diferentes aplicativos, quais são as tendências de uso e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="143be-169">Customers might want to apply a telemetry analysis of how users switch between different applications, what the usage trends are, and so on.</span></span> <span data-ttu-id="143be-170">O objetivo da empresa é otimizar o uso de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="143be-170">The goal for the business is to optimize application usage.</span></span> <span data-ttu-id="143be-171">Ela também pode querer combinar diferentes aplicativos ou rotinas específicas de logon.</span><span class="sxs-lookup"><span data-stu-id="143be-171">They also might want to combine different applications or specific sign-on routines.</span></span>

<span data-ttu-id="143be-172">Para atingir essa meta, precisamos determinar as IDs de uma sessão e o tempo de latência desde a última sessão ocorrida.</span><span class="sxs-lookup"><span data-stu-id="143be-172">To achieve this goal, we have to determine session IDs and lag time between the last session that occurred.</span></span>

<span data-ttu-id="143be-173">Precisamos encontrar um logon anterior e atribuí-lo a todas as sessões que estão sendo geradas para o mesmo aplicativo.</span><span class="sxs-lookup"><span data-stu-id="143be-173">We need to find a previous sign-in and then assign this sign-in to all sessions that are being generated to the same application.</span></span> <span data-ttu-id="143be-174">Primeiro desafio: o script base U-SQL não nos permite aplicar cálculos sobre colunas já calculadas com a função LAG.</span><span class="sxs-lookup"><span data-stu-id="143be-174">The first challenge is that U-SQL base script doesn't allow us to apply calculations over already-calculated columns with LAG function.</span></span> <span data-ttu-id="143be-175">Segundo desafio: temos que manter a sessão específica para todas as sessões no mesmo período.</span><span class="sxs-lookup"><span data-stu-id="143be-175">The second challenge is that we have to keep the specific session for all sessions within the same time period.</span></span>

<span data-ttu-id="143be-176">Para resolver esse problema, use uma variável global dentro da seção code-behind: `static public string globalSession;`.</span><span class="sxs-lookup"><span data-stu-id="143be-176">To solve this problem, we use a global variable inside a code-behind section: `static public string globalSession;`.</span></span>

<span data-ttu-id="143be-177">Essa variável global é aplicada a todo o conjunto de linhas durante a execução do nosso script.</span><span class="sxs-lookup"><span data-stu-id="143be-177">This global variable is applied to the entire rowset during our script execution.</span></span>

<span data-ttu-id="143be-178">Veja abaixo a seção code-behind do nosso programa U-SQL:</span><span class="sxs-lookup"><span data-stu-id="143be-178">Here is the code-behind section of our U-SQL program:</span></span>

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

<span data-ttu-id="143be-179">Este exemplo mostra a variável global `static public string globalSession;` usada dentro da função `getStampUserSession` sendo reinicializada sempre que o parâmetro Session é alterado.</span><span class="sxs-lookup"><span data-stu-id="143be-179">This example shows the global variable `static public string globalSession;` used inside the `getStampUserSession` function and getting reinitialized each time the Session parameter is changed.</span></span>

<span data-ttu-id="143be-180">O script base U-SQL é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="143be-180">The U-SQL base script is as follows:</span></span>

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
    TO @out2
    ORDER BY UserName, EventDateTime ASC
    USING Outputters.Csv();
```

<span data-ttu-id="143be-181">A função `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` é chamada aqui durante o segundo cálculo do conjunto de linhas da memória.</span><span class="sxs-lookup"><span data-stu-id="143be-181">Function `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` is called here during the second memory rowset calculation.</span></span> <span data-ttu-id="143be-182">Ele passa a coluna `UserSessionTimestamp` e retorna o valor até que `UserSessionTimestamp` seja alterado.</span><span class="sxs-lookup"><span data-stu-id="143be-182">It passes the `UserSessionTimestamp` column and returns the value until `UserSessionTimestamp` has changed.</span></span>

<span data-ttu-id="143be-183">O arquivo de saída é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="143be-183">The output file is as follows:</span></span>

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

<span data-ttu-id="143be-184">Esse exemplo demonstra um cenário de caso de uso mais complicado em que usamos uma variável global dentro da seção code-behind aplicada a todo um conjunto de linhas da memória.</span><span class="sxs-lookup"><span data-stu-id="143be-184">This example demonstrates a more complicated use-case scenario in which we use a global variable inside a code-behind section that's applied to the entire memory rowset.</span></span>

## <a name="use-user-defined-types-udt"></a><span data-ttu-id="143be-185">Tipos de CLR definidos pelo usuário: UDT</span><span class="sxs-lookup"><span data-stu-id="143be-185">Use user-defined types: UDT</span></span>
<span data-ttu-id="143be-186">Os tipos definidos pelo usuário, ou UDT, são outro recurso de programação do U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-186">User-defined types, or UDT, is another programmability feature of U-SQL.</span></span> <span data-ttu-id="143be-187">O UDT do U-SQL atua como um tipo definido pelo usuário regular de C#.</span><span class="sxs-lookup"><span data-stu-id="143be-187">U-SQL UDT acts like a regular C# user-defined type.</span></span> <span data-ttu-id="143be-188">C# é uma linguagem fortemente tipada que permite o uso de tipos definidos pelo usuário personalizados e internos.</span><span class="sxs-lookup"><span data-stu-id="143be-188">C# is a strongly typed language that allows the use of built-in and custom user-defined types.</span></span>

<span data-ttu-id="143be-189">O U-SQL não pode implicitamente serializar ou desserializar UDTs arbitrários quando o UDT é passado entre os vértices em conjuntos de linhas.</span><span class="sxs-lookup"><span data-stu-id="143be-189">U-SQL cannot implicitly serialize or de-serialize arbitrary UDTs when the UDT is passed between vertices in rowsets.</span></span> <span data-ttu-id="143be-190">Isso significa que o usuário precisa fornecer um formatador explícito usando a interface IFormatter.</span><span class="sxs-lookup"><span data-stu-id="143be-190">This means that the user has to provide an explicit formatter by using the IFormatter interface.</span></span> <span data-ttu-id="143be-191">Isso fornece ao U-SQL métodos de serialização e desserialização para o UDT.</span><span class="sxs-lookup"><span data-stu-id="143be-191">This provides U-SQL with the serialize and de-serialize methods for the UDT.</span></span>

> [!NOTE]
> <span data-ttu-id="143be-192">Extratores internos e outputters de U-SQL atualmente não podem serializar ou desserializar dados de UDT de ou para arquivos, mesmo com o conjunto do IFormatter.</span><span class="sxs-lookup"><span data-stu-id="143be-192">U-SQL’s built-in extractors and outputters currently cannot serialize or de-serialize UDT data to or from files even with the IFormatter set.</span></span> <span data-ttu-id="143be-193">Assim, quando você está gravando dados UDT em um arquivo com a instrução OUTPUT ou lendo com um extrator, precisa passá-lo como uma cadeia de caracteres ou matriz de bytes.</span><span class="sxs-lookup"><span data-stu-id="143be-193">So when you're writing UDT data to a file with the OUTPUT statement, or reading it with an extractor, you have to pass it as a string or byte array.</span></span> <span data-ttu-id="143be-194">Em seguida, deve chamar o código de serialização e desserialização (ou seja, o método ToString () do UDT) explicitamente.</span><span class="sxs-lookup"><span data-stu-id="143be-194">Then you call the serialization and deserialization code (that is, the UDT’s ToString() method) explicitly.</span></span> <span data-ttu-id="143be-195">Por outro lado, extratores definidos pelo usuário e outputters podem ler e gravar UDTs.</span><span class="sxs-lookup"><span data-stu-id="143be-195">User-defined extractors and outputters, on the other hand, can read and write UDTs.</span></span>

<span data-ttu-id="143be-196">Se tentarmos usam o UDT em EXTRATOR ou OUTPUTTER (fora do SELECT anterior), conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="143be-196">If we try to use UDT in EXTRACTOR or OUTPUTTER (out of previous SELECT), as shown here:</span></span>

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="143be-197">Recebemos o seguinte erro:</span><span class="sxs-lookup"><span data-stu-id="143be-197">We receive the following error:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINOUTPUTTER: Outputters.Text was used to output column myfield of type
MyNameSpace.Myfunction_Returning_UDT.

Description:

Outputters.Text only supports built-in types.

Resolution:

Implement a custom outputter that knows how to serialize this type, or call a serialization method on the type in
the preceding SELECT.   C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\
USQL-Programmability\Types.usql 52  1   USQL-Programmability
```

<span data-ttu-id="143be-198">Para trabalhar com UDT em outptutter, também temos que serializá-lo para cadeia de caracteres com o método ToString() ou criar um outputter personalizado.</span><span class="sxs-lookup"><span data-stu-id="143be-198">To work with UDT in outputter, we either have to serialize it to string with the ToString() method or create a custom outputter.</span></span>

<span data-ttu-id="143be-199">Atualmente, os UDTs não podem ser usados em GROUP BY.</span><span class="sxs-lookup"><span data-stu-id="143be-199">UDTs currently cannot be used in GROUP BY.</span></span> <span data-ttu-id="143be-200">Se o UDT for usado em GROUP BY, o seguinte erro será gerado:</span><span class="sxs-lookup"><span data-stu-id="143be-200">If UDT is used in GROUP BY, the following error is thrown:</span></span>

```
Error   1   E_CSC_USER_INVALIDTYPEINCLAUSE: GROUP BY doesn't support type MyNameSpace.Myfunction_Returning_UDT
for column myfield

Description:

GROUP BY doesn't support UDT or Complex types.

Resolution:

Add a SELECT statement where you can project a scalar column that you want to use with GROUP BY.
C:\Users\sergeypu\Documents\Visual Studio 2013\Projects\USQL-Programmability\USQL-Programmability\Types.usql
62  5   USQL-Programmability
```

<span data-ttu-id="143be-201">Para definir um UDT, temos que:</span><span class="sxs-lookup"><span data-stu-id="143be-201">To define a UDT, we have to:</span></span>

* <span data-ttu-id="143be-202">Adicione os seguintes namespaces:</span><span class="sxs-lookup"><span data-stu-id="143be-202">Add the following namespaces:</span></span>

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* <span data-ttu-id="143be-203">Adicione `Microsoft.Analytics.Interfaces`, que é necessário para as interfaces UDT.</span><span class="sxs-lookup"><span data-stu-id="143be-203">Add `Microsoft.Analytics.Interfaces`, which is required for the UDT interfaces.</span></span> <span data-ttu-id="143be-204">Além disso, `System.IO` pode ser necessário para definir a interface IFormatter.</span><span class="sxs-lookup"><span data-stu-id="143be-204">In addition, `System.IO` might be needed to define the IFormatter interface.</span></span>

* <span data-ttu-id="143be-205">Defina o tipo definido usado com o atributo SqlUserDefinedType.</span><span class="sxs-lookup"><span data-stu-id="143be-205">Define a used-defined type with SqlUserDefinedType attribute.</span></span>

<span data-ttu-id="143be-206">**SqlUserDefinedType** é usado para marcar uma definição de tipo em um assembly como um UDT (tipo definido pelo usuário) no U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-206">**SqlUserDefinedType** is used to mark a type definition in an assembly as a user-defined type (UDT) in U-SQL.</span></span> <span data-ttu-id="143be-207">As propriedades no atributo refletem as características físicas do UDT.</span><span class="sxs-lookup"><span data-stu-id="143be-207">The properties on the attribute reflect the physical characteristics of the UDT.</span></span> <span data-ttu-id="143be-208">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="143be-208">This class cannot be inherited.</span></span>

<span data-ttu-id="143be-209">SqlUserDefinedType é um atributo necessário para a definição de UDT.</span><span class="sxs-lookup"><span data-stu-id="143be-209">SqlUserDefinedType is a required attribute for UDT definition.</span></span>

<span data-ttu-id="143be-210">O construtor da classe:</span><span class="sxs-lookup"><span data-stu-id="143be-210">The constructor of the class:</span></span>  

* <span data-ttu-id="143be-211">SqlUserDefinedTypeAttribute(type formatter)</span><span class="sxs-lookup"><span data-stu-id="143be-211">SqlUserDefinedTypeAttribute (type formatter)</span></span>

* <span data-ttu-id="143be-212">Digite o parâmetro formatter: Required para definir um formatador UDT, mais especificamente, o tipo da interface `IFormatter` deve ser passado aqui.</span><span class="sxs-lookup"><span data-stu-id="143be-212">Type formatter: Required parameter to define an UDT formatter--specifically, the type of the `IFormatter` interface must be passed here.</span></span>

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* <span data-ttu-id="143be-213">O UDT típico também requer a definição da interface IFormatter, conforme mostrado no exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="143be-213">Typical UDT also requires definition of the IFormatter interface, as shown in the following example:</span></span>

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

<span data-ttu-id="143be-214">A interface `IFormatter` serializa e desserializa um gráfico de objeto com o tipo raiz de \<typeparamref name="T">.</span><span class="sxs-lookup"><span data-stu-id="143be-214">The `IFormatter` interface serializes and de-serializes an object graph with the root type of \<typeparamref name="T">.</span></span>

<span data-ttu-id="143be-215">\<typeparam name="T">O tipo raiz para serialização e desserialização do gráfico de objeto.</span><span class="sxs-lookup"><span data-stu-id="143be-215">\<typeparam name="T">The root type for the object graph to serialize and de-serialize.</span></span>

* <span data-ttu-id="143be-216">**Desserializar**: desserializa os dados no fluxo fornecido e reconstitui o gráfico de objetos.</span><span class="sxs-lookup"><span data-stu-id="143be-216">**Deserialize**: De-serializes the data on the provided stream and reconstitutes the graph of objects.</span></span>

* <span data-ttu-id="143be-217">**Serializar**: serializa um objeto ou gráfico de objetos com determinada raiz para o fluxo fornecido.</span><span class="sxs-lookup"><span data-stu-id="143be-217">**Serialize**: Serializes an object, or graph of objects, with the given root to the provided stream.</span></span>

<span data-ttu-id="143be-218">Instância `MyType`: a instância do tipo.</span><span class="sxs-lookup"><span data-stu-id="143be-218">`MyType` instance: Instance of the type.</span></span>  
<span data-ttu-id="143be-219">Gravador `IColumnWriter`/leitor `IColumnReader`: o fluxo da coluna subjacente.</span><span class="sxs-lookup"><span data-stu-id="143be-219">`IColumnWriter` writer / `IColumnReader` reader: The underlying column stream.</span></span>  
<span data-ttu-id="143be-220">Contexto `ISerializationContext`: enumeração que define um conjunto de sinalizadores que especifica o contexto de origem ou destino para o fluxo durante a serialização.</span><span class="sxs-lookup"><span data-stu-id="143be-220">`ISerializationContext` context: Enum that defines a set of flags that specifies the source or destination context for the stream during serialization.</span></span>

* <span data-ttu-id="143be-221">**Intermediário**: especifica que o contexto de origem ou de destino não é um armazenamento persistente.</span><span class="sxs-lookup"><span data-stu-id="143be-221">**Intermediate**: Specifies that the source or destination context is not a persisted store.</span></span>

* <span data-ttu-id="143be-222">**Persistência**: especifica que o contexto de origem ou de destino é um armazenamento persistente.</span><span class="sxs-lookup"><span data-stu-id="143be-222">**Persistence**: Specifies that the source or destination context is a persisted store.</span></span>

<span data-ttu-id="143be-223">Como um tipo C# regular, uma definição de UDT do U-SQL pode incluir substituições para operadores como +/==/!=.</span><span class="sxs-lookup"><span data-stu-id="143be-223">As a regular C# type, a U-SQL UDT definition can include overrides for operators such as +/==/!=.</span></span> <span data-ttu-id="143be-224">Ele também pode incluir métodos estáticos.</span><span class="sxs-lookup"><span data-stu-id="143be-224">It can also include static methods.</span></span> <span data-ttu-id="143be-225">Por exemplo, se formos usar esse UDT como um parâmetro para uma função agregada MIN do U-SQL, teremos que definir a substituição do operador <.</span><span class="sxs-lookup"><span data-stu-id="143be-225">For example, if we are going to use this UDT as a parameter to a U-SQL MIN aggregate function, we have to define < operator override.</span></span>

<span data-ttu-id="143be-226">Anteriormente neste guia, demonstramos um exemplo da identificação do período fiscal na data específica no formato Qn:Pn (Q1:P10).</span><span class="sxs-lookup"><span data-stu-id="143be-226">Earlier in this guide, we demonstrated an example for fiscal period identification from the specific date in the format Qn:Pn (Q1:P10).</span></span> <span data-ttu-id="143be-227">O exemplo a seguir mostra como definir um tipo personalizado para os valores do período fiscal.</span><span class="sxs-lookup"><span data-stu-id="143be-227">The following example shows how to define a custom type for fiscal period values.</span></span>

<span data-ttu-id="143be-228">Abaixo temos um exemplo de uma seção code-behind com interface IFormatter e UDT personalizado:</span><span class="sxs-lookup"><span data-stu-id="143be-228">Following is an example of a code-behind section with custom UDT and IFormatter interface:</span></span>

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

<span data-ttu-id="143be-229">O tipo definido inclui dois números: trimestre e mês.</span><span class="sxs-lookup"><span data-stu-id="143be-229">The defined type includes two numbers: quarter and month.</span></span> <span data-ttu-id="143be-230">Os operadores ==/!=/>/< e o método estático ToString() são definidos aqui.</span><span class="sxs-lookup"><span data-stu-id="143be-230">Operators ==/!=/>/< and static method ToString() are defined here.</span></span>

<span data-ttu-id="143be-231">Como mencionado anteriormente, o UDT pode ser usado nas expressões SELECT, mas não pode ser usado em OUTPUTTER/EXTRACTOR sem serialização personalizada.</span><span class="sxs-lookup"><span data-stu-id="143be-231">As mentioned earlier, UDT can be used in SELECT expressions, but cannot be used in OUTPUTTER/EXTRACTOR without custom serialization.</span></span> <span data-ttu-id="143be-232">Ele precisa ser serializado como uma cadeia de caracteres com ToString() ou usado com um OUTPUTTER/EXTRACTOR personalizado.</span><span class="sxs-lookup"><span data-stu-id="143be-232">It either has to be serialized as a string with ToString() or used with a custom OUTPUTTER/EXTRACTOR.</span></span>

<span data-ttu-id="143be-233">Agora, vamos falar sobre o uso do UDT.</span><span class="sxs-lookup"><span data-stu-id="143be-233">Now let’s discuss usage of UDT.</span></span> <span data-ttu-id="143be-234">Na seção code-behind, alteramos a nossa função GetFiscalPeriod para o seguinte:</span><span class="sxs-lookup"><span data-stu-id="143be-234">In a code-behind section, we changed our GetFiscalPeriod function to the following:</span></span>

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

<span data-ttu-id="143be-235">Como você pode ver, ela retorna o valor do nosso tipo FiscalPeriod.</span><span class="sxs-lookup"><span data-stu-id="143be-235">As you can see, it returns the value of our FiscalPeriod type.</span></span>

<span data-ttu-id="143be-236">Aqui, fornecemos um exemplo de como usá-lo ainda mais no script base U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-236">Here we provide an example of how to use it further in U-SQL base script.</span></span> <span data-ttu-id="143be-237">Este exemplo demonstra as diferentes formas de invocação do UDT no script U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-237">This example demonstrates different forms of UDT invocation from U-SQL script.</span></span>

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

       // This user-defined type was created in the prior SELECT.  Passing the UDT to this subsequent SELECT would have failed if the UDT was not annotated with an IFormatter.
           fiscalperiod_adjusted.ToString() AS fiscalperiod_adjusted,
           user,
           des
    FROM @rs1;

OUTPUT @rs2 
    TO @output_file 
    USING Outputters.Text();
```

<span data-ttu-id="143be-238">Veja um exemplo de uma seção completa code-behind:</span><span class="sxs-lookup"><span data-stu-id="143be-238">Here's an example of a full code-behind section:</span></span>

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

## <a name="use-user-defined-aggregates-udagg"></a><span data-ttu-id="143be-239">Use agregações definidas pelo usuário: UDAGG</span><span class="sxs-lookup"><span data-stu-id="143be-239">Use user-defined aggregates: UDAGG</span></span>
<span data-ttu-id="143be-240">As agregações definidas pelo usuário são funções relacionadas à agregação que não são enviadas para uso imediato com o U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-240">User-defined aggregates are any aggregation-related functions that are not shipped out-of-the-box with U-SQL.</span></span> <span data-ttu-id="143be-241">O exemplo pode ser uma agregação para executar um cálculo matemático personalizado, concatenações de cadeia de caracteres ou manipulações com cadeias de caracteres, etc.</span><span class="sxs-lookup"><span data-stu-id="143be-241">The example can be an aggregate to perform custom math calculations, string concatenations, manipulations with strings, and so on.</span></span>

<span data-ttu-id="143be-242">A definição de classe base da agregação definida pelo usuário é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="143be-242">The user-defined aggregate base class definition is as follows:</span></span>

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

<span data-ttu-id="143be-243">**SqlUserDefinedAggregate** indica que o tipo deve ser registrado como uma agregação definida pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-243">**SqlUserDefinedAggregate** indicates that the type should be registered as a user-defined aggregate.</span></span> <span data-ttu-id="143be-244">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="143be-244">This class cannot be inherited.</span></span>

<span data-ttu-id="143be-245">O atributo SqlUserDefinedType é **opcional** para a definição de UDAGG.</span><span class="sxs-lookup"><span data-stu-id="143be-245">SqlUserDefinedType attribute is **optional** for UDAGG definition.</span></span>


<span data-ttu-id="143be-246">A classe base permite passar três parâmetros abstratos: dois como parâmetros de entrada e um como resultado.</span><span class="sxs-lookup"><span data-stu-id="143be-246">The base class allows you to pass three abstract parameters: two as input parameters and one as the result.</span></span> <span data-ttu-id="143be-247">Os tipos de dados são variáveis e devem ser definidos durante a herança da classe.</span><span class="sxs-lookup"><span data-stu-id="143be-247">The data types are variable and should be defined during class inheritance.</span></span>

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

* <span data-ttu-id="143be-248">**Init** é invocado uma vez para cada grupo durante o cálculo.</span><span class="sxs-lookup"><span data-stu-id="143be-248">**Init** invokes once for each group during computation.</span></span> <span data-ttu-id="143be-249">Ele fornece uma rotina de inicialização para cada grupo de agregação.</span><span class="sxs-lookup"><span data-stu-id="143be-249">It provides an initialization routine for each aggregation group.</span></span>  
* <span data-ttu-id="143be-250">**Accumulate** é executado uma vez para cada valor.</span><span class="sxs-lookup"><span data-stu-id="143be-250">**Accumulate** is executed once for each value.</span></span> <span data-ttu-id="143be-251">Ele fornece a funcionalidade principal para o algoritmo de agregação.</span><span class="sxs-lookup"><span data-stu-id="143be-251">It provides the main functionality for the aggregation algorithm.</span></span> <span data-ttu-id="143be-252">Ele pode ser usado para agregar valores com vários tipos de dados que são definidos durante a herança da classe.</span><span class="sxs-lookup"><span data-stu-id="143be-252">It can be used to aggregate values with various data types that are defined during class inheritance.</span></span> <span data-ttu-id="143be-253">Ele pode aceitar dois parâmetros de tipos de dados variáveis.</span><span class="sxs-lookup"><span data-stu-id="143be-253">It can accept two parameters of variable data types.</span></span>
* <span data-ttu-id="143be-254">**Terminate** é executado uma vez por grupo de agregação no fim do processamento para gerar o resultado para cada grupo.</span><span class="sxs-lookup"><span data-stu-id="143be-254">**Terminate** is executed once per aggregation group at the end of processing to output the result for each group.</span></span>

<span data-ttu-id="143be-255">Para declarar tipos de dados de entrada e saída corretos, use a seguinte definição de classe:</span><span class="sxs-lookup"><span data-stu-id="143be-255">To declare correct input and output data types, use the class definition as follows:</span></span>

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* <span data-ttu-id="143be-256">T1: primeiro parâmetro para accumulate</span><span class="sxs-lookup"><span data-stu-id="143be-256">T1: First parameter to accumulate</span></span>
* <span data-ttu-id="143be-257">T2: primeiro parâmetro para accumulate</span><span class="sxs-lookup"><span data-stu-id="143be-257">T2: First parameter to accumulate</span></span>
* <span data-ttu-id="143be-258">TResult: tipo de retorno de terminate</span><span class="sxs-lookup"><span data-stu-id="143be-258">TResult: Return type of terminate</span></span>

<span data-ttu-id="143be-259">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="143be-259">For example:</span></span>

```
public class GuidAggregate : IAggregate<string, int, int>
```

<span data-ttu-id="143be-260">ou o</span><span class="sxs-lookup"><span data-stu-id="143be-260">or</span></span>

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a><span data-ttu-id="143be-261">Usar UDAGG no U-SQL</span><span class="sxs-lookup"><span data-stu-id="143be-261">Use UDAGG in U-SQL</span></span>
<span data-ttu-id="143be-262">Para usar a UDAGG, primeiramente defina-a no code-behind ou faça referência a ela na DLL de programação existente, conforme discutido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="143be-262">To use UDAGG, first define it in code-behind or reference it from the existent programmability DLL as discussed earlier.</span></span>

<span data-ttu-id="143be-263">Em seguida, use a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="143be-263">Then use the following syntax:</span></span>

```
AGG<UDAGG_functionname>(param1,param2)
```

<span data-ttu-id="143be-264">Veja um exemplo de UDAGG:</span><span class="sxs-lookup"><span data-stu-id="143be-264">Here is an example of UDAGG:</span></span>

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

<span data-ttu-id="143be-265">E o script base U-SQL:</span><span class="sxs-lookup"><span data-stu-id="143be-265">And base U-SQL script:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="143be-266">Nesse cenário de caso de uso, concatenamos os GUIDs de classe para usuários específicos.</span><span class="sxs-lookup"><span data-stu-id="143be-266">In this use-case scenario, we concatenate class GUIDs for the specific users.</span></span>

## <a name="use-user-defined-objects-udo"></a><span data-ttu-id="143be-267">Usar objetos definidos pelo usuário: UDO</span><span class="sxs-lookup"><span data-stu-id="143be-267">Use user-defined objects: UDO</span></span>
<span data-ttu-id="143be-268">O U-SQL permite definir objetos de programação personalizados que são chamados de objetos definidos pelo usuário ou UDO.</span><span class="sxs-lookup"><span data-stu-id="143be-268">U-SQL enables you to define custom programmability objects, which are called user-defined objects or UDO.</span></span>

<span data-ttu-id="143be-269">Veja a seguinte lista de UDO no U-SQL:</span><span class="sxs-lookup"><span data-stu-id="143be-269">The following is a list of UDO in U-SQL:</span></span>

* <span data-ttu-id="143be-270">Extratores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="143be-270">User-defined extractors</span></span>
    * <span data-ttu-id="143be-271">Extrair linha por linha</span><span class="sxs-lookup"><span data-stu-id="143be-271">Extract row by row</span></span>
    * <span data-ttu-id="143be-272">Usado para implementar extração de dados de arquivos estruturados personalizados</span><span class="sxs-lookup"><span data-stu-id="143be-272">Used to implement data extraction from custom structured files</span></span>

* <span data-ttu-id="143be-273">Outputters definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="143be-273">User-defined outputters</span></span>
    * <span data-ttu-id="143be-274">Gerar linha por linha</span><span class="sxs-lookup"><span data-stu-id="143be-274">Output row by row</span></span>
    * <span data-ttu-id="143be-275">Usado para gerar tipos de dados personalizados ou formatos de arquivo personalizado</span><span class="sxs-lookup"><span data-stu-id="143be-275">Used to output custom data types or custom file formats</span></span>

* <span data-ttu-id="143be-276">Processadores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="143be-276">User-defined processors</span></span>
    * <span data-ttu-id="143be-277">Usar uma linha e gerar uma linha</span><span class="sxs-lookup"><span data-stu-id="143be-277">Take one row and produce one row</span></span>
    * <span data-ttu-id="143be-278">Usado para reduzir o número de colunas ou produzir novas colunas com valores derivados de um conjunto de colunas existente</span><span class="sxs-lookup"><span data-stu-id="143be-278">Used to reduce the number of columns or produce new columns with values that are derived from an existing column set</span></span>

* <span data-ttu-id="143be-279">Aplicadores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="143be-279">User-defined appliers</span></span>
    * <span data-ttu-id="143be-280">Usar uma linha e gerar 0 para n linhas</span><span class="sxs-lookup"><span data-stu-id="143be-280">Take one row and produce 0 to n rows</span></span>
    * <span data-ttu-id="143be-281">Usado com OUTER/CROSS APPLY</span><span class="sxs-lookup"><span data-stu-id="143be-281">Used with OUTER/CROSS APPLY</span></span>

* <span data-ttu-id="143be-282">Combinadores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="143be-282">User-defined combiners</span></span>
    * <span data-ttu-id="143be-283">Combina conjuntos de linhas — JOINs definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="143be-283">Combines rowsets--user-defined JOINs</span></span>

* <span data-ttu-id="143be-284">Redutores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="143be-284">User-defined reducers</span></span>
    * <span data-ttu-id="143be-285">Usar n linhas e gerar uma linha</span><span class="sxs-lookup"><span data-stu-id="143be-285">Take n rows and produce one row</span></span>
    * <span data-ttu-id="143be-286">Usado para reduzir o número de linhas</span><span class="sxs-lookup"><span data-stu-id="143be-286">Used to reduce the number of rows</span></span>

<span data-ttu-id="143be-287">Geralmente, o UDO é chamado explicitamente no script U-SQL como parte das seguintes instruções U-SQL:</span><span class="sxs-lookup"><span data-stu-id="143be-287">UDO is typically called explicitly in U-SQL script as part of the following U-SQL statements:</span></span>

* <span data-ttu-id="143be-288">EXTRACT</span><span class="sxs-lookup"><span data-stu-id="143be-288">EXTRACT</span></span>
* <span data-ttu-id="143be-289">OUTPUT</span><span class="sxs-lookup"><span data-stu-id="143be-289">OUTPUT</span></span>
* <span data-ttu-id="143be-290">PROCESS</span><span class="sxs-lookup"><span data-stu-id="143be-290">PROCESS</span></span>
* <span data-ttu-id="143be-291">COMBINE</span><span class="sxs-lookup"><span data-stu-id="143be-291">COMBINE</span></span>
* <span data-ttu-id="143be-292">REDUCE</span><span class="sxs-lookup"><span data-stu-id="143be-292">REDUCE</span></span>

> [!NOTE]  
> <span data-ttu-id="143be-293">UDOs são limitados para consumir 0,5 GB de memória.</span><span class="sxs-lookup"><span data-stu-id="143be-293">UDO’s are limited to consume 0.5Gb memory.</span></span>  <span data-ttu-id="143be-294">Essa limitação de memória não se aplica a execuções locais.</span><span class="sxs-lookup"><span data-stu-id="143be-294">This memory limitation does not apply to local executions.</span></span>

## <a name="use-user-defined-extractors"></a><span data-ttu-id="143be-295">Usar extratores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="143be-295">Use user-defined extractors</span></span>
<span data-ttu-id="143be-296">O U-SQL permite importar dados externos usando uma instrução EXTRACT.</span><span class="sxs-lookup"><span data-stu-id="143be-296">U-SQL allows you to import external data by using an EXTRACT statement.</span></span> <span data-ttu-id="143be-297">Uma instrução EXTRACT pode usar extratores de UDO internos:</span><span class="sxs-lookup"><span data-stu-id="143be-297">An EXTRACT statement can use built-in UDO extractors:</span></span>  

* <span data-ttu-id="143be-298">*Extractors.Text()*: fornece extração dos arquivos de texto delimitados de diferentes codificações.</span><span class="sxs-lookup"><span data-stu-id="143be-298">*Extractors.Text()*: Provides extraction from delimited text files of different encodings.</span></span>

* <span data-ttu-id="143be-299">*Extractors.Csv()*: fornece extração de arquivos CSV (valores separados por vírgula) de diferentes codificações.</span><span class="sxs-lookup"><span data-stu-id="143be-299">*Extractors.Csv()*: Provides extraction from comma-separated value (CSV) files of different encodings.</span></span>

* <span data-ttu-id="143be-300">*Extractors.Tsv()*: fornece extração de arquivos TSV (valores separados por tabulação) de diferentes codificações.</span><span class="sxs-lookup"><span data-stu-id="143be-300">*Extractors.Tsv()*: Provides extraction from tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="143be-301">Pode ser útil desenvolver um extrator personalizado.</span><span class="sxs-lookup"><span data-stu-id="143be-301">It can be useful to develop a custom extractor.</span></span> <span data-ttu-id="143be-302">Isso pode ser útil durante a importação de dados para executar uma das seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="143be-302">This can be helpful during data import if we want to do any of the following tasks:</span></span>

* <span data-ttu-id="143be-303">Modificar dados de entrada ao dividir colunas e modificar os valores individuais.</span><span class="sxs-lookup"><span data-stu-id="143be-303">Modify input data by splitting columns and modifying individual values.</span></span> <span data-ttu-id="143be-304">A funcionalidade PROCESSOR é melhor para combinar colunas.</span><span class="sxs-lookup"><span data-stu-id="143be-304">The PROCESSOR functionality is better for combining columns.</span></span>
* <span data-ttu-id="143be-305">Analisar dados não estruturados, como páginas da Web e emails, ou semiestruturados, como XML/JSON.</span><span class="sxs-lookup"><span data-stu-id="143be-305">Parse unstructured data such as Web pages and emails, or semi-unstructured data such as XML/JSON.</span></span>
* <span data-ttu-id="143be-306">Analisar dados na codificação sem suporte.</span><span class="sxs-lookup"><span data-stu-id="143be-306">Parse data in unsupported encoding.</span></span>

<span data-ttu-id="143be-307">Para definir o extrator definido pelo usuário, ou UDE, precisamos criar uma interface `IExtractor`.</span><span class="sxs-lookup"><span data-stu-id="143be-307">To define a user-defined extractor, or UDE, we need to create an `IExtractor` interface.</span></span> <span data-ttu-id="143be-308">Todos os parâmetros de entrada para o extrator, como delimitadores de linha/coluna e codificação precisam ser definidos no construtor da classe.</span><span class="sxs-lookup"><span data-stu-id="143be-308">All input parameters to the extractor, such as column/row delimiters, and encoding, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="143be-309">A interface `IExtractor` também deve conter uma definição para a substituição `IEnumerable<IRow>` da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="143be-309">The `IExtractor`  interface should also contain a definition for the `IEnumerable<IRow>` override as follows:</span></span>

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

<span data-ttu-id="143be-310">O atributo **SqlUserDefinedExtractor** indica que o tipo deve ser registrado como um extrator definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-310">The **SqlUserDefinedExtractor** attribute indicates that the type should be registered as a user-defined extractor.</span></span> <span data-ttu-id="143be-311">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="143be-311">This class cannot be inherited.</span></span>

<span data-ttu-id="143be-312">SqlUserDefinedExtractor é um atributo opcional para a definição de UDE.</span><span class="sxs-lookup"><span data-stu-id="143be-312">SqlUserDefinedExtractor is an optional attribute for UDE definition.</span></span> <span data-ttu-id="143be-313">Ele é usado para definir a propriedade AtomicFileProcessing do objeto UDE.</span><span class="sxs-lookup"><span data-stu-id="143be-313">It used to define AtomicFileProcessing property for the UDE object.</span></span>

* <span data-ttu-id="143be-314">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="143be-314">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="143be-315">**true** = indica que esse extrator exige arquivos de entrada atômicos (JSON, XML, ...)</span><span class="sxs-lookup"><span data-stu-id="143be-315">**true** = Indicates that this extractor requires atomic input files (JSON, XML, ...)</span></span>
* <span data-ttu-id="143be-316">**false** = indica que esse extrator pode lidar com arquivos divididos/distribuídos (CSV, SEQ, ...)</span><span class="sxs-lookup"><span data-stu-id="143be-316">**false** = Indicates that this extractor can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="143be-317">Os principais objetos de programação do UDE são **input** e **output**.</span><span class="sxs-lookup"><span data-stu-id="143be-317">The main UDE programmability objects are **input** and **output**.</span></span> <span data-ttu-id="143be-318">O objeto de entrada é usado para enumerar os dados de entrada como `IUnstructuredReader`.</span><span class="sxs-lookup"><span data-stu-id="143be-318">The input object is used to enumerate input data as `IUnstructuredReader`.</span></span> <span data-ttu-id="143be-319">O objeto de saída é usado para definir os dados de saída como resultado da atividade extractor.</span><span class="sxs-lookup"><span data-stu-id="143be-319">The output object is used to set output data as a result of the extractor activity.</span></span>

<span data-ttu-id="143be-320">Os dados de entrada são acessados por meio de `System.IO.Stream` e `System.IO.StreamReader`.</span><span class="sxs-lookup"><span data-stu-id="143be-320">The input data is accessed through `System.IO.Stream` and `System.IO.StreamReader`.</span></span>

<span data-ttu-id="143be-321">Para enumeração de colunas de entrada, primeiramente dividimos o fluxo de entrada usando um delimitador de linha.</span><span class="sxs-lookup"><span data-stu-id="143be-321">For input columns enumeration, we first split the input stream by using a row delimiter.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

<span data-ttu-id="143be-322">Em seguida, dividimos ainda mais a linha de entrada em partes de coluna.</span><span class="sxs-lookup"><span data-stu-id="143be-322">Then, further split input row into column parts.</span></span>

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

<span data-ttu-id="143be-323">Para definir os dados de saída, usamos o método `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="143be-323">To set output data, we use the `output.Set` method.</span></span>

<span data-ttu-id="143be-324">É importante entender que o extrator personalizado só gera colunas e valores que são definidos com a saída.</span><span class="sxs-lookup"><span data-stu-id="143be-324">It's important to understand that the custom extractor only outputs columns and values that are defined with the output.</span></span> <span data-ttu-id="143be-325">Defina a chamada do método.</span><span class="sxs-lookup"><span data-stu-id="143be-325">Set method call.</span></span>

```
output.Set<string>(count, part);
```

<span data-ttu-id="143be-326">A saída real do extrator é disparada chamando `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="143be-326">The actual extractor output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="143be-327">Vejamos o exemplo do extrator:</span><span class="sxs-lookup"><span data-stu-id="143be-327">Following is the extractor example:</span></span>

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
         //Read the input line by line
         foreach (Stream current in input.Split(_encoding.GetBytes("\r\n")))
         {
        using (System.IO.StreamReader streamReader = new StreamReader(current, this._encoding))
         {
             line = streamReader.ReadToEnd().Trim();
             //Split the input by the column delimiter
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
                 // for column “user”, convert to UPPER case
                 output.Set<string>(count, part.ToUpper());

             }
             else
             {
                 // keep the rest of the columns as-is
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

<span data-ttu-id="143be-328">Nesse cenário de caso de uso, o extrator regenera o GUID para a coluna "guid" e converte os valores da coluna "usuário" em letras maiúsculas.</span><span class="sxs-lookup"><span data-stu-id="143be-328">In this use-case scenario, the extractor regenerates the GUID for “guid” column and converts the values of “user” column to upper case.</span></span> <span data-ttu-id="143be-329">Os extratores personalizados podem produzir resultados mais complicados ao analisar dados de entrada e manipulá-los.</span><span class="sxs-lookup"><span data-stu-id="143be-329">Custom extractors can produce more complicated results by parsing input data and manipulating it.</span></span>

<span data-ttu-id="143be-330">Script base U-SQL que usa um extrator personalizado:</span><span class="sxs-lookup"><span data-stu-id="143be-330">Following is base U-SQL script that uses a custom extractor:</span></span>

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

OUTPUT @rs0 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-outputters"></a><span data-ttu-id="143be-331">Usar outputters definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="143be-331">Use user-defined outputters</span></span>
<span data-ttu-id="143be-332">O outputter definido pelo usuário é outro UDO do U-SQL que permite estender uma funcionalidade interna do U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-332">User-defined outputter is another U-SQL UDO that allows you to extend built-in U-SQL functionality.</span></span> <span data-ttu-id="143be-333">Assim como o extrator, há vários outputters internos.</span><span class="sxs-lookup"><span data-stu-id="143be-333">Similar to the extractor, there are several built-in outputters.</span></span>

* <span data-ttu-id="143be-334">*Outputters.Text()*: grava dados em arquivos de texto delimitados de codificações diferentes.</span><span class="sxs-lookup"><span data-stu-id="143be-334">*Outputters.Text()*: Writes data to delimited text files of different encodings.</span></span>
* <span data-ttu-id="143be-335">*Outputters.Csv()*: grava dados em arquivos CSV (valores separados por vírgula) de codificações diferentes.</span><span class="sxs-lookup"><span data-stu-id="143be-335">*Outputters.Csv()*: Writes data to comma-separated value (CSV) files of different encodings.</span></span>
* <span data-ttu-id="143be-336">*Outputters.Tsv()*: grava dados em arquivos TSV (valores separados por tabulação) de codificações diferentes.</span><span class="sxs-lookup"><span data-stu-id="143be-336">*Outputters.Tsv()*: Writes data to tab-separated value (TSV) files of different encodings.</span></span>

<span data-ttu-id="143be-337">O outputter personalizado permite gravar dados em um formato definido personalizado.</span><span class="sxs-lookup"><span data-stu-id="143be-337">Custom outputter allows you to write data in a custom defined format.</span></span> <span data-ttu-id="143be-338">Isso pode ser útil para as seguintes tarefas:</span><span class="sxs-lookup"><span data-stu-id="143be-338">This can be useful for the following tasks:</span></span>

* <span data-ttu-id="143be-339">Gravando dados em arquivos semiestruturados ou não estruturados.</span><span class="sxs-lookup"><span data-stu-id="143be-339">Writing data to semi-structured or unstructured files.</span></span>
* <span data-ttu-id="143be-340">Gravar dados em codificações sem suporte.</span><span class="sxs-lookup"><span data-stu-id="143be-340">Writing data not supported encodings.</span></span>
* <span data-ttu-id="143be-341">Modificar dados de saída ou adicionar atributos personalizados.</span><span class="sxs-lookup"><span data-stu-id="143be-341">Modifying output data or adding custom attributes.</span></span>

<span data-ttu-id="143be-342">Para definir o outputter definido pelo usuário, precisamos criar a interface `IOutputter`.</span><span class="sxs-lookup"><span data-stu-id="143be-342">To define user-defined outputter, we need to create the `IOutputter` interface.</span></span>

<span data-ttu-id="143be-343">A seguir temos a implementação da classe `IOutputter` base:</span><span class="sxs-lookup"><span data-stu-id="143be-343">Following is the base `IOutputter` class implementation:</span></span>

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

<span data-ttu-id="143be-344">Todos os parâmetros de entrada para o outputter, como delimitadores de linha/coluna, codificação e afins precisam ser definidos no construtor da classe.</span><span class="sxs-lookup"><span data-stu-id="143be-344">All input parameters to the outputter, such as column/row delimiters, encoding, and so on, need to be defined in the constructor of the class.</span></span> <span data-ttu-id="143be-345">A interface `IOutputter` também deve conter uma definição para a substituição `void Output`.</span><span class="sxs-lookup"><span data-stu-id="143be-345">The `IOutputter` interface should also contain a definition for `void Output` override.</span></span> <span data-ttu-id="143be-346">O atributo `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` pode ser definido opcionalmente para o processamento de arquivos atômico.</span><span class="sxs-lookup"><span data-stu-id="143be-346">The attribute `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` can optionally be set for atomic file processing.</span></span> <span data-ttu-id="143be-347">Para saber mais, consulte os detalhes a seguir.</span><span class="sxs-lookup"><span data-stu-id="143be-347">For more information, see the following details.</span></span>

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

* <span data-ttu-id="143be-348">`Output` é chamado para cada linha de entrada.</span><span class="sxs-lookup"><span data-stu-id="143be-348">`Output` is called for each input row.</span></span> <span data-ttu-id="143be-349">Retorna o conjunto de linhas `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="143be-349">It returns the `IUnstructuredWriter output` rowset.</span></span>
* <span data-ttu-id="143be-350">A classe Constructor é usada para passar parâmetros ao outputter definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-350">The Constructor class is used to pass parameters to the user-defined outputter.</span></span>
* <span data-ttu-id="143be-351">`Close` é usado para, opcionalmente, substituir e liberar estado caro ou determinar quando a última linha foi gravada.</span><span class="sxs-lookup"><span data-stu-id="143be-351">`Close` is used to optionally override to release expensive state or determine when the last row was written.</span></span>

<span data-ttu-id="143be-352">O atributo **SqlUserDefinedOutputter** indica que o tipo deve ser registrado como um outputter definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-352">**SqlUserDefinedOutputter** attribute indicates that the type should be registered as a user-defined outputter.</span></span> <span data-ttu-id="143be-353">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="143be-353">This class cannot be inherited.</span></span>

<span data-ttu-id="143be-354">SqlUserDefinedOutputter é um atributo opcional para a definição de um outputter definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-354">SqlUserDefinedOutputter is an optional attribute for a user-defined outputter definition.</span></span> <span data-ttu-id="143be-355">Ele é usado para definir a propriedade AtomicFileProcessing.</span><span class="sxs-lookup"><span data-stu-id="143be-355">It's used to define the AtomicFileProcessing property.</span></span>

* <span data-ttu-id="143be-356">bool     AtomicFileProcessing</span><span class="sxs-lookup"><span data-stu-id="143be-356">bool     AtomicFileProcessing</span></span>   

* <span data-ttu-id="143be-357">**true** = indica que esse outputter exige arquivos de saída atômicos (JSON, XML, ...)</span><span class="sxs-lookup"><span data-stu-id="143be-357">**true** = Indicates that this outputter requires atomic output files (JSON, XML, ...)</span></span>
* <span data-ttu-id="143be-358">**false** = indica que esse outputter pode lidar com arquivos divididos/distribuídos (CSV, SEQ, ...)</span><span class="sxs-lookup"><span data-stu-id="143be-358">**false** = Indicates that this outputter can deal with split / distributed files (CSV, SEQ, ...)</span></span>

<span data-ttu-id="143be-359">Os principais objetos de programação são **row** e **output**.</span><span class="sxs-lookup"><span data-stu-id="143be-359">The main programmability objects are **row** and **output**.</span></span> <span data-ttu-id="143be-360">O objeto **row** é usado para enumerar os dados de saída como interface `IRow`.</span><span class="sxs-lookup"><span data-stu-id="143be-360">The **row** object is used to enumerate output data as `IRow` interface.</span></span> <span data-ttu-id="143be-361">**Saída** é usado para definir os dados de saída para o arquivo de destino.</span><span class="sxs-lookup"><span data-stu-id="143be-361">**Output** is used to set output data to the target file.</span></span>

<span data-ttu-id="143be-362">Os dados de saída são acessados por meio da interface `IRow`.</span><span class="sxs-lookup"><span data-stu-id="143be-362">The output data is accessed through the `IRow` interface.</span></span> <span data-ttu-id="143be-363">Os dados de saída são passados em uma linha por vez.</span><span class="sxs-lookup"><span data-stu-id="143be-363">Output data is passed a row at a time.</span></span>

<span data-ttu-id="143be-364">Os valores individuais são enumerados chamando o método Get da interface IRow:</span><span class="sxs-lookup"><span data-stu-id="143be-364">The individual values are enumerated by calling the Get method of the IRow interface:</span></span>

```
row.Get<string>("column_name")
```

<span data-ttu-id="143be-365">Os nomes de coluna individuais podem ser determinados chamando `row.Schema`:</span><span class="sxs-lookup"><span data-stu-id="143be-365">Individual column names can be determined by calling `row.Schema`:</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="143be-366">Essa abordagem permite que criar um outputter flexível para qualquer esquema de metadados.</span><span class="sxs-lookup"><span data-stu-id="143be-366">This approach enables you to build a flexible outputter for any metadata schema.</span></span>

<span data-ttu-id="143be-367">Os dados de saída são gravados em um arquivo usando `System.IO.StreamWriter`.</span><span class="sxs-lookup"><span data-stu-id="143be-367">The output data is written to file by using `System.IO.StreamWriter`.</span></span> <span data-ttu-id="143be-368">O parâmetro de fluxo é definido como `output.BaseStrea` como parte do `IUnstructuredWriter output`.</span><span class="sxs-lookup"><span data-stu-id="143be-368">The stream parameter is set to `output.BaseStrea` as part of `IUnstructuredWriter output`.</span></span>

<span data-ttu-id="143be-369">Observe que é importante liberar o buffer de dados para o arquivo depois de cada iteração de linha.</span><span class="sxs-lookup"><span data-stu-id="143be-369">Note that it's important to flush the data buffer to the file after each row iteration.</span></span> <span data-ttu-id="143be-370">Além disso, o objeto `StreamWriter` deve ser usado com o atributo Disposable habilitado (padrão) e a palavra-chave **using**:</span><span class="sxs-lookup"><span data-stu-id="143be-370">In addition, the `StreamWriter` object must be used with the Disposable attribute enabled (default) and with the **using** keyword:</span></span>

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

<span data-ttu-id="143be-371">Caso contrário, chame o método Flush() explicitamente depois de cada iteração.</span><span class="sxs-lookup"><span data-stu-id="143be-371">Otherwise, call Flush() method explicitly after each iteration.</span></span> <span data-ttu-id="143be-372">Vamos mostrar isso no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="143be-372">We show this in the following example.</span></span>

### <a name="set-headers-and-footers-for-user-defined-outputter"></a><span data-ttu-id="143be-373">Definir cabeçalhos e rodapés para outputter definido pelo usuário</span><span class="sxs-lookup"><span data-stu-id="143be-373">Set headers and footers for user-defined outputter</span></span>
<span data-ttu-id="143be-374">Para definir um cabeçalho, use o fluxo de execução única de iteração.</span><span class="sxs-lookup"><span data-stu-id="143be-374">To set a header, use single iteration execution flow.</span></span>

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

<span data-ttu-id="143be-375">O código no primeiro bloco `if (isHeaderRow)` é executado apenas uma vez.</span><span class="sxs-lookup"><span data-stu-id="143be-375">The code in the first `if (isHeaderRow)` block is executed only once.</span></span>

<span data-ttu-id="143be-376">Para o rodapé, use a referência à instância do objeto `System.IO.Stream` (`output.BaseStream`).</span><span class="sxs-lookup"><span data-stu-id="143be-376">For the footer, use the reference to the instance of `System.IO.Stream` object (`output.BaseStream`).</span></span> <span data-ttu-id="143be-377">Escreva o rodapé no método Close () da interface `IOutputter`.</span><span class="sxs-lookup"><span data-stu-id="143be-377">Write the footer in the Close() method of the `IOutputter` interface.</span></span>  <span data-ttu-id="143be-378">(Para saber mais, veja a seção a seguir.)</span><span class="sxs-lookup"><span data-stu-id="143be-378">(For more information, see the following example.)</span></span>

<span data-ttu-id="143be-379">Veja um exemplo de um outputter definido pelo usuário:</span><span class="sxs-lookup"><span data-stu-id="143be-379">Following is an example of a user-defined outputter:</span></span>

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

    // The Close method is used to write the footer to the file. It's executed only once, after all rows
    public override void Close().
    {
    //Reference to IO.Stream object - g_writer
    StreamWriter streamWriter = new StreamWriter(g_writer, this.encoding);
    streamWriter.Write("</table>");
    streamWriter.Flush();
    streamWriter.Close();
    }

    public override void Output(IRow row, IUnstructuredWriter output)
    {
    System.IO.StreamWriter streamWriter = new StreamWriter(output.BaseStream, this.encoding);

    // Metadata schema initialization to enumerate column names
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
        // Data type enumeration--required to match the distinct list of types from OUTPUT statement
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
    // Reference to the instance of the IO.Stream object for footer generation
    g_writer = output.BaseStream;
    streamWriter.Flush();
    }
}

// Define the factory classes
public static class Factory
{
    public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
    {
    return new HTMLOutputter(isHeader, encoding);
    }
}
```

<span data-ttu-id="143be-380">E o script base U-SQL:</span><span class="sxs-lookup"><span data-stu-id="143be-380">And U-SQL base script:</span></span>

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
    TO @output_file 
    USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="143be-381">Esse é um outputter HTML, que cria um arquivo HTML com dados da tabela.</span><span class="sxs-lookup"><span data-stu-id="143be-381">This is an HTML outputter, which creates an HTML file with table data.</span></span>

### <a name="call-outputter-from-u-sql-base-script"></a><span data-ttu-id="143be-382">Chamando outputter do script base U-SQL</span><span class="sxs-lookup"><span data-stu-id="143be-382">Call outputter from U-SQL base script</span></span>
<span data-ttu-id="143be-383">Para chamar um outputter personalizado do script base U-SQL, a nova instância do objeto outputter deve ser criada.</span><span class="sxs-lookup"><span data-stu-id="143be-383">To call a custom outputter from the base U-SQL script, the new instance of the outputter object has to be created.</span></span>

```sql
OUTPUT @rs0 TO @output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

<span data-ttu-id="143be-384">Para evitar a criação de uma instância do objeto no script base, podemos criar um wrapper de função, conforme mostrado em nosso exemplo anterior:</span><span class="sxs-lookup"><span data-stu-id="143be-384">To avoid creating an instance of the object in base script, we can create a function wrapper, as shown in our earlier example:</span></span>

```c#
        // Define the factory classes
        public static class Factory
        {
            public static HTMLOutputter HTMLOutputter(bool isHeader = false, Encoding encoding = null)
            {
                return new HTMLOutputter(isHeader, encoding);
            }
        }
```

<span data-ttu-id="143be-385">Nesse caso, a chamada original se parece com esta:</span><span class="sxs-lookup"><span data-stu-id="143be-385">In this case, the original call looks like the following:</span></span>

```
OUTPUT @rs0 
TO @output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a><span data-ttu-id="143be-386">Usar processadores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="143be-386">Use user-defined processors</span></span>
<span data-ttu-id="143be-387">O processador definido pelo usuário, ou UDP, é um tipo de UDO do U-SQL que permite processar as linhas de entrada aplicando recursos de programação.</span><span class="sxs-lookup"><span data-stu-id="143be-387">User-defined processor, or UDP, is a type of U-SQL UDO that enables you to process the incoming rows by applying programmability features.</span></span> <span data-ttu-id="143be-388">O UDP permite combinar colunas, modificar valores e adicionar novas colunas, se necessário.</span><span class="sxs-lookup"><span data-stu-id="143be-388">UDP enables you to combine columns, modify values, and add new columns if necessary.</span></span> <span data-ttu-id="143be-389">Basicamente, ele ajuda a processar um conjunto de linhas para produzir elementos de dados necessários.</span><span class="sxs-lookup"><span data-stu-id="143be-389">Basically, it helps to process a rowset to produce required data elements.</span></span>

<span data-ttu-id="143be-390">Para definir um UDP, precisamos criar uma interface `IProcessor` com o atributo `SqlUserDefinedProcessor`, que é opcional para o UDP.</span><span class="sxs-lookup"><span data-stu-id="143be-390">To define a UDP, we need to create an `IProcessor` interface with the `SqlUserDefinedProcessor` attribute, which is optional for UDP.</span></span>

<span data-ttu-id="143be-391">Essa interface deve conter a definição para a substituição do conjunto de linhas de interface `IRow`, conforme mostrado no exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="143be-391">This interface should contain the definition for the `IRow` interface rowset override, as shown in the following example:</span></span>

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

<span data-ttu-id="143be-392">**SqlUserDefinedProcessor** indica que o tipo deve ser registrado como um processador definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-392">**SqlUserDefinedProcessor** indicates that the type should be registered as a user-defined processor.</span></span> <span data-ttu-id="143be-393">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="143be-393">This class cannot be inherited.</span></span>

<span data-ttu-id="143be-394">O atributo SqlUserDefinedProcessor é **opcional** para a definição de UDP.</span><span class="sxs-lookup"><span data-stu-id="143be-394">The SqlUserDefinedProcessor attribute is **optional** for UDP definition.</span></span>

<span data-ttu-id="143be-395">Os principais objetos de programação são **input** e **output**.</span><span class="sxs-lookup"><span data-stu-id="143be-395">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="143be-396">O objeto Input é usado para enumerar dados de entrada e saída e para definir dados de saída como resultado da atividade do processador.</span><span class="sxs-lookup"><span data-stu-id="143be-396">The input object is used to enumerate input columns and output, and to set output data as a result of the processor activity.</span></span>

<span data-ttu-id="143be-397">Para enumeração de colunas de entrada, usamos o método `input.Get`.</span><span class="sxs-lookup"><span data-stu-id="143be-397">For input columns enumeration, we use the `input.Get` method.</span></span>

```
string column_name = input.Get<string>("column_name");
```

<span data-ttu-id="143be-398">O parâmetro para o método `input.Get` é uma coluna passada como parte da cláusula `PRODUCE` da instrução `PROCESS` do script base U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-398">The parameter for `input.Get` method is a column that's passed as part of the `PRODUCE` clause of the `PROCESS` statement of the U-SQL base script.</span></span> <span data-ttu-id="143be-399">Precisamos usar o tipo de dados correto aqui.</span><span class="sxs-lookup"><span data-stu-id="143be-399">We need to use the correct data type here.</span></span>

<span data-ttu-id="143be-400">Para saída, use o método `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="143be-400">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="143be-401">É importante observar que o produtor personalizado gera apenas colunas e valores definidos com a chamada de método `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="143be-401">It's important to note that custom producer only outputs columns and values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", mycolumn);
```

<span data-ttu-id="143be-402">A saída real do processador é disparada chamando `return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="143be-402">The actual processor output is triggered by calling `return output.AsReadOnly();`.</span></span>

<span data-ttu-id="143be-403">Veja abaixo um exemplo de processador:</span><span class="sxs-lookup"><span data-stu-id="143be-403">Following is a processor example:</span></span>

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

<span data-ttu-id="143be-404">Nesse cenário de caso de uso, o processador está gerando a nova coluna chamada "full_description" combinando as colunas existentes, nesse caso, "user" em letras maiúsculas e "des".</span><span class="sxs-lookup"><span data-stu-id="143be-404">In this use-case scenario, the processor is generating a new column called “full_description” by combining the existing columns--in this case, “user” in upper case, and “des”.</span></span> <span data-ttu-id="143be-405">Ele também regenera um GUID e retorna o original, bem como novos valores de GUID.</span><span class="sxs-lookup"><span data-stu-id="143be-405">It also regenerates a GUID and returns the original and new GUID values.</span></span>

<span data-ttu-id="143be-406">Como você pode ver no exemplo anterior, é possível chamar métodos C# durante a chamada de método `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="143be-406">As you can see from the previous example, you can call C# methods during `output.Set` method call.</span></span>

<span data-ttu-id="143be-407">Abaixo temos um exemplo de script base U-SQL que usa um processador personalizado:</span><span class="sxs-lookup"><span data-stu-id="143be-407">Following is an example of base U-SQL script that uses a custom processor:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

## <a name="use-user-defined-appliers"></a><span data-ttu-id="143be-408">Usar aplicadores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="143be-408">Use user-defined appliers</span></span>
<span data-ttu-id="143be-409">O aplicador definido pelo usuário do U-SQL permite invocar uma função C# personalizada para cada linha retornada pela expressão de tabela externa de uma consulta.</span><span class="sxs-lookup"><span data-stu-id="143be-409">A U-SQL user-defined applier enables you to invoke a custom C# function for each row that's returned by the outer table expression of a query.</span></span> <span data-ttu-id="143be-410">A entrada à direita é avaliada para cada linha a começar da entrada à esquerda e as linhas que são produzidas são combinadas para a saída final.</span><span class="sxs-lookup"><span data-stu-id="143be-410">The right input is evaluated for each row from the left input, and the rows that are produced are combined for the final output.</span></span> <span data-ttu-id="143be-411">A lista de colunas produzida pelo operador APPLY é a combinação do conjunto de colunas na entrada à esquerda e à direita.</span><span class="sxs-lookup"><span data-stu-id="143be-411">The list of columns that are produced by the APPLY operator are the combination of the set of columns in the left and the right input.</span></span>

<span data-ttu-id="143be-412">O aplicador definido pelo usuário está sendo invocado como parte da expressão SELECT do U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-412">User-defined applier is being invoked as part of the USQL SELECT expression.</span></span>

<span data-ttu-id="143be-413">A chamada característica ao aplicador definidor pelo usuário se parece com esta:</span><span class="sxs-lookup"><span data-stu-id="143be-413">The typical call to the user-defined applier looks like the following:</span></span>

```
SELECT …
FROM …
CROSS APPLYis used to pass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

<span data-ttu-id="143be-414">Para saber mais sobre como usar aplicadores na expressão SELECT., veja [U-SQL SELECT selecionando de CROSS APPLY e OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span><span class="sxs-lookup"><span data-stu-id="143be-414">For more information about using appliers in a SELECT expression, see [U-SQL SELECT Selecting from CROSS APPLY and OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).</span></span>

<span data-ttu-id="143be-415">A definição de classe base do aplicador definido pelo usuário é a seguinte:</span><span class="sxs-lookup"><span data-stu-id="143be-415">The user-defined applier base class definition is as follows:</span></span>

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

<span data-ttu-id="143be-416">Para definir um aplicador definido pelo usuário, precisamos criar a interface `IApplier` com o atributo [`SqlUserDefinedApplier`], que é opcional para a definição de aplicador definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-416">To define a user-defined applier, we need to create the `IApplier` interface with the [`SqlUserDefinedApplier`] attribute, which is optional for a user-defined applier definition.</span></span>

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

* <span data-ttu-id="143be-417">Apply é chamado para cada linha da tabela outer.</span><span class="sxs-lookup"><span data-stu-id="143be-417">Apply is called for each row of the outer table.</span></span> <span data-ttu-id="143be-418">Ele retorna o conjunto de linhas de saída `IUpdatableRow`.</span><span class="sxs-lookup"><span data-stu-id="143be-418">It returns the `IUpdatableRow` output rowset.</span></span>
* <span data-ttu-id="143be-419">A classe Constructor é usada para passar parâmetros ao aplicador definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-419">The Constructor class is used to pass parameters to the user-defined applier.</span></span>

<span data-ttu-id="143be-420">**SqlUserDefinedApplier** indica que o tipo deve ser registrado como um aplicador definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-420">**SqlUserDefinedApplier** indicates that the type should be registered as a user-defined applier.</span></span> <span data-ttu-id="143be-421">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="143be-421">This class cannot be inherited.</span></span>

<span data-ttu-id="143be-422">O atributo **SqlUserDefinedApplier** é **opcional** para a definição do aplicador definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-422">**SqlUserDefinedApplier** is **optional** for a user-defined applier definition.</span></span>


<span data-ttu-id="143be-423">Os principais objetos de programação são os seguintes:</span><span class="sxs-lookup"><span data-stu-id="143be-423">The main programmability objects are as follows:</span></span>

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

<span data-ttu-id="143be-424">Os conjuntos de linhas de entrada são passados como entrada `IRow`.</span><span class="sxs-lookup"><span data-stu-id="143be-424">Input rowsets are passed as `IRow` input.</span></span> <span data-ttu-id="143be-425">As linhas de saída são geradas como a interface de saída `IUpdatableRow`.</span><span class="sxs-lookup"><span data-stu-id="143be-425">The output rows are generated as `IUpdatableRow` output interface.</span></span>

<span data-ttu-id="143be-426">Os nomes de coluna individuais podem ser determinados pela chamada do método de esquema `IRow`.</span><span class="sxs-lookup"><span data-stu-id="143be-426">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="143be-427">Para obter os valores de dados reais do `IRow` de entrada, usamos o método Get() da interface `IRow`.</span><span class="sxs-lookup"><span data-stu-id="143be-427">To get the actual data values from the incoming `IRow`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="143be-428">Ou, então, usamos o nome de coluna de esquema:</span><span class="sxs-lookup"><span data-stu-id="143be-428">Or we use the schema column name:</span></span>

```
row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="143be-429">Os valores de saída devem ser definidos com a saída `IUpdatableRow`:</span><span class="sxs-lookup"><span data-stu-id="143be-429">The output values must be set with `IUpdatableRow` output:</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="143be-430">É importante entender que o aplicador personalizado só produz colunas e valores definidos com a chamada ao método `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="143be-430">It is important to understand that custom appliers only output columns and values that are defined with `output.Set` method call.</span></span>

<span data-ttu-id="143be-431">A saída real é disparada chamando `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="143be-431">The actual output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="143be-432">Os parâmetros de aplicador definido pelo usuário podem ser passados para o construtor.</span><span class="sxs-lookup"><span data-stu-id="143be-432">The user-defined applier parameters can be passed to the constructor.</span></span> <span data-ttu-id="143be-433">O aplicador pode retornar um número variável de colunas que precisa ser definido durante a chamada ao aplicador no script base U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-433">Applier can return a variable number of columns that need to be defined during the applier call in base U-SQL Script.</span></span>

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

<span data-ttu-id="143be-434">Veja abaixo o exemplo do aplicador definido pelo usuário:</span><span class="sxs-lookup"><span data-stu-id="143be-434">Here is the user-defined applier example:</span></span>

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

<span data-ttu-id="143be-435">Abaixo está o script base U-SQL para esse aplicador definido pelo usuário:</span><span class="sxs-lookup"><span data-stu-id="143be-435">Following is the base U-SQL script for this user-defined applier:</span></span>

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

OUTPUT @rs1 TO @output_file USING Outputters.Text();
```

<span data-ttu-id="143be-436">Nesse cenário de caso de uso, o aplicador definido pelo usuário atua como um analisador de valor delimitado por vírgula para as propriedades de frota de carros.</span><span class="sxs-lookup"><span data-stu-id="143be-436">In this use case scenario, user-defined applier acts as a comma-delimited value parser for the car fleet properties.</span></span> <span data-ttu-id="143be-437">As linhas do arquivo de entrada têm a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="143be-437">The input file rows look like the following:</span></span>

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

<span data-ttu-id="143be-438">Trata-se de um típico arquivo TSV delimitado por tab com a coluna de propriedades contendo propriedades do carro, como fabricante e modelo.</span><span class="sxs-lookup"><span data-stu-id="143be-438">It is a typical tab-delimited TSV file with a properties column that contains car properties such as make and model.</span></span> <span data-ttu-id="143be-439">Essas propriedades precisam ser analisadas pelas colunas da tabela.</span><span class="sxs-lookup"><span data-stu-id="143be-439">Those properties must be parsed to the table columns.</span></span> <span data-ttu-id="143be-440">O aplicador fornecido também permite gerar um número dinâmico de propriedades no conjunto de linhas de resultados, com base no parâmetro que é passado.</span><span class="sxs-lookup"><span data-stu-id="143be-440">The applier that's provided also enables you to generate a dynamic number of properties in the result rowset, based on the parameter that's passed.</span></span> <span data-ttu-id="143be-441">Você pode gerar todas as propriedades ou somente um conjunto específico de propriedades.</span><span class="sxs-lookup"><span data-stu-id="143be-441">You can generate either all properties or a specific set of properties only.</span></span>

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

<span data-ttu-id="143be-442">O aplicador definido pelo usuário pode ser chamado como uma nova instância do objeto do aplicador:</span><span class="sxs-lookup"><span data-stu-id="143be-442">The user-defined applier can be called as a new instance of applier object:</span></span>

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

<span data-ttu-id="143be-443">Ou com a invocação de um método de fábrica wrapper:</span><span class="sxs-lookup"><span data-stu-id="143be-443">Or with the invocation of a wrapper factory method:</span></span>

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a><span data-ttu-id="143be-444">Usar combinadores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="143be-444">Use user-defined combiners</span></span>
<span data-ttu-id="143be-445">O combinador definido pelo usuário, ou UDC, permite combinar linhas dos conjuntos de linhas esquerdo e direito, com base em lógica personalizada.</span><span class="sxs-lookup"><span data-stu-id="143be-445">User-defined combiner, or UDC, enables you to combine rows from left and right rowsets, based on custom logic.</span></span> <span data-ttu-id="143be-446">O Combinador Definido pelo Usuário é usado com a expressão COMBINE.</span><span class="sxs-lookup"><span data-stu-id="143be-446">User-defined combiner is used with COMBINE expression.</span></span>

<span data-ttu-id="143be-447">Um combinador está sendo invocado com a expressão COMBINE, que fornece as informações necessárias sobre os conjuntos de linhas de entrada, as colunas de agrupamento, o esquema de resultado esperado e as informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="143be-447">A combiner is being invoked with the COMBINE expression that provides the necessary information about both the input rowsets, the grouping columns, the expected result schema, and additional information.</span></span>

<span data-ttu-id="143be-448">Para chamar um combinador em um script base U-SQL, usamos a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="143be-448">To call a combiner in a base U-SQL script, we use the following syntax:</span></span>

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

<span data-ttu-id="143be-449">Para saber mais, veja [Expressão COMBINE (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span><span class="sxs-lookup"><span data-stu-id="143be-449">For more information, see [COMBINE Expression (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).</span></span>

<span data-ttu-id="143be-450">Para definir um combinador definido pelo usuário, precisamos criar a interface `ICombiner` com o atributo [`SqlUserDefinedCombiner`], que é opcional para a definição do combinador definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-450">To define a user-defined combiner, we need to create the `ICombiner` interface with the [`SqlUserDefinedCombiner`] attribute, which is optional for a user-defined Combiner definition.</span></span>

<span data-ttu-id="143be-451">Definição da classe `ICombiner` base:</span><span class="sxs-lookup"><span data-stu-id="143be-451">Base `ICombiner` class definition:</span></span>

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

<span data-ttu-id="143be-452">A implementação personalizada de uma interface `ICombiner` deve conter a definição para uma substituição Combine `IEnumerable<IRow>`.</span><span class="sxs-lookup"><span data-stu-id="143be-452">The custom implementation of an `ICombiner` interface should contain the definition for an `IEnumerable<IRow>` Combine override.</span></span>

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

<span data-ttu-id="143be-453">O atributo **SqlUserDefinedCombiner** indica que o tipo deve ser registrado como um combinador definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-453">The **SqlUserDefinedCombiner** attribute indicates that the type should be registered as a user-defined combiner.</span></span> <span data-ttu-id="143be-454">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="143be-454">This class cannot be inherited.</span></span>

<span data-ttu-id="143be-455">**SqlUserDefinedCombiner** é usado para definir a propriedade do modo Combinador.</span><span class="sxs-lookup"><span data-stu-id="143be-455">**SqlUserDefinedCombiner** is used to define the Combiner mode property.</span></span> <span data-ttu-id="143be-456">É um atributo opcional para a definição do combinador definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-456">It is an optional attribute for a user-defined combiner definition.</span></span>

<span data-ttu-id="143be-457">Modo CombinerMode</span><span class="sxs-lookup"><span data-stu-id="143be-457">CombinerMode     Mode</span></span>

<span data-ttu-id="143be-458">A enumeração CombinerMode pode usar os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="143be-458">CombinerMode enum can take the following values:</span></span>

* <span data-ttu-id="143be-459">Completo (0) Cada linha de saída depende potencialmente de todas as linhas de entrada da esquerda e direita com o mesmo valor de chave.</span><span class="sxs-lookup"><span data-stu-id="143be-459">Full  (0) Every output row potentially depends on all the input rows from left and right       with the same key value.</span></span>

* <span data-ttu-id="143be-460">Esquerda (1) Cada linha de saída depende de uma única linha de entrada da esquerda (e potencialmente de todas as linhas da direita com o mesmo valor de chave).</span><span class="sxs-lookup"><span data-stu-id="143be-460">Left  (1) Every output row depends on a single input row from the left (and potentially all rows       from the right with the same key value).</span></span>

* <span data-ttu-id="143be-461">Direita (2) Cada linha de saída depende de uma única linha de entrada da direita (e potencialmente de todas as linhas da esquerda com o mesmo valor de chave).</span><span class="sxs-lookup"><span data-stu-id="143be-461">Right (2)     Every output row depends on a single input row from the right (and potentially all rows       from the left with the same key value).</span></span>

* <span data-ttu-id="143be-462">Interno (3) Cada linha de saída depende de uma única linha de entrada da esquerda e direita com o mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="143be-462">Inner (3) Every output row depends on a single input row from left and right with the same value.</span></span>

<span data-ttu-id="143be-463">Exemplo:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span><span class="sxs-lookup"><span data-stu-id="143be-463">Example:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]</span></span>


<span data-ttu-id="143be-464">Os principais objetos de programação são:</span><span class="sxs-lookup"><span data-stu-id="143be-464">The main programmability objects are:</span></span>

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

<span data-ttu-id="143be-465">Os conjuntos de linhas de entrada são passados como tipo `IRowset` **esquerdo** e **direito** da interface.</span><span class="sxs-lookup"><span data-stu-id="143be-465">Input rowsets are passed as **left** and **right** `IRowset` type of interface.</span></span> <span data-ttu-id="143be-466">Ambos os conjuntos de linhas precisam ser enumerados para processamento.</span><span class="sxs-lookup"><span data-stu-id="143be-466">Both rowsets must be enumerated for processing.</span></span> <span data-ttu-id="143be-467">Você só pode enumerar cada interface uma vez e, portanto, temos que enumerá-las e armazená-las se necessário.</span><span class="sxs-lookup"><span data-stu-id="143be-467">You can only enumerate each interface once, so we have to enumerate and cache it if necessary.</span></span>

<span data-ttu-id="143be-468">Para fins de caching, podemos criar um tipo List\<T\> de estrutura de memória como resultado de uma execução da consulta LINQ, especificamente List<`IRow`>.</span><span class="sxs-lookup"><span data-stu-id="143be-468">For caching purposes, we can create a List\<T\> type of memory structure as a result of a LINQ query execution, specifically List<`IRow`>.</span></span> <span data-ttu-id="143be-469">O tipo de dados anônimo também pode ser usado durante a enumeração.</span><span class="sxs-lookup"><span data-stu-id="143be-469">The anonymous data type can be used during enumeration as well.</span></span>

<span data-ttu-id="143be-470">Veja [Introdução a consultas LINQ (C#)](https://msdn.microsoft.com/library/bb397906.aspx) para obter mais informações sobre consultas LINQ e [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) para obter mais informações sobre a interface IEnumerable\<T\>.</span><span class="sxs-lookup"><span data-stu-id="143be-470">See [Introduction to LINQ Queries (C#)](https://msdn.microsoft.com/library/bb397906.aspx) for more information about LINQ queries, and [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) for more information about IEnumerable\<T\> interface.</span></span>

<span data-ttu-id="143be-471">Para obter os valores de dados reais do `IRowset` de entrada, usamos o método Get() da interface `IRow`.</span><span class="sxs-lookup"><span data-stu-id="143be-471">To get the actual data values from the incoming `IRowset`, we use the Get() method of `IRow` interface.</span></span>

```
mycolumn = row.Get<int>("mycolumn")
```

<span data-ttu-id="143be-472">Os nomes de coluna individuais podem ser determinados pela chamada do método de esquema `IRow`.</span><span class="sxs-lookup"><span data-stu-id="143be-472">Individual column names can be determined by calling the `IRow` Schema method.</span></span>

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

<span data-ttu-id="143be-473">Ou usando o nome de coluna de esquema:</span><span class="sxs-lookup"><span data-stu-id="143be-473">Or by using the schema column name:</span></span>

```
c# row.Get<int>(row.Schema[0].Name)
```

<span data-ttu-id="143be-474">A enumeração geral com o LINQ se parece com este exemplo:</span><span class="sxs-lookup"><span data-stu-id="143be-474">The general enumeration with LINQ looks like the following:</span></span>

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

<span data-ttu-id="143be-475">Depois de enumerar os dois conjuntos de linhas, vamos executar um loop por todas as linhas.</span><span class="sxs-lookup"><span data-stu-id="143be-475">After enumerating both rowsets, we are going to loop through all rows.</span></span> <span data-ttu-id="143be-476">Para cada linha no conjunto de linhas à esquerda, vamos localizar todas as linhas que satisfazem a condição de nosso combinador.</span><span class="sxs-lookup"><span data-stu-id="143be-476">For each row in the left rowset, we are going to find all rows that satisfy the condition of our combiner.</span></span>

<span data-ttu-id="143be-477">Os valores de saída devem ser definidos com a saída `IUpdatableRow`.</span><span class="sxs-lookup"><span data-stu-id="143be-477">The output values must be set with `IUpdatableRow` output.</span></span>

```
output.Set<int>("mycolumn", mycolumn)
```

<span data-ttu-id="143be-478">A saída real é disparada chamando `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="143be-478">The actual output is triggered by calling to `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="143be-479">Veja abaixo um exemplo do combinador:</span><span class="sxs-lookup"><span data-stu-id="143be-479">Following is a combiner example:</span></span>

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

<span data-ttu-id="143be-480">Nesse cenário de caso de uso, estamos criando um relatório de análise para o varejista.</span><span class="sxs-lookup"><span data-stu-id="143be-480">In this use-case scenario, we are building an analytics report for the retailer.</span></span> <span data-ttu-id="143be-481">O objetivo é encontrar todos os produtos que custam mais de US$ 20,000 e são vendidos por meio de sites mais rapidamente do que pelo varejista comum durante determinado período.</span><span class="sxs-lookup"><span data-stu-id="143be-481">The goal is to find all products that cost more than $20,000 and that sell through the website faster than through the regular retailer within a certain time frame.</span></span>

<span data-ttu-id="143be-482">Veja abaixo o script base U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-482">Here is the base U-SQL script.</span></span> <span data-ttu-id="143be-483">Você pode comparar a lógica entre JOIN regular e um combinador:</span><span class="sxs-lookup"><span data-stu-id="143be-483">You can compare the logic between a regular JOIN and a combiner:</span></span>

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

OUTPUT @rs1 TO @output_file1 USING Outputters.Tsv();
OUTPUT @rs2 TO @output_file2 USING Outputters.Tsv();
```

<span data-ttu-id="143be-484">O combinador definido pelo usuário pode ser chamado como uma nova instância do objeto do aplicador:</span><span class="sxs-lookup"><span data-stu-id="143be-484">A user-defined combiner can be called as a new instance of the applier object:</span></span>

```
USING new MyNameSpace.MyCombiner();
```


<span data-ttu-id="143be-485">Ou com a invocação de um método de fábrica wrapper:</span><span class="sxs-lookup"><span data-stu-id="143be-485">Or with the invocation of a wrapper factory method:</span></span>

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a><span data-ttu-id="143be-486">Usar redutores definidos pelo usuário</span><span class="sxs-lookup"><span data-stu-id="143be-486">Use user-defined reducers</span></span>

<span data-ttu-id="143be-487">O U-SQL permite escrever redutores de conjunto de linhas personalizados em C# usando a estrutura de extensibilidade do operador definido pelo usuário e implementando uma interface IReducer.</span><span class="sxs-lookup"><span data-stu-id="143be-487">U-SQL enables you to write custom rowset reducers in C# by using the user-defined operator extensibility framework and implementing an IReducer interface.</span></span>

<span data-ttu-id="143be-488">O redutor definido pelo usuário, ou UDR, pode ser usado para eliminar linhas desnecessárias durante a extração (importação) de dados.</span><span class="sxs-lookup"><span data-stu-id="143be-488">User-defined reducer, or UDR, can be used to eliminate unnecessary rows during data extraction (import).</span></span> <span data-ttu-id="143be-489">Ele também pode ser usado para manipular e avaliar as linhas e colunas.</span><span class="sxs-lookup"><span data-stu-id="143be-489">It also can be used to manipulate and evaluate rows and columns.</span></span> <span data-ttu-id="143be-490">Com base na lógica de programação, ele também pode definir quais linhas precisam ser extraídas.</span><span class="sxs-lookup"><span data-stu-id="143be-490">Based on programmability logic, it can also define which rows need to be extracted.</span></span>

<span data-ttu-id="143be-491">Para definir uma classe UDR, precisamos criar uma interface `IReducer` com um atributo `SqlUserDefinedReducer` opcional.</span><span class="sxs-lookup"><span data-stu-id="143be-491">To define a UDR class, we need to create an `IReducer` interface with an optional `SqlUserDefinedReducer` attribute.</span></span>

<span data-ttu-id="143be-492">Essa interface de classe deve conter uma definição para substituição do conjunto de linhas da interface `IEnumerable`.</span><span class="sxs-lookup"><span data-stu-id="143be-492">This class interface should contain a definition for the `IEnumerable` interface rowset override.</span></span>

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

<span data-ttu-id="143be-493">O atributo **SqlUserDefinedReducer** indica que o tipo deve ser registrado como um redutor definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-493">The **SqlUserDefinedReducer** attribute indicates that the type should be registered as a user-defined reducer.</span></span> <span data-ttu-id="143be-494">Essa classe não pode ser herdada.</span><span class="sxs-lookup"><span data-stu-id="143be-494">This class cannot be inherited.</span></span>
<span data-ttu-id="143be-495">**SqlUserDefinedReducer** é um atributo opcional para a definição do redutor definido pelo usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-495">**SqlUserDefinedReducer** is an optional attribute for a user-defined reducer definition.</span></span> <span data-ttu-id="143be-496">Ele é usado para definir a propriedade IsRecursive.</span><span class="sxs-lookup"><span data-stu-id="143be-496">It's used to define IsRecursive property.</span></span>

* <span data-ttu-id="143be-497">bool     IsRecursive</span><span class="sxs-lookup"><span data-stu-id="143be-497">bool     IsRecursive</span></span>    
* <span data-ttu-id="143be-498">**true**  = indica se esse Redutor é idempotente</span><span class="sxs-lookup"><span data-stu-id="143be-498">**true**  = Indicates whether this Reducer is idempotent</span></span>

<span data-ttu-id="143be-499">Os principais objetos de programação são **input** e **output**.</span><span class="sxs-lookup"><span data-stu-id="143be-499">The main programmability objects are **input** and **output**.</span></span> <span data-ttu-id="143be-500">O objeto de entrada é usado para enumerar linhas de entrada.</span><span class="sxs-lookup"><span data-stu-id="143be-500">The input object is used to enumerate input rows.</span></span> <span data-ttu-id="143be-501">Output é usado para definir as linhas de saída como resultado da redução da atividade.</span><span class="sxs-lookup"><span data-stu-id="143be-501">Output is used to set output rows as a result of reducing activity.</span></span>

<span data-ttu-id="143be-502">Para enumeração de linhas de entrada, usamos o método `Row.Get`.</span><span class="sxs-lookup"><span data-stu-id="143be-502">For input rows enumeration, we use the `Row.Get` method.</span></span>

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

<span data-ttu-id="143be-503">O parâmetro para o método `Row.Get` é uma coluna passada como parte da classe `PRODUCE` da instrução `REDUCE` do script base U-SQL.</span><span class="sxs-lookup"><span data-stu-id="143be-503">The parameter for the `Row.Get` method is a column that's passed as part of the `PRODUCE` class of the `REDUCE` statement of the U-SQL base script.</span></span> <span data-ttu-id="143be-504">Precisamos usar o tipo de dados correto aqui também.</span><span class="sxs-lookup"><span data-stu-id="143be-504">We need to use the correct data type here as well.</span></span>

<span data-ttu-id="143be-505">Para saída, use o método `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="143be-505">For output, use the `output.Set` method.</span></span>

<span data-ttu-id="143be-506">É importante entender que redutor personalizado apenas produz valores que são definidos com a chamada de método `output.Set`.</span><span class="sxs-lookup"><span data-stu-id="143be-506">It is important to understand that custom reducer only outputs values that are defined with the `output.Set` method call.</span></span>

```
output.Set<string>("mycolumn", guid);
```

<span data-ttu-id="143be-507">A saída real do redutor é disparada chamando `yield return output.AsReadOnly();`.</span><span class="sxs-lookup"><span data-stu-id="143be-507">The actual reducer output is triggered by calling `yield return output.AsReadOnly();`.</span></span>

<span data-ttu-id="143be-508">Abaixo temos um exemplo de redutor:</span><span class="sxs-lookup"><span data-stu-id="143be-508">Following is a reducer example:</span></span>

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

<span data-ttu-id="143be-509">Nesse cenário de caso de uso, o redutor está ignorando linhas com um nome de usuário vazio.</span><span class="sxs-lookup"><span data-stu-id="143be-509">In this use-case scenario, the reducer is skipping rows with an empty user name.</span></span> <span data-ttu-id="143be-510">Para cada linha no conjunto de linhas, ele lê cada coluna necessária e avalia o comprimento do nome do usuário.</span><span class="sxs-lookup"><span data-stu-id="143be-510">For each row in rowset, it reads each required column, then evaluates the length of the user name.</span></span> <span data-ttu-id="143be-511">Ele só produz a linha real se o comprimento do valor de nome de usuário for maior que 0.</span><span class="sxs-lookup"><span data-stu-id="143be-511">It outputs the actual row only if user name value length is more than 0.</span></span>

<span data-ttu-id="143be-512">Abaixo temos um script base U-SQL que usa um redutor personalizado:</span><span class="sxs-lookup"><span data-stu-id="143be-512">Following is base U-SQL script that uses a custom reducer:</span></span>

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
    TO @output_file 
    USING Outputters.Text();
```
