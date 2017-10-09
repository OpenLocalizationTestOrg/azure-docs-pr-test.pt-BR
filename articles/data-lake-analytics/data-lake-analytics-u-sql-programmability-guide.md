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
# <a name="u-sql-programmability-guide"></a>Guia de programação do U-SQL

O U-SQL é uma linguagem de consulta projetada para o tipo big data de cargas de trabalho. Um dos recursos exclusivos de saudação do U-SQL é a combinação de saudação de linguagem declarativa do tipo SQL Olá com extensibilidade hello e programação que é fornecida pelo c#. Neste guia, nos concentraremos nas extensibilidade hello e programação da linguagem de U-SQL Olá habilitado por c#.

## <a name="requirements"></a>Requisitos

Baixe e instale as [Ferramentas do Azure Data Lake para Visual Studio](https://www.microsoft.com/download/details.aspx?id=49504).

## <a name="get-started-with-u-sql"></a>Introdução ao U-SQL  

Vejamos Olá script U-SQL a seguir:

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

Ele define um conjunto de linhas chamado @a e cria um conjunto de linhas chamado @results de @a.

## <a name="c-types-and-expressions-in-u-sql-script"></a>Tipos e expressões de C# no script U-SQL

Uma expressão de U-SQL é uma expressão de C# combinada com operações lógicas U-SQL como `AND`, `OR` e `NOT`. Expressões U-SQL podem ser usadas com SELECT, EXTRACT, WHERE, HAVING, GROUP BY e DECLARE.

Por exemplo, Olá script a seguir analisa uma cadeia de um valor DateTime na cláusula SELECT hello.

```
@results =
    SELECT
        customer,
    amount,
    DateTime.Parse(date) AS date
    FROM @a;    
```

Olá script a seguir analisa uma cadeia de caracteres de um valor de data e hora em uma instrução DECLARE.

```
DECLARE @d DateTime = ToDateTime.Date("2016/01/01");
```

### <a name="use-c-expressions-for-data-type-conversions"></a>Usar expressões C# para conversões de tipo de dados
saudação de exemplo a seguir demonstra como você pode fazer uma conversão de dados de data e hora usando expressões de c#. Neste cenário específico, dados de data e hora da cadeia de caracteres são convertida toostandard datetime com notação de hora 00:00:00 meia-noite.

```
DECLARE @dt String = "2016-07-06 10:23:15";

@rs1 =
    SELECT 
        Convert.ToDateTime(Convert.ToDateTime(@dt).ToString("yyyy-MM-dd")) AS dt,
        dt AS olddt
    FROM @rs0;
OUTPUT @rs1 too@output_file USING Outputters.Text();
```

### <a name="use-c-expressions-for-todays-date"></a>Usar expressões C# para a data de hoje
toopull a data de hoje, podemos usar Olá expressão c# a seguir:

```
DateTime.Now.ToString("M/d/yyyy")
```

Aqui está um exemplo de como toouse essa expressão em um script:

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



## <a name="using-net-assemblies"></a>Usando assemblies .NET
Modelo de extensibilidade do U-SQL se baseia no código personalizado do hello capacidade tooadd. Atualmente, U-SQL fornece maneiras fáceis tooadd sua própria Microsoft. Código de rede (em especial, c#). No entanto, você também pode adicionar código personalizado escrito em outras linguagens .NET, como VB.NET ou F#. 

### <a name="register-a-net-assembly"></a>Registrar um assembly .NET

Use tooplace de instrução de CREATE ASSEMBLY hello um assembly do .NET em um banco de dados de U-SQL. Quando um assembly é um banco de dados, scripts U-SQL podem usar esses assemblies usando a instrução de referência de ASSEMBLY hello. 

Olá mostrado no código a seguir como tooregister um assembly:

```
CREATE ASSEMBLY MyDB.[MyAssembly]
    FROM "/myassembly.dll";
```

Olá mostrado no código a seguir como tooreference um assembly:

```
REFERENCE ASSEMBLY MyDB.[MyAssembly];
```

Consulte Olá [instruções de registro do assembly](https://blogs.msdn.microsoft.com/azuredatalake/2016/08/26/how-to-register-u-sql-assemblies-in-your-u-sql-catalog/) que abrange a este tópico mais detalhadamente.


### <a name="use-assembly-versioning"></a>Usar o controle de versão do assembly
Atualmente, U-SQL usa saudação do .NET Framework versão 4.5. Portanto, certifique-se de que seus próprios assemblies são compatíveis com essa versão do tempo de execução de saudação.

Conforme mencionado anteriormente, o U-SQL executa código em um formato de 64 bits (x64). Portanto, certifique-se de que seu código seja compilado toorun em x64. Caso contrário, você obterá o erro de formato incorreto de saudação mostrado anteriormente.

Cada arquivo de recurso e DLL de assembly carregado, como um tempo de execução diferente, um assembly nativo ou um arquivo config, pode ter no máximo 400 MB. tamanho total de saudação de recursos implantados, por meio do recurso de IMPLANTAR ou por meio de referências tooassemblies e seus arquivos adicionais, não pode exceder 3 GB.

Por fim, observe que cada banco de dados U-SQL pode conter apenas uma versão de qualquer determinado assembly. Por exemplo, se você precisar tanto versão 7 e 8 do hello NewtonSoft Json.Net biblioteca, você precisa tooregistê-los em dois bancos de dados diferentes. Além disso, cada script só pode fazer referência a versão de tooone de um determinado assembly DLL. Nesse sentido, U-SQL segue Olá c# assembly gerenciamento e controle de versão de semântica.


## <a name="use-user-defined-functions-udf"></a>Funções definidas pelo usuário: UDF
Funções definidas pelo usuário U-SQL ou UDF, estiver programando rotinas que aceitam parâmetros, executam uma ação (como um cálculo complexo) e retornam Olá resultado dessa ação como um valor. Olá retornar o valor de UDF só pode ser um único valor escalar. A UDF do U-SQL pode ser chamado no script base U-SQL como qualquer outra função escalar C#.

Recomendamos que você inicialize as funções do U-SQL definidas pelo usuário como **públicas** e **estáticas**.

```
public static string MyFunction(string param1)
{
    return "my result";
}
```

Primeiro vamos examinar Olá o exemplo simples de criação de um UDF.

Neste cenário de caso de uso, é preciso toodetermine Olá período fiscal, incluindo o trimestre fiscal hello e mês fiscal do hello entrar pela primeira vez para usuário específico hello. Olá primeiro mês fiscal do ano de saudação em nosso cenário é junho.

período de toocalculate, apresentamos Olá função c# a seguir:

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

Ela simplesmente calcula o mês e o trimestre fiscal e retorna um valor de cadeia de caracteres. Junho, Olá primeiro mês do hello primeiro trimestre fiscal, usamos "Q1:P1". No caso de julho, usamos "Q1:P2" e assim por diante.

Essa é uma regular c# função que estamos toouse contínuo em nosso projeto U-SQL.

Aqui está a aparência da seção de código por trás de saudação neste cenário:

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

Agora, vamos toocall essa função de script U-SQL de base de saudação. toodo isso, temos tooprovide um nome totalmente qualificado para a função hello, incluindo o namespace de saudação, que nesse caso é NameSpace.Class.Function(parameter).

```
USQL_Programmability.CustomFunctions.GetFiscalPeriod(dt)
```

O seguinte é script base do hello real U-SQL:

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

O seguinte é um arquivo de saída Olá Olá da execução do script:

```
0d8b9630-d5ca-11e5-8329-251efa3a2941,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User1",""

20843640-d771-11e5-b87b-8b7265c75a44,2016-02-11T07:04:17.2630000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User2",""

301f23d2-d690-11e5-9a98-4b4f60a1836f,2016-02-11T09:01:33.9720000-08:00,2016-06-01T00:00:00.0000000,"Q3:8","User3",""
```

Esse exemplo demonstra um uso simples de UDF embutida no U-SQL.

### <a name="keep-state-between-udf-invocations"></a>Manter o estado entre invocações da UDF
Objetos de programação c# U-SQL podem ser mais sofisticados, utilizando a interatividade por meio de variáveis globais do hello por trás do código. Vamos examinar Olá seguindo o cenário de caso de uso de negócios.

Em grandes organizações, os usuários podem alternar entre diversos aplicativos internos. Eles podem incluir o Microsoft Dynamics CRM, o PowerBI e assim por diante. Os clientes talvez queira tooapply uma análise de telemetria de como os usuários alternam entre diferentes aplicativos, o uso de saudação mostra as tendências são e assim por diante. meta de Hello para empresas Olá é toooptimize o uso do aplicativo. Eles também seja toocombine diferentes aplicativos ou as rotinas de logon específicas.

tooachieve essa meta, temos toodetermine IDs de sessão e o tempo de atraso entre hello última sessão que ocorreu.

Precisamos toofind uma entrada anterior e, em seguida, atribuir esse sessões de entrada tooall que estão sendo gerado toohello mesmo aplicativo. Olá primeiro desafio é que script base U-SQL não permite nos cálculos de tooapply colunas já calculado com a função LAG. Olá segundo desafio é que temos de sessão específica do tookeep Olá para todas as sessões em Olá mesmo período de tempo.

toosolve esse problema, usamos uma variável global dentro de uma seção de lógica: `static public string globalSession;`.

Essa variável global é aplicado toohello todo conjunto de linhas durante a execução do nosso script.

Aqui é Olá por trás do código da seção de nosso programa U-SQL:

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

Este exemplo mostra Olá variável global `static public string globalSession;` usada dentro de saudação `getStampUserSession` função e Obtendo reinicializada cada sessão de parâmetro for alterado de saudação do tempo.

Olá U-SQL script base é o seguinte:

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

Função `USQLApplication21.UserSession.getStampUserSession(UserSessionTimestamp)` é chamado aqui durante o cálculo de conjunto de linhas de memória segundo hello. Ele passa Olá `UserSessionTimestamp` Olá valor até que a coluna e retorna `UserSessionTimestamp` foi alterado.

arquivo de saída de saudação é da seguinte maneira:

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

Este exemplo demonstra um cenário de caso de uso mais complicado que usamos uma variável global dentro de uma seção de lógica que é o conjunto de linhas do toohello aplicada memória inteira.

## <a name="use-user-defined-types-udt"></a>Tipos de CLR definidos pelo usuário: UDT
Os tipos definidos pelo usuário, ou UDT, são outro recurso de programação do U-SQL. O UDT do U-SQL atua como um tipo definido pelo usuário regular de C#. C# é uma linguagem fortemente tipada que permite o uso de saudação de tipos internos e personalizados definidos pelo usuário.

U-SQL implicitamente não é possível serializar ou desserializar UDTs arbitrários quando Olá UDT é transmitido entre vértices em conjuntos de linhas. Isso significa que o usuário Olá tem tooprovide um formatador explícita usando Olá IFormatter interface. Isso fornece U-SQL com hello serializar e desserializar métodos para Olá UDT.

> [!NOTE]
> U-SQL Extratores internos e outputters atualmente não é possível serializar ou desserializar tooor de dados UDT de arquivos mesmo com hello IFormatter conjunto. Portanto, quando você está escrevendo o arquivo de tooa dados UDT com hello declaração de saída ou lê-lo com um extrator, você tem toopass-lo como uma cadeia de caracteres ou matriz de bytes. Em seguida, você chamar serialização hello e a desserialização de código (ou seja, o método ToString () de saudação do UDT) explicitamente. Extratores definidas pelo usuário e outputters em outros Olá mão, podem ler e gravar UDTs.

Se tentarmos toouse UDT EXTRATOR ou OUTPUTTER (fora da seleção anterior), conforme mostrado aqui:

```
@rs1 =
    SELECT 
        MyNameSpace.Myfunction_Returning_UDT(filed1) AS myfield
    FROM @rs0;

OUTPUT @rs1 
    too@output_file 
    USING Outputters.Text();
```

Recebemos Olá erro a seguir:

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

toowork com UDT no outputter, podemos ter tooserialize-toostring com hello método ToString () ou criar um outputter personalizado.

Atualmente, os UDTs não podem ser usados em GROUP BY. Se o UDT é usado em GROUP BY, Olá erro a seguir é gerada:

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

toodefine um UDT, temos:

* Adicione Olá namespaces a seguir:

```
using Microsoft.Analytics.Interfaces
using System.IO;
```

* Adicionar `Microsoft.Analytics.Interfaces`, que é necessário para as interfaces UDT de saudação. Além disso, `System.IO` pode ser a interface de IFormatter Olá toodefine necessários.

* Defina o tipo definido usado com o atributo SqlUserDefinedType.

**SqlUserDefinedType** é toomark usada uma definição de tipo em um assembly como um tipo definido pelo usuário (UDT) em U-SQL. Propriedades de saudação no atributo Olá refletem características físicas de saudação do hello UDT. Essa classe não pode ser herdada.

SqlUserDefinedType é um atributo necessário para a definição de UDT.

Construtor de saudação da classe hello:  

* SqlUserDefinedTypeAttribute(type formatter)

* Formatador do tipo: necessário parâmetro toodefine um formatador UDT — especificamente, o tipo de saudação da saudação `IFormatter` interface deve ser passada aqui.

```
[SqlUserDefinedType(typeof(MyTypeFormatter))]
public class MyType
{ … }
```

* UDT típico também requer a definição da interface de IFormatter hello, conforme mostrado no exemplo a seguir de saudação:

```
public class MyTypeFormatter : IFormatter<MyType>
{
    public void Serialize(MyType instance, IColumnWriter writer, ISerializationContext context)
    { … }

    public MyType Deserialize(IColumnReader reader, ISerializationContext context)
    { … }
}
```

Olá `IFormatter` interface serializa e desfaz a serialização de um gráfico de objeto com tipo de raiz de saudação do \<typeparamref name = "T" >.

\<typeparam name = "T" > Olá tipo raiz para Olá objeto gráfico tooserialize e desserializar.

* **Desserializar**: desfaz a serialização de dados Olá fluxo Olá fornecido e reconstitui gráfico Olá de objetos.

* **Serializar**: serializa um objeto ou o gráfico de objetos, com hello recebe o fluxo de toohello fornecido de raiz.

`MyType`instância: instância de tipo hello.  
`IColumnWriter`Gravador / `IColumnReader` leitor: Olá subjacente de fluxo de coluna.  
`ISerializationContext`contexto: Enum que define um conjunto de sinalizadores que especifica o contexto de origem ou destino de saudação de fluxo Olá durante a serialização.

* **Intermediário**: Especifica o contexto Olá origem ou destino não é um armazenamento persistente.

* **Persistência**: Especifica o contexto Olá origem ou destino é um armazenamento persistente.

Como um tipo C# regular, uma definição de UDT do U-SQL pode incluir substituições para operadores como +/==/!=. Ele também pode incluir métodos estáticos. Por exemplo, se formos toouse desse UDT como uma função de agregação MIN U-SQL de tooa do parâmetro, temos toodefine < substituição de operador.

Neste guia, demonstramos um exemplo de identificação do período fiscal de data de saudação específica no formato Olá Qn:Pn (Q1:P10). saudação de exemplo a seguir mostra como toodefine um tipo personalizado para os valores do período fiscais.

Abaixo temos um exemplo de uma seção code-behind com interface IFormatter e UDT personalizado:

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

tipo definido Hello inclui dois números: trimestre e mês. Os operadores ==/!=/>/< e o método estático ToString() são definidos aqui.

Como mencionado anteriormente, o UDT pode ser usado nas expressões SELECT, mas não pode ser usado em OUTPUTTER/EXTRACTOR sem serialização personalizada. Ele tem toobe serializado como uma cadeia de caracteres com ToString () ou usados com um OUTPUTTER/EXTRATOR personalizado.

Agora, vamos falar sobre o uso do UDT. Em uma seção de lógica, alteramos nossas seguinte de toohello GetFiscalPeriod função:

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

Como você pode ver, ele retorna o valor de saudação do nosso tipo FiscalPeriod.

Aqui, fornecemos um exemplo de como a toouse-lo posteriormente no script base U-SQL. Este exemplo demonstra as diferentes formas de invocação do UDT no script U-SQL.

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

Veja um exemplo de uma seção completa code-behind:

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

## <a name="use-user-defined-aggregates-udagg"></a>Use agregações definidas pelo usuário: UDAGG
As agregações definidas pelo usuário são funções relacionadas à agregação que não são enviadas para uso imediato com o U-SQL. exemplo Hello pode ser uma agregação tooperform matemáticas personalizadas cálculos concatenações, manipulações de cadeias de caracteres e assim por diante.

a definição de classe base de agregação definida pelo usuário Olá é o seguinte:

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

**SqlUserDefinedAggregate** indica que o tipo de saudação deve ser registrado como uma agregação definida pelo usuário. Essa classe não pode ser herdada.

O atributo SqlUserDefinedType é **opcional** para a definição de UDAGG.


Olá classe base permite que você toopass três parâmetros de abstrata: dois como parâmetros de entrada e outra como resultado de saudação. tipos de dados de saudação são variáveis e devem ser definidos durante a herança de classe.

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

* **Init** é invocado uma vez para cada grupo durante o cálculo. Ele fornece uma rotina de inicialização para cada grupo de agregação.  
* **Accumulate** é executado uma vez para cada valor. Ele fornece funcionalidade principal Olá para o algoritmo de agregação de saudação. Pode ser usado tooaggregate valores com vários tipos de dados que são definidos durante a herança de classe. Ele pode aceitar dois parâmetros de tipos de dados variáveis.
* **Encerrar** é executada uma vez por grupo de agregação no final de saudação do processamento toooutput Olá resultado para cada grupo.

entrada correta toodeclare e tipos de dados de saída, use a definição de classe hello como segue:

```
public abstract class IAggregate<T1, T2, TResult> : IAggregate
```

* T1: Primeiro parâmetro tooaccumulate
* T2: Primeiro parâmetro tooaccumulate
* TResult: tipo de retorno de terminate

Por exemplo:

```
public class GuidAggregate : IAggregate<string, int, int>
```

ou o

```
public class GuidAggregate : IAggregate<string, string, string>
```

### <a name="use-udagg-in-u-sql"></a>Usar UDAGG no U-SQL
primeiro, toouse UDAGG, defini-lo no code-behind ou fazer referência de programação existente de saudação DLL conforme discutido anteriormente.

Em seguida, use Olá sintaxe a seguir:

```
AGG<UDAGG_functionname>(param1,param2)
```

Veja um exemplo de UDAGG:

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

E o script base U-SQL:

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

Neste cenário de caso de uso, podemos concatenar GUIDs de classe para usuários específicos hello.

## <a name="use-user-defined-objects-udo"></a>Usar objetos definidos pelo usuário: UDO
U-SQL permite que objetos de programação personalizada toodefine, que são chamados objetos definidos pelo usuário ou do UDO.

a seguir Olá é uma lista de UDO em U-SQL:

* Extratores definidos pelo usuário
    * Extrair linha por linha
    * Usado tooimplement extração de dados de arquivos estruturados personalizados

* Outputters definidos pelo usuário
    * Gerar linha por linha
    * Usado toooutput tipos de dados personalizados ou formatos de arquivo personalizados

* Processadores definidos pelo usuário
    * Usar uma linha e gerar uma linha
    * Tooreduce usado Olá o número de colunas ou produzir novas colunas com valores que são derivados de um conjunto de coluna existente

* Aplicadores definidos pelo usuário
    * Coloque uma linha e produzir 0 linhas toon
    * Usado com OUTER/CROSS APPLY

* Combinadores definidos pelo usuário
    * Combina conjuntos de linhas — JOINs definidos pelo usuário

* Redutores definidos pelo usuário
    * Usar n linhas e gerar uma linha
    * Usado tooreduce Olá número de linhas

UDO é geralmente chamado explicitamente no script U-SQL como parte da saudação instruções U-SQL a seguir:

* EXTRACT
* OUTPUT
* PROCESS
* COMBINE
* REDUCE

> [!NOTE]  
> UDO é limitados tooconsume 0,5 Gb memória.  Essa limitação de memória não se aplica a toolocal execuções.

## <a name="use-user-defined-extractors"></a>Usar extratores definidos pelo usuário
U-SQL permite que dados externos tooimport usando uma instrução de EXTRAÇÃO. Uma instrução EXTRACT pode usar extratores de UDO internos:  

* *Extractors.Text()*: fornece extração dos arquivos de texto delimitados de diferentes codificações.

* *Extractors.Csv()*: fornece extração de arquivos CSV (valores separados por vírgula) de diferentes codificações.

* *Extractors.Tsv()*: fornece extração de arquivos TSV (valores separados por tabulação) de diferentes codificações.

Ele pode ser útil toodevelop um extrator personalizado. Isso pode ser útil durante a importação de dados se quisermos toodo qualquer uma das seguintes tarefas de saudação:

* Modificar dados de entrada ao dividir colunas e modificar os valores individuais. Olá funcionalidade do processador é melhor para a combinação de colunas.
* Analisar dados não estruturados, como páginas da Web e emails, ou semiestruturados, como XML/JSON.
* Analisar dados na codificação sem suporte.

toodefine extrator de definida pelo usuário, ou excluir, precisamos toocreate um `IExtractor` interface. Todas as entrada extrator de toohello parâmetros, como delimitadores de coluna/linha e a codificação, precisam toobe definida no construtor de saudação da classe de saudação. Olá `IExtractor` interface também deve conter uma definição para Olá `IEnumerable<IRow>` substituir da seguinte maneira:

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

Olá **SqlUserDefinedExtractor** atributo indica que tipo de saudação deve ser registrado como um extrator definido pelo usuário. Essa classe não pode ser herdada.

SqlUserDefinedExtractor é um atributo opcional para a definição de UDE. Ele usado toodefine AtomicFileProcessing propriedade para o objeto de uir hello.

* bool     AtomicFileProcessing   

* **true** = indica que esse extrator exige arquivos de entrada atômicos (JSON, XML, ...)
* **false** = indica que esse extrator pode lidar com arquivos divididos/distribuídos (CSV, SEQ, ...)

os objetos de programação uir principais Olá são **entrada** e **saída**. objeto de entrada Hello está dados de entrada usado tooenumerate como `IUnstructuredReader`. saudação do objeto de saída é usada tooset dados de saída como resultado da atividade de extrator de saudação.

dados de entrada Hello são acessados por meio de `System.IO.Stream` e `System.IO.StreamReader`.

Para a enumeração de colunas de entrada do primeiro dividiremos fluxo de entrada hello usando um delimitador de linha.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
}
```

Em seguida, dividimos ainda mais a linha de entrada em partes de coluna.

```
foreach (Stream current in input.Split(my_row_delimiter))
{
…
    string[] parts = line.Split(my_column_delimiter);
    foreach (string part in parts)
    { … }
}
```

dados de saída tooset, usamos Olá `output.Set` método.

É importante toounderstand que Olá extrator personalizado produz somente colunas e valores que são definidos com saída de hello. Defina a chamada do método.

```
output.Set<string>(count, part);
```

saída do Hello extrator real é disparada pela chamada `yield return output.AsReadOnly();`.

O seguinte é um exemplo extrator de hello:

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

Neste cenário de caso de uso, extrator de saudação regenera Olá GUID para a coluna "guid" e converte os valores de saudação do caso de tooupper de coluna de "usuário". Os extratores personalizados podem produzir resultados mais complicados ao analisar dados de entrada e manipulá-los.

Script base U-SQL que usa um extrator personalizado:

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

## <a name="use-user-defined-outputters"></a>Usar outputters definidos pelo usuário
Outputter definida pelo usuário é outro UDO U-SQL que permite a você uma funcionalidade interna tooextend U-SQL. Extrator de toohello semelhante, há vários outputters internos.

* *Outputters.Text()*: grava dados toodelimited arquivos de texto de codificações diferentes.
* *Outputters.Csv()*: grava arquivos de (CSV) de diferentes codificações de valor toocomma separada dos dados.
* *Outputters.Tsv()*: grava arquivos de (TSV) diferentes codificações de valor tootab separada dos dados.

Outputter personalizada permite que você toowrite dados em um formato definido personalizado. Isso pode ser útil para Olá tarefas a seguir:

* Gravando arquivos de dados estruturados toosemi ou não estruturados.
* Gravar dados em codificações sem suporte.
* Modificar dados de saída ou adicionar atributos personalizados.

toodefine definido pelo usuário outputter, precisamos Olá toocreate `IOutputter` interface.

A seguir é hello base `IOutputter` implementação da classe:

```
public abstract class IOutputter : IUserDefinedOperator
{
    protected IOutputter();

    public virtual void Close();
    public abstract void Output(IRow input, IUnstructuredWriter output);
}
```

Todas as entrada parâmetros toohello outputter, como delimitadores de coluna/linha, codificação e assim por diante, precisam toobe definida no construtor de saudação da classe de saudação. Olá `IOutputter` interface também deve conter uma definição para `void Output` substituir. atributo Olá `[SqlUserDefinedOutputter(AtomicFileProcessing = true)` opcionalmente pode ser definido para o processamento de arquivos atômicas. Para obter mais informações, consulte Olá detalhes a seguir.

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

* `Output` é chamado para cada linha de entrada. Ele retorna Olá `IUnstructuredWriter output` conjunto de linhas.
* Olá classe construtor é usado ao definido pelo usuário outputter de toohello de parâmetros toopass.
* `Close`é usado toooptionally substituição do estado caro toorelease ou determinar quando a última linha de saudação foi gravada.

**SqlUserDefinedOutputter** atributo indica que o tipo de saudação deve ser registrado como um outputter definida pelo usuário. Essa classe não pode ser herdada.

SqlUserDefinedOutputter é um atributo opcional para a definição de um outputter definido pelo usuário. Ele tenha usado a propriedade de AtomicFileProcessing Olá toodefine.

* bool     AtomicFileProcessing   

* **true** = indica que esse outputter exige arquivos de saída atômicos (JSON, XML, ...)
* **false** = indica que esse outputter pode lidar com arquivos divididos/distribuídos (CSV, SEQ, ...)

objetos de programação principal Olá são **linha** e **saída**. Olá **linha** objeto é usado tooenumerate dados de saída como `IRow` interface. **Saída** é usado tooset arquivo de destino de toohello de dados de saída.

Olá dados de saída são acessados por meio de saudação `IRow` interface. Os dados de saída são passados em uma linha por vez.

valores individuais de saudação são enumerados chamando Olá Get método da interface de IRow hello:

```
row.Get<string>("column_name")
```

Os nomes de coluna individuais podem ser determinados chamando `row.Schema`:

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Essa abordagem permite que você toobuild um outputter flexível para qualquer esquema de metadados.

Olá dados de saída são gravados toofile usando `System.IO.StreamWriter`. parâmetro de fluxo de saudação está definido muito`output.BaseStrea` como parte do `IUnstructuredWriter output`.

Observe que é importante tooflush Olá dados buffer toohello arquivo depois de cada iteração de linha. Além disso, Olá `StreamWriter` objeto deve ser usado com hello descartáveis atributo habilitado (padrão) e Olá **usando** palavra-chave:

```
using (StreamWriter streamWriter = new StreamWriter(output.BaseStream, this._encoding))
{
…
}
```

Caso contrário, chame o método Flush() explicitamente depois de cada iteração. Vamos mostrar isso em Olá exemplo a seguir.

### <a name="set-headers-and-footers-for-user-defined-outputter"></a>Definir cabeçalhos e rodapés para outputter definido pelo usuário
tooset um cabeçalho, use o fluxo de execução única iteração.

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

Olá Olá código primeiro `if (isHeaderRow)` bloco é executado apenas uma vez.

Rodapé Olá, usar a instância de toohello de referência de saudação do `System.IO.Stream` objeto (`output.BaseStream`). Gravar rodapé Olá no hello método Close () do hello `IOutputter` interface.  (Para obter mais informações, consulte Olá exemplo a seguir).

Veja um exemplo de um outputter definido pelo usuário:

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

E o script base U-SQL:

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

Esse é um outputter HTML, que cria um arquivo HTML com dados da tabela.

### <a name="call-outputter-from-u-sql-base-script"></a>Chamando outputter do script base U-SQL
toocall um outputter personalizado do script U-SQL da base hello, nova instância de saudação do objeto de outputter Olá tem toobe criado.

```sql
OUTPUT @rs0 too@output_file USING new USQL_Programmability.HTMLOutputter(isHeader: true);
```

tooavoid criando uma instância de saudação do objeto no script base, podemos criar um wrapper de função, conforme mostrado no exemplo anterior:

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

Nesse caso, chamada original Olá Olá seguinte aparência:

```
OUTPUT @rs0 
too@output_file 
USING USQL_Programmability.Factory.HTMLOutputter(isHeader: true);
```

## <a name="use-user-defined-processors"></a>Usar processadores definidos pelo usuário
Processador definida pelo usuário ou UDP, é um tipo de UDO U-SQL que permite que você tooprocess linhas de entrada hello aplicando recursos de programação. UDP permite toocombine colunas, modifique os valores e adicionar novas colunas, se necessário. Basicamente, ele ajuda a tooprocess elementos de dados de tooproduce necessário um conjunto de linhas.

toodefine um UDP, precisamos toocreate um `IProcessor` interface com hello `SqlUserDefinedProcessor` atributo, que é opcional para UDP.

Esta interface deve conter a definição de saudação para Olá `IRow` substituir o conjunto de linhas de interface, conforme mostrado no exemplo a seguir de saudação:

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

**SqlUserDefinedProcessor** indica que tipo de saudação deve ser registrado como um processador definida pelo usuário. Essa classe não pode ser herdada.

Olá SqlUserDefinedProcessor atributo é **opcional** para definição de UDP.

objetos de programação principal Olá são **entrada** e **saída**. objeto de entrada Hello está tooenumerate usado colunas de entrada e saída e tooset dados de saída como resultado da atividade do processador hello.

Enumeração de colunas de entrada, usamos Olá `input.Get` método.

```
string column_name = input.Get<string>("column_name");
```

Olá parâmetro `input.Get` método é uma coluna que é passada como parte da saudação `PRODUCE` cláusula da saudação `PROCESS` instrução do script base Olá U-SQL. Precisamos toouse aqui, o tipo de dados correto do hello.

Saída, use Olá `output.Set` método.

É importante toonote que produtor personalizado gera apenas colunas e valores que são definidos com hello `output.Set` chamada de método.

```
output.Set<string>("mycolumn", mycolumn);
```

saída de processador real Hello é disparada pela chamada `return output.AsReadOnly();`.

Veja abaixo um exemplo de processador:

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

Neste cenário de caso de uso, o processador hello está gerando uma nova coluna chamada "full_description" combinando Olá colunas existentes – nesse caso, "usuário" em letras maiusculas e "des". Ele também gera um GUID e retorna Olá originais e novos valores GUID.

Como você pode ver do exemplo anterior hello, você pode chamar métodos c# durante `output.Set` chamada de método.

Abaixo temos um exemplo de script base U-SQL que usa um processador personalizado:

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

## <a name="use-user-defined-appliers"></a>Usar aplicadores definidos pelo usuário
Um aplicador de U-SQL definida pelo usuário permite que você tooinvoke personalizado c# função para cada linha que é retornada pela expressão da tabela externa saudação de uma consulta. entrada de saudação à direita é avaliada para cada linha da entrada esquerda hello e linhas de saudação que são produzidas são combinadas para saída final hello. lista de saudação de colunas que são produzidas pelo operador APPLY de saudação são a combinação de saudação de conjunto de saudação de colunas da esquerda hello e hello entrada à direita.

Aplicador definido pelo usuário está sendo invocado como parte da saudação USQL selecione expressão.

Olá típica chamada toohello definida pelo usuário aplicador de alterações é semelhante Olá a seguir:

```
SELECT …
FROM …
CROSS APPLYis used toopass parameters
new MyScript.MyApplier(param1, param2) AS alias(output_param1 string, …);
```

Para saber mais sobre como usar aplicadores na expressão SELECT., veja [U-SQL SELECT selecionando de CROSS APPLY e OUTER APPLY](https://msdn.microsoft.com/library/azure/mt621307.aspx).

definição Hello, definido pelo usuário aplicador de alterações classe base é a seguinte:

```
public abstract class IApplier : IUserDefinedOperator
{
protected IApplier();

public abstract IEnumerable<IRow> Apply(IRow input, IUpdatableRow output);
}
```

toodefine um aplicador definida pelo usuário, precisamos Olá toocreate `IApplier` interface com hello [`SqlUserDefinedApplier`] atributo, que é opcional para uma definição de aplicador de alterações definido pelo usuário.

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

* Aplicar é chamado para cada linha da tabela externa hello. Ele retorna Olá `IUpdatableRow` conjunto de linhas de saída.
* classe de construtor Olá é toopass usados parâmetros toohello definida pelo usuário aplicador.

**SqlUserDefinedApplier** indica que o tipo de saudação deve ser registrado como um aplicador definido pelo usuário. Essa classe não pode ser herdada.

O atributo **SqlUserDefinedApplier** é **opcional** para a definição do aplicador definido pelo usuário.


objetos de programação principal Olá são da seguinte maneira:

```
public override IEnumerable<IRow> Apply(IRow input, IUpdatableRow output)
```

Os conjuntos de linhas de entrada são passados como entrada `IRow`. Olá linhas de saída são geradas como `IUpdatableRow` interface de saída.

Nomes de coluna individuais podem ser determinados por chamada hello `IRow` método de esquema.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

valores de dados reais de saudação tooget de saudação entrada `IRow`, usamos o método Get () Olá `IRow` interface.

```
mycolumn = row.Get<int>("mycolumn")
```

Ou podemos usar o nome da coluna de esquema hello:

```
row.Get<int>(row.Schema[0].Name)
```

Olá valores de saída devem ser definidos com `IUpdatableRow` saída:

```
output.Set<int>("mycolumn", mycolumn)
```

É importante toounderstand que aplicadores personalizados saída somente colunas e valores que são definidos com `output.Set` chamada de método.

saída real Olá é disparada pela chamada `yield return output.AsReadOnly();`.

parâmetros aplicador de alterações da saudação definidos pelo usuário podem ser passados toohello construtor. Aplicador pode retornar um número variável de colunas que precisa toobe definida durante a chamada de saudação aplicador de alterações no Script U-SQL base.

```
new USQL_Programmability.ParserApplier ("all") AS properties(make string, model string, year string, type string, millage int);
```

Aqui está o exemplo de aplicador de alterações definido pelo usuário hello:

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

O seguinte é script U-SQL base de saudação para este aplicador definido pelo usuário:

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

Neste cenário de caso de uso, definido pelo usuário aplicador de alterações funciona como um analisador de valor separado por vírgulas para carro Olá frota propriedades. linhas do arquivo de entrada Hello aparência Olá a seguir:

```
103 Z1AB2CD123XY45889   Ford,Explorer,2005,SUV,152345
303 Y0AB2CD34XY458890   Shevrolet,Cruise,2010,4Dr,32455
210 X5AB2CD45XY458893   Nissan,Altima,2011,4Dr,74000
```

Trata-se de um típico arquivo TSV delimitado por tab com a coluna de propriedades contendo propriedades do carro, como fabricante e modelo. Essas propriedades devem ser analisado toohello colunas da tabela. aplicador de saudação que é fornecido também permite que você toogenerate dinâmica várias propriedades em Olá resultam de linhas, com base no parâmetro de saudação que é passado. Você pode gerar todas as propriedades ou somente um conjunto específico de propriedades.

    …USQL_Programmability.ParserApplier ("all")
    …USQL_Programmability.ParserApplier ("make")
    …USQL_Programmability.ParserApplier ("make&model")

aplicador de saudação definido pelo usuário pode ser chamado como uma nova instância do objeto aplicador de alterações:

```
CROSS APPLY new MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

Ou com a invocação de saudação de um método de fábrica de wrapper:

```c#
    CROSS APPLY MyNameSpace.MyApplier (parameter: “value”) AS alias([columns types]…);
```

## <a name="use-user-defined-combiners"></a>Usar combinadores definidos pelo usuário
Combinação definida pelo usuário ou UDC, permite que você toocombine linhas conjuntos de linhas à esquerda e direita, com base em lógica personalizada. O Combinador Definido pelo Usuário é usado com a expressão COMBINE.

Uma combinação está sendo invocada com a expressão de COMBINAR Olá que fornece informações necessárias de saudação sobre ambos os conjuntos de linhas de entrada hello, Olá agrupamento de colunas, hello esperado esquema de resultados e informações adicionais.

toocall uma combinação de um script U-SQL base, usamos Olá sintaxe a seguir:

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

Para saber mais, veja [Expressão COMBINE (U-SQL)](https://msdn.microsoft.com/library/azure/mt621339.aspx).

toodefine uma combinação definida pelo usuário, precisamos Olá toocreate `ICombiner` interface com hello [`SqlUserDefinedCombiner`] atributo, que é opcional para uma definição de combinação definida pelo usuário.

Definição da classe `ICombiner` base:

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

Olá implementação personalizada de um `ICombiner` interface deve conter a definição de saudação para um `IEnumerable<IRow>` combinar a substituição.

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

Olá **SqlUserDefinedCombiner** atributo indica que o tipo de saudação deve ser registrado como uma combinação definida pelo usuário. Essa classe não pode ser herdada.

**SqlUserDefinedCombiner** é propriedade de modo de combinação de saudação toodefine usado. É um atributo opcional para a definição do combinador definido pelo usuário.

Modo CombinerMode

Enumeração CombinerMode pode assumir Olá valores a seguir:

* Completo (0), que cada linha de saída depende de todas as linhas de entrada hello, da esquerda e direita com hello mesmo valor de chave.

* Esquerda (1) depende de cada linha de saída em uma única linha de entrada da esquerda da saudação (e potencialmente todas as linhas a partir de saudação à direita com hello mesmo valor de chave).

* Right (2) depende de cada linha de saída em uma única linha de entrada da saudação à direita (e potencialmente todas as linhas da esquerda Olá com hello que mesmo valor de chave).

* Interno (3) depende de cada linha de saída em uma única entrada de linha da esquerda e direita com hello mesmo valor.

Exemplo:    [`SqlUserDefinedCombiner(Mode=CombinerMode.Left)`]


objetos de programação principal Olá são:

```c#
    public override IEnumerable<IRow> Combine(IRowset left, IRowset right,
        IUpdatableRow output
```

Os conjuntos de linhas de entrada são passados como tipo `IRowset` **esquerdo** e **direito** da interface. Ambos os conjuntos de linhas precisam ser enumerados para processamento. Só é possível enumerar cada interface de uma vez, podemos ter tooenumerate e armazene em cache se necessário.

Para fins de caching, podemos criar um tipo List\<T\> de estrutura de memória como resultado de uma execução da consulta LINQ, especificamente List<`IRow`>. tipo de dados anônimos Olá pode ser usado durante a enumeração também.

Consulte [Introdução tooLINQ consultas (c#)](https://msdn.microsoft.com/library/bb397906.aspx) para obter mais informações sobre consultas LINQ e [IEnumerable\<T\> Interface](https://msdn.microsoft.com/library/9eekhta0(v=vs.110).aspx) para obter mais informações sobre o IEnumerable\<T\> interface.

valores de dados reais de saudação tooget de saudação entrada `IRowset`, usamos o método Get () Olá `IRow` interface.

```
mycolumn = row.Get<int>("mycolumn")
```

Nomes de coluna individuais podem ser determinados por chamada hello `IRow` método de esquema.

```
ISchema schema = row.Schema;
var col = schema[i];
string val = row.Get<string>(col.Name)
```

Ou usando o nome da coluna de esquema hello:

```
c# row.Get<int>(row.Schema[0].Name)
```

a enumeração geral Olá com LINQ semelhante ao seguinte hello:

```
var myRowset =
            (from row in left.Rows
                          select new
                          {
                              Mycolumn = row.Get<int>("mycolumn"),
                          }).ToList();
```

Depois de enumerar os dois conjuntos de linhas, vamos tooloop por todas as linhas. Para cada linha no conjunto de linhas à esquerda Olá, vamos toofind todas as linhas que satisfazem a condição de saudação do nosso combinação.

Olá valores de saída devem ser definidos com `IUpdatableRow` saída.

```
output.Set<int>("mycolumn", mycolumn)
```

saída real Olá é disparada pela chamada muito`yield return output.AsReadOnly();`.

Veja abaixo um exemplo do combinador:

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

Neste cenário de caso de uso, estamos criando um relatório de análise de revendedor de saudação. meta de saudação é toofind todos os produtos que custam mais de US $20.000 e que vendem através do site de hello mais rapidamente do que através de revendedor de saudação normal em um determinado intervalo de tempo.

Aqui está o script U-SQL de base de saudação. Você pode comparar a lógica de saudação entre uma junção comum e uma combinação:

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

Uma combinação definida pelo usuário pode ser chamada como uma nova instância do objeto de saudação aplicador de alterações:

```
USING new MyNameSpace.MyCombiner();
```


Ou com a invocação de saudação de um método de fábrica de wrapper:

```
USING MyNameSpace.MyCombiner();
```

## <a name="use-user-defined-reducers"></a>Usar redutores definidos pelo usuário

U-SQL permite que você toowrite reducers de conjunto de linhas personalizadas em c# usando a estrutura de extensibilidade do operador definido pelo usuário hello e implementando uma interface IReducer.

Redutor definido pelo usuário ou UDR, pode ser linhas desnecessárias tooeliminate usado durante a extração de dados (importação). Também pode ser usado toomanipulate e avaliar as linhas e colunas. Com base na lógica de programação, ele também pode definir quais linhas necessário toobe extraído.

toodefine uma classe UDR, precisamos toocreate um `IReducer` interface com um recurso opcional `SqlUserDefinedReducer` atributo.

Essa interface de classe deve conter uma definição para Olá `IEnumerable` substituir o conjunto de linhas de interface.

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

Olá **SqlUserDefinedReducer** atributo indica que o tipo de saudação deve ser registrado como um redutor definido pelo usuário. Essa classe não pode ser herdada.
**SqlUserDefinedReducer** é um atributo opcional para a definição do redutor definido pelo usuário. Ele usou toodefine IsRecursive propriedade.

* bool     IsRecursive    
* **true**  = indica se esse Redutor é idempotente

objetos de programação principal Olá são **entrada** e **saída**. objeto de entrada Hello está tooenumerate usado linhas de entrada. A saída é usada tooset linhas de saída como resultado de reduzir a atividade.

Enumeração de linhas de entrada, usamos Olá `Row.Get` método.

```
foreach (IRow row in input.Rows)
{
    row.Get<string>("mycolumn");
}
```

Olá parâmetro hello `Row.Get` método é uma coluna que é passada como parte da saudação `PRODUCE` classe de saudação `REDUCE` instrução do script base Olá U-SQL. Precisamos toouse Olá tipo de dados correto aqui também.

Saída, use Olá `output.Set` método.

É importante toounderstand que Redutor personalizado somente saídas os valores que são definidos com hello `output.Set` chamada de método.

```
output.Set<string>("mycolumn", guid);
```

saída do Hello Redutor real é disparada pela chamada `yield return output.AsReadOnly();`.

Abaixo temos um exemplo de redutor:

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

Neste cenário de caso de uso, Redutor hello está ignorando linhas com um nome de usuário vazio. Para cada linha no conjunto de linhas, lê cada coluna necessária, em seguida, avalia o comprimento de Olá Olá do nome de usuário. Ele produz real da linha hello somente se o comprimento do valor de nome de usuário é maior que 0.

Abaixo temos um script base U-SQL que usa um redutor personalizado:

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
