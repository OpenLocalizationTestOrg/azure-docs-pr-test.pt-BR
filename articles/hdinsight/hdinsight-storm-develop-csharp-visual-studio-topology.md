---
title: "topologias de profusão de aaaApache com Visual Studio e c# - HDInsight do Azure | Microsoft Docs"
description: "Saiba como toocreate as topologias Storm em c#. Crie uma topologia de contagem de palavras simples no Visual Studio usando ferramentas Hadoop de saudação do Visual Studio."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 380d804f-a8c5-4b20-9762-593ec4da5a0d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/02/2017
ms.author: larryfr
ms.openlocfilehash: b3fb01a4dda144fd7fb4141e624e31e667f93753
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="develop-c-topologies-for-apache-storm-by-using-hello-data-lake-tools-for-visual-studio"></a>Desenvolver topologias c# para o Apache Storm usando ferramentas de Data Lake Olá para o Visual Studio

Saiba como toocreate uma topologia c# Storm usando hello Azure Data Lake (Hadoop) ferramentas para Visual Studio. Este documento orienta pelo processo de saudação de criar um projeto Storm no Visual Studio, testá-lo localmente e implantá-la tooan Apache Storm no cluster HDInsight do Azure.

Você também aprenderá como topologias híbridas toocreate que usam componentes c# e Java.

> [!NOTE]
> Enquanto etapas Olá neste documento dependem de um ambiente de desenvolvimento do Windows com o Visual Studio, o projeto compilado Olá pode ser tooeither enviado um cluster Linux ou HDInsight baseados no Windows. Somente os clusters baseados em Linux criados depois de 28 de outubro de 2016 são compatíveis com as topologias do SCP.NET.

topologia toouse c# com um cluster baseado em Linux, você deve atualizar Olá Microsoft.SCP.Net.SDK NuGet pacote usado pelo seu projeto tooversion 0.10.0.6 ou posterior. versão de saudação do pacote de saudação também deve corresponder a versão principal de saudação do Storm instalado no HDInsight.

| Versão do HDInsight | Versão do Storm | Versão do SCP.NET | Versão Mono padrão |
|:-----------------:|:-------------:|:---------------:|:--------------------:|
| 3.3 |0.10.x |0.10.x.x</br>(somente em HDInsight baseado no Windows) | ND |
| 3.4 | 0.10.0.x | 0.10.0.x | 3.2.8 |
| 3,5 | 1.0.2.x | 1.0.0.x | 4.2.1 |
| 3.6 | 1.1.0.x | 1.0.0.x | 4.2.8 |

> [!IMPORTANT]
> C# topologias em clusters baseados em Linux devem usar o .NET 4.5 e use toorun Mono no cluster do HDInsight hello. Verificar [compatibilidade Mono](http://www.mono-project.com/docs/about-mono/compatibility/) para possíveis incompatibilidades.

## <a name="install-visual-studio"></a>Instalar Visual Studio

Você pode desenvolver c# topologias com SCP.NET usando uma saudação seguintes versões do Visual Studio:

* Visual Studio 2012 com [Atualização 4](http://www.microsoft.com/download/details.aspx?id=39305)

* Visual Studio 2013 com [Atualização 4](http://www.microsoft.com/download/details.aspx?id=44921) ou [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)

* Visual Studio 2015 ou [Visual Studio 2015 Community](https://go.microsoft.com/fwlink/?LinkId=532606)

* Visual Studio 2017 (qualquer edição)

## <a name="install-data-lake-tools-for-visual-studio"></a>Instalar ferramentas do Data Lake para Visual Studio

ferramentas de Data Lake tooinstall para Visual Studio, siga as etapas de saudação em [começar a usar as ferramentas de Data Lake para Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

## <a name="install-java"></a>Instalar o Java

Quando você enviar uma topologia Storm do Visual Studio, SCP.NET gera um arquivo zip que contém as dependências e topologia de saudação. Java é usado toocreate esses arquivos, zip, porque ele usa um formato que é mais compatível com clusters baseados em Linux.

1. Instale Olá Java Developer Kit (JDK) 7 ou posterior em seu ambiente de desenvolvimento. Você pode obter Olá Oracle JDK [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html). Você também pode usar [outras distribuições do Java](http://openjdk.java.net/).

2. Olá `JAVA_HOME` diretório de toohello de ponto de deve variável de ambiente que contém Java.

3. Olá `PATH` variável de ambiente deve incluir Olá `%JAVA_HOME%\bin` directory.

Você pode usar o hello c# console aplicativo tooverify Java e hello JDK estão corretamente instalados a seguir:

```csharp
using System;
using System.IO;
namespace ConsoleApplication2
{
   class Program
   {
       static void Main(string[] args)
       {
           string javaHome = Environment.GetEnvironmentVariable(“JAVA_HOME”);
           if (!string.IsNullOrEmpty(javaHome))
           {
               string jarExe = Path.Combine(javaHome + @”\bin”, “jar.exe”);
               if (File.Exists(jarExe))
               {
                   Console.WriteLine(“JAVA Is Installed properly”);
                    return;
               }
               else
               {
                   Console.WriteLine(“A valid JAVA JDK is not found. Looks like JRE is installed instead of JDK.”);
               }
           }
           else
           {
             Console.WriteLine(“A valid JAVA JDK is not found. JAVA_HOME environment variable is not set.”);
           }
       }  
   }
}
```

## <a name="storm-templates"></a>Modelos do Storm

ferramentas de Data Lake Olá para Visual Studio fornecem Olá modelos a seguir:

| Tipo de projeto | Demonstra |
| --- | --- |
| Aplicativo Storm |Um projeto de topologia Storm vazio. |
| Amostra de gravador do SQL Azure Storm |Como toowrite tooAzure banco de dados SQL. |
| Amostra de leitor do Azure Cosmos DB do Storm |Como tooread do banco de dados do Azure Cosmos. |
| Amostra do gravador do Azure Cosmos DB do Storm |Como toowrite tooAzure Cosmos DB. |
| Amostra de leitor de Hub de Eventos do Storm |Como tooread de Hubs de eventos do Azure. |
| Amostra do gravador de Hub de Eventos do Storm |Como toowrite tooAzure Hubs de eventos. |
| Amostra de leitor HBase do Storm |Como clusters de tooread do HBase em HDInsight. |
| Amostra de gravador HBase do Storm |Como clusters de tooHBase toowrite no HDInsight. |
| Amostra híbrida do Storm |Como toouse um componente de Java. |
| Amostra do Storm |Uma topologia básica de contagem de palavras. |

> [!WARNING]
> Nem todos os modelos funcionarão com o HDInsight baseado em Linux. Pacotes NuGet usados pelos modelos de saudação podem não ser compatíveis com Mono. Verificar Olá [compatibilidade Mono](http://www.mono-project.com/docs/about-mono/compatibility/) de documento e usar o hello [.NET portabilidade analisador](hdinsight-hadoop-migrate-dotnet-to-linux.md#automated-portability-analysis) tooidentify possíveis problemas.

Etapas Olá neste documento, você usa Olá básica Storm aplicativo projeto tipo toocreate uma topologia.

### <a name="hbase-templates-notes"></a>Notas de modelos de HBase

Olá HBase leitor e modelos de gravador usam Olá API REST do HBase, não Olá HBase API do Java, toocommunicate com um HBase no cluster HDInsight.

### <a name="eventhub-templates-notes"></a>Notas de modelos do EventHub

> [!IMPORTANT]
> Olá baseados em Java EventHub spout componente incluído com hello modelo EventHub leitor pode não funcionar com Storm no HDInsight versão 3.5 ou posterior. Uma versão atualizada deste componente está disponível em [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/HDI3.5/lib).

Para uma topologia de exemplo que usa esse componente e funciona com Storm no HDInsight 3.5, consulte [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

## <a name="create-a-c-topology"></a>Criar uma topologia C#

1. Abra o Visual Studio, selecione **Arquivo** > **Novo** e **Projeto**.

2. De saudação **novo projeto** janela, expanda **instalado** > **modelos**e selecione **Azure Data Lake**. Saudação de modelos, selecione lista **profusão de aplicativo**. Na parte inferior de saudação da tela hello, digite **WordCount** como nome de saudação do aplicativo hello.

    ![Captura de tela da janela Novo Projeto](./media/hdinsight-storm-develop-csharp-visual-studio-topology/new-project.png)

3. Depois que você criou o projeto hello, você deve ter Olá seguintes arquivos:

   * **Program.CS**: este arquivo define topologia Olá para o seu projeto. Uma topologia padrão consistindo em um spout e um bolt é criada por padrão.

   * **Spout.cs**: um spout de exemplo que emite números aleatórios.

   * **Bolt.CS**: um raio de exemplo que mantém uma contagem de números emitidos pelo spout hello.

     Quando você cria o projeto hello, downloads do NuGet hello mais recente [SCP.NET pacote](https://www.nuget.org/packages/Microsoft.SCP.Net.SDK/).

     [!INCLUDE [scp.net version important](../../includes/hdinsight-storm-scpdotnet-version.md)]

### <a name="implement-hello-spout"></a>Spout de saudação implementar

1. Abra **Spout.cs**. Spouts são dados tooread usado em uma topologia de uma fonte externa. Olá principais componentes para uma spout são:

   * **NextTuple**: chamado como uma tempestade quando spout Olá é permitido tooemit novas tuplas.

   * **ACK** (topologia transacional somente): trata confirmações iniciadas por outros componentes na topologia de saudação de tuplas enviadas do spout hello. Confirmar uma tupla avisa spout Olá que ele foi processado com êxito por componentes downstream.

   * **Falha** (topologia transacional somente): trata tuplas que são falha processamento de outros componentes na topologia de saudação. Implementando um método Fail permite toore-emitir tupla Olá para que possa ser processado novamente.

2. Substitua o conteúdo de saudação do hello **Spout** classe com hello texto a seguir. Este spout aleatoriamente emite uma frase em topologia hello.

    ```csharp
    private Context ctx;
    private Random r = new Random();
    string[] sentences = new string[] {
        "hello cow jumped over hello moon",
        "an apple a day keeps hello doctor away",
        "four score and seven years ago",
        "snow white and hello seven dwarfs",
        "i am at two with nature"
    };

    public Spout(Context ctx)
    {
        // Set hello instance context
        this.ctx = ctx;

        Context.Logger.Info("Generator constructor called");

        // Declare Output schema
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // hello schema for hello default output stream is
        // a tuple that contains a string field
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(null, outputSchema));
    }

    // Get an instance of hello spout
    public static Spout Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Spout(ctx);
    }

    public void NextTuple(Dictionary<string, Object> parms)
    {
        Context.Logger.Info("NextTuple enter");
        // hello sentence toobe emitted
        string sentence;

        // Get a random sentence
        sentence = sentences[r.Next(0, sentences.Length - 1)];
        Context.Logger.Info("Emit: {0}", sentence);
        // Emit it
        this.ctx.Emit(new Values(sentence));

        Context.Logger.Info("NextTuple exit");
    }

    public void Ack(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        // Only used for transactional topologies
    }
    ```

### <a name="implement-hello-bolts"></a>Implementar Olá parafusos

1. Excluir Olá **Bolt.cs** arquivo de projeto do hello.

2. Em **Solution Explorer**, clique com botão direito hello e selecione **adicionar** > **novo item**. Olá, selecione lista **profusão de raio**e digite **Splitter.cs** como nome de saudação. Repita este toocreate processo chamada de uma segunda brilhante **Counter.cs**.

   * **Splitter.cs**: implementa um bolt que divide as frases em palavras individuais e emite um novo fluxo de palavras.

   * **Counter.CS**: implementa um raio contagens de cada palavra e emite um novo fluxo de palavras e contagem de saudação para cada palavra.

     > [!NOTE]
     > Esses parafusos de leitura e gravação toostreams, mas você também pode usar um raio toocommunicate com fontes, como um banco de dados ou o serviço.

3. Abra **Splitter.cs**. Ele tem apenas um método por padrão: **Execute**. Olá método Execute é chamado quando o raio Olá recebe uma tupla para o processamento. Aqui, você pode ler e processar tuplas de entradas e emitir tuplas de saída.

4. Substitua o conteúdo de saudação do hello **divisor** classe com hello código a seguir:

    ```csharp
    private Context ctx;

    // Constructor
    public Splitter(Context ctx)
    {
        Context.Logger.Info("Splitter constructor called");
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // Input contains a tuple with a string field (hello sentence)
        inputSchema.Add("default", new List<Type>() { typeof(string) });
        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // Outbound contains a tuple with a string field (hello word)
        outputSchema.Add("default", new List<Type>() { typeof(string) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance of hello bolt
    public static Splitter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Splitter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello sentence from hello tuple
        string sentence = tuple.GetString(0);
        // Split at space characters
        foreach (string word in sentence.Split(' '))
        {
            Context.Logger.Info("Emit: {0}", word);
            //Emit each word
            this.ctx.Emit(new Values(word));
        }

        Context.Logger.Info("Execute exit");
    }
    ```

5. Abra **Counter.cs**e substitua o conteúdo de classe de saudação com os seguintes hello:

    ```csharp
    private Context ctx;

    // Dictionary for holding words and counts
    private Dictionary<string, int> counts = new Dictionary<string, int>();

    // Constructor
    public Counter(Context ctx)
    {
        Context.Logger.Info("Counter constructor called");
        // Set instance context
        this.ctx = ctx;

        // Declare Input and Output schemas
        Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string field - hello word
        inputSchema.Add("default", new List<Type>() { typeof(string) });

        Dictionary<string, List<Type>> outputSchema = new Dictionary<string, List<Type>>();
        // A tuple containing a string and integer field - hello word and hello word count
        outputSchema.Add("default", new List<Type>() { typeof(string), typeof(int) });
        this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, outputSchema));
    }

    // Get a new instance
    public static Counter Get(Context ctx, Dictionary<string, Object> parms)
    {
        return new Counter(ctx);
    }

    // Called when a new tuple is available
    public void Execute(SCPTuple tuple)
    {
        Context.Logger.Info("Execute enter");

        // Get hello word from hello tuple
        string word = tuple.GetString(0);
        // Do we already have an entry for hello word in hello dictionary?
        // If no, create one with a count of 0
        int count = counts.ContainsKey(word) ? counts[word] : 0;
        // Increment hello count
        count++;
        // Update hello count in hello dictionary
        counts[word] = count;

        Context.Logger.Info("Emit: {0}, count: {1}", word, count);
        // Emit hello word and count information
        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new List<SCPTuple> { tuple }, new Values(word, count));
        Context.Logger.Info("Execute exit");
    }
    ```

### <a name="define-hello-topology"></a>Definir a topologia de saudação

Spouts e parafusos são organizados em um gráfico, que define como os dados de saudação fluem entre os componentes. Para esta topologia, o gráfico de saudação é da seguinte maneira:

![Diagrama de como os componentes são organizados](./media/hdinsight-storm-develop-csharp-visual-studio-topology/wordcount-topology.png)

Sentenças são emitidas pelos spout hello e são distribuídas tooinstances de raio do divisor de saudação. raio de separador de saudação quebra sentenças Olá em palavras, que são distribuídas toohello raio de contador.

Porque a contagem de palavras é mantida localmente na instância do contador hello, queremos toomake-se de que palavras específicas fluem toohello mesma instância do contador de raio. Cada instância controla palavras específicas. Como o raio do divisor Olá mantém sem estado, realmente não importa qual instância do divisor Olá recebe quais sentença.

Abra **Program.cs**. método importante Olá é **GetTopologyBuilder**, que é usado toodefine Olá topologia enviada tooStorm. Substitua o conteúdo de saudação do **GetTopologyBuilder** com hello topologia de saudação do código tooimplement descrita anteriormente a seguir:

```csharp
// Create a new topology named 'WordCount'
TopologyBuilder topologyBuilder = new TopologyBuilder("WordCount" + DateTime.Now.ToString("yyyyMMddHHmmss"));

// Add hello spout toohello topology.
// Name hello component 'sentences'
// Name hello field that is emitted as 'sentence'
topologyBuilder.SetSpout(
    "sentences",
    Spout.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"sentence"}}
    },
    1);
// Add hello splitter bolt toohello topology.
// Name hello component 'splitter'
// Name hello field that is emitted 'word'
// Use suffleGrouping toodistribute incoming tuples
//   from hello 'sentences' spout across instances
//   of hello splitter
topologyBuilder.SetBolt(
    "splitter",
    Splitter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word"}}
    },
    1).shuffleGrouping("sentences");

// Add hello counter bolt toohello topology.
// Name hello component 'counter'
// Name hello fields that are emitted 'word' and 'count'
// Use fieldsGrouping tooensure that tuples are routed
//   toocounter instances based on hello contents of field
//   position 0 (hello word). This could also have been
//   List<string>(){"word"}.
//   This ensures that hello word 'jumped', for example, will always
//   go toohello same instance
topologyBuilder.SetBolt(
    "counter",
    Counter.Get,
    new Dictionary<string, List<string>>()
    {
        {Constants.DEFAULT_STREAM_ID, new List<string>(){"word", "count"}}
    },
    1).fieldsGrouping("splitter", new List<int>() { 0 });

// Add topology config
topologyBuilder.SetTopologyConfig(new Dictionary<string, string>()
{
    {"topology.kryo.register","[\"[B\"]"}
});

return topologyBuilder;
```

## <a name="submit-hello-topology"></a>Enviar Olá topologia

1. Em **Solution Explorer**, clique com botão direito hello e selecione **enviar tooStorm no HDInsight**.

   > [!NOTE]
   > Se solicitado, insira as credenciais de saudação para sua assinatura do Azure. Se você tiver mais de uma assinatura, entre toohello que contém seu Storm no cluster HDInsight.

2. Selecione seu Storm no cluster HDInsight Olá **Cluster Storm** lista suspensa e selecione **enviar**. Você pode monitorar se o envio de saudação foi bem-sucedida usando Olá **saída** janela.

3. Quando a topologia de saudação foi enviada com êxito, Olá **Storm topologias** para cluster Olá deve aparecer. Selecione Olá **WordCount** topologia de saudação listar tooview informações sobre Olá executando topologia.

   > [!NOTE]
   > Você também pode exibir **topologias Storm** do **Gerenciador de Servidores**. Expanda **Azure** > **HDInsight**, clique com o botão direito do mouse em cluster do Storm no HDInsight e selecione **Exibir Topologias do Storm**.

    informações de tooview sobre os componentes de saudação na topologia hello, clique duas vezes no componente Olá no diagrama de saudação.

4. De saudação **Resumo da topologia** exibir, clique em **Kill** toostop topologia de saudação.

   > [!NOTE]
   > Topologias Storm continuam toorun até que eles são desativados ou Olá cluster é excluído.

## <a name="transactional-topology"></a>Topologia transacional

topologia de saudação anterior não é transacional. componentes de saudação na topologia de saudação não implementam mensagens tooreplaying de funcionalidade. Para obter um exemplo de uma topologia de transacional, criar um projeto e selecione **profusão de exemplo** como o tipo de projeto hello.

Topologias transacionais implementam Olá toosupport reprodução de dados a seguir:

* **Cache de metadados**: spout Olá deve armazenar metadados sobre dados Olá emitidos, para que os dados de saudação podem ser recuperados e emitidos novamente se ocorrer uma falha. Como dados de saudação emitidos pelo exemplo hello são pequenos, dados brutos de saudação para cada tupla são armazenados em um dicionário para reprodução.

* **ACK**: cada raio na topologia Olá pode chamar `this.ctx.Ack(tuple)` tooacknowledge que ele processou com êxito uma tupla. Quando todos os parafusos controladas Olá tupla, Olá `Ack` método spout Olá é invocado. Olá `Ack` método permite que os dados de tooremove de spout Olá que foi armazenado em cache para reprodução.

* **Falha**: cada raio pode chamar `this.ctx.Fail(tuple)` tooindicate que o processamento falhou para uma coleção de itens. Falha de saudação propaga toohello `Fail` método spout hello, onde pode ser reproduzida Olá tupla usando armazenado em cache de metadados.

* **ID de Sequência**: ao emitir uma tupla, uma ID de sequência exclusiva poderá ser especificada. Esse valor identifica tupla Olá para processamento de reprodução (Ack e falhas). Por exemplo, Olá spout em Olá **profusão de exemplo** projeto usa a seguinte Olá ao emitir dados:

        this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), lastSeqId);

    Esse código emite uma tupla que contém um fluxo de padrão de toohello frase, com valor de ID de sequência de saudação contido em **lastSeqId**. Neste exemplo, **lastSeqId** é incrementado para todas as tuplas emitidas.

Conforme demonstrado no hello **profusão de exemplo** do projeto, se um componente é transacional pode ser definido em tempo de execução, com base na configuração.

## <a name="hybrid-topology-with-c-and-java"></a>Topologia híbrida com C# e Java

Você também pode usar ferramentas de Data Lake para topologias Visual Studio toocreate híbrida, em que alguns componentes são c# e outros são Java.

Para um exemplo de topologia híbrida, crie um projeto e selecione **Amostra Híbrida do Storm**. Esse tipo de exemplo demonstra Olá conceitos a seguir:

* **Spout Java** e **bolt C#**: definidos em **HybridTopology_javaSpout_csharpBolt**.

    * Uma versão transacional é definida em **HybridTopologyTx_javaSpout_csharpBolt**.

* **Spout C#** e **bolt Java**: definidos em **HybridTopology_csharpSpout_javaBolt**.

    * Uma versão transacional é definida em **HybridTopologyTx_csharpSpout_javaBolt**.

  > [!NOTE]
  > Esta versão também demonstra como toouse Clojure código de um arquivo de texto como um componente de Java.


topologia de saudação tooswitch que é usada quando o projeto de saudação é enviado, simplesmente mover Olá `[Active(true)]` instrução toohello topologia que toouse, antes de enviá-lo toohello cluster.

> [!NOTE]
> Todos os arquivos de Java Olá necessárias são fornecidos como parte deste projeto em Olá **JavaDependency** pasta.

Considere o seguinte hello quando você está criando e enviando uma topologia híbrida:

* Você deve usar **JavaComponentConstructor** toocreate uma instância da classe Java para um spout ou um raio de saudação.

* Você deve usar **microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer** tooJSON os objetos de dados de tooserialize ou de componentes de Java do Java.

* Ao enviar o servidor de toohello Olá topologia, você deve usar o hello **configurações adicionais** Olá de toospecify opção **caminhos de arquivo Java**. caminho de saudação especificado deve ser o diretório de saudação que contém arquivos JAR Olá que contêm classes Java.

### <a name="azure-event-hubs"></a>Hubs de eventos do Azure

A versão SCP.NET 0.9.4.203 introduz uma nova classe e o método especificamente para trabalhar com spout de Hub de eventos da saudação (um spout de Java que lê de Hubs de eventos). Quando você cria uma topologia que utiliza spout um Hub de eventos, use Olá métodos a seguir:

* **EventHubSpoutConfig** classe: cria um objeto que contém a configuração de saudação de componente de spout hello.

* **TopologyBuilder.SetEventHubSpout** método: adiciona a topologia de toohello Olá Hub de eventos spout componente.

> [!NOTE]
> Você ainda deve usar Olá **CustomizedInteropJSONSerializer** tooserialize dados produzidos por spout hello.

## <a id="configurationmanager"></a>Usar o ConfigurationManager

Não use **ConfigurationManager** tooretrieve configuração valores de parafuso e spout componentes. Isso pode causar uma exceção de ponteiro nulo. Em vez disso, configuração de saudação para seu projeto é passada para topologia de profusão de saudação como um par de chave e valor no contexto de topologia de saudação. Cada componente que se baseia em valores de configuração deve recuperá-los do contexto de saudação durante a inicialização.

Olá código a seguir demonstra como tooretrieve estes valores:

```csharp
public class MyComponent : ISCPBolt
{
    // toohold configuration information loaded from context
    Configuration configuration;
    ...
    public MyComponent(Context ctx, Dictionary<string, Object> parms)
    {
        // Save a copy of hello context for this component instance
        this.ctx = ctx;
        // If it exists, load hello configuration for hello component
        if(parms.ContainsKey(Constants.USER_CONFIG))
        {
            this.configuration = parms[Constants.USER_CONFIG] as System.Configuration.Configuration;
        }
        // Retrieve hello value of "Foo" from configuration
        var foo = this.configuration.AppSettings.Settings["Foo"].Value;
    }
    ...
}
```

Se você usar um `Get` método tooreturn uma instância do seu componente, você deve garantir que ele passa dois Olá `Context` e `Dictionary<string, Object>` construtor de toohello de parâmetros. Olá é um exemplo básico `Get` método corretamente passa esses valores:

```csharp
public static MyComponent Get(Context ctx, Dictionary<string, Object> parms)
{
    return new MyComponent(ctx, parms);
}
```

## <a name="how-tooupdate-scpnet"></a>Como tooupdate SCP.NET

As versões recentes do SCP.NET oferecem suporte à atualização de pacote por meio do NuGet. Quando uma nova atualização estiver disponível, você receberá uma notificação de atualização. seleção de toomanually para uma atualização, siga estas etapas:

1. Em **Solution Explorer**, clique com botão direito hello e selecione **gerenciar pacotes NuGet**.

2. No Gerenciador de pacotes de saudação, selecione **atualizações**. Se uma atualização estiver disponível, ela será listada. Clique em **atualização** para Olá pacote tooinstall-lo.

> [!IMPORTANT]
> Se seu projeto foi criado com uma versão anterior do SCP.NET que não usou o NuGet, você deve executar Olá versão mais recente de tooa de tooupdate de etapas a seguir:
>
> 1. Em **Solution Explorer**, clique com botão direito hello e selecione **gerenciar pacotes NuGet**.
> 2. Usando Olá **pesquisa** campo, pesquisar e, em seguida, adicionar, **Microsoft.SCP.Net.SDK** toohello projeto.

## <a name="troubleshoot-common-issues-with-topologies"></a>Solucionar problemas comuns com topologias

### <a name="null-pointer-exceptions"></a>Exceções de ponteiro nulo

Quando você estiver usando uma topologia c# com um cluster HDInsight baseados em Linux, parafuso e spout componentes que usam **ConfigurationManager** tooread definições de configuração em tempo de execução podem retornar exceções de ponteiro nulo.

configuração Olá para seu projeto é passada para a topologia de profusão de saudação como um par de chave e valor no contexto de topologia de saudação. Ele pode ser recuperado do objeto de dicionário de saudação que é passado tooyour componentes quando eles são iniciados.

Para obter mais informações, consulte Olá [ConfigurationManager](#configurationmanager) seção deste documento.

### <a name="systemtypeloadexception"></a>System.TypeLoadException

Quando você estiver usando uma topologia c# com um cluster HDInsight baseados em Linux, você pode encontrar hello erro a seguir:

    System.TypeLoadException: Failure has occurred while loading a type.

Esse erro ocorre quando você usa um binário que não é compatível com a versão de saudação do .NET que oferece suporte a Mono.

Para clusters HDInsight baseados em Linux, verifique se o projeto usa binários compilados para o .NET 4.5.

### <a name="test-a-topology-locally"></a>Testar uma topologia localmente

Embora seja fácil toodeploy um cluster de tooa de topologia, em alguns casos, talvez seja necessário tootest uma topologia localmente. Use Olá toorun as etapas a seguir e testar a topologia de exemplo hello neste tutorial localmente no seu ambiente de desenvolvimento.

> [!WARNING]
> Testes locais funcionam somente para topologias básicas exclusivamente em C#. Você não pode usar o teste local para topologias híbridas ou topologias que usam vários fluxos.

1. Em **Solution Explorer**, clique com botão direito hello e selecione **propriedades**. Nas propriedades do projeto hello, alterar Olá **tipo de saída** muito**aplicativo de Console**.

    ![Captura de tela de propriedades do projeto, com Tipo de saída realçado](./media/hdinsight-storm-develop-csharp-visual-studio-topology/outputtype.png)

   > [!NOTE]
   > Lembre-se de saudação toochange **tipo de saída** fazer muito**biblioteca de classes** antes de implantar o cluster de tooa topologia hello.

2. Em **Solution Explorer**, clique com botão direito hello e, em seguida, selecione **adicionar** > **Novo Item**. Selecione **classe**e digite **LocalTest.cs** como o nome da classe hello. Por fim, clique em **Adicionar**.

3. Abra **LocalTest.cs**e adicione o seguinte Olá **usando** instrução na parte superior da saudação:

    ```csharp
    using Microsoft.SCP;
    ```

4. De código a seguir de saudação de uso como conteúdo de saudação do hello **LocalTest** classe:

    ```csharp
    // Drives hello topology components
    public void RunTestCase()
    {
        // An empty dictionary for use when creating components
        Dictionary<string, Object> emptyDictionary = new Dictionary<string, object>();

        #region Test hello spout
        {
            Console.WriteLine("Starting spout");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext spoutCtx = LocalContext.Get();
            // Get a new instance of hello spout, using hello local context
            Spout sentences = Spout.Get(spoutCtx, emptyDictionary);

            // Emit 10 tuples
            for (int i = 0; i < 10; i++)
            {
                sentences.NextTuple(emptyDictionary);
            }
            // Use LocalContext toopersist hello data stream toofile
            spoutCtx.WriteMsgQueueToFile("sentences.txt");
            Console.WriteLine("Spout finished");
        }
        #endregion

        #region Test hello splitter bolt
        {
            Console.WriteLine("Starting splitter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext splitterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Splitter splitter = Splitter.Get(splitterCtx, emptyDictionary);

            // Set hello data stream toohello data created by hello spout
            splitterCtx.ReadFromFileToMsgQueue("sentences.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = splitterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                splitter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            splitterCtx.WriteMsgQueueToFile("splitter.txt");
            Console.WriteLine("Splitter bolt finished");
        }
        #endregion

        #region Test hello counter bolt
        {
            Console.WriteLine("Starting counter bolt");
            // LocalContext is a local-mode context that can be used tooinitialize
            // components in hello development environment.
            LocalContext counterCtx = LocalContext.Get();
            // Get a new instance of hello bolt
            Counter counter = Counter.Get(counterCtx, emptyDictionary);

            // Set hello data stream toohello data created by splitter bolt
            counterCtx.ReadFromFileToMsgQueue("splitter.txt");
            // Get a batch of tuples from hello stream
            List<SCPTuple> batch = counterCtx.RecvFromMsgQueue();
            // Process each tuple in hello batch
            foreach (SCPTuple tuple in batch)
            {
                counter.Execute(tuple);
            }
            // Use LocalContext toopersist hello data stream toofile
            counterCtx.WriteMsgQueueToFile("counter.txt");
            Console.WriteLine("Counter bolt finished");
        }
        #endregion
    }
    ```

    Tirar um tooread momento por meio de comentários de código hello. Esse código usa **LocalContext** toorun componentes de saudação no ambiente de desenvolvimento hello e persistir TDS Olá entre arquivos de componentes de tootext na unidade local hello.

1. Abra **Program.cs**e adicione Olá após toohello **principal** método:

    ```csharp
    Console.WriteLine("Starting tests");
    System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "WordCount-LocalTest");
    // Initialize hello runtime
    SCPRuntime.Initialize();

    //If we are not running under hello local context, throw an error
    if (Context.pluginType != SCPPluginType.SCP_NET_LOCAL)
    {
        throw new Exception(string.Format("unexpected pluginType: {0}", Context.pluginType));
    }
    // Create test instance
    LocalTest tests = new LocalTest();
    // Run tests
    tests.RunTestCase();
    Console.WriteLine("Tests finished");
    Console.ReadKey();
    ```

2. Salvar alterações de saudação e, em seguida, clique em **F5** ou selecione **depurar** > **iniciar depuração** toostart projeto de saudação. Uma janela do console deve aparecer e registrar o status como progresso de testes de saudação. Quando **testes terminado** for exibida, pressione qualquer janela de saudação tooclose chave.

3. Use **Windows Explorer** diretório de saudação toolocate que contém seu projeto. Por exemplo: **C:\Users\<seu_nome_de_usuário>\Documents\Visual Studio 2013\Projects\WordCount\WordCount**. Nesse diretório, abra **Bin** e clique em **Depurar**. Você deve ver os arquivos de texto de saudação que foram produzidos quando Olá testes executados: sentences.txt, counter.txt e splitter.txt. Abra cada arquivo de texto e inspecionar dados hello.

   > [!NOTE]
   > Os dados da cadeia de caracteres persistem como uma matriz de valores decimais nesses arquivos. Por exemplo, \[[97,103,111]] em Olá **splitter.txt** arquivo é palavra hello *e*.

> [!NOTE]
> Ser Olá-se de tooset **tipo de projeto** fazer muito**biblioteca de classes** antes de implantar tooa Storm no cluster HDInsight.

### <a name="log-information"></a>Registrando informações no log

É possível registrar em log com facilidade informações de seus componentes de topologia usando o `Context.Logger`. Por exemplo, o seguinte Olá cria uma entrada de log informativa:

```csharp
Context.Logger.Info("Component started");
```

Informações registradas podem ser exibidas de saudação **Log do serviço de Hadoop**, que se encontra no **Server Explorer**. Expanda a entrada de saudação para seu Storm no cluster HDInsight e, em seguida, expanda **Log do serviço de Hadoop**. Por fim, selecione Olá tooview de arquivo de log.

> [!NOTE]
> Olá logs são armazenados no hello conta de armazenamento do Azure que é usada pelo cluster. logs de saudação tooview no Visual Studio, você deve entrar no toohello assinatura do Azure que possui a conta de armazenamento hello.

### <a name="view-error-information"></a>Exibir informações de erro

tooview erros que ocorreram em uma topologia em execução, use Olá etapas a seguir:

1. De **Server Explorer**, Olá Storm no cluster HDInsight e selecione **topologias profusão de exibição**.

2. Para Olá **Spout** e **Bolts**, Olá **último erro** coluna contém informações sobre o último erro de saudação.

3. Selecione Olá **Spout Id** ou **raio Id** para o componente de saudação que tem um erro listado. Na página de detalhes de saudação que é exibido, adicional erro informações estão listadas no hello **erros** seção final Olá Olá página.

4. tooobtain obter mais informações, selecionadas um **porta** de saudação **executores** seção da página hello, toosee Olá Storm trabalho log Olá últimos minutos.

### <a name="errors-submitting-topologies"></a>Erros durante o envio de topologias

Se você encontrar erros ao enviar uma topologia tooHDInsight, você pode encontrar registros para componentes do servidor de saudação que manipulam o envio de topologia no seu cluster HDInsight. tooretrieve esses logs, use Olá comando a seguir em uma linha de comando:

    scp sshuser@clustername-ssh.azurehdinsight.net:/var/log/hdinsight-scpwebapi/hdinsight-scpwebapi.out .

Substituir __sshuser__ com hello SSH a conta de usuário para o cluster de saudação. Substituir __clustername__ com o nome de saudação do cluster do HDInsight hello. Para saber mais sobre como usar o `scp` e o `ssh` com o HDInsight, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Envios podem falhar por vários motivos:

* JDK não está instalado ou não está no caminho de saudação.
* Dependências de Java necessárias não são incluídas no envio de saudação.
* Dependências incompatíveis.
* Nomes de topologia duplicados.

Se hello `hdinsight-scpwebapi.out` log contém um `FileNotFoundException`, isso pode ser causado por Olá condições a seguir:

* Olá JDK não está no caminho de saudação no ambiente de desenvolvimento de saudação. Verifique se esse Olá JDK está instalado no ambiente de desenvolvimento hello e que `%JAVA_HOME%/bin` está no caminho de saudação.
* Uma dependência de Java está ausente. Verifique se que você está incluindo todos os arquivos JAR necessários como parte do envio de saudação.

## <a name="next-steps"></a>Próximas etapas

Para obter um exemplo de processamento de dados de Hubs de eventos, consulte [Processar eventos dos Hubs de Eventos do Azure com Storm no HDInsight](hdinsight-storm-develop-csharp-event-hub-topology.md).

Para obter um exemplo de uma topologia de C# que divide os dados de fluxo em vários fluxos, consulte [Exemplo de Storm C#](https://github.com/Blackmist/csharp-storm-example).

toodiscover obter mais informações sobre como criar c# topologias, consulte [GitHub](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/SCPNet-GettingStarted.md).

Para mais toowork maneiras com HDInsight e mais Storm em amostras de HDInsight, consulte Olá documentos a seguir:

**Microsoft SCP.NET**

* [Guia de programação do SCP](hdinsight-storm-scp-programming-guide.md)

**Apache Storm no HDInsight**

* [Implantar e monitorar topologias com o Apache Storm no HDInsight](hdinsight-storm-deploy-monitor-topology.md)
* [Topologias de exemplo para Storm no HDInsight](hdinsight-storm-example-topology.md)

**Apache Hadoop no HDInsight**

* [Usar o Hive com Hadoop no HDInsight](hdinsight-use-hive.md)
* [Usar o Pig com Hadoop no HDInsight](hdinsight-use-pig.md)
* [Usar o MapReduce com Hadoop no HDInsight](hdinsight-use-mapreduce.md)

**Apache HBase no HDInsight**

* [Introdução ao HBase no HDInsight](hdinsight-hbase-tutorial-get-started.md)
