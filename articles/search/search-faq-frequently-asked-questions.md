---
title: aaaFrequently perguntas frequentes (FAQ) sobre a pesquisa do Azure | Microsoft Docs
description: "Obter respostas a perguntas toocommon sobre o serviço de pesquisa do Microsoft Azure"
services: search
author: HeidiSteen
manager: jhubbard
ms.service: search
ms.technology: search
ms.topic: article
ms.date: 08/03/2017
ms.author: heidist
ms.openlocfilehash: 2c573750600d80585b746bfce20d6c0f8df5a262
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-search---frequently-asked-questions-faq"></a>Azure Search - FAQ (perguntas frequentes)
 
 Encontre respostas toocommonly perguntas frequentes sobre conceitos, cenários e código relacionam tooAzure pesquisa.

## <a name="platform"></a>Plataforma

### <a name="how-is-azure-search-different-from-full-text-search-in-my-dbms"></a>Como o Azure Search é diferente da pesquisa de texto completo no meu DBMS?

O Azure Search dá suporte a várias fontes de dados, a [análise linguística para vários idiomas](https://docs.microsoft.com/rest/api/searchservice/language-support), a [análises personalizadas para entradas de dados interessantes e incomuns](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search), a controles de classificação por meio de pesquisa [perfis de pontuação](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index)e a recursos de experiência do usuário, como digitação antecipada, realce de ocorrências e navegação facetada. Ele também inclui outros recursos, como sinônimos e sintaxe de consulta avançada, mas esses geralmente não são recursos diferenciados.

### <a name="what-is-hello-difference-between-azure-search-and-elasticsearch"></a>Qual é a diferença Olá entre a pesquisa do Azure e Elasticsearch?

Ao comparar as tecnologias de pesquisa, os clientes frequentemente solicitam informações específicas sobre como o Azure Search compara com o Elasticsearch. Os clientes que optarem pesquisa do Azure sobre Elasticsearch para pesquisa de seu projetos de aplicativo normalmente fizerem-lo porque fizemos uma chave tarefa mais fácil ou precisam de integração interna de saudação com outras tecnologias da Microsoft:

+ O Azure Search é um serviço de nuvem totalmente gerenciado com SLA (contratos de nível de serviço) de 99,9%, quando provisionados com redundância suficiente (2 réplicas para acesso de leitura, 3 réplicas para leitura e gravação).
+ Os [Processadores de linguagem natural](https://docs.microsoft.com/rest/api/searchservice/language-support) da Microsoft oferecem análise linguística de ponta.  
+ Os [Indexadores do Azure Search](search-indexer-overview.md) podem rastrear uma variedade de fontes de dados do Azure para indexação inicial e incremental.
+ Se você precisar de resposta rápida toofluctuations na consulta ou volumes de indexação, você poderá usar [controles deslizantes](search-manage.md#scale-up-or-down) em Olá portal do Azure, ou executar um [script do PowerShell](search-manage-powershell.md), ignorando o gerenciamento de fragmento diretamente.  
+ [Pontuação e recursos de ajuste](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) fornecem Olá significa para influenciar as pontuações de classificação de pesquisa além do qual o mecanismo de pesquisa Olá sozinho pode fornecer. 

### <a name="can-i-pause-azure-search-service-and-stop-billing"></a>Posso pausar o serviço Azure Search e interromper a cobrança?

Não é possível pausar o serviço de saudação. Recursos de computação e armazenamento são alocados para seu uso exclusivo ao serviço de saudação é criado. Não é possível toorelease e recuperar os recursos sob demanda. 

## <a name="indexing-operations"></a>Operações de indexação

### <a name="backup-and-restore-or-download-and-move-indexes-or-index-snapshots"></a>Índices de backup e restauração (ou download e mover) ou instantâneos de índice?

Embora você possa [obter uma definição de índice](https://docs.microsoft.com/rest/api/searchservice/get-index) a qualquer momento, não há nenhum extração de índice, um instantâneo ou um recurso de restauração de backup para baixar um *preenchido* índice em execução no sistema local do hello nuvem tooa, ou movendo-o serviço de pesquisa do Azure tooanother. 

Os índices são criados e preenchidos a partir de código que você grava e executar apenas em pesquisa do Azure na nuvem de saudação. Normalmente, os clientes que desejam toomove um serviço de índice de tooanother fazê-lo editando o seu código toouse um novo ponto de extremidade e, em seguida, execute novamente a indexação. Se você desejar Olá capacidade tootake um instantâneo ou um índice de backup, emitir um voto [User Voice](https://feedback.azure.com/forums/263029-azure-search/suggestions/8021610-backup-snapshot-of-index).

### <a name="can-i-index-from-sql-database-replicas-applies-tooazure-sql-database-indexershttpsdocsmicrosoftcomazuresearchsearch-howto-connecting-azure-sql-database-to-azure-search-using-indexers"></a>Pode indexar das réplicas de banco de dados SQL (aplica-se também[indexadores de banco de dados do Azure SQL](https://docs.microsoft.com/azure/search/search-howto-connecting-azure-sql-database-to-azure-search-using-indexers))

 Não existem restrições no uso de saudação de réplicas primárias ou secundárias como uma fonte de dados quando estiver criando um índice do zero. No entanto, a atualização de um índice com atualizações incrementais (com base em registros modificados) requer réplica primária hello. Esse requisito vem do Banco de Dados SQL, que garante o controle de alterações somente em réplicas primárias. Se você tentar usar réplicas secundárias para uma carga de trabalho de atualização do índice, não há nenhuma garantia que você obtém todos os dados de saudação.

## <a name="search-operations"></a>Operações de pesquisa

### <a name="can-i-search-across-multiple-indexes"></a>Posso pesquisar em vários índices?

Não, essa operação não tem suporte. A pesquisa é sempre tooa escopo único índice.

### <a name="can-i-restrict-search-corpus-access-by-user-identity"></a>Posso restringir o acesso à pesquisa pela identidade do usuário?

O Azure Search não tem um modelo de segurança baseado em função para o acesso a dados por usuário. A autenticação é a todos os direitos ou somente leitura no nível de serviço de saudação. Alguns clientes implementaram soluções baseadas no parâmetro de pesquisa [ `$filter`](https://docs.microsoft.com/rest/api/searchservice/search-documents), mas isso é, no máximo, uma solução alternativa. Se você quiser esse recurso, vote no [User Voice](https://feedback.azure.com/forums/263029-azure-search/category/86074-security).

### <a name="why-are-there-zero-matches-on-terms-i-know-toobe-valid"></a>Por que há zero correspondências em termos de que saber toobe válido?

caso mais comum de saudação não é saber que cada tipo de consulta oferece suporte a níveis de análise linguística e comportamentos de pesquisa diferente. Pesquisa de texto completo, que é a carga de trabalho predominantes hello, inclui uma fase de análise de linguagem que divide os termos abaixo tooroot formulários. Esse aspecto da análise de consulta converte uma rede mais ampla sobre possíveis correspondências, porque hello editáveis termo corresponde a um número maior de variantes.

Se você invocar [outros tipos de consulta](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) (pesquisa com curinga, pesquisa difusa, pesquisa por proximidade, sugestões, entre outros), não haverá nenhuma análise linguística. Termos são adicionados a árvore de consulta toohello como-é. 

### <a name="why-is-hello-search-rank-a-constant-or-equal-score-of-10-for-every-hit"></a>Por que é uma pontuação igual ou constante de 1.0 para cada ocorrência classificação Olá?

Por padrão, os resultados da pesquisa são classificados com base em Olá [propriedades estatísticas dos termos de correspondência](search-lucene-query-architecture.md#stage-4-scoring)e ordenado toolow alta no conjunto de resultados de saudação. No entanto, alguns tipos (curinga, prefixo, regex) de consulta sempre contribuir uma pontuação constante toohello geral de pontuação de documento. Este comportamento ocorre por design. Pesquisa do Azure impõe uma constante de pontuação tooallow correspondências localizadas por meio de consulta expansão toobe incluído nos resultados de hello, sem afetar a classificação de saudação. 

Por exemplo, suponha que uma entrada de "turnê*" em uma pesquisa com curinga produz correspondências em "turim", "turrão" e "turmalina". Considerando a natureza Olá desses resultados, não é possível inferir tooreasonably quais termos são mais valiosos do que outras pessoas. Por esse motivo, podemos ignorar as frequências dos termos ao pontuar resultados em consultas dos tipos caractere curinga, prefixo e regex. Resultados da pesquisa com base em uma entrada parcial recebem uma constante de pontuação tooavoid tendência para correspondências potencialmente inesperadas.

## <a name="design-patterns"></a>Padrões de design

### <a name="what-is-hello-best-approach-for-implementing-localized-search"></a>O que é a melhor abordagem Olá para implementar pesquisa localizada?

A maioria dos clientes escolher campos dedicados em uma coleção quando se trata de localidades diferentes toosupporting (idiomas) em Olá mesmo índice. Campos específicos de localidade tornam possível tooassign um analisador apropriado. Por exemplo, atribuição de campo de tooa do analisador de francês do Microsoft hello contendo cadeias de caracteres franceses. Isso também simplifica a filtragem. Se você souber que uma consulta é iniciada em uma página de fr-fr, você pode limitar o campo de toothis de resultados de pesquisa. Criar um [perfil de pontuação](https://docs.microsoft.com/rest/api/searchservice/add-scoring-profiles-to-a-search-index) toogive Olá campo mais peso relativo.

## <a name="next-steps"></a>Próximas etapas

A sua pergunta é sobre a falta de um recurso ou funcionalidade? Solicitar recurso Olá Olá [User Voice web site](https://feedback.azure.com/forums/263029-azure-search).

## <a name="see-also"></a>Consulte também

 [StackOverflow: Azure Search](https://stackoverflow.com/questions/tagged/azure-search)   
 [Como funciona a pesquisa de texto completo no Azure Search](search-lucene-query-architecture.md)  
 [O que é a Pesquisa do Azure?](search-what-is-azure-search.md)

 