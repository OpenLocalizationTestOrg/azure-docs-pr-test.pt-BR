---
title: tipos de dados complexos toomodel aaaHow na pesquisa do Azure | Microsoft Docs
description: "As estruturas de dados aninhadas e hierárquicas podem ser modeladas em um índice do Azure Search usando o conjunto de linhas nivelado e o tipo de dados Coleções."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a>Como os tipos de dados complexos toomodel na pesquisa do Azure
Conjuntos de dados externos usados toopopulate um índice de pesquisa do Azure, às vezes, incluem subestruturas hierárquicas ou aninhadas que não dividir organizado em um conjunto de linhas da tabela. Os exemplos dessas estruturas podem incluir vários locais e números de telefone para um único cliente, vários tamanhos e cores para um único SKU, vários autores de um único livro e assim por diante. Em termos de modelagem, você pode ver essas estruturas chamado tooas *tipos de dados complexos*, *composta de tipos de dados*, *tipos de dados compostos*, ou *agregação tipos de dados*, tooname alguns.

Tipos de dados complexos não são suportados na pesquisa do Azure, mas uma solução alternativa comprovada inclui um processo de duas etapas de estrutura Olá a simplificação e, em seguida, usando um **coleção** estrutura interna do tooreconstitute saudação do tipo de dados. Seguir técnica Olá descrita neste artigo permite toobe conteúdo Olá pesquisada, faceta, filtrados e classificados.

## <a name="example-of-a-complex-data-structure"></a>Exemplo de uma estrutura de dados complexos
Normalmente, dados de saudação em questão residem como um conjunto de documentos XML ou JSON, ou como itens em um repositório NoSQL, como o banco de dados do Azure Cosmos. Estruturalmente, desafio Olá origina-se de ter vários itens filho que precisam toobe pesquisados e filtrados.  Como um ponto de partida para ilustrar a solução alternativa de saudação levar Olá documento JSON que lista um conjunto de contatos como um exemplo a seguir:

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

Enquanto campos Olá chamado 'id', 'name' e 'empresa' podem facilmente ser mapeados individualmente como campos dentro de um índice de pesquisa do Azure, o campo do hello 'local' contém uma matriz de locais, tendo ambos um conjunto de IDs de local, bem como descrições de local. Considerando que a pesquisa do Azure não tem um tipo de dados que oferece suporte a isso, é preciso um toomodel de maneira diferente isso na pesquisa do Azure. 

> [!NOTE]
> Essa técnica também é descrita por Kirk Evans uma postagem de blog [a indexação de documentos com pesquisa do Azure](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), que mostra uma técnica chamada "nivelamento Olá dados", no qual você teria um campo chamado `locationsID` e `locationsDescription` que são ambos [coleções](https://msdn.microsoft.com/library/azure/dn798938.aspx) (ou uma matriz de cadeias de caracteres).   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a>Parte 1: Mesclar matriz Olá em campos individuais
toocreate um índice de pesquisa do Azure que acomoda a esse conjunto de dados, criar campos individuais para estruturados aninhada Olá: `locationsID` e `locationsDescription` com um tipo de dados de [coleções](https://msdn.microsoft.com/library/azure/dn798938.aspx) (ou uma matriz de cadeias de caracteres). Nesses campos você seria indexar valores hello '1' e '2' hello `locationsID` campo para valores de John Smith e hello '3' & '4' em Olá `locationsID` campo Jen Campbell.  

Os dados no Azure Search ficariam assim: 

![dados de exemplo, 2 linhas](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a>Parte 2: Adicionar um campo de conjunto na definição de índice de saudação
No esquema de índice hello, definições de campo Olá podem parecer exemplo toothis semelhante.

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a>Validar comportamentos de pesquisa e, opcionalmente, estender índice Olá
Supondo que você índice criado hello e dados carregados de saudação, agora você pode testar execução de consulta de pesquisa Olá solução tooverify no conjunto de dados de saudação. Cada campo da **coleção** deve ser **pesquisável**, **filtrável** e **lapidável**. Você deve ser capaz de toorun consultas como:

* Localize todas as pessoas que trabalham na Olá 'Adventureworks Headquarters'.
* Obter uma contagem do número de saudação de pessoas que trabalham em um escritório' Início'.  
* Olá que as pessoas que trabalham em um escritório' Início', mostram quais outros escritórios que funcionam junto com uma contagem de pessoas de saudação em cada local.  

Onde essa técnica cai distância é quando você precisa toodo uma pesquisa que combina o id de local de saudação, bem como descrição do local de hello. Por exemplo:

* Localize todas as pessoas onde elas têm um Escritório Central E uma Identificação de local 4.  

Se você recuperar o conteúdo original hello, semelhante a este:

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

No entanto, agora que dividimos dados saudação em campos separados, não temos nenhuma maneira de saber se a saudação inicial do Office para Jen Campbell relaciona muito`locationsID 3` ou `locationsID 4`.  

toohandle nesse caso, defina outro campo no índice de saudação que combina todos os dados de saudação em uma única coleção.  Para nosso exemplo, chamaremos esse campo `locationsCombined` e estamos separará conteúdo Olá com um `||` Embora você possa escolher qualquer separador que você acha que seria um conjunto exclusivo de caracteres para o seu conteúdo. Por exemplo: 

![dados de exemplo, 2 linhas com separador](./media/search-howto-complex-data-types/sample-data-2.png)

Usando esse campo `locationsCombined` , agora podemos aceitar ainda mais consultas, como:

* Mostre uma contagem de pessoas que trabalham em um 'Escritório Central' com uma Id de local '4'.  
* Procure as pessoas que trabalham em um ‘Escritório Central' com uma Id de local '4'. 

## <a name="limitations"></a>Limitações
Essa técnica é útil para vários cenários, mas ela não é aplicável em todos os casos.  Por exemplo:

1. Se você não tem um conjunto estático de campos no seu tipo de dados complexos e não havia nenhuma maneira toomap todos os possíveis Olá tipos tooa único campo. 
2. Atualizando objetos de saudação aninhado requer toodetermine algum trabalho extra exatamente o que precisa toobe atualizado no índice de pesquisa do Azure Olá

## <a name="sample-code"></a>Exemplo de código
Você pode ver um exemplo sobre como tooindex um dados JSON complexos configurado na pesquisa do Azure e executar um número de consultas sobre este conjunto de dados neste [repositório GitHub](https://github.com/liamca/AzureSearchComplexTypes).

## <a name="next-step"></a>Próxima etapa
[Voto para o suporte nativo para tipos de dados complexos](https://feedback.azure.com/forums/263029-azure-search) em hello Azure UserVoice de pesquisa de página e fornecer qualquer entrada adicional que você deseja tooconsider sobre implementação de recurso. Você também pode alcançar toome diretamente no Twitter em @liamca.

