---
title: recursos de JSON de banco de dados SQL aaaAzure | Microsoft Docs
description: "Banco de dados SQL do Azure permite que você tooparse, consulta e formatar dados na notação de notação JSON (JavaScript Object)."
services: sql-database
documentationcenter: 
author: jovanpop-msft
manager: jhubbard
editor: 
ms.assetid: 55860105-2f5f-4b10-87a0-99faa32b5653
ms.service: sql-database
ms.custom: develop databases
ms.devlang: NA
ms.date: 11/15/2016
ms.author: jovanpop
ms.workload: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.openlocfilehash: 30a31a1b01482ec276646b6fd6ca0c1f581168d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="458af-103">Introdução aos recursos do JSON no Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="458af-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="458af-104">O Banco de Dados SQL do Azure permite que você analise e consulte os dados representados no formato JavaScript Object Notation [(JSON)](http://www.json.org/) e exporte seus dados relacionais como texto JSON.</span><span class="sxs-lookup"><span data-stu-id="458af-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="458af-105">JSON é um formato de dados popular usado para a troca de dados em aplicativos Web modernos e móveis.</span><span class="sxs-lookup"><span data-stu-id="458af-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="458af-106">O JSON também é usado para armazenar dados semi-estruturados em arquivos de log ou em bancos de dados NoSQL como [Banco de Dados do Azure Cosmos](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="458af-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="458af-107">Muitos serviços de Web REST retornam resultados formatados como texto JSON ou aceitam dados formatados como JSON.</span><span class="sxs-lookup"><span data-stu-id="458af-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="458af-108">A maioria dos serviços do Azure como o [Azure Search](https://azure.microsoft.com/services/search/), o [Armazenamento do Azure](https://azure.microsoft.com/services/storage/) e o [Banco de dados do Azure Cosmos](https://azure.microsoft.com/services/documentdb/) tem pontos de extremidade REST que retornam ou consomem JSON.</span><span class="sxs-lookup"><span data-stu-id="458af-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="458af-109">O Banco de Dados SQL do Azure lhe permite trabalhar facilmente com dados JSON e integrar seu banco de dados com serviços modernos.</span><span class="sxs-lookup"><span data-stu-id="458af-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="458af-110">Visão geral</span><span class="sxs-lookup"><span data-stu-id="458af-110">Overview</span></span>
<span data-ttu-id="458af-111">Banco de dados SQL do Azure fornece Olá funções para trabalhar com dados JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="458af-111">Azure SQL Database provides hello following functions for working with JSON data:</span></span>

![Funções JSON](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="458af-113">Se você tiver texto JSON, você pode extrair dados de JSON ou verificar se JSON está formatado corretamente usando funções internas Olá [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), e [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) .</span><span class="sxs-lookup"><span data-stu-id="458af-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using hello built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="458af-114">Olá [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) função permite que você atualize o valor dentro do texto JSON.</span><span class="sxs-lookup"><span data-stu-id="458af-114">hello [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="458af-115">Para consultas e análises mais avançadas, a função [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) pode transformar uma matriz de objetos JSON em um conjunto de linhas.</span><span class="sxs-lookup"><span data-stu-id="458af-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="458af-116">Qualquer consulta SQL pode ser executada em Olá retornada um conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="458af-116">Any SQL query can be executed on hello returned result set.</span></span> <span data-ttu-id="458af-117">Finalmente, há uma cláusula [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) que lhe permite formatar os dados armazenados nas tabelas relacionais como texto JSON.</span><span class="sxs-lookup"><span data-stu-id="458af-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="458af-118">Formatação de dados relacional no formato JSON</span><span class="sxs-lookup"><span data-stu-id="458af-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="458af-119">Se você tiver um serviço web que usa dados do banco de dados de saudação de camada e fornece uma resposta em JSON formatar ou cliente estruturas ou bibliotecas JavaScript que aceitam dados formatados como JSON, você pode formatar o conteúdo do banco de dados como JSON diretamente em uma consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="458af-119">If you have a web service that takes data from hello database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="458af-120">Você não tiver um código de aplicativo de toowrite que formata os resultados do banco de dados do SQL Azure como JSON, ou incluem alguns resultados de consulta de tabela do JSON serialização biblioteca tooconvert e, em seguida, serializar o formato de tooJSON de objetos.</span><span class="sxs-lookup"><span data-stu-id="458af-120">You no longer have toowrite application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library tooconvert tabular query results and then serialize objects tooJSON format.</span></span> <span data-ttu-id="458af-121">Em vez disso, você pode usar o hello JSON cláusula tooformat SQL dos resultados da consulta como JSON no SQL Azure e usá-lo diretamente no seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="458af-121">Instead, you can use hello FOR JSON clause tooformat SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="458af-122">No hello exemplo a seguir, linhas da tabela Sales. Customer de saudação são formatadas como JSON usando Olá cláusula FOR JSON:</span><span class="sxs-lookup"><span data-stu-id="458af-122">In hello following example, rows from hello Sales.Customer table are formatted as JSON by using hello FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="458af-123">cláusula FOR JSON PATH de saudação formata os resultados de saudação de consulta de saudação como texto JSON.</span><span class="sxs-lookup"><span data-stu-id="458af-123">hello FOR JSON PATH clause formats hello results of hello query as JSON text.</span></span> <span data-ttu-id="458af-124">Nomes de coluna são usados como chaves, enquanto os valores de célula Olá são gerados como valores JSON:</span><span class="sxs-lookup"><span data-stu-id="458af-124">Column names are used as keys, while hello cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="458af-125">conjunto de resultados de saudação é formatado como uma matriz JSON onde cada linha é formatada como um objeto JSON separado.</span><span class="sxs-lookup"><span data-stu-id="458af-125">hello result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="458af-126">CAMINHO indica que você pode personalizar o formato de saída de saudação do seu resultado JSON usando a notação de aliases de coluna.</span><span class="sxs-lookup"><span data-stu-id="458af-126">PATH indicates that you can customize hello output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="458af-127">Olá consulta a seguir altera Olá nome da chave de "CustomerName" hello em formato de JSON de saída de hello e coloca os números de telefone e fax na subobjeto hello "Contato":</span><span class="sxs-lookup"><span data-stu-id="458af-127">hello following query changes hello name of hello "CustomerName" key in hello output JSON format, and puts phone and fax numbers in hello "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="458af-128">saída de Hello dessa consulta tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="458af-128">hello output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="458af-129">Neste exemplo, é retornado um único objeto JSON em vez de uma matriz especificando Olá [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) opção.</span><span class="sxs-lookup"><span data-stu-id="458af-129">In this example we returned a single JSON object instead of an array by specifying hello [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="458af-130">Você pode usar essa opção se souber que está retornando um único objeto como resultado da consulta.</span><span class="sxs-lookup"><span data-stu-id="458af-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="458af-131">valor principal Olá Olá cláusula FOR JSON é que ela permite retornar dados hierárquicos complexos de seu banco de dados formatado como objetos JSON aninhados ou matrizes.</span><span class="sxs-lookup"><span data-stu-id="458af-131">hello main value of hello FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="458af-132">saudação de exemplo mostra como tooinclude pedidos que pertencem a toohello cliente como uma matriz aninhada de pedidos a seguir:</span><span class="sxs-lookup"><span data-stu-id="458af-132">hello following example shows how tooinclude Orders that belong toohello Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="458af-133">Em vez de enviar os dados do cliente tooget consultas separadas e, em seguida, toofetch uma lista de pedidos relacionadas, você pode obter todos os dados necessários de saudação com uma única consulta, conforme mostrado no hello saída de exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="458af-133">Instead of sending separate queries tooget Customer data and then toofetch a list of related Orders, you can get all hello necessary data with a single query, as shown in hello following sample output:</span></span>

```
{
  "Name":"Nada Jovanovic",
  "Phone":"(215) 555-0100",
  "Fax":"(215) 555-0101",
  "Orders":[
    {"OrderID":382,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":395,"OrderDate":"2013-01-07","ExpectedDeliveryDate":"2013-01-08"},
    {"OrderID":1657,"OrderDate":"2013-01-31","ExpectedDeliveryDate":"2013-02-01"}
]
}
```

## <a name="working-with-json-data"></a><span data-ttu-id="458af-134">Trabalhando com dados JSON</span><span class="sxs-lookup"><span data-stu-id="458af-134">Working with JSON data</span></span>
<span data-ttu-id="458af-135">Se você não tem dados estruturados estritamente, se você tiver subobjetos complexas, matrizes ou dados hierárquicos, ou se suas estruturas de dados evoluem ao longo do tempo, formato JSON de saudação pode ajudá-lo toorepresent qualquer estrutura de dados complexos.</span><span class="sxs-lookup"><span data-stu-id="458af-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, hello JSON format can help you toorepresent any complex data structure.</span></span>

<span data-ttu-id="458af-136">JSON é um formato textual que pode ser usado como qualquer outro tipo de cadeia de caracteres no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="458af-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="458af-137">Você pode enviar ou armazenar dados JSON como um NVARCHAR padrão:</span><span class="sxs-lookup"><span data-stu-id="458af-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

```
CREATE TABLE Products (
  Id int identity primary key,
  Title nvarchar(200),
  Data nvarchar(max)
)
go
CREATE PROCEDURE InsertProduct(@title nvarchar(200), @json nvarchar(max))
AS BEGIN
    insert into Products(Title, Data)
    values(@title, @json)
END
```

<span data-ttu-id="458af-138">Olá dados JSON usados neste exemplo é representada usando o tipo do hello nvarchar (max).</span><span class="sxs-lookup"><span data-stu-id="458af-138">hello JSON data used in this example is represented by using hello NVARCHAR(MAX) type.</span></span> <span data-ttu-id="458af-139">JSON pode ser inserido nessa tabela ou fornecido como um argumento de procedimento Olá armazenado usando sintaxe de Transact-SQL padrão, conforme mostrado no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="458af-139">JSON can be inserted into this table or provided as an argument of hello stored procedure using standard Transact-SQL syntax as shown in hello following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="458af-140">Qualquer linguagem ou biblioteca do lado do cliente que trabalhe com dados de cadeia de caracteres no Banco de Dados SQL do Azure também funciona com dados JSON.</span><span class="sxs-lookup"><span data-stu-id="458af-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="458af-141">JSON pode ser armazenado em qualquer tabela que dá suporte ao tipo NVARCHAR hello, como uma tabela com otimização de memória ou uma tabela com versão do sistema.</span><span class="sxs-lookup"><span data-stu-id="458af-141">JSON can be stored in any table that supports hello NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="458af-142">JSON não introduz nenhuma restrição no código do lado do cliente hello ou na camada de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="458af-142">JSON does not introduce any constraint either in hello client-side code or in hello database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="458af-143">Consultando dados JSON</span><span class="sxs-lookup"><span data-stu-id="458af-143">Querying JSON data</span></span>
<span data-ttu-id="458af-144">Se você tiver dados formatados como JSON armazenados em tabelas SQL do Azure, as funções JSON permitem que você use esses dados em qualquer consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="458af-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="458af-145">As funções JSON que estão disponíveis no Banco de Dados SQL do Azure permitem que você trate os dados formatados como JSON como qualquer outro tipo de dados do SQL.</span><span class="sxs-lookup"><span data-stu-id="458af-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="458af-146">Você pode facilmente extrair valores de saudação texto JSON e usam dados JSON em qualquer consulta:</span><span class="sxs-lookup"><span data-stu-id="458af-146">You can easily extract values from hello JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="458af-147">Olá função JSON_VALUE extrai um valor de texto JSON armazenado na coluna de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="458af-147">hello JSON_VALUE function extracts a value from JSON text stored in hello Data column.</span></span> <span data-ttu-id="458af-148">Essa função usa tooreference um caminho de JavaScript como um valor em tooextract de texto JSON.</span><span class="sxs-lookup"><span data-stu-id="458af-148">This function uses a JavaScript-like path tooreference a value in JSON text tooextract.</span></span> <span data-ttu-id="458af-149">valor de saudação extraída pode ser usado em qualquer parte da consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="458af-149">hello extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="458af-150">Olá função JSON_QUERY é tooJSON_VALUE semelhante.</span><span class="sxs-lookup"><span data-stu-id="458af-150">hello JSON_QUERY function is similar tooJSON_VALUE.</span></span> <span data-ttu-id="458af-151">Ao contrário de JSON_VALUE, essa função extrai subobjetos complexos, como matrizes ou objetos que são colocados em texto JSON.</span><span class="sxs-lookup"><span data-stu-id="458af-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="458af-152">função JSON_MODIFY de saudação permite especificar o caminho de saudação do valor de saudação em texto JSON Olá que deve ser atualizado, bem como um novo valor que substituirá Olá antigo.</span><span class="sxs-lookup"><span data-stu-id="458af-152">hello JSON_MODIFY function lets you specify hello path of hello value in hello JSON text that should be updated, as well as a new value that will overwrite hello old one.</span></span> <span data-ttu-id="458af-153">Dessa forma, que você pode atualizar facilmente texto JSON sem analisando a estrutura inteira hello.</span><span class="sxs-lookup"><span data-stu-id="458af-153">This way you can easily update JSON text without reparsing hello entire structure.</span></span>

<span data-ttu-id="458af-154">Como JSON é armazenado em um padrão de texto, não há nenhuma garantia que valores hello armazenados em colunas de texto estão formatados corretamente.</span><span class="sxs-lookup"><span data-stu-id="458af-154">Since JSON is stored in a standard text, there are no guarantees that hello values stored in text columns are properly formatted.</span></span> <span data-ttu-id="458af-155">Você pode verificar se o texto armazenado na coluna JSON está formatado corretamente usando o padrão de restrições de verificação de banco de dados SQL e hello função ISJSON:</span><span class="sxs-lookup"><span data-stu-id="458af-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and hello ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="458af-156">Se o texto de entrada hello está corretamente formatado JSON, Olá função ISJSON retorna o valor de saudação 1.</span><span class="sxs-lookup"><span data-stu-id="458af-156">If hello input text is properly formatted JSON, hello ISJSON function returns hello value 1.</span></span> <span data-ttu-id="458af-157">Em cada inserção ou atualização de coluna JSON, essa restrição irá verificar se o novo valor de texto não é um JSON malformado.</span><span class="sxs-lookup"><span data-stu-id="458af-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="458af-158">Transformando o JSON em formato tabular</span><span class="sxs-lookup"><span data-stu-id="458af-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="458af-159">O Banco de Dados SQL do Azure também permite transformar coleções de JSON em formato tabular e carregar ou consultar dados JSON.</span><span class="sxs-lookup"><span data-stu-id="458af-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="458af-160">OPENJSON é uma função com valor de tabela que analisa texto JSON, localiza uma matriz de objetos JSON, itera por meio de elementos de saudação da matriz de saudação e retorna uma linha no resultado Olá para cada elemento da matriz de saudação.</span><span class="sxs-lookup"><span data-stu-id="458af-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through hello elements of hello array, and returns one row in hello output result for each element of hello array.</span></span>

![JSON tabular](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="458af-162">O exemplo hello acima, podemos especificar onde toolocate Olá matriz JSON que deve ser aberto (em $ Oi. Caminho de pedidos), a quais colunas devem ser retornadas como resultado, e onde toofind Olá valores JSON que serão retornados como células.</span><span class="sxs-lookup"><span data-stu-id="458af-162">In hello example above, we can specify where toolocate hello JSON array that should be opened (in hello $.Orders path), what columns should be returned as result, and where toofind hello JSON values that will be returned as cells.</span></span>

<span data-ttu-id="458af-163">É possível transformar uma matriz JSON em Olá @orders variável em um conjunto de linhas, analisar esse conjunto de resultados, ou inserir linhas em uma tabela padrão:</span><span class="sxs-lookup"><span data-stu-id="458af-163">We can transform a JSON array in hello @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

```
CREATE PROCEDURE InsertOrders(@orders nvarchar(max))
AS BEGIN

    insert into Orders(Number, Date, Customer, Quantity)
    select Number, Date, Customer, Quantity
    OPENJSON (@orders)
     WITH (
            Number varchar(200),
            Date datetime,
            Customer varchar(200),
            Quantity int
     )

END
```
<span data-ttu-id="458af-164">coleção de saudação de pedidos formatada como uma matriz JSON e fornecido como um procedimento armazenado de toohello de parâmetro pode ser analisado e inserido na tabela de pedidos de saudação.</span><span class="sxs-lookup"><span data-stu-id="458af-164">hello collection of orders formatted as a JSON array and provided as a parameter toohello stored procedure can be parsed and inserted into hello Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="458af-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="458af-165">Next steps</span></span>
<span data-ttu-id="458af-166">toolearn como toointegrate JSON em seu aplicativo, confira esses recursos:</span><span class="sxs-lookup"><span data-stu-id="458af-166">toolearn how toointegrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="458af-167">Blog do TechNet</span><span class="sxs-lookup"><span data-stu-id="458af-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="458af-168">Documentação do MSDN</span><span class="sxs-lookup"><span data-stu-id="458af-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="458af-169">Vídeo do Canal 9</span><span class="sxs-lookup"><span data-stu-id="458af-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="458af-170">toolearn sobre os vários cenários para integrar o JSON em seu aplicativo, consulte demonstrações Olá neste [vídeo do Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) ou encontrar um cenário que corresponde a seu caso de uso em [postagens no Blog do JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span><span class="sxs-lookup"><span data-stu-id="458af-170">toolearn about various scenarios for integrating JSON into your application, see hello demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

