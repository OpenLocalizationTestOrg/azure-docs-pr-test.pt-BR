---
title: arquitetura de mecanismo (Lucene) de pesquisa de texto de aaaFull na pesquisa do Azure | Microsoft Docs
description: "Explicação dos conceitos de recuperação Lucene consulta processamento e o documento para pesquisa de texto completo, como tooAzure relacionado a pesquisa."
services: search
manager: jhubbard
author: yahnoosh
documentationcenter: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/06/2017
ms.author: jlembicz
ms.openlocfilehash: c6d1bea8d40154fd9237b9e44584cdfcd193cbd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-full-text-search-works-in-azure-search"></a>Como funciona a pesquisa de texto completo no Azure Search

Este artigo é para desenvolvedores que precisam de uma compreensão mais profunda de como a pesquisa de texto completo do Lucene funciona no Azure Search. Para consultas de texto, o Azure Search fornecerá perfeitamente os resultados esperados na maioria dos cenários, mas, ocasionalmente, você pode obter um resultado que pode parecer "estranho". Nessas situações, ter um plano de fundo em Olá quatro estágios da execução da consulta Lucene (análise lexical, análise de consulta, correspondência, a pontuação de documento) pode ajudar a identificar alterações específicas tooquery parâmetros ou configuração que fornecerão Olá de índice resultado desejado. 

> [!Note] 
> O Azure Search usa o Lucene para pesquisa de texto completo, mas a integração do Lucene não é completa. Estamos seletivamente expor e estender cenários Lucene funcionalidade tooenable Olá importante tooAzure pesquisa. 

## <a name="architecture-overview-and-diagram"></a>Diagrama e visão geral da arquitetura

Processamento de uma consulta de pesquisa de texto completo inicia com termos de pesquisa tooextract do texto de consulta de saudação de análise. mecanismo de pesquisa Olá usa um tooretrieve de indexar documentos com os termos correspondentes. Termos de consulta individual, às vezes, são divididos e reconstituído em nova toocast de formulários uma rede mais ampla sobre o que poderia ser considerado como uma correspondência potencial. Um conjunto de resultados, em seguida, é classificado por um relevância pontuação tooeach atribuído correspondente documento individual. Aqueles na parte superior de saudação do hello classificado lista são retornados toohello aplicativo de chamada.

A execução de consulta redefinida, tem quatro fases: 

1. Análise da consulta 
2. Análise léxica 
3. Recuperação de documentos 
4. Pontuação 

diagrama de saudação abaixo ilustra Olá componentes usados tooprocess uma solicitação de pesquisa. 

 ![Diagrama da arquitetura de consulta do Lucene no Azure Search][1]


| Principais componentes | Descrição funcional | 
|----------------|------------------------|
|**Analisadores de consulta** | Separar os termos de consulta de operadores de consulta e criar o mecanismo de pesquisa de toohello Olá consulta estrutura (árvore de consulta) toobe enviado. |
|**Analisadores** | Executam a análise léxica dos termos de consulta. Esse processo pode envolver a transformação, remoção ou expansão dos termos de consulta. |
|**Índice** | Uma estrutura de dados eficiente usado toostore e organizar pesquisáveis termos extraídos de documentos indexados. |
|**Mecanismo de pesquisa** | Recupera e pontuações de correspondência de documentos com base no conteúdo de saudação do índice Olá invertido. |

## <a name="anatomy-of-a-search-request"></a>Anatomia de uma solicitação de pesquisa

Uma solicitação de pesquisa é uma especificação completa do que deve ser retornado em um conjunto de resultados. Na forma mais simples, é uma consulta vazia sem critérios de nenhum tipo. Um exemplo mais realista inclui parâmetros, vários termos, talvez com escopo toocertain campos, com possivelmente uma expressão de filtro e as regras de ordenação de consulta.  

Olá, exemplo a seguir é uma solicitação de pesquisa que você pode enviar tooAzure pesquisa usando Olá [API REST](https://docs.microsoft.com/rest/api/searchservice/search-documents).  

~~~~
POST /indexes/hotels/docs/search?api-version=2016-09-01 
{  
    "search": "Spacious, air-condition* +\"Ocean view\"",  
    "searchFields": "description, title",  
    "searchMode": "any",
    "filter": "price ge 60 and price lt 300",  
    "orderby": "geo.distance(location, geography'POINT(-159.476235 22.227659)')", 
    "queryType": "full" 
 } 
~~~~

Para essa solicitação, o mecanismo de pesquisa Olá Olá a seguir:

1. Filtra os documentos cujo preço de saudação é pelo menos US $60 e menor que US $300.
2. Executa a consulta de saudação. Neste exemplo, consulta de pesquisa de saudação consiste de frases e termos: `"Spacious, air-condition* +\"Ocean view\""` (os usuários geralmente não insira pontuação, mas incluí-lo no exemplo hello permite tooexplain como analisadores de tratar). Para essa consulta, o mecanismo de pesquisa de saudação examina descrição Olá e campos de título especificado em `searchFields` para documentos que contenham "Exibição Oceano" e além no termo de hello "amplo" ou em termos que começam com hello prefixo "air-condition". Olá `searchMode` parâmetro está toomatch usado em qualquer termo (padrão) ou todos eles, para casos em que um termo não é explicitamente necessário (`+`).
3. Pedidos Olá conjunto resultante de hotéis por proximidade tooa dado geografia local e, em seguida, retornado toohello aplicativo de chamada. 

Olá maior parte deste artigo é sobre o processamento de saudação *consulta de pesquisa*: `"Spacious, air-condition* +\"Ocean view\""`. Filtragem e ordenação estão fora do escopo. Para obter mais informações, consulte Olá [documentação de referência de API de pesquisa](https://docs.microsoft.com/rest/api/searchservice/search-documents).

<a name="stage1"></a>
## <a name="stage-1-query-parsing"></a>Estágio 1: Análise da consulta 

Conforme observado, cadeia de caracteres de consulta de saudação é Olá primeira linha da solicitação de saudação: 

~~~~
 "search": "Spacious, air-condition* +\"Ocean view\"", 
~~~~

Analisador separa os operadores de consulta de saudação (como `*` e `+` no exemplo hello) da pesquisa de termos e deconstructs consulta de pesquisa de saudação em *subconsultas* de um tipo com suporte: 

+ *consulta de termo* para termos independentes (espaçoso, por exemplo)
+ *consulta de frase* para termos entre aspas (vista para o mar, por exemplo)
+ *consulta de prefixo* por termos seguidos por um operador de prefixo `*` (ar-condicio, por exemplo)

Para obter uma lista completa dos tipos de consulta com suporte, consulte [sintaxe da consulta do Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

Operadores associados com uma subconsulta determinam se a consulta hello "deve ser" ou "deve ser" satisfeito para que um documento toobe considerados uma correspondência. Por exemplo, `+"Ocean view"` é "deve" vencimento toohello `+` operador. 

Analisador de consulta Olá reestrutura subconsultas Olá em um *árvore de consulta* (uma estrutura interna que representa a consulta Olá) passa no mecanismo de pesquisa toohello. No primeiro estágio da análise de consulta hello, árvore de consulta Olá tem esta aparência.  

 ![Booliano consulta modo de pesquisa qualquer][2]

### <a name="supported-parsers-simple-and-full-lucene"></a>Analisadores com suporte: simples e Lucena completa 

 O Azure Search apresenta duas linguagens de consulta diferentes, `simple` (padrão) e `full`. Por definição Olá `queryType` parâmetro com sua solicitação de pesquisa, você informar o analisador de consulta Olá a linguagem de consulta que você escolher para que ele saiba como toointerpret Olá operadores e sintaxe. Olá [idioma de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) é intuitiva e robusta, geralmente adequado toointerpret entrada do usuário como-sem processamento no lado do cliente. Ela oferece suporte a operadores de consulta familiares de mecanismos de pesquisa. Olá [Lucene completo a linguagem de consulta](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), que você obtém definindo `queryType=full`, estende o idioma de consulta simples saudação padrão adicionando suporte para mais operadores e tipos de consulta como caractere curinga, difusa, regex e consultas com escopo de campo. Por exemplo, uma expressão regular enviada na sintaxe de consulta simples será interpretada como uma cadeia de caracteres de consulta e não é uma expressão. solicitação de exemplo Hello neste artigo usa a linguagem de consulta Olá Lucene completo.

### <a name="impact-of-searchmode-on-hello-parser"></a>Impacto de searchMode no analisador de saudação 

Outro parâmetro de solicitação de pesquisa que afeta a análise é hello `searchMode` parâmetro. Ele controla o operador de padrão de saudação para consultas booleanas: qualquer (padrão) ou todos.  

Quando `searchMode=any`, que é saudação padrão, o delimitador de espaço de saudação entre amplo e air-condition é ou (`||`), tornando o texto de consulta de exemplo hello equivalente a: 

~~~~
Spacious,||air-condition*+"Ocean view" 
~~~~

Operadores explícitos, como `+` na `+"Ocean view"`, são sejam ambíguos na construção de consulta booliano (termo Olá *deve* correspondem). É menos óbvio como Olá toointerpret restantes termos: amplo e air-condition. O mecanismo de pesquisa Olá deve localizar correspondências no mar *e* amplo *e* air-condition? Ou ele deve localizar mar mais *um* de saudação restantes termos? 

Por padrão (`searchMode=any`), o mecanismo de pesquisa Olá assume interpretação mais ampla de saudação. Cada campo *deve* ter uma correspondência, refletindo a semântica de "ou". árvore de consulta inicial de saudação ilustrado anteriormente, com hello duas "deve" operações, mostra saudação padrão.  

Suponha que agora definimos `searchMode=all`. Nesse caso, o espaço de saudação é interpretado como uma operação "e". Cada um dos termos de saudação restantes deve ambos estar presente na Olá documento tooqualify como uma correspondência. consulta de exemplo Hello resultante será interpretada da seguinte maneira: 

~~~~
+Spacious,+air-condition*+"Ocean view"  
~~~~

Uma árvore de consulta modificada para essa consulta seria a seguinte, onde um documento correspondente é a interseção de saudação de todas as três subconsultas: 

 ![Booliano consulta modo de pesquisa todos][3]

> [!Note] 
> Escolher `searchMode=any` em vez de `searchMode=all` é uma decisão melhor ao executar consultas representativas. Os usuários que são provavelmente tooinclude operadores (comum ao documento pesquisando armazena) pode encontrar resultados mais intuitiva se `searchMode=all` informa construções de consulta boolean. Para obter mais informações sobre a interação entre a saudação entre `searchMode` e operadores, consulte [sintaxe de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search).

<a name="stage2"></a>
## <a name="stage-2-lexical-analysis"></a>Estágio 2: Análise léxica 

Processo de analisadores léxicos *consultas de termos* e *consultas de frase* depois Olá árvore de consulta é estruturada. Um analisador aceita Olá texto entradas dadas tooit pelo analisador hello, processos Olá texto e, em seguida, envia de volta token termos toobe incorporadas Olá árvore de consulta. 

saudação de forma mais comum de análise lexical é *análise linguística* que transforma os termos de consulta com base em regras tooa específico dado idioma: 

* Reduzindo forma consulta termo toohello raiz de uma palavra 
* Removendo palavras não-essenciais (palavras irrelevantes, como "o/a" ou "e" em português) 
* Dividir uma palavra composta em componentes 
* Colocando letras minúsculas em uma palavra de letras maiúsculas 

Todas essas operações tendem tooerase diferenças entre a entrada de texto de saudação fornecida pelos termos de usuário e hello de saudação armazenados no índice de saudação. Essas operações vão além do processamento de texto e exigem conhecimento profundo do idioma de saudação em si. tooadd essa camada de reconhecimento de linguística, pesquisa do Azure oferece suporte a uma lista extensa de [analisadores de idioma](https://docs.microsoft.com/rest/api/searchservice/language-support) do Lucene e Microsoft.

> [!Note]
> Requisitos de análise podem variar de tooelaborate mínimo dependendo do cenário. Você pode controlar a complexidade da análise lexical Olá selecionando um dos analisadores de saudação predefinida ou criando seu próprio [analisador personalizado](https://docs.microsoft.com/rest/api/searchservice/Custom-analyzers-in-Azure-Search). Analisadores são campos toosearchable no escopo e são especificadas como parte de uma definição de campo. Isso permite que você toovary lexicais em uma base por campo. Não for especificado, Olá *padrão* Lucene analisador é usada.

Em nosso exemplo, tooanalysis anterior, árvore de consulta inicial de saudação tem termo hello "Spacious" com um "S" maiuscula e uma vírgula que Olá analisador de consulta interpreta como parte do termo da consulta hello (uma vírgula não é considerada um operador de linguagem de consulta).  

Quando o analisador de padrão de saudação processa termo Olá, ele será minúsculas "exibição Oceano" e "amplo" e remover o caractere de vírgula hello. árvore de consulta modificada Olá será semelhante ao seguinte: 

 ![Consulta booliana com termos analisados][4]

### <a name="testing-analyzer-behaviors"></a>Testando os comportamentos do analisador 

comportamento de saudação de um analisador pode ser testado usando Olá [analisar API](https://docs.microsoft.com/rest/api/searchservice/test-analyzer). Forneça o texto de saudação que deseja tooanalyze toosee quais termos fornecidos analyzer irá gerar. Por exemplo, toosee como processaria analisador padrão Olá Olá texto "air-condition", você pode emitir Olá solicitação a seguir:

~~~~
{ 
    "text": "air-condition",
    "analyzer": "standard"
}
~~~~

Analisador padrão saudação quebra o texto de entrada hello em Olá dois tokens, anotando-las com atributos como iniciar e deslocamentos de término (usados para realçar as ocorrências), bem como sua posição (usada para correspondência de frase) a seguir:

~~~~
{  
  "tokens": [
    {
      "token": "air",
      "startOffset": 0,
      "endOffset": 3,
      "position": 0
    },
    {
      "token": "condition",
      "startOffset": 4,
      "endOffset": 13,
      "position": 1
    }
  ]
}
~~~~

### <a name="exceptions-toolexical-analysis"></a>Análise de toolexical de exceções 

Análise lexical aplica-se somente os tipos de tooquery que exigem termos completos – uma consulta de termo ou uma consulta de frase. Ele não se aplica a tipos de tooquery com termos incompletos – consulta de prefixo, consulta curinga, regex consulta – ou consulta difusa tooa. Os tipos, incluindo Olá prefixo consulta com o termo de consulta *air-condition\**  em nosso exemplo, são adicionados diretamente toohello árvore de consulta, ignorando o estágio de análise de saudação. Olá somente transformação executada em termos de consulta desses tipos é minúsculas.

<a name="stage3"></a>
## <a name="stage-3-document-retrieval"></a>Estágio 3: Recuperação de documentos 

Recuperação de documentos se refere a documentos toofinding com os termos correspondentes no índice de saudação. Este estágio é melhor compreendido por meio de um exemplo. Vamos começar com um índice de hotéis com hello esquema simples a seguir: 

~~~~
{   
    "name": "hotels",     
    "fields": [     
        { "name": "id", "type": "Edm.String", "key": true, "searchable": false },     
        { "name": "title", "type": "Edm.String", "searchable": true },     
        { "name": "description", "type": "Edm.String", "searchable": true }
    ] 
} 
~~~~

Suponha ainda que esse índice contém Olá quatro documentos a seguir: 

~~~~
{ 
    "value": [
        {         
            "id": "1",         
            "title": "Hotel Atman",         
            "description": "Spacious rooms, ocean view, walking distance toohello beach."   
        },       
        {         
            "id": "2",         
            "title": "Beach Resort",        
            "description": "Located on hello north shore of hello island of Kauaʻi. Ocean view."     
        },       
        {         
            "id": "3",         
            "title": "Playa Hotel",         
            "description": "Comfortable, air-conditioned rooms with ocean view."
        },       
        {         
            "id": "4",         
            "title": "Ocean Retreat",         
            "description": "Quiet and secluded"
        }    
    ]
}
~~~~

**Como os termos são indexados**

recuperação de toounderstand ajuda tooknow alguns conceitos básicos sobre indexação. unidade de saudação de armazenamento é um índice invertido, um para cada campo pesquisável. Dentro de um índice invertido está uma lista classificada de todos os termos de todos os documentos. Cada termo mapeia toohello lista de documentos em que ele ocorre, como demonstrados no exemplo hello abaixo.

termos de saudação tooproduce no índice invertido, mecanismo de pesquisa Olá executa análise lexical sobre o conteúdo da saudação de documentos, toowhat semelhante acontece durante o processamento de consulta. Entradas de texto são passadas tooan analyzer, em minúsculas, retirada de pontuação e assim por diante, dependendo da configuração do analisador de saudação. É comum, mas não é necessária, toouse Olá mesmo analisadores de pesquisa e as operações de indexação para que os termos de consulta pareça mais com termos no índice de saudação.

> [!Note]
> O Azure Search permite especificar diferentes analisadores para indexação e pesquisa através dos parâmetros de campo adicionais `indexAnalyzer` e `searchAnalyzer`. Se não for especificado, Olá analisador com hello `analyzer` propriedade é usada para indexação e pesquisa.  

**Índice invertido para documentos de exemplo**

Retornando tooour exemplo, para Olá **título** campo, índice invertida de saudação tem esta aparência:

| Termo | Lista de documentos |
|------|---------------|
| atman | 1 |
| praia | 2 |
| hotel | 1, 3 |
| mar | 4  |
| playa | 3 |
| resort | 3 |
| retiro | 4 |

No campo de título de hello, apenas *hotel* aparece em dois documentos: 1, 3.

Para Olá **descrição** campo, o índice de saudação é da seguinte maneira:

| Termo | Lista de documentos |
|------|---------------|
| ar | 3
| e | 4
| praia | 1
| condicionado | 3
| confortável | 3
| distância | 1
| ilha | 2
| kauaʻi | 2
| local | 2
| norte | 2
| mar | 1, 2, 3
| de | 2
| em |2
| silencioso | 4
| quartos  | 1, 3
| reservado | 4
| beira-mar | 2
| espaçoso | 1
| Olá | 1, 2
| muito| 1
| view | 1, 2, 3
| a pé | 1
| por: | 3


**Correspondência de termos de consulta com os termos indexados**

Considerando índices de saudação invertida acima, vamos retornar toohello exemplo de consulta e ver como correspondência de documentos são encontrados para a consulta de exemplo. Lembre-se de que árvore de consulta final que Olá tem esta aparência: 

 ![Consulta booliana com termos analisados][4]

Durante a execução de consulta, consultas individuais são executadas em campos pesquisáveis Olá independentemente. 

+ TermQuery Hello, corresponde a "amplo", 1 (Hotel Atman) do documento. 

+ Olá PrefixQuery, "air-condition *", não corresponde a todos os documentos. 

  Esse é um comportamento que às vezes confunde os desenvolvedores. Embora o termo de saudação com ar condicionado existe no documento hello, será dividida em dois termos pelo analisador de padrão de saudação. Lembre-se de que as consultas de prefixo, que contêm termos parciais, não são analisadas. Portanto termos de prefixo "air-condition" é pesquisados no hello índice invertido e não encontrado.

+ PhraseQuery Hello, "exibição Oceano", procura termos hello "ocean" e "Exibir" e verifica a proximidade de saudação de termos no documento original hello. 1, 2 e 3 de documentos correspondem a esta consulta no campo de descrição de saudação. Documento de aviso 4 tem azul-marinho Olá termo no título hello, mas não é considerado uma correspondência, como estamos procurando frase de "exibição Oceano" Olá, em vez de palavras individuais. 

> [!Note]
> Uma consulta de pesquisa é executada independentemente em todos os campos pesquisáveis Olá índice de pesquisa do Azure, a menos que você limitar campos Olá com hello `searchFields` parâmetro, conforme ilustrado na solicitação de pesquisa do exemplo hello. Documentos que correspondam a qualquer um dos campos de saudação selecionado são retornados. 

Em Olá inteira, para consulta de saudação em questão, documentos Olá correspondentes são 1, 2, 3. 

## <a name="stage-4-scoring"></a>Estágio 4: Pontuação  

Todos os documentos em um conjunto de resultados de pesquisa recebe uma pontuação de relevância. função Hello da pontuação de relevância Olá é toorank superior esses documentos melhor responder a um usuário pergunta conforme expresso pela consulta de pesquisa de saudação. pontuação de saudação é calculada com base nas propriedades estatísticas dos termos correspondentes. Em Olá núcleo da saudação pontuação fórmula é [TF/IDF (frequência de documento inversa da frequência do termo)](https://en.wikipedia.org/wiki/Tf%E2%80%93idf). Em consultas que contêm termos comuns e raros, TF/IDF promove resultados que contenham o termo raros hello. Por exemplo, em um índice hipotético com todos os artigos da Wikipédia, de documentos de consulta Olá correspondentes *presidente Olá*, correspondência de documentos *presidente* são considerados mais relevantes do que correspondência de documentos *o*.


### <a name="scoring-example"></a>Exemplo de pontuação

Lembre-se de saudação três documentos que correspondem a consulta de exemplo:
~~~~
search=Spacious, air-condition* +"Ocean view"  
~~~~
~~~~
{  
  "value": [
    {
      "@search.score": 0.25610128,
      "id": "1",
      "title": "Hotel Atman",
      "description": "Spacious rooms, ocean view, walking distance toohello beach."
    },
    {
      "@search.score": 0.08951007,
      "id": "3",
      "title": "Playa Hotel",
      "description": "Comfortable, air-conditioned rooms with ocean view."
    },
    {
      "@search.score": 0.05967338,
      "id": "2",
      "title": "Ocean Resort",
      "description": "Located on a cliff on hello north shore of hello island of Kauai. Ocean view."
    }
  ]
}
~~~~

Documento 1 consulta Olá correspondentes melhor porque ambos Olá termo *amplo* e frase necessário Olá *mar* ocorrer no campo de descrição de saudação. documentos próximas duas Olá correspondem apenas a frase de saudação *mar*. Talvez ele ser surpreendentes essa pontuação de relevância Olá para documento 2 e 3 é diferente, mesmo que eles correspondido consulta Olá Olá mesma maneira. Isso ocorre porque Olá pontuação fórmula tem mais componentes do que apenas TF/IDF. Nesse caso, o documento 3 recebeu uma pontuação ligeiramente mais alta porque sua descrição é mais curta. Saiba mais sobre [prático pontuação fórmula do Lucene](https://lucene.apache.org/core/4_0_0/core/org/apache/lucene/search/similarities/TFIDFSimilarity.html) toounderstand como o tamanho do campo e outros fatores podem influenciar Olá pontuação de relevância.

Alguns tipos (curinga, prefixo, regex) de consulta sempre contribuir uma pontuação constante toohello geral de pontuação de documento. Isso permite que as correspondências encontradas por meio de consulta expansão toobe incluído nos resultados da saudação, mas sem afetar a classificação de saudação. 

Um exemplo ilustra por que isso é importante. Pesquisas com curinga, inclusive pesquisas de prefixo, são ambíguas por definição, porque a entrada hello é uma cadeia de caracteres parcial com correspondências possíveis em um grande número de termos diferentes (considere uma entrada de "tour *", com correspondências encontradas em "viagens", "tourettes", e " tourmaline"). Considerando a natureza Olá desses resultados, não é possível inferir tooreasonably quais termos são mais valiosos do que outras pessoas. Por esse motivo, podemos ignorar as frequências dos termos ao pontuar resultados em consultas dos tipos caractere curinga, prefixo e regex. Em uma solicitação de pesquisa de várias partes que inclui termos parciais e completas, resultados de entrada parcial Olá são incorporados com uma constante de pontuação tooavoid tendência para correspondências potencialmente inesperadas.

### <a name="score-tuning"></a>Ajuste da pontuação

Há duas maneiras de pontuações de relevância tootune na pesquisa do Azure:

1. **Perfis de pontuação** promover documentos Olá classificado lista de resultados com base em um conjunto de regras. Em nosso exemplo, é possível considerar documentos correspondentes no campo de título hello mais relevante do que os documentos correspondam no campo de descrição de saudação. Além disso, se o índice tiver um campo preço para cada hotel, poderíamos promover documentos com preços mais baixos. Saiba mais como muito[adicionar um índice de pesquisa tooa perfis de pontuação.](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)
2. **Aumento de termos** (disponível apenas na sintaxe da consulta completa Lucene Olá) fornece um operador de aumento `^` que podem ser aplicadas tooany parte da árvore de consulta hello. Em nosso exemplo, em vez de procurar no prefixo Olá *air-condition*\*, um pode procurar qualquer uma das palavras exatas Olá *air-condition* ou prefixo hello, mas os documentos que correspondam Olá exata termo são com classificação mais alta por aumento toohello termo consulta: *ar condição ^ 2 | | AIR-condition**. Saiba mais sobre [incremento do termo](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search#bkmk_termboost).


### <a name="scoring-in-a-distributed-index"></a>Pontuação em um índice distribuído

Todos os índices de pesquisa do Azure são automaticamente dividido em vários fragmentos, possibilitando tooquickly distribuir índice Olá entre vários nós durante a escala do serviço para cima ou reduzir. Quando uma solicitação de pesquisa é emitida, ela é emitida em relação a cada fragmento de forma independente. Olá resultados de cada fragmento são, em seguida, mesclados e ordenados pela classificação (se nenhuma outra ordem é definida). É importante tooknow que Olá pontuação função pesos consulta frequência do termo em relação a sua frequência de documento inversa em todos os documentos no fragmento hello, não em todos os fragmentos!

Isso significa que uma pontuação de relevância *pode* ser diferentes para documentos idênticos se estes estiverem em fragmentos diferentes. Felizmente, tais diferenças tendem toodisappear à medida que aumenta de número de saudação de documentos do índice de saudação devido a distribuição do mesmo termo toomore. Não é possível tooassume no qual fragmento qualquer dado documento será colocado. No entanto, supondo que uma chave de documento não é alterado, será sempre atribuído toohello mesmo fragmento.

Em geral, a pontuação de documento não é atributo melhor Olá ordenação documentos se a estabilidade de ordem é importante. Por exemplo, não dado documento dois com pontuação idêntica, há nenhuma garantia de qual item aparecerá primeiro nas execuções subsequentes do hello mesma consulta. Pontuação de documento somente dará uma ideia geral de relevância do documento relativo tooother documentos no conjunto de resultados de saudação.

## <a name="conclusion"></a>Conclusão

sucesso Olá dos mecanismos de pesquisa da internet gerou expectativas para pesquisa de texto completo em dados privados. Para quase qualquer tipo de experiência de pesquisa, agora esperamos Olá mecanismo toounderstand nossa intenção, mesmo quando os termos estão incorretas ou incompleta. Esperamos até correspondências com base em termos equivalentes ou sinônimos que nem especificamos.

Do ponto de vista técnico, pesquisa de texto completo é altamente complexa, exigindo análise linguística sofisticada e tooprocessing uma abordagem sistemática de forma a processar, expanda e transformar os termos de consulta toodeliver um resultado relevante. Devido a complexidades inerentes hello, há uma série de fatores que podem afetar o resultado de saudação de uma consulta. Por esse motivo, investir mecânica de saudação de toounderstand Olá tempo de pesquisa de texto completo oferece benefícios tangíveis durante a tentativa de toowork a resultados inesperados.  

Este artigo explorou a pesquisa de texto completo no contexto de saudação da pesquisa do Azure. Esperamos que ele fornece suficientes em segundo plano toorecognize possíveis causas e resoluções para tratar de problemas comuns de consulta. 

## <a name="next-steps"></a>Próximas etapas

+ Criar índice de exemplo hello, experimente consultas diferentes e examine os resultados. Para obter instruções, consulte [construir e consultar um índice no portal de saudação](search-get-started-portal.md#query-index).

+ Tente a sintaxe de consulta adicionais de saudação [procurar documentos](https://docs.microsoft.com/rest/api/searchservice/search-documents#examples) seção de exemplo ou de [sintaxe de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) no Gerenciador de pesquisa no portal de saudação.

+ Revisão [perfis de pontuação](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) se você quiser tootune classificando em seu aplicativo de pesquisa.

+ Saiba como tooapply [analisadores de idioma específico lexicais](https://docs.microsoft.com/rest/api/searchservice/language-support).

+ [Configurar analisadores personalizados](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) para o mínimo de processamento ou processamento especializado em campos específicos.

+ [Compare os analisadores padrão e inglês](http://alice.unearth.ai/) lado a lado neste site da Web de demonstração. 

## <a name="see-also"></a>Consulte também

[API REST para pesquisar documentos](https://docs.microsoft.com/rest/api/searchservice/search-documents)

[Sintaxe de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search)

[Sintaxe de consulta Lucene completa](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search)

[Controlar os resultados da pesquisa](https://docs.microsoft.com/azure/search/search-pagination-page-layout)

<!--Image references-->
[1]: ./media/search-lucene-query-architecture/architecture-diagram2.png
[2]: ./media/search-lucene-query-architecture/azSearch-queryparsing-should2.png
[3]: ./media/search-lucene-query-architecture/azSearch-queryparsing-must2.png
[4]: ./media/search-lucene-query-architecture/azSearch-queryparsing-spacious2.png
