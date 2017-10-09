---
title: aaaAzure Cosmos banco de dados modelo de recursos e conceitos | Microsoft Docs
description: "Saiba mais sobre o modelo de hierárquica do Azure Cosmos DB de bancos de dados, coleções, função definida pelo usuário (UDF), documentos, recursos de toomanage permissões e muito mais."
keywords: "Modelo hierárquico, cosmosdb, azure, Microsoft azure"
services: cosmos-db
documentationcenter: 
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: ef9d5c0c-0867-4317-bb1b-98e219799fd5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2017
ms.author: anhoh
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fc3642232b86cc27901ebd97456c386829324632
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-hierarchical-resource-model-and-core-concepts"></a>Modelo de recurso hierárquico e principais conceitos do Azure Cosmos DB
entidades de banco de dados que gerencia o banco de dados do Azure Cosmos Hello são chamados tooas **recursos**. Cada recurso é identificado de maneira exclusiva por um URI lógico. Você pode interagir com os recursos de saudação usando verbos HTTP padrão, os cabeçalhos de solicitação/resposta e códigos de status. 

Lendo este artigo, você será capaz de tooanswer Olá perguntas a seguir:

* O que é o modelo de recurso do Cosmos DB?
* Quais são de sistema definidos recursos como recursos de toouser contrário definido?
* Como eu acesso um recurso?
* Como eu trabalho com coleções?
* Como trabalhar com procedimentos armazenados, disparadores e UDFs (Funções Definidas pelo Usuário)?

## <a name="hierarchical-resource-model"></a>Modelo de recursos hierárquico
Como hello diagrama a seguir ilustra, Olá Cosmos DB hierárquica **modelo de recurso** consistem em conjuntos de recursos em uma conta de banco de dados, cada endereçável por meio de um URI de lógico e estável. Um conjunto de recursos será chamado tooas um **feed** neste artigo. 

> [!NOTE]
> Banco de dados do Azure Cosmos oferece um protocolo TCP altamente eficiente, que também é RESTful no seu modelo de comunicação, disponível por meio de saudação [API cliente .NET do DocumentDB](documentdb-sdk-dotnet.md).
> 
> 

![Modelo de recurso hierárquico do Azure Cosmos DB][1]  
**Modelo de recursos hierárquico**   

toostart trabalhar com recursos, você deve [criar uma conta de banco de dados](create-documentdb-dotnet.md) usando sua assinatura do Azure. Uma conta do banco de dados pode ser formada por um conjunto de **bancos de dados**, cada um contendo diversas **coleções**, cada uma delas, por sua vez, contendo **procedimentos armazenados, gatilhos, UDFs, documentos** e **anexos** relacionados. Um banco de dados também associada **usuários**, cada um com um conjunto de **permissões** tooaccess coleções, procedimentos armazenados, disparadores, UDFs, documentos ou anexos. Enquanto bancos de dados, usuários, permissões e coleções são recursos definidos pelo sistema com esquemas bastante conhecidos, os documentos e anexos possuem conteúdos JSON arbitrários, definidos pelo usuário.  

| Recurso | Descrição |
| --- | --- |
| Conta de banco de dados |Uma conta de banco de dados está associada a um conjunto de bancos de dados e uma quantidade fixa de armazenamento de blobs para anexos. Você pode criar uma ou mais contas do banco de dados usando sua assinatura do Azure. Para obter mais informações, visite nossa [página de preços](https://azure.microsoft.com/pricing/details/cosmos-db/). |
| Banco de dados |Um banco de dados é um contêiner lógico de armazenamento de documentos particionado em coleções. Ele também é um contêiner para usuários. |
| Usuário |Olá namespace lógico para definir permissões. |
| Permissão |Um token de autorização associado a um usuário para um recurso específico do acesso tooa. |
| Coleção |Uma coleção é um contêiner de documentos JSON e Olá associados a lógica do aplicativo JavaScript. Uma coleção é uma entidade faturável, onde hello [custo](performance-levels.md) é determinado pelo nível de desempenho Olá associado à coleta de saudação. Coleções podem abranger um ou mais partições/servidores e pode ser dimensionado toohandle praticamente ilimitados volumes de armazenamento ou de taxa de transferência. |
| Procedimento armazenado |Lógica de aplicativo escrita em JavaScript que é registrada com uma coleção e executado de forma transacional no mecanismo de banco de dados de saudação. |
| Gatilho |Lógica de aplicativo escrita em JavaScript executada antes ou depois de uma operação de inserção, substituição ou exclusão. |
| UDF |Uma lógica de aplicativo escrita em JavaScript. UDFs habilitar toomodel um operador de consulta personalizada e, portanto, estendem a linguagem de consulta Olá core API DocumentDB. |
| Documento |Conteúdo JSON (arbitrário) definido pelo usuário. Por padrão, nenhum esquema precisa toobe definido nem índices secundários precisarem toobe fornecido para Olá todos os documentos adicionados tooa coleção. |
| Anexo |Um anexo é um documento especial que contém referências e metadados associados a blobs/mídias externos. desenvolvedor Olá pode escolher o blob de saudação toohave gerenciada pelo banco de dados do Cosmos ou armazená-lo com um provedor de serviço blob externo, como OneDrive, Dropbox, etc. |

## <a name="system-vs-user-defined-resources"></a>Recursos definidos pelo sistema versus usuário
Recursos como contas do banco de dados, bancos de dados, coleções, usuários, permissões, procedimentos armazenados, gatilhos e UDFs, todos possuem um esquema fixo e são chamados de recursos do sistema. Por outro lado, recursos, como documentos e anexos não têm restrições no esquema de saudação e exemplos de recursos definida pelo usuário. No Cosmos DB, ambos os recursos definidos pelo sistema e pelo usuário são representados e gerenciados como JSON em conformidade com o padrão. Todos os recursos, sistema ou usuário definida, tem Olá propriedades comuns a seguir.

> [!NOTE]
> Observe que todas as propriedades geradas pelo sistema em um recurso têm como prefixo um sublinhado (_) na sua representação JSON.
> 
> 

<table>
    <tbody>
        <tr>
            <td valign="top"><p><strong>Propriedade</strong></p></td>
            <td valign="top"><p><strong>Configurável pelo usuário ou gerada pelo sistema?</strong></p></td>
            <td valign="top"><p><strong>Finalidade</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>_rid</p></td>
            <td valign="top"><p>Gerada pelo sistema</p></td>
            <td valign="top"><p>Gerados pelo sistema, identificador exclusivo e hierárquico do recurso de saudação</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_etag</p></td>
            <td valign="top"><p>Gerada pelo sistema</p></td>
            <td valign="top"><p>ETag do recurso Olá necessário para o controle de simultaneidade otimista</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_ts</p></td>
            <td valign="top"><p>Gerada pelo sistema</p></td>
            <td valign="top"><p>Último carimbo de hora atualizado do recurso de saudação</p></td>
        </tr>
        <tr>
            <td valign="top"><p>_self</p></td>
            <td valign="top"><p>Gerada pelo sistema</p></td>
            <td valign="top"><p>URI endereçável exclusivo do recurso de saudação</p></td>
        </tr>
        <tr>
            <td valign="top"><p>ID</p></td>
            <td valign="top"><p>Gerada pelo sistema</p></td>
            <td valign="top"><p>Nome exclusivo do recurso Olá definido pelo usuário (com hello mesma partição valor de chave). Se o usuário Olá não especificar uma id, uma id será gerada pelo sistema</p></td>
        </tr>
    </tbody>
</table>

### <a name="wire-representation-of-resources"></a>Representação da conexão dos recursos
Cosmos banco de dados não exige qualquer extensões proprietárias toohello JSON padrão ou especiais codificações; ele funciona com documentos JSON compatíveis padrão.  

### <a name="addressing-a-resource"></a>Endereçamento de um recurso
Todos os recursos são endereçáveis pelo URI. Olá valor Olá **Self** propriedade de um recurso representa Olá URI relativo do recurso de saudação. Hello formato de saudação URI consiste Olá /\<feed\>/ segmentos de caminho de { RID}:  

| Valor de Olá Self | Descrição |
| --- | --- |
| /dbs |Feed de bancos de dados em uma conta de banco de dados |
| /dbs/{dbName} |Banco de dados com uma id de correspondência do valor Olá {dbName} |
| /dbs/{dbName}/colls/ |Feed de coleções em um banco de dados |
| /dbs/{dbName}/colls/{collName} |Coleção com uma id de correspondência do valor Olá {collName} |
| /dbs/{dbName}/colls/{collName}/docs |Feed de documentos em uma coleção |
| /dbs/{dbName}/colls/{collName}/docs/{docId} |Um documento com uma id de correspondência do valor Olá {doc} |
| /dbs/{dbName}/users/ |Feed de usuários em um banco de dados |
| /dbs/{dbName}/users/{userId} |Usuário com uma id de correspondência do valor Olá {user} |
| /dbs/{dbName}/users/{userId}/permissions |Feed de permissões em um usuário |
| /dbs/{dbName}/users/{userId}/permissions/{permissionId} |Permissão com uma id de correspondência do valor Olá {permissão} |

Cada recurso tem um nome de usuário exclusivo definido exposto por meio da propriedade de id de saudação. Observação: para documentos, se o usuário Olá não especificar uma id nossos SDKs com suporte gerará automaticamente uma id exclusiva para o documento de saudação. id de saudação é uma cadeia de caracteres definida pelo usuário, de caracteres too256 que é exclusiva no contexto de saudação de um recurso específico do pai. 

Cada recurso também tem um identificador de recurso hierárquica de gerada pelo sistema (também chamado tooas uma RID), que está disponível por meio da propriedade Olá RID. Olá RID codifica toda a hierarquia de um determinado recurso hello e é que uma representação interna conveniente usado tooenforce a integridade referencial de maneira distribuída. Olá RID é exclusivo dentro de uma conta de banco de dados e ele é usado internamente pelo banco de dados do Cosmos para roteamento eficiente, sem a necessidade de pesquisas de partição cruzada. Olá valores Olá Self e propriedades de RID Olá são representações alternativas e canônicas de um recurso. 

suporte a APIs REST Olá endereçamento de recursos e roteamento de solicitações por id de saudação e propriedades de RID hello.

## <a name="database-accounts"></a>Contas de banco de dados
É possível provisionar uma ou mais contas de bancos de dados do Cosmos DB usando sua assinatura do Azure.

Você pode criar e gerenciar contas de banco de dados do banco de dados do Cosmos via Olá Portal do Azure em [http://portal.azure.com/](https://portal.azure.com/). Criar e gerenciar uma conta do banco de dados requer acesso administrativo e pode ser feito somente com sua assinatura do Azure. 

### <a name="database-account-properties"></a>Propriedades de contas de banco de dados
Como parte do provisionamento e gerenciamento de uma conta de banco de dados, você pode configurar e ler Olá propriedades a seguir:  

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p><strong>Nome da Propriedade</strong></p></td>
            <td valign="top"><p><strong>Descrição</strong></p></td>
        </tr>
        <tr>
            <td valign="top"><p>Política de Consistência</p></td>
            <td valign="top"><p>Defina esse nível de consistência propriedade tooconfigure saudação padrão para todas as coleções de saudação em sua conta do banco de dados. Você pode substituir o nível de consistência de saudação em uma base por solicitação usando o cabeçalho de solicitação Olá [x-ms-consistency-level]. <p><p>Observe que essa propriedade só se aplica a toohello <i>recursos definidos pelo usuário</i>. Todos os recursos definidos pelo sistema são toosupport configurado leituras/consultas com forte consistência.</p></td>
        </tr>
        <tr>
            <td valign="top"><p>Chaves de autorização</p></td>
            <td valign="top"><p>Essas são Olá primário e secundárias chaves mestre e somente leitura que fornecem administrativas acessar tooall de recursos de saudação na conta de banco de dados de saudação.</p></td>
        </tr>
    </tbody>
</table>

Observe que na adição tooprovisioning, configurar e gerenciar sua conta do banco de dados de saudação Portal do Azure, você pode também programaticamente criar e gerenciar contas de banco de dados do banco de dados do Cosmos usando Olá [APIs REST do Azure Cosmos DB](/rest/api/documentdb/) como Assim como [cliente SDKs](documentdb-sdk-dotnet.md).  

## <a name="databases"></a>Bancos de dados
Um banco de dados do banco de dados do Cosmos é um contêiner lógico de uma ou mais coleções e usuários, conforme mostrado no diagrama a seguir de saudação. Você pode criar qualquer número de bancos de dados em um toooffer de entidade de conta de banco de dados Cosmos DB limites.  

![Modelo hierárquico de coleções e conta de banco de dados][2]  
**Um banco de dados é um contêiner lógico de usuários e coleções**

Um banco de dados pode conter armazenamento de documentos praticamente ilimitado dividido nas coleções.

### <a name="elastic-scale-of-a-cosmos-db-database"></a>Escala elástica de um banco de dados do Cosmos DB
Um banco de dados do banco de dados do Cosmos é Elástico por padrão – desde alguns toopetabytes GB de armazenamento de documentos SSD feito e taxa de transferência fornecida. 

Ao contrário de um banco de dados RDBMS tradicional, um banco de dados no banco de dados do Cosmos não é tooa escopo único computador. Com o banco de dados do Cosmos, conforme a escala do aplicativo precisa toogrow, você pode criar mais coleções, bancos de dados ou ambos. Na verdade, vários aplicativos internos da Microsoft utilizam o Cosmos DB na escala do cliente criando bancos de dados do Cosmos DB extremamente grandes, cada um contendo milhares de coleções com terabytes de armazenamento de documentos. Você pode aumentar ou reduzir um banco de dados, adicionando ou removendo coleções toomeet requisitos de escala do seu aplicativo. 

Você pode criar qualquer número de coleções em uma oferta de toohello de entidade de banco de dados. Cada coleção tem armazenamento SSD feito e taxa de transferência provisionado para você dependendo do nível de desempenho selecionados hello.

Um banco de dados do Cosmos DB também é um contêiner de usuários. Um usuário, por sua vez, é um namespace lógico para um conjunto de permissões que fornece toocollections refinada de autorização e acesso, documentos e anexos.  

Como com outros recursos no modelo de recurso de banco de dados do Cosmos hello, bancos de dados podem ser criados, substituídos, excluídos, ler ou enumeradas facilmente usando o hello [APIs REST](/rest/api/documentdb/) ou qualquer Olá [cliente SDKs](documentdb-sdk-dotnet.md). Cosmos DB garante a consistência forte para a leitura ou consultar metadados de saudação de um recurso de banco de dados. A exclusão de um banco de dados automaticamente garante que você não pode acessar qualquer uma das coleções de saudação ou usuários contidos nele.   

## <a name="collections"></a>Coleções
Uma coleção do Cosmos DB é um contêiner de seus documentos JSON. 

### <a name="elastic-ssd-backed-document-storage"></a>Armazenamento de documentos com suporte de SSD elástico
Uma coleção é intrinsicamente elástica; ela cresce e é reduzida automaticamente conforme você adiciona ou remove documentos. Coleções são recursos lógicos e podem abranger um ou mais servidores ou partições físicas. número de Olá de partições em uma coleção é determinado pelo banco de dados do Cosmos com base no tamanho do armazenamento hello e taxa de transferência fornecida da sua coleção hello. Cada partição no DB Cosmos tem uma quantidade fixa de armazenamento com suporte de SSD associado a ela e é replicada para alta disponibilidade. Gerenciamento de partição é totalmente gerenciado pelo banco de dados do Azure Cosmos, e você não tem código complexo toowrite ou gerenciar as partições. As coleções do Cosmos DB são **praticamente ilimitadas** em termos de armazenamento e produtividade. 

### <a name="automatic-indexing-of-collections"></a>Indexação automática de coleções
O Cosmos DB é um verdadeiro sistema de banco de dados sem esquemas. Não suponha ou exigir qualquer esquema para documentos JSON hello. Conforme você adiciona a coleção de tooa de documentos, banco de dados do Cosmos os índices automaticamente e estão disponíveis para você tooquery. A indexação automática de documentos sem a necessidade de esquemas ou de índices secundários é uma das principais funcionalidades do Cosmos DB e é habilitada por técnicas de manutenção de índice otimizada para gravação, livre de bloqueios e estruturada para log. O Cosmos DB dá suporte a um volume sustentado de gravações extremamente rápidas, ao mesmo tempo que oferece consultas consistentes. Armazenamento de documento e de índice são usado toocalculate Olá armazenamento consumido por cada coleção. Você pode controlar Olá armazenamento e desempenho compensações associadas indexação Configurando a política de indexação Olá para uma coleção. 

### <a name="configuring-hello-indexing-policy-of-a-collection"></a>Configurando a política de indexação de saudação de uma coleção
Olá, política de cada coleção de indexação permite que você toomake desempenho e armazenamento associadas com a indexação de vantagens e desvantagens. Olá opções a seguir estão disponível tooyou como parte da configuração de indexação:  

* Escolha se a coleção de saudação indexa automaticamente todos os documentos de saudação ou não. Por padrão, todos os documentos são indexados automaticamente. Você pode escolher tooturn desativar a indexação automática e adicionar seletivamente apenas o índice de toohello documentos específicos. Por outro lado, você pode seletivamente escolher tooexclude somente documentos específicos. Você pode obter isso definindo Olá automática de propriedade toobe true ou false no indexingPolicy saudação de uma coleção e usando o cabeçalho de solicitação Olá [x-ms-indexingdirective] durante a inserção, substituição ou exclusão de um documento.  
* Escolha se tooinclude ou excluir caminhos específicos ou padrões nos seus documentos de Olá índice. Você pode obter isso por configuração includedPaths e excludedPaths no indexingPolicy de saudação de uma coleção respectivamente. Você também pode configurar Olá armazenamento e desempenho as compensações de intervalo e hash de consultas de padrões de caminho específico. 
* Escolha entre atualizações de índice síncronas (consistentes) e assíncronas (lentas). Por padrão, o índice de saudação é atualizado de forma síncrona em cada inserção, substituição ou exclusão de uma coleção de toohello do documento. Isso permite consultas Olá toohonor Olá mesmo nível de consistência de leituras de documento hello. Enquanto Cosmos DB é otimizada de gravação e oferece suporte a volumes prolongados de gravações de documento junto com a manutenção do índice síncrona e fazer consultas consistentes, você pode configurar determinada coleções tooupdate seu índice lentamente. A indexação lenta aumenta o desempenho de gravação de saudação adicional e é ideal para cenários de ingestão em massa para coleções de leitura intensa principalmente.

Olá, política de indexação pode ser alterado por executar um PUT na coleção de saudação. Isso pode ser obtido por meio de saudação [SDK de cliente](documentdb-sdk-dotnet.md), Olá [Portal do Azure](https://portal.azure.com) ou hello [APIs REST](/rest/api/documentdb/).

### <a name="querying-a-collection"></a>Consultando uma coleção
documentos de saudação dentro de uma coleção podem ter esquemas arbitrárias e você pode consultar documentos dentro de uma coleção sem fornecer qualquer esquema ou os índices secundários antecipadamente. Você pode consultar a coleção de saudação usando Olá [API DocumentDB do Azure Cosmos DB: referência de sintaxe SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx), que fornece operadores espaciais hierárquicas e relacionais avançados e extensibilidade via UDFs baseados em JavaScript. Gramática JSON permite que documentos JSON como árvores com rótulos como nós de árvore de saudação de modelagem. Isso é explorado pelas técnicas de indexação automática da API do DocumentDB, bem como pelo dialeto SQL da API do DocumentDB. Olá linguagem de consulta DocumetDB API consiste em três aspectos principais:   

1. Um pequeno conjunto de operações de consulta que mapeiam naturalmente a estrutura de árvore toohello incluindo projeções e consultas hierárquicas. 
2. Um subconjunto de operações relacionais, incluindo composição, filtragem, projeções, agregados e junções automáticas. 
3. UDFs puras baseadas em JavaScript que funcionam com (1) e (2).  

modelo de consulta de banco de dados do Cosmos Olá tentativas toostrike um equilíbrio entre a funcionalidade de simplicidade e eficiência. mecanismo de banco de dados do banco de dados do Cosmos Olá compila e executa instruções de consulta SQL Olá nativamente. Você pode consultar uma coleção usando Olá [APIs REST](/rest/api/documentdb/) ou qualquer Olá [cliente SDKs](documentdb-sdk-dotnet.md). Olá .NET SDK vem com um provedor LINQ.

> [!TIP]
> Você pode experimentar Olá API DocumentDB e executar consultas SQL em nosso conjunto de dados no hello [parque de consulta](https://www.documentdb.com/sql/demo).
> 
> 

## <a name="multi-document-transactions"></a>Transações entre vários documentos
Transações de banco de dados fornecem um modelo de programação previsível e seguro para lidar com as alterações simultâneas toohello dados. Em RDBMS, lógica de negócios de toowrite de maneira tradicional de saudação é toowrite **procedimentos armazenados** e/ou **gatilhos** e enviar toohello servidor de banco de dados para execução transacional. Em RDBMS, Programador de aplicativo hello é necessário toodeal com duas linguagens de programação diferentes: 

* saudação (não-transacional) aplicativo linguagem de programação (por exemplo, JavaScript, Python, c#, Java, etc.)
* T-SQL, Olá transacional linguagem de programação que é executada nativamente pelo banco de dados de saudação

Em virtude do seu compromisso profundo tooJavaScript e JSON diretamente no mecanismo de banco de dados hello, Cosmos DB fornece um modelo de programação intuitivo para JavaScript em execução com base em lógica do aplicativo diretamente em coleções de saudação em termos de procedimentos armazenados e gatilhos. Isso permite que tanto a seguir Olá para:

* Controlar a implementação eficiente de simultaneidade, recuperação, automática de indexação de gráficos de objeto JSON Olá diretamente no mecanismo de banco de dados de saudação
* Naturalmente expressar o fluxo de controle, a variável de escopo, a atribuição e integração de primitivos com transações de banco de dados diretamente em termos de linguagem de programação de JavaScript Olá de tratamento de exceção

lógica de JavaScript Olá registrada em um nível de coleção pode emitir, em seguida, operações de banco de dados em documentos de saudação do hello considerando a coleção. Banco de dados do cosmos implicitamente Olá encapsula JavaScript com base em procedimentos armazenados e disparadores em um ambiente transações ACID com isolamento de instantâneo em documentos dentro de uma coleção. Durante o curso de saudação de sua execução, se Olá JavaScript lança uma exceção, em seguida, Olá toda transação foi anulada. Olá modelo de programação resultante é muito simples mas poderosas. Os desenvolvedores de JavaScript obtêm um modelo de programação “durável”, ao mesmo tempo em que utilizam os construtores de linguagem e primitivas de biblioteca com os quais estão familiarizados.   

Olá capacidade tooexecute JavaScript diretamente no banco de dados de saudação mecanismo Olá mesmo espaço de endereço, como o pool de buffers Olá permite alto desempenho e a execução transacional das operações de banco de dados em relação a documentos de saudação de uma coleção. Além disso, mecanismo de banco de dados do banco de dados do Cosmos torna toohello um compromisso profundo JSON e JavaScript elimina qualquer incompatibilidade de impedância entre sistemas de tipos de saudação do aplicativo e banco de dados de saudação.   

Depois de criar uma coleção, você pode registrar os procedimentos armazenados, gatilhos e UDFs com uma coleção usando Olá [APIs REST](/rest/api/documentdb/) ou qualquer Olá [cliente SDKs](documentdb-sdk-dotnet.md). Após o registro, você pode fazer referência a eles e executá-los. Considere seguinte Olá escrito inteiramente em JavaScript, abaixo do código Olá leva dois argumentos (nome do catálogo e o nome do autor) de procedimento armazenado e cria um novo documento, consultas para um documento e, em seguida, atualiza-– tudo dentro de uma transação ACID implícita. A qualquer momento durante a execução de Olá, se for lançada uma exceção de JavaScript, Olá toda transação é anulada.

    function businessLogic(name, author) {
        var context = getContext();
        var collectionManager = context.getCollection();        
        var collectionLink = collectionManager.getSelfLink()

        // create a new document.
        collectionManager.createDocument(collectionLink,
            {id: name, author: author},
            function(err, documentCreated) {
                if(err) throw new Error(err.message);

                // filter documents by author
                var filterQuery = "SELECT * from root r WHERE r.author = 'George R.'";
                collectionManager.queryDocuments(collectionLink,
                    filterQuery,
                    function(err, matchingDocuments) {
                        if(err) throw new Error(err.message);

                        context.getResponse().setBody(matchingDocuments.length);

                        // Replace hello author name for all documents that satisfied hello query.
                        for (var i = 0; i < matchingDocuments.length; i++) {
                            matchingDocuments[i].author = "George R. R. Martin";
                            // we don’t need tooexecute a callback because they are in parallel
                            collectionManager.replaceDocument(matchingDocuments[i]._self,
                                matchingDocuments[i]);   
                        }
                    })
            })
    };

cliente Olá pode "Enviar" hello acima de banco de dados de toohello lógica de JavaScript para execução transacional por meio de HTTP POST. Para obter mais informações sobre como usar métodos HTTP, consulte [Interações RESTful com recursos do Azure Cosmos DB](https://msdn.microsoft.com/library/azure/mt622086.aspx). 

    client.createStoredProcedureAsync(collection._self, {id: "CRUDProc", body: businessLogic})
       .then(function(createdStoredProcedure) {
            return client.executeStoredProcedureAsync(createdStoredProcedure.resource._self,
                "NoSQL Distilled",
                "Martin Fowler");
        })
        .then(function(result) {
            console.log(result);
        },
        function(error) {
            console.log(error);
        });


Observe que porque o banco de dados de saudação nativamente compreende JSON e JavaScript, não há nenhuma incompatibilidade de sistema de tipo, "Mapeamento de OR" ou mágico de geração de código necessária.   

Procedimentos armazenados e gatilhos interagem com os documentos em uma coleção por meio de um modelo de objeto bem definidos, que expõe o contexto atual de coleção Olá coleta e hello.  

Coleções no hello API DocumentDB podem ser criado, excluídos, leitura ou enumeradas facilmente usando o hello [APIs REST](/rest/api/documentdb/) ou qualquer Olá [cliente SDKs](documentdb-sdk-dotnet.md). Olá API DocumentDB sempre fornece consistência forte para a leitura ou consultar metadados de saudação de uma coleção. A exclusão de uma coleção automaticamente garante que você não pode acessar qualquer um dos documentos hello, anexos, procedimentos armazenados, gatilhos e UDFs contém nele.   

## <a name="stored-procedures-triggers-and-user-defined-functions-udf"></a>Procedimentos armazenados, gatilhos e UDF (Funções Definidas pelo Usuário)
Conforme descrito na seção anterior hello, você pode escrever toorun de lógica de aplicativo diretamente em uma transação dentro do mecanismo de banco de dados de saudação. a lógica do aplicativo Hello pode ser escrita inteiramente em JavaScript e pode ser modelada como um procedimento armazenado, gatilho ou uma UDF. Olá código JavaScript em um procedimento armazenado ou um disparador pode inserir, substituir, excluir, documentos de leitura ou de consulta dentro de uma coleção. Em Olá outro lado, Olá JavaScript dentro de um UDF não pode inserir, substituir ou excluir documentos. UDFs enumerar documentos de saudação do conjunto de resultados da consulta e geram outro conjunto de resultados. Para multilocatários, o Cosmos DB impõe uma rígida governança de recursos baseada em reserva. Cada procedimento armazenado, gatilho ou uma UDF obtém um quantum fixo de toodo de recursos de sistema operacional seu trabalho. Além disso, procedimentos armazenados, gatilhos ou UDFs não é possível vincular com bibliotecas JavaScript externas e estão na lista negra se excederem os orçamentos de recurso de saudação alocados toothem. Você pode registrar, cancelar o registro de procedimentos armazenados, gatilhos ou UDFs com uma coleção usando Olá APIs REST.  Após o registro, um procedimento armazenado, gatilho ou UDF é pré-compilado e armazenado como um código de byte que é executado posteriormente. Olá seção a seguir ilustra como você pode usar Olá SDK de JavaScript do Cosmos DB tooregister, executar e cancelar o registro de um procedimento armazenado, gatilho e uma UDF. Olá SDK de JavaScript é um wrapper simple sobre Olá [APIs REST](/rest/api/documentdb/). 

### <a name="registering-a-stored-procedure"></a>Registrando um procedimento armazenado
O registro de um procedimento armazenado cria um novo recurso de procedimento armazenado em uma coleção por meio do HTTP POST.  

    var storedProc = {
        id: "validateAndCreate",
        body: function (documentToCreate) {
            documentToCreate.id = documentToCreate.id.toUpperCase();

            var collectionManager = getContext().getCollection();
            collectionManager.createDocument(collectionManager.getSelfLink(),
                documentToCreate,
                function(err, documentCreated) {
                    if(err) throw new Error('Error while creating document: ' + err.message;
                    getContext().getResponse().setBody('success - created ' + 
                            documentCreated.name);
                });
        }
    };

    client.createStoredProcedureAsync(collection._self, storedProc)
        .then(function (createdStoredProcedure) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-stored-procedure"></a>Executando um procedimento armazenado
Execução de um procedimento armazenado é feita por meio de um HTTP POST em um recurso de procedimento armazenado existente, passando parâmetros de procedimento toohello no corpo da solicitação de saudação.

    var inputDocument = {id : "document1", author: "G. G. Marquez"};
    client.executeStoredProcedureAsync(createdStoredProcedure.resource._self, inputDocument)
        .then(function(executionResult) {
            assert.equal(executionResult, "success - created DOCUMENT1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-stored-procedure"></a>Cancelando o registro de um procedimento armazenado
Cancelar o registro de um procedimento armazenado é um processo simples, feito com a emissão de um HTTP DELETE para um recurso do procedimento armazenado existente.   

    client.deleteStoredProcedureAsync(createdStoredProcedure.resource._self)
        .then(function (response) {
            return;
        }, function(error) {
            console.log("Error");
        });


### <a name="registering-a-pre-trigger"></a>Registrando um pré-gatilho
O registro de um gatilho é realizado ao criar um novo recurso de gatilho em uma coleção por meio do HTTP POST. Você pode especificar se o gatilho de saudação é uma versão anterior ou um tipo de gatilho e hello post de operação pode ser associado (por exemplo, criar, substituir, excluir ou todos).   

    var preTrigger = {
        id: "upperCaseId",
        body: function() {
                var item = getContext().getRequest().getBody();
                item.id = item.id.toUpperCase();
                getContext().getRequest().setBody(item);
        },
        triggerType: TriggerType.Pre,
        triggerOperation: TriggerOperation.All
    }

    client.createTriggerAsync(collection._self, preTrigger)
        .then(function (createdPreTrigger) {
            console.log("Successfully created trigger");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-pre-trigger"></a>Executando um pré-gatilho
Execução de um gatilho é feita especificando o nome hello de um gatilho existente em tempo de saudação de emitir a solicitação do hello PUT/POST/exclusão de um recurso de documento por meio do cabeçalho de solicitação de saudação.  

    client.createDocumentAsync(collection._self, { id: "doc1", key: "Love in hello Time of Cholera" }, { preTriggerInclude: "upperCaseId" })
        .then(function(createdDocument) {
            assert.equal(createdDocument.resource.id, "DOC1");
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-pre-trigger"></a>Cancelando o registro de um pré-gatilho
O cancelamento do registro de um gatilho é feito simplesmente ao emitir um comando HTTP DELETE para um recurso de gatilho existente.  

    client.deleteTriggerAsync(createdPreTrigger._self);
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

### <a name="registering-a-udf"></a>Registrando uma UDF
O registro de uma UDF é realizado ao criar um novo recurso de UDF em uma coleção por meio do HTTP POST.  

    var udf = { 
        id: "mathSqrt",
        body: function(number) {
                return Math.sqrt(number);
        },
    };
    client.createUserDefinedFunctionAsync(collection._self, udf)
        .then(function (createdUdf) {
            console.log("Successfully created stored procedure");
        }, function(error) {
            console.log("Error");
        });

### <a name="executing-a-udf-as-part-of-hello-query"></a>Execução de um UDF como parte da consulta Olá
Um UDF pode ser especificado como parte da consulta SQL hello e é usado como um núcleo de saudação do modo tooextend [linguagem de consulta SQL para Olá API DocumentDB](https://msdn.microsoft.com/library/azure/dn782250.aspx).

    var filterQuery = "SELECT udf.mathSqrt(r.Age) AS sqrtAge FROM root r WHERE r.FirstName='John'";
    client.queryDocuments(collection._self, filterQuery).toArrayAsync();
        .then(function(queryResponse) {
            var queryResponseDocuments = queryResponse.feed;
        }, function(error) {
            console.log("Error");
        });

### <a name="unregistering-a-udf"></a>Cancelando o registro de uma UDF
O cancelamento do registro de uma UDF é feito simplesmente ao emitir um comando HTTP DELETE para um recurso de UDF existente.  

    client.deleteUserDefinedFunctionAsync(createdUdf._self)
        .then(function(response) {
            return;
        }, function(error) {
            console.log("Error");
        });

Embora os trechos de código Olá acima mostraram registro hello (POST), o cancelamento do registro (PUT), lista/leitura (GET) e execução (POST) por meio de saudação [SDK de JavaScript](https://github.com/Azure/azure-documentdb-js), você também pode usar o hello [APIs REST](/rest/api/documentdb/) ou outros [cliente SDKs](documentdb-sdk-dotnet.md). 

## <a name="documents"></a>Documentos
Você pode inserir, substituir, excluir, ler, enumerar e consultar documentos JSON arbitrários em uma coleção. Cosmos banco de dados não exige qualquer esquema e não requer índices secundários na ordem toosupport consultas em documentos em uma coleção. tamanho máximo de saudação para um documento é 2 MB.   

Sendo um serviço de banco de dados verdadeiramente aberto, o Cosmos DB não inverte nenhum tipo de dados especializado (por exemplo, data e hora) nem codificações específicas para documentos JSON. Observe que o banco de dados do Cosmos não exigem qualquer especial JSON convenções toocodify Olá relações entre vários documentos; sintaxe SQL de saudação do Cosmos DB fornece operadores de consulta relacional e hierárquica muito poderoso documentos tooquery e projeto sem anotações especiais ou necessidade toocodify relações entre documentos usando propriedades distintos.  

Como com todos os outros recursos, os documentos podem ser criados, substituídos, excluídos, ler, enumerados e consultados facilmente usando APIs REST ou qualquer Olá [cliente SDKs](documentdb-sdk-dotnet.md). Exclusão de um documento instantaneamente libera Olá cota correspondente tooall de anexos Olá aninhado. Olá ler o nível de consistência de documentos segue a política de consistência de saudação na conta de banco de dados de saudação. Essa política pode ser substituída com base em cada solicitação, dependendo dos requisitos de consistência de dados de seu aplicativo. Ao consultar documentos, Olá ler consistência segue Olá definido na coleção de saudação do modo de indexação. Para "consistente", isso segue a política de consistência da conta hello. 

## <a name="attachments-and-media"></a>Anexos e mídia
Cosmos banco de dados permite que você toostore binário blobs/mídia com banco de dados do Cosmos (máximo de 2 GB por conta) ou tooyour de mídia remota próprio repositório. Ele também permite toorepresent Olá metadados de uma mídia em termos de um documento especial chamado de anexo. Um anexo em Cosmos DB é um documento de (JSON) especial que referências Olá mídia/blob armazenado em outro lugar. Um anexo é simplesmente um documento especial que captura Olá metadados (por exemplo, o local, o autor etc.) de uma mídia armazenada em um armazenamento de mídia remota. 

Considere um aplicativo de leitura social que usa o banco de dados do Cosmos toostore anotações e realça os metadados, incluindo comentários, indicadores, classificações, equipara/preferências pessoais etc. associados para um livro eletrônico de um determinado usuário.   

* Hello conteúdo do catálogo de saudação em si é armazenado no armazenamento de mídia hello ou disponível como parte da conta de banco de dados do banco de dados do Cosmos ou um repositório de mídia remota. 
* Um aplicativo poderá armazenar os metadados de cada usuário como um documento distinto, por exemplo, os metadados de Joe para o book1 são armazenados em um documento cuja referência é /colls/joe/docs/book1. 
* Anexos apontando toohello páginas de conteúdo de um determinado registro de um usuário são armazenados em um documento correspondente do hello, por exemplo, /colls/joe/docs/book1/chapter1, /colls/joe/docs/book1/chapter2 etc. 

Observe que os exemplos de saudação listados acima use hierarquia de recursos do ids amigável tooconvey hello. Recursos são acessados por meio de saudação APIs REST por meio de ids de recurso exclusivo. 

Para mídia de saudação que é gerenciada pelo banco de dados do Cosmos, propriedade de _media de saudação do anexo de saudação fará referência a mídia de saudação por seu URI. Cosmos DB garantirá mídia de coletar Olá toogarbage quando todas as referências de saudação pendentes serão descartadas. Cosmos DB gera anexo hello quando você carregar uma nova mídia hello e popula Olá _media toopoint toohello recém-adicionado mídia automaticamente. Se você escolher a mídia de saudação toostore em um armazenamento de blob remoto gerenciado por você (por exemplo, o OneDrive, o armazenamento do Azure, DropBox etc), você ainda pode usar a mídia de saudação tooreference anexos. Nesse caso, você mesmo cria anexo hello e preencher sua propriedade _media.   

Assim como acontece com todos os outros recursos, anexos podem ser criados, substituídos, excluídos, ler ou enumeradas facilmente usando APIs REST ou qualquer um dos SDKs de cliente de saudação. Como com os documentos, Olá do nível de consistência de anexos de leitura segue a política de consistência de saudação na conta de banco de dados de saudação. Essa política pode ser substituída com base em cada solicitação, dependendo dos requisitos de consistência de dados de seu aplicativo. Ao consultar anexos, Olá ler consistência segue Olá definido na coleção de saudação do modo de indexação. Para "consistente", isso segue a política de consistência da conta hello. 
 

## <a name="users"></a>Usuários
Um usuário do Cosmos DB representa um namespace lógico para agrupar permissões. Um usuário de banco de dados do Cosmos pode corresponder tooa usuário em um sistema de gerenciamento de identidade ou uma função de aplicativo predefinido. Para o banco de dados do Cosmos, um usuário simplesmente representa uma abstração toogroup um conjunto de permissões em um banco de dados.   

Para implementar a multilocação em seu aplicativo, você pode criar usuários no banco de dados do Cosmos que corresponde a usuários reais de tooyour ou locatários de saudação do seu aplicativo. Você pode criar permissões para um determinado usuário que correspondem a controle de acesso de toohello sobre várias coleções, documentos, anexos, etc.   

Como seus aplicativos precisam tooscale com o crescimento de usuário, você pode adotar tooshard de várias maneiras seus dados. Você pode modelar seus usuários da seguinte forma:   

* Cada usuário mapeado tooa banco de dados.
* Cada usuário mapeado tooa coleção. 
* Documentos correspondente toomultiple usuários vá coleção tooa dedicado. 
* Documentos correspondente toomultiple usuários vá tooa conjunto de coleções.   

Independentemente da estratégia de fragmentação específico Olá que você escolher, podem ser usuários reais de modelo como usuários no banco de dados do banco de dados do Cosmos e associar o usuário de tooeach permissões refinadas.  

![Coleções do usuário][3]  
**Estratégias de fragmentação e modelagem de usuários**

Como todos os outros recursos, os usuários no banco de dados do Cosmos podem ser criados, substituído, excluído, ler ou enumeradas facilmente usando APIs REST ou qualquer um dos SDKs de cliente de saudação. Cosmos DB sempre fornece consistência forte para a leitura ou consultar metadados de saudação de um recurso de usuário. Vale a pena destacar que a exclusão de um usuário automaticamente garante que você não pode acessar qualquer uma das permissões Olá contidas nele. Embora Olá Cosmos DB recupera cota Olá de permissões Olá como parte do usuário Olá excluído no plano de fundo Olá, permissões Olá excluído está disponível imediatamente novamente para você toouse.  

## <a name="permissions"></a>Permissões
De uma perspectiva do controle de acesso, recursos como as contas do banco de dados, bancos de dados, usuários e permissão são considerados recursos *administrativos*, uma vez que requerem permissões administrativas. Em Olá outro lado, recursos, incluindo coleções hello, documentos, anexos, procedimentos armazenados, disparadores, e UDFs estão no escopo em um determinado banco de dados e consideradas *recursos do aplicativo*. Correspondente toohello dois tipos de recursos e funções hello acessá-los (ou seja, o administrador de saudação e o usuário), o modelo de autorização Olá define dois tipos de *chaves de acesso*: *chave mestra* e *a chave de recurso*. Olá master key faz parte da conta do banco de dados de saudação e é fornecida toohello desenvolvedor (ou o administrador) que é o provisionamento de conta de banco de dados de saudação. Essa chave mestra tem semântica de administrador, que pode ser usado tooauthorize tooboth de acesso administrativo e recursos do aplicativo. Em contraste, uma chave de recurso é uma chave de acesso granulares que permite acesso tooa *específico* recurso de aplicativo. Assim, captura relação Olá entre usuário Olá de um banco de dados e Olá permissões Olá usuário para um recurso específico (por exemplo, coleta, documento, anexo, procedimento armazenado, gatilho ou UDF).   

Olá somente tooobtain de forma que uma chave de recurso é criando um recurso de permissão em um determinado usuário. Observe que, em ordem toocreate ou recuperar uma permissão, uma chave mestra deve ser apresentada no cabeçalho de autorização de saudação. Um recurso de permissão vincula o usuário de recurso, seu acesso e Olá Olá. Depois de criar um recurso de permissão, Olá usuário só precisa de chave de recurso associado Olá toopresent no recurso relevante do toohello ordem toogain acesso. Portanto, uma chave de recurso pode ser exibida como uma representação lógica e compact do recurso de permissão de saudação.  

Assim como acontece com todos os outros recursos, as permissões no banco de dados do Cosmos podem ser criadas, substituído, excluído, ler ou enumeradas facilmente usando APIs REST ou qualquer um dos SDKs de cliente de saudação. Cosmos DB sempre fornece consistência forte para a leitura ou consultar metadados de saudação de uma permissão. 

## <a name="next-steps"></a>Próximas etapas
Saiba mais sobre como trabalhar com recursos usando comandos HTTP em [Interações RESTful com recursos do Cosmos DB](https://msdn.microsoft.com/library/azure/mt622086.aspx).

[1]: media/documentdb-resources/resources1.png
[2]: media/documentdb-resources/resources2.png
[3]: media/documentdb-resources/resources3.png

