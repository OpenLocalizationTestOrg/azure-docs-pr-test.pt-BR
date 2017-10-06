---
title: "Guia de programação aaaSCP.NET | Microsoft Docs"
description: Saiba como toouse SCP.NET toocreate. Topologias de Storm em sua empresa para usam com Storm no HDInsight.
services: hdinsight
documentationcenter: 
author: raviperi
manager: jhubbard
editor: cgronlun
ms.assetid: 34192ed0-b1d1-4cf7-a3d4-5466301cf307
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/16/2016
ms.author: raviperi
ms.openlocfilehash: a57f4217b07e0e82a3f36650308695fbb45d9128
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scp-programming-guide"></a>Guia de programação do SCP
SCP é uma plataforma toobuild em tempo real, o aplicativo de processamento de dados confiáveis, consistentes e de alto desempenho. Ele é criado na parte superior do [Apache Storm](http://storm.incubator.apache.org/) – um sistema criado pela comunidades Olá OSS de processamento de fluxo. O Storm foi projetado por Nathan Marz e tornou-se um software livre por meio do Twitter. Ele utiliza um [ZooKeeper Apache](http://zookeeper.apache.org/), Apache outro projeto tooenable coordenação de distribuído altamente confiável e gerenciamento de estado. 

Não só projeto Olá SCP movido Storm no Windows, mas também o projeto de saudação adicionado extensões e personalização do ecossistema do Windows hello. extensões de saudação incluem a experiência do desenvolvedor do .NET e bibliotecas, personalização de saudação inclui implantação baseada em Windows. 

personalização e extensão Olá é feita de forma que não precisamos projetos de OSS Olá toofork e utilizamos foi derivadas ecossistemas criadas sobre profusão de.

## <a name="processing-model"></a>Modelo de processamento
dados de saudação nos SCP são modelados como fluxos contínuos de tuplas. Normalmente Olá tuplas fluem para alguns fila pela primeira vez, em seguida, obtido e transformados por hospedado dentro de uma topologia de profusão de lógica de negócios, por fim Olá saída pode ser conectada como tuplas tooanother SCP sistema ou ser confirmada toostores como sistema de arquivos distribuídos ou bancos de dados como o SQL Server.

![Um diagrama de uma fila alimentar tooprocessing de dados, que alimenta um repositório de dados](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

No Storm, a topologia de um aplicativo define um gráfico de computação. Cada nó em uma topologia contém a lógica de processamento, e os links entre os nós indicam o fluxo de dados. Olá nós tooinject dados de entrada em topologia Olá são chamados de Spouts, que podem ser usado toosequence Olá dados. Olá dados de entrada podem residir em arquivos de log, o banco de dados transacional, o contador de desempenho do sistema nós de saudação do etc. com os fluxos de dados de entrada e saída são chamados parafusos, que Olá a filtragem de dados reais e as seleções e agregação.

O SCP oferece suporte aos melhores esforços de processamento de dados, pelo menos uma vez e exatamente uma vez. Em um aplicativo de processamento de streaming distribuído, vários erros podem ocorrer durante o processamento de dados, como interrupção da rede, falha do computador ou erro de código do usuário, entre outros. Processamento de at-least-once garante que todos os dados serão processados pelo menos uma vez por repetir automaticamente Olá dados mesmo quando o erro ocorre. O processamento de pelo menos uma vez é simples e confiável e bastante adequado a muitos aplicativos. No entanto, quando o aplicativo hello requer que a contagem exata, por exemplo, at-least-once processamento é insuficiente porque hello mesmos dados podem potencialmente ser reproduzidos na topologia de aplicativo hello. Nesse caso, exatamente-depois que o processamento é projetado resultados de saudação se toomake está correto mesmo quando dados saudação podem ser repetidos e processados várias vezes.

SCP permite que aplicativos de processo de dados .NET desenvolvedores toodevelop em tempo real ao aproveitar Olá Máquina Virtual Java (JVM) baseado em Storm sob abrangem hello. Olá .NET e JVM se comunicam por meio de soquete local TCP. Basicamente cada Spout/raio é um par de processo do .net/Java, onde a lógica de saudação do usuário é executado no processo de .net como um plug-in.

toobuild um aplicativo sobre SCP de processamento de dados, várias etapas são necessárias:

* Projetar e implementar Olá Spouts toopull nos dados da fila.
* Projetar e implementar dados de entrada parafusos tooprocess hello e salvar dados tooexternal repositórios como banco de dados.
* Design de topologia Olá, enviar e executar topologia hello. Olá topologia define vértices e dados saudação fluxos entre os vértices de saudação. SCP vai levar a especificação de topologia hello e implantá-lo em um cluster Storm, onde cada vértice é executado em um nó de lógico. Olá failover e dimensionamento serão ser manipulados pelo Agendador de tarefas Storm hello.

Este documento usará toowalk alguns exemplos simples como aplicativo de processamento de dados toobuild com SCP.

## <a name="scp-plugin-interface"></a>Interface do plug-in do SCP
Plug-ins de SCP (ou aplicativos) são EXEs autônomo que ambos podem executar dentro do Visual Studio durante a fase de desenvolvimento hello e esteja conectados ao pipeline de profusão de saudação após a implantação em produção. Gravando Olá SCP plug-in é apenas Olá mesmo que escrever quaisquer outros aplicativos do console de Windows padrão. Plataforma SCP.NET declara alguma interface para spout/brilhante e código de plug-in do usuário Olá deve implementar essas interfaces. Olá principal objetivo desse design é que o usuário Olá pode se concentrar em suas próprias lógicas de negócios e deixando outros toobe itens tratado pela plataforma SCP.NET.

código de plug-in do usuário Olá deve implementar uma das interfaces do seguinte hello, depende se a topologia de saudação é transacional ou não transacional, e se o componente de saudação é spout ou raio.

* ISCPSpout
* ISCPBolt
* ISCPTxSpout
* ISCPBatchBolt

### <a name="iscpplugin"></a>ISCPPlugin
ISCPPlugin é uma interface comum para todos os tipos de plug-ins de saudação. Atualmente, trata-se de uma interface fictícia.

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a>ISCPSpout
ISCPSpout é a interface Olá para spout não transacional.

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

Quando `NextTuple()` é chamado, Olá C\# código do usuário pode emitir uma ou mais tuplas. Se não houver nada tooemit, esse método deve retornar sem emitir nada. Observe que `NextTuple()`, `Ack()` e `Fail()` são chamados em um loop coeso em um único thread no processo C\#. Quando não houver nenhum tooemit tuplas, é toohave cortês NextTuple suspensão por um curto período de tempo (por exemplo, 10 milissegundos), não toowaste muito da CPU.

`Ack()` e `Fail()` serão chamados somente quando o mecanismo de reconhecimento estiver habilitado no arquivo de especificações. Olá `seqId` é usado tooidentify Olá tupla que é confirmada ou falhou. Para que se ack é habilitado na topologia não-transacional, Olá emit função a seguir deve ser usada em Spout:

    public abstract void Emit(string streamId, List<object> values, long seqId); 

Se não há suporte para o ack na topologia não-transacional, Olá `Ack()` e `Fail()` pode ser deixado como função vazia.

Olá `parms` parâmetros de entrada nessas funções são dicionário apenas vazio, elas estão reservadas para uso futuro.

### <a name="iscpbolt"></a>ISCPBolt
ISCPBolt é a interface de saudação de raio não transacional.

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

Quando a nova coleção de itens estiver disponível, Olá `Execute()` função será chamada tooprocess-lo.

### <a name="iscptxspout"></a>ISCPTxSpout
ISCPTxSpout é a interface Olá para spout transacional.

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

Assim como suas contrapartes não transacionais, `NextTx()`, `Ack()` e `Fail()` são chamados em um loop coeso em um único thread no processo C\#. Quando não houver nenhum tooemit de dados, é toohave cortês `NextTx` de espera por um curto período de tempo (10 milissegundos) assim como não toowaste muito da CPU.

`NextTx()`é chamado toostart uma nova transação, hello parâmetro out `seqId` tooidentify usado Olá transação, que também é usado em `Ack()` e `Fail()`. Em `NextTx()`, usuários podem emitir dados tooJava lado. Olá dados serão armazenados na reprodução de toosupport ZooKeeper. Porque a capacidade de saudação do ZooKeeper é bastante limitada, usuário só deve emitir metadados, não os dados em massa em spout transacional.

O Storm reproduzirá uma transação automaticamente se falhar, por isso, `Fail()` não deve ser chamado em um caso normal. Mas se SCP pode verificar metadados Olá emitidos pelo spout transacional, ele pode chamar `Fail()` quando Olá metadados são inválido.

Olá `parms` parâmetros de entrada nessas funções são dicionário apenas vazio, elas estão reservadas para uso futuro.

### <a name="iscpbatchbolt"></a>ISCPBatchBolt
ISCPBatchBolt é a interface de saudação de raio transacional.

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

`Execute()`é chamado quando há nova tupla que chegam a isoladas hello. `FinishBatch()` é chamado quando essa transação é encerrada. Olá `parms` parâmetro de entrada é reservado para uso futuro.

Para topologia transacional, há um conceito importante: `StormTxAttempt`. Ele tem dois campos, `TxId` e `AttemptId`. `TxId`é usado tooidentify uma transação específica e para uma determinada transação, pode haver vários tentativa se transação Olá falha e for repetido. SCP.NET novo será um diferentes ISCPBatchBolt objeto tooprocess cada `StormTxAttempt`, como o que significam Storm no lado do Java. Olá finalidade esse design é toosupport processamento de transações paralelas. Usuário deverão ser mantidos em mente que se a tentativa da transação for concluída, o objeto de ISCPBatchBolt correspondente hello será destruído e coletado como lixo.

## <a name="object-model"></a>Modelo de objeto
SCP.NET também fornece um conjunto simples de objetos de chave para os desenvolvedores tooprogram com. Eles são **Context**, **StateStore** e **SCPRuntime**. Eles serão discutidos em parte Olá restante desta seção.

### <a name="context"></a>Contexto
Contexto fornece um aplicativo de toohello ambiente em execução. Cada instância ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) possui uma instância de Contexto correspondente. funcionalidade Olá fornecida pelo contexto pode ser dividida em duas partes: parte estática hello (1), que está disponível no hello inteiro C\# processar parte dinâmica hello (2), que está disponível somente para a instância do contexto específica hello.

### <a name="static-part"></a>Parte Estática
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

`Logger` é fornecido para fins de obtenção de log.

`pluginType`é usado tooindicate tipo de plug-in de saudação de saudação C\# processo. Se Olá C\# processo é executado no modo de teste local (sem Java), é do tipo de plug-in de saudação `SCP_NET_LOCAL`.

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

`Config`é fornecida tooget parâmetros de configuração do lado do Java. Olá parâmetros são passados do lado do Java quando C\# plug-in é inicializado. Olá `Config` parâmetros são divididos em duas partes: `stormConf` e `pluginConf`.

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

`stormConf`é definidos pelo profusão de parâmetros e `pluginConf` é parâmetros Olá definidos pelo SCP. Por exemplo:

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

`TopologyContext`é fornecido o contexto de topologia do tooget Olá, é mais útil para componentes com vários paralelismo. Aqui está um exemplo:

    //demo how tooget TopologyContext info
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)                      
    {
        Context.Logger.Info("TopologyContext info:");
        TopologyContext topologyContext = Context.TopologyContext;                    
        Context.Logger.Info("taskId: {0}", topologyContext.GetThisTaskId());          
        taskIndex = topologyContext.GetThisTaskIndex();
        Context.Logger.Info("taskIndex: {0}", taskIndex);
        string componentId = topologyContext.GetThisComponentId();                    
        Context.Logger.Info("componentId: {0}", componentId);
        List<int> componentTasks = topologyContext.GetComponentTasks(componentId);  
        Context.Logger.Info("taskNum: {0}", componentTasks.Count);                    
    }

### <a name="dynamic-part"></a>Parte Dinâmica
Olá interfaces a seguir é pertinente tooa determinada a instância do contexto. a instância do contexto Olá é criada pela plataforma SCP.NET e passada toohello código do usuário:

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

Para não-transacional spout suporte ack, Olá método a seguir é fornecida:

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

Para não-transacional raio ack de suporte, ele deve explicitamente `Ack()` ou `Fail()` Olá tupla que ele recebeu. E, ao emitir nova tupla, deve também especificar âncoras Olá de tupla novo hello. Olá métodos a seguir é fornecido.

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a>StateStore
`StateStore` oferece serviços de metadados, geração de sequência monotônica e coordenação sem espera. Abstrações de simultaneidade distribuídas de níveis mais altos podem ser baseadas no `StateStore`, incluindo bloqueios distribuídos, filas distribuídas, barreiras e serviços transacionais.

SCP aplicativos podem usar o hello `State` objeto toopersist algumas informações no ZooKeeper, especialmente para a topologia transacional. Fazendo isso, se spout transacional falhar e reiniciar, ele pode recuperar informações necessárias de saudação do ZooKeeper e reinicie o pipeline de saudação.

Olá `StateStore` objeto principalmente tem estes métodos:

    /// <summary>
    /// Static method tooretrieve a state store of hello given path and connStr 
    /// </summary>
    /// <param name="storePath">StateStore Path</param>
    /// <param name="connStr">StateStore Address</param>
    /// <returns>Instance of StateStore</returns>
    public static StateStore Get(string storePath, string connStr);

    /// <summary>
    /// Create a new state object in this state store instance
    /// </summary>
    /// <returns>State from StateStore</returns>
    public State Create();

    /// <summary>
    /// Retrieve all states that were previously uncommitted, excluding all aborted states 
    /// </summary>
    /// <returns>Uncommited States</returns>
    public IEnumerable<State> GetUnCommitted();

    /// <summary>
    /// Get all hello States in hello StateStore
    /// </summary>
    /// <returns>All hello States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all hello committed states
    /// </summary>
    /// <returns>Registries contain hello Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all hello Aborted State in hello StateStore
    /// </summary>
    /// <returns>Registries contain hello Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of hello State</typeparam>
    public State GetState(long stateId)

Olá `State` objeto principalmente tem estes métodos:

    /// <summary>
    /// Set hello status of hello state object toocommit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set hello status of hello state object tooabort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under hello give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get hello attribute value associated with hello given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

Para Olá `Commit()` método, quando simpleMode está definida tootrue, ele simplesmente excluir Olá correspondente ZNode em ZooKeeper. Caso contrário, ele excluirá Olá ZNode atual e adicionar um novo nó Olá confirmado\_caminho.

### <a name="scpruntime"></a>SCPRuntime
SCPRuntime fornece Olá dois métodos a seguir.

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

`Initialize()`é o ambiente de tempo de execução Olá SCP tooinitialize usado. Nesse método, Olá C\# processo conectará toohello Java e obtém os parâmetros de configuração e do contexto de topologia.

`LaunchPlugin()`tookick usado fora da mensagem de saudação está processando o loop. Nesse loop, Olá C\# plug-in receberá mensagens formulário lado Java (incluindo sinais tuplas e controle) e processar mensagens de saudação, talvez chamando o método de interface hello fornecem pelo código do usuário hello. o parâmetro de entrada Hello para o método `LaunchPlugin()` é um delegado que pode retornar um objeto que implementa a interface ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

Para ISCPBatchBolt, podemos obter `StormTxAttempt` de `parms`e usá-lo toojudge se trata de uma tentativa de reproduzido. Geralmente, isso é feito em um raio de confirmação de saudação e ele é demonstrado no hello `HelloWorldTx` exemplo.

Em geral, Olá SCP plug-ins pode ser executado em dois modos aqui:

1. Modo de teste local: Nesse modo, Olá SCP plug-ins (Olá C\# código do usuário) executado dentro do Visual Studio durante a fase de desenvolvimento de saudação. `LocalContext`pode ser usado nesse modo, o que fornece o método tooserialize Olá emitido tuplas toolocal arquivos e leia-os de volta toomemory.
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. Modo normal: Nesse modo, plug-ins do hello SCP são iniciados pelo processo de java storm.
   
    Aqui está um exemplo da inicialização do plugin do SCP:
   
        namespace Scp.App.HelloWorld
        {
        public class Generator : ISCPSpout
        {
            … …
            public static Generator Get(Context ctx, Dictionary<string, Object> parms)
            {
            return new Generator(ctx);
            }
        }
   
        class HelloWorld
        {
            static void Main(string[] args)
            {
            /* Setting hello environment variable here can change hello log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a>Linguagem de Especificação da Topologia
A Especificação da Topologia do SCP é uma linguagem específica do domínio para descrever e configurar topologias do SCP. Ela se baseia no Clojure DSL do Storm (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) e é estendida pelo SCP.

Especificações de topologia podem ser enviadas diretamente toostorm de cluster para execução via Olá ***runspec*** comando.

SCP.NET tem adicionar siga funções toodefine Olá topologia transacional:

| **Novas funções** | **Parâmetros** | **Descrição** |
| --- | --- | --- |
| **tx-topolopy** |topology-name<br />spout-map<br />bolt-map |Definir uma topologia transacional com o nome de topologia hello, &nbsp;spouts mapa de definição e mapa de definição de parafusos Olá |
| **scp-tx-spout** |exec-name<br />args<br />fields |Defina um spout transacional. Ele será executado o aplicativo hello com ***nome exec*** usando ***args***.<br /><br />Olá ***campos*** é Olá campos de saída para spout |
| **scp-tx-batch-bolt** |exec-name<br />args<br />fields |Defina um bolt em lote transacional. Ele será executado o aplicativo hello com ***nome exec*** usando ***args.***<br /><br />Olá campos é hello campos de saída para o raio. |
| **scp-tx-commit-bolt** |exec-name<br />args<br />fields |Defina um bolt confirmador transacional. Ele será executado o aplicativo hello com ***nome exec*** usando ***args***.<br /><br />Olá ***campos*** é Olá campos de saída para o raio |
| **nontx-topolopy** |topology-name<br />spout-map<br />bolt-map |Definir uma topologia não transacional com o nome de topologia hello,&nbsp; spouts mapa de definição e mapa de definição de parafusos Olá |
| **scp-spout** |exec-name<br />args<br />fields<br />Parâmetros |Defina um spout não transacional. Ele será executado o aplicativo hello com ***nome exec*** usando ***args***.<br /><br />Olá ***campos*** é Olá campos de saída para spout<br /><br />Olá ***parâmetros*** é opcional, usá-lo toospecify alguns parâmetros, como "nontransactional.ack.enabled". |
| **scp-bolt** |exec-name<br />args<br />fields<br />Parâmetros |Defina um bolt não transacional. Ele será executado o aplicativo hello com ***nome exec*** usando ***args***.<br /><br />Olá ***campos*** é Olá campos de saída para o raio<br /><br />Olá ***parâmetros*** é opcional, usá-lo toospecify alguns parâmetros, como "nontransactional.ack.enabled". |

O SCP.NET possui as seguintes palavras-chave definidas:

| **Palavras-chave** | **Descrição** |
| --- | --- |
| **:name** |Definir Olá topologia nome |
| **:topology** |Definir Olá topologia usando Olá acima funções e que criam as. |
| **:p** |Defina a dica de paralelismo Olá para cada spout ou raio. |
| **:config** |Definir Configurar parâmetro ou atualização Olá existentes |
| **:schema** |Defina Olá esquema de fluxo. |

Todos os parâmetros utilizados com frequência:

| **Parâmetro** | **Descrição** |
| --- | --- |
| **"plugin.name"** |nome do arquivo exe do plug-in de saudação c# |
| **"plugin.args"** |args do plugin |
| **"output.schema"** |Esquema de saída |
| **"nontransactional.ack.enabled"** |Se o reconhecimento está ativado para a topologia não transacional |

comando de runspec Hello será implantado junto com os bits de hello, uso de saudação é como:

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

Olá ***recurso dir*** parâmetro é opcional, você precisa toospecify, quando você deseja tooplug C\# aplicativo e esse diretório conterá aplicativo hello, dependências hello e configurações.

Olá ***classpath*** parâmetro também é opcional. É usado toospecify Olá Java classpath arquivo especificações Olá contém Java Spout ou raio.

## <a name="miscellaneous-features"></a>Recursos diversos
### <a name="input-and-output-schema-declaration"></a>Declaração de esquema de entrada e saída
usuário Olá pode emitir tupla em C\# processar, hello plataforma precisa tooserialize Olá tupla em byte [], do lado do tooJava de transferência, e Storm transferirá os destinos de toohello essa tupla. Enquanto isso, no componente downstream, Olá C\# processo receber tupla do lado do java e convertê-la tipos originais toohello pela plataforma, todas essas operações são ocultos por Olá plataforma.

toosupport Olá serialização e desserialização de, o código do usuário precisa toodeclare esquema de saudação do hello entradas e saídas.

esquema de fluxo de entrada/saída de saudação é definido como um dicionário, chave de saudação é Olá StreamId e Olá é Olá tipos de colunas de saudação. componente de saudação pode ter vários fluxos declarados.

    public class ComponentStreamSchema
    {
        public Dictionary<string, List<Type>> InputStreamSchema { get; set; }
        public Dictionary<string, List<Type>> OutputStreamSchema { get; set; }
        public ComponentStreamSchema(Dictionary<string, List<Type>> input, Dictionary<string, List<Type>> output)
        {
            InputStreamSchema = input;
            OutputStreamSchema = output;
        }
    }


Objeto de contexto, temos Olá adicionado seguinte API:

    public void DeclareComponentSchema(ComponentStreamSchema schema)

Código do usuário deve verificar se tuplas Olá emitidas obedecer ao esquema Olá definida para esse fluxo ou sistema Olá lançará uma exceção de tempo de execução.

### <a name="multi-stream-support"></a>Suportes a múltiplos fluxos
SCP dá suporte ao usuário código tooemit ou recebimento de vários fluxos distintos em Olá mesmo tempo. suporte de saudação reflete no objeto de contexto hello como Olá Emit método aceita um parâmetro de ID de fluxo opcionais.

Dois métodos em Olá objeto de contexto SCP.NET foram adicionados. Eles são usados tooemit tupla ou tuplas toospecify StreamId. Olá StreamId é uma cadeia de caracteres e precisa toobe consistente em ambas as C\# e Olá especificação de definição de topologia.

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

fluxo de não existente de tooa emissão Olá fará com que as exceções de tempo de execução.

### <a name="fields-grouping"></a>Agrupamento de Campos
Olá que compilação no agrupamento de campos em Strom não está funcionando corretamente em SCP.NET. Em Olá lado Java Proxy, todos os tipos de dados de campos de saudação são, na verdade, byte [] e campos Olá agrupamento usa Olá byte [] objeto hash código tooperform Olá de agrupamento. o código de hash de objeto do Hello byte [] é o endereço de saudação do objeto na memória. Para que agrupar Olá seja incorreto de dois bytes [] objetos Olá que compartilhar o mesmo conteúdo, mas não Olá mesmo endereço.

SCP.NET adiciona um método de agrupamento personalizados, e ele usará o conteúdo de saudação do agrupamento de Olá Olá byte [] toodo. Em **especificação** sintaxe de saudação do arquivo, é como:

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


Aqui,

1. “scp-field-group” significa “Agrupamento de campo personalizado implementado pelo SCP”.
2. “:tx” ou “:non-tx” significa que se trata de uma topologia transacional. Precisamos essas informações como Olá iniciando o índice é diferente em tx versus não tx topologias.
3. [0,1] significa o hashset dos IDs do campo, começando do 0.

### <a name="hybrid-topology"></a>Topologia híbrida
Olá que Storm nativo é escrito em Java. E SCP.Net foi aprimorada tooenable nosso toowrite personalizada C\# código toohandle sua lógica de negócios. Mas também damos suporte a topologias híbridas, que contêm não apenas spouts/bolts do C\#, mas também do Java.

### <a name="specify-java-spoutbolt-in-spec-file"></a>Especificar o Spout/Bol do Java no arquivo de especificações
No arquivo especial, "scp spout" e "raio scp" também podem ser usado toospecify Java Spouts e parafusos, aqui está um exemplo:

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

Aqui `microsoft.scp.example.HybridTopology.Generator` é Olá nome da classe Java Spout de saudação.

### <a name="specify-java-classpath-in-runspec-command"></a>Especificar o caminho de classe do Java no comando runSpec
Se você quiser toosubmit topologia contendo Java Spouts ou parafusos, for necessário toofirst Olá de compilação Java Spouts ou parafusos e obter arquivos Jar de saudação. Em seguida, você deve especificar o classpath java Olá que contém os arquivos Jar do hello durante o envio de topologia. Aqui está um exemplo:

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

Aqui **exemplos\\HybridTopology\\java\\destino\\**  é o hello pasta que contém o arquivo Jar do Java Spout/raio de saudação.

### <a name="serialization-and-deserialization-between-java-and-c"></a>Serialização e desserialização entre Java e C\
Nosso componente SCP inclui lado de Java e de C\#. Em ordem toointeract com Spouts/parafusos Java nativo, serialização/desserialização deve ser feita entre C e do Java\# lado, conforme ilustrado na Olá gráfico a seguir.

![diagrama de componente de java enviando componente tooSCP enviar tooJava componente](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. **Serialização no lado do Java e desserialização no lado do C\#**
   
   Primeiro, fornecemos a implementação padrão para serialização no lado do Java e a desserialização no lado do C\#. método de serialização Hello no lado do Java pode ser especificado no arquivo especificações:
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   Olá método de desserialização em C\# deve ser especificada em C\# código do usuário:
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   Esta implementação padrão deve lidar com a maioria dos casos, se o tipo de dados de saudação não é muito complexo. Em certos casos, ou porque hello tipo de dados do usuário é muito complexo ou hello desempenho de nossa implementação padrão não atende aos Olá requisito do usuário, o usuário pode plug-in sua própria implementação.
   
   Olá serializar interface java lado é definida como:
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   Olá desserializar interface em C\# lado é definida como:
   
   interface pública ICustomizedInteropCSharpDeserializer
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. **Serialização no lado do C\# e desserialização no lado do Java**
   
   Olá o método de serialização em C\# deve ser especificada em C\# código do usuário:
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   Olá método de desserialização no lado do Java deve ser especificado no arquivo especificações:
   
     (scp-spout
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   Aqui "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" é o nome de saudação do desserializador e "microsoft.scp.example.HybridTopology.Person" é dados de saudação de classe de destino de saudação são desserializados para.
   
   O usuário também pode usar um plug-in para sua própria implementação de serializador de C\# e desserializador de Java. Esta é a interface Olá para C\# serializador:
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   Esta é a interface de saudação para desserialização de Java:
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a>Modo de host do SCP
Nesse modo, o usuário pode compilar tooDLL seus códigos e usar SCPHost.exe fornecido pela topologia de toosubmit SCP. arquivo de especificação de saudação tem esta aparência:

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

Aqui, `plugin.name` é especificado como `SCPHost.exe` fornecido pelo SDK do SCP. O SCPHost.exe aceita exatamente três parâmetros:

1. Olá primeiro um é nome da DLL hello, que é `"HelloWorld.dll"` neste exemplo.
2. Olá, um segundo é nome da classe hello, que é `"Scp.App.HelloWorld.Generator"` neste exemplo.
3. Olá terceiro um é Olá nome de um método estático público, que pode ser invocado tooget uma instância de ISCPPlugin.

No modo do host, o código do usuário é compilado como DLL e é invocado pela plataforma SCP. Então plataforma SCP pode obter controle total da lógica de processamento inteiro hello. Portanto, recomendamos que nossos clientes toosubmit topologia em modo de SCP do host porque ele pode simplificar a experiência de desenvolvimento hello e nos trazem mais flexibilidade e melhor compatibilidade com versões anteriores também a versão mais recente.

## <a name="scp-programming-examples"></a>Exemplos de programação do SCP
### <a name="helloworld"></a>HelloWorld
**HelloWorld** é um exemplo muito simples tooshow uma amostra de SCP.Net. Ele usa uma topologia não transacional com um spout chamado **generator** e dois bolts chamados **splitter** e **counter**. spout Olá **gerador** irá gerar aleatoriamente alguns sentenças e emitir essas frases muito**divisor**. raio Olá **divisor** serão divididas Olá sentenças toowords e emitir essas palavras muito**contador** raio. Olá raio "counter" usa um número de ocorrência do dicionário toorecord saudação de cada palavra.

Há dois arquivos de especificações, **HelloWorld.spec** e **HelloWorld\_EnableAck.spec** para este exemplo. Em Olá C\# código, ele pode descobrir se o ack está habilitado obtendo pluginConf de saudação do lado do Java.

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

Spout Olá, se a confirmação for habilitada, um dicionário é usado toocache Olá tuplas que não foram controladas. Se for chamado Fail(), hello tupla com falha será reproduzida:

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get hello cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay hello failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a>HelloWorldTx
Olá **HelloWorldTx** exemplo demonstra como topologia transacional tooimplement. Ele tem um spout chamado **generator**, um bolt em lote chamado **partial-count** e um bolt de confirmação chamado **count-sum**. Também há três arquivos txt pré-criados: **DataSource0.txt**, **DataSource1.txt** e **DataSource2.txt**.

Em cada transação, Olá spout **gerador** será aleatoriamente escolher dois arquivos de saudação criada previamente três arquivos e emitir toohello de nomes de arquivo hello dois **parcial contagem** raio. raio Olá **parcial contagem** obterá primeiro nome de arquivo hello da tupla Olá recebida, Olá abrir arquivo e contagem Olá o número de palavras neste arquivo e, finalmente, emitir hello word número toohello **contagem total**raio. Olá **contagem soma** raio resumirá contagem total de saudação.

tooachieve **exatamente uma vez** semântica, raio de confirmação de saudação **contagem soma** necessário toojudge se trata de uma transação repetida. Neste exemplo, ele possui uma variável do membro estático:

    public static long lastCommittedTxId = -1; 

Quando uma instância de ISCPBatchBolt é criada, ele receberá Olá `txAttempt` de parâmetros de entrada:

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from hello input parms */
        if (parms.ContainsKey(Constants.STORM_TX_ATTEMPT))
        {
            StormTxAttempt txAttempt = (StormTxAttempt)parms[Constants.STORM_TX_ATTEMPT];
            return new CountSum(ctx, txAttempt);
        }
        else
        {
            throw new Exception("null txAttempt");
        }
    }

Quando `FinishBatch()` é chamado, hello `lastCommittedTxId` será update se não for uma transação repetida.

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update hello toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a>HybridTopology
Essa topologia contém um Spout do Java e um Bolt do C\#. Ele usa Olá implementação padrão de serialização e desserialização fornecida pela plataforma SCP. Por favor Olá ref **HybridTopology.spec** na **exemplos\\HybridTopology** pasta para obter detalhes de especificação de arquivo hello, e **SubmitTopology.bat** como toospecify Java classpath.

### <a name="scphostdemo"></a>SCPHostDemo
Este exemplo é Olá essencialmente igual HelloWorld. Hello somente diferença é que o código de usuário Olá é compilado como DLL e topologia Olá é enviada usando SCPHost.exe. Faça a seção de saudação de ref "Modo de Host do SCP" para explicação mais detalhada.

## <a name="next-steps"></a>Próximas etapas
Para obter exemplos de topologias Storm criados usando o SCP, consulte seguinte hello:

* [Desenvolver topologias C# para o Apache Storm no HDInsight usando o Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Processar eventos dos Hubs de Evento do Azure com o Storm no HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [Criar vários fluxos de dados em uma topologia Storm em C#](hdinsight-storm-twitter-trending.md)
* [Usar dados do Power Bi toovisualize de uma topologia Storm](hdinsight-storm-power-bi-topology.md)
* [Processar dados do sensor do veículo a partir de Hubs de Evento usando o Storm no HDInsight](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [Extração, transformação e carregamento (ETL) de Hubs de eventos do Azure tooHBase](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [Correlacionar eventos usando Storm e HBase no HDInsight](hdinsight-storm-correlation-topology.md)

