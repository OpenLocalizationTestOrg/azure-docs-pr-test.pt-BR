---
title: "aaaWhat é a pesquisa do Azure | Microsoft Docs"
description: "O Azure Search é um serviço de pesquisa em nuvem hospedado totalmente gerenciado. Saiba mais nesta visão geral do recurso."
services: search
manager: jhubbard
author: ashmaka
documentationcenter: 
ms.assetid: 50bed849-b716-4cc9-bbbc-b5b34e2c6153
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/26/2017
ms.author: ashmaka
ms.openlocfilehash: b38a7e93a7f0e0d5f8a3779858032271b3883778
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-search"></a>O que é o Azure Search?
O Azure Search é uma solução de pesquisa como serviço na nuvem que oferece aos desenvolvedores APIs e ferramentas para adicionar uma experiência de pesquisa avançada aos dados em aplicativos Web, móveis e empresariais.

A funcionalidade é exposta por meio de um simples [API REST](/rest/api/searchservice/) ou [.NET SDK](search-howto-dotnet-sdk.md) que mascara a complexidade inerente Olá da tecnologia de pesquisa. Adição tooAPIs, Olá portal do Azure fornece suporte de protótipos e administração. A infraestrutura e a disponibilidade são gerenciadas pela Microsoft.

<a name="feature-drilldown"></a>

## <a name="feature-summary"></a>Resumo de recursos

| Categoria | Recursos |
|----------|----------|
|Análise de texto e pesquisa de texto completo | [**Pesquisa de texto completo**](search-lucene-query-architecture.md) é um caso de uso primário para a maioria dos aplicativos baseados em pesquisa. As consultas podem ser formuladas usando uma sintaxe com suporte: <br/><br/>[**Sintaxe de consulta simples**](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search), que oferece operadores lógicos, operadores de pesquisa de frase, operadores de sufixo e operadores de precedência.<br/><br/>A [**sintaxe de consulta Lucene**](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search) oferece todo o suporte de consulta simples, além de pesquisa difusa, pesquisa por proximidade, aumento de termo e expressões regulares.| 
| Integração de dados | Os índices do Azure Search aceitam dados de qualquer fonte, desde que eles sejam enviados como uma estrutura de dados JSON. <br/><br/> Opcionalmente, para fontes de dados com suporte no Azure, você pode usar [ **indexadores** ](search-indexer-overview.md) tooautomatically rastreamento [banco de dados do SQL Azure](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md), [banco de dados do Azure Cosmos](search-howto-index-documentdb.md), ou [armazenamento de BLOBs do Azure](search-howto-indexing-azure-blob-storage.md) toosync o índice de pesquisa do conteúdo com o repositório de dados primário. Os indexadores de Blob do Azure podem executar a *decodificação de documentos* para [indexar os principais formatos de arquivo](search-howto-indexing-azure-blob-storage.md), incluindo documentos do Microsoft Office, PDF e HTML. |
| Análise do Search | Os [**analisadores léxicos personalizados**](https://docs.microsoft.com/rest/api/searchservice/custom-analyzers-in-azure-search) estão disponíveis para consultas de pesquisa complexas usando a correspondência fonética e expressões regulares. |
| Suporte ao idioma | [**Analisadores de idioma** ](https://docs.microsoft.com/rest/api/searchservice/language-support) Lucene, bem como a Microsoft do idioma natural de processadores disponíveis em linguística do 56 diferentes idiomas toointelligently identificador específico do idioma incluindo verbais, sexo, plural irregular substantivos (por exemplo, ' mouse' versus 'mice'), word eliminação de composição, quebra de palavras (para idiomas sem espaços) e muito mais. |
| Pesquisa geográfica | O Azure Search com inteligência processa, filtra e exibe as localizações geográficas. Ele permite que os usuários tooexplore dados com base na proximidade de saudação de um local físico do tooa de resultados de pesquisa. [Assista a este vídeo](https://channel9.msdn.com/Shows/Data-Exposed/Azure-Search-and-Geospatial-Data) ou [examinar este exemplo](https://github.com/Azure-Samples/search-dotnet-asp-net-mvc-jobs) toolearn mais. |
| Recursos da experiência do usuário | [**Sugestões de pesquisa**](https://docs.microsoft.com/rest/api/searchservice/suggesters) podem ser habilitadas para consultas de preenchimento automático em uma barra de pesquisa. Documentos reais no índice são sugeridos conforme os usuários inserem a entrada de pesquisa parcial. <br/><br/>A [**navegação facetada**](https://docs.microsoft.com/azure/search/search-faceted-navigation) é habilitada por meio de um único parâmetro de consulta. A pesquisa do Azure retorna uma estrutura de navegação facetada que você pode usar como código Olá atrás de uma lista de categorias para filtragem direcionado automaticamente (por exemplo, toofilter itens de catálogo por faixa de preços ou marca). <br/><br/> [**Filtros** ](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search) pode ser a navegação facetada tooincorporate usado na interface do usuário do aplicativo, aprimorar formulação de consulta e filtro com base em critérios de usuário ou desenvolvedor especificado. Crie filtros usando a sintaxe do OData hello.<br/><br/> [**O realce de ocorrências** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) aplica-se de forma visual atting tooa correspondência de palavra-chave nos resultados da pesquisa. Você pode escolher quais campos retornam os trechos de código destacados.<br/><br/>[**Classificação** ](https://docs.microsoft.com/rest/api/searchservice/Search-Documents) é oferecido para vários campos por meio do esquema de índice hello e alternado, em seguida, no momento da consulta com um parâmetro de pesquisa único.<br/><br/> [**Paginação** ](search-pagination-page-layout.md) e os resultados da pesquisa de limitação é simples com controle de saudação bem ajustada pesquisa do Azure oferece sobre os resultados da pesquisa.  
| Relevância | A [**pontuação simples**](/rest/api/searchservice/add-scoring-profiles-to-a-search-index) é o principal benefício do Azure Search. Perfis de pontuação são de relevância de toomodel usado como uma função de valores em Olá documentos próprios. Por exemplo, você talvez queira produtos mais recentes ou com desconto produtos tooappear superior nos resultados da pesquisa hello. Você também pode criar perfis de pontuação usando marcas de pontuação personalizadas com base nas preferências de pesquisa do cliente que você controlou e armazenou separadamente. |
| Monitoramento e emissão de relatórios | [**Análise de tráfego de pesquisa** ](search-traffic-analytics.md) são coletados e analisados toounlock informações de que os usuários estão digitando na caixa de pesquisa de saudação. <br/><br/>As métricas nas consultas por segundo, latência e limitação são capturadas e informadas nas páginas do portal sem nenhuma configuração adicional necessária. Você também pode monitorar facilmente o índice e as contagens de documentos para poder ajustar a capacidade quando necessário. Para obter mais informações, consulte [Administração do serviço](search-manage.md) |
| Ferramentas para criação de protótipos e inspeção | No portal de saudação, você pode usar o hello [ **Assistente de importação de dados** ](search-import-data-portal.md) tooconfigure indexadores, toostand designer se um índice, de índice e [ **pesquisar no Explorador de** ](search-explorer.md) tootest consultas e refinar os perfis de pontuação. Você também pode abrir qualquer índice tooview seu esquema. |
| Infraestrutura | Olá **plataforma altamente disponível** garante uma experiência de serviço de pesquisa extremamente confiável. Quando dimensionada corretamente, o [Azure Search oferece um SLA de 99,9%](https://azure.microsoft.com/support/legal/sla/search/v1_0/).<br/><br/> **Totalmente gerenciado e escalonável** como uma solução de ponta a ponta, o Azure Search não exige nenhum gerenciamento de infraestrutura. Seu serviço pode ser adaptada tooyour necessidades dimensionando duas dimensões toohandle mais armazenamento de documentos, superior cargas de consulta ou ambos.

## <a name="how-it-works"></a>Como ele funciona
### <a name="step-1-provision-service"></a>Etapa 1: Provisionar serviço
Você pode criar um serviço de pesquisa do Azure no hello [portal do Azure](https://portal.azure.com/) ou por meio de saudação [API de gerenciamento de recursos do Azure](/rest/api/searchmanagement/). Você pode escolher qualquer serviço gratuito Olá compartilhado com outros assinantes, ou um [paga camada](https://azure.microsoft.com/pricing/details/search/) que dedica recursos utilizados apenas pelo seu serviço. Para as camadas pagas, você pode dimensionar um serviço em duas dimensões: 

- Adicione réplicas toogrow que carrega sua consulta pesada de toohandle de capacidade.   
- Adicione partições toogrow armazenamento para documentos mais. 

Ao manipular o armazenamento de documentos e a taxa de transferência de consultas separadamente, é possível calibrar a alocação de recursos de acordo com os requisitos de produção.

### <a name="step-2-create-index"></a>Etapa 2: Criar índice
Antes de carregar o conteúdo pesquisável, primeiro é necessário definir um índice do Azure Search. Um índice é como uma tabela de banco de dados que contém os dados e pode aceitar consultas de pesquisa. Definir Olá índice esquema toomap tooreflect Olá estrutura dos documentos Olá desejar toosearch, toofields semelhante em um banco de dados.

Um esquema pode ser criado em hello Azure Olá portal ou programaticamente usando [.NET SDK](search-howto-dotnet-sdk.md) ou [API REST](/rest/api/searchservice/).

### <a name="step-3-index-data"></a>Etapa 3: Indexar dados
Depois de definir um índice, você está conteúdo tooupload pronto. É possível usar um modelo push ou pull.

modelo de pull Olá recupera dados de fontes de dados externas. Há suporte para ele por meio de *indexadores* que simplificam e automatizam aspectos da ingestão de dados, como se conectar a dados, lê-los ou serializá-los. Os [indexadores](/rest/api/searchservice/Indexer-operations) estão disponíveis para o Azure Cosmos DB, Banco de Dados SQL do Azure, Armazenamento de Blobs do Azure e SQL Server hospedado em uma VM do Azure. É possível configurar um indexador para uma atualização de dados sob demanda ou agendada.

modelo de push Olá é fornecido por meio de saudação SDK ou APIs REST, usado para enviar o índice de tooan documentos atualizados. Você pode enviar dados de praticamente qualquer conjunto de dados usando o formato JSON de saudação. Consulte [adicionar, atualizar ou excluir documentos](/rest/api/searchservice/addupdate-or-delete-documents) ou [como toouse Olá .NET SDK)](search-howto-dotnet-sdk.md) para obter orientação sobre o carregamento de dados.

### <a name="step-4-search"></a>Etapa 4: Pesquisar
Depois de preencher um índice, você pode [emitir consultas de pesquisa](/rest/api/searchservice/Search-Documents) solicitações de ponto de extremidade do serviço tooyour usando HTTP simple com API REST ou hello .NET SDK.

## <a name="how-it-compares"></a>Como ele se compara

Os clientes costumam perguntar sobre as semelhanças da [pesquisa de texto completo do Azure Search](search-lucene-query-architecture.md) com a [pesquisa de texto completo](https://en.wikipedia.org/wiki/Full_text_search) de seus produtos de banco de dados. Nossa resposta é que os recursos de idioma de pesquisa do Azure são mais avançada e mais flexível, com suporte para consultas Lucene, analisadores de idioma do Lucene e a Microsoft, analisadores personalizados para fonéticas ou outras entradas especializadas e dados de toomerge de capacidade de saudação do várias fontes no índice de pesquisa de saudação. 

Outro ponto de inflexão é uma solução de pesquisa endereços experiência de pesquisa inteira hello. Por exemplo, você poderá desejar ter uma pontuação personalizada de resultados, navegação facetada para a filtragem autodirecionada, realce de ocorrências e sugestões de consulta de digitação antecipada. 

As ferramentas para o monitoramento e entendimento das atividades de consulta também podem influenciar uma decisão de solução de pesquisa. Por exemplo, o Azure Search dá suporte à [análise de tráfego de pesquisa](search-traffic-analytics.md) para métricas na taxa de clickthrough, nas principais pesquisas, nas pesquisas sem cliques e assim por diante. Em produtos onde a pesquisa é um complemento, é improvável toofind esses recursos.

Outra consideração é a utilização de recursos. Em geral, a pesquisa em idioma natural é computacionalmente intensiva. Alguns dos nossos clientes descarregados tooAzure operações de pesquisa pesquisa como recursos de máquina de toopreserve um modo de processamento de transações. Externalização de pesquisa, você pode facilmente ajustar escala toomatch consulta volume.

Depois de decidir toogo com a pesquisa dedicada, sua próxima decisão é entre um servidor local ou de um serviço de nuvem. Um serviço de nuvem é a escolha certa Olá se você desejar um [solução turnkey com sobrecarga mínima e a manutenção e a escala ajustável](#cloud-service-advantage).

No paradigma da nuvem hello, vários provedores oferecem recursos de comparáveis da linha de base, com a pesquisa de texto completo e pesquisa geográfica Olá capacidade toohandle um determinado nível de ambiguidade em entradas de pesquisa. Normalmente, ele tem um [recurso especializado](#feature-drilldown), ou facilidade hello e simplicidade geral de gerenciamento que determina a saudação melhor ajuste, ferramentas e APIs.

Entre os provedores de nuvem, o Azure Search é mais forte para cargas de trabalho de pesquisa de texto completo em relação aos repositórios de conteúdo e bancos de dados do Azure, para aplicativos que se baseiam principalmente na pesquisa para recuperação de informações e navegação de conteúdo. As principais vantagens incluem:

+ Integração de dados do Azure (rastreadores) na camada de indexação Olá
+ Portal do Azure para o gerenciamento central
+ Escala do Azure, confiabilidade e disponibilidade superior
+ Análise linguística e personalizada, com analisadores para a pesquisa sólida de texto completo em 56 idiomas
+ [Principais recursos comuns aplicativos centrados em toosearch](#feature-drilldown): classificação, facetas, sugestões, sinônimos, pesquisa geográfica e muito mais.

> [!Note]
> toobe fontes de dados criptografado, o Azure não são totalmente suportados, mas dependem de uma metodologia de push com uso mais intensivo de código em vez de indexadores. Usar nossas APIs, você pode direcionar qualquer índice de pesquisa do Azure JSON documento coleção tooan.

Entre nossos clientes, essas tooleverage capaz de hello mais ampla variedade de recursos na pesquisa do Azure incluem catálogos online, programas de linha de negócios e aplicativos de descoberta do documento.

## <a name="rest-api--net-sdk"></a>API REST | SDK .Net

Embora muitas tarefas podem ser executadas no portal de hello, pesquisa do Azure destina-se para desenvolvedores que querem toointegrate a funcionalidade de pesquisa em aplicativos existentes. Olá, interfaces de programação a seguir está disponível.

|Plataforma |Descrição |
|-----|------------|
|[REST](/rest/api/searchservice/) | Comandos HTTP suportados por qualquer plataforma de programação e linguagem, incluindo Xamarin, Java e JavaScript|
|[SDK .NET](search-howto-dotnet-sdk.md) | Wrapper de .NET para API REST de saudação oferece eficiente de codificação em c# e outras linguagens de código gerenciado que visam Olá do .NET Framework |

## <a name="free-trial"></a>Avaliação gratuita
Os assinantes do Azure podem [provisionar um serviço na camada gratuita Olá](search-create-service-portal.md).

Se você não for um assinante, poderá [abrir uma conta do Azure gratuitamente](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F). Você obtém créditos para experimentar os serviços pagos do Azure. Depois que eles são usados, você pode manter a conta hello e usar [liberar os serviços do Azure](https://azure.microsoft.com/free/). Seu cartão de crédito nunca é cobrado a menos que você explicitamente alterar suas configurações e pergunte toobe cobrado.

Se preferir, você pode [ativar benefícios para assinantes do MSDN](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A261C142F): todos os meses, sua assinatura do MSDN concede créditos que podem ser usados para serviços pagos do Azure. 

## <a name="how-tooget-started"></a>A inicialização de tooget

1. Criar um serviço no hello [grátis](search-create-service-portal.md).

2. Percorrer uma ou mais das Olá tutoriais a seguir. 

  + [Como toouse Olá .NET SDK](search-howto-dotnet-sdk.md) demonstra Olá principal etapas no código gerenciado.  
  + [Introdução à API REST de saudação](https://github.com/Azure-Samples/search-rest-api-getting-started) mostra Olá mesmo etapas usando Olá API REST.  
  + [Criar seu primeiro índice no portal de saudação](search-get-started-portal.md) demonstra os recursos internos de indexação e protótipo do portal hello.   

Mecanismos de pesquisa são drivers de saudação comuns de recuperação de informações nos aplicativos móveis, Web hello e repositórios de dados corporativos. A pesquisa do Azure fornece ferramentas para criar um toothose semelhante de experiência de pesquisa em grandes sites da web comercial.

Neste vídeo de 9 minutos com o gerente de programa Liam Cavanagh, saiba como a integração de um mecanismo de pesquisa pode trazer vantagens para seu aplicativo. As demonstrações breves abrangem os principais recursos do Azure Search e a aparência de um fluxo de trabalho típico. 

>[!VIDEO https://channel9.msdn.com/Events/Connect/2016/138/player]
 
+ O vídeo de 0-3 minutos aborda os principais recursos e casos de uso.
+ O vídeo de 3-4 minutos aborda o provisionamento de serviços. 
+ 4 a 6 minutos abrange importar dados Assistente usado toocreate um índice usando o conjunto de dados do hello imóveis internos.
+ O vídeo de 6-9 minutos aborda o Gerenciador de Pesquisa e várias consultas.


