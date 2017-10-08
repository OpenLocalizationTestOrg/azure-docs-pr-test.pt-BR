---
title: dicas de aaaPerformance - Azure Cosmos banco de dados NoSQL | Microsoft Docs
description: "Saiba o desempenho do banco de dados do cliente configuração Opções tooimprove Azure Cosmos DB"
keywords: como tooimprove desempenho banco de dados
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
documentationcenter: 
ms.assetid: 94ff155e-f9bc-488f-8c7a-5e7037091bb9
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/23/2017
ms.author: mimig
ms.openlocfilehash: 4f3e82ae5048e3dbc20b0fd891a2d3aa22adf3fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-tips-for-azure-cosmos-db"></a>Dicas de desempenho para o Azure Cosmos DB
O Azure Cosmos DB é um banco de dados distribuído rápido e flexível que pode ser dimensionado perfeitamente com garantia de latência e produtividade. Você não tem alterações de arquitetura principais toomake ou escrever códigos complexos tooscale seu banco de dados com o banco de dados do Cosmos. Aumentar e reduzir é tão fácil quanto fazer uma única chamada da API ou uma [chamada do método do SDK](set-throughput.md#set-throughput-sdk). No entanto, porque Cosmos DB é acessado por meio de chamadas de rede existe são otimizações do lado do cliente pode fazer tooachieve máximo desempenho.

Assim, se você estiver se perguntando "Como posso melhorar o desempenho do meu banco de dados?", Considere Olá as opções a seguir:

## <a name="networking"></a>Rede
<a id="direct-connection"></a>

1. **Política de conexão: usar o modo de conexão direta**

    Como um cliente se conecta tooCosmos banco de dados tem implicações importantes sobre o desempenho, especialmente em termos de latência do cliente observado. Há duas configurações de chave de configuração disponíveis para configurar a diretiva de Conexão-conexão de saudação do cliente *modo* e hello [conexão *protocolo*](#connection-protocol).  Olá dois modos disponíveis são:

   1. Modo Gateway (padrão)
   2. Modo Direto

      Modo de gateway tem suporte em todas as plataformas do SDK e é Olá configurado padrão.  Se seu aplicativo é executado em uma rede corporativa com restrições de firewall estrita, o modo de Gateway é Olá melhor opção porque ele usa a porta HTTPS padrão de saudação e um ponto de extremidade. Olá compensação de desempenho, no entanto, é que o modo de Gateway envolve um salto de rede adicionais sempre que dados é lida ou gravados tooCosmos banco de dados. Por isso, o modo direto oferece melhor desempenho devido toofewer saltos de rede.
<a id="use-tcp"></a>
2. **Diretiva de Conexão: usar o protocolo TCP Olá**

    Ao usar o Modo Direto, há duas opções de protocolo disponíveis:

   * TCP
   * HTTPS

     O Cosmos DB oferece um modelo de programação RESTful simples e aberto por HTTPS. Além disso, ele oferece um protocolo TCP eficiente, que também é RESTful no seu modelo de comunicação e está disponível por meio do SDK de cliente .NET hello. Tanto TCP direto quanto HTTPS usam SSL para criptografar tráfego e autenticação inicial. Para melhor desempenho, use o protocolo TCP hello quando possível.

     Ao usar TCP no modo de Gateway, porta TCP 443 é Olá porta DB Cosmos e 10255 é a porta de API do MongoDB hello. Ao usar TCP em modo direto, em portas do Gateway toohello adição, você deve tooensure porta de saudação entre 10000 e 20000 está aberto como banco de dados do Cosmos usa portas TCP dinâmicas. Se essas portas não estão abertas e você tentar toouse TCP, você receberá o erro 503 Serviço indisponível.

     Olá modo de conectividade é configurado durante a construção de saudação da instância de DocumentClient Olá com parâmetro de ConnectionPolicy hello. Se for usado o modo direto, Olá protocolo também pode definir no parâmetro de ConnectionPolicy hello.

    ```C#
    var serviceEndpoint = new Uri("https://contoso.documents.net");
    var authKey = new "your authKey from hello Azure portal";
    DocumentClient client = new DocumentClient(serviceEndpoint, authKey,
    new ConnectionPolicy
    {
        ConnectionMode = ConnectionMode.Direct,
        ConnectionProtocol = Protocol.Tcp
    });
    ```

    Como TCP só tem suporte em modo direto, se o modo de Gateway é usado, em seguida, Olá protocolo HTTPS é sempre usado toocommunicate com hello Gateway e hello valor do protocolo em Olá que connectionpolicy será ignorado.

    ![Ilustração de saudação diretiva de conexão de banco de dados do Azure Cosmos](./media/performance-tips/connection-policy.png)

3. **Chame a latência de inicialização tooavoid OpenAsync na primeira solicitação**

    Por padrão, a primeira solicitação de saudação tem uma latência mais alta porque ele tem a tabela de roteamento de endereço do toofetch hello. essa latência de inicialização em Olá tooavoid primeiro solicitar, você deve chamar OpenAsync() uma vez durante a inicialização da seguinte maneira.

        await client.OpenAsync();
   <a id="same-region"></a>
4. **Colocar os clientes na mesma região do Azure para o desempenho**

    Quando possível, coloque Olá de quaisquer aplicativos que chamam Cosmos DB mesma região Olá banco de dados do banco de dados do Cosmos. Para obter uma comparação aproximada, chama tooCosmos DB dentro Olá concluir a mesma região dentro de 1 a 2 ms, mas a latência de saudação entre hello Oeste e Costa Leste de saudação dos EUA é > 50 ms. Essa latência provavelmente pode variar de solicitação toorequest dependendo da rota Olá tomada por solicitação Olá conforme ele passa de limite do hello cliente toohello datacenter do Azure. Olá menor latência possível é obtida, garantindo chamada hello aplicativo está localizado em Olá mesma região do Azure Olá provisionado ponto de extremidade do banco de dados do Cosmos. Para obter uma lista de regiões disponíveis, consulte [Regiões do Azure](https://azure.microsoft.com/regions/#services).

    ![Ilustração de saudação diretiva de conexão de banco de dados do Azure Cosmos](./media/performance-tips/same-region.png)
   <a id="increase-threads"></a>
5. **Aumentar o número de threads/tarefas**

    Como chamadas tooAzure Cosmos DB são feitas pela rede hello, talvez seja necessário toovary grau de saudação de paralelismo de suas solicitações para que o aplicativo de cliente hello gasta muito pouco tempo de espera entre solicitações. Por exemplo, se você estiver usando. Do NET [biblioteca paralela de tarefas](https://msdn.microsoft.com//library/dd460717.aspx), criar na ordem de saudação de 100 tarefas ler ou gravar tooCosmos banco de dados.

## <a name="sdk-usage"></a>Uso do SDK
1. **Instalar o SDK mais recente de Olá**

    Olá Cosmos SDKs do banco de dados estão sendo constantemente tooprovide aprimorado Olá melhor desempenho. Consulte Olá [Cosmos DB SDK](documentdb-sdk-dotnet.md) páginas toodetermine Olá SDK mais recente e examine melhorias.
2. **Usar um cliente de banco de dados do Cosmos singleton para o tempo de vida de saudação do seu aplicativo**

    Observe que cada instância do DocumentClient tem um thread seguro e realiza um gerenciamento de conexão eficiente e o cache de endereço ao operar no Modo Direto. gerenciamento de conexão eficiente tooallow e melhor desempenho por DocumentClient, é recomendável toouse uma única instância de DocumentClient por AppDomain para o tempo de vida de saudação do aplicativo hello.

   <a id="max-connection"></a>
3. **Aumentar System.Net MaxConnections por host usando o modo de Gateway**

    Cosmos DB solicitações feitas por HTTPS/REST ao usar o modo de Gateway e estão sujeitos toohello limite de conexão padrão por nome de host ou endereço IP. Talvez seja necessário tooset Olá MaxConnections tooa maior valor (100-1000) para que hello biblioteca de cliente pode utilizar várias conexões simultâneas tooCosmos banco de dados. Olá .NET SDK 1.8.0 e acima, Olá valor padrão para [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx) é 50 e toochange Olá valor, você pode definir Olá [Documents.Client.ConnectionPolicy.MaxConnectionLimit ](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.connectionpolicy.maxconnectionlimit.aspx) tooa maior valor.   
4. **Ajustar consultas paralelas para coleções particionadas**

     SDK do DocumentDB .NET versão 1.9.0 e acima de consultas paralelas suporte, que permitem que você tooquery uma coleção particionada em paralelo (consulte [trabalhando com hello SDKs](documentdb-partition-data.md#working-with-the-azure-cosmos-db-sdks) e hello relacionadas [exemplos de código](https://github.com/Azure/azure-documentdb-dotnet/blob/master/samples/code-samples/Queries/Program.cs) para mais informações). Consultas paralelas são a latência da consulta tooimprove projetado e taxa de transferência sobre sua contraparte serial. Consultas paralelas fornecem dois parâmetros que os usuários podem ajustar toocustom ajustar seus requisitos, (a) MaxDegreeOfParallelism: número de máximo de saudação do toocontrol de partições, em seguida, pode ser consultado em paralelo e (b) MaxBufferedItemCount: toocontrol Olá inúmeros pré-busca de resultados.

    (a) ***Ajuste de MaxDegreeOfParallelism\:*** a consulta paralela funciona consultando várias partições em paralelo. No entanto, dados de uma coleta particionada individual são buscados em série com respeito toohello consulta. Assim, definindo Olá MaxDegreeOfParallelism toohello o número de partições tem a chance de máximo de saudação de atingir Olá a maioria das consultas de alto desempenho, desde que todas as outras condições do sistema permanecem Olá mesmo. Se você não souber o número de saudação de partições, você pode definir o número alto da saudação MaxDegreeOfParallelism tooa e sistema Olá escolhe mínimo hello (número de partições, a entrada fornecida pelo usuário) como Olá MaxDegreeOfParallelism.

    É importante toonote que paralelo de consultas produzir Olá melhores benefícios se Olá dados forem distribuídos uniformemente em todas as partições com respeito toohello consulta. Se Olá particionada coleção é particionada forma que todos ou a maior parte dos dados hello retornados por uma consulta é concentrada em algumas partições (na pior das hipóteses, uma partição) e desempenho Olá de consulta Olá seria um afunilamento por essas partições.

    (b) ***ajuste MaxBufferedItemCount\: *** consulta paralela é resultados de busca de toopre projetado enquanto o lote atual de saudação de resultados está sendo processada pelo cliente hello. Olá pré-leitura ajuda a melhoria de latência geral de uma consulta. MaxBufferedItemCount é Olá parâmetro toolimit Olá número de resultados pré-buscados. Configuração MaxBufferedItemCount toohello esperado número de resultados retornados (ou um número mais alto) permite Olá consulta tooreceive máximo benefício de busca prévia.

    Observe que funciona pré-busca Olá mesmo maneira independentemente da saudação MaxDegreeOfParallelism e há um único buffer para dados de saudação de todas as partições.  
5. **Ativar o GC no lado do servidor**

    Reduzir Olá frequência da coleta de lixo pode ajudar em alguns casos. No .NET, defina [gcServer](https://msdn.microsoft.com/library/ms229357.aspx) tootrue.
6. **Implementar a retirada em intervalos de RetryAfter**

    Durante o teste de desempenho, você deve aumentar a carga até que uma pequena taxa de solicitações seja restringida. Se limitada, o aplicativo de cliente hello deve retirada na limitação para o intervalo de repetição especificada pelo servidor de saudação. Respeitar Olá retirada garante que você passe a quantidade mínima de tempo de espera entre as repetições. Suporte de política de repetição está incluído na versão 1.8.0 e posterior da saudação documentos [.NET](documentdb-sdk-dotnet.md) e [Java](documentdb-sdk-java.md), versão 1.9.0 e acima de saudação [Node.js](documentdb-sdk-node.md) e [ Python](documentdb-sdk-python.md), e todas as versões com suporte do hello [.NET Core](documentdb-sdk-dotnet-core.md) SDKs. Para saber mais, confira [Exceder os limites da taxa de transferência reservada](request-units.md#RequestRateTooLarge) e [RetryAfter](https://msdn.microsoft.com/library/microsoft.azure.documents.documentclientexception.retryafter.aspx).
7. **Escalar horizontalmente sua carga de trabalho do cliente**

    Se você estiver testando em níveis de alta taxa de transferência (> 50.000 RU/s), aplicativo de cliente hello pode se tornar um afunilamento Olá devido toohello máquina limitar na utilização da CPU ou de rede. Se você chegar a este ponto, você pode continuar a conta de banco de dados do Cosmos de saudação toopush mais expandindo seus aplicativos de cliente em vários servidores.
8. **Armazenar em cache os URIs do documento para uma menor latência de leitura**

    Documento URIs sempre que possível para melhor desempenho de leitura de saudação do cache.
   <a id="tune-page-size"></a>
9. **Ajustar o tamanho da página Olá para feeds de consultas/leitura para melhorar o desempenho**

    Quando executar a maior parte de leitura de documentos usando leitura feed funcionalidade (por exemplo, ReadDocumentFeedAsync) ou ao emitir uma consulta SQL do DocumentDB, os resultados de saudação são retornados de modo segmentado se Olá conjunto de resultados for muito grande. Por padrão, os resultados são retornados em blocos de 100 itens ou 1 MB, o limite que for atingido primeiro.

    tooreduce número de saudação de rede tooretrieve de viagens de ida e necessárias todos os resultados aplicável, você pode aumentar o tamanho da página hello usando too1000 de tooup de cabeçalho de solicitação x-ms-max-item-count. Em casos em que você precisa toodisplay apenas alguns resultados, por exemplo, se sua API de aplicativo ou de interface do usuário retorna apenas 10 resultados de um tempo, você também pode diminuir Olá tamanho too10 tooreduce Olá taxa de transferência página consumida para leituras e consultas.

    Você também pode definir o tamanho da página hello usando Olá disponível SDKs de banco de dados do Cosmos.  Por exemplo:

        IQueryable<dynamic> authorResults = client.CreateDocumentQuery(documentCollection.SelfLink, "SELECT p.Author FROM Pages p WHERE p.Title = 'About Seattle'", new FeedOptions { MaxItemCount = 1000 });
10. **Aumentar o número de threads/tarefas**

    Consulte [aumentar o número de threads/tarefas](#increase-threads) em Olá seção de rede.

11. **Usar o processamento do host de 64 bits**

    Olá SDK do DocumentDB funciona em um processo de host de 32 bits quando você estiver usando o SDK do DocumentDB .NET versão 1.11.4 e posterior. No entanto, se você usa consultas entre partições, recomenda-se o processamento de host de 64 bits para melhorar o desempenho. Olá seguintes tipos de aplicativos que o host de 32 bits processar como padrão hello, portanto em ordem toochange ou too64 bits, siga estas etapas com base no tipo de saudação do seu aplicativo:

    - Para aplicativos do executável, isso pode ser feito por Olá desmarcando **preferir 32-bit** opção Olá **propriedades do projeto** janela Olá **criar** guia.

    - Para projetos de teste com base em VSTest, isso pode ser feito selecionando **teste**->**configurações do teste**->**padrão arquitetura de processador X64**, de saudação **Visual Studio Test** opção de menu.

    - Para aplicativos Web ASP.NET implantados localmente, isso pode ser feito verificando Olá **versão de 64 bits de saudação uso do IIS Express para sites e projetos**, em **ferramentas** ->  **Opções de**->**projetos e soluções**->**projetos Web**.

    - Para aplicativos Web ASP.NET implantados no Azure, isso pode ser feito escolhendo Olá **plataforma de 64 bits** em Olá **configurações de aplicativo** em Olá portal do Azure.

## <a name="indexing-policy"></a>Política de indexação
1. **Usar a indexação lenta para as taxas de ingestão de tempo máximo mais rápidas**

    Banco de dados do cosmos permite toospecify – no nível de coleção hello – uma política de indexação, o que permite que você toochoose se desejar Olá documentos em um toobe coleção indexada automaticamente ou não.  Além disso, você também pode escolher entre as atualizações do índice síncronas (Consistentes) e assíncronas (Lentas). Por padrão, o índice de saudação é atualizado de forma síncrona em cada inserção, substituir ou excluir de uma coleção de toohello do documento. Modo síncrono toohonor de consultas do modo habilita Olá Olá mesmo [nível de consistência](consistency-levels.md) da saudação documento lê sem qualquer atraso de índice Olá muito "atualizado".

    A indexação lenta pode ser considerada para cenários em que os dados são gravados em intermitências e deseja tooamortize Olá trabalho necessário tooindex conteúdo em um período mais longo de tempo. A indexação lenta também permite que você toouse sua provisionado a taxa de transferência com eficiência e atender solicitações de gravação em horários de pico com latência mínima. É importante toonote, no entanto, que, quando a indexação lento está habilitada, resultados da consulta são eventualmente consistentes, independentemente do nível de consistência de saudação configurado para conta de banco de dados do Cosmos hello.

    Portanto, modo consistente de indexação (IndexingPolicy.IndexingMode é definido tooConsistent) incorre em custos unidade solicitação de hello mais alto por gravação enquanto Lazy indexação modo (IndexingPolicy.IndexingMode é definido tooLazy) e nenhum indexação (IndexingPolicy.Automatic é definido tooFalse) tenha o custo zero indexação Olá tempo de gravação.
2. **Excluir caminhos não utilizados da indexação para ter gravações mais rápidas**

    Política de indexação do cosmos do banco de dados também permite que você toospecify que tooinclude caminhos de documento ou excluídos da indexação, aproveitando os caminhos de indexação (IndexingPolicy.IncludedPaths e IndexingPolicy.ExcludedPaths). use Olá dos caminhos de indexação pode oferecer desempenho aprimorado de gravação e armazenamento de índice inferior para cenários que Olá padrões de consulta são conhecidos com antecedência, assim como os custos de indexação diretamente correlacionado toohello número exclusivo caminhos indexados.  Por exemplo, a saudação de código a seguir mostra como tooexclude uma seção inteira de saudação documentos (também conhecido como uma subárvore) de indexação usando hello "*" curinga.

    ```C#
    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*");
    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);
    ```

    Para obter mais informações, consulte [Políticas de indexação do Azure Cosmos DB](indexing-policies.md).

## <a name="throughput"></a>Taxa de transferência
<a id="measure-rus"></a>

1. **Medir e ajustar para o uso mais baixo de unidades/segundo da solicitação**

    Cosmos banco de dados oferece um conjunto avançado de operações de banco de dados, incluindo consultas relacionais e hierárquicas com UDFs, procedimentos armazenados e gatilhos – todos os controles em documentos hello dentro de uma coleção de banco de dados. custo de saudação associado a cada uma dessas operações varia de acordo com hello da CPU, e/s e memória necessária toocomplete Olá operação. Em vez de pensar sobre e gerenciamento de recursos de hardware, você pode pensar uma unidade de solicitação (RU) como uma única medida para Olá recursos necessários tooperform várias operações de banco de dados e o serviço de uma solicitação de aplicativo.

    [Unidades de solicitação](request-units.md) são provisionados para cada conta de banco de dados com base no número de saudação de unidades de capacidade que você comprar. O consumo da unidade de solicitação é avaliado em termos de taxa por segundo. Aplicativos que excedem a unidade de solicitação provisionado Olá taxa para sua conta é limitada até que a taxa de saudação fique abaixo Olá nível reservado para a conta de saudação. Se o seu aplicativo exigir um nível mais alto de taxa de transferência, você pode comprar unidades de capacidade adicionais.

    complexidade de saudação de uma consulta afeta quantas unidades de solicitação são consumidas para uma operação. número de Olá de predicados, natureza de predicados hello, número de UDFs e tamanho de saudação do conjunto de dados de origem Olá todos influenciam o custo de saudação de operações de consulta.

    sobrecarga de saudação toomeasure de qualquer operação (criar, atualizar ou excluir), inspecionar o cabeçalho x-ms-taxa de solicitação de saudação (ou Olá propriedade RequestCharge equivalente em ResourceResponse<T> ou FeedResponse<T> em Olá .NET SDK) toomeasure número de saudação de unidades de solicitação consumida por essas operações.

    ```C#
    // Measure hello performance (request units) of writes
    ResourceResponse<Document> response = await client.CreateDocumentAsync(collectionSelfLink, myDocument);
    Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);
    // Measure hello performance (request units) of queries
    IDocumentQuery<dynamic> queryable = client.CreateDocumentQuery(collectionSelfLink, queryString).AsDocumentQuery();
    while (queryable.HasMoreResults)
         {
              FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>();
              Console.WriteLine("Query batch consumed {0} request units", queryResponse.RequestCharge);
         }
    ```             

    taxa de solicitação retornada nesse cabeçalho Hello é uma fração de sua taxa de transferência fornecida (ou seja, 2000 RUs / segundo). Por exemplo, se hello consulta anterior retorna 1KB de 1000 documentos, o custo de saudação da operação de saudação é 1000. Como tal, dentro de um segundo, servidor de saudação honra apenas dois tais solicitações antes da limitação de solicitações subsequentes. Para obter mais informações, consulte [unidades de solicitação](request-units.md) e hello [Calculadora de unidade de solicitação](https://www.documentdb.com/capacityplanner).
<a id="429"></a>
2. **Lidar com uma limitação da taxa/taxa de solicitação muito grande**

    Quando um cliente tenta tooexceed Olá taxa de transferência reservada para uma conta, não há sem degradação do desempenho no servidor de saudação e sem uso da capacidade da taxa de transferência além do nível de saudação reservada. servidor de saudação preventivamente terminará solicitação Olá com RequestRateTooLarge (código de status HTTP 429) e retorno Olá o cabeçalho x-ms-repetição-após-ms indicando de saudação período de tempo, em milissegundos, que Olá usuário deve aguardar antes de tentar novamente a solicitação de saudação.

        HTTP Status 429,
        Status Line: RequestRateTooLarge
        x-ms-retry-after-ms :100

    Olá SDKs implicitamente todos os catch essa resposta, respeitam Olá servidor especificado cabeçalho retry-after e repita a solicitação hello. A menos que sua conta está sendo acessada simultaneamente por vários clientes, a próxima repetição de saudação terá êxito.

    Se você tiver mais de um cliente cumulativamente funcionando consistentemente acima de taxa de solicitação hello, Olá contagem de repetições padrão atualmente too9 conjunto internamente pelo cliente Olá pode não ser suficiente; Nesse caso, o cliente hello gera um DocumentClientException com o aplicativo de 429 toohello status código. Contagem de repetições saudação padrão pode ser alterada por Olá configuração RetryOptions na instância de ConnectionPolicy hello. Por padrão, Olá DocumentClientException com código de status 429 será retornado após um tempo de espera cumulativo de 30 segundos se solicitação Olá continua toooperate acima a taxa de solicitação de saudação. Isso ocorre mesmo quando Olá repetir contagem atual é menor que a contagem de repetição máxima Olá, seja padrão Olá 9 ou um valor definido pelo usuário.

    Enquanto automatizada hello comportamento de repetição ajuda tooimprove flexibilidade e facilidade de uso para Olá a maioria dos aplicativos, pode vir oposto ao fazer as avaliações de desempenho, especialmente quando medindo a latência.  latência de cliente observado Hello serão apresentam picos se experimento Olá atinge a limitação do servidor de saudação e faz com que o cliente Olá repetição de toosilently do SDK. latência de tooavoid picos durante testes de desempenho, medidas Olá custos retornado por cada operação e garantir que as solicitações são operando abaixo de taxa de solicitação reservado hello. Para saber mais, consulte [Unidades de solicitação](request-units.md).
3. **Design de documentos menores para uma maior taxa de transferência**

    Olá a carga de solicitação (ou seja, o custo de processamento de solicitação) de uma determinada operação é diretamente correlacionado toohello tamanho do documento hello. As operações em documentos grandes custam mais que as operações de documentos pequenos.

## <a name="next-steps"></a>Próximas etapas
Para um tooevaluate do aplicativo usado de exemplo Cosmos DB para cenários de alto desempenho em algumas máquinas cliente, consulte [desempenho e dimensionamento de teste com o banco de dados do Cosmos](performance-testing.md).

Além disso, toolearn mais sobre como criar seu aplicativo de escala e de alto desempenho, consulte [particionamento e escala no banco de dados do Azure Cosmos](partition-data.md).
