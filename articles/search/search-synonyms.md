---
pageTitle: Synonyms in Azure Search (preview) | Microsoft Docs
description: "Documentação preliminar para o recurso de sinônimos (visualização) hello, exposto em Olá API de REST de pesquisa do Azure."
services: search
documentationCenter: 
authors: mhko
manager: pablocas
editor: 
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/07/2016
ms.author: nateko
ms.openlocfilehash: 2695139d2b298fa2e7c1814715fdf96729f594ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="synonyms-in-azure-search-preview"></a>Sinônimos no Azure Search (versão prévia)

Sinônimos nos mecanismos de pesquisa associar termos equivalentes que implicitamente expandem o escopo da saudação de uma consulta, sem ter tooactually fornecem os termos de saudação do usuário hello. Por exemplo, termo de determinado hello "dog" e associações de sinônimo de "canino" e "filhote de cachorro", todos os documentos que contenham "dog", "canino" ou "filhote de cachorro" corresponderá no escopo de saudação de consulta de saudação.

No Azure Search, a expansão do sinônimo é feita no momento da consulta. Você pode adicionar sinônimo mapas tooa serviço sem operações de tooexisting de interrupção. Você pode adicionar uma **synonymMaps** definição de campo propriedade tooa sem toorebuild Olá índice. Consulte [Atualizar Índice](https://docs.microsoft.com/rest/api/searchservice/update-index) para obter mais informações.

## <a name="feature-availability"></a>Disponibilidade de recursos

sinônimos Olá recurso está atualmente em visualização e somente tem suporte no hello versão de api de visualização mais recente (api-version = 2016-09-01-Preview). Não há suporte do portal do Azure no momento. Como Olá API versão for especificada na solicitação Olá, é possível toocombine disponibilidade geral (GA) e APIs de visualização no hello mesmo aplicativo. No entanto, as APIs de versão prévia não estão no SLA e os recursos podem mudar, portanto, não recomendamos usá-las em aplicativos de produção.

## <a name="how-toouse-synonyms-in-azure-search"></a>Como a pesquisa de sinônimos toouse no Azure

Na pesquisa do Azure, suporte de sinônimo baseia-se em mapas que você define e carregar o serviço tooyour de sinônimo. Esses mapas constituem um recurso independente (como índices ou fontes de dados) e podem ser usados por qualquer campo pesquisável em um índice do serviço de pesquisa.

Mapas de sinônimo e índices são mantidos de maneira independente. Depois de definir um mapa de sinônimo e carregue-o serviço de tooyour, você pode habilitar o recurso de sinônimo de saudação em um campo, adicionando uma nova propriedade chamada **synonymMaps** na definição de campo hello. Criar, atualizar e excluir que um mapa de sinônimo é sempre uma operação do documento inteiro, que significa que você não pode criar, atualizar ou excluir partes de mapa de sinônimo Olá incrementalmente. Até mesmo uma única entrada a atualização requer um recarregamento.

A incorporação de sinônimos ao seu aplicativo de pesquisa é um processo de duas etapas:

1.  Adicione um serviço de pesquisa do sinônimo mapa tooyour por meio de saudação APIs abaixo.  

2.  Configure um campo pesquisável toouse Olá sinônimo mapa na definição de índice de saudação.

### <a name="synonymmaps-resource-apis"></a>APIs do recurso SynonymMaps

#### <a name="add-or-update-a-synonym-map-under-your-service-using-post-or-put"></a>Adicione ou atualize um mapa de sinônimos em seu serviço, usando POST ou PUT.

Mapas de sinônimo são carregados toohello serviço via POST ou PUT. Cada regra deve ser delimitada por Olá caractere de nova linha ('\n'). Você pode definir too5, 000 regras por mapa de sinônimo em um serviço gratuito e 10.000 regras em todos os outros SKUs. Cada regra pode ter até too20 expansões.

Nesta visualização, mapas de sinônimo devem estar no formato de Apache Solr de saudação que é explicado abaixo. Se você tiver um dicionário de sinônimo existente em um formato diferente e quiser toouse-lo diretamente, informe-em [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

Você pode criar um novo mapa de sinônimo usando HTTP POST, como no exemplo a seguir de saudação:

    POST https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "name":"mysynonymmap",
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

Como alternativa, você pode usar PUT e especificar o nome do mapa de sinônimo Olá em Olá URI. Se o mapa de sinônimo Olá não existir, ele será criado.

    PUT https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

    {  
       "format":"solr",
       "synonyms": "
          USA, United States, United States of America\n
          Washington, Wash., WA => WA\n"
    }

##### <a name="apache-solr-synonym-format"></a>Formato de sinônimo Apache Solr

formato de Solr Olá dá suporte aos mapeamentos de sinônimo equivalente e explícitas. As regras de mapeamento aderem a especificação de filtro de sinônimo toohello código-fonte aberto do Apache Solr, descritas neste documento: [SynonymFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymFilter). Abaixo está um exemplo de regra de sinônimos equivalentes.
```
              USA, United States, United States of America
```

Com a regra de saudação acima, um consulta de pesquisa "EUA" expandirá muito "EUA" ou "EUA" ou "Estados Unidos da América".

Mapeamento explícito é indicado por uma seta "=>". Quando especificado, uma sequência de prazo de uma consulta de pesquisa que corresponda a saudação esquerda de "= >" será substituído pelo alternativas Olá no lado direito hello. Dada a regra de saudação abaixo, consultas de pesquisa "Washington", "Washington." ou "WA" será todos regravado muito "WA". Mapeamento explícito aplica-se em direção de saudação especificada e não regravar consulta hello "WA" muito "Washington" neste caso.
```
              Washington, Wash., WA => WA
```

#### <a name="list-synonym-maps-under-your-service"></a>Liste os mapas de sinônimos em seu serviço.

    GET https://[servicename].search.windows.net/synonymmaps?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="get-a-synonym-map-under-your-service"></a>Obtenha um mapa de sinônimos em seu serviço.

    GET https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

#### <a name="delete-a-synonyms-map-under-your-service"></a>Exclua um mapa de sinônimos em seu serviço.

    DELETE https://[servicename].search.windows.net/synonymmaps/mysynonymmap?api-version=2016-09-01-Preview
    api-key: [admin key]

### <a name="configure-a-searchable-field-toouse-hello-synonym-map-in-hello-index-definition"></a>Configure um campo pesquisável toouse Olá sinônimo mapa na definição de índice de saudação.

Uma nova propriedade de campo **synonymMaps** pode ser usado toospecify toouse de mapa um sinônimo para um campo pesquisável. Mapas de sinônimo são recursos de nível de serviço e podem ser referenciados por qualquer campo de um índice no serviço de saudação.

    POST https://[servicename].search.windows.net/indexes?api-version=2016-09-01-Preview
    api-key: [admin key]

    {
       "name":"myindex",
       "fields":[
          {
             "name":"id",
             "type":"Edm.String",
             "key":true
          },
          {
             "name":"name",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"en.lucene",
             "synonymMaps":[
                "mysynonymmap"
             ]
          },
          {
             "name":"name_jp",
             "type":"Edm.String",
             "searchable":true,
             "analyzer":"ja.microsoft",
             "synonymMaps":[
                "japanesesynonymmap"
             ]
          }
       ]
    }

**synonymMaps** podem ser especificados para campos de pesquisa de tipo de saudação 'EDM. String' ou 'Collection'.

> [!NOTE]
> Nesta versão prévia, só pode haver um mapa de sinônimos por campo. Se você quiser toouse vários mapas de sinônimo, informe-em [UserVoice](https://feedback.azure.com/forums/263029-azure-search).

## <a name="impact-of-synonyms-on-other-search-features"></a>Impacto de sinônimos em outros recursos de pesquisa

recurso de sinônimos Olá reconfigura a consulta original Olá com sinônimos com hello operador OR. Por esse motivo, realce de ocorrências e perfis de pontuação tratam termo original hello e sinônimos como equivalentes.

Recurso de sinônimo se aplica a consultas de toosearch e não se aplica a toofilters ou facetas. Da mesma forma, as sugestões são baseadas apenas no termo original da saudação; correspondências de sinônimo não apareceu na resposta de saudação.

Expansões de sinônimo não se aplicam a termos de pesquisa toowildcard; prefixo, difuso e os termos de regex não são expandidas.

## <a name="tips-for-building-a-synonym-map"></a>Dicas para criação de um mapa de sinônimos

- Um mapa de sinônimos conciso e bem projetado é mais eficiente do que uma lista de possíveis correspondências. Dicionários excessivamente grandes ou complexos levar mais tempo tooparse e afetam a latência da consulta Olá se consulta Olá expande toomany sinônimos. Em vez de estimativa na qual os termos podem ser usados, você pode obter os termos de saudação real por meio de um [relatório de análise de tráfego de pesquisa](search-traffic-analytics.md).

- Como um preliminar e a validação exercício, habilitar e, em seguida, use esse relatório tooprecisely determinar quais termos se beneficiar de uma correspondência de sinônimo e continue toouse como validação que o mapa de sinônimo está produzindo um resultado melhor. No relatório de saudação predefinido, Olá blocos "consultas de pesquisa mais comuns" e "consultas de pesquisa de resultado de Zero" fornecerá Olá informações necessárias.

- Você pode criar vários mapas de sinônimos para o aplicativo de pesquisa (por exemplo, por idioma, se seu aplicativo dá suporte a uma base de clientes com vários idiomas). Atualmente, um campo só pode usar um deles. Atualize a propriedade synonymMaps de um campo a qualquer momento.

## <a name="next-steps"></a>Próximas etapas

- Se você tiver um índice existente em um ambiente de desenvolvimento (não seja de produção), fazer experiências com um pequeno dicionário toosee como adição de saudação de sinônimos altera Olá experiência de pesquisa, incluindo o impacto em perfis de pontuação, ocorrências realce e sugestões.

- [Habilitar análise de tráfego de pesquisa](search-traffic-analytics.md) e use Olá predefinidos toolearn quais termos são usados mais e quais os retorno Olá zero documentos de relatório do Power BI. Armado com essas informações, revise tooinclude sinônimos dicionário Olá improdutivos consultas que devem ser Resolvendo toodocuments no índice.
