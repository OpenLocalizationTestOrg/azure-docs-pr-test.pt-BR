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
# <a name="getting-started-with-json-features-in-azure-sql-database"></a>Introdução aos recursos do JSON no Banco de Dados SQL do Azure
O Banco de Dados SQL do Azure permite que você analise e consulte os dados representados no formato JavaScript Object Notation [(JSON)](http://www.json.org/) e exporte seus dados relacionais como texto JSON.

JSON é um formato de dados popular usado para a troca de dados em aplicativos Web modernos e móveis. O JSON também é usado para armazenar dados semi-estruturados em arquivos de log ou em bancos de dados NoSQL como [Banco de Dados do Azure Cosmos](https://azure.microsoft.com/services/documentdb/). Muitos serviços de Web REST retornam resultados formatados como texto JSON ou aceitam dados formatados como JSON. A maioria dos serviços do Azure como o [Azure Search](https://azure.microsoft.com/services/search/), o [Armazenamento do Azure](https://azure.microsoft.com/services/storage/) e o [Banco de dados do Azure Cosmos](https://azure.microsoft.com/services/documentdb/) tem pontos de extremidade REST que retornam ou consomem JSON.

O Banco de Dados SQL do Azure lhe permite trabalhar facilmente com dados JSON e integrar seu banco de dados com serviços modernos.

## <a name="overview"></a>Visão geral
Banco de dados SQL do Azure fornece Olá funções para trabalhar com dados JSON a seguir:

![Funções JSON](./media/sql-database-json-features/image_1.png)

Se você tiver texto JSON, você pode extrair dados de JSON ou verificar se JSON está formatado corretamente usando funções internas Olá [JSON_VALUE](https://msdn.microsoft.com/library/dn921898.aspx), [JSON_QUERY](https://msdn.microsoft.com/library/dn921884.aspx), e [ISJSON](https://msdn.microsoft.com/library/dn921896.aspx) . Olá [JSON_MODIFY](https://msdn.microsoft.com/library/dn921892.aspx) função permite que você atualize o valor dentro do texto JSON. Para consultas e análises mais avançadas, a função [OPENJSON](https://msdn.microsoft.com/library/dn921885.aspx) pode transformar uma matriz de objetos JSON em um conjunto de linhas. Qualquer consulta SQL pode ser executada em Olá retornada um conjunto de resultados. Finalmente, há uma cláusula [FOR JSON](https://msdn.microsoft.com/library/dn921882.aspx) que lhe permite formatar os dados armazenados nas tabelas relacionais como texto JSON.

## <a name="formatting-relational-data-in-json-format"></a>Formatação de dados relacional no formato JSON
Se você tiver um serviço web que usa dados do banco de dados de saudação de camada e fornece uma resposta em JSON formatar ou cliente estruturas ou bibliotecas JavaScript que aceitam dados formatados como JSON, você pode formatar o conteúdo do banco de dados como JSON diretamente em uma consulta SQL. Você não tiver um código de aplicativo de toowrite que formata os resultados do banco de dados do SQL Azure como JSON, ou incluem alguns resultados de consulta de tabela do JSON serialização biblioteca tooconvert e, em seguida, serializar o formato de tooJSON de objetos. Em vez disso, você pode usar o hello JSON cláusula tooformat SQL dos resultados da consulta como JSON no SQL Azure e usá-lo diretamente no seu aplicativo.

No hello exemplo a seguir, linhas da tabela Sales. Customer de saudação são formatadas como JSON usando Olá cláusula FOR JSON:

```
select CustomerName, PhoneNumber, FaxNumber
from Sales.Customers
FOR JSON PATH
```

cláusula FOR JSON PATH de saudação formata os resultados de saudação de consulta de saudação como texto JSON. Nomes de coluna são usados como chaves, enquanto os valores de célula Olá são gerados como valores JSON:

```
[
{"CustomerName":"Eric Torres","PhoneNumber":"(307) 555-0100","FaxNumber":"(307) 555-0101"},
{"CustomerName":"Cosmina Vlad","PhoneNumber":"(505) 555-0100","FaxNumber":"(505) 555-0101"},
{"CustomerName":"Bala Dixit","PhoneNumber":"(209) 555-0100","FaxNumber":"(209) 555-0101"}
]
```

conjunto de resultados de saudação é formatado como uma matriz JSON onde cada linha é formatada como um objeto JSON separado.

CAMINHO indica que você pode personalizar o formato de saída de saudação do seu resultado JSON usando a notação de aliases de coluna. Olá consulta a seguir altera Olá nome da chave de "CustomerName" hello em formato de JSON de saída de hello e coloca os números de telefone e fax na subobjeto hello "Contato":

```
select CustomerName as Name, PhoneNumber as [Contact.Phone], FaxNumber as [Contact.Fax]
from Sales.Customers
where CustomerID = 931
FOR JSON PATH, WITHOUT_ARRAY_WRAPPER
```

saída de Hello dessa consulta tem esta aparência:

```
{
    "Name":"Nada Jovanovic",
    "Contact":{
           "Phone":"(215) 555-0100",
           "Fax":"(215) 555-0101"
    }
}
```

Neste exemplo, é retornado um único objeto JSON em vez de uma matriz especificando Olá [WITHOUT_ARRAY_WRAPPER](https://msdn.microsoft.com/library/mt631354.aspx) opção. Você pode usar essa opção se souber que está retornando um único objeto como resultado da consulta.

valor principal Olá Olá cláusula FOR JSON é que ela permite retornar dados hierárquicos complexos de seu banco de dados formatado como objetos JSON aninhados ou matrizes. saudação de exemplo mostra como tooinclude pedidos que pertencem a toohello cliente como uma matriz aninhada de pedidos a seguir:

```
select CustomerName as Name, PhoneNumber as Phone, FaxNumber as Fax,
        Orders.OrderID, Orders.OrderDate, Orders.ExpectedDeliveryDate
from Sales.Customers Customer
    join Sales.Orders Orders
        on Customer.CustomerID = Orders.CustomerID
where Customer.CustomerID = 931
FOR JSON AUTO, WITHOUT_ARRAY_WRAPPER

```

Em vez de enviar os dados do cliente tooget consultas separadas e, em seguida, toofetch uma lista de pedidos relacionadas, você pode obter todos os dados necessários de saudação com uma única consulta, conforme mostrado no hello saída de exemplo a seguir:

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
Se você não tem dados estruturados estritamente, se você tiver subobjetos complexas, matrizes ou dados hierárquicos, ou se suas estruturas de dados evoluem ao longo do tempo, formato JSON de saudação pode ajudá-lo toorepresent qualquer estrutura de dados complexos.

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

Olá dados JSON usados neste exemplo é representada usando o tipo do hello nvarchar (max). JSON pode ser inserido nessa tabela ou fornecido como um argumento de procedimento Olá armazenado usando sintaxe de Transact-SQL padrão, conforme mostrado no exemplo a seguir de saudação:

```
EXEC InsertProduct 'Toy car', '{"Price":50,"Color":"White","tags":["toy","children","games"]}'
```

Qualquer linguagem ou biblioteca do lado do cliente que trabalhe com dados de cadeia de caracteres no Banco de Dados SQL do Azure também funciona com dados JSON. JSON pode ser armazenado em qualquer tabela que dá suporte ao tipo NVARCHAR hello, como uma tabela com otimização de memória ou uma tabela com versão do sistema. JSON não introduz nenhuma restrição no código do lado do cliente hello ou na camada de banco de dados de saudação.

## <a name="querying-json-data"></a>Consultando dados JSON
Se você tiver dados formatados como JSON armazenados em tabelas SQL do Azure, as funções JSON permitem que você use esses dados em qualquer consulta SQL.

As funções JSON que estão disponíveis no Banco de Dados SQL do Azure permitem que você trate os dados formatados como JSON como qualquer outro tipo de dados do SQL. Você pode facilmente extrair valores de saudação texto JSON e usam dados JSON em qualquer consulta:

```
select Id, Title, JSON_VALUE(Data, '$.Color'), JSON_QUERY(Data, '$.tags')
from Products
where JSON_VALUE(Data, '$.Color') = 'White'

update Products
set Data = JSON_MODIFY(Data, '$.Price', 60)
where Id = 1
```

Olá função JSON_VALUE extrai um valor de texto JSON armazenado na coluna de dados de saudação. Essa função usa tooreference um caminho de JavaScript como um valor em tooextract de texto JSON. valor de saudação extraída pode ser usado em qualquer parte da consulta SQL.

Olá função JSON_QUERY é tooJSON_VALUE semelhante. Ao contrário de JSON_VALUE, essa função extrai subobjetos complexos, como matrizes ou objetos que são colocados em texto JSON.

função JSON_MODIFY de saudação permite especificar o caminho de saudação do valor de saudação em texto JSON Olá que deve ser atualizado, bem como um novo valor que substituirá Olá antigo. Dessa forma, que você pode atualizar facilmente texto JSON sem analisando a estrutura inteira hello.

Como JSON é armazenado em um padrão de texto, não há nenhuma garantia que valores hello armazenados em colunas de texto estão formatados corretamente. Você pode verificar se o texto armazenado na coluna JSON está formatado corretamente usando o padrão de restrições de verificação de banco de dados SQL e hello função ISJSON:

```
ALTER TABLE Products
    ADD CONSTRAINT [Data should be formatted as JSON]
        CHECK (ISJSON(Data) > 0)
```

Se o texto de entrada hello está corretamente formatado JSON, Olá função ISJSON retorna o valor de saudação 1. Em cada inserção ou atualização de coluna JSON, essa restrição irá verificar se o novo valor de texto não é um JSON malformado.

## <a name="transforming-json-into-tabular-format"></a>Transformando o JSON em formato tabular
O Banco de Dados SQL do Azure também permite transformar coleções de JSON em formato tabular e carregar ou consultar dados JSON.

OPENJSON é uma função com valor de tabela que analisa texto JSON, localiza uma matriz de objetos JSON, itera por meio de elementos de saudação da matriz de saudação e retorna uma linha no resultado Olá para cada elemento da matriz de saudação.

![JSON tabular](./media/sql-database-json-features/image_2.png)

O exemplo hello acima, podemos especificar onde toolocate Olá matriz JSON que deve ser aberto (em $ Oi. Caminho de pedidos), a quais colunas devem ser retornadas como resultado, e onde toofind Olá valores JSON que serão retornados como células.

É possível transformar uma matriz JSON em Olá @orders variável em um conjunto de linhas, analisar esse conjunto de resultados, ou inserir linhas em uma tabela padrão:

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
coleção de saudação de pedidos formatada como uma matriz JSON e fornecido como um procedimento armazenado de toohello de parâmetro pode ser analisado e inserido na tabela de pedidos de saudação.

## <a name="next-steps"></a>Próximas etapas
toolearn como toointegrate JSON em seu aplicativo, confira esses recursos:

* [Blog do TechNet](https://blogs.technet.microsoft.com/dataplatforminsider/2016/01/05/json-in-sql-server-2016-part-1-of-4/)
* [Documentação do MSDN](https://msdn.microsoft.com/library/dn921897.aspx)
* [Vídeo do Canal 9](https://channel9.msdn.com/Shows/Data-Exposed/SQL-Server-2016-and-JSON-Support)

toolearn sobre os vários cenários para integrar o JSON em seu aplicativo, consulte demonstrações Olá neste [vídeo do Channel 9](https://channel9.msdn.com/Events/DataDriven/SQLServer2016/JSON-as-a-bridge-betwen-NoSQL-and-relational-worlds) ou encontrar um cenário que corresponde a seu caso de uso em [postagens no Blog do JSON](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/).

