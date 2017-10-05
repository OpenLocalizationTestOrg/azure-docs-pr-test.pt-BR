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
# <a name="getting-started-with-json-features-in-azure-sql-database"></a>Introdução aos recursos do JSON no Banco de Dados SQL do Azure
O Banco de Dados SQL do Azure permite que você analise e consulte os dados representados no formato JavaScript Object Notation [(JSON)](http://www.json.org/) e exporte seus dados relacionais como texto JSON.

JSON é um formato de dados popular usado para a troca de dados em aplicativos Web modernos e móveis. O JSON também é usado para armazenar dados semi-estruturados em arquivos de log ou em bancos de dados NoSQL como [Banco de Dados do Azure Cosmos](https://azure.microsoft.com/services/documentdb/). Muitos serviços de Web REST retornam resultados formatados como texto JSON ou aceitam dados formatados como JSON. A maioria dos serviços do Azure como o [Azure Search](https://azure.microsoft.com/services/search/), o [Armazenamento do Azure](https://azure.microsoft.com/services/storage/) e o [Banco de dados do Azure Cosmos](https://azure.microsoft.com/services/documentdb/) tem pontos de extremidade REST que retornam ou consomem JSON.

O Banco de Dados SQL do Azure lhe permite trabalhar facilmente com dados JSON e integrar seu banco de dados com serviços modernos.

## <a name="overview"></a>Visão geral
O Banco de Dados SQL do Azure fornece as seguintes funções para trabalhar com dados JSON:

![Funções JSON](./media/sql-database-json-features/image_1.png)

Se você tiver texto JSON, pode extrair dados JSON ou verificar se o JSON está formatado corretamente usando as funções internas [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx) e [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx). A função [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) permite que você atualize o valor dentro do texto JSON. Para consultas e análises mais avançadas, a função [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) pode transformar uma matriz de objetos JSON em um conjunto de linhas. Qualquer consulta SQL pode ser executada no conjunto de resultados retornado. Finalmente, há uma cláusula [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) que lhe permite formatar os dados armazenados nas tabelas relacionais como texto JSON.

## <a name="formatting-relational-data-in-json-format"></a>Formatação de dados relacional no formato JSON
Se você tiver um serviço Web que usa dados da camada de banco de dados e fornece uma resposta no formato JSON ou bibliotecas ou estruturas JavaScript do lado do cliente que aceitam dados formatados como JSON, você pode formatar o conteúdo do banco de dados como JSON diretamente em uma consulta SQL. Você não precisa escrever o código do aplicativo que formata os resultados do Banco de Dados SQL do Azure como JSON ou incluir uma biblioteca de serialização JSON para converter os resultados de consulta de tabela e, em seguida, serializar objetos no formato JSON. Em vez disso, você pode usar a cláusula FOR JSON para formatar os resultados da consulta SQL como JSON no Banco de Dados SQL do Azure e usá-lo diretamente em seu aplicativo.

No exemplo a seguir, as linhas da tabela Sales.Customer são formatadas como JSON usando a cláusula FOR JSON:

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

A cláusula FOR JSON PATH formata os resultados da consulta como texto JSON. Nomes de coluna são usados como chaves, enquanto os valores de célula são gerados como valores JSON:

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

O conjunto de resultados é formatado como uma matriz JSON em que cada linha é formatada como um objeto JSON separado.

PATH indica que você pode personalizar o formato de saída do seu resultado JSON usando a notação de pontos de aliases de coluna. A consulta a seguir altera o nome da chave "CustomerName" no formato JSON de saída e coloca os números de telefone e fax no subobjeto "Contact":

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

A saída dessa consulta tem o seguinte aspecto:

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

Neste exemplo é retornado um único objeto JSON em vez de uma matriz, especificando a opção [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx). Você pode usar essa opção se souber que está retornando um único objeto como resultado da consulta.

O principal valor da cláusula FOR JSON é que ela permite retornar dados hierárquicos complexos de seu banco de dados formatado como matrizes ou objetos JSON aninhados. O exemplo a seguir mostra como incluir Pedidos que pertencem ao Cliente como uma matriz aninhada de Pedidos:

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

Em vez de enviar consultas separadas para obter dados do Cliente e, em seguida, para obter uma lista de Pedidos relacionados, você pode obter todos os dados necessários com uma única consulta, conforme mostrado na seguinte saída de exemplo:

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

## <a name="working-with-json-data"></a>Trabalhando com dados JSON
Se você não tiver dados estritamente estruturados, se tiver subobjetos, matrizes ou dados hierárquicos complexos ou se suas estruturas de dados evoluem ao longo do tempo, o formato JSON pode ajudá-lo a representar qualquer estrutura de dados complexos.

JSON é um formato textual que pode ser usado como qualquer outro tipo de cadeia de caracteres no Banco de Dados SQL do Azure. Você pode enviar ou armazenar dados JSON como um NVARCHAR padrão:

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

Os dados JSON usados neste exemplo são representados usando o tipo NVARCHAR(MAX). JSON pode ser inserido nessa tabela ou fornecido como um argumento de procedimento armazenado usando sintaxe Transact-SQL padrão, conforme mostrado no exemplo a seguir:

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

Qualquer linguagem ou biblioteca do lado do cliente que trabalhe com dados de cadeia de caracteres no Banco de Dados SQL do Azure também funciona com dados JSON. JSON pode ser armazenado em qualquer tabela que suporta o tipo NVARCHAR, como uma tabela com otimização de memória ou uma tabela com versão do sistema. JSON não apresenta qualquer restrição no código do lado do cliente ou na camada de banco de dados.

## <a name="querying-json-data"></a>Consultando dados JSON
Se você tiver dados formatados como JSON armazenados em tabelas SQL do Azure, as funções JSON permitem que você use esses dados em qualquer consulta SQL.

As funções JSON que estão disponíveis no Banco de Dados SQL do Azure permitem que você trate os dados formatados como JSON como qualquer outro tipo de dados do SQL. Você pode facilmente extrair valores de texto JSON e usar dados JSON em qualquer consulta:

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

A função JSON_VALUE extrai um valor de texto JSON armazenado na coluna de Dados. Essa função usa um caminho de JavaScript para fazer referência a um valor em texto JSON para extração. O valor extraído pode ser usado em qualquer parte da consulta SQL.

A função JSON_QUERY é semelhante à JSON_VALUE. Ao contrário de JSON_VALUE, essa função extrai subobjetos complexos, como matrizes ou objetos que são colocados em texto JSON.

A função JSON_MODIFY permite especificar o caminho do valor em texto JSON que deve ser atualizado, bem como um novo valor que substituirá o antigo. Dessa forma você pode atualizar facilmente o texto JSON sem ter que reanalisar toda a estrutura.

Como JSON é armazenado em um texto padrão, não há nenhuma garantia de que os valores armazenados em colunas de texto estão formatados corretamente. Você pode verificar se o texto armazenado na coluna do JSON está formatado corretamente usando restrições de verificação padrão do Banco de Dados SQL do Azure e a função ISJSON:

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

Se o texto de entrada estiver formatado corretamente como JSON, a função ISJSON retornará o valor 1. Em cada inserção ou atualização de coluna JSON, essa restrição irá verificar se o novo valor de texto não é um JSON malformado.

## <a name="transforming-json-into-tabular-format"></a>Transformando o JSON em formato tabular
O Banco de Dados SQL do Azure também permite transformar coleções de JSON em formato tabular e carregar ou consultar dados JSON.

OPENJSON é uma função com valor de tabela que analisa texto JSON, localiza uma matriz de objetos JSON, itera através dos elementos da matriz e retorna uma linha no resultado de saída para cada elemento da matriz.

![JSON tabular](./media/sql-database-json-features/image_2.png)

No exemplo acima, podemos especificar onde localizar a matriz JSON que deve ser aberta (no caminho $.Orders), quais colunas devem ser retornadas como resultado e onde encontrar os valores JSON que serão retornados como células.

Podemos transformar uma matriz JSON na variável @orders em um conjunto de linhas, analisar o conjunto de resultados ou inserir linhas em uma tabela padrão:

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
A coleção de pedidos formatada como uma matriz JSON e fornecida como um parâmetro para o procedimento armazenado pode ser analisada e inserida na tabela Pedidos.

## <a name="next-steps"></a>Próximas etapas
Para saber como integrar o JSON em seu aplicativo, consulte estes recursos:

* [Blog do TechNet](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [Documentação do MSDN](https://msdn.microsoft.com/library/dn921897.aspx)
* [Vídeo do Canal 9](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

Para saber mais sobre vários cenários para integrar o JSON em seu aplicativo, confira as demonstrações neste [vídeo do Canal 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) ou encontre um cenário que corresponda ao seu caso de uso nas [postagens no Blog do JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).

