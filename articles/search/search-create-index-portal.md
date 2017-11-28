---
title: "AAA \"criar um índice (portal - pesquisa do Azure) | Microsoft Docs\""
description: "Crie um índice usando Olá Portal do Azure."
services: search
manager: jhubbard
author: heidisteen
documentationcenter: 
ms.assetid: 
ms.service: search
ms.devlang: NA
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 06/20/2017
ms.author: heidist
ms.openlocfilehash: 4c5d663499bf73a8883690aa9482b6ba59d1ddf6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-search-index-using-hello-azure-portal"></a>Criar um índice de pesquisa do Azure usando Olá Portal do Azure
> [!div class="op_single_selector"]
> * [Visão geral](search-what-is-an-index.md)
> * [Portal](search-create-index-portal.md)
> * [.NET](search-create-index-dotnet.md)
> * [REST](search-create-index-rest-api.md)
> 
> 

Use o designer de índice internas de saudação no tooprototype portal do Azure ou criar um [índice de pesquisa](search-what-is-an-index.md) toorun em seu serviço de pesquisa do Azure. 

## <a name="prerequisites"></a>Pré-requisitos

Este artigo pressupõe que você tenha uma [assinatura do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) e um [serviço do Azure Search](search-create-service-portal.md).  

## <a name="find-your-search-service"></a>Encontrar o serviço de pesquisa
1. Entrar toohello página do portal do Azure e examine Olá [pesquisar serviços para sua assinatura](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)
2. Selecione o serviço Azure Search.

## <a name="name-hello-index"></a>Índice de saudação do nome

1. Clique em Olá **Adicionar índice** botão na barra de comandos de saudação na parte superior de saudação da página de saudação.
2. Dê um nome ao seu índice do Azure Search 
   * Comece com uma letra.
   * Use apenas letras minúsculas, dígitos ou traços (“-”).
   * Limitam Olá nome too60 caracteres.

  nome do índice Olá se torna parte da URL de ponto de extremidade de saudação usada em um índice toohello conexões e para enviar solicitações HTTP em Olá API de REST de pesquisa do Azure.

## <a name="define-hello-fields-of-your-index"></a>Definir campos de saudação do índice

Composição de índice inclui um *coleção de campos* que define dados pesquisáveis Olá no índice. Mais especificamente, ele especifica estrutura Olá de documentos que você carregar separadamente. coleção de campos de saudação inclui campos obrigatórios e opcionais, denominado e digitado, com toodetermine de atributos de índice como campo Olá pode ser usado.

1. Em Olá **Add Index** folha, clique em **campos >** tooslide abrir a folha de definição de campo hello. 

2. Aceitar Olá gerado *chave* campo do tipo EDM. Por padrão, o campo de saudação é chamado *id* , mas você pode renomeá-lo como cadeia de caracteres hello satisfaz [as regras de nomenclatura](https://docs.microsoft.com/rest/api/searchservice/Naming-rules). Um campo de chave é obrigatório para cada índice do Azure Search e deve ser uma cadeia de caracteres.

3. Adicione campos toofully especificar você fará o upload de documentos de saudação. Se os documentos consistem em uma *id*, *nome do hotel*, *endereço*, *city*, e *região*, criar um campo correspondente para cada um no índice de saudação. Saudação de revisão [design diretrizes na seção de saudação abaixo](#design) para obter ajuda na definição de atributos.

4. Opcionalmente, adicione campos que são usados internamente em expressões de filtro. No campo Olá possível definir atributos de campos de tooexclude de operações de pesquisa.

5. Quando terminar, clique em **Okey** toosave e crie o índice de saudação.

## <a name="tips-for-adding-fields"></a>Dicas para adicionar campos

Criar um índice no portal de saudação é teclado intensivo. Minimize as etapas seguindo este fluxo de trabalho:

1. Primeiro, crie lista de campos de saudação inserindo nomes e tipos de dados de configuração.

2. Em seguida, usar Olá caixas de seleção na parte superior de saudação do toobulk cada atributo Habilitar configuração Olá para todos os campos e seletivamente desmarque caixas para Olá alguns campos que não exigem a ele. Por exemplo, os campos de cadeia de caracteres normalmente são pesquisáveis. Dessa forma, você pode clicar em **Retrievable** e **pesquisável** tooboth valores retorno Olá Olá campo nos resultados da pesquisa, bem como permitir que a pesquisa de texto completo no campo de saudação. 

<a name="design"></a>
## <a name="design-guidance-for-setting-attributes"></a>Diretrizes de design para configuração de atributos

Embora seja possível adicionar novos campos a qualquer momento, definições de campo existentes são bloqueadas tempo de vida de saudação do índice de saudação. Por esse motivo, os desenvolvedores geralmente usam portal Olá para criação de índices simples, teste ideias ou usando Olá páginas do portal toolook uma configuração. Frequente iteração sobre um design de índice é mais eficiente se você seguir uma abordagem baseada em código para que você pode recriar índice Olá facilmente.

Analisadores e sugestões estão associados a campos antes de índice Olá é salvo. Ser tooclick-se por meio de cada página com guias tooadd idioma analisadores ou sugestões tooyour definição de índice.

Geralmente, os campos de cadeia de caracteres são marcados como **Pesquisáveis** e **Recuperáveis**.

Resultados da pesquisa toonarrow campos usados incluem **Sortable**, **Filterable**, e **Facetable**.

Os atributos de campo determinam como um campo é usado, por exemplo, se ele é usado na pesquisa de texto completo, na navegação facetada, nas operações de classificação e assim por diante. Olá, a tabela a seguir descreve cada atributo.

|Atributo|Descrição|  
|---------------|-----------------|  
|**searchable**|Texto completo pesquisável, assunto toolexical análise como quebra de palavras durante a indexação. Se você definir um valor de tooa campo pesquisável como "dia ensolarado", internamente ele será dividido em Olá tokens individuais "Ensolarado" e "dia". Para obter detalhes, consulte [Como funciona a pesquisa de texto completo](search-lucene-query-architecture.md).|  
|**filterable**|Referenciado nas consultas **$filter**. Campos filtráveis dos tipos `Edm.String` ou `Collection(Edm.String)` não são submetidos à separação de palavras. Portanto, as comparações são apenas para correspondências exatas. Por exemplo, se você definir um campo f muito "dia ensolarado", `$filter=f eq 'sunny'` encontrará nenhuma correspondência, mas `$filter=f eq 'sunny day'` será. |  
|**sortable**|Por padrão Olá sistema classifica os resultados pela pontuação, mas você pode configurar a classificação com base em campos em documentos de saudação. Campos do tipo `Collection(Edm.String)` não podem ser **sortable**. |  
|**facetable**|Normalmente, usado em uma apresentação dos resultados da pesquisa que inclui uma contagem de ocorrências por categoria (por exemplo, hotéis em uma cidade específica). Essa opção não pode ser usada com campos do tipo `Edm.GeographyPoint`. Campos do tipo `Edm.String` que são **filterable**, **sortable** ou **facetable** podem ter um tamanho de, no máximo, 32 quilobytes. Para obter detalhes, consulte [Criar índice (API REST)](https://docs.microsoft.com/rest/api/searchservice/create-index).|  
|**chave**|Identificador exclusivo para documentos no índice de saudação. Exatamente um campo deve ser escolhido como campo de chave hello e ele deve ser do tipo `Edm.String`.|  
|**retrievable**|Determina se o campo Olá pode ser retornado em um resultado de pesquisa. Isso é útil quando você deseja toouse um campo (como *margem de lucro*) como um filtro, classificação ou pontuação mecanismo, mas não não desejar Olá campo toobe toohello visível usuários finais. Esse atributo deve ser `true` for `key` .|  

## <a name="create-hello-hotels-index-used-in-example-api-sections"></a>Criar índice de hotéis Olá usado nas seções de API de exemplo

A documentação da API do Azure Search inclui exemplos de código que apresentam um índice de *hotéis* simples. No hello capturas de tela abaixo, você pode ver a definição de índice hello, incluindo o analisador de idioma francês Olá especificado durante a definição de índice, que você poderá recriá-la como um exercício no portal de saudação.

![](./media/search-create-index-portal/field-definitions.png)

![](./media/search-create-index-portal/set-analyzer.png)

## <a name="next-steps"></a>Próximas etapas

Depois de criar um índice de pesquisa do Azure, você pode mover toohello próxima etapa: [carregar dados pesquisáveis no índice Olá](search-what-is-data-import.md).

Como alternativa, você também poderá examinar os índices mais detalhadamente. Além disso toohello coleção de campos, um índice também especifica analisadores, sugestões, perfis e configurações de CORS de pontuação. Olá portal fornece páginas com guias para definir elementos mais comuns da saudação: campos, analisadores e sugestões. toocreate ou modifique outros elementos, você pode usar o hello API REST ou o SDK do .NET.

## <a name="see-also"></a>Consulte também

 [Como funciona a pesquisa de texto completo](search-lucene-query-architecture.md)  
 [API REST do serviço Search](https://docs.microsoft.com/rest/api/searchservice/) [SDK do .NET](https://docs.microsoft.com/dotnet/api/overview/azure/search?view=azure-dotnet)

