---
title: aaaAzure Cosmos DB perguntas frequentes | Microsoft Docs
description: "Obtenha respostas toofrequently perguntas frequentes sobre o Azure Cosmos DB, um serviço de banco de dados globalmente distribuídos, vários modelos. Aprenda sobre capacidade, níveis de desempenho e dimensionamento."
keywords: Perguntas de banco de dados, perguntas frequentes, documentdb, azure, Microsoft azure
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: b68d1831-35f9-443d-a0ac-dad0c89f245b
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: mimig
ms.openlocfilehash: 59e047d9acd8ac05facc96655747d7495a45317a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-faq"></a>Perguntas frequentes do Azure Cosmos DB
## <a name="azure-cosmos-db-fundamentals"></a>Conceitos básicos do Azure Cosmos DB
### <a name="what-is-azure-cosmos-db"></a>O que é o Azure Cosmos DB?
O Azure Cosmos DB é um serviço de multimodelo de banco de dados replicado globalmente que oferece consultas avançadas de dados sem esquemas, ajuda a fornecer um desempenho confiável e configurável e possibilita um desenvolvimento rápido. Ela é obtida por meio de uma plataforma gerenciada que é apoiada por power hello e alcançar do Microsoft Azure. 

Banco de dados do Azure Cosmos é a melhor solução Olá jogos portáteis, da web, e aplicativos de IoT quando a taxa de transferência previsível, alta disponibilidade, baixa latência e um modelo de dados sem esquema são os requisitos principais. Ele fornece flexibilidade de esquemas e indexação avançada e inclui suporte a transações de vários documentos com JavaScript integrado. 

Para mais perguntas de banco de dados, as respostas e instruções para implantar e usar esse serviço, consulte Olá [página de documentação do banco de dados do Azure Cosmos](https://azure.microsoft.com/documentation/services/cosmos-db/).

### <a name="what-happened-toodocumentdb"></a>Quais tooDocumentDB com?
Olá API DocumentDB é um dos Olá suporte para APIs e modelos de dados para o banco de dados do Azure Cosmos. Além disso, o Azure Cosmos DB dá suporte com a API do Graph (versão prévia), a API de Tabela (versão prévia) e a API do MongoDB. Para obter mais informações, consulte [Perguntas de clientes do DocumentDB](#moving-to-cosmos-db).

### <a name="how-do-i-get-toomy-documentdb-account-in-hello-azure-portal"></a>Como obter toomy conta DocumentDB Olá portal do Azure?
No hello portal do Azure, clique em ícone de banco de dados do Azure Cosmos Olá no painel esquerdo da saudação. Se você tiver uma conta do DocumentDB antes, agora você tem uma conta de banco de dados do Azure Cosmos, com a cobrança de tooyour nenhuma alteração.

### <a name="what-are-hello-typical-use-cases-for-azure-cosmos-db"></a>Quais são os casos de uso típicos Olá para o banco de dados do Azure Cosmos?
Banco de dados do Azure Cosmos é uma boa escolha para jogos de móveis, web, novo, e aplicativos de IoT onde automáticas de escala, desempenho previsível, rápida a ordem dos tempos de resposta de milissegundo e Olá tooquery de capacidade sobre dados sem esquema é importante. Banco de dados do Azure Cosmos presta toorapid desenvolvimento e suporte a iteração contínua Olá dos modelos de dados de aplicativo. Os aplicativos que gerenciam conteúdo e dados gerados pelo usuário são [casos de uso comuns do Azure Cosmos DB](use-cases.md). 

### <a name="how-does-azure-cosmos-db-offer-predictable-performance"></a>Como o Azure Cosmos DB oferece um desempenho previsível?
Um [unidade de solicitação](request-units.md) (RU) é a medida de saudação da taxa de transferência de banco de dados do Azure Cosmos. Uma taxa de transferência de 1 RU corresponde a taxa de transferência toohello de saudação GET de um documento de 1 KB. Cada operação no Azure Cosmos DB, incluindo leituras, gravações, consultas SQL e execuções de procedimento armazenado, tem um valor de RU determinístico com base na operação de Olá Olá taxa de transferência necessária toocomplete. Em vez de pensar em CPU, E/S, memória e como cada uma dessas medidas afeta a produtividade do seu aplicativo, você pode pensar em uma medida de RU única.

Você pode reservar cada contêiner do Azure Cosmos DB com produtividade provisionada em termos de RUs da produtividade por segundo. Para aplicativos de qualquer escala, você pode avaliar o desempenho de solicitações individuais toomeasure seus valores RU e provisionar um total de saudação do contêiner toohandle de unidades de solicitação em todas as solicitações. Você também pode expandir ou reduzir a taxa de transferência do contêiner como necessidades de saudação do evolve seu aplicativo. Para obter mais informações sobre unidades de solicitação e para obter ajuda para determinar seu contêiner precisa, consulte [estimando as necessidades de taxa de transferência](request-units.md#estimating-throughput-needs) e tente Olá [Calculadora de taxa de transferência](https://www.documentdb.com/capacityplanner). termo Olá *contêiner* aqui se refere a coleção de API do DocumentDB tooa toorefers, graph API do Graph, coleção de API do MongoDB e tabela de API de tabela. 

### <a name="how-does-azure-cosmos-db-support-various-data-models-such-as-keyvalue-columnar-document-and-graph"></a>Como o Azure Cosmos DB dá suporte a vários modelos de dados, como chave/valor, colunar, documento e gráfico?

Documento de chave/valor (tabela), coluna, e os modelos são todos com suporte nativo devido a saudação ARS (átomos, registros e as sequências) criar esse banco de dados do Azure Cosmos de dados do gráfico são criados em. Átomos, registros e as sequências podem ser facilmente projetado e mapeadas toovarious modelos de dados. Olá APIs para um subconjunto de modelos são direita disponível agora (documentos, MongoDB, tabela e APIs de gráfico) e outros modelos de dados específico tooadditional estará disponíveis em Olá futuro.

Banco de dados do Azure Cosmos tem um esquema desconhecido indexação mecanismo capaz de indexação automaticamente todos os dados de saudação que ele consome sem a necessidade de qualquer esquema ou os índices secundários de desenvolvedor hello. mecanismo de saudação se baseia em um conjunto de layouts de índice lógico (árvore invertido, coluna,) que separar o layout de armazenamento de saudação do índice hello e subsistemas de processamento de consulta. Cosmos DB também tem um conjunto de protocolos de transmissão e APIs de saudação toosupport de capacidade de maneira extensível e convertê-las com eficiência toohello core modelo (1) e hello índice lógico layouts de dados (2) tornando capaz de dar suporte a vários modelos de dados nativo .

### <a name="is-azure-cosmos-db-hipaa-compliant"></a>O Azure Cosmos DB está em conformidade com a HIPAA?
Sim, o Azure Cosmos DB está em conformidade com a HIPAA. HIPAA estabelece requisitos para Olá usar, divulgação de informações e a proteção de informações de integridade individualmente identificáveis. Para obter mais informações, consulte Olá [Microsoft Trust Center](https://www.microsoft.com/en-us/TrustCenter/Compliance/HIPAA).

### <a name="what-are-hello-storage-limits-of-azure-cosmos-db"></a>Quais são os limites de armazenamento de saudação do banco de dados do Azure Cosmos?
Não há nenhum limite toohello total de dados que um contêiner pode armazenar no banco de dados do Azure Cosmos.

### <a name="what-are-hello-throughput-limits-of-azure-cosmos-db"></a>Quais são os limites de taxa de transferência de saudação do banco de dados do Azure Cosmos?
Não há nenhum limite toohello total de taxa de transferência que pode dar suporte a um contêiner no banco de dados do Azure Cosmos. Olá chave ideia é toodistribute sua carga de trabalho aproximadamente uniformemente entre um suficientemente grande número de chaves de partição.

### <a name="how-much-does-azure-cosmos-db-cost"></a>Quanto custa o Azure Cosmos DB?
Para obter detalhes, consulte toohello [detalhes de preços do Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/) página. Encargos de uso do Azure DB Cosmos são determinados pelo número de saudação de contêineres provisionados, número de saudação de horas contêineres Olá estavam online e Olá provisionado taxa de transferência para cada contêiner. termo Olá *contêineres* aqui se refere a coleção de API DocumentDB toohello, graph API do Graph, coleção de API do MongoDB e tabelas de API de tabela. 

### <a name="is-a-free-account-available"></a>Existe uma conta gratuita disponível?
Se você for novo tooAzure, você pode se inscrever para uma [conta gratuita do Azure](https://azure.microsoft.com/free/), que oferece 30 dias e e um tootry de crédito todos Olá serviços do Azure. Se você tiver uma assinatura do Visual Studio, você também está qualificado para [livre créditos Azure](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/) toouse em qualquer serviço do Azure. 

Você também pode usar o hello [emulador de banco de dados do Azure Cosmos](local-emulator.md) toodevelop e teste seu aplicativo localmente para livre, sem criar uma assinatura do Azure. Quando estiver satisfeito com como seu aplicativo está funcionando no hello Azure Cosmos DB emulador, você pode alternar toousing uma conta de banco de dados do Azure Cosmos na nuvem hello.

### <a name="how-can-i-get-additional-help-with-azure-cosmos-db"></a>Como fazer para obter mais ajuda com o Azure Cosmos DB?
Se você precisar de nenhuma ajuda, alcançar toous em [estouro de pilha](http://stackoverflow.com/questions/tagged/azure-cosmosdb) ou hello [Fórum do MSDN](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB), ou agendar um bate-papo individuais com a equipe de engenharia de banco de dados do Azure Cosmos Olá enviando email muito[ askcosmosdb@microsoft.com](mailto:askcosmosdb@microsoft.com). 

## <a name="set-up-azure-cosmos-db"></a>Configurar o Azure Cosmos DB
### <a name="how-do-i-sign-up-for-azure-cosmos-db"></a>Como fazer para se inscrever no Azure Cosmos DB?
Banco de dados do Azure Cosmos está disponível no hello portal do Azure. Primeiro, inscreva-se para uma assinatura do Azure. Depois que você se inscrever, você pode adicionar uma API de documentos, o Graph API (visualização), a API de API de tabela (visualização) ou MongoDB conta tooyour assinatura do Azure.

### <a name="what-is-a-master-key"></a>O que é uma chave mestra?
Uma chave mestra é uma tooaccess de token de segurança todos os recursos para uma conta. Indivíduos com chave Olá tem recursos de tooall de acesso de leitura e gravação na conta de banco de dados de saudação. Seja cauteloso ao distribuir chaves mestras. Olá chave de mestre primária e secundária mestre estão disponíveis em Olá **chaves** folha de saudação [portal do Azure][azure-portal]. Para saber mais sobre as chaves, consulte [Exibir, copiar e regenerar chaves de acesso](manage-account.md#keys).

### <a name="what-are-hello-regions-that-preferredlocations-can-be-set-to"></a>O que são regiões de saudação PreferredLocations pode ser definido como? 
Olá PreferredLocations valor pode ser definido como tooany de hello Azure regiões em que o banco de dados do Cosmos está disponível. Para obter uma lista de regiões disponíveis, consulte [Regiões do Azure](https://azure.microsoft.com/regions/).

### <a name="is-there-anything-i-should-be-aware-of-when-distributing-data-across-hello-world-via-hello-azure-datacenters"></a>Há algo que deve estar ciente de quando a distribuição de dados entre Olá, mundo via Olá datacenters do Azure? 
Banco de dados do Azure Cosmos está presente em todas as regiões do Azure, como especificado em hello [regiões do Azure](https://azure.microsoft.com/regions/) página. Porque ele é o serviço principal de hello, cada novo datacenter tem uma presença de banco de dados do Azure Cosmos. 

Quando você definir uma região, lembre-se de que o Azure Cosmos DB respeita nuvens soberanas e governamentais. Ou seja, se você criar uma conta em uma região soberana, não poderá replicar fora da região soberana. Da mesma forma, você não pode habilitar a replicação em outros locais soberanos de uma conta externa. 

## <a name="develop-against-hello-documentdb-api"></a>Desenvolver Olá API DocumentDB

### <a name="how-do-i-start-developing-against-hello-documentdb-api"></a>Como iniciar o desenvolvimento em relação a saudação API DocumentDB?
API de documentos da Microsoft está disponível em Olá [portal do Azure][azure-portal]. Primeiro você deve se inscrever para uma assinatura do Azure. Quando você se inscrever para uma assinatura do Azure, você pode adicionar documentos API contêiner tooyour assinatura do Azure. Para obter instruções sobre como adicionar uma conta do Azure Cosmos DB, consulte [Criar uma conta de banco de dados do Azure Cosmos DB](create-documentdb-dotnet.md#create-account). Se você tiver uma conta do DocumentDB em Olá anterior, agora você tem uma conta de banco de dados do Azure Cosmos. 

[SDKs](documentdb-sdk-dotnet.md) estão disponíveis para .NET, Python, Node.js, JavaScript e Java. Os desenvolvedores também podem usar o hello [APIs de HTTP RESTful](/rest/api/documentdb/) toointeract com recursos de banco de dados do Azure Cosmos de várias plataformas e idiomas.

### <a name="can-i-access-some-ready-made-samples-tooget-a-head-start"></a>Posso acessar alguns tooget prontos exemplos como ponto de partida?
Exemplos de saudação API DocumentDB [.NET](documentdb-dotnet-samples.md), [Java](https://github.com/Azure/azure-documentdb-java), [Node.js](documentdb-nodejs-samples.md), e [Python](documentdb-python-samples.md) SDKs estão disponíveis no GitHub.


### <a name="does-hello-documentdb-api-database-support-schema-free-data"></a>Dá Olá livre de esquemas dados de suporte de banco de dados API de documentos?
Sim, Olá API DocumentDB permite que aplicativos toostore arbitrários documentos JSON sem definições de esquema ou dicas. Dados estão imediatamente disponíveis para consulta por meio da interface de consulta de banco de dados SQL do Azure Cosmos hello.  

### <a name="does-hello-documentdb-api-support-acid-transactions"></a>Olá API DocumentDB oferece suporte a transações ACID?
Sim, Olá API DocumentDB oferece suporte a transações de entre documentos expressadas como gatilhos e procedimentos armazenados de JavaScript. As transações são tooa única partição dentro de cada coleção de escopo e executado com a semântica ACID como "tudo ou nada," isolada de outras solicitações de usuário e código em execução simultaneamente. Se as exceções são geradas por meio da execução de lado do servidor de saudação do código do aplicativo JavaScript, transação inteira Olá será revertida. Para saber mais sobre transações, confira [Transações de programa de banco de dados](programming.md#database-program-transactions).

### <a name="what-is-a-collection"></a>O que é uma coleção?
Uma coleção é um grupo de documentos e sua lógica de aplicativo JavaScript associada. Uma coleção é uma entidade faturável, onde hello [custo](performance-levels.md) é determinado pela taxa de transferência hello e usou o armazenamento. Coleções podem abranger uma ou mais partições ou os servidores e pode ser dimensionado toohandle praticamente ilimitados volumes de armazenamento ou de taxa de transferência.

Coleções também são entidades de cobrança Olá para o banco de dados do Azure Cosmos. Cada coleção é cobrada por hora, com base na taxa de transferência provisionado hello e espaço de armazenamento usado. Para obter mais informações, consulte o [Preço do Azure Cosmos DB](https://azure.microsoft.com/pricing/details/cosmos-db/). 

### <a name="how-do-i-create-a-database"></a>Como crio um banco de dados?
Você pode criar bancos de dados usando Olá [portal do Azure](https://portal.azure.com), conforme descrito em [adicionar uma coleção](create-documentdb-dotnet.md#create-collection), uma saudação [SDKs do banco de dados do Azure Cosmos](documentdb-sdk-dotnet.md), ou hello [APIs REST](/rest/api/documentdb/). 

### <a name="how-do-i-set-up-users-and-permissions"></a>Como configuro usuários e permissões?
Você pode criar usuários e permissões usando uma saudação [SDKs de API de banco de dados do Cosmos](documentdb-sdk-dotnet.md) ou hello [APIs REST](/rest/api/documentdb/).  

### <a name="does-hello-documentdb-api-support-sql"></a>Olá API DocumentDB dá suporte a SQL?
Olá linguagem de consulta SQL é um avançada subconjunto da funcionalidade de consulta de saudação que é suportado pelo SQL. Olá linguagem de consulta de banco de dados SQL do Azure Cosmos fornece operadores relacionais e hierárquicos avançados e extensibilidade por meio de funções com base em JavaScript, definido pelo usuário (UDFs). Gramática JSON permite a modelagem documentos JSON como árvores conosco rotulados, que são usados por técnicas de indexação automática de banco de dados do Azure Cosmos hello e dialeto de consulta SQL de saudação do banco de dados do Azure Cosmos. Para obter informações sobre como usar a gramática de SQL, consulte Olá [QueryDocumentDB] [ query] artigo.

### <a name="does-hello-documentdb-api-support-sql-aggregation-functions"></a>Dá Olá funções de agregação de SQL de suporte de API de documentos?
Olá API DocumentDB oferece suporte à agregação de baixa latência em qualquer escala por meio de funções de agregação `COUNT`, `MIN`, `MAX`, `AVG`, e `SUM` via Olá gramática de SQL. Para saber mais, consulte [Funções de agregação](documentdb-sql-query.md#Aggregates).

### <a name="how-does-hello-documentdb-api-provide-concurrency"></a>Como Olá API DocumentDB fornece a simultaneidade?
Olá API DocumentDB oferece suporte a controle de simultaneidade otimista (OCC) por meio de marcas de entidade HTTP ou ETags. Cada recurso da API de documentos com uma ETag e Olá ETag está definido no servidor de saudação toda vez que um documento é atualizado. cabeçalho ETag de saudação e o valor atual da saudação são incluídos em todas as mensagens de resposta. ETags pode ser usadas com hello If-Match cabeçalho tooallow Olá server toodecide se um recurso deve ser atualizado. Olá valor If-Match é toobe de valor de ETag Olá comparado. Se Olá valor ETag corresponder servidor Olá valor de ETag, o recurso de Olá for atualizado. Se Olá ETag não estiver mais atual, o servidor de saudação rejeita operação Olá com um "HTTP 412 Falha de pré-condição" código de resposta. cliente Olá busca novamente Olá recurso tooacquire Olá valor atual de ETag para o recurso de saudação. Além disso, ETags pode ser usadas com toodetermine de cabeçalho If-None-Match Olá se um buscar novamente de um recurso é necessária.

a simultaneidade otimista toouse no .NET, use Olá [AccessCondition](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.accesscondition.aspx) classe. Para obter um exemplo .NET, consulte [Program.cs](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/DocumentManagement/Program.cs) no exemplo de DocumentManagement hello no GitHub.

### <a name="how-do-i-perform-transactions-in-hello-documentdb-api"></a>Como executar transações Olá API DocumentDB?
Olá API DocumentDB oferece suporte a transações integrada à linguagem por meio de procedimentos armazenados de JavaScript e gatilhos. Todas as operações de banco de dados dentro de scripts são executadas em isolamento de instantâneo. Se ele é uma coleção de partição única, execução de saudação é coleção toohello no escopo. Se coleção Olá estiver particionada, a execução de saudação será toodocuments com escopo definido por hello mesmo valor de chave de partição na coleção de saudação. Um instantâneo de versões do documento hello (ETags) é realizado no início de saudação da transação de saudação e confirmado somente se o script hello tiver êxito. Se Olá JavaScript gera um erro, transação Olá será revertida. Para obter mais informações, consulte a [Programação JavaScript do lado do servidor para o Azure Cosmos DB](programming.md).

### <a name="how-can-i-bulk-insert-documents-into-cosmos-db"></a>Como posso inserir documentos em massa no Cosmos DB?
Você pode fazer a inserção em massa documentos no Azure Cosmos DB de uma das duas maneiras:

* ferramenta de migração do Hello dados, conforme descrito em [ferramenta de migração do banco de dados para o banco de dados do Azure Cosmos](import-data.md).
* Procedimentos armazenados, conforme descrito em [Programação de JavaScript do lado do servidor para o Azure Cosmos DB](programming.md).

### <a name="does-hello-documentdb-api-support-resource-link-caching"></a>Olá API DocumentDB dá suporte a cache de link de recurso?
Sim. Como o Azure Cosmos DB é um serviço RESTful, os links de recursos são imutáveis e podem ser armazenados em cache. Clientes de API do DocumentDB podem especificar um "cabeçalho If-None-Match" para leituras em qualquer tipo de recurso de documento ou uma coleção e, em seguida, atualize suas cópias locais após a versão do servidor de saudação foi alterada.

### <a name="is-a-local-instance-of-documentdb-api-available"></a>Uma instância local da API do DocumentDB está disponível?
Sim. Olá [emulador de banco de dados do Azure Cosmos](local-emulator.md) emula uma alta fidelidade de saudação serviço de banco de dados do Cosmos. Ele oferece suporte à funcionalidade que é idêntica tooAzure Cosmos banco de dados, incluindo suporte para criar e consultar documentos JSON, provisionamento e coleções de dimensionamento e a execução de procedimentos armazenados e gatilhos. Você pode desenvolver e testar aplicativos usando hello Azure Cosmos DB emulador e implantá-las tooAzure em uma escala global, fazendo com que uma única configuração de alterar o ponto de extremidade de conexão de toohello para o banco de dados do Azure Cosmos.

## <a name="develop-against-hello-api-for-mongodb"></a>Desenvolver Olá API para o MongoDB
### <a name="what-is-hello-azure-cosmos-db-api-for-mongodb"></a>O que é hello Azure Cosmos DB API para o MongoDB?
Olá API de banco de dados do Azure Cosmos para o MongoDB é uma camada de compatibilidade que permite que aplicativos tooeasily e transparente se comunicar com o mecanismo de banco de dados do banco de dados do Azure Cosmos nativo hello usando existente, com suporte da comunidade Apache MongoDB APIs e os drivers. Os desenvolvedores agora podem usar o MongoDB ferramenta cadeias e habilidades toobuild aplicativos existentes que tiram proveito do banco de dados do Azure Cosmos. Os desenvolvedores se beneficiam da saudação recursos exclusivos do banco de dados do Azure Cosmos, que incluem a manutenção de indexação automática, o backup, contratos de nível de serviço com suporte financeiro (SLAs) e assim por diante.

### <a name="how-do-i-connect-toomy-api-for-mongodb-database"></a>Como conecto toomy API para o banco de dados do MongoDB?
Olá toohello de tooconnect forma mais rápida do Azure Cosmos DB API para o MongoDB é toohead pela toohello [portal do Azure](https://portal.azure.com). Vá tooyour conta e, em seguida, no menu de navegação à esquerda de saudação, clique em **início rápido**. Início rápido é Olá melhor maneira tooget código trechos tooconnect tooyour banco de dados. 

O Azure Cosmos DB impõe padrões e requisitos de segurança rígidos. Contas do Azure do banco de dados do Cosmos exigem autenticação e comunicação segura via SSL, portanto, se toouse TLSv1.2.

Para obter mais informações, consulte [conectar tooyour API para o banco de dados do MongoDB](connect-mongodb-account.md).

### <a name="are-there-additional-error-codes-for-an-api-for-mongodb-database"></a>Há códigos de erro adicionais para um banco de dados da API para MongoDB?
Em adição toohello MongoDB códigos de erro comuns, Olá MongoDB API tem seus próprios códigos de erro específica:


| Erro               | Código  | Descrição  | Solução  |
|---------------------|-------|--------------|-----------|
| TooManyRequests     | 16500 | número total de saudação de unidades de solicitação consumido excedeu Olá taxa de unidade de solicitação de provisionamento para a coleção de saudação e foi acelerado. | Considere a possibilidade de dimensionar a taxa de transferência de saudação da coleção de saudação do hello portal do Azure ou tentar novamente. |
| ExceededMemoryLimit | 16501 | Como um serviço multilocatário, a operação de saudação excedeu alocação de memória do cliente hello. | Reduzir o escopo de saudação da operação de saudação por meio de critérios de consulta mais restritivos ou entre em contato com o suporte da saudação [portal do Azure](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade). <br><br>Exemplo: *&nbsp;&nbsp;&nbsp;&nbsp;db.getCollection('users').aggregate([<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$match: {name: "Andy"}}, <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{$sort: {age: -1}}<br>&nbsp;&nbsp;&nbsp;&nbsp;])*) |

## <a name="develop-with-hello-table-api-preview"></a>Desenvolver com hello API de tabela (visualização)

### <a name="terms"></a>Termos 
Hello Azure Cosmos DB: API de tabela (visualização) se refere a oferta premium de toohello por banco de dados do Azure Cosmos para suporte de tabela anunciado na compilação de 2017. 

tabela padrão de saudação SDK é a tabela de armazenamento do Azure existente Olá SDK. 

### <a name="how-can-i-use-hello-new-table-api-preview-offering"></a>Como usar a nova oferta de API de tabela (visualização) Olá? 
Olá API de tabela de banco de dados do Azure Cosmos está disponível no hello [portal do Azure][azure-portal]. Primeiro você deve se inscrever para uma assinatura do Azure. Depois que você se inscrever, você pode adicionar uma conta de API de tabela de banco de dados do Azure Cosmos tooyour assinatura do Azure e, em seguida, adicione a conta de tooyour de tabelas. 

Durante o período de visualização hello, quando [SDKs](../cosmos-db/table-sdk-dotnet.md) estão disponíveis para .NET, você pode começar executando Olá [API tabela](../cosmos-db/create-table-dotnet.md) início rápido do artigo.

### <a name="do-i-need-a-new-sdk-toouse-hello-table-api-preview"></a>É necessário uma saudação de toouse SDK nova API de tabela (visualização)? 
Sim, Olá [tabela de armazenamento Premium do Windows Azure (visualização) SDK](https://www.nuget.org/packages/WindowsAzure.Storage-PremiumTable) está disponível no NuGet. Informações adicionais estão disponíveis em Olá [API .NET de tabela de banco de dados do Azure Cosmos: Baixe e notas de versão](https://github.com/Microsoft/azure-docs-pr/cosmos-db/table-sdk-dotnet.md) página. 

### <a name="how-do-i-provide-feedback-about-hello-sdk-or-bugs"></a>Como posso fornecer comentários sobre Olá SDK ou bugs?
Você pode compartilhar seus comentários em qualquer Olá maneiras a seguir:

* [Uservoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api)
* [Fórum do MSDN](https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=AzureDocumentDB)
* [Stackoverflow](http://stackoverflow.com/questions/tagged/azure-cosmosdb)

### <a name="what-is-hello-connection-string-that-i-need-toouse-tooconnect-toohello-table-api-preview"></a>O que é a cadeia de caracteres de conexão de saudação que eu preciso toouse tooconnect toohello API de tabela (visualização)?
cadeia de caracteres de conexão de saudação é:
```
DefaultEndpointsProtocol=https;AccountName=<AccountNamefromCosmos DB;AccountKey=<FromKeysPaneofCosmosDB>;TableEndpoint=https://<AccountNameFromDocumentDB>.documents.azure.com
```
Você pode obter a cadeia de caracteres de conexão Olá Olá chaves na página de no hello portal do Azure. 

### <a name="how-do-i-override-hello-config-settings-for-hello-request-options-in-hello-new-table-api-preview"></a>Como substituir o hello definições de configurações para opções de solicitação Olá Olá nova API de tabela (visualização)?
Para obter informações sobre definições de configuração, consulte [Recursos do Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). Você pode alterar configurações de hello, adicionando-tooapp.config na seção appSettings de saudação no aplicativo de cliente hello.

    <appSettings>
        <add key="TableConsistencyLevel" value="Eventual|Strong|Session|BoundedStaleness|ConsistentPrefix"/>
        <add key="TableThroughput" value="<PositiveIntegerValue"/>
        <add key="TableIndexingPolicy" value="<jsonindexdefn>"/>
        <add key="TableUseGatewayMode" value="True|False"/>
        <add key="TablePreferredLocations" value="Location1|Location2|Location3|Location4>"/>....
    </appSettings>


### <a name="are-there-any-changes-for-customers-who-are-using-hello-existing-standard-table-sdk"></a>Há alterações para clientes que estão usando a tabela padrão existente Olá SDK?
Nenhuma. Não há nenhuma alteração para clientes novos ou existentes que estão usando a tabela padrão existente Olá SDK. 

### <a name="how-do-i-view-table-data-that-is-stored-in-azure-cosmos-db-for-use-with-hello-table-api-review"></a>Como exibir dados de tabela que são armazenados no banco de dados do Azure Cosmos para uso com hello API de tabela (revisão)? 
Você pode usar dados de saudação do hello toobrowse portal do Azure. Você também pode usar o hello código da API de tabela (visualização) ou ferramentas de saudação mencionadas na resposta Avançar hello. 

### <a name="which-tools-work-with-hello-table-api-preview"></a>Quais ferramentas funcionam com hello API de tabela (visualização)? 
Você pode usar a versão mais antiga de saudação do Pesquisador de objetos do Azure (0.8.9).

Ferramentas com hello flexibilidade tootake uma cadeia de caracteres de conexão no formato de saudação especificado anteriormente pode dar suporte a Olá nova API de tabela (visualização). Uma lista de ferramentas de tabela é fornecida em Olá [ferramentas de cliente de armazenamento do Azure](../storage/common/storage-explorers.md) página. 

### <a name="do-powershell-or-azure-cli-work-with-hello-new-table-api-preview"></a>PowerShell ou CLI do Azure funciona com a API de tabela novo hello (visualização)?
Estamos planejando suporte tooadd PowerShell e a CLI do Azure para a API de tabela (visualização). 

### <a name="is-hello-concurrency-on-operations-controlled"></a>É a simultaneidade Olá em operações controladas?
Sim, a simultaneidade otimista é fornecida por meio do uso de saudação do mecanismo de ETag hello. 

### <a name="is-hello-odata-query-model-supported-for-entities"></a>É hello modelo de consulta OData com suporte para entidades? 
Sim, Olá API de tabela (visualização) dá suporte à consulta OData e consulta LINQ. 

### <a name="can-i-connect-toohello-standard-azure-table-and-hello-new-premium-table-api-preview-side-by-side-in-hello-same-application"></a>Posso conectar toohello tabelas padrão e premium nova API de tabela (visualização) lado a lado em Olá Olá mesmo aplicativo? 
Sim, você pode se conectar com a criação de duas instâncias separadas do hello CloudTableClient, cada uma apontando tooits possui URI pela cadeia de caracteres de conexão de saudação.

### <a name="how-do-i-migrate-an-existing-azure-table-storage-application-toothis-new-offering"></a>Como migrar uma existente tabela do Azure aplicativo toothis nova oferta de armazenamento?
tootake aproveitar a nova oferta de API de tabela Olá em seus dados de armazenamento de tabela existentes, entre em contato com [ askcosmosdb@microsoft.com ](mailto:askcosmosdb@microsoft.com). 

### <a name="what-is-hello-roadmap-for-this-service-and-when-will-you-offer-other-standard-table-api-functionality"></a>Qual o roteiro Olá para este serviço, e quando você oferecerá outra funcionalidade da API de tabela padrão?
Planejamos tooadd suporte para SAS tokens, ServiceContext, estatísticas, cliente lado criptografia, análise e outros recursos à medida que avança para GA. Você pode nos enviar comentários no [Uservoice](https://feedback.azure.com/forums/599062-azure-cosmos-db-table-api). 

### <a name="how-is-expansion-of-hello-storage-size-done-for-this-service-if-for-example-i-start-with-n-gb-of-data-and-my-data-will-grow-too1-tb-over-time"></a>Como é a expansão do tamanho de armazenamento Olá feito para esse serviço se, por exemplo, começam com * n * GB de dados e Meus dados crescerá too1 TB ao longo do tempo? 
Banco de dados do Azure Cosmos é projetado tooprovide armazenamento ilimitado por meio do uso de saudação de escala horizontal. serviço de saudação pode monitorar e efetivamente aumentar seu armazenamento. 

### <a name="how-do-i-monitor-hello-table-api-preview-offering"></a>Como monitorar a oferta de API de tabela (visualização) Olá?
Você pode usar o hello API de tabela (visualização) **métricas** painel toomonitor solicitações e utilização de armazenamento. 

### <a name="how-do-i-calculate-hello-throughput-i-require"></a>Como calcular a taxa de transferência Olá que preciso?
Você pode usar Olá capacidade avaliador toocalculate Olá TableThroughput necessária para operações de saudação. Para obter mais informações, consulte [Estimate Request Units and Data Storage](https://www.documentdb.com/capacityplanner) (Estimar Unidades de Solicitação e Armazenamento de Dados). Em geral, você pode representar a entidade como JSON e forneça os números de saudação de suas operações. 

### <a name="can-i-use-hello-new-table-api-preview-sdk-locally-with-hello-emulator"></a>É possível usar Olá nova API de tabela (visualização) SDK localmente com o emulador Olá?
Sim, você pode usar o hello API de tabela (visualização) com o emulador de local de hello quando você usar Olá novo SDK. emulador de nova toodownload, ir muito[Olá Use emulador do Azure Cosmos banco de dados para teste e desenvolvimento local](local-emulator.md). Olá valor StorageConnectionString em App. config precisa toobe:

```
DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=C2y6yDjf5/R+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw/Jw==;TableEndpoint=https://localhost:8081`. 
```

### <a name="can-my-existing-application-work-with-hello-table-api-preview"></a>Meu aplicativo existente pode funcionar com hello API de tabela (visualização)? 
área da superfície de Olá Olá nova API de tabela (visualização) é compatível com hello existente de tabela padrão do Azure SDK em Olá criar, excluir, atualizar e operações na API .NET do hello de consulta. Certifique-se de que você tem uma chave de linha, como Olá API de tabela (visualização) requer uma chave de partição e uma chave de linha. Também planejamos tooadd mais suporte do SDK como continuar para GA dessa oferta de serviço.

### <a name="do-i-need-toomigrate-my-existing-azure-table-based-applications-toohello-new-sdk-if-i-do-not-want-toouse-hello-table-api-preview-features"></a>É necessário toomigrate meu toohello aplicativos baseados em tabela do Azure existente novo SDK se eu não quero toouse recursos da API de tabela (visualização) de saudação?
Não, você pode criar e usar os ativos presentes da Tabela Standard sem nenhum tipo de interrupção. No entanto, se você não usar Olá nova API de tabela (visualização), você não pode se beneficiar do índice automáticas hello, opção de consistência adicionais hello ou distribuição global. 

### <a name="how-do-i-add-replication-of-hello-data-in-hello-premium-table-api-preview-across-multiple-regions-of-azure"></a>Como adicionar a replicação de dados de saudação do premium Olá API de tabela (visualização) por várias regiões do Azure?
Você pode usar do portal do Azure Cosmos DB Olá [as configurações de replicação global](tutorial-global-distribution-documentdb.md#portal) regiões tooadd adequados para seu aplicativo. toodevelop um aplicativo distribuído globalmente, você também deve adicionar seu aplicativo com hello PreferredLocation informações conjunto toohello região local para oferecer baixa latência de leitura. 

### <a name="how-do-i-change-hello-primary-write-region-for-hello-account-in-hello-premium-table-api-preview"></a>Como alterar a região de gravação primária Olá para conta de saudação do premium Olá API de tabela (visualização)?
Você pode usar o hello Azure Cosmos DB replicação global painel portal tooadd uma região e, em seguida, fazer failover região necessário toohello. Para obter instruções, consulte [Desenvolvendo com contas em várias regiões do Azure Cosmos DB](regional-failover.md). 

### <a name="how-do-i-configure-my-preferred-read-regions-for-low-latency-when-i-distribute-my-data"></a>Como fazer para configurar minhas regiões de leitura preferenciais com baixa latência ao distribuir meus dados? 
toohelp leiam localmente hello, use a chave de PreferredLocation de saudação no arquivo App. config de saudação. Para aplicativos existentes, Olá API de tabela (visualização) gera um erro se LocationMode for definido. Remova esse código, porque premium Olá API de tabela (visualização) seleciona essas informações no arquivo App. config de saudação. Para obter mais informações, consulte [Recursos do Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="how-should-i-think-about-consistency-levels-in-hello-table-api-preview"></a>Como deve pensar sobre os níveis de consistência no hello API de tabela (visualização)? 
O Azure Cosmos DB fornece compensações bem fundamentadas entre consistência, disponibilidade e latência. Banco de dados do Azure Cosmos oferece cinco níveis de consistência tooTable desenvolvedores de API (visualização), para que você pode escolher modelo de consistência direita Olá no nível de tabela hello e fazer solicitações individuais ao consultar dados de saudação. Quando um cliente se conecta, ele pode especificar um nível de consistência. Você pode alterar o nível de saudação por meio de configuração do hello App. config para o valor de saudação da chave de TableConsistencyLevel hello. 

Olá API de tabela (visualização) fornece baixa latência lê com "ler seus próprios gravações," com a coerência de sessão como padrão de saudação. Para obter mais informações, consulte [Níveis de consistência](consistency-levels.md). 

Por padrão, o armazenamento de tabela do Azure fornece consistência forte dentro de uma região e consistência Eventual em locais secundários hello. 

### <a name="does-azure-cosmos-db-offer-more-consistency-levels-than-standard-tables"></a>O Azure Cosmos DB oferece mais níveis de consistência do que as tabelas standard?
Sim, para obter informações sobre como toobenefit de saudação distribuídos a natureza do banco de dados do Azure Cosmos, consulte [níveis de consistência](consistency-levels.md). Porque garantias são fornecidas para níveis de consistência Olá, você pode usá-los com confiança. Para obter mais informações, consulte [Recursos do Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities).

### <a name="when-global-distribution-is-enabled-how-long-does-it-take-tooreplicate-hello-data"></a>Quando a distribuição global é habilitada, quanto tempo leva dados de saudação tooreplicate?
Podemos confirmar dados Olá forma duradoura na região local hello e enviar por push regiões de tooother dados Olá imediatamente em questão de milissegundos. Essa replicação depende apenas Olá ida e volta RTT (tempo) do hello datacenter. toolearn mais sobre a funcionalidade de distribuição global de saudação do Azure Cosmos DB, consulte [o banco de dados do Azure Cosmos: um serviço de banco de dados globalmente distribuídos no Azure](distribute-data-globally.md).

### <a name="can-hello-read-request-consistency-level-be-changed"></a>Nível de consistência de solicitação de leitura de saudação pode ser alterado?
Com o banco de dados do Azure Cosmos, você pode definir o nível de consistência de saudação no nível do contêiner de saudação (na tabela de saudação). Usando Olá SDK, você pode alterar o nível de hello, fornecendo o valor de saudação para TableConsistencyLevel chave no arquivo App. config de saudação. Olá os valores possíveis são: forte, envelhecimento limitado, sessão, prefixo consistente e Eventual. Para obter mais informações, consulte [Níveis ajustáveis de consistência de dados no Azure Cosmos DB](consistency-levels.md). ideia chave Olá é que você não pode definir consistência de solicitação Olá nível em mais de configuração de saudação para tabela hello. Por exemplo, você não pode definir Olá consistência para a tabela de saudação no Eventual Olá solicitação consistência nível e a forte. 

### <a name="how-does-hello-premium-table-api-preview-account-handle-failover-if-a-region-goes-down"></a>Como a conta de API de tabela (visualização) premium Olá tratar failover se uma região for desativada? 
premium Olá API de tabela (visualização) emprestada de plataforma globalmente distribuídos de saudação do banco de dados do Azure Cosmos. tooensure que seu aplicativo pode tolerar tempo de inatividade do datacenter, habilitar pelo menos uma região mais conta Olá no portal do Azure Cosmos DB Olá [desenvolvendo com contas de banco de dados do Azure Cosmos várias regiões](regional-failover.md). Você pode definir a prioridade de saudação da região hello usando o portal de saudação [desenvolvendo com contas de banco de dados do Azure Cosmos várias regiões](regional-failover.md). 

Você pode adicionar regiões quantas desejar para conta hello e controlar onde ele pode realizar o failover tooby fornecendo uma prioridade de failover. Obviamente, banco de dados toouse Olá, é necessário muito tooprovide existe um aplicativo. Quando você fizer isso, os clientes não terão o tempo de inatividade. SDK de cliente Olá é automaticamente hospedagem. Ou seja, ele pode detectar região Olá para baixo e automaticamente o failover toohello nova região.

### <a name="is-hello-premium-table-api-preview-enabled-for-backups"></a>Premium Olá API de tabela (visualização) está habilitada para backups?
Sim, premium Olá API de tabela (visualização) emprestada de plataforma de saudação do banco de dados do Azure Cosmos para backups. Os backups são feitos automaticamente. Para obter mais informações, consulte [Backup e restauração online com o Azure Cosmos DB](online-backup-and-restore.md).

 
### <a name="does-hello-table-api-preview-index-all-attributes-of-an-entity-by-default"></a>Olá API de tabela (visualização) indexa todos os atributos de uma entidade por padrão?
Sim, por padrão, todos os atributos de uma entidade são indexados. Para obter mais informações, consulte [Azure Cosmos DB: indexando políticas](indexing-policies.md). 

### <a name="does-this-mean-i-do-not-have-toocreate-multiple-indexes-toosatisfy-hello-queries"></a>Isso significa não têm toocreate vários índices toosatisfy Olá consultas? 
Sim, o Azure Cosmos DB fornece a indexação automática de todos os atributos sem nenhuma definição de esquema. Essa automação libera os desenvolvedores toofocus no aplicativo hello em vez de no gerenciamento e criação de índice. Para obter mais informações, consulte [Azure Cosmos DB: indexando políticas](indexing-policies.md).

### <a name="can-i-change-hello-indexing-policy"></a>Alterar política de indexação Olá?
Sim, você pode alterar a política de indexação hello, fornecendo a definição de índice de saudação. Para obter mais informações, consulte [Recursos do Azure Cosmos DB](../cosmos-db/tutorial-develop-table-dotnet.md#azure-cosmos-db-capabilities). Você precisa tooproperly codificar e configurações de saudação de escape. 

No formato json de cadeia de caracteres no arquivo App. config de saudação:
```
{
  "indexingMode": "consistent",
  "automatic": true,
  "includedPaths": [
    {
      "path": "/somepath",
      "indexes": [
        {
          "kind": "Range",
          "dataType": "Number",
          "precision": -1
        },
        {
          "kind": "Range",
          "dataType": "String",
          "precision": -1
        } 
      ]
    }
  ],
  "excludedPaths": 
[
 {
      "path": "/anotherpath"
 }
]
}
```

### <a name="azure-cosmos-db-as-a-platform-seems-toohave-lot-of-capabilities-such-as-sorting-aggregates-hierarchy-and-other-functionality-will-you-be-adding-these-capabilities-toohello-table-api"></a>Azure DB Cosmos como uma plataforma parece toohave vários recursos, como classificação, agregações, hierarquia e outras funcionalidades. Você adicionará essas toohello recursos API tabela? 
Na visualização, Olá API tabela fornece Olá mesma funcionalidade como armazenamento de tabela do Azure de consulta. O Azure Cosmos DB também oferece suporte à classificação, agregações, consulta geoespacial, hierarquia e uma ampla variedade de funções internas. Forneceremos uma funcionalidade adicional no hello API de tabela em uma atualização futura do serviço. Para obter mais informações, consulte [Consultas SQL para a API do DocumentDB do Azure Cosmos DB](../documentdb/documentdb-sql-query.md).
 
### <a name="when-should-i-change-tablethroughput-for-hello-table-api-preview"></a>Quando devo alterar TableThroughput para Olá API de tabela (visualização)?
Você deve alterar TableThroughput quando se aplica uma saudação condições a seguir:
* Você estiver executando uma extração, transformação e carregamento (ETL) de dados, ou quiser tooupload muitos dados em um curto período de tempo. 
* Você precisa de mais taxa de transferência do contêiner de saudação no back-end hello. Por exemplo, você verá que taxa de transferência de Olá usada é maior que a taxa de transferência fornecida Olá, e você estiver obtendo limitadas. Para obter mais informações, consulte [Definir a taxa de transferência para contêineres do Azure Cosmos DB](set-throughput.md).

### <a name="can-i-scale-up-or-scale-down-hello-throughput-of-my-table-api-preview-table"></a>Pode aumentar ou reduzir a taxa de transferência de saudação de minha tabela de API de tabela (visualização)? 
Sim, você pode usar a taxa de transferência do portal do Azure Cosmos DB Olá escala painel tooscale hello. Para obter mais informações, veja [Configurar produtividade](set-throughput.md).

### <a name="is-a-default-tablethroughput-set-for-newly-provisioned-tables"></a>Há uma configuração padrão de TableThroughput para as tabelas recém-provisionadas?
Sim, se você não substituir Olá TableThroughput via App. config e não use um contêiner criado previamente no banco de dados do Azure Cosmos, o serviço Olá cria uma tabela com taxa de transferência de 400.
 
### <a name="is-there-any-change-of-pricing-for-existing-customers-of-hello-standard-table-api"></a>Há qualquer alteração de preços para os clientes atuais do API de tabela padrão Olá?
Nenhuma. Não há nenhuma alteração de preço para aqueles que já são clientes da API de Tabela Standard. 

### <a name="how-is-hello-price-calculated-for-hello-table-api-preview"></a>Como o preço de saudação é calculado para Olá API de tabela (visualização)? 
preço de saudação depende Olá alocada TableThroughput. 

### <a name="how-do-i-handle-any-throttling-on-hello-tables-in-table-api-preview-offering"></a>Como manipular qualquer limitação nas tabelas de saudação na API de tabela (visualização) oferece? 
Se taxa de solicitação de saudação excede a capacidade de saudação de taxa de transferência provisionado Olá para o contêiner subjacente Olá, você obterá um erro e Olá SDK tentará Olá chamada Aplicando política de repetição de saudação.

### <a name="why-do-i-need-toochoose-a-throughput-apart-from-partitionkey-and-rowkey-tootake-advantage-of-hello-premium-table-api-preview-offering-of-azure-cosmos-db"></a>Por que preciso toochoose além PartitionKey e RowKey vantagem tootake de oferta de API de tabela (visualização) premium Olá do banco de dados do Azure Cosmos uma taxa de transferência?
Banco de dados do Azure Cosmos define uma taxa de transferência padrão para o contêiner se você não fornecer um arquivo App. config de saudação. 

O Azure Cosmos DB fornece garantias de desempenho e latência com limites superiores na operação. Essa garantia é possível quando o mecanismo Olá pode aplicar governança em operações do locatário hello. Configuração TableThroughput garante que você obtenha Olá garantia de taxa de transferência e latência, como plataforma Olá reserva essa capacidade e garante sucesso operacional. 

Usando a especificação de taxa de transferência hello, elasticidade altere toobenefit de periodicidade de saudação do seu aplicativo, atendam às necessidades de produção de hello e economizar custos.

### <a name="azure-storage-sdk-has-been-very-inexpensive-for-me-because-i-pay-only-toostore-hello-data-and-i-rarely-query-hello-new-azure-cosmos-db-offering-seems-toobe-charging-me-even-though-i-have-not-performed-a-single-transaction-or-stored-anything-can-you-please-explain"></a>SDK de armazenamento do Azure foi muito baixo custo, porque eu pagar apenas os dados de saudação toostore e raramente de consulta. nova oferta de banco de dados do Azure Cosmos Olá parece toobe Carregando me mesmo que eu não executada uma única transação ou armazenados nada. Vocês podem explicar?

Banco de dados do Azure Cosmos é projetado toobe um sistema globalmente distribuído baseados em SLA com garantia de disponibilidade, latência e taxa de transferência. Quando você reservar a taxa de transferência de banco de dados do Azure Cosmos, é garantido, ao contrário de taxa de transferência de saudação de outros sistemas. O Azure Cosmos DB fornece recursos adicionais que os clientes solicitaram, como índices secundários e distribuição global. Durante o período de visualização hello, fornecemos um modelo de otimização de taxa de transferência e, eventualmente, estamos planejando tooprovide toomeet um modelo de otimização de armazenamento necessidades de nossos clientes. 

### <a name="i-never-get-a-quota-full-notification-indicating-that-a-partition-is-full-when-i-ingest-data-into-table-storage-with-hello-table-api-preview-i-do-get-this-message-is-this-offering-limiting-me-and-forcing-me-toochange-my-existing-application"></a>Eu nunca recebi uma notificação de “cota cheia” (indicando que uma partição está cheia) quando realizo a ingestão de dados no armazenamento de tabelas. Com hello API de tabela (visualização), recebo a seguinte mensagem. Essa oferta limitando-me e forçando-me toochange meu aplicativo?

O Azure Cosmos DB é um sistema baseado em SLA que fornece escala ilimitada com garantias de latência, produtividade, disponibilidade e consistência. tooensure garantia de desempenho premium, certifique-se de que o tamanho dos dados e índice são gerenciáveis e escalonáveis. limite de 10 GB de Olá Olá número de entidades ou itens por chave de partição é tooensure que fornecemos ótimo desempenho de consulta e de pesquisa. tooensure que seu aplicativo dimensione bem até mesmo para o armazenamento do Azure, é recomendável que você *não* criar uma partição ativa, armazenando todas as informações em uma partição e consultá-los. 

### <a name="so-partitionkey-and-rowkey-are-still-required-with-hello-new-table-api-preview"></a>Para a PartitionKey e RowKey ainda são necessárias com hello nova API de tabela (visualização)? 
Sim. Porque a área de superfície de saudação do hello API de tabela (visualização) for toothat semelhante de saudação SDK de armazenamento de tabela, chave de partição Olá fornece um modo eficiente toodistribute Olá de dados. chave de linha de saudação é exclusivo dentro dessa partição. Olá linha principais necessidades toobe presente e não pode ser nulo como em Olá SDK padrão. comprimento de saudação do RowKey é de 255 bytes e comprimento de saudação da PartitionKey é 100 bytes (em breve toobe aumentado too1 KB). 

### <a name="what-are-hello-error-messages-for-hello-table-api-preview"></a>Quais são as mensagens de erro de saudação do hello API de tabela (visualização)?
Porque essa visualização é compatível com a tabela de saudação padrão, a maioria dos erros de saudação mapeará toohello erros da tabela de saudação padrão. 

### <a name="why-do-i-get-throttled-when-i-try-toocreate-lot-of-tables-one-after-another-in-hello-table-api-preview"></a>Por que obter limitado quando tento toocreate muitas tabelas após o outro no hello API de tabela (visualização)?
O Azure Cosmos DB é um sistema baseado em SLA que fornece garantia de latência, produtividade, disponibilidade e consistência. Porque é um sistema configurado, ele reserva recursos tooguarantee esses requisitos. taxa de saudação rápida de criação de tabelas é detectada e limitada. É recomendável que você examine a taxa de saudação de criação de tabelas e reduzi-lo tooless que 5 por minuto. Lembre-se de que Olá API de tabela (visualização) é um sistema provisionado. momento Olá provisioná-la, você começará toopay para ele. 

## <a name="develop-against-hello-graph-api-preview"></a>Desenvolver Olá Graph API (visualização)
### <a name="how-can-i-apply-hello-functionality-of-graph-api-preview-tooazure-cosmos-db"></a>Como posso aplicar a funcionalidade de saudação do Graph API (visualização) tooAzure Cosmos DB?
Você pode usar uma extensão biblioteca tooapply Olá a funcionalidade da API do Graph (visualização). Essa biblioteca é chamada de Gráficos do Microsoft Azure e está disponível no NuGet. 

### <a name="it-looks-like-you-support-hello-gremlin-graph-traversal-language-do-you-plan-tooadd-more-forms-of-query"></a>Parece que você oferece suporte a idioma de passagem Olá Gremlin gráfico. Você planeja tooadd mais formas de consulta?
Sim, estamos planejando tooadd outros mecanismos para consulta no hello futuras. 

### <a name="how-can-i-use-hello-new-graph-api-preview-offering"></a>Como usar a nova oferta de API do Graph (visualização) Olá? 
saudação de Introdução, completa tooget [API do Graph](../cosmos-db/create-graph-dotnet.md) início rápido do artigo.

<a id="moving-to-cosmos-db"></a>
## <a name="questions-from-documentdb-customers"></a>Perguntas de clientes do DocumentDB
### <a name="why-are-you-moving-tooazure-cosmos-db"></a>Por que você está movendo tooAzure Cosmos DB? 

Banco de dados do Azure Cosmos é Olá próximo grande melhoria nos bancos de dados de nuvem em escala global distribuídas. Como um cliente de documentos, agora você tem acesso toohello inovador sistema e os recursos oferecidos pelo Azure Cosmos DB.

Banco de dados do Azure Cosmos iniciado como "Florence de projeto" no 2010 nos pontos problemáticos de saudação tooaddress enfrentados pelos desenvolvedores na criação de aplicativos em larga escala dentro da Microsoft. desafios de saudação da criação de aplicativos distribuídos globalmente não são exclusivo tooMicrosoft, é disponibilizada Olá primeira geração dessa tecnologia de 2015 tooAzure desenvolvedores no formulário de saudação do DocumentDB do Azure. 

Desde então, nós adicionados novos recursos e aumentamos a gama de possibilidades. Banco de dados do Azure Cosmos é resultado de saudação. Como parte desta versão, os clientes do DocumentDB, com seus dados, automática e totalmente se tornaram clientes do Azure Cosmos DB. Esses recursos estão em áreas de saudação do mecanismo de banco de dados principal Olá, bem como distribuição global, escalabilidade elástica e SLAs do setor e abrangentes. Especificamente, podemos evoluíram o mapa de tooefficiently de mecanismo do hello Azure Cosmos DB banco de dados todos os modelos de dados populares, sistemas de tipos e APIs toohello modelo de dados do banco de dados do Azure Cosmos. 

Olá, manifestação de voltados para o desenvolvedor atual desse trabalho é novo suporte a saudação de [Gremlin](../cosmos-db/graph-introduction.md) e [APIs de armazenamento de tabela](../cosmos-db/table-introduction.md). E este é o início de saudação apenas. Planejamos tooadd outras APIs populares e modelos de dados mais recentes ao longo do tempo, com os avanços mais no desempenho e armazenamento em escala global. 

É importante toopoint out que Olá DocumentDB [dialeto SQL](../documentdb/documentdb-sql-query.md) sempre foi apenas um dos Olá várias APIs que hello Azure Cosmos DB subjacente pode dar suporte. Para desenvolvedores que usam um serviço totalmente gerenciado, como o banco de dados do Azure Cosmos, hello apenas o serviço de toohello de interface é hello APIs que são expostos pelo serviço de saudação. Nada muda realmente para os clientes existentes do DocumentDB. Banco de dados do Azure Cosmos, você obtém exatamente Olá que SQL mesmo API que DocumentDB oferece. E agora (e em futuras de saudação), você pode acessar outros recursos anteriormente inacessíveis 

Outra manifestação de nosso trabalho contínuo é a base de saudação estendida escalabilidade global e flexível de taxa de transferência e armazenamento. Fizemos vários aprimoramentos fundamentais toohello subsistema de distribuição global. Uma saudação muitos recursos voltados para o desenvolvedor é Olá prefixo consistente modelo de consistência, que faz com que um total cinco modelos de consistência bem definidos. Lançaremos muitos outros recursos interessantes quando estiverem perfeitamente desenvolvidos. 

### <a name="what-do-i-need-toodo-tooensure-that-my-documentdb-resources-continue-toorun-on-azure-cosmos-db"></a>O que eu preciso tooensure toodo que meus recursos DocumentDB continuam toorun no banco de dados do Azure Cosmos?

Você não precisa nenhuma alteração de toomake em todos os. Os recursos de DocumentDB agora são recursos de banco de dados do Azure Cosmos e houve sem interrupção do serviço de saudação quando essa mudança ocorreu.

### <a name="what-changes-do-i-need-toomake-for-my-app-toowork-with-azure-cosmos-db"></a>O que fazem alterações necessário toomake para toowork meu aplicativo com o banco de dados do Azure Cosmos?

Não há nenhum toomake de alterações. Nomes de pacote do NuGet, namespaces e classes não foram alterados. Como sempre, é recomendável que você mantenha sua SDKs backup toodate tootake proveito dos aprimoramentos e recursos mais recentes de saudação. 

### <a name="whats-changed-in-hello-azure-portal"></a>O que mudou no hello portal do Azure?

Documentos não aparecerá mais no portal de saudação como um serviço do Azure. Em seu lugar é um novo ícone de banco de dados do Azure Cosmos, conforme mostrado na Olá a imagem a seguir. Todas as coleções estão disponíveis, como sempre estiveram e você ainda pode dimensionar a produtividade, alterar os níveis de consistência e monitorar SLAs. recursos de saudação do Gerenciador de dados (visualização) foram aperfeiçoados. Você pode exibir e editar documentos, criar e executar consultas e trabalhar com procedimentos armazenados, disparadores e da UDF de uma página, conforme mostrado no Olá a imagem a seguir: 

![folha de coleções de banco de dados do Azure Cosmos Olá](./media/faq/cosmos-db-data-explorer.png)

### <a name="are-there-changes-toopricing"></a>Há alterações toopricing?

Não, custo Olá executar seu aplicativo no banco de dados do Azure Cosmos é Olá mesmo antes.

### <a name="are-there-changes-toohello-slas"></a>Há alterações toohello SLAs?

Não, hello SLAs para disponibilidade, consistência, latência e taxa de transferência permanecerão inalteradas e ainda são exibidos no portal de saudação. Para obter mais informações, veja [SLA para Azure Cosmos DB](https://azure.microsoft.com/support/legal/sla/cosmos-db/).
   
![Aplicativo de tarefas pendentes com os dados de exemplo](./media/faq/azure-cosmosdb-portal-metrics-slas.png)


[azure-portal]: https://portal.azure.com
[query]: documentdb-sql-query.md
