---
title: "aaaAzure vários idiomas de pesquisa | Microsoft Docs"
description: "A Pesquisa do Azure dá suporte a 56 idiomas, aproveitando os analisadores de linguagem da Lucene e a tecnologia Processamento de Linguagem Natural da Microsoft."
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a>Crie um índice para documentos em vários idiomas na Pesquisa do Azure
> [!div class="op_single_selector"]
>
> * [Portal](search-language-support.md)
> * [REST](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [.NET](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

Unleashing power Olá de analisadores de idioma é tão fácil quanto uma propriedade de configuração em um campo de pesquisa na definição de índice de saudação. Agora você pode executar esta etapa no portal de saudação.

Abaixo estão capturas de tela de saudação folhas de Portal do Azure para pesquisa do Azure que permitem que os usuários toodefine um esquema de índice. Desta folha, os usuários podem criar todos os campos de saudação e defina a propriedade de analisador de saudação para cada um deles.

> [!IMPORTANT]
> Somente você pode definir um analisador de idioma durante a definição de campo, como em quando criar um novo índice de saudação de plano de fundo para cima ou ao adicionar um novo índice de campo tooan existente. Verifique se que você especificar completamente todos os atributos, incluindo analyzer hello, ao criar o campo de saudação. Você não ser capaz de tooedit atributos hello ou altere o tipo de analisador de hello quando você salvar as alterações.
>
>

## <a name="define-a-new-field-definition"></a>Definir uma nova definição de campo
1. Entrar toohello [portal do Azure](https://portal.azure.com) e abra Olá blade de serviço do seu serviço de pesquisa.
2. Clique em **Adicionar índice** no comando Olá barra na parte superior de saudação do hello serviço painel toostart um novo índice, ou abra um tooset de índice existente em novos campos que você está adicionando um analisador de índice existente tooan.
3. folha de campos de saudação for exibida, fornecendo opções para definir o esquema de saudação do índice hello, incluindo Olá analisador guia usado para escolher um analisador de linguagem.
4. Nos campos, inicie uma definição de campo fornecendo um nome, escolhendo o tipo de dados de saudação e a configuração atributos toomark Olá campo como texto completo pesquisável, recuperáveis nos resultados da pesquisa, pode ser usados em estruturas de navegação de faceta, classificável e assim por diante.
5. Antes de avançarmos toohello próximo campo, abra Olá **analisador** guia.

![][1]
*tooselect um analisador, clique em Guia do analisador Olá na folha de campos de saudação*

## <a name="choose-an-analyzer"></a>Escolha um analisador
1. Role o campo de saudação toofind que você está definindo.
2. Se você ainda não marcado como campo hello como pesquisa, clique em Olá caixa de seleção agora toomark como **pesquisável**.
3. Clique em Olá analisador área toodisplay Olá lista de analisadores disponíveis.
4. Escolha o analisador Olá toouse desejado.

![][2]
*Selecione um dos analisadores de saudação com suporte para cada campo*

Por padrão, todos os campos pesquisáveis usam Olá [analisador padrão Lucene](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) que é independente do idioma. lista completa de saudação de tooview de analisadores de suporte, consulte [suporte de idioma na pesquisa do Azure](https://msdn.microsoft.com/library/azure/dn879793.aspx).

Analisador de linguagem Olá selecionada para um campo, ele será usado com cada solicitação de indexação e pesquisa para esse campo. Quando uma consulta é feita em vários campos usando analisadores de diferentes, consulta hello será processada independentemente por analisadores de saudação à direita de cada campo.

Muitos aplicativos web e móveis servem os usuários em todo o mundo hello usando diferentes idiomas. É possível toodefine um índice para um cenário de como isso criando um campo para cada idioma com suporte.

![][3]
*Definição de índice com um campo de descrição para cada idioma com suporte*

Se o idioma de saudação do agente Olá emitindo uma consulta for conhecido, uma solicitação de pesquisa pode ser campo específico do escopo tooa usando Olá **searchFields** parâmetro de consulta. Olá consulta a seguir será emitida somente em relação a descrição de saudação em polonês:

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

Você pode consultar o índice do portal de saudação usando **pesquisar no Explorador de** toopaste em uma toohello semelhante de consulta mostrada acima. Gerenciador de pesquisa está disponível na barra de comandos de saudação na folha de serviço hello. Consulte [consultar seu índice de pesquisa do Azure no portal de saudação](search-explorer.md) para obter detalhes.

Às vezes, hello idioma do agente Olá emitindo uma consulta não for conhecida, no qual caso Olá consulta pode ser emitida em relação a todos os campos simultaneamente. Se necessário, a preferência de resultados em um determinado idioma pode ser definida usando os [perfis de pontuação](https://msdn.microsoft.com/library/azure/dn798928.aspx). O exemplo hello abaixo, correspondências encontradas na descrição de saudação em inglês serão totalizadas toomatches relativo mais alto em polonês e francês:

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

Se você for um desenvolvedor do .NET, observe que você pode configurar os analisadores de idioma usando Olá [SDK .NET da pesquisa do Azure](http://www.nuget.org/packages/Microsoft.Azure.Search). versão mais recente de saudação inclui suporte para analisadores de idioma de Microsoft hello também.

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
