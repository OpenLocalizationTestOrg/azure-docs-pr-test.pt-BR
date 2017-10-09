---
title: "os serviços do Service Fabric aaaPartitioning | Microsoft Docs"
description: "Descreve como os serviços com monitoração de estado toopartition Service Fabric. Partições permite o armazenamento de dados em máquinas locais Olá para que dados e computação podem ser dimensionados em conjunto."
services: service-fabric
documentationcenter: .net
author: msfussell
manager: timlt
editor: 
ms.assetid: 3b7248c8-ea92-4964-85e7-6f1291b5cc7b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: msfussell
ms.openlocfilehash: 6ead48716c08f4212535202ee69d169067d5c6d8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="partition-service-fabric-reliable-services"></a>Particionar Reliable Services do Service Fabric
Este artigo fornece uma introdução toohello conceitos básicos de particionamento serviços confiáveis do Azure Service Fabric. Olá código-fonte usado no artigo Olá também está disponível em [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="partitioning"></a>Particionamento
O particionamento não é exclusivo tooService malha. Na verdade, é um padrão núcleo da criação de serviços escalonáveis. Em um sentido mais amplo, podemos pensar em particionamento como um conceito de divisão do estado (dados) e de computação de desempenho e escalabilidade de tooimprove acessível unidades menor. Uma forma bem conhecida de particionamento é o [particionamento de dados][wikipartition], também conhecido como fragmentação.

### <a name="partition-service-fabric-stateless-services"></a>Particionar serviços sem estado do Service Fabric
Para serviços sem estado, você pode pensar em uma partição como uma unidade lógica que contém uma ou mais instâncias de um serviço. A Figura 1 mostra um serviço sem estado com cinco instâncias distribuídas em um cluster usando uma partição.

![Serviço sem estado](./media/service-fabric-concepts-partitioning/statelessinstances.png)

Há realmente dois tipos de soluções de serviço sem estado. Hello primeiro um é um serviço que mantém seu estado externamente, por exemplo em um banco de dados do SQL Azure (como um site que armazena dados e informações de sessão Olá). Olá, um segundo é somente para computação serviços (como miniaturas uma calculadora ou imagem) que não gerencia qualquer estado persistente.

Em ambos os casos o particionamento de um serviço sem estado é um cenário muito raro – a escalabilidade e disponibilidade normalmente são obtidas pela adição de mais instâncias. Olá somente tempo tooconsider várias partições para instâncias de serviço sem monitoração de estado é quando você precisa do roteamento especial do toomeet solicitações.

Por exemplo, considere um caso em que os usuários com IDs de um determinado intervalo só devem ser atendidos por uma instância de determinado serviço. Outro exemplo de quando é possível particionar um serviço sem monitoração de estado é quando você tiver um back-end realmente particionado (por exemplo, um SQL banco de dados fragmentado) e você deseja toocontrol qual instância de serviço deve gravar toohello fragmentos do banco de dados – ou realizar outro trabalho de preparação em Olá serviço sem monitoração de estado que exige Olá mesmo informações de particionamento como é usado em Olá back-end. Esses tipos de cenários também podem ser resolvidos de diferentes maneiras e não exigem, necessariamente, particionamento de serviço.

Olá restante deste passo a passo se concentra nos serviços de monitoração de estado.

### <a name="partition-service-fabric-stateful-services"></a>Particionar serviços com estado do Service Fabric
Service Fabric torna fácil toodevelop serviços escalonáveis de monitoração de estado, oferecendo uma maneira de primeira classe toopartition estado (dados). Conceitualmente, você pode pensar em uma partição de um serviço com monitoração de estado como uma unidade de escala que é altamente confiável por meio de [réplicas](service-fabric-availability-services.md) que são distribuídos e equilibrada em Olá nós em um cluster.

No contexto de saudação do serviços de malha do serviço com monitoração de estado refere-se toohello o processo de determinar que uma partição de serviço é responsável por uma parte do estado de conclusão Olá do serviço de saudação. (Conforme mencionado anteriormente, uma partição é um conjunto de [réplicas](service-fabric-availability-services.md)). Uma grande vantagem do Service Fabric é que ele coloca partições Olá em nós diferentes. Isso permite que o limite de recurso do nó de tooa toogrow. Como dados saudação crescer, aumento de partições e do Service Fabric redistribui partições em nós. Isso garante a saudação continuação uso eficiente dos recursos de hardware.

toogive você, por exemplo, digamos que você comece com um cluster de nó 5 e um serviço que é configurado toohave 10 partições e um destino de três réplicas. Nesse caso, Service Fabric deve equilibrar e distribuir réplicas Olá em cluster hello – e acabar com dois [réplicas](service-fabric-availability-services.md) por nó.
Se você precisar agora tooscale nós de too10 cluster hello, Service Fabric seria reequilibrar Olá primário [réplicas](service-fabric-availability-services.md) em todos os nós de 10. Da mesma forma, se você voltar too5 nós em escala, Service Fabric seria reequilibrar todas as réplicas de saudação em nós Olá 5.  

Figura 2 mostra a distribuição de saudação de 10 partições antes e depois de dimensionamento do cluster hello.

![Serviço com estado](./media/service-fabric-concepts-partitioning/partitions.png)

Como resultado, Olá expansão é obtido desde que as solicitações de clientes são distribuídas entre computadores, é melhor desempenho geral do aplicativo hello e contenção no toochunks de acesso de dados é reduzida.

## <a name="plan-for-partitioning"></a>Plano de particionamento
Antes de implementar um serviço, você deve sempre considerar Olá estratégia é necessário tooscale-out de particionamento. Há maneiras diferentes, mas todos eles se concentrar no que aplicativo hello precisa tooachieve. Contexto Olá neste artigo, vamos considerar alguns Olá aspectos mais importantes.

Uma boa abordagem é toothink sobre estrutura de saudação do estado de saudação que precisa toobe particionada, como primeira etapa de saudação.

Veja abaixo um exemplo simples Se você fosse toobuild um serviço para uma pesquisa countywide, você pode criar uma partição de cada cidade no município de saudação. Em seguida, você pode armazenar Olá votos para cada pessoa cidade Olá na partição de saudação corresponde toothat cidade. A Figura 3 ilustra um conjunto de pessoas e hello cidade em que eles residem.

![Partição simples](./media/service-fabric-concepts-partitioning/cities.png)

Como a população de saudação de cidades varia muito, você pode acabar com algumas partições que contêm muitos dados (por exemplo, Seattle) e outras partições com muito pouco estado (por exemplo, Kirkland). Então, qual é o impacto de saudação de partições com quantidades irregulares de estado?

Se você pensar sobre o exemplo hello novamente, você pode ver facilmente que partição Olá que contém a saudação votos para Seattle obterão mais tráfego que Kirkland Olá um. Por padrão, o Service Fabric torna-se de que há sobre Olá mesmo número de réplicas primárias e secundárias em cada nó. Assim, você pode acabar com nós que hospedam réplicas que atendem a mais tráfego e outras que atendem a menos tráfego. Preferencialmente deseje tooavoid ativa e frios pontos como isso em um cluster.

Em ordem tooavoid isso, você deve fazer duas coisas, de um ponto de vista particionamento:

* Tente o estado de saudação toopartition para que ele é distribuído uniformemente entre todas as partições.
* Relatório de carga de cada uma das réplicas Olá para o serviço de saudação. (Para obter informações sobre como fazer isso, leia este artigo sobre [métricas e carga](service-fabric-cluster-resource-manager-metrics.md)). Malha do serviço fornecem a carga de tooreport de recurso Olá consumida por serviços, como a quantidade de memória ou o número de registros. Com base nas métricas de saudação relatadas, o Service Fabric detecta que algumas partições estão servindo cargas mais altas que outros e redistribui cluster Olá pela movimentação réplicas toomore adequado nós, para que geral nenhum nó está sobrecarregado.

Às vezes, você não tem como saber quantos dados haverá em uma determinada partição. Uma recomendação geral é toodo ambos – primeiro, adotando uma estratégia de particionamento que se espalha dados saudação uniformemente entre partições hello e, segundo, pelo relatório de carga.  método primeiro Hello impede situações descritas no hello votação de exemplo, enquanto Olá segundo ajuda a suavizar temporárias diferenças no access ou carga ao longo do tempo.

Outro aspecto do planejamento de partição é número correto de saudação de toochoose de toobegin de partições com.
Do ponto de vista do Service Fabric, não há nada que impeça começar com um número de partições maior do o previsto para o cenário.
Na verdade, supondo que o número máximo de saudação de partições é uma abordagem válida.

Em casos raros, você acabará precisando de mais partições do que escolheu inicialmente. Como você não pode alterar a contagem de partição Olá após o fato de hello, você precisaria tooapply algumas abordagens de partição avançadas, como criar uma nova instância de serviço da saudação mesmo tipo de serviço. Também é necessário tooimplement alguma lógica do lado do cliente que roteia Olá solicitações toohello instância de serviço correto, com base no conhecimento do lado do cliente que deve manter o código do cliente.

Outra consideração de planejamento de particionamento é recursos de computação disponíveis hello. Como estado de saudação precisa toobe acessados e armazenados, você está toofollow associada:

* Limites de largura de banda de rede
* Limites de memória do sistema
* Limites de armazenamento de disco

O que acontece se você tiver restrições de recursos em um cluster em execução? resposta de saudação é que você pode expandir simplesmente Olá cluster tooaccommodate Olá novos requisitos.

[Guia de planejamento de capacidade de saudação](service-fabric-capacity-planning.md) oferece orientação sobre como toodetermine quantos nós de cluster precisa.

## <a name="get-started-with-partitioning"></a>Introdução ao particionamento
Esta seção descreve como tooget iniciada com o particionamento de seu serviço.

O Service Fabric oferece uma variedade de três esquemas de partição:

* Intervalo de particionamento (também conhecido como UniformInt64Partition).
* Particionamento nomeado. Aplicativos que usam esse modelo geralmente têm dados em bucket, dentro de um conjunto limitado. Alguns exemplos comuns de campos de dados usados como chaves de partição nomeada seriam regiões, códigos postais, grupos de clientes ou outros limites de negócios.
* Particionamento de singleton. Partições de singleton normalmente são usadas quando o serviço Olá não requer qualquer roteamento adicional. Por exemplo, serviços sem estado usam esse esquema de particionamento por padrão.

Os esquemas de particionamento Singleton e Nomeado são formulários especiais de partições de intervalos. Por padrão, modelos do Visual Studio Olá para uso do Service Fabric alcance particionamento, conforme é Olá um mais comuns e úteis. Olá restante deste artigo se concentra no esquema de particionamento intervalos hello.

### <a name="ranged-partitioning-scheme"></a>Esquema de particionamento por intervalos
Isso é usado toospecify um número inteiro (identificadas por uma chave baixa e alta chave) de intervalo e um número de partições (n). Ele cria partições n, cada responsáveis por um subintervalo sem sobreposição de saudação geral de intervalo de chave de partição. Por exemplo, um esquema de particionamento por intervalos com uma chave baixa de 0, uma chave de alta de 99 e uma contagem de 4 criaria quatro partições, conforme mostrado abaixo.

![Particionamento por intervalos](./media/service-fabric-concepts-partitioning/range-partitioning.png)

Uma abordagem comum é toocreate um hash com base em uma chave exclusiva no conjunto de dados de saudação. Alguns exemplos comuns de chaves seriam um número de identificação de veículo (VIN), uma ID de funcionário ou uma cadeia de caracteres exclusiva. Usando essa chave exclusiva, você poderia, em seguida, gerar um código hash, o intervalo de chave de saudação do módulo, toouse como sua chave. Você pode especificar hello superior e limites inferiores da saudação chave intervalo permitido.

### <a name="select-a-hash-algorithm"></a>Selecionar um algoritmo de hash
Uma parte importante de hash é selecionar o algoritmo de hash. Uma consideração é se o objetivo de saudação é chaves semelhante de toogroup próximos um do outro (hash confidenciais localidade) – ou se a atividade deve ser distribuída em larga escala em todas as partições (hash de distribuição), que é mais comum.

características de saudação de um algoritmo de hash de distribuição BOM são que é fácil toocompute, ele tem poucos conflitos e distribui chaves Olá uniformemente. Um bom exemplo de um algoritmo de hash eficiente é hello [FNV 1](https://en.wikipedia.org/wiki/Fowler%E2%80%93Noll%E2%80%93Vo_hash_function) algoritmo de hash.

Um bom recurso para obter opções de algoritmo hash geral código é hello [página da Wikipédia sobre funções de hash](http://en.wikipedia.org/wiki/Hash_function).

## <a name="build-a-stateful-service-with-multiple-partitions"></a>Criar um serviço com estado com várias partições
Vamos criar seu primeiro serviço com estado confiável com várias partições. Neste exemplo, você criará um aplicativo muito simples, onde você deseja toostore todos os sobrenomes que começam com hello mesmo letra no hello mesma partição.

Antes de gravar qualquer código, você precisa toothink sobre partições hello e chaves de partição. Você precisa 26 partições (uma para cada letra no alfabeto Olá), mas e sobre Olá chaves baixa e alta?
Como desejamos literalmente toohave uma partição por letra, podemos usar 0 como chave baixa hello e 25 como chave de alta hello, como cada letra é sua própria chave.

> [!NOTE]
> Este é um cenário simplificado, como na realidade distribuição Olá seria irregular. Último nomes que começam com letras hello "S" ou "M" são mais comuns que Olá aqueles começando com "X" ou "Y".
> 
> 

1. Abra **Visual Studio** > **Arquivo** > **Novo** > **Projeto**.
2. Em Olá **novo projeto** caixa de diálogo caixa, escolha o aplicativo de serviço de malha hello.
3. Chame projeto hello "AlphabetPartitions".
4. Em Olá **criar um serviço** caixa de diálogo caixa, escolha **com monitoração de estado** de serviço e chamá-lo "Alphabet.Processing" conforme mostrado na imagem de saudação abaixo.
       ![Caixa de diálogo Novo serviço no Visual Studio][1]

  <!--  ![Stateful service screenshot](./media/service-fabric-concepts-partitioning/createstateful.png)-->

5. Defina o número de saudação de partições. Arquivo de Applicationmanifest.xml de saudação abrir localizado no Olá ApplicationPackageRoot pasta Olá AlphabetPartitions projeto e atualize Olá parâmetro Processing_PartitionCount too26 conforme mostrado abaixo.
   
    ```xml
    <Parameter Name="Processing_PartitionCount" DefaultValue="26" />
    ```
   
    Você também precisa Olá tooupdate LowKey e HighKey propriedades de elemento StatefulService Olá Olá ApplicationManifest.xml, conforme mostrado abaixo.
   
    ```xml
    <Service Name="Processing">
      <StatefulService ServiceTypeName="ProcessingType" TargetReplicaSetSize="[Processing_TargetReplicaSetSize]" MinReplicaSetSize="[Processing_MinReplicaSetSize]">
        <UniformInt64Partition PartitionCount="[Processing_PartitionCount]" LowKey="0" HighKey="25" />
      </StatefulService>
    </Service>
    ```
6. Para Olá toobe de serviço acessível, abra um ponto de extremidade em uma porta, adicionando o elemento de ponto de extremidade de saudação do ServiceManifest.xml (localizado na pasta de PackageRoot Olá) para Olá Alphabet.Processing serviço conforme mostrado abaixo:
   
    ```xml
    <Endpoint Name="ProcessingServiceEndpoint" Port="8089" Protocol="http" Type="Internal" />
    ```
   
    Agora o serviço de saudação é configurado toolisten tooan ponto de extremidade interno com 26 partições.
7. Em seguida, você precisa toooverride Olá `CreateServiceReplicaListeners()` método da classe de processamento de saudação.
   
   > [!NOTE]
   > Para este exemplo, supomos que você esteja usando um HttpCommunicationListener simples. Para obter mais informações sobre a comunicação de serviço confiável, consulte [modelo de comunicação de serviço confiável Olá](service-fabric-reliable-services-communication.md).
   > 
   > 
8. Um padrão recomendado para a URL de saudação que uma réplica escuta em é Olá formato a seguir: `{scheme}://{nodeIp}:{port}/{partitionid}/{replicaid}/{guid}`.
    Portanto, você tooconfigure sua toolisten de ouvinte de comunicação em pontos de extremidade correto hello e com esse padrão.
   
    Várias réplicas do serviço podem ser hospedadas em Olá mesmo computador, para que esse endereço precisa toobe toohello exclusivo réplica. Isso é porque a ID de partição + ID de réplica na URL de saudação. HttpListener pode escutar em vários endereços Olá que mesma porta como prefixo da URL Olá é exclusivo.
   
    Olá que GUID extra há um caso avançada em réplicas secundárias também escutam solicitações somente leitura. Quando esse for o caso de Olá, você deseja toomake-se de que um novo endereço exclusivo é usado durante a transição de endereço de saudação toosecondary primário tooforce clientes toore resolver. '+' é usado como o endereço de saudação aqui para que hello réplica escuta em todos os códigos de saudação hosts disponíveis (IP, FQDM, localhost, etc.) abaixo mostra um exemplo.
   
    ```CSharp
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
         return new[] { new ServiceReplicaListener(context => this.CreateInternalListener(context))};
    }
    private ICommunicationListener CreateInternalListener(ServiceContext context)
    {
   
         EndpointResourceDescription internalEndpoint = context.CodePackageActivationContext.GetEndpoint("ProcessingServiceEndpoint");
         string uriPrefix = String.Format(
                "{0}://+:{1}/{2}/{3}-{4}/",
                internalEndpoint.Protocol,
                internalEndpoint.Port,
                context.PartitionId,
                context.ReplicaOrInstanceId,
                Guid.NewGuid());
   
         string nodeIP = FabricRuntime.GetNodeContext().IPAddressOrFQDN;
   
         string uriPublished = uriPrefix.Replace("+", nodeIP);
         return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInternalRequest);
    }
    ```
   
    Também vale a pena observar que Olá publicado URL é ligeiramente diferente do prefixo de URL escutando hello.
    URL de escuta Olá recebe tooHttpListener. Olá que publicado URL é Olá que é publicado toohello serviço de nomenclatura do Service Fabric, que é usado para descoberta de serviço. Os clientes pedirão esse endereço por meio desse serviço de descoberta. endereço de saudação que os clientes obtêm necessidades toohave Olá real IP ou FQDN do nó de saudação em ordem tooconnect. Portanto, você precisa tooreplace '+' com hello do nó IP ou FQDN conforme mostrado acima.
9. Olá última etapa é Olá tooadd lógica toohello serviço conforme mostrado abaixo de processamento.
   
    ```CSharp
    private async Task ProcessInternalRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        string output = null;
        string user = context.Request.QueryString["lastname"].ToString();
   
        try
        {
            output = await this.AddUserAsync(user);
        }
        catch (Exception ex)
        {
            output = ex.Message;
        }
   
        using (HttpListenerResponse response = context.Response)
        {
            if (output != null)
            {
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    private async Task<string> AddUserAsync(string user)
    {
        IReliableDictionary<String, String> dictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<String, String>>("dictionary");
   
        using (ITransaction tx = this.StateManager.CreateTransaction())
        {
            bool addResult = await dictionary.TryAddAsync(tx, user.ToUpperInvariant(), user);
   
            await tx.CommitAsync();
   
            return String.Format(
                "User {0} {1}",
                user,
                addResult ? "sucessfully added" : "already exists");
        }
    }
    ```
   
    `ProcessInternalRequest`Leituras Olá valores de parâmetro usado de cadeia de caracteres do Olá consulta toocall Olá partição e chamadas `AddUserAsync` dicionário confiável do tooadd Olá lastname toohello `dictionary`.
10. Vamos adicionar um toosee de projeto do serviço sem monitoração de estado toohello como você pode chamar uma partição específica.
    
    Esse serviço serve como uma interface simples da web que aceita Olá lastname como um parâmetro de cadeia de caracteres de consulta, determina a chave de partição hello e envia toohello Alphabet.Processing serviço para processamento.
11. Em Olá **criar um serviço** caixa de diálogo caixa, escolha **sem monitoração de estado** de serviço e chamá-lo "Alphabet.Web" conforme mostrado abaixo.
    
    ![Captura de tela de serviço sem estado](./media/service-fabric-concepts-partitioning/createnewstateless.png).
12. Atualize informações de ponto de extremidade Olá no hello ServiceManifest.xml de saudação Alphabet.WebApi serviço tooopen uma porta, conforme mostrado abaixo.
    
    ```xml
    <Endpoint Name="WebApiServiceEndpoint" Protocol="http" Port="8081"/>
    ```
13. É necessário tooreturn uma coleção de ServiceInstanceListeners na classe Olá Web. Novamente, você pode escolher tooimplement um HttpCommunicationListener simple.
    
    ```CSharp
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        return new[] {new ServiceInstanceListener(context => this.CreateInputListener(context))};
    }
    private ICommunicationListener CreateInputListener(ServiceContext context)
    {
        // Service instance's URL is hello node's IP & desired port
        EndpointResourceDescription inputEndpoint = context.CodePackageActivationContext.GetEndpoint("WebApiServiceEndpoint")
        string uriPrefix = String.Format("{0}://+:{1}/alphabetpartitions/", inputEndpoint.Protocol, inputEndpoint.Port);
        var uriPublished = uriPrefix.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);
        return new HttpCommunicationListener(uriPrefix, uriPublished, this.ProcessInputRequest);
    }
    ```
14. Agora, é necessário tooimplement lógica de processamento de saudação. Olá chamadas HttpCommunicationListener `ProcessInputRequest` quando chegar a uma solicitação. Vamos em frente e adicione Olá código abaixo.
    
    ```CSharp
    private async Task ProcessInputRequest(HttpListenerContext context, CancellationToken cancelRequest)
    {
        String output = null;
        try
        {
            string lastname = context.Request.QueryString["lastname"];
            char firstLetterOfLastName = lastname.First();
            ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    
            ResolvedServicePartition partition = await this.servicePartitionResolver.ResolveAsync(alphabetServiceUri, partitionKey, cancelRequest);
            ResolvedServiceEndpoint ep = partition.GetEndpoint();
    
            JObject addresses = JObject.Parse(ep.Address);
            string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
            UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
            primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
            string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    
            output = String.Format(
                    "Result: {0}. <p>Partition key: '{1}' generated from hello first letter '{2}' of input value '{3}'. <br>Processing service partition ID: {4}. <br>Processing service replica address: {5}",
                    result,
                    partitionKey,
                    firstLetterOfLastName,
                    lastname,
                    partition.Info.Id,
                    primaryReplicaAddress);
        }
        catch (Exception ex) { output = ex.Message; }
    
        using (var response = context.Response)
        {
            if (output != null)
            {
                output = output + "added tooPartition: " + primaryReplicaAddress;
                byte[] outBytes = Encoding.UTF8.GetBytes(output);
                response.OutputStream.Write(outBytes, 0, outBytes.Length);
            }
        }
    }
    ```
    
    Vamos ver o passo a passo. código de Olá lê a primeira letra de saudação do parâmetro de cadeia de caracteres de consulta Olá `lastname` em char. Em seguida, ele determina a chave de partição Olá para essa letra de subtraindo o valor hexadecimal de saudação do `A` do valor hexadecimal de saudação da primeira letra dos hello sobrenomes.
    
    ```CSharp
    string lastname = context.Request.QueryString["lastname"];
    char firstLetterOfLastName = lastname.First();
    ServicePartitionKey partitionKey = new ServicePartitionKey(Char.ToUpper(firstLetterOfLastName) - 'A');
    ```
    
    Lembre-se de que, neste exemplo, estamos usando 26 partições com uma chave de partição por partição.
    Em seguida, podemos obter partição de serviço Olá `partition` para essa chave usando Olá `ResolveAsync` método hello `servicePartitionResolver` objeto. `servicePartitionResolver` é definido como
    
    ```CSharp
    private readonly ServicePartitionResolver servicePartitionResolver = ServicePartitionResolver.GetDefault();
    ```
    
    Olá `ResolveAsync` URI de serviço do método leva hello, chave de partição hello e um token de cancelamento como parâmetros. Olá URI do serviço para o serviço de processamento de saudação é `fabric:/AlphabetPartitions/Processing`. Em seguida, podemos obter ponto de extremidade de saudação da partição hello.
    
    ```CSharp
    ResolvedServiceEndpoint ep = partition.GetEndpoint()
    ```
    
    Finalmente, criar URL de ponto de extremidade hello mais querystring hello e chamar o serviço de processamento de saudação.
    
    ```CSharp
    JObject addresses = JObject.Parse(ep.Address);
    string primaryReplicaAddress = (string)addresses["Endpoints"].First();
    
    UriBuilder primaryReplicaUriBuilder = new UriBuilder(primaryReplicaAddress);
    primaryReplicaUriBuilder.Query = "lastname=" + lastname;
    
    string result = await this.httpClient.GetStringAsync(primaryReplicaUriBuilder.Uri);
    ```
    
    Depois de processamento Olá, podemos gravar saída Olá novamente.
15. Olá última etapa é o serviço de saudação tootest. O Visual Studio usa parâmetros do aplicativo para implantação local e na nuvem. serviço de saudação tootest com 26 partições localmente, você precisa Olá tooupdate `Local.xml` arquivo na pasta de ApplicationParameters saudação do projeto de AlphabetPartitions hello, conforme mostrado abaixo:
    
    ```xml
    <Parameters>
      <Parameter Name="Processing_PartitionCount" Value="26" />
      <Parameter Name="WebApi_InstanceCount" Value="1" />
    </Parameters>
    ```
16. Depois de concluir a implantação, você pode verificar o serviço hello e todas as suas partições em Olá Service Fabric Explorer.
    
    ![Captura de tela do Gerenciador do Service Fabric](./media/service-fabric-concepts-partitioning/sfxpartitions.png)
17. Em um navegador, você pode testar Olá lógica de particionamento, inserindo `http://localhost:8081/?lastname=somename`. Você verá que cada sobrenome que inicia com hello a mesma letra está sendo armazenada no hello mesma partição.
    
    ![Captura de tela do navegador](./media/service-fabric-concepts-partitioning/samplerunning.png)

código-fonte inteira saudação do exemplo hello está disponível em [GitHub](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/AlphabetPartitions).

## <a name="next-steps"></a>Próximas etapas
Para obter informações sobre os conceitos de malha do serviço, consulte o seguinte hello:

* [Disponibilidade dos serviços de malha do serviço](service-fabric-availability-services.md)
* [Escalabilidade de serviços da Malha do Serviço](service-fabric-concepts-scalability.md)
* [Planejamento de capacidade para Aplicativos do Service Fabric](service-fabric-capacity-planning.md)

[wikipartition]: https://en.wikipedia.org/wiki/Partition_(database)

[1]: ./media/service-fabric-create-your-first-application-in-visual-studio/new-project-dialog-2.png