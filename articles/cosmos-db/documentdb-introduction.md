---
title: 'Azure Cosmos DB: API do DocumentDB | Microsoft Docs'
description: "Saiba como você pode usar o banco de dados do Azure Cosmos toostore e consultar grandes volumes de documentos JSON com baixa latência usando SQL e JavaScript."
keywords: banco de dados JSON, banco de dados de documentos
services: cosmos-db
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 686cdd2b-704a-4488-921e-8eefb70d5c63
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/22/2017
ms.author: mimig
ms.openlocfilehash: c96dfa5e2685782a99d2bcaf992f88dd2bef920b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooazure-cosmos-db-documentdb-api"></a>Introdução tooAzure Cosmos DB: API de documentos

O [Azure Cosmos DB](introduction.md) é o serviço multimodelo de banco de dados da Microsoft, distribuído globalmente, para aplicativos críticos. Banco de dados do Azure Cosmos fornece [distribuição global turnkey](distribute-data-globally.md), [dimensionamento Elástico de taxa de transferência e armazenamento](partition-data.md) latências de milissegundo em todo o mundo, dígito no percentual de 99th hello, [cinco níveis de consistência bem definidos](consistency-levels.md)e a garantia de alta disponibilidade, apoiada por [SLAs do setor](https://azure.microsoft.com/support/legal/sla/cosmos-db/). Banco de dados do Azure Cosmos [indexa automaticamente os dados](http://www.vldb.org/pvldb/vol8/p1668-shukla.pdf) sem exigir que você toodeal com o gerenciamento de esquema e de índice. Ele tem vários modelos e suporta modelos de dados de colunas, gráficos, valores-chave e documentos. 

![API do Azure DocumentDB](./media/documentdb-introduction/cosmosdb-documentdb.png) 

Com hello API DocumentDB, o banco de dados do Azure Cosmos fornece avançada e familiar [capacidades de consulta SQL](documentdb-sql-query.md) com latência baixa consistente sobre os dados JSON sem esquema. Neste artigo, nós fornecemos uma visão geral do hello Azure Cosmos DB API DocumentDB e como você pode usá-lo toostore grandes volumes de dados JSON, consultá-los em ordem de latência de milissegundos e evoluir esquema Olá facilmente. 

## <a name="what-capabilities-and-key-features-does-azure-cosmos-db-offer"></a>Quais benefícios e os principais recursos que o Azure Cosmos DB oferece?
DB de Cosmos do Azure, por meio de saudação API DocumentDB, oferece Olá principais recursos e benefícios a seguir:

* **Taxa de transferência de forma escalonável e armazenamento:** facilmente aumentar ou reduzir sua toomeet de banco de dados JSON em que seu aplicativo precisa. Os dados são armazenados em SSD (discos de estado sólido) para fornecer latências baixas previsíveis. Banco de dados do Azure Cosmos oferece suporte a contêineres para armazenar dados JSON chamado coleções que podem ser dimensionado toovirtually tamanhos de armazenamento ilimitado e taxa de transferência fornecida. Você pode dimensionar elasticamente o Azure Cosmos DB com desempenho previsível à medida que o aplicativo cresce. 


* **Replicação de várias regiões:** Azure Cosmos DB transparentemente replica seu tooall as regiões de dados que você associou com sua conta do banco de dados do Azure Cosmos, permitindo que você toodevelop aplicativos que exigem acesso global toodata proporcionando Alternar entre consistência, disponibilidade e desempenho, todos com garantias correspondentes. Banco de dados do Azure Cosmos fornece failover transparente de regional com APIs de hospedagem múltipla e a taxa de transferência da escala tooelastically Olá capacidade e armazenamento globo hello. Saiba mais em [Como distribuir dados globalmente com o Azure Cosmos DB](distribute-data-globally.md).

* **Consultas ad hoc com sintaxe SQL familiar:** armazene documentos JSON heterogêneos e consulte-os com uma sintaxe SQL familiar. Banco de dados do Azure Cosmos utiliza um bloqueio de nível de simultaneidade, livre, log estruturado de índice de tooautomatically tecnologia indexação todo o conteúdo de documento. Isso permite consultas em tempo real avançadas sem dicas de esquema Olá necessidade toospecify, índices secundários ou modos de exibição. Saiba mais em [Consulta do Azure Cosmos DB](documentdb-sql-query.md). 
* **Execução de JavaScript no banco de dados de saudação:** Express lógica do aplicativo, como procedimentos armazenados, gatilhos e funções definidas pelo usuário (UDFs) usando JavaScript padrão. Isso permite que seu toooperate de lógica de aplicativo sobre dados sem se preocupar incompatibilidade Olá entre o aplicativo hello e o esquema de banco de dados de saudação. Olá API DocumentDB fornece uma execução transacional JavaScript da lógica de aplicativo diretamente no mecanismo de banco de dados de saudação. integração profunda de saudação do JavaScript permite a execução de saudação de operações de inserção, substituição, DELETE e SELECT de dentro de um programa JavaScript como uma transação a isoladas. Saiba mais em [Programação no lado servidor do DocumentDB](programming.md).

* **Níveis de consistência ajustáveis:** Select de cinco bem definidas compensação ideal de tooachieve do níveis de consistência entre a consistência e desempenho. Para operações de consulta e leitura, o Azure Cosmos DB oferece cinco níveis de consistência diferentes: forte, desatualização limitada, sessão, prefixo constante e eventual. Esses níveis de consistência bem definidos, granular permitem toomake som prós e contras latência, a disponibilidade e a consistência. Saiba mais em [usar consistência níveis de desempenho e disponibilidade de toomaximize](consistency-levels.md).

* **Totalmente gerenciado:** eliminar Olá necessidade toomanage banco de dados e máquina recursos. Como um serviço do Microsoft Azure totalmente gerenciado, você faça não necessidade toomanage VMs, implanta e configurar o software, gerenciar dimensionamento ou lida com as atualizações da camada de dados complexos. Cada banco de dados é salvo em backup automaticamente e protegido contra falhas regionais. Você pode facilmente adicionar uma conta de banco de dados do Azure Cosmos e provisionar capacidade conforme necessário, permitindo que você toofocus em seu aplicativo em vez de operar e gerenciar seu banco de dados. 

* **Aberto pelo design:** comece a usar o Banco de Dados de Documentos rapidamente, com habilidades e ferramentas já existentes. Programar Olá API DocumentDB é simples e acessível e não requerem que você tooadopt novas ferramentas ou aderir toocustom extensões tooJSON ou JavaScript. Você pode acessar toda a funcionalidade de banco de dados de saudação incluindo CRUD, consulta e processamento em uma interface simples de HTTP RESTful de JavaScript. Olá API DocumentDB adote formatos existentes, linguagens e padrões, oferecendo recursos de banco de dados-los de alto valor.

* **A indexação automática:** por padrão, o banco de dados do Azure Cosmos automaticamente indexa todos os documentos de saudação no banco de dados de saudação e não espera nem exigir qualquer esquema ou a criação de índices secundários. Não quer tooindex tudo? Não se preocupe, você também pode [recusar caminhos nos arquivos JSON](indexing-policies.md) .

* **Suporte de feed de alteração:** feed de alteração fornece uma lista ordenada de documentos em uma coleção de banco de dados do Azure Cosmos na ordem de saudação na qual elas foram modificadas. Este feed pode ser usado toolisten para toodata modificações nos dados de tooreplicate ordem, disparar chamadas de API ou executar o processamento de fluxo em atualizações. Feed de alterações é habilitado automaticamente e fácil toouse: [saber mais sobre como alterar o feed](https://docs.microsoft.com/azure/cosmos-db/change-feed). 

## <a name="data-management"></a>Como gerenciar dados com hello API DocumentDB?
Olá API DocumentDB ajuda a gerenciar dados JSON por meio de recursos de banco de dados bem definido. Esses recursos são replicados para alta disponibilidade e são endereçáveis exclusivamente por seu URI lógico. Olá API DocumentDB oferece um HTTP simple com base em modelo de programação RESTful para todos os recursos. 


conta de banco de dados do banco de dados do Azure Cosmos Olá é um namespace exclusivo que lhe dá acesso tooAzure Cosmos DB. Antes de criar uma conta de banco de dados, você deve ter uma assinatura do Azure, que dá a você acessar tooa variedade de serviços do Azure. 

Todos os recursos do Azure Cosmos DB são modelados e armazenados como documentos JSON. Os recursos são gerenciados como itens, que são documentos JSON contendo metadados e como feeds que são coleções de itens. Conjuntos de itens estão contidos dentro de seus respectivos feeds.

imagem de saudação abaixo mostra as relações de saudação entre os recursos de banco de dados do Azure Cosmos Olá:

![relação hierárquica entre os recursos no banco de dados do Azure Cosmos Olá][1] 

Uma conta do banco de dados é formada por um conjunto de bancos de dados, cada um contendo diversas coleções, cada uma delas pode conter procedimentos armazenados, gatilhos, UDFs, documentos e anexos relacionados. Um banco de dados também tem usuários associados, cada um com um conjunto de permissões tooaccess várias outras coleções, procedimentos armazenados, disparadores, UDFs, documentos ou anexos. Enquanto bancos de dados, usuários, permissões e coleções são recursos definidos pelo sistema com esquemas bastante conhecidos, os documentos, procedimentos armazenados, gatilhos, UDFs e anexos possuem conteúdo JSON arbitrário e definido pelo usuário.  

> [!NOTE]
> Como Olá API DocumentDB estava disponível anteriormente como Olá serviço DocumentDB do Azure, você pode continuar tooprovision, monitorar e gerenciar as contas criadas por meio de saudação do Azure API de REST de gerenciamento de recursos ou ferramentas usando Olá DocumentDB do Azure ou o banco de dados do Azure Cosmos nomes de recursos. Usamos os nomes de saudação alternadamente quando se referirem toohello APIs do DocumentDB do Azure. 

## <a name="develop"></a>Como é possível desenvolver aplicativos com hello API DocumentDB?

Banco de dados do Azure Cosmos expõe recursos por meio de saudação APIs REST que pode ser chamado por qualquer linguagem capaz de fazer solicitações HTTP/HTTPS. Além disso, nós oferecemos bibliotecas de programação para vários idiomas populares para Olá API DocumentDB. bibliotecas de cliente Olá simplificam muitos aspectos de trabalhar com hello API ao manipular detalhes de como o cache de endereço, gerenciamento de exceções, novas tentativas automáticas e assim por diante. Bibliotecas estão disponíveis atualmente para Olá plataformas e idiomas a seguir:  

| Baixar | Documentação |
| --- | --- |
| [SDK .NET](http://go.microsoft.com/fwlink/?LinkID=402989) |[Biblioteca .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) |
| [SDK do Node.js](http://go.microsoft.com/fwlink/?LinkID=402990) |[Biblioteca do Node.js](http://azure.github.io/azure-documentdb-node/) |
| [Java SDK](http://go.microsoft.com/fwlink/?LinkID=402380) |[Biblioteca do Java](/java/api/com.microsoft.azure.documentdb) |
| [SDK do JavaScript](http://go.microsoft.com/fwlink/?LinkID=402991) |[Biblioteca do JavaScript](http://azure.github.io/azure-documentdb-js/) |
| n/d |[SDK do JavaScript do lado servidor](http://azure.github.io/azure-documentdb-js-server/) |
| [SDK do Python](https://pypi.python.org/pypi/pydocumentdb) |[Biblioteca do Python](http://azure.github.io/azure-documentdb-python/) |
| n/d | [API para MongoDB](mongodb-introduction.md)


Usando Olá [emulador de banco de dados do Azure Cosmos](local-emulator.md), você pode desenvolver e testar seu aplicativo localmente com hello API DocumentDB, sem criar uma assinatura do Azure ou incorrer em todos os custos. Quando estiver satisfeito com o funcionamento seu aplicativo no emulador hello, você pode alternar toousing uma conta de banco de dados do Azure Cosmos na nuvem hello.

Além do basic criar, ler, atualizar e excluir operações, Olá API DocumentDB fornece uma interface de consulta avançada do SQL para recuperar documentos JSON e suporte do servidor para execução transacional da lógica do aplicativo JavaScript. interfaces de execução de consulta e script Hello estão disponíveis por meio de todas as bibliotecas de plataforma, bem como Olá APIs REST. 

### <a name="sql-query"></a>Consulta SQL
Olá API DocumentDB oferece suporte a consultar documentos JavaScript usando uma linguagem SQL, que está enraizada no hello digite sistema e expressões com suporte para consultas relacionais, espaciais e hierárquicas. linguagem de consulta do DocumentDB Olá é simples e poderosas interface tooquery JSON documentos. idioma Olá suporta um subconjunto de gramática SQL ANSI e adiciona integração profunda do objeto, matrizes, construção de objeto e invocação de função JavaScript. Olá API DocumentDB fornece seu modelo de consulta sem qualquer esquema explícito ou dicas de indexação de desenvolvedor hello.

Funções definidas pelo usuário (UDFs) pode ser registradas com hello API DocumentDB e referenciadas como parte de uma consulta SQL, estendendo assim a lógica de aplicativo personalizado em toosupport Olá gramática. Esses UDFs são gravados como programas de JavaScript e executados no banco de dados de saudação. 

Para desenvolvedores .NET, Olá API DocumentDB [.NET SDK](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.linq.aspx) também oferece um provedor de consulta LINQ. 

### <a name="transactions-and-javascript-execution"></a>Execução de transações e do JavaScript
Olá API DocumentDB permite que você toowrite a lógica do aplicativo como programas nomeados escritos inteiramente em JavaScript. Esses programas são registrados para uma coleção e podem executar operações de banco de dados em documentos hello dentro de uma determinada coleção. O JavaScript pode ser registrado para execução como gatilho, procedimento armazenado ou função definida pelo usuário (UDF). Procedimentos armazenados e gatilhos podem criar, ler, atualizar e excluir documentos enquanto executar funções definidas pelo usuário como parte da lógica de execução de consulta Olá sem acesso de gravação toohello coleção.

Execução de JavaScript em Olá Cosmos DB é modelada conceitos Olá suportados por sistemas de banco de dados relacional, com JavaScript como uma substituição moderna para o Transact-SQL. Toda lógica do JavaScript é executada em uma transação ACID ambiente com isolamento de instantâneo. Durante o curso de saudação de sua execução, se Olá JavaScript lança uma exceção, em seguida, Olá toda transação foi anulada.

## <a name="are-there-any-online-courses-on-azure-cosmos-db"></a>Há algum processo online no Azure Cosmos DB?

Sim, há um curso da [Microsoft Virtual Academy](https://mva.microsoft.com/en-US/training-courses/azure-documentdb-planetscale-nosql-16847) sobre o Azure DocumentDB. 

>[!VIDEO https://mva.microsoft.com/en-US/training-courses-embed/azure-documentdb-planetscale-nosql-16847]
>
>

## <a name="next-steps"></a>Próximas etapas
Já possui uma conta do Azure? Em seguida, acompanhe os nossos [Inícios rápidos](../cosmos-db/create-documentdb-dotnet.md), que exibem um passo a passo sobre a criação de uma conta e a introdução ao Azure Cosmos DB.

[1]: ./media/documentdb-introduction/json-database-resources1.png

