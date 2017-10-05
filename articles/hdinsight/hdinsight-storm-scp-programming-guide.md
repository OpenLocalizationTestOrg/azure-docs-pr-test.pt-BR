---
title: "Guia de programação do SCP.NET | Microsoft Docs"
description: Saiba como usar SCP.NET para criar topologias do Storm baseadas em .NET para usar com o Storm no HDInsight.
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
ms.openlocfilehash: 3d76aebd2a1fd729c8e0639e6afcbde4c3fb752b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="scp-programming-guide"></a><span data-ttu-id="40c4a-103">Guia de programação do SCP</span><span class="sxs-lookup"><span data-stu-id="40c4a-103">SCP programming guide</span></span>
<span data-ttu-id="40c4a-104">SCP é uma plataforma para a criação de aplicativos de processamento de dados em tempo real, confiáveis, consistentes e de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="40c4a-104">SCP is a platform to build real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="40c4a-105">Ele é baseado no [Apache Storm](http://storm.incubator.apache.org/) , um sistema de processamento de fluxo projetado pelas comunidades de OSS.</span><span class="sxs-lookup"><span data-stu-id="40c4a-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by the OSS communities.</span></span> <span data-ttu-id="40c4a-106">O Storm foi projetado por Nathan Marz e tornou-se um software livre por meio do Twitter.</span><span class="sxs-lookup"><span data-stu-id="40c4a-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="40c4a-107">Ele aproveita o [Apache ZooKeeper](http://zookeeper.apache.org/), outro projeto da Apache, para habilitar uma coordenação distribuída e gerenciamento de estado altamente confiáveis.</span><span class="sxs-lookup"><span data-stu-id="40c4a-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project to enable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="40c4a-108">O projeto SCP não apenas compatibilizou o Storm no Windows como também incluiu extensões e personalização para o ecossistema do Windows.</span><span class="sxs-lookup"><span data-stu-id="40c4a-108">Not only the SCP project ported Storm on Windows but also the project added extensions and customization for the Windows ecosystem.</span></span> <span data-ttu-id="40c4a-109">As extensões incluem a experiência dos desenvolvedores e as bibliotecas do .NET; a personalização inclui a implantação baseada em Windows.</span><span class="sxs-lookup"><span data-stu-id="40c4a-109">The extensions include .NET developer experience, and libraries, the customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="40c4a-110">A extensão e a personalização são realizadas de forma que não precisamos bifurcar projetos de OSS e podemos utilizar ecossistemas derivados baseados no Storm.</span><span class="sxs-lookup"><span data-stu-id="40c4a-110">The extension and customization is done in such a way that we do not need to fork the OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="40c4a-111">Modelo de processamento</span><span class="sxs-lookup"><span data-stu-id="40c4a-111">Processing model</span></span>
<span data-ttu-id="40c4a-112">Os dados no SCP são modelados como fluxos contínuos de tuplas.</span><span class="sxs-lookup"><span data-stu-id="40c4a-112">The data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="40c4a-113">Geralmente, as tuplas são transmitidas para alguma fila primeiro, depois, são apanhadas e transformadas pela lógica de negócios hospedada em uma topologia do Storm; por fim, o resultado pode ser conectado como tuplas a outro sistema do SCP ou ser confirmado para armazenamentos, como o sistema de arquivos distribuído, ou bancos de dados, como o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="40c4a-113">Typically the tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally the output could be piped as tuples to another SCP system, or be committed to stores like distributed file system or databases like SQL Server.</span></span>

![Um diagrama de uma fila que fornece dados para processamento, alimentando um armazenamento de dados](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="40c4a-115">No Storm, a topologia de um aplicativo define um gráfico de computação.</span><span class="sxs-lookup"><span data-stu-id="40c4a-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="40c4a-116">Cada nó em uma topologia contém a lógica de processamento, e os links entre os nós indicam o fluxo de dados.</span><span class="sxs-lookup"><span data-stu-id="40c4a-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="40c4a-117">Os nós que injetam dados de entrada na topologia são chamados Spouts, que podem ser usados para sequenciar os dados.</span><span class="sxs-lookup"><span data-stu-id="40c4a-117">The nodes to inject input data into the topology are called Spouts, which can be used to sequence the data.</span></span> <span data-ttu-id="40c4a-118">Os dados de entrada podem residir em arquivos de log, banco de dados transacional e contadores de desempenho do sistema, entre outros. Os nós com fluxos de dados de entrada e de saída são chamados de Bolts, que realizam a filtragem, seleções e agregação reais dos dados.</span><span class="sxs-lookup"><span data-stu-id="40c4a-118">The input data could reside in file logs, transactional database, system performance counter etc. The nodes with both input and output data flows are called Bolts, which do the actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="40c4a-119">O SCP oferece suporte aos melhores esforços de processamento de dados, pelo menos uma vez e exatamente uma vez.</span><span class="sxs-lookup"><span data-stu-id="40c4a-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="40c4a-120">Em um aplicativo de processamento de streaming distribuído, vários erros podem ocorrer durante o processamento de dados, como interrupção da rede, falha do computador ou erro de código do usuário, entre outros. O processamento ao menos uma vez assegura que todos os dados serão processados pelo menos uma vez, reproduzindo automaticamente os mesmos dados quando o erro ocorre.</span><span class="sxs-lookup"><span data-stu-id="40c4a-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically the same data when error happens.</span></span> <span data-ttu-id="40c4a-121">O processamento de pelo menos uma vez é simples e confiável e bastante adequado a muitos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="40c4a-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="40c4a-122">No entanto, quando o aplicativo exige uma contagem exata, por exemplo, o processamento de pelo menos uma vez é insuficiente, já que os mesmos dados podem ser reproduzidos na topologia do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="40c4a-122">However, when the application requires exact counting, for example, at-least-once processing is insufficient since the same data could potentially be played in the application topology.</span></span> <span data-ttu-id="40c4a-123">Nesse caso, o processamento de exatamente uma vez é projetado para assegurar que o resultado esteja correto mesmo quando os dados possam ser reproduzidos e processados várias vezes.</span><span class="sxs-lookup"><span data-stu-id="40c4a-123">In that case, exactly-once processing is designed to make sure the result is correct even when the data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="40c4a-124">O SCP permite que os desenvolvedores do .NET desenvolvam aplicativos de processamento de dados em tempo real e aproveitem o Storm baseado em JVM (Máquina Virtual Java) ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="40c4a-124">SCP enables .NET developers to develop real time data process applications while leverage the Java Virtual Machine (JVM) based Storm under the cover.</span></span> <span data-ttu-id="40c4a-125">O .NET e o JVM se comunicam por meio do soquete local do TCP.</span><span class="sxs-lookup"><span data-stu-id="40c4a-125">The .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="40c4a-126">Basicamente, cada Spout/Bolt é um par de processos do .Net/Java, em que a lógica do usuário é executada no processo do .Net como um plugin.</span><span class="sxs-lookup"><span data-stu-id="40c4a-126">Basically each Spout/Bolt is a .Net/Java process pair, where the user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="40c4a-127">Para criar um aplicativo de processamento de dados baseado no SCP, várias etapas são necessárias:</span><span class="sxs-lookup"><span data-stu-id="40c4a-127">To build a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="40c4a-128">Projete e implemente os Spouts para extrair dados da fila.</span><span class="sxs-lookup"><span data-stu-id="40c4a-128">Design and implement the Spouts to pull in data from queue.</span></span>
* <span data-ttu-id="40c4a-129">Projete e implemente os Bolts para processar os dados de entrada e salvar os dados em armazenamentos externos, como um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="40c4a-129">Design and implement Bolts to process the input data, and save data to external stores such as Database.</span></span>
* <span data-ttu-id="40c4a-130">Projete a topologia e depois envie-a e execute-a.</span><span class="sxs-lookup"><span data-stu-id="40c4a-130">Design the topology, then submit and run the topology.</span></span> <span data-ttu-id="40c4a-131">A topologia define os vértices e os fluxos de dados entre os vértices.</span><span class="sxs-lookup"><span data-stu-id="40c4a-131">The topology defines vertexes and the data flows between the vertexes.</span></span> <span data-ttu-id="40c4a-132">O SCP assume a especificação da topologia e a implanta em um cluster do Storm, em que cada vértice é executado em um nó lógico.</span><span class="sxs-lookup"><span data-stu-id="40c4a-132">SCP will take the topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="40c4a-133">O failover e o dimensionamento serão realizados pelo agendador de tarefas do Storm.</span><span class="sxs-lookup"><span data-stu-id="40c4a-133">The failover and scaling will be taken care of by the Storm task scheduler.</span></span>

<span data-ttu-id="40c4a-134">Este documento usará exemplos simples para mostrar como criar aplicativos de processamento de dados com o SCP.</span><span class="sxs-lookup"><span data-stu-id="40c4a-134">This document will use some simple examples to walk through how to build data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="40c4a-135">Interface do plug-in do SCP</span><span class="sxs-lookup"><span data-stu-id="40c4a-135">SCP Plugin Interface</span></span>
<span data-ttu-id="40c4a-136">Plugins (ou aplicativos) do SCP são EXEs independentes que podem ser executados dentro do Visual Studio durante a fase de desenvolvimento e podem ser conectados ao pipeline do Storm após a implantação na produção.</span><span class="sxs-lookup"><span data-stu-id="40c4a-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during the development phase, and be plugged into the Storm pipeline after deployment in production.</span></span> <span data-ttu-id="40c4a-137">Escrever o plugin do SCP é igual escrever qualquer outro aplicativo do console do Windows padrão.</span><span class="sxs-lookup"><span data-stu-id="40c4a-137">Writing the SCP plugin is just the same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="40c4a-138">A plataforma do SCP.NET declara alguma interface para spout/bolt, e o código de plugin do usuário deve implementar essas interfaces.</span><span class="sxs-lookup"><span data-stu-id="40c4a-138">SCP.NET platform declares some interface for spout/bolt, and the user plugin code should implement these interfaces.</span></span> <span data-ttu-id="40c4a-139">O principal propósito desse design é que o usuário possa se concentrar em sua própria lógica de negócios, e deixar que as outras coisas sejam realizadas pela plataforma do SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="40c4a-139">The main purpose of this design is that the user can focus on their own business logics, and leaving other things to be handled by SCP.NET platform.</span></span>

<span data-ttu-id="40c4a-140">O código do plugin do usuário deve implementar uma das seguintes interfaces, dependendo de se a topologia é transacional ou não transacional e se o componente é um spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="40c4a-140">The user plugin code should implement one of the followings interfaces, depends on whether the topology is transactional or non-transactional, and whether the component is spout or bolt.</span></span>

* <span data-ttu-id="40c4a-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="40c4a-141">ISCPSpout</span></span>
* <span data-ttu-id="40c4a-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="40c4a-142">ISCPBolt</span></span>
* <span data-ttu-id="40c4a-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="40c4a-143">ISCPTxSpout</span></span>
* <span data-ttu-id="40c4a-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="40c4a-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="40c4a-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="40c4a-145">ISCPPlugin</span></span>
<span data-ttu-id="40c4a-146">ISCPPlugin é a interface comum para todos os tipos de plugins.</span><span class="sxs-lookup"><span data-stu-id="40c4a-146">ISCPPlugin is the common interface for all kinds of plugins.</span></span> <span data-ttu-id="40c4a-147">Atualmente, trata-se de uma interface fictícia.</span><span class="sxs-lookup"><span data-stu-id="40c4a-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="40c4a-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="40c4a-148">ISCPSpout</span></span>
<span data-ttu-id="40c4a-149">ISCPSpout é a interface para spout não transacional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-149">ISCPSpout is the interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="40c4a-150">Quando `NextTuple()` é chamado, o código do usuário C\# pode emitir uma ou mais tuplas.</span><span class="sxs-lookup"><span data-stu-id="40c4a-150">When `NextTuple()` is called, the C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="40c4a-151">Se não houver nada a ser emitido, esse método deverá retornar sem emitir nada.</span><span class="sxs-lookup"><span data-stu-id="40c4a-151">If there is nothing to emit, this method should return without emitting anything.</span></span> <span data-ttu-id="40c4a-152">Observe que `NextTuple()`, `Ack()` e `Fail()` são chamados em um loop coeso em um único thread no processo C\#.</span><span class="sxs-lookup"><span data-stu-id="40c4a-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="40c4a-153">Quando não há tuplas a serem emitidas, é recomendável fazer com que NextTuple entre em repouso por um curto período de tempo (como 10 milissegundos) para não sobrecarregar a CPU.</span><span class="sxs-lookup"><span data-stu-id="40c4a-153">When there are no tuples to emit, it is courteous to have NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="40c4a-154">`Ack()` e `Fail()` serão chamados somente quando o mecanismo de reconhecimento estiver habilitado no arquivo de especificações.</span><span class="sxs-lookup"><span data-stu-id="40c4a-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="40c4a-155">O `seqId` é usado para identificar a tupla reconhecida ou com falha.</span><span class="sxs-lookup"><span data-stu-id="40c4a-155">The `seqId` is used to identify the tuple which is acked or failed.</span></span> <span data-ttu-id="40c4a-156">Portanto, se o reconhecimento for habilitado em uma topologia não transacional, a seguinte função de emissão deverá ser usada no Spout:</span><span class="sxs-lookup"><span data-stu-id="40c4a-156">So if ack is enabled in non-transactional topology, the following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="40c4a-157">Se não há suporte para o ack na topologia não transacional, `Ack()` e `Fail()` podem ser deixadas como funções vazias.</span><span class="sxs-lookup"><span data-stu-id="40c4a-157">If ack is not supported in non-transactional topology, the `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="40c4a-158">Os parâmetros de entrada `parms` nessas funções são apenas um Dicionário vazio e são reservados para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="40c4a-158">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="40c4a-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="40c4a-159">ISCPBolt</span></span>
<span data-ttu-id="40c4a-160">ISCPBolt é a interface para bolt não transacional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-160">ISCPBolt is the interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="40c4a-161">Quando uma nova tupla está disponível, a função `Execute()` é chamada para processá-la.</span><span class="sxs-lookup"><span data-stu-id="40c4a-161">When new tuple is available, the `Execute()` function will be called to process it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="40c4a-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="40c4a-162">ISCPTxSpout</span></span>
<span data-ttu-id="40c4a-163">ISCPTxSpout é a interface para spout transacional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-163">ISCPTxSpout is the interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="40c4a-164">Assim como suas contrapartes não transacionais, `NextTx()`, `Ack()` e `Fail()` são chamados em um loop coeso em um único thread no processo C\#.</span><span class="sxs-lookup"><span data-stu-id="40c4a-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="40c4a-165">Quando não há dados a serem emitidos, é recomendável fazer com que `NextTx` entre em repouso por um curto período de tempo (como 10 milissegundos) para não sobrecarregar a CPU.</span><span class="sxs-lookup"><span data-stu-id="40c4a-165">When there are no data to emit, it is courteous to have `NextTx` sleep for a short amount of time (10 milliseconds) so as not to waste too much CPU.</span></span>

<span data-ttu-id="40c4a-166">O `NextTx()` é chamado para iniciar uma nova transação, e o parâmetro de saída `seqId` é usado para identificar a transação, que também é usado em `Ack()` e `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="40c4a-166">`NextTx()` is called to start a new transaction, the out parameter `seqId` is used to identify the transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="40c4a-167">No `NextTx()`, o usuário pode emitir dados para o lado do Java.</span><span class="sxs-lookup"><span data-stu-id="40c4a-167">In `NextTx()`, user can emit data to Java side.</span></span> <span data-ttu-id="40c4a-168">Os dados serão armazenados no ZooKeeper para oferecer suporte à reprodução.</span><span class="sxs-lookup"><span data-stu-id="40c4a-168">The data will be stored in ZooKeeper to support replay.</span></span> <span data-ttu-id="40c4a-169">Como a capacidade do ZooKeeper é bastante limitada, o usuário deve emitir somente metadados, e não dados em massa no spout transacional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-169">Because the capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="40c4a-170">O Storm reproduzirá uma transação automaticamente se falhar, por isso, `Fail()` não deve ser chamado em um caso normal.</span><span class="sxs-lookup"><span data-stu-id="40c4a-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="40c4a-171">Mas se o SCP puder verificar os metadados emitidos pelo spout transacional, ele poderá chamar `Fail()` quando os metadados forem inválidos.</span><span class="sxs-lookup"><span data-stu-id="40c4a-171">But if SCP can check the metadata emitted by transactional spout, it can call `Fail()` when the metadata is invalid.</span></span>

<span data-ttu-id="40c4a-172">Os parâmetros de entrada `parms` nessas funções são apenas um Dicionário vazio e são reservados para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="40c4a-172">The `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="40c4a-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="40c4a-173">ISCPBatchBolt</span></span>
<span data-ttu-id="40c4a-174">ISCPBatchBolt é a interface para bolt transacional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-174">ISCPBatchBolt is the interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="40c4a-175">`Execute()` é chamado quando há novas tuplas chegando no bolt.</span><span class="sxs-lookup"><span data-stu-id="40c4a-175">`Execute()` is called when there is new tuple arriving at the bolt.</span></span> <span data-ttu-id="40c4a-176">`FinishBatch()` é chamado quando essa transação é encerrada.</span><span class="sxs-lookup"><span data-stu-id="40c4a-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="40c4a-177">O parâmetro de entrada `parms` é reservado para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="40c4a-177">The `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="40c4a-178">Para topologia transacional, há um conceito importante: `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="40c4a-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="40c4a-179">Ele tem dois campos, `TxId` e `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="40c4a-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="40c4a-180">`TxId` é usado para identificar uma transação específica e, para uma determinada transação, poderá haver várias tentativas se a transação falhar e for reproduzida.</span><span class="sxs-lookup"><span data-stu-id="40c4a-180">`TxId` is used to identify a specific transaction, and for a given transaction, there may be multiple attempt if the transaction fails and is replayed.</span></span> <span data-ttu-id="40c4a-181">O SCP.NET terá um novo objeto ISCPBatchBolt diferente para processar cada `StormTxAttempt`, assim como o Storm faz no lado do Java.</span><span class="sxs-lookup"><span data-stu-id="40c4a-181">SCP.NET will new a different ISCPBatchBolt object to process each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="40c4a-182">O propósito desse design é oferecer suporte ao processamento de transações paralelas.</span><span class="sxs-lookup"><span data-stu-id="40c4a-182">The purpose of this design is to support parallel transactions processing.</span></span> <span data-ttu-id="40c4a-183">O usuário deve manter em mente que, se uma tentativa de transação for concluída, o objeto ISCPBatchBolt correspondente será destruído e o lixo será coletado.</span><span class="sxs-lookup"><span data-stu-id="40c4a-183">User should keep it in mind that if transaction attempt is finished, the corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="40c4a-184">Modelo de objeto</span><span class="sxs-lookup"><span data-stu-id="40c4a-184">Object Model</span></span>
<span data-ttu-id="40c4a-185">O SCP.NET também oferece um conjunto simples de objetos chave para que os desenvolvedores realizem a programação.</span><span class="sxs-lookup"><span data-stu-id="40c4a-185">SCP.NET also provides a simple set of key objects for developers to program with.</span></span> <span data-ttu-id="40c4a-186">Eles são **Context**, **StateStore** e **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="40c4a-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="40c4a-187">Eles serão discutidos no restante desta seção.</span><span class="sxs-lookup"><span data-stu-id="40c4a-187">They will be discussed in the rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="40c4a-188">Contexto</span><span class="sxs-lookup"><span data-stu-id="40c4a-188">Context</span></span>
<span data-ttu-id="40c4a-189">O Contexto oferece um ambiente de execução ao aplicativo.</span><span class="sxs-lookup"><span data-stu-id="40c4a-189">Context provides a running environment to the application.</span></span> <span data-ttu-id="40c4a-190">Cada instância ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) possui uma instância de Contexto correspondente.</span><span class="sxs-lookup"><span data-stu-id="40c4a-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="40c4a-191">A funcionalidade fornecido pelo Contexto pode ser dividida em duas partes: (1) a parte estática, que está disponível em todo o processo C\#, (2) a parte dinâmica, que está disponível apenas para a instância específica do Contexto.</span><span class="sxs-lookup"><span data-stu-id="40c4a-191">The functionality provided by Context can be divided into two parts: (1) the static part which is available in the whole C\# process, (2) the dynamic part which is only available for the specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="40c4a-192">Parte Estática</span><span class="sxs-lookup"><span data-stu-id="40c4a-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="40c4a-193">`Logger` é fornecido para fins de obtenção de log.</span><span class="sxs-lookup"><span data-stu-id="40c4a-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="40c4a-194">`pluginType` é usado para indicar o tipo de plug-in do processo do C\#.</span><span class="sxs-lookup"><span data-stu-id="40c4a-194">`pluginType` is used to indicate the plugin type of the C\# process.</span></span> <span data-ttu-id="40c4a-195">Se o processo do C\# for executado no modo de teste local (sem Java), o tipo de plug-in será `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="40c4a-195">If the C\# process is run in local test mode (without Java), the plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="40c4a-196">`Config` é fornecido para obter os parâmetros de configuração do lado do Java.</span><span class="sxs-lookup"><span data-stu-id="40c4a-196">`Config` is provided to get configuration parameters from Java side.</span></span> <span data-ttu-id="40c4a-197">Os parâmetros são transmitidos do lado do Java quando o plugin do C\# é inicializado.</span><span class="sxs-lookup"><span data-stu-id="40c4a-197">The parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="40c4a-198">O parâmetros `Config` são divididos em duas partes: `stormConf` e `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="40c4a-198">The `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="40c4a-199">`stormConf` são parâmetros definidos pelo Storm e `pluginConf` são os parâmetros definidos pelo SCP.</span><span class="sxs-lookup"><span data-stu-id="40c4a-199">`stormConf` is parameters defined by Storm and `pluginConf` is the parameters defined by SCP.</span></span> <span data-ttu-id="40c4a-200">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="40c4a-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="40c4a-201">`TopologyContext` é fornecido para obter o contexto da tipologia, é mais útil para componentes com vários paralelismos.</span><span class="sxs-lookup"><span data-stu-id="40c4a-201">`TopologyContext` is provided to get the topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="40c4a-202">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="40c4a-202">Here is an example:</span></span>

    //demo how to get TopologyContext info
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

### <a name="dynamic-part"></a><span data-ttu-id="40c4a-203">Parte Dinâmica</span><span class="sxs-lookup"><span data-stu-id="40c4a-203">Dynamic Part</span></span>
<span data-ttu-id="40c4a-204">As seguintes interfaces são pertinentes a uma determinada instância do Contexto.</span><span class="sxs-lookup"><span data-stu-id="40c4a-204">The following interfaces are pertinent to a certain Context instance.</span></span> <span data-ttu-id="40c4a-205">A instância do Contexto é criada pela plataforma do SCP.NET e transmitida ao código do usuário:</span><span class="sxs-lookup"><span data-stu-id="40c4a-205">The Context instance is created by SCP.NET platform and passed to the user code:</span></span>

    // Declare the Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple to default stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple to the specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="40c4a-206">Para o reconhecimento do suporte a spout não transacional, o seguinte método é fornecido:</span><span class="sxs-lookup"><span data-stu-id="40c4a-206">For non-transactional spout supporting ack, the following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="40c4a-207">Para ack de suporte a bolt não transacional, ele deve exibir explicitamente `Ack()` ou `Fail()` para a tupla recebida.</span><span class="sxs-lookup"><span data-stu-id="40c4a-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` the tuple it received.</span></span> <span data-ttu-id="40c4a-208">E, ao emitir uma nova tupla, também deve especificar as âncoras da nova tupla.</span><span class="sxs-lookup"><span data-stu-id="40c4a-208">And when emitting new tuple, it must also specify the anchors of the new tuple.</span></span> <span data-ttu-id="40c4a-209">Os seguintes métodos são fornecidos.</span><span class="sxs-lookup"><span data-stu-id="40c4a-209">The following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="40c4a-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="40c4a-210">StateStore</span></span>
<span data-ttu-id="40c4a-211">`StateStore` oferece serviços de metadados, geração de sequência monotônica e coordenação sem espera.</span><span class="sxs-lookup"><span data-stu-id="40c4a-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="40c4a-212">Abstrações de simultaneidade distribuídas de níveis mais altos podem ser baseadas no `StateStore`, incluindo bloqueios distribuídos, filas distribuídas, barreiras e serviços transacionais.</span><span class="sxs-lookup"><span data-stu-id="40c4a-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="40c4a-213">Os aplicativos do SCP podem usar o objeto `State` para persistir algumas informações no ZooKeeper, especialmente para a topologia transacional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-213">SCP applications may use the `State` object to persist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="40c4a-214">Ao fazer isso, se o spout transacional travar e for reiniciado, ele poderá recuperar as informações necessárias do ZooKeeper e reiniciar o pipeline.</span><span class="sxs-lookup"><span data-stu-id="40c4a-214">Doing so, if transactional spout crashes and restart, it can retrieve the necessary information from ZooKeeper and restart the pipeline.</span></span>

<span data-ttu-id="40c4a-215">O objeto `StateStore` tem principalmente os seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="40c4a-215">The `StateStore` object mainly has these methods:</span></span>

    /// <summary>
    /// Static method to retrieve a state store of the given path and connStr 
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
    /// Get all the States in the StateStore
    /// </summary>
    /// <returns>All the States</returns>
    public IEnumerable<State> States();

    /// <summary>
    /// Get state or registry object
    /// </summary>
    /// <param name="info">Registry Name(Registry only)</param>
    /// <typeparam name="T">Type, Registry or State</typeparam>
    /// <returns>Return Registry or State</returns>
    public T Get<T>(string info = null);

    /// <summary>
    /// List all the committed states
    /// </summary>
    /// <returns>Registries contain the Committed State </returns> 
    public IEnumerable<Registry> Commited();

    /// <summary>
    /// List all the Aborted State in the StateStore
    /// </summary>
    /// <returns>Registries contain the Aborted State</returns>
    public IEnumerable<Registry> Aborted();

    /// <summary>
    /// Retrieve an existing state object from this state store instance 
    /// </summary>
    /// <returns>State from StateStore</returns>
    /// <typeparam name="T">stateId, id of the State</typeparam>
    public State GetState(long stateId)

<span data-ttu-id="40c4a-216">O objeto `State` tem principalmente os seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="40c4a-216">The `State` object mainly has these methods:</span></span>

    /// <summary>
    /// Set the status of the state object to commit 
    /// </summary>
    public void Commit(bool simpleMode = true); 

    /// <summary>
    /// Set the status of the state object to abort 
    /// </summary>
    public void Abort();

    /// <summary>
    /// Put an attribute value under the give key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <param name="attribute">State Attribute</param> 
    public void PutAttribute<T>(string key, T attribute); 

    /// <summary>
    /// Get the attribute value associated with the given key 
    /// </summary>
    /// <param name="key">Key</param> 
    /// <returns>State Attribute</returns>               
    public T GetAttribute<T>(string key);                    

<span data-ttu-id="40c4a-217">Para o método `Commit()` , quando simpleMode é configurado como verdadeiro, ele simplesmente exclui o ZNode correspondente no ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="40c4a-217">For the `Commit()` method, when simpleMode is set to true, it will simply delete the corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="40c4a-218">Caso contrário, ele exclui o ZNode atual e adiciona um novo nó no COMMITTED\_PATH.</span><span class="sxs-lookup"><span data-stu-id="40c4a-218">Otherwise, it will delete the current ZNode, and adding a new node in the COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="40c4a-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="40c4a-219">SCPRuntime</span></span>
<span data-ttu-id="40c4a-220">SCPRuntime oferece os seguintes dois métodos.</span><span class="sxs-lookup"><span data-stu-id="40c4a-220">SCPRuntime provides the following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="40c4a-221">`Initialize()` é usado para inicializar o ambiente de tempo de execução do SCP.</span><span class="sxs-lookup"><span data-stu-id="40c4a-221">`Initialize()` is used to initialize the SCP runtime environment.</span></span> <span data-ttu-id="40c4a-222">Nesse método, o processo do C\# se conecta ao lado do Java e obtém os parâmetros de configuração e o contexto da topologia.</span><span class="sxs-lookup"><span data-stu-id="40c4a-222">In this method, the C\# process will connect to the Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="40c4a-223">`LaunchPlugin()` é usado para iniciar o loop de processamento de mensagem.</span><span class="sxs-lookup"><span data-stu-id="40c4a-223">`LaunchPlugin()` is used to kick off the message processing loop.</span></span> <span data-ttu-id="40c4a-224">Nesse loop, o plugin do C\# recebe mensagens do lado do Java (incluindo tuplas e sinais de controle) e, então, processa as mensagens, talvez chamando o método da interface fornecido pelo código do usuário.</span><span class="sxs-lookup"><span data-stu-id="40c4a-224">In this loop, the C\# plugin will receive messages form Java side (including tuples and control signals), and then process the messages, perhaps calling the interface method provide by the user code.</span></span> <span data-ttu-id="40c4a-225">O parâmetro de entrada para o método `LaunchPlugin()` é um delegado que pode retornar um objeto que implementa a interface ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.</span><span class="sxs-lookup"><span data-stu-id="40c4a-225">The input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="40c4a-226">Para ISCPBatchBolt, podemos obter `StormTxAttempt` de `parms` e usá-lo para julgar se trata-se de uma tentativa reproduzida.</span><span class="sxs-lookup"><span data-stu-id="40c4a-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it to judge whether it is a replayed attempt.</span></span> <span data-ttu-id="40c4a-227">Isso geralmente é feito no bolt de confirmação, e é demonstrado no exemplo `HelloWorldTx` .</span><span class="sxs-lookup"><span data-stu-id="40c4a-227">This is usually done at the commit bolt, and it is demonstrated in the `HelloWorldTx` example.</span></span>

<span data-ttu-id="40c4a-228">Em termos gerais, os plugins do SCP podem ser executados em dois modos aqui:</span><span class="sxs-lookup"><span data-stu-id="40c4a-228">Generally speaking, the SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="40c4a-229">Modo de Teste Local: nesse modo, os plug-ins do SCP (o código de usuário C\#) é executado dentro do Visual Studio durante a fase de desenvolvimento.</span><span class="sxs-lookup"><span data-stu-id="40c4a-229">Local Test Mode: In this mode, the SCP plugins (the C\# user code) run inside Visual Studio during the development phase.</span></span> <span data-ttu-id="40c4a-230">`LocalContext` pode ser usado nesse modo, oferecendo um método para serializar as tuplas emitidas para os arquivos locais e lê-los de volta na memória.</span><span class="sxs-lookup"><span data-stu-id="40c4a-230">`LocalContext` can be used in this mode, which provides method to serialize the emitted tuples to local files, and read them back to memory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="40c4a-231">Modo Regular: nesse modo, os plug-ins do SCP são lançados pelo processo de Java do Storm.</span><span class="sxs-lookup"><span data-stu-id="40c4a-231">Regular Mode: In this mode, the SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="40c4a-232">Aqui está um exemplo da inicialização do plugin do SCP:</span><span class="sxs-lookup"><span data-stu-id="40c4a-232">Here is an example of launching SCP plugin:</span></span>
   
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
            /* Setting the environment variable here can change the log file name */
            System.Environment.SetEnvironmentVariable("microsoft.scp.logPrefix", "HelloWorld");
   
            SCPRuntime.Initialize();
            SCPRuntime.LaunchPlugin(new newSCPPlugin(Generator.Get));
            }
        }
        }

## <a name="topology-specification-language"></a><span data-ttu-id="40c4a-233">Linguagem de Especificação da Topologia</span><span class="sxs-lookup"><span data-stu-id="40c4a-233">Topology Specification Language</span></span>
<span data-ttu-id="40c4a-234">A Especificação da Topologia do SCP é uma linguagem específica do domínio para descrever e configurar topologias do SCP.</span><span class="sxs-lookup"><span data-stu-id="40c4a-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="40c4a-235">Ela se baseia no Clojure DSL do Storm (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) e é estendida pelo SCP.</span><span class="sxs-lookup"><span data-stu-id="40c4a-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="40c4a-236">As especificações de topologia podem ser enviadas diretamente ao cluster do Storm para execução por meio do comando ***runspec***.</span><span class="sxs-lookup"><span data-stu-id="40c4a-236">Topology specifications can be submitted directly to storm cluster for execution via the ***runspec*** command.</span></span>

<span data-ttu-id="40c4a-237">O SCP.NET adicionou as seguintes funções para definir a Topologia Transacional:</span><span class="sxs-lookup"><span data-stu-id="40c4a-237">SCP.NET has add follow functions to define the Transactional Topology:</span></span>

| <span data-ttu-id="40c4a-238">**Novas funções**</span><span class="sxs-lookup"><span data-stu-id="40c4a-238">**New Functions**</span></span> | <span data-ttu-id="40c4a-239">**Parâmetros**</span><span class="sxs-lookup"><span data-stu-id="40c4a-239">**Parameters**</span></span> | <span data-ttu-id="40c4a-240">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="40c4a-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="40c4a-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="40c4a-241">**tx-topolopy**</span></span> |<span data-ttu-id="40c4a-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="40c4a-242">topology-name</span></span><br /><span data-ttu-id="40c4a-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="40c4a-243">spout-map</span></span><br /><span data-ttu-id="40c4a-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="40c4a-244">bolt-map</span></span> |<span data-ttu-id="40c4a-245">Defina uma topologia transacional com o nome da topologia, o &nbsp;mapa de definição de spouts e o mapa de definição de bolts</span><span class="sxs-lookup"><span data-stu-id="40c4a-245">Define a transactional topology with the topology name, &nbsp;spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="40c4a-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="40c4a-246">**scp-tx-spout**</span></span> |<span data-ttu-id="40c4a-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="40c4a-247">exec-name</span></span><br /><span data-ttu-id="40c4a-248">args</span><span class="sxs-lookup"><span data-stu-id="40c4a-248">args</span></span><br /><span data-ttu-id="40c4a-249">fields</span><span class="sxs-lookup"><span data-stu-id="40c4a-249">fields</span></span> |<span data-ttu-id="40c4a-250">Defina um spout transacional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-250">Define a transactional spout.</span></span> <span data-ttu-id="40c4a-251">Isso executará o aplicativo com ***exec-name*** usando ***args***.</span><span class="sxs-lookup"><span data-stu-id="40c4a-251">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="40c4a-252">O ***fields*** são os Campos de Saída do spout</span><span class="sxs-lookup"><span data-stu-id="40c4a-252">The ***fields*** is the Output Fields for spout</span></span> |
| <span data-ttu-id="40c4a-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="40c4a-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="40c4a-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="40c4a-254">exec-name</span></span><br /><span data-ttu-id="40c4a-255">args</span><span class="sxs-lookup"><span data-stu-id="40c4a-255">args</span></span><br /><span data-ttu-id="40c4a-256">fields</span><span class="sxs-lookup"><span data-stu-id="40c4a-256">fields</span></span> |<span data-ttu-id="40c4a-257">Defina um bolt em lote transacional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="40c4a-258">Executará um aplicativo com o ***exec-name*** usando ***args.***</span><span class="sxs-lookup"><span data-stu-id="40c4a-258">It will run the application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="40c4a-259">Os Fields são os Campos de Saída do bolt.</span><span class="sxs-lookup"><span data-stu-id="40c4a-259">The Fields is the Output Fields for bolt.</span></span> |
| <span data-ttu-id="40c4a-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="40c4a-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="40c4a-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="40c4a-261">exec-name</span></span><br /><span data-ttu-id="40c4a-262">args</span><span class="sxs-lookup"><span data-stu-id="40c4a-262">args</span></span><br /><span data-ttu-id="40c4a-263">fields</span><span class="sxs-lookup"><span data-stu-id="40c4a-263">fields</span></span> |<span data-ttu-id="40c4a-264">Defina um bolt confirmador transacional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="40c4a-265">Isso executará o aplicativo com ***exec-name*** usando ***args***.</span><span class="sxs-lookup"><span data-stu-id="40c4a-265">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="40c4a-266">O ***fields*** são os Campos de Saída do bolt</span><span class="sxs-lookup"><span data-stu-id="40c4a-266">The ***fields*** is the Output Fields for bolt</span></span> |
| <span data-ttu-id="40c4a-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="40c4a-267">**nontx-topolopy**</span></span> |<span data-ttu-id="40c4a-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="40c4a-268">topology-name</span></span><br /><span data-ttu-id="40c4a-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="40c4a-269">spout-map</span></span><br /><span data-ttu-id="40c4a-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="40c4a-270">bolt-map</span></span> |<span data-ttu-id="40c4a-271">Defina uma topologia não transacional com o nome da topologia, o &nbsp;mapa de definição de spouts e o mapa de definição de bolts</span><span class="sxs-lookup"><span data-stu-id="40c4a-271">Define a nontransactional topology with the topology name,&nbsp; spouts definition map and the bolts definition map</span></span> |
| <span data-ttu-id="40c4a-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="40c4a-272">**scp-spout**</span></span> |<span data-ttu-id="40c4a-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="40c4a-273">exec-name</span></span><br /><span data-ttu-id="40c4a-274">args</span><span class="sxs-lookup"><span data-stu-id="40c4a-274">args</span></span><br /><span data-ttu-id="40c4a-275">fields</span><span class="sxs-lookup"><span data-stu-id="40c4a-275">fields</span></span><br /><span data-ttu-id="40c4a-276">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="40c4a-276">parameters</span></span> |<span data-ttu-id="40c4a-277">Defina um spout não transacional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-277">Define a nontransactional spout.</span></span> <span data-ttu-id="40c4a-278">Isso executará o aplicativo com ***exec-name*** usando ***args***.</span><span class="sxs-lookup"><span data-stu-id="40c4a-278">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="40c4a-279">O ***fields*** são os Campos de Saída do spout</span><span class="sxs-lookup"><span data-stu-id="40c4a-279">The ***fields*** is the Output Fields for spout</span></span><br /><br /><span data-ttu-id="40c4a-280">O ***parameters*** são opcionais, usados para especificar alguns parâmetros como "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="40c4a-280">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="40c4a-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="40c4a-281">**scp-bolt**</span></span> |<span data-ttu-id="40c4a-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="40c4a-282">exec-name</span></span><br /><span data-ttu-id="40c4a-283">args</span><span class="sxs-lookup"><span data-stu-id="40c4a-283">args</span></span><br /><span data-ttu-id="40c4a-284">fields</span><span class="sxs-lookup"><span data-stu-id="40c4a-284">fields</span></span><br /><span data-ttu-id="40c4a-285">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="40c4a-285">parameters</span></span> |<span data-ttu-id="40c4a-286">Defina um bolt não transacional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="40c4a-287">Isso executará o aplicativo com ***exec-name*** usando ***args***.</span><span class="sxs-lookup"><span data-stu-id="40c4a-287">It will run the application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="40c4a-288">O ***fields*** são os Campos de Saída do bolt</span><span class="sxs-lookup"><span data-stu-id="40c4a-288">The ***fields*** is the Output Fields for bolt</span></span><br /><br /><span data-ttu-id="40c4a-289">O ***parameters*** são opcionais, usados para especificar alguns parâmetros como "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="40c4a-289">The ***parameters*** is optional, using it to specify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="40c4a-290">O SCP.NET possui as seguintes palavras-chave definidas:</span><span class="sxs-lookup"><span data-stu-id="40c4a-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="40c4a-291">**Palavras-chave**</span><span class="sxs-lookup"><span data-stu-id="40c4a-291">**Key Words**</span></span> | <span data-ttu-id="40c4a-292">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="40c4a-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="40c4a-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="40c4a-293">**:name**</span></span> |<span data-ttu-id="40c4a-294">Defina o nome da topologia</span><span class="sxs-lookup"><span data-stu-id="40c4a-294">Define the Topology Name</span></span> |
| <span data-ttu-id="40c4a-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="40c4a-295">**:topology**</span></span> |<span data-ttu-id="40c4a-296">Defina a Topologia usando as funções acima e as integradas.</span><span class="sxs-lookup"><span data-stu-id="40c4a-296">Define the Topology using the above functions and build in ones.</span></span> |
| <span data-ttu-id="40c4a-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="40c4a-297">**:p**</span></span> |<span data-ttu-id="40c4a-298">Defina a dica de paralelismo para cada spout ou bolt.</span><span class="sxs-lookup"><span data-stu-id="40c4a-298">Define the parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="40c4a-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="40c4a-299">**:config**</span></span> |<span data-ttu-id="40c4a-300">Defina o parâmetro de configuração ou atualize os existentes</span><span class="sxs-lookup"><span data-stu-id="40c4a-300">Define configure parameter or update the existing ones</span></span> |
| <span data-ttu-id="40c4a-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="40c4a-301">**:schema**</span></span> |<span data-ttu-id="40c4a-302">Defina o esquema do fluxo.</span><span class="sxs-lookup"><span data-stu-id="40c4a-302">Define the Schema of Stream.</span></span> |

<span data-ttu-id="40c4a-303">Todos os parâmetros utilizados com frequência:</span><span class="sxs-lookup"><span data-stu-id="40c4a-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="40c4a-304">**Parâmetro**</span><span class="sxs-lookup"><span data-stu-id="40c4a-304">**Parameter**</span></span> | <span data-ttu-id="40c4a-305">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="40c4a-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="40c4a-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="40c4a-306">**"plugin.name"**</span></span> |<span data-ttu-id="40c4a-307">nome do arquivo exe do plugin do C#</span><span class="sxs-lookup"><span data-stu-id="40c4a-307">exe file name of the C# plugin</span></span> |
| <span data-ttu-id="40c4a-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="40c4a-308">**"plugin.args"**</span></span> |<span data-ttu-id="40c4a-309">args do plugin</span><span class="sxs-lookup"><span data-stu-id="40c4a-309">plugin args</span></span> |
| <span data-ttu-id="40c4a-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="40c4a-310">**"output.schema"**</span></span> |<span data-ttu-id="40c4a-311">Esquema de saída</span><span class="sxs-lookup"><span data-stu-id="40c4a-311">Output schema</span></span> |
| <span data-ttu-id="40c4a-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="40c4a-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="40c4a-313">Se o reconhecimento está ativado para a topologia não transacional</span><span class="sxs-lookup"><span data-stu-id="40c4a-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="40c4a-314">O comando runspec será implantado juntamente com os bits, o uso é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="40c4a-314">The runspec command will be deployed together with the bits, the usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="40c4a-315">O parâmetro***resource-dir*** é opcional, você precisa especificá-lo quando quiser conectar um aplicativo do C\#, e esse diretório conterá o aplicativo, as dependências e as configurações.</span><span class="sxs-lookup"><span data-stu-id="40c4a-315">The ***resource-dir*** parameter is optional, you need to specify it when you want to plug a C\# application, and this directory will contain the application, the dependencies and configurations.</span></span>

<span data-ttu-id="40c4a-316">O parâmetro ***classpath*** também é opcional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-316">The ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="40c4a-317">Ele é usado para especificar o caminho de classe do Java se o arquivo de especificações contiver Spout ou Bolt do Java.</span><span class="sxs-lookup"><span data-stu-id="40c4a-317">It is used to specify the Java classpath if the spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="40c4a-318">Recursos diversos</span><span class="sxs-lookup"><span data-stu-id="40c4a-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="40c4a-319">Declaração de esquema de entrada e saída</span><span class="sxs-lookup"><span data-stu-id="40c4a-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="40c4a-320">O usuário pode emitir uma tupla no processo do C\#, a plataforma precisa serializar a tupla em bytes, transferi-la para o lado do Java e o Storm transferirá essa tupla aos destinos.</span><span class="sxs-lookup"><span data-stu-id="40c4a-320">The user can emit tuple in C\# process, the platform needs to serialize the tuple into byte[], transfer to Java side, and Storm will transfer this tuple to the targets.</span></span> <span data-ttu-id="40c4a-321">Enquanto isso, no componente downstream, o processo do C\# receberá a tupla de volta do lado do Java e a converterá para os tipos originais pela plataforma; todas essas operações são ocultadas pela plataforma.</span><span class="sxs-lookup"><span data-stu-id="40c4a-321">Meanwhile in downstream component, the C\# process will receive tuple back from java side, and convert it to the original types by platform, all these operations are hidden by the Platform.</span></span>

<span data-ttu-id="40c4a-322">Para oferecer suporte à serialização e desserialização, o código do usuário precisa declarar o esquema das entradas e saídas.</span><span class="sxs-lookup"><span data-stu-id="40c4a-322">To support the serialization and deserialization, user code needs to declare the schema of the inputs and outputs.</span></span>

<span data-ttu-id="40c4a-323">O esquema de fluxo de entrada/saída é definido como um dicionário, a chave é o StreamId e o valor são os Tipos das colunas.</span><span class="sxs-lookup"><span data-stu-id="40c4a-323">The input/output stream schema is defined as a dictionary, the key is the StreamId and the value is the Types of the columns.</span></span> <span data-ttu-id="40c4a-324">O componente pode ter múltiplos fluxos declarados.</span><span class="sxs-lookup"><span data-stu-id="40c4a-324">The component can have multi-streams declared.</span></span>

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


<span data-ttu-id="40c4a-325">No objeto de Contexto, temos a seguinte API adicionada:</span><span class="sxs-lookup"><span data-stu-id="40c4a-325">In Context object, we have the following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="40c4a-326">O código do usuário deve assegurar que as tuplas emitidas obedecem ao esquema definido para esse fluxo, ou o sistema lançará uma exceção de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="40c4a-326">User code must make sure the tuples emitted obey the schema defined for that stream, or the system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="40c4a-327">Suportes a múltiplos fluxos</span><span class="sxs-lookup"><span data-stu-id="40c4a-327">Multi-Stream Support</span></span>
<span data-ttu-id="40c4a-328">O SCP oferece suporte ao código do usuário para emitir ou receber de vários fluxos diferentes ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="40c4a-328">SCP supports user code to emit or receive from multiple distinct streams at the same time.</span></span> <span data-ttu-id="40c4a-329">O suporte é refletido no objeto de Contexto conforme o método de Emissão assume um parâmetro de ID de fluxo opcional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-329">The support reflects in the Context object as the Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="40c4a-330">Dois métodos no objeto de Contexto do SCP.NET foram adicionados.</span><span class="sxs-lookup"><span data-stu-id="40c4a-330">Two methods in the SCP.NET Context object have been added.</span></span> <span data-ttu-id="40c4a-331">Eles são usados para emitir uma Tupla ou Tuplas para especificar o StreamId.</span><span class="sxs-lookup"><span data-stu-id="40c4a-331">They are used to emit Tuple or Tuples to specify StreamId.</span></span> <span data-ttu-id="40c4a-332">O StreamId é uma cadeia de caracteres e precisa ser consistente no C\# e na Especificação de Definição da Topologia.</span><span class="sxs-lookup"><span data-stu-id="40c4a-332">The StreamId is a string and it needs to be consistent in both C\# and the Topology Definition Spec.</span></span>

        /* Emit tuple to the specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="40c4a-333">A emissão para um fluxo não existente causará exceções de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="40c4a-333">The emitting to a non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="40c4a-334">Agrupamento de Campos</span><span class="sxs-lookup"><span data-stu-id="40c4a-334">Fields Grouping</span></span>
<span data-ttu-id="40c4a-335">O Agrupamento de Campos interno no Storm não está funcionando adequadamente no SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="40c4a-335">The build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="40c4a-336">No lado do Proxy Java, todos os tipos de dados de campo são na verdade byte[] e o agrupamento de campos usa o código hash do objeto byte[] para realizar o agrupamento.</span><span class="sxs-lookup"><span data-stu-id="40c4a-336">On the Java Proxy side, all the fields data types are actually byte[], and the fields grouping uses the byte[] object hash code to perform the grouping.</span></span> <span data-ttu-id="40c4a-337">O código hash do objeto byte[] é o endereço desse objeto na memória.</span><span class="sxs-lookup"><span data-stu-id="40c4a-337">The byte[] object hash code is the address of this object in memory.</span></span> <span data-ttu-id="40c4a-338">Por isso, o agrupamento estará incorreto para dois objetos byte[] que compartilharem o mesmo conteúdo, mas não o mesmo endereço.</span><span class="sxs-lookup"><span data-stu-id="40c4a-338">So the grouping will be wrong for two byte[] objects that share the same content but not the same address.</span></span>

<span data-ttu-id="40c4a-339">O SCP.NET adiciona um método de agrupamento personalizado e utiliza o conteúdo de byte[] para realizar o agrupamento.</span><span class="sxs-lookup"><span data-stu-id="40c4a-339">SCP.NET adds a customized grouping method, and it will use the content of the byte[] to do the grouping.</span></span> <span data-ttu-id="40c4a-340">No arquivo **SPEC** , a sintaxe é parecida com:</span><span class="sxs-lookup"><span data-stu-id="40c4a-340">In **SPEC** file, the syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="40c4a-341">Aqui,</span><span class="sxs-lookup"><span data-stu-id="40c4a-341">Here,</span></span>

1. <span data-ttu-id="40c4a-342">“scp-field-group” significa “Agrupamento de campo personalizado implementado pelo SCP”.</span><span class="sxs-lookup"><span data-stu-id="40c4a-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="40c4a-343">“:tx” ou “:non-tx” significa que se trata de uma topologia transacional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="40c4a-344">Precisamos dessa informação, uma vez que o índice de início é diferente em topologias tx em relação às não tx.</span><span class="sxs-lookup"><span data-stu-id="40c4a-344">We need this information since the starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="40c4a-345">[0,1] significa o hashset dos IDs do campo, começando do 0.</span><span class="sxs-lookup"><span data-stu-id="40c4a-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="40c4a-346">Topologia híbrida</span><span class="sxs-lookup"><span data-stu-id="40c4a-346">Hybrid topology</span></span>
<span data-ttu-id="40c4a-347">O Storm nativo é escrito em Java.</span><span class="sxs-lookup"><span data-stu-id="40c4a-347">The native Storm is written in Java.</span></span> <span data-ttu-id="40c4a-348">E SCP.Net foi aprimorado para permitir que nossas personalizações sejam escritas em código C\# para lidar com a lógica de negócios.</span><span class="sxs-lookup"><span data-stu-id="40c4a-348">And SCP.Net has enhanced it to enable our customs to write C\# code to handle their business logic.</span></span> <span data-ttu-id="40c4a-349">Mas também damos suporte a topologias híbridas, que contêm não apenas spouts/bolts do C\#, mas também do Java.</span><span class="sxs-lookup"><span data-stu-id="40c4a-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="40c4a-350">Especificar o Spout/Bol do Java no arquivo de especificações</span><span class="sxs-lookup"><span data-stu-id="40c4a-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="40c4a-351">No arquivo de especificações, "scp-spout" e "scp-bolt" também podem ser usados para especificar Spouts e Bolts do Java, aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="40c4a-351">In spec file, "scp-spout" and "scp-bolt" can also be used to specify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="40c4a-352">Aqui `microsoft.scp.example.HybridTopology.Generator` é o nome da classe Spout do Java.</span><span class="sxs-lookup"><span data-stu-id="40c4a-352">Here `microsoft.scp.example.HybridTopology.Generator` is the name of the Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="40c4a-353">Especificar o caminho de classe do Java no comando runSpec</span><span class="sxs-lookup"><span data-stu-id="40c4a-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="40c4a-354">Se quiser enviar uma topologia contendo Spouts ou Bolts do Java, será necessário primeiro compilar os Spouts ou Bolts do Java e obter os arquivos Jar.</span><span class="sxs-lookup"><span data-stu-id="40c4a-354">If you want to submit topology containing Java Spouts or Bolts, you need to first compile the Java Spouts or Bolts and get the Jar files.</span></span> <span data-ttu-id="40c4a-355">Depois, você deve especificar o caminho de classe do Java que contém os arquivos Jar ao enviar a topologia.</span><span class="sxs-lookup"><span data-stu-id="40c4a-355">Then you should specify the java classpath that contains the Jar files when submitting topology.</span></span> <span data-ttu-id="40c4a-356">Veja um exemplo:</span><span class="sxs-lookup"><span data-stu-id="40c4a-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="40c4a-357">Aqui, **examples\\HybridTopology\\java\\target\\** é a pasta que contém o arquivo Jar do Spout/Bolt.</span><span class="sxs-lookup"><span data-stu-id="40c4a-357">Here **examples\\HybridTopology\\java\\target\\** is the folder containing the Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="40c4a-358">Serialização e desserialização entre Java e C\\</span><span class="sxs-lookup"><span data-stu-id="40c4a-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="40c4a-359">Nosso componente SCP inclui lado de Java e de C\#.</span><span class="sxs-lookup"><span data-stu-id="40c4a-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="40c4a-360">Para interagir com Spouts/Bolts Java nativos, a Serialização/Desserialização deve ser realizada entre o lado do Java e C\#, conforme ilustrado no gráfico a seguir.</span><span class="sxs-lookup"><span data-stu-id="40c4a-360">In order to interact with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in the following graph.</span></span>

![diagrama do componente java enviando ao componente SCP enviando ao componente Java](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="40c4a-362">**Serialização no lado do Java e desserialização no lado do C\#**</span><span class="sxs-lookup"><span data-stu-id="40c4a-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="40c4a-363">Primeiro, fornecemos a implementação padrão para serialização no lado do Java e a desserialização no lado do C\#.</span><span class="sxs-lookup"><span data-stu-id="40c4a-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="40c4a-364">O método de serialização no lado do Java pode ser especificado no arquivo SPEC:</span><span class="sxs-lookup"><span data-stu-id="40c4a-364">The serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="40c4a-365">O método de desserialização no lado do C\# deve ser especificado no código do usuário do C\#:</span><span class="sxs-lookup"><span data-stu-id="40c4a-365">The deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="40c4a-366">Essa implementação padrão deve lidar com a maioria dos casos se o tipo de dados não for muito complexo.</span><span class="sxs-lookup"><span data-stu-id="40c4a-366">This default implementation should handle most cases if the data type is not too complex.</span></span> <span data-ttu-id="40c4a-367">Para determinados casos, seja porque o tipo de dados do usuário é muito complexo ou porque o desempenho de nossa implementação padrão não atende o requisito do usuário, o usuário pode conectar sua própria implementação.</span><span class="sxs-lookup"><span data-stu-id="40c4a-367">For certain cases, either because the user data type is too complex, or because the performance of our default implementation does not meet the user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="40c4a-368">A interface de serialização no lado do Java é definida como:</span><span class="sxs-lookup"><span data-stu-id="40c4a-368">The serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="40c4a-369">A interface de desserialização no lado do C\# é definida como:</span><span class="sxs-lookup"><span data-stu-id="40c4a-369">The deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="40c4a-370">interface pública ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="40c4a-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="40c4a-371">**Serialização no lado do C\# e desserialização no lado do Java**</span><span class="sxs-lookup"><span data-stu-id="40c4a-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="40c4a-372">O método de serialização no lado do C\# deve ser especificado no código do usuário do C\#:</span><span class="sxs-lookup"><span data-stu-id="40c4a-372">The serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="40c4a-373">O método de Desserialização no lado do Java deve ser especificado no arquivo SPEC:</span><span class="sxs-lookup"><span data-stu-id="40c4a-373">The Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="40c4a-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="40c4a-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="40c4a-375">Aqui "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" é o nome do Desserializador e "microsoft.scp.example.HybridTopology.Person" é a classe de destino para a qual os dados são desserializados.</span><span class="sxs-lookup"><span data-stu-id="40c4a-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is the name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is the target class the data is deserialized to.</span></span>
   
   <span data-ttu-id="40c4a-376">O usuário também pode usar um plug-in para sua própria implementação de serializador de C\# e desserializador de Java.</span><span class="sxs-lookup"><span data-stu-id="40c4a-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="40c4a-377">Essa é a interface para o serializador do C\#:</span><span class="sxs-lookup"><span data-stu-id="40c4a-377">This is the interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="40c4a-378">Essa é a interface para o Deserializador Java:</span><span class="sxs-lookup"><span data-stu-id="40c4a-378">This is the interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="40c4a-379">Modo de host do SCP</span><span class="sxs-lookup"><span data-stu-id="40c4a-379">SCP Host Mode</span></span>
<span data-ttu-id="40c4a-380">Nesse modo, o usuário pode compilar seus códigos como DLL e usar o SCPHost.exe fornecido pelo SCP para enviar a topologia.</span><span class="sxs-lookup"><span data-stu-id="40c4a-380">In this mode, user can compile their codes to DLL, and use SCPHost.exe provided by SCP to submit topology.</span></span> <span data-ttu-id="40c4a-381">O arquivo de especificações tem a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="40c4a-381">The spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="40c4a-382">Aqui, `plugin.name` é especificado como `SCPHost.exe` fornecido pelo SDK do SCP.</span><span class="sxs-lookup"><span data-stu-id="40c4a-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="40c4a-383">O SCPHost.exe aceita exatamente três parâmetros:</span><span class="sxs-lookup"><span data-stu-id="40c4a-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="40c4a-384">O primeiro é o nome DLL, que é `"HelloWorld.dll"` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="40c4a-384">The first one is the DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="40c4a-385">O segundo é o nome da Classe, que é `"Scp.App.HelloWorld.Generator"` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="40c4a-385">The second one is the Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="40c4a-386">O terceiro é o nome de um método estático público, que pode ser invocado para obter uma instância do ISCPPlugin.</span><span class="sxs-lookup"><span data-stu-id="40c4a-386">The third one is the name of a public static method, which can be invoked to get an instance of ISCPPlugin.</span></span>

<span data-ttu-id="40c4a-387">No modo do host, o código do usuário é compilado como DLL e é invocado pela plataforma SCP.</span><span class="sxs-lookup"><span data-stu-id="40c4a-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="40c4a-388">Por isso, a plataforma do SCP pode ter controle total de toda a lógica de processamento.</span><span class="sxs-lookup"><span data-stu-id="40c4a-388">So SCP platform can get full control of the whole processing logic.</span></span> <span data-ttu-id="40c4a-389">Portanto, recomendamos que nossos clientes enviem a topologia no modo do host do SCP, uma vez que isso pode simplificar a experiência do desenvolvimento e oferecer mais flexibilidade e uma maior compatibilidade com versões anteriores também para versões posteriores.</span><span class="sxs-lookup"><span data-stu-id="40c4a-389">So we recommend our customers to submit topology in SCP host mode since it can simplify the development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="40c4a-390">Exemplos de programação do SCP</span><span class="sxs-lookup"><span data-stu-id="40c4a-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="40c4a-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="40c4a-391">HelloWorld</span></span>
<span data-ttu-id="40c4a-392">**HelloWorld** é um exemplo muito simples para mostrar um pouco do SCP.Net.</span><span class="sxs-lookup"><span data-stu-id="40c4a-392">**HelloWorld** is a very simple example to show a taste of SCP.Net.</span></span> <span data-ttu-id="40c4a-393">Ele usa uma topologia não transacional com um spout chamado **generator** e dois bolts chamados **splitter** e **counter**.</span><span class="sxs-lookup"><span data-stu-id="40c4a-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="40c4a-394">O spout **generator** gerará aleatoriamente algumas frases e as enviará para o **splitter**.</span><span class="sxs-lookup"><span data-stu-id="40c4a-394">The spout **generator** will randomly generate some sentences, and emit these sentences to **splitter**.</span></span> <span data-ttu-id="40c4a-395">O bolt **splitter** as divide em palavras e envia essas palavras ao bolt **counter**.</span><span class="sxs-lookup"><span data-stu-id="40c4a-395">The bolt **splitter** will split the sentences to words and emit these words to **counter** bolt.</span></span> <span data-ttu-id="40c4a-396">O bolt “counter” usa um dicionário para registrar o número de ocorrências de cada palavra.</span><span class="sxs-lookup"><span data-stu-id="40c4a-396">The bolt "counter" uses a dictionary to record the occurrence number of each word.</span></span>

<span data-ttu-id="40c4a-397">Há dois arquivos de especificações, **HelloWorld.spec** e **HelloWorld\_EnableAck.spec** para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="40c4a-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="40c4a-398">No código do C\#, ele pode descobrir se o reconhecimento está habilitado obtendo o pluginConf no lado do Java.</span><span class="sxs-lookup"><span data-stu-id="40c4a-398">In the C\# code, it can find out whether ack is enabled by getting the pluginConf from Java side.</span></span>

    /* demo how to get pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="40c4a-399">No spout, se o reconhecimento estiver habilitado, um dicionário é usado para armazenar em cache as tuplas que não foram reconhecidas.</span><span class="sxs-lookup"><span data-stu-id="40c4a-399">In the spout, if ack is enabled, a dictionary is used to cache the tuples that have not been acked.</span></span> <span data-ttu-id="40c4a-400">Se Fail() for chamado, a tupla com falha é reproduzida:</span><span class="sxs-lookup"><span data-stu-id="40c4a-400">If Fail() is called, the failed tuple will be replayed:</span></span>

    public void Fail(long seqId, Dictionary<string, Object> parms)
    {
        Context.Logger.Info("Fail, seqId: {0}", seqId);
        if (cachedTuples.ContainsKey(seqId))
        {
            /* get the cached tuple */
            string sentence = cachedTuples[seqId];

            /* replay the failed tuple */
            Context.Logger.Info("Re-Emit: {0}, seqId: {1}", sentence, seqId);
            this.ctx.Emit(Constants.DEFAULT_STREAM_ID, new Values(sentence), seqId);
        }
        else
        {
            Context.Logger.Warn("Fail(), can't find cached tuple for seqId {0}!", seqId);
        }
    }

### <a name="helloworldtx"></a><span data-ttu-id="40c4a-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="40c4a-401">HelloWorldTx</span></span>
<span data-ttu-id="40c4a-402">O exemplo **HelloWorldTx** demonstra como implementar a topologia transacional.</span><span class="sxs-lookup"><span data-stu-id="40c4a-402">The **HelloWorldTx** example demonstrates how to implement transactional topology.</span></span> <span data-ttu-id="40c4a-403">Ele tem um spout chamado **generator**, um bolt em lote chamado **partial-count** e um bolt de confirmação chamado **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="40c4a-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="40c4a-404">Também há três arquivos txt pré-criados: **DataSource0.txt**, **DataSource1.txt** e **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="40c4a-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="40c4a-405">Em cada transação, o spout **generator** escolhe aleatoriamente dois arquivos dos três arquivos pré-criados e emite os dois nomes dos arquivos ao bolt **partial-count**.</span><span class="sxs-lookup"><span data-stu-id="40c4a-405">In each transaction, the spout **generator** will randomly choose two files from the pre-created three files, and emit the two file names to the **partial-count** bolt.</span></span> <span data-ttu-id="40c4a-406">O bolt **partial-count** primeiro obtém o nome do arquivo da tupla recebida, depois, abre o arquivo e conta o número de palavras nesse arquivo e, por fim, emite o número de palavras ao bolt **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="40c4a-406">The bolt **partial-count** will first get the file name from the received tuple, then open the file and count the number of words in this file, and finally emit the word number to the **count-sum** bolt.</span></span> <span data-ttu-id="40c4a-407">O bolt **count-sum** resume a contagem total.</span><span class="sxs-lookup"><span data-stu-id="40c4a-407">The **count-sum** bolt will summarize the total count.</span></span>

<span data-ttu-id="40c4a-408">Para alcançar a semântica **exatamente uma vez**, o bolt de confirmação **count-sum** precisa julgar que se trata de uma transação reproduzida.</span><span class="sxs-lookup"><span data-stu-id="40c4a-408">To achieve **exactly once** semantics, the commit bolt **count-sum** need to judge whether it is a replayed transaction.</span></span> <span data-ttu-id="40c4a-409">Neste exemplo, ele possui uma variável do membro estático:</span><span class="sxs-lookup"><span data-stu-id="40c4a-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="40c4a-410">Quando uma instância ISCPBatchBolt é criada, ela obtém `txAttempt` dos parâmetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="40c4a-410">When an ISCPBatchBolt instance is created, it will get the `txAttempt` from input parameters:</span></span>

    public static CountSum Get(Context ctx, Dictionary<string, Object> parms)
    {
        /* for transactional topology, we can get txAttempt from the input parms */
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

<span data-ttu-id="40c4a-411">Quando `FinishBatch()` é chamado, o `lastCommittedTxId` será atualizado se não for uma transação reproduzida.</span><span class="sxs-lookup"><span data-stu-id="40c4a-411">When `FinishBatch()` is called, the `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

    public void FinishBatch(Dictionary<string, Object> parms)
    {
        /* judge whether it is a replayed transaction? */
        bool replay = (this.txAttempt.TxId <= lastCommittedTxId);

        if (!replay)
        {
            /* If it is not replayed, update the toalCount and lastCommittedTxId vaule */
            totalCount = totalCount + this.count;
            lastCommittedTxId = this.txAttempt.TxId;
        }
        … …
    }


### <a name="hybridtopology"></a><span data-ttu-id="40c4a-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="40c4a-412">HybridTopology</span></span>
<span data-ttu-id="40c4a-413">Essa topologia contém um Spout do Java e um Bolt do C\#.</span><span class="sxs-lookup"><span data-stu-id="40c4a-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="40c4a-414">Ela usa a implementação de serialização e desserialização padrão fornecida pela plataforma do SCP.</span><span class="sxs-lookup"><span data-stu-id="40c4a-414">It uses the default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="40c4a-415">Consulte **HybridTopology.spec** na pasta **examples\\HybridTopology** para obter os detalhes do arquivo de especificações e **SubmitTopology.bat** para saber como especificar o caminho de classe de Java.</span><span class="sxs-lookup"><span data-stu-id="40c4a-415">Please ref the **HybridTopology.spec** in **examples\\HybridTopology** folder for the spec file details, and **SubmitTopology.bat** for how to specify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="40c4a-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="40c4a-416">SCPHostDemo</span></span>
<span data-ttu-id="40c4a-417">Este exemplo é igual ao HelloWorld em essência.</span><span class="sxs-lookup"><span data-stu-id="40c4a-417">This example is the same as HelloWorld in essence.</span></span> <span data-ttu-id="40c4a-418">A única diferença é que o código do usuário é compilado como DLL e a topologia é enviada usando SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="40c4a-418">The only difference is that the user code is compiled as DLL and the topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="40c4a-419">Consulte a seção “Modo de host do SCP” para obter explicações mais detalhadas.</span><span class="sxs-lookup"><span data-stu-id="40c4a-419">Please ref the section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="40c4a-420">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="40c4a-420">Next Steps</span></span>
<span data-ttu-id="40c4a-421">Para obter exemplos de topologias Storm criadas usando o SCP, consulte o seguinte:</span><span class="sxs-lookup"><span data-stu-id="40c4a-421">For examples of Storm topologies created using SCP, see the following:</span></span>

* [<span data-ttu-id="40c4a-422">Desenvolver topologias C# para o Apache Storm no HDInsight usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="40c4a-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="40c4a-423">Processar eventos dos Hubs de Evento do Azure com o Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="40c4a-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="40c4a-424">Criar vários fluxos de dados em uma topologia Storm em C#</span><span class="sxs-lookup"><span data-stu-id="40c4a-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="40c4a-425">Usar o Power BI para visualizar dados da topologia Storm</span><span class="sxs-lookup"><span data-stu-id="40c4a-425">Use Power Bi to visualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="40c4a-426">Processar dados do sensor do veículo a partir de Hubs de Evento usando o Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="40c4a-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="40c4a-427">ETL (Extração, Transformação e Carregamento) de Hubs de Eventos do Azure para HBase</span><span class="sxs-lookup"><span data-stu-id="40c4a-427">Extract, Transform, and Load (ETL) from Azure Event Hubs to HBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="40c4a-428">Correlacionar eventos usando Storm e HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="40c4a-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

