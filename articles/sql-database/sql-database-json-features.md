---
title: Recursos JSON do Banco de Dados SQL do Azure | Microsoft Docs
description: "O Banco de Dados SQL do Azure permite que você analise, consulte e formate dados na notação JSON (JavaScript Object Notation)."
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
ms.openlocfilehash: 883e661107dd838f5c381cdef2c7f891b9a9389c
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="getting-started-with-json-features-in-azure-sql-database"></a><span data-ttu-id="f1bc4-103">Introdução aos recursos do JSON no Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="f1bc4-103">Getting started with JSON features in Azure SQL Database</span></span>
<span data-ttu-id="f1bc4-104">O Banco de Dados SQL do Azure permite que você analise e consulte os dados representados no formato JavaScript Object Notation [(JSON)](http://www.json.org/) e exporte seus dados relacionais como texto JSON.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-104">Azure SQL Database lets you parse and query data represented in JavaScript Object Notation [(JSON)](http://www.json.org/) format, and export your relational data as JSON text.</span></span>

<span data-ttu-id="f1bc4-105">JSON é um formato de dados popular usado para a troca de dados em aplicativos Web modernos e móveis.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-105">JSON is a popular data format used for exchanging data in modern web and mobile applications.</span></span> <span data-ttu-id="f1bc4-106">O JSON também é usado para armazenar dados semi-estruturados em arquivos de log ou em bancos de dados NoSQL como [Banco de Dados do Azure Cosmos](https://azure.microsoft.com/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="f1bc4-106">JSON is also used for storing semi-structured data in log files or in NoSQL databases like [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/).</span></span> <span data-ttu-id="f1bc4-107">Muitos serviços de Web REST retornam resultados formatados como texto JSON ou aceitam dados formatados como JSON.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-107">Many REST web services return results formatted as JSON text or accept data formatted as JSON.</span></span> <span data-ttu-id="f1bc4-108">A maioria dos serviços do Azure como o [Azure Search](https://azure.microsoft.com/services/search/), o [Armazenamento do Azure](https://azure.microsoft.com/services/storage/) e o [Banco de dados do Azure Cosmos](https://azure.microsoft.com/services/documentdb/) tem pontos de extremidade REST que retornam ou consomem JSON.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-108">Most Azure services such as [Azure Search](https://azure.microsoft.com/services/search/), [Azure Storage](https://azure.microsoft.com/services/storage/), and [Azure Cosmos DB](https://azure.microsoft.com/services/documentdb/) have REST endpoints that return or consume JSON.</span></span>

<span data-ttu-id="f1bc4-109">O Banco de Dados SQL do Azure lhe permite trabalhar facilmente com dados JSON e integrar seu banco de dados com serviços modernos.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-109">Azure SQL Database lets you work with JSON data easily and integrate your database with modern services.</span></span>

## <a name="overview"></a><span data-ttu-id="f1bc4-110">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f1bc4-110">Overview</span></span>
<span data-ttu-id="f1bc4-111">O Banco de Dados SQL do Azure fornece as seguintes funções para trabalhar com dados JSON:</span><span class="sxs-lookup"><span data-stu-id="f1bc4-111">Azure SQL Database provides the following functions for working with JSON data:</span></span>

![Funções JSON](./media/sql-database-json-features/image_1.png)

<span data-ttu-id="f1bc4-113">Se você tiver texto JSON, pode extrair dados JSON ou verificar se o JSON está formatado corretamente usando as funções internas [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx) e [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1bc4-113">If you have JSON text, you can extract data from JSON or verify that JSON is properly formatted by using the built-in functions [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), and [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx).</span></span> <span data-ttu-id="f1bc4-114">A função [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) permite que você atualize o valor dentro do texto JSON.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-114">The [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) function lets you update value inside JSON text.</span></span> <span data-ttu-id="f1bc4-115">Para consultas e análises mais avançadas, a função [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) pode transformar uma matriz de objetos JSON em um conjunto de linhas.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-115">For more advanced querying and analysis, [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) function can transform an array of JSON objects into a set of rows.</span></span> <span data-ttu-id="f1bc4-116">Qualquer consulta SQL pode ser executada no conjunto de resultados retornado.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-116">Any SQL query can be executed on the returned result set.</span></span> <span data-ttu-id="f1bc4-117">Finalmente, há uma cláusula [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) que lhe permite formatar os dados armazenados nas tabelas relacionais como texto JSON.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-117">Finally, there is a [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) clause that lets you format data stored in your relational tables as JSON text.</span></span>

## <a name="formatting-relational-data-in-json-format"></a><span data-ttu-id="f1bc4-118">Formatação de dados relacional no formato JSON</span><span class="sxs-lookup"><span data-stu-id="f1bc4-118">Formatting relational data in JSON format</span></span>
<span data-ttu-id="f1bc4-119">Se você tiver um serviço Web que usa dados da camada de banco de dados e fornece uma resposta no formato JSON ou bibliotecas ou estruturas JavaScript do lado do cliente que aceitam dados formatados como JSON, você pode formatar o conteúdo do banco de dados como JSON diretamente em uma consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-119">If you have a web service that takes data from the database layer and provides a response in JSON format, or client-side JavaScript frameworks or libraries that accept data formatted as JSON, you can format your database content as JSON directly in a SQL query.</span></span> <span data-ttu-id="f1bc4-120">Você não precisa escrever o código do aplicativo que formata os resultados do Banco de Dados SQL do Azure como JSON ou incluir uma biblioteca de serialização JSON para converter os resultados de consulta de tabela e, em seguida, serializar objetos no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-120">You no longer have to write application code that formats results from Azure SQL Database as JSON, or include some JSON serialization library to convert tabular query results and then serialize objects to JSON format.</span></span> <span data-ttu-id="f1bc4-121">Em vez disso, você pode usar a cláusula FOR JSON para formatar os resultados da consulta SQL como JSON no Banco de Dados SQL do Azure e usá-lo diretamente em seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-121">Instead, you can use the FOR JSON clause to format SQL query results as JSON in Azure SQL Database and use it directly in your application.</span></span>

<span data-ttu-id="f1bc4-122">No exemplo a seguir, as linhas da tabela Sales.Customer são formatadas como JSON usando a cláusula FOR JSON:</span><span class="sxs-lookup"><span data-stu-id="f1bc4-122">In the following example, rows from the Sales.Customer table are formatted as JSON by using the FOR JSON clause:</span></span>

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

<span data-ttu-id="f1bc4-123">A cláusula FOR JSON PATH formata os resultados da consulta como texto JSON.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-123">The FOR JSON PATH clause formats the results of the query as JSON text.</span></span> <span data-ttu-id="f1bc4-124">Nomes de coluna são usados como chaves, enquanto os valores de célula são gerados como valores JSON:</span><span class="sxs-lookup"><span data-stu-id="f1bc4-124">Column names are used as keys, while the cell values are generated as JSON values:</span></span>

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

<span data-ttu-id="f1bc4-125">O conjunto de resultados é formatado como uma matriz JSON em que cada linha é formatada como um objeto JSON separado.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-125">The result set is formatted as a JSON array where each row is formatted as a separate JSON object.</span></span>

<span data-ttu-id="f1bc4-126">PATH indica que você pode personalizar o formato de saída do seu resultado JSON usando a notação de pontos de aliases de coluna.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-126">PATH indicates that you can customize the output format of your JSON result by using dot notation in column aliases.</span></span> <span data-ttu-id="f1bc4-127">A consulta a seguir altera o nome da chave "CustomerName" no formato JSON de saída e coloca os números de telefone e fax no subobjeto "Contact":</span><span class="sxs-lookup"><span data-stu-id="f1bc4-127">The following query changes the name of the "CustomerName" key in the output JSON format, and puts phone and fax numbers in the "Contact" sub-object:</span></span>

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

<span data-ttu-id="f1bc4-128">A saída dessa consulta tem o seguinte aspecto:</span><span class="sxs-lookup"><span data-stu-id="f1bc4-128">The output of this query looks like this:</span></span>

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

<span data-ttu-id="f1bc4-129">Neste exemplo é retornado um único objeto JSON em vez de uma matriz, especificando a opção [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx).</span><span class="sxs-lookup"><span data-stu-id="f1bc4-129">In this example we returned a single JSON object instead of an array by specifying the [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) option.</span></span> <span data-ttu-id="f1bc4-130">Você pode usar essa opção se souber que está retornando um único objeto como resultado da consulta.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-130">You can use this option if you know that you are returning a single object as a result of query.</span></span>

<span data-ttu-id="f1bc4-131">O principal valor da cláusula FOR JSON é que ela permite retornar dados hierárquicos complexos de seu banco de dados formatado como matrizes ou objetos JSON aninhados.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-131">The main value of the FOR JSON clause is that it lets you return complex hierarchical data from your database formatted as nested JSON objects or arrays.</span></span> <span data-ttu-id="f1bc4-132">O exemplo a seguir mostra como incluir Pedidos que pertencem ao Cliente como uma matriz aninhada de Pedidos:</span><span class="sxs-lookup"><span data-stu-id="f1bc4-132">The following example shows how to include Orders that belong to the Customer as a nested array of Orders:</span></span>

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

<span data-ttu-id="f1bc4-133">Em vez de enviar consultas separadas para obter dados do Cliente e, em seguida, para obter uma lista de Pedidos relacionados, você pode obter todos os dados necessários com uma única consulta, conforme mostrado na seguinte saída de exemplo:</span><span class="sxs-lookup"><span data-stu-id="f1bc4-133">Instead of sending separate queries to get Customer data and then to fetch a list of related Orders, you can get all the necessary data with a single query, as shown in the following sample output:</span></span>

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

## <a name="working-with-json-data"></a><span data-ttu-id="f1bc4-134">Trabalhando com dados JSON</span><span class="sxs-lookup"><span data-stu-id="f1bc4-134">Working with JSON data</span></span>
<span data-ttu-id="f1bc4-135">Se você não tiver dados estritamente estruturados, se tiver subobjetos, matrizes ou dados hierárquicos complexos ou se suas estruturas de dados evoluem ao longo do tempo, o formato JSON pode ajudá-lo a representar qualquer estrutura de dados complexos.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-135">If you don’t have strictly structured data, if you have complex sub-objects, arrays, or hierarchical data, or if your data structures evolve over time, the JSON format can help you to represent any complex data structure.</span></span>

<span data-ttu-id="f1bc4-136">JSON é um formato textual que pode ser usado como qualquer outro tipo de cadeia de caracteres no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-136">JSON is a textual format that can be used like any other string type in Azure SQL Database.</span></span> <span data-ttu-id="f1bc4-137">Você pode enviar ou armazenar dados JSON como um NVARCHAR padrão:</span><span class="sxs-lookup"><span data-stu-id="f1bc4-137">You can send or store JSON data as a standard NVARCHAR:</span></span>

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

<span data-ttu-id="f1bc4-138">Os dados JSON usados neste exemplo são representados usando o tipo NVARCHAR(MAX).</span><span class="sxs-lookup"><span data-stu-id="f1bc4-138">The JSON data used in this example is represented by using the NVARCHAR(MAX) type.</span></span> <span data-ttu-id="f1bc4-139">JSON pode ser inserido nessa tabela ou fornecido como um argumento de procedimento armazenado usando sintaxe Transact-SQL padrão, conforme mostrado no exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="f1bc4-139">JSON can be inserted into this table or provided as an argument of the stored procedure using standard Transact-SQL syntax as shown in the following example:</span></span>

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

<span data-ttu-id="f1bc4-140">Qualquer linguagem ou biblioteca do lado do cliente que trabalhe com dados de cadeia de caracteres no Banco de Dados SQL do Azure também funciona com dados JSON.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-140">Any client-side language or library that works with string data in Azure SQL Database will also work with JSON data.</span></span> <span data-ttu-id="f1bc4-141">JSON pode ser armazenado em qualquer tabela que suporta o tipo NVARCHAR, como uma tabela com otimização de memória ou uma tabela com versão do sistema.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-141">JSON can be stored in any table that supports the NVARCHAR type, such as a Memory-optimized table or a System-versioned table.</span></span> <span data-ttu-id="f1bc4-142">JSON não apresenta qualquer restrição no código do lado do cliente ou na camada de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-142">JSON does not introduce any constraint either in the client-side code or in the database layer.</span></span>

## <a name="querying-json-data"></a><span data-ttu-id="f1bc4-143">Consultando dados JSON</span><span class="sxs-lookup"><span data-stu-id="f1bc4-143">Querying JSON data</span></span>
<span data-ttu-id="f1bc4-144">Se você tiver dados formatados como JSON armazenados em tabelas SQL do Azure, as funções JSON permitem que você use esses dados em qualquer consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-144">If you have data formatted as JSON stored in Azure SQL tables, JSON functions let you use this data in any SQL query.</span></span>

<span data-ttu-id="f1bc4-145">As funções JSON que estão disponíveis no Banco de Dados SQL do Azure permitem que você trate os dados formatados como JSON como qualquer outro tipo de dados do SQL.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-145">JSON functions that are available in Azure SQL database let you treat data formatted as JSON as any other SQL data type.</span></span> <span data-ttu-id="f1bc4-146">Você pode facilmente extrair valores de texto JSON e usar dados JSON em qualquer consulta:</span><span class="sxs-lookup"><span data-stu-id="f1bc4-146">You can easily extract values from the JSON text, and use JSON data in any query:</span></span>

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

<span data-ttu-id="f1bc4-147">A função JSON_VALUE extrai um valor de texto JSON armazenado na coluna de Dados.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-147">The JSON_VALUE function extracts a value from JSON text stored in the Data column.</span></span> <span data-ttu-id="f1bc4-148">Essa função usa um caminho de JavaScript para fazer referência a um valor em texto JSON para extração.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-148">This function uses a JavaScript-like path to reference a value in JSON text to extract.</span></span> <span data-ttu-id="f1bc4-149">O valor extraído pode ser usado em qualquer parte da consulta SQL.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-149">The extracted value can be used in any part of SQL query.</span></span>

<span data-ttu-id="f1bc4-150">A função JSON_QUERY é semelhante à JSON_VALUE.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-150">The JSON_QUERY function is similar to JSON_VALUE.</span></span> <span data-ttu-id="f1bc4-151">Ao contrário de JSON_VALUE, essa função extrai subobjetos complexos, como matrizes ou objetos que são colocados em texto JSON.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-151">Unlike JSON_VALUE, this function extracts complex sub-object such as arrays or objects that are placed in JSON text.</span></span>

<span data-ttu-id="f1bc4-152">A função JSON_MODIFY permite especificar o caminho do valor em texto JSON que deve ser atualizado, bem como um novo valor que substituirá o antigo.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-152">The JSON_MODIFY function lets you specify the path of the value in the JSON text that should be updated, as well as a new value that will overwrite the old one.</span></span> <span data-ttu-id="f1bc4-153">Dessa forma você pode atualizar facilmente o texto JSON sem ter que reanalisar toda a estrutura.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-153">This way you can easily update JSON text without reparsing the entire structure.</span></span>

<span data-ttu-id="f1bc4-154">Como JSON é armazenado em um texto padrão, não há nenhuma garantia de que os valores armazenados em colunas de texto estão formatados corretamente.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-154">Since JSON is stored in a standard text, there are no guarantees that the values stored in text columns are properly formatted.</span></span> <span data-ttu-id="f1bc4-155">Você pode verificar se o texto armazenado na coluna do JSON está formatado corretamente usando restrições de verificação padrão do Banco de Dados SQL do Azure e a função ISJSON:</span><span class="sxs-lookup"><span data-stu-id="f1bc4-155">You can verify that text stored in JSON column is properly formatted by using standard Azure SQL Database check constraints and the ISJSON function:</span></span>

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

<span data-ttu-id="f1bc4-156">Se o texto de entrada estiver formatado corretamente como JSON, a função ISJSON retornará o valor 1.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-156">If the input text is properly formatted JSON, the ISJSON function returns the value 1.</span></span> <span data-ttu-id="f1bc4-157">Em cada inserção ou atualização de coluna JSON, essa restrição irá verificar se o novo valor de texto não é um JSON malformado.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-157">On every insert or update of JSON column, this constraint will verify that new text value is not malformed JSON.</span></span>

## <a name="transforming-json-into-tabular-format"></a><span data-ttu-id="f1bc4-158">Transformando o JSON em formato tabular</span><span class="sxs-lookup"><span data-stu-id="f1bc4-158">Transforming JSON into tabular format</span></span>
<span data-ttu-id="f1bc4-159">O Banco de Dados SQL do Azure também permite transformar coleções de JSON em formato tabular e carregar ou consultar dados JSON.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-159">Azure SQL Database also lets you transform JSON collections into tabular format and load or query JSON data.</span></span>

<span data-ttu-id="f1bc4-160">OPENJSON é uma função com valor de tabela que analisa texto JSON, localiza uma matriz de objetos JSON, itera através dos elementos da matriz e retorna uma linha no resultado de saída para cada elemento da matriz.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-160">OPENJSON is a table-value function that parses JSON text, locates an array of JSON objects, iterates through the elements of the array, and returns one row in the output result for each element of the array.</span></span>

![JSON tabular](./media/sql-database-json-features/image_2.png)

<span data-ttu-id="f1bc4-162">No exemplo acima, podemos especificar onde localizar a matriz JSON que deve ser aberta (no caminho $.Orders), quais colunas devem ser retornadas como resultado e onde encontrar os valores JSON que serão retornados como células.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-162">In the example above, we can specify where to locate the JSON array that should be opened (in the $.Orders path), what columns should be returned as result, and where to find the JSON values that will be returned as cells.</span></span>

<span data-ttu-id="f1bc4-163">Podemos transformar uma matriz JSON na variável @orders em um conjunto de linhas, analisar o conjunto de resultados ou inserir linhas em uma tabela padrão:</span><span class="sxs-lookup"><span data-stu-id="f1bc4-163">We can transform a JSON array in the @orders variable into a set of rows, analyze this result set, or insert rows into a standard table:</span></span>

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
<span data-ttu-id="f1bc4-164">A coleção de pedidos formatada como uma matriz JSON e fornecida como um parâmetro para o procedimento armazenado pode ser analisada e inserida na tabela Pedidos.</span><span class="sxs-lookup"><span data-stu-id="f1bc4-164">The collection of orders formatted as a JSON array and provided as a parameter to the stored procedure can be parsed and inserted into the Orders table.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1bc4-165">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f1bc4-165">Next steps</span></span>
<span data-ttu-id="f1bc4-166">Para saber como integrar o JSON em seu aplicativo, consulte estes recursos:</span><span class="sxs-lookup"><span data-stu-id="f1bc4-166">To learn how to integrate JSON into your application, check out these resources:</span></span>

* [<span data-ttu-id="f1bc4-167">Blog do TechNet</span><span class="sxs-lookup"><span data-stu-id="f1bc4-167">TechNet Blog</span></span>](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [<span data-ttu-id="f1bc4-168">Documentação do MSDN</span><span class="sxs-lookup"><span data-stu-id="f1bc4-168">MSDN documentation</span></span>](https://msdn.microsoft.com/library/dn921897.aspx)
* [<span data-ttu-id="f1bc4-169">Vídeo do Canal 9</span><span class="sxs-lookup"><span data-stu-id="f1bc4-169">Channel 9 video</span></span>](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

<span data-ttu-id="f1bc4-170">Para saber mais sobre vários cenários para integrar o JSON em seu aplicativo, confira as demonstrações neste [vídeo do Canal 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) ou encontre um cenário que corresponda ao seu caso de uso nas [postagens no Blog do JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span><span class="sxs-lookup"><span data-stu-id="f1bc4-170">To learn about various scenarios for integrating JSON into your application, see the demos in this [Channel 9 video](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) or find a scenario that matches your use case in [JSON Blog posts](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).</span></span>

