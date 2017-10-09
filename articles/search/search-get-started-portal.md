---
título: aaa "Tutorial: criar seu primeiro índice de pesquisa do Azure no portal de saudação | Descrição de Microsoft Docs": em Olá portal do Azure, use predefinidos toogenerate de dados de exemplo um índice. Explore a pesquisa de texto completo, filtros, facetas, pesquisa difusa, pesquisa geográfica e muito mais.
serviços: Pesquisar documentationcenter: ' autor: manager HeidiSteen: jhubbard editor: ' marcas: portal do azure

MS. AssetID: 21adc351-69bb-4a39-bc59-598c60c8f958 MS. Service: Pesquisar MS. devlang: na Workload: Pesquisar MS. Topic: artigo herói tgt_pltfrm: MS. Date na: 26/06/2017 Author: heidist

---
# <a name="tutorial-create-your-first-azure-search-index-in-hello-portal"></a>Tutorial: Criar seu primeiro índice de pesquisa do Azure no portal de saudação

Em Olá portal do Azure, comece com um tooquickly de conjunto de dados de exemplo predefinidos gerar um índice usando Olá **importar dados** assistente. Explore a pesquisa de texto completo, filtros, facetas, pesquisa difusa e pesquisa geográfica com o **Search Explorer**.  

Esta introdução sem código apresenta dados predefinidos para que você possa escrever consultas interessantes imediatamente. Embora as ferramentas de portal não sejam um bom substituto para o código, elas são úteis para essas tarefas:

+ Aprendizado prático com curva de aprendizagem mínima
+ Crie um protótipo de índice antes de escrever código em **Importar dados**
+ Teste consultas e sintaxe de analisador no **Search Explorer**
+ Exibir um existente publicado tooyour serviço de índice e consultar seus atributos

**Tempo estimado:** cerca de 15 minutos, mas poderá ser maior se houver a necessidade de fazer inscrição na conta ou no serviço. 

Como alternativa, a entender o uso de um [tooprogramming de Introdução com base em código de pesquisa do Azure no .NET](search-howto-dotnet-sdk.md).

## <a name="prerequisites"></a>Pré-requisitos

Este tutorial assume que você tem uma [assinatura do Azure](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F) e [o serviço Azure Search](search-create-service-portal.md). 

Se você não quiser tooprovision um serviço imediatamente, você pode assistir a uma demonstração de 6 minutos de saudação as etapas neste tutorial, começando em cerca de três minutos a esta [vídeo de visão geral da pesquisa do Azure](https://channel9.msdn.com/Events/Connect/2016/138).

## <a name="find-your-service"></a>Localizar o serviço
1. Entrar toohello [portal do Azure](https://portal.azure.com).
2. Abra o painel de serviço de saudação do seu serviço de pesquisa do Azure. Se você não fixar um painel de tooyour Olá serviço lado a lado, você pode encontrar o serviço dessa forma: 
   
   * No hello Jumpbar, clique em **mais serviços** na parte inferior de Olá Olá esquerdo do painel de navegação.
   * Na caixa de pesquisa hello, digite *pesquisa* tooget uma lista de pesquisa de serviços para sua assinatura. O serviço deve aparecer na lista de saudação. 

## <a name="check-for-space"></a>Verificar o espaço
Muitos clientes começam com o serviço gratuito hello. Esta versão é limitado toothree índices, três fontes de dados e três indexadores. Verifique se há espaço para itens extras antes de começar. Este tutorial cria uma unidade de cada objeto. 

> [!TIP] 
> Blocos no painel de serviço Olá mostram quantos índices, indexadores e fontes de dados já tiver. bloco de indexador Olá mostra indicadores de êxito e falha. Olá bloco tooview Olá indexador contagem de clique. 
>
> ![Blocos de indexadores e fontes de dados][1]
>

## <a name="create-index"></a> Criar um índice e carregar dados
Consultas de pesquisa são iteradas em um *índice* que contém os dados pesquisáveis, metadados e construções usados para otimizar certos comportamentos de pesquisa.

tookeep esta tarefa baseado no portal, usamos um conjunto de dados de exemplo interno que pode ser rastreado um indexador via Olá **importar dados** assistente. 

#### <a name="step-1-start-hello-import-data-wizard"></a>Etapa 1: Iniciar o Assistente de importação de dados de saudação
1. No painel de serviço de pesquisa do Azure, clique em **importar dados** em toostart de barra de comando Olá um assistente que cria e preenche um índice.
   
    ![Comando Importar de dados][2]

2. No Assistente de saudação, clique em **fonte de dados** > **exemplos** > **realestate us-exemplo**. Essa fonte de dados é pré-configurada com um nome, um tipo e as informações de conexão. Depois de criada, ela se torna uma "fonte de dados existente" que pode ser reutilizada em outras operações de importação.

    ![Selecionar o conjunto de dados de exemplo][9]

3. Clique em **Okey** toouse-lo.

#### <a name="step-2-define-hello-index"></a>Etapa 2: Definir índice Olá
Criando um índice é geralmente manual e baseada em código, mas o assistente Olá pode gerar um índice para qualquer fonte de dados pode rastrear. No mínimo, um índice exige um nome e uma coleção de campos, com um campo marcado como Olá toouniquely chave do documento identificam cada documento.

Campos têm atributos e tipos de dados. saudação de caixas de seleção na parte superior da saudação são *indexar atributos* controlando como Olá campo é usado. 

* **Recuperável** significa que ele aparece na lista de resultados da pesquisa. Você pode marcar campos individuais como fora dos limites para os resultados de pesquisa ao desmarcar essa caixa de seleção, por exemplo, quando os campos forem usados somente em expressões de filtro. 
* **Filtrável**, **Classificável** e **Com faceta** determinam se um campo pode ser usado em um filtro, em uma classificação ou em uma estrutura de navegação com facetas. 
* **Pesquisável** significa que um campo é incluído na pesquisa de texto completo. As cadeias de caracteres são pesquisáveis. Campos numéricos e boolianos geralmente são marcados como não pesquisáveis. 

Por padrão, o Assistente de saudação examina fonte de dados Olá identificadores exclusivos como base Olá para o campo de chave hello. As cadeias de caracteres são atribuídas como recuperáveis e pesquisáveis. Os números inteiros são atribuídos como recuperáveis, pesquisáveis, classificáveis e facetáveis.

  ![Índice realestate gerado][3]

Clique em **Okey** toocreate índice de saudação.

#### <a name="step-3-define-hello-indexer"></a>Etapa 3: Definir indexador Olá
Ainda no hello **importar dados** assistente, clique em **indexador** > **nome**e digite um nome para o indexador hello. 

Esse objeto define um processo executável. Você pode colocá-lo em agendamento recorrente, mas para o indexador de saudação agora use saudação padrão opção toorun uma vez, imediatamente, quando você clica em **Okey**.  

  ![indexador realestate][8]

## <a name="check-progress"></a>Verificar o andamento
toomonitor dados importar, volte toohello painel de serviço, role para baixo e clique duas vezes em Olá **indexadores** bloco tooopen Olá indexadores lista. Você deve ver o indexador Olá recém-criado na lista hello, com status indicando "em andamento" ou o êxito, juntamente com o número de saudação de documentos indexados.

   ![Mensagem de andamento do indexador][4]

## <a name="query-index"></a>Índice de saudação de consulta
Agora você tem um índice de pesquisa é tooquery pronto. **Pesquisar no Explorador de** é uma ferramenta de consulta incorporada ao portal de saudação. Ele fornece uma caixa de pesquisa para que você possa verificar se os resultados da pesquisa são os esperados. 

> [!TIP]
> Em Olá [vídeo de visão geral da pesquisa do Azure](https://channel9.msdn.com/Events/Connect/2016/138), Olá etapas a seguir é demonstrada no 6m08s do vídeo hello.
>

1. Clique em **pesquisar no Explorador de** na barra de comandos de saudação.

   ![Comando Search Explorer][5]

2. Clique em **índice de alteração** em Olá da barra de comandos tooswitch muito*realestate us-exemplo*.

   ![Comandos de índice e API][6]

3. Clique em **versão da API definir** em toosee Olá de barra de comando que APIs REST estão disponíveis. Visualize fornecem APIs que acesso toonew recursos geralmente ainda não liberados. Para consultas de saudação abaixo, use versão disponível da saudação (2016-09-01) ser quando direcionado. 

    > [!NOTE]
    > [API de REST de pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/search-documents) e hello [biblioteca .NET](search-howto-dotnet-sdk.md#core-scenarios) são totalmente equivalentes, mas **pesquisar no Explorador de** é somente as chamadas REST toohandle equipado. Ele aceita a sintaxe para ambos [sintaxe de consulta simples](https://docs.microsoft.com/rest/api/searchservice/simple-query-syntax-in-azure-search) e [completo analisador de consulta do Lucene](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search), além de todos os Olá parâmetros de pesquisa disponíveis no [pesquisar documento](https://docs.microsoft.com/rest/api/searchservice/search-documents) operações.
    > 

4. Na barra de pesquisa hello, insira cadeias de caracteres de consulta do hello abaixo e clique em **pesquisa**.

  ![Exemplo de consulta de pesquisa][7]

**`search=seattle`**

+ Olá `search` parâmetro é usado tooinput uma pesquisa de palavra-chave de pesquisa de texto completo, nesse caso, retornando listagens em estado de King County, Washington, que contém *Seattle* em qualquer campo pesquisável no documento de saudação. 

+ **Pesquisar no Explorador de** retorna resultados em JSON, que é detalhado e é difícil tooread se documentos têm uma estrutura densa. Dependendo de seus documentos, talvez seja necessário código toowrite identificadores pesquisar elementos importantes de tooextract de resultados. 

+ Documentos são compostos de todos os campos marcados como recuperáveis no índice de saudação. atributos de índice tooview no portal de saudação, clique em *realestate us-exemplo* em Olá **índices** lado a lado.

**`search=seattle&$count=true&$top=100`**

+ Olá `&` símbolo é tooappend usados parâmetros de pesquisa, que podem ser especificados em qualquer ordem. 

+  Olá `$count=true` parâmetro retorna uma contagem de soma de saudação de todos os documentos retornados. Você pode verificar consultas de filtro monitorando alterações relatadas por `$count=true`. 

+ Olá `$top=100` retorna hello mais alto classificados 100 documentos fora Olá total. Por padrão, a pesquisa do Azure retorna Olá primeiros 50 melhores correspondências. Você pode aumentar ou diminuir a quantidade Olá via `$top`.

**`search=*&facet=city&$top=2`**

+ `search=*` é uma pesquisa vazia. Pesquisas vazias pesquisam tudo. Um motivo para enviar uma consulta vazia é muito filtrar ou faceta em um conjunto completo de Olá de documentos. Por exemplo, você deseja tooconsist de estrutura de navegação uma faceta de todas as cidades em índice hello.

+  `facet`Retorna uma navegação de estrutura que você pode passar tooa controle de interface do usuário. Ela retorna categorias e uma contagem. Nesse caso, categorias são com base no número de saudação de cidades. Não há nenhuma agregação no Azure Search, mas você pode aproximar agregação com `facet`, que retorna uma contagem de documentos em cada categoria.

+ `$top=2`recupera dois documentos, que ilustra que você pode usar `top` tooboth reduzir ou aumentar os resultados.

**`search=seattle&facet=beds`**

+ Essa consulta é faceta para camas em uma pesquisa de texto para *Seattle*. `"beds"`pode ser especificado como uma faceta como campo hello está marcado como recuperáveis, podem ser filtrados e facetable no índice hello e hello valores que ele contém (numérico, 1 a 5), são adequadas para categorizar listagens em grupos (listagens com 3 quartos, 4 quartos). 

+ Somente campos filtráveis podem ser facetados. Somente campos recuperáveis podem ser retornados nos resultados da saudação.

**`search=seattle&$filter=beds gt 3`**

+ Olá `filter` parâmetro retorna resultados que coincidem Olá critérios fornecidos. Nesse caso, quartos maiores que 3. 

+ A sintaxe de filtro é uma construção de OData. Para saber mais, confira [Sintaxe de filtro OData](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search).

**`search=granite countertops&highlight=description`**

+ Realce de ocorrências refere-se tooformatting no texto correspondência de palavra-chave hello, considerando correspondências são encontrados em um campo específico. Se o termo de pesquisa profundamente é inserido em uma descrição, você pode adicionar toomake realce de ocorrência-toospot mais fácil. Nesse caso, a saudação formatada frase `"granite countertops"` é mais fácil toosee no campo de descrição de saudação.

**`search=mice&highlight=description`**

+ A pesquisa de texto completo localiza formas com semântica semelhante. Nesse caso, os resultados da pesquisa contêm texto realçado para "mouse", para residências com infestação do mouse na pesquisa de palavra-chave tooa resposta em "mouse". Diferentes formas de saudação mesma palavra pode aparecer nos resultados devido a análise linguística. 

+ O Azure Search dá suporte a 56 analisadores da Lucene e da Microsoft. padrão de saudação usado pela pesquisa do Azure é analisador Lucene padrão de saudação. 

**`search=samamish`**

+ Palavras incorretas, como 'samamish' para o limite de Samammish Olá no hello área de Seattle, falharem tooreturn correspondências no comuns de pesquisa. erros de ortografia toohandle, você pode usar a pesquisa difusa, descrita no exemplo a seguir hello.

**`search=samamish~&queryType=full`**

+ Pesquisa difusa é habilitada quando você especificar Olá `~` de símbolo e usar o analisador de consulta completa hello, que interpreta e analise corretamente Olá `~` sintaxe. 

+ A pesquisa difusa está disponível quando você escolher analisador de consulta completa hello, que ocorre quando você configura `queryType=full`. Para obter mais informações sobre cenários de consulta habilitados pelo analisador de consulta completa hello, consulte [Lucene sintaxe de consulta na pesquisa do Azure](https://docs.microsoft.com/rest/api/searchservice/lucene-query-syntax-in-azure-search).

+ Quando `queryType` é não for especificado, o analisador de consulta simples saudação padrão é usado. Analisador de consulta simples Olá é mais rápido, mas se você precisar de pesquisa difusa, expressões regulares, pesquisa por proximidade ou outros tipos de consulta avançada, você precisará sintaxe completa da saudação. 

**`search=*&$count=true&$filter=geo.distance(location,geography'POINT(-122.121513 47.673988)') le 5`**

+ A pesquisa geoespacial tem suporte por meio de saudação [edm. Tipo de dados GeographyPoint](https://docs.microsoft.com/rest/api/searchservice/supported-data-types) em um campo que contém as coordenadas. A pesquisa geográfica é um tipo de filtro, especificado na [sintaxe do filtro OData](https://docs.microsoft.com/rest/api/searchservice/odata-expression-syntax-for-azure-search). 

+ consulta de exemplo Hello filtra todos os resultados para dados posicionais, onde os resultados são menos de 5 quilômetros de um determinado ponto (especificado como coordenadas de latitude e longitude). Adicionando `$count`, você pode ver quantos resultados é retornado quando você alterar a distância hello ou coordenadas de saudação. 

+ A pesquisa geográfica é útil se seu aplicativo de pesquisa tem um recurso de “Encontrar nas proximidades” ou usa a navegação de mapa. Entretanto, ela não é uma pesquisa de texto completo. Se você tiver requisitos de usuário para pesquisa em uma cidade ou país por nome, adicione campos que contêm nomes de cidade ou o país, nos toocoordinates de adição.

## <a name="next-steps"></a>Próximas etapas

+ Modifique qualquer um dos objetos de saudação que você acabou de criar. Depois de executar o Assistente de saudação uma vez, você pode voltar e exibir ou modificar os componentes individuais: fonte de dados, indexador ou índice. Algumas edições, como Olá alterando o tipo de dados do campo Olá, não são permitidas no índice hello, mas a maioria das propriedades e configurações são modificáveis.

  componentes individuais do tooview, clique em Olá **índice**, **indexador**, ou **fontes de dados** blocos no seu painel toodisplay uma lista de objetos existentes. toolearn mais sobre as edições de índice que não exigem uma reconstrução, consulte [Atualizar índice (API REST do Azure Search)](https://docs.microsoft.com/rest/api/searchservice/update-index).

+ Tente ferramentas hello e etapas com outras fontes de dados. Olá conjunto de dados de exemplo, `realestate-us-sample`, é de um banco de dados SQL que pode rastrear a pesquisa do Azure. Além do Banco de Dados SQL do Azure, o Azure Search pode rastrear e inferir um índice de estruturas de dados simples no Armazenamento de Tabelas do Azure, no Armazenamento de Blobs, no SQL Server em uma VM do Azure e no Azure Cosmos DB. Todas essas fontes de dados têm suporte no Assistente de saudação. No código, você pode preencher um índice facilmente usando um *indexador*.

+ Todas as outras fontes de dados do indexador não têm suporte por meio de um modelo de push, onde seu código envia novos e alterados conjuntos de linhas no índice de tooyour JSON. Para saber mais, confira [Adicionar, atualizar ou excluir documentos no Azure Search](https://docs.microsoft.com/rest/api/searchservice/addupdate-or-delete-documents).

Para saber mais sobre outros recursos mencionados neste artigo, acesse estes links:

* [Visão geral dos indexadores](search-indexer-overview.md)
* [Criar índice (inclui uma explicação detalhada de atributos de índice Olá)](https://docs.microsoft.com/rest/api/searchservice/create-index)
* [Gerenciador de Pesquisa](search-explorer.md)
* [Pesquisar documentos (inclui exemplos de sintaxe de consulta)](https://docs.microsoft.com/rest/api/searchservice/search-documents)


<!--Image references-->
[1]: ./media/search-get-started-portal/tiles-indexers-datasources2.png
[2]: ./media/search-get-started-portal/import-data-cmd2.png
[3]: ./media/search-get-started-portal/realestateindex2.png
[4]: ./media/search-get-started-portal/indexers-inprogress2.png
[5]: ./media/search-get-started-portal/search-explorer-cmd2.png
[6]: ./media/search-get-started-portal/search-explorer-changeindex-se2.png
[7]: ./media/search-get-started-portal/search-explorer-query2.png
[8]: ./media/search-get-started-portal/realestate-indexer2.png
[9]: ./media/search-get-started-portal/import-datasource-sample2.png