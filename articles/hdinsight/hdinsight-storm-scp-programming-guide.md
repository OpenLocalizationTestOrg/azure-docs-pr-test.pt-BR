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
# <a name="scp-programming-guide"></a><span data-ttu-id="f23cf-103">Guia de programação do SCP</span><span class="sxs-lookup"><span data-stu-id="f23cf-103">SCP programming guide</span></span>
<span data-ttu-id="f23cf-104">SCP é uma plataforma toobuild em tempo real, o aplicativo de processamento de dados confiáveis, consistentes e de alto desempenho.</span><span class="sxs-lookup"><span data-stu-id="f23cf-104">SCP is a platform toobuild real time, reliable, consistent and high performance data processing application.</span></span> <span data-ttu-id="f23cf-105">Ele é criado na parte superior do [Apache Storm](http://storm.incubator.apache.org/) – um sistema criado pela comunidades Olá OSS de processamento de fluxo.</span><span class="sxs-lookup"><span data-stu-id="f23cf-105">It is built on top of [Apache Storm](http://storm.incubator.apache.org/) -- a stream processing system designed by hello OSS communities.</span></span> <span data-ttu-id="f23cf-106">O Storm foi projetado por Nathan Marz e tornou-se um software livre por meio do Twitter.</span><span class="sxs-lookup"><span data-stu-id="f23cf-106">Storm is designed by Nathan Marz and open sourced by Twitter.</span></span> <span data-ttu-id="f23cf-107">Ele utiliza um [ZooKeeper Apache](http://zookeeper.apache.org/), Apache outro projeto tooenable coordenação de distribuído altamente confiável e gerenciamento de estado.</span><span class="sxs-lookup"><span data-stu-id="f23cf-107">It leverages [Apache ZooKeeper](http://zookeeper.apache.org/), another Apache project tooenable highly reliable distributed coordination and state management.</span></span> 

<span data-ttu-id="f23cf-108">Não só projeto Olá SCP movido Storm no Windows, mas também o projeto de saudação adicionado extensões e personalização do ecossistema do Windows hello.</span><span class="sxs-lookup"><span data-stu-id="f23cf-108">Not only hello SCP project ported Storm on Windows but also hello project added extensions and customization for hello Windows ecosystem.</span></span> <span data-ttu-id="f23cf-109">extensões de saudação incluem a experiência do desenvolvedor do .NET e bibliotecas, personalização de saudação inclui implantação baseada em Windows.</span><span class="sxs-lookup"><span data-stu-id="f23cf-109">hello extensions include .NET developer experience, and libraries, hello customization includes Windows-based deployment.</span></span> 

<span data-ttu-id="f23cf-110">personalização e extensão Olá é feita de forma que não precisamos projetos de OSS Olá toofork e utilizamos foi derivadas ecossistemas criadas sobre profusão de.</span><span class="sxs-lookup"><span data-stu-id="f23cf-110">hello extension and customization is done in such a way that we do not need toofork hello OSS projects and we could leverage derived ecosystems built on top of Storm.</span></span>

## <a name="processing-model"></a><span data-ttu-id="f23cf-111">Modelo de processamento</span><span class="sxs-lookup"><span data-stu-id="f23cf-111">Processing model</span></span>
<span data-ttu-id="f23cf-112">dados de saudação nos SCP são modelados como fluxos contínuos de tuplas.</span><span class="sxs-lookup"><span data-stu-id="f23cf-112">hello data in SCP is modeled as continuous streams of tuples.</span></span> <span data-ttu-id="f23cf-113">Normalmente Olá tuplas fluem para alguns fila pela primeira vez, em seguida, obtido e transformados por hospedado dentro de uma topologia de profusão de lógica de negócios, por fim Olá saída pode ser conectada como tuplas tooanother SCP sistema ou ser confirmada toostores como sistema de arquivos distribuídos ou bancos de dados como o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f23cf-113">Typically hello tuples flow into some queue first, then picked up, and transformed by business logic hosted inside a Storm topology, finally hello output could be piped as tuples tooanother SCP system, or be committed toostores like distributed file system or databases like SQL Server.</span></span>

![Um diagrama de uma fila alimentar tooprocessing de dados, que alimenta um repositório de dados](media/hdinsight-storm-scp-programming-guide/queue-feeding-data-to-processing-to-data-store.png)

<span data-ttu-id="f23cf-115">No Storm, a topologia de um aplicativo define um gráfico de computação.</span><span class="sxs-lookup"><span data-stu-id="f23cf-115">In Storm, an application topology defines a graph of computation.</span></span> <span data-ttu-id="f23cf-116">Cada nó em uma topologia contém a lógica de processamento, e os links entre os nós indicam o fluxo de dados.</span><span class="sxs-lookup"><span data-stu-id="f23cf-116">Each node in a topology contains processing logic, and links between nodes indicate data flow.</span></span> <span data-ttu-id="f23cf-117">Olá nós tooinject dados de entrada em topologia Olá são chamados de Spouts, que podem ser usado toosequence Olá dados.</span><span class="sxs-lookup"><span data-stu-id="f23cf-117">hello nodes tooinject input data into hello topology are called Spouts, which can be used toosequence hello data.</span></span> <span data-ttu-id="f23cf-118">Olá dados de entrada podem residir em arquivos de log, o banco de dados transacional, o contador de desempenho do sistema nós de saudação do etc. com os fluxos de dados de entrada e saída são chamados parafusos, que Olá a filtragem de dados reais e as seleções e agregação.</span><span class="sxs-lookup"><span data-stu-id="f23cf-118">hello input data could reside in file logs, transactional database, system performance counter etc. hello nodes with both input and output data flows are called Bolts, which do hello actual data filtering and selections and aggregation.</span></span>

<span data-ttu-id="f23cf-119">O SCP oferece suporte aos melhores esforços de processamento de dados, pelo menos uma vez e exatamente uma vez.</span><span class="sxs-lookup"><span data-stu-id="f23cf-119">SCP supports best efforts, at-least-once and exactly-once data processing.</span></span> <span data-ttu-id="f23cf-120">Em um aplicativo de processamento de streaming distribuído, vários erros podem ocorrer durante o processamento de dados, como interrupção da rede, falha do computador ou erro de código do usuário, entre outros. Processamento de at-least-once garante que todos os dados serão processados pelo menos uma vez por repetir automaticamente Olá dados mesmo quando o erro ocorre.</span><span class="sxs-lookup"><span data-stu-id="f23cf-120">In a distributed streaming processing application, various errors may happen during data processing, such as network outage, machine failure, or user code error etc. At-least-once processing ensures all data will be processed at least once by replaying automatically hello same data when error happens.</span></span> <span data-ttu-id="f23cf-121">O processamento de pelo menos uma vez é simples e confiável e bastante adequado a muitos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="f23cf-121">At-least-once processing is simple and reliable and suits well in many applications.</span></span> <span data-ttu-id="f23cf-122">No entanto, quando o aplicativo hello requer que a contagem exata, por exemplo, at-least-once processamento é insuficiente porque hello mesmos dados podem potencialmente ser reproduzidos na topologia de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="f23cf-122">However, when hello application requires exact counting, for example, at-least-once processing is insufficient since hello same data could potentially be played in hello application topology.</span></span> <span data-ttu-id="f23cf-123">Nesse caso, exatamente-depois que o processamento é projetado resultados de saudação se toomake está correto mesmo quando dados saudação podem ser repetidos e processados várias vezes.</span><span class="sxs-lookup"><span data-stu-id="f23cf-123">In that case, exactly-once processing is designed toomake sure hello result is correct even when hello data may be replayed and processed multiple times.</span></span>

<span data-ttu-id="f23cf-124">SCP permite que aplicativos de processo de dados .NET desenvolvedores toodevelop em tempo real ao aproveitar Olá Máquina Virtual Java (JVM) baseado em Storm sob abrangem hello.</span><span class="sxs-lookup"><span data-stu-id="f23cf-124">SCP enables .NET developers toodevelop real time data process applications while leverage hello Java Virtual Machine (JVM) based Storm under hello cover.</span></span> <span data-ttu-id="f23cf-125">Olá .NET e JVM se comunicam por meio de soquete local TCP.</span><span class="sxs-lookup"><span data-stu-id="f23cf-125">hello .NET and JVM communicate via TCP local socket.</span></span> <span data-ttu-id="f23cf-126">Basicamente cada Spout/raio é um par de processo do .net/Java, onde a lógica de saudação do usuário é executado no processo de .net como um plug-in.</span><span class="sxs-lookup"><span data-stu-id="f23cf-126">Basically each Spout/Bolt is a .Net/Java process pair, where hello user logic runs in .Net process as a plugin.</span></span>

<span data-ttu-id="f23cf-127">toobuild um aplicativo sobre SCP de processamento de dados, várias etapas são necessárias:</span><span class="sxs-lookup"><span data-stu-id="f23cf-127">toobuild a data processing application on top of SCP, several steps are needed:</span></span>

* <span data-ttu-id="f23cf-128">Projetar e implementar Olá Spouts toopull nos dados da fila.</span><span class="sxs-lookup"><span data-stu-id="f23cf-128">Design and implement hello Spouts toopull in data from queue.</span></span>
* <span data-ttu-id="f23cf-129">Projetar e implementar dados de entrada parafusos tooprocess hello e salvar dados tooexternal repositórios como banco de dados.</span><span class="sxs-lookup"><span data-stu-id="f23cf-129">Design and implement Bolts tooprocess hello input data, and save data tooexternal stores such as Database.</span></span>
* <span data-ttu-id="f23cf-130">Design de topologia Olá, enviar e executar topologia hello.</span><span class="sxs-lookup"><span data-stu-id="f23cf-130">Design hello topology, then submit and run hello topology.</span></span> <span data-ttu-id="f23cf-131">Olá topologia define vértices e dados saudação fluxos entre os vértices de saudação.</span><span class="sxs-lookup"><span data-stu-id="f23cf-131">hello topology defines vertexes and hello data flows between hello vertexes.</span></span> <span data-ttu-id="f23cf-132">SCP vai levar a especificação de topologia hello e implantá-lo em um cluster Storm, onde cada vértice é executado em um nó de lógico.</span><span class="sxs-lookup"><span data-stu-id="f23cf-132">SCP will take hello topology specification and deploy it on a Storm cluster, where each vertex runs on one logical node.</span></span> <span data-ttu-id="f23cf-133">Olá failover e dimensionamento serão ser manipulados pelo Agendador de tarefas Storm hello.</span><span class="sxs-lookup"><span data-stu-id="f23cf-133">hello failover and scaling will be taken care of by hello Storm task scheduler.</span></span>

<span data-ttu-id="f23cf-134">Este documento usará toowalk alguns exemplos simples como aplicativo de processamento de dados toobuild com SCP.</span><span class="sxs-lookup"><span data-stu-id="f23cf-134">This document will use some simple examples toowalk through how toobuild data processing application with SCP.</span></span>

## <a name="scp-plugin-interface"></a><span data-ttu-id="f23cf-135">Interface do plug-in do SCP</span><span class="sxs-lookup"><span data-stu-id="f23cf-135">SCP Plugin Interface</span></span>
<span data-ttu-id="f23cf-136">Plug-ins de SCP (ou aplicativos) são EXEs autônomo que ambos podem executar dentro do Visual Studio durante a fase de desenvolvimento hello e esteja conectados ao pipeline de profusão de saudação após a implantação em produção.</span><span class="sxs-lookup"><span data-stu-id="f23cf-136">SCP plugins (or applications) are standalone EXEs that can both run inside Visual Studio during hello development phase, and be plugged into hello Storm pipeline after deployment in production.</span></span> <span data-ttu-id="f23cf-137">Gravando Olá SCP plug-in é apenas Olá mesmo que escrever quaisquer outros aplicativos do console de Windows padrão.</span><span class="sxs-lookup"><span data-stu-id="f23cf-137">Writing hello SCP plugin is just hello same as writing any other standard Windows console applications.</span></span> <span data-ttu-id="f23cf-138">Plataforma SCP.NET declara alguma interface para spout/brilhante e código de plug-in do usuário Olá deve implementar essas interfaces.</span><span class="sxs-lookup"><span data-stu-id="f23cf-138">SCP.NET platform declares some interface for spout/bolt, and hello user plugin code should implement these interfaces.</span></span> <span data-ttu-id="f23cf-139">Olá principal objetivo desse design é que o usuário Olá pode se concentrar em suas próprias lógicas de negócios e deixando outros toobe itens tratado pela plataforma SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="f23cf-139">hello main purpose of this design is that hello user can focus on their own business logics, and leaving other things toobe handled by SCP.NET platform.</span></span>

<span data-ttu-id="f23cf-140">código de plug-in do usuário Olá deve implementar uma das interfaces do seguinte hello, depende se a topologia de saudação é transacional ou não transacional, e se o componente de saudação é spout ou raio.</span><span class="sxs-lookup"><span data-stu-id="f23cf-140">hello user plugin code should implement one of hello followings interfaces, depends on whether hello topology is transactional or non-transactional, and whether hello component is spout or bolt.</span></span>

* <span data-ttu-id="f23cf-141">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="f23cf-141">ISCPSpout</span></span>
* <span data-ttu-id="f23cf-142">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="f23cf-142">ISCPBolt</span></span>
* <span data-ttu-id="f23cf-143">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="f23cf-143">ISCPTxSpout</span></span>
* <span data-ttu-id="f23cf-144">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="f23cf-144">ISCPBatchBolt</span></span>

### <a name="iscpplugin"></a><span data-ttu-id="f23cf-145">ISCPPlugin</span><span class="sxs-lookup"><span data-stu-id="f23cf-145">ISCPPlugin</span></span>
<span data-ttu-id="f23cf-146">ISCPPlugin é uma interface comum para todos os tipos de plug-ins de saudação.</span><span class="sxs-lookup"><span data-stu-id="f23cf-146">ISCPPlugin is hello common interface for all kinds of plugins.</span></span> <span data-ttu-id="f23cf-147">Atualmente, trata-se de uma interface fictícia.</span><span class="sxs-lookup"><span data-stu-id="f23cf-147">Currently, it is a dummy interface.</span></span>

    public interface ISCPPlugin 
    {
    }

### <a name="iscpspout"></a><span data-ttu-id="f23cf-148">ISCPSpout</span><span class="sxs-lookup"><span data-stu-id="f23cf-148">ISCPSpout</span></span>
<span data-ttu-id="f23cf-149">ISCPSpout é a interface Olá para spout não transacional.</span><span class="sxs-lookup"><span data-stu-id="f23cf-149">ISCPSpout is hello interface for non-transactional spout.</span></span>

     public interface ISCPSpout : ISCPPlugin                    
     {
         void NextTuple(Dictionary<string, Object> parms);         
         void Ack(long seqId, Dictionary<string, Object> parms);   
         void Fail(long seqId, Dictionary<string, Object> parms);  
     }

<span data-ttu-id="f23cf-150">Quando `NextTuple()` é chamado, Olá C\# código do usuário pode emitir uma ou mais tuplas.</span><span class="sxs-lookup"><span data-stu-id="f23cf-150">When `NextTuple()` is called, hello C\# user code can emit one or more tuples.</span></span> <span data-ttu-id="f23cf-151">Se não houver nada tooemit, esse método deve retornar sem emitir nada.</span><span class="sxs-lookup"><span data-stu-id="f23cf-151">If there is nothing tooemit, this method should return without emitting anything.</span></span> <span data-ttu-id="f23cf-152">Observe que `NextTuple()`, `Ack()` e `Fail()` são chamados em um loop coeso em um único thread no processo C\#.</span><span class="sxs-lookup"><span data-stu-id="f23cf-152">It should be noted that `NextTuple()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="f23cf-153">Quando não houver nenhum tooemit tuplas, é toohave cortês NextTuple suspensão por um curto período de tempo (por exemplo, 10 milissegundos), não toowaste muito da CPU.</span><span class="sxs-lookup"><span data-stu-id="f23cf-153">When there are no tuples tooemit, it is courteous toohave NextTuple sleep for a short amount of time (such as 10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="f23cf-154">`Ack()` e `Fail()` serão chamados somente quando o mecanismo de reconhecimento estiver habilitado no arquivo de especificações.</span><span class="sxs-lookup"><span data-stu-id="f23cf-154">`Ack()` and `Fail()` will be called only when ack mechanism is enabled in spec file.</span></span> <span data-ttu-id="f23cf-155">Olá `seqId` é usado tooidentify Olá tupla que é confirmada ou falhou.</span><span class="sxs-lookup"><span data-stu-id="f23cf-155">hello `seqId` is used tooidentify hello tuple which is acked or failed.</span></span> <span data-ttu-id="f23cf-156">Para que se ack é habilitado na topologia não-transacional, Olá emit função a seguir deve ser usada em Spout:</span><span class="sxs-lookup"><span data-stu-id="f23cf-156">So if ack is enabled in non-transactional topology, hello following emit function should be used in Spout:</span></span>

    public abstract void Emit(string streamId, List<object> values, long seqId); 

<span data-ttu-id="f23cf-157">Se não há suporte para o ack na topologia não-transacional, Olá `Ack()` e `Fail()` pode ser deixado como função vazia.</span><span class="sxs-lookup"><span data-stu-id="f23cf-157">If ack is not supported in non-transactional topology, hello `Ack()` and `Fail()` can be left as empty function.</span></span>

<span data-ttu-id="f23cf-158">Olá `parms` parâmetros de entrada nessas funções são dicionário apenas vazio, elas estão reservadas para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="f23cf-158">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbolt"></a><span data-ttu-id="f23cf-159">ISCPBolt</span><span class="sxs-lookup"><span data-stu-id="f23cf-159">ISCPBolt</span></span>
<span data-ttu-id="f23cf-160">ISCPBolt é a interface de saudação de raio não transacional.</span><span class="sxs-lookup"><span data-stu-id="f23cf-160">ISCPBolt is hello interface for non-transactional bolt.</span></span>

    public interface ISCPBolt : ISCPPlugin 
    {
    void Execute(SCPTuple tuple);           
    }

<span data-ttu-id="f23cf-161">Quando a nova coleção de itens estiver disponível, Olá `Execute()` função será chamada tooprocess-lo.</span><span class="sxs-lookup"><span data-stu-id="f23cf-161">When new tuple is available, hello `Execute()` function will be called tooprocess it.</span></span>

### <a name="iscptxspout"></a><span data-ttu-id="f23cf-162">ISCPTxSpout</span><span class="sxs-lookup"><span data-stu-id="f23cf-162">ISCPTxSpout</span></span>
<span data-ttu-id="f23cf-163">ISCPTxSpout é a interface Olá para spout transacional.</span><span class="sxs-lookup"><span data-stu-id="f23cf-163">ISCPTxSpout is hello interface for transactional spout.</span></span>

    public interface ISCPTxSpout : ISCPPlugin
    {
        void NextTx(out long seqId, Dictionary<string, Object> parms);  
        void Ack(long seqId, Dictionary<string, Object> parms);         
        void Fail(long seqId, Dictionary<string, Object> parms);        
    }

<span data-ttu-id="f23cf-164">Assim como suas contrapartes não transacionais, `NextTx()`, `Ack()` e `Fail()` são chamados em um loop coeso em um único thread no processo C\#.</span><span class="sxs-lookup"><span data-stu-id="f23cf-164">Just like their non-transactional counter-part, `NextTx()`, `Ack()`, and `Fail()` are all called in a tight loop in a single thread in C\# process.</span></span> <span data-ttu-id="f23cf-165">Quando não houver nenhum tooemit de dados, é toohave cortês `NextTx` de espera por um curto período de tempo (10 milissegundos) assim como não toowaste muito da CPU.</span><span class="sxs-lookup"><span data-stu-id="f23cf-165">When there are no data tooemit, it is courteous toohave `NextTx` sleep for a short amount of time (10 milliseconds) so as not toowaste too much CPU.</span></span>

<span data-ttu-id="f23cf-166">`NextTx()`é chamado toostart uma nova transação, hello parâmetro out `seqId` tooidentify usado Olá transação, que também é usado em `Ack()` e `Fail()`.</span><span class="sxs-lookup"><span data-stu-id="f23cf-166">`NextTx()` is called toostart a new transaction, hello out parameter `seqId` is used tooidentify hello transaction, which is also used in `Ack()` and `Fail()`.</span></span> <span data-ttu-id="f23cf-167">Em `NextTx()`, usuários podem emitir dados tooJava lado.</span><span class="sxs-lookup"><span data-stu-id="f23cf-167">In `NextTx()`, user can emit data tooJava side.</span></span> <span data-ttu-id="f23cf-168">Olá dados serão armazenados na reprodução de toosupport ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="f23cf-168">hello data will be stored in ZooKeeper toosupport replay.</span></span> <span data-ttu-id="f23cf-169">Porque a capacidade de saudação do ZooKeeper é bastante limitada, usuário só deve emitir metadados, não os dados em massa em spout transacional.</span><span class="sxs-lookup"><span data-stu-id="f23cf-169">Because hello capacity of ZooKeeper is very limited, user should only emit metadata, not bulk data in transactional spout.</span></span>

<span data-ttu-id="f23cf-170">O Storm reproduzirá uma transação automaticamente se falhar, por isso, `Fail()` não deve ser chamado em um caso normal.</span><span class="sxs-lookup"><span data-stu-id="f23cf-170">Storm will replay a transaction automatically if it fails, so `Fail()` should not be called in normal case.</span></span> <span data-ttu-id="f23cf-171">Mas se SCP pode verificar metadados Olá emitidos pelo spout transacional, ele pode chamar `Fail()` quando Olá metadados são inválido.</span><span class="sxs-lookup"><span data-stu-id="f23cf-171">But if SCP can check hello metadata emitted by transactional spout, it can call `Fail()` when hello metadata is invalid.</span></span>

<span data-ttu-id="f23cf-172">Olá `parms` parâmetros de entrada nessas funções são dicionário apenas vazio, elas estão reservadas para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="f23cf-172">hello `parms` input parameters in these functions are just empty Dictionary, they are reserved for future use.</span></span>

### <a name="iscpbatchbolt"></a><span data-ttu-id="f23cf-173">ISCPBatchBolt</span><span class="sxs-lookup"><span data-stu-id="f23cf-173">ISCPBatchBolt</span></span>
<span data-ttu-id="f23cf-174">ISCPBatchBolt é a interface de saudação de raio transacional.</span><span class="sxs-lookup"><span data-stu-id="f23cf-174">ISCPBatchBolt is hello interface for transactional bolt.</span></span>

    public interface ISCPBatchBolt : ISCPPlugin           
    {
        void Execute(SCPTuple tuple);
        void FinishBatch(Dictionary<string, Object> parms);  
    }

<span data-ttu-id="f23cf-175">`Execute()`é chamado quando há nova tupla que chegam a isoladas hello.</span><span class="sxs-lookup"><span data-stu-id="f23cf-175">`Execute()` is called when there is new tuple arriving at hello bolt.</span></span> <span data-ttu-id="f23cf-176">`FinishBatch()` é chamado quando essa transação é encerrada.</span><span class="sxs-lookup"><span data-stu-id="f23cf-176">`FinishBatch()` is called when this transaction is ended.</span></span> <span data-ttu-id="f23cf-177">Olá `parms` parâmetro de entrada é reservado para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="f23cf-177">hello `parms` input parameter is reserved for future use.</span></span>

<span data-ttu-id="f23cf-178">Para topologia transacional, há um conceito importante: `StormTxAttempt`.</span><span class="sxs-lookup"><span data-stu-id="f23cf-178">For transactional topology, there is an important concept – `StormTxAttempt`.</span></span> <span data-ttu-id="f23cf-179">Ele tem dois campos, `TxId` e `AttemptId`.</span><span class="sxs-lookup"><span data-stu-id="f23cf-179">It has two fields, `TxId` and `AttemptId`.</span></span> <span data-ttu-id="f23cf-180">`TxId`é usado tooidentify uma transação específica e para uma determinada transação, pode haver vários tentativa se transação Olá falha e for repetido.</span><span class="sxs-lookup"><span data-stu-id="f23cf-180">`TxId` is used tooidentify a specific transaction, and for a given transaction, there may be multiple attempt if hello transaction fails and is replayed.</span></span> <span data-ttu-id="f23cf-181">SCP.NET novo será um diferentes ISCPBatchBolt objeto tooprocess cada `StormTxAttempt`, como o que significam Storm no lado do Java.</span><span class="sxs-lookup"><span data-stu-id="f23cf-181">SCP.NET will new a different ISCPBatchBolt object tooprocess each `StormTxAttempt`, just like what Storm do in Java side.</span></span> <span data-ttu-id="f23cf-182">Olá finalidade esse design é toosupport processamento de transações paralelas.</span><span class="sxs-lookup"><span data-stu-id="f23cf-182">hello purpose of this design is toosupport parallel transactions processing.</span></span> <span data-ttu-id="f23cf-183">Usuário deverão ser mantidos em mente que se a tentativa da transação for concluída, o objeto de ISCPBatchBolt correspondente hello será destruído e coletado como lixo.</span><span class="sxs-lookup"><span data-stu-id="f23cf-183">User should keep it in mind that if transaction attempt is finished, hello corresponding ISCPBatchBolt object will be destroyed and garbage collected.</span></span>

## <a name="object-model"></a><span data-ttu-id="f23cf-184">Modelo de objeto</span><span class="sxs-lookup"><span data-stu-id="f23cf-184">Object Model</span></span>
<span data-ttu-id="f23cf-185">SCP.NET também fornece um conjunto simples de objetos de chave para os desenvolvedores tooprogram com.</span><span class="sxs-lookup"><span data-stu-id="f23cf-185">SCP.NET also provides a simple set of key objects for developers tooprogram with.</span></span> <span data-ttu-id="f23cf-186">Eles são **Context**, **StateStore** e **SCPRuntime**.</span><span class="sxs-lookup"><span data-stu-id="f23cf-186">They are **Context**, **StateStore**, and **SCPRuntime**.</span></span> <span data-ttu-id="f23cf-187">Eles serão discutidos em parte Olá restante desta seção.</span><span class="sxs-lookup"><span data-stu-id="f23cf-187">They will be discussed in hello rest part of this section.</span></span>

### <a name="context"></a><span data-ttu-id="f23cf-188">Contexto</span><span class="sxs-lookup"><span data-stu-id="f23cf-188">Context</span></span>
<span data-ttu-id="f23cf-189">Contexto fornece um aplicativo de toohello ambiente em execução.</span><span class="sxs-lookup"><span data-stu-id="f23cf-189">Context provides a running environment toohello application.</span></span> <span data-ttu-id="f23cf-190">Cada instância ISCPPlugin (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) possui uma instância de Contexto correspondente.</span><span class="sxs-lookup"><span data-stu-id="f23cf-190">Each ISCPPlugin instance (ISCPSpout/ISCPBolt/ISCPTxSpout/ISCPBatchBolt) has a corresponding Context instance.</span></span> <span data-ttu-id="f23cf-191">funcionalidade Olá fornecida pelo contexto pode ser dividida em duas partes: parte estática hello (1), que está disponível no hello inteiro C\# processar parte dinâmica hello (2), que está disponível somente para a instância do contexto específica hello.</span><span class="sxs-lookup"><span data-stu-id="f23cf-191">hello functionality provided by Context can be divided into two parts: (1) hello static part which is available in hello whole C\# process, (2) hello dynamic part which is only available for hello specific Context instance.</span></span>

### <a name="static-part"></a><span data-ttu-id="f23cf-192">Parte Estática</span><span class="sxs-lookup"><span data-stu-id="f23cf-192">Static Part</span></span>
    public static ILogger Logger = null;
    public static SCPPluginType pluginType;                      
    public static Config Config { get; set; }                    
    public static TopologyContext TopologyContext { get; set; }  

<span data-ttu-id="f23cf-193">`Logger` é fornecido para fins de obtenção de log.</span><span class="sxs-lookup"><span data-stu-id="f23cf-193">`Logger` is provided for log purpose.</span></span>

<span data-ttu-id="f23cf-194">`pluginType`é usado tooindicate tipo de plug-in de saudação de saudação C\# processo.</span><span class="sxs-lookup"><span data-stu-id="f23cf-194">`pluginType` is used tooindicate hello plugin type of hello C\# process.</span></span> <span data-ttu-id="f23cf-195">Se Olá C\# processo é executado no modo de teste local (sem Java), é do tipo de plug-in de saudação `SCP_NET_LOCAL`.</span><span class="sxs-lookup"><span data-stu-id="f23cf-195">If hello C\# process is run in local test mode (without Java), hello plugin type is `SCP_NET_LOCAL`.</span></span>

    public enum SCPPluginType 
    {
        SCP_NET_LOCAL = 0,       
        SCP_NET_SPOUT = 1,       
        SCP_NET_BOLT = 2,        
        SCP_NET_TX_SPOUT = 3,   
        SCP_NET_BATCH_BOLT = 4  
    }

<span data-ttu-id="f23cf-196">`Config`é fornecida tooget parâmetros de configuração do lado do Java.</span><span class="sxs-lookup"><span data-stu-id="f23cf-196">`Config` is provided tooget configuration parameters from Java side.</span></span> <span data-ttu-id="f23cf-197">Olá parâmetros são passados do lado do Java quando C\# plug-in é inicializado.</span><span class="sxs-lookup"><span data-stu-id="f23cf-197">hello parameters are passed from Java side when C\# plugin is initialized.</span></span> <span data-ttu-id="f23cf-198">Olá `Config` parâmetros são divididos em duas partes: `stormConf` e `pluginConf`.</span><span class="sxs-lookup"><span data-stu-id="f23cf-198">hello `Config` parameters are divided into two parts: `stormConf` and `pluginConf`.</span></span>

    public Dictionary<string, Object> stormConf { get; set; }  
    public Dictionary<string, Object> pluginConf { get; set; }  

<span data-ttu-id="f23cf-199">`stormConf`é definidos pelo profusão de parâmetros e `pluginConf` é parâmetros Olá definidos pelo SCP.</span><span class="sxs-lookup"><span data-stu-id="f23cf-199">`stormConf` is parameters defined by Storm and `pluginConf` is hello parameters defined by SCP.</span></span> <span data-ttu-id="f23cf-200">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f23cf-200">For example:</span></span>

    public class Constants
    {
        … …

        // constant string for pluginConf
        public static readonly String NONTRANSACTIONAL_ENABLE_ACK = "nontransactional.ack.enabled";  

        // constant string for stormConf
        public static readonly String STORM_ZOOKEEPER_SERVERS = "storm.zookeeper.servers";           
        public static readonly String STORM_ZOOKEEPER_PORT = "storm.zookeeper.port";                 
    }

<span data-ttu-id="f23cf-201">`TopologyContext`é fornecido o contexto de topologia do tooget Olá, é mais útil para componentes com vários paralelismo.</span><span class="sxs-lookup"><span data-stu-id="f23cf-201">`TopologyContext` is provided tooget hello topology context, it is most useful for components with multiple parallelism.</span></span> <span data-ttu-id="f23cf-202">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="f23cf-202">Here is an example:</span></span>

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

### <a name="dynamic-part"></a><span data-ttu-id="f23cf-203">Parte Dinâmica</span><span class="sxs-lookup"><span data-stu-id="f23cf-203">Dynamic Part</span></span>
<span data-ttu-id="f23cf-204">Olá interfaces a seguir é pertinente tooa determinada a instância do contexto.</span><span class="sxs-lookup"><span data-stu-id="f23cf-204">hello following interfaces are pertinent tooa certain Context instance.</span></span> <span data-ttu-id="f23cf-205">a instância do contexto Olá é criada pela plataforma SCP.NET e passada toohello código do usuário:</span><span class="sxs-lookup"><span data-stu-id="f23cf-205">hello Context instance is created by SCP.NET platform and passed toohello user code:</span></span>

    // Declare hello Output and Input Stream Schemas

    public void DeclareComponentSchema(ComponentStreamSchema schema);   

    // Emit tuple toodefault stream.
    public abstract void Emit(List<object> values);                   

    // Emit tuple toohello specific stream.
    public abstract void Emit(string streamId, List<object> values);  

<span data-ttu-id="f23cf-206">Para não-transacional spout suporte ack, Olá método a seguir é fornecida:</span><span class="sxs-lookup"><span data-stu-id="f23cf-206">For non-transactional spout supporting ack, hello following method is provided:</span></span>

    // for non-transactional Spout which supports ack
    public abstract void Emit(string streamId, List<object> values, long seqId);  

<span data-ttu-id="f23cf-207">Para não-transacional raio ack de suporte, ele deve explicitamente `Ack()` ou `Fail()` Olá tupla que ele recebeu.</span><span class="sxs-lookup"><span data-stu-id="f23cf-207">For non-transactional bolt supporting ack, it should explicitly `Ack()` or `Fail()` hello tuple it received.</span></span> <span data-ttu-id="f23cf-208">E, ao emitir nova tupla, deve também especificar âncoras Olá de tupla novo hello.</span><span class="sxs-lookup"><span data-stu-id="f23cf-208">And when emitting new tuple, it must also specify hello anchors of hello new tuple.</span></span> <span data-ttu-id="f23cf-209">Olá métodos a seguir é fornecido.</span><span class="sxs-lookup"><span data-stu-id="f23cf-209">hello following methods are provided.</span></span>

    public abstract void Emit(string streamId, IEnumerable<SCPTuple> anchors, List<object> values); 
    public abstract void Ack(SCPTuple tuple);
    public abstract void Fail(SCPTuple tuple);

### <a name="statestore"></a><span data-ttu-id="f23cf-210">StateStore</span><span class="sxs-lookup"><span data-stu-id="f23cf-210">StateStore</span></span>
<span data-ttu-id="f23cf-211">`StateStore` oferece serviços de metadados, geração de sequência monotônica e coordenação sem espera.</span><span class="sxs-lookup"><span data-stu-id="f23cf-211">`StateStore` provides metadata services, monotonic sequence generation, and wait-free coordination.</span></span> <span data-ttu-id="f23cf-212">Abstrações de simultaneidade distribuídas de níveis mais altos podem ser baseadas no `StateStore`, incluindo bloqueios distribuídos, filas distribuídas, barreiras e serviços transacionais.</span><span class="sxs-lookup"><span data-stu-id="f23cf-212">Higher-level distributed concurrency abstractions can be built on `StateStore`, including distributed locks, distributed queues, barriers, and transaction services.</span></span>

<span data-ttu-id="f23cf-213">SCP aplicativos podem usar o hello `State` objeto toopersist algumas informações no ZooKeeper, especialmente para a topologia transacional.</span><span class="sxs-lookup"><span data-stu-id="f23cf-213">SCP applications may use hello `State` object toopersist some information in ZooKeeper, especially for transactional topology.</span></span> <span data-ttu-id="f23cf-214">Fazendo isso, se spout transacional falhar e reiniciar, ele pode recuperar informações necessárias de saudação do ZooKeeper e reinicie o pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="f23cf-214">Doing so, if transactional spout crashes and restart, it can retrieve hello necessary information from ZooKeeper and restart hello pipeline.</span></span>

<span data-ttu-id="f23cf-215">Olá `StateStore` objeto principalmente tem estes métodos:</span><span class="sxs-lookup"><span data-stu-id="f23cf-215">hello `StateStore` object mainly has these methods:</span></span>

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

<span data-ttu-id="f23cf-216">Olá `State` objeto principalmente tem estes métodos:</span><span class="sxs-lookup"><span data-stu-id="f23cf-216">hello `State` object mainly has these methods:</span></span>

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

<span data-ttu-id="f23cf-217">Para Olá `Commit()` método, quando simpleMode está definida tootrue, ele simplesmente excluir Olá correspondente ZNode em ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="f23cf-217">For hello `Commit()` method, when simpleMode is set tootrue, it will simply delete hello corresponding ZNode in ZooKeeper.</span></span> <span data-ttu-id="f23cf-218">Caso contrário, ele excluirá Olá ZNode atual e adicionar um novo nó Olá confirmado\_caminho.</span><span class="sxs-lookup"><span data-stu-id="f23cf-218">Otherwise, it will delete hello current ZNode, and adding a new node in hello COMMITTED\_PATH.</span></span>

### <a name="scpruntime"></a><span data-ttu-id="f23cf-219">SCPRuntime</span><span class="sxs-lookup"><span data-stu-id="f23cf-219">SCPRuntime</span></span>
<span data-ttu-id="f23cf-220">SCPRuntime fornece Olá dois métodos a seguir.</span><span class="sxs-lookup"><span data-stu-id="f23cf-220">SCPRuntime provides hello following two methods.</span></span>

    public static void Initialize();

    public static void LaunchPlugin(newSCPPlugin createDelegate);  

<span data-ttu-id="f23cf-221">`Initialize()`é o ambiente de tempo de execução Olá SCP tooinitialize usado.</span><span class="sxs-lookup"><span data-stu-id="f23cf-221">`Initialize()` is used tooinitialize hello SCP runtime environment.</span></span> <span data-ttu-id="f23cf-222">Nesse método, Olá C\# processo conectará toohello Java e obtém os parâmetros de configuração e do contexto de topologia.</span><span class="sxs-lookup"><span data-stu-id="f23cf-222">In this method, hello C\# process will connect toohello Java side, and gets configuration parameters and topology context.</span></span>

<span data-ttu-id="f23cf-223">`LaunchPlugin()`tookick usado fora da mensagem de saudação está processando o loop.</span><span class="sxs-lookup"><span data-stu-id="f23cf-223">`LaunchPlugin()` is used tookick off hello message processing loop.</span></span> <span data-ttu-id="f23cf-224">Nesse loop, Olá C\# plug-in receberá mensagens formulário lado Java (incluindo sinais tuplas e controle) e processar mensagens de saudação, talvez chamando o método de interface hello fornecem pelo código do usuário hello.</span><span class="sxs-lookup"><span data-stu-id="f23cf-224">In this loop, hello C\# plugin will receive messages form Java side (including tuples and control signals), and then process hello messages, perhaps calling hello interface method provide by hello user code.</span></span> <span data-ttu-id="f23cf-225">o parâmetro de entrada Hello para o método `LaunchPlugin()` é um delegado que pode retornar um objeto que implementa a interface ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt.</span><span class="sxs-lookup"><span data-stu-id="f23cf-225">hello input parameter for method `LaunchPlugin()` is a delegate that can return an object that implement ISCPSpout/IScpBolt/ISCPTxSpout/ISCPBatchBolt interface.</span></span>

    public delegate ISCPPlugin newSCPPlugin(Context ctx, Dictionary\<string, Object\> parms); 

<span data-ttu-id="f23cf-226">Para ISCPBatchBolt, podemos obter `StormTxAttempt` de `parms`e usá-lo toojudge se trata de uma tentativa de reproduzido.</span><span class="sxs-lookup"><span data-stu-id="f23cf-226">For ISCPBatchBolt, we can get `StormTxAttempt` from `parms`, and use it toojudge whether it is a replayed attempt.</span></span> <span data-ttu-id="f23cf-227">Geralmente, isso é feito em um raio de confirmação de saudação e ele é demonstrado no hello `HelloWorldTx` exemplo.</span><span class="sxs-lookup"><span data-stu-id="f23cf-227">This is usually done at hello commit bolt, and it is demonstrated in hello `HelloWorldTx` example.</span></span>

<span data-ttu-id="f23cf-228">Em geral, Olá SCP plug-ins pode ser executado em dois modos aqui:</span><span class="sxs-lookup"><span data-stu-id="f23cf-228">Generally speaking, hello SCP plugins may run in two modes here:</span></span>

1. <span data-ttu-id="f23cf-229">Modo de teste local: Nesse modo, Olá SCP plug-ins (Olá C\# código do usuário) executado dentro do Visual Studio durante a fase de desenvolvimento de saudação.</span><span class="sxs-lookup"><span data-stu-id="f23cf-229">Local Test Mode: In this mode, hello SCP plugins (hello C\# user code) run inside Visual Studio during hello development phase.</span></span> <span data-ttu-id="f23cf-230">`LocalContext`pode ser usado nesse modo, o que fornece o método tooserialize Olá emitido tuplas toolocal arquivos e leia-os de volta toomemory.</span><span class="sxs-lookup"><span data-stu-id="f23cf-230">`LocalContext` can be used in this mode, which provides method tooserialize hello emitted tuples toolocal files, and read them back toomemory.</span></span>
   
        public interface ILocalContext
        {
            List\<SCPTuple\> RecvFromMsgQueue();
            void WriteMsgQueueToFile(string filepath, bool append = false);  
            void ReadFromFileToMsgQueue(string filepath);                    
        }
2. <span data-ttu-id="f23cf-231">Modo normal: Nesse modo, plug-ins do hello SCP são iniciados pelo processo de java storm.</span><span class="sxs-lookup"><span data-stu-id="f23cf-231">Regular Mode: In this mode, hello SCP plugins are launched by storm java process.</span></span>
   
    <span data-ttu-id="f23cf-232">Aqui está um exemplo da inicialização do plugin do SCP:</span><span class="sxs-lookup"><span data-stu-id="f23cf-232">Here is an example of launching SCP plugin:</span></span>
   
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

## <a name="topology-specification-language"></a><span data-ttu-id="f23cf-233">Linguagem de Especificação da Topologia</span><span class="sxs-lookup"><span data-stu-id="f23cf-233">Topology Specification Language</span></span>
<span data-ttu-id="f23cf-234">A Especificação da Topologia do SCP é uma linguagem específica do domínio para descrever e configurar topologias do SCP.</span><span class="sxs-lookup"><span data-stu-id="f23cf-234">SCP Topology Specification is a domain specific language for describing and configuring SCP topologies.</span></span> <span data-ttu-id="f23cf-235">Ela se baseia no Clojure DSL do Storm (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) e é estendida pelo SCP.</span><span class="sxs-lookup"><span data-stu-id="f23cf-235">It is based on Storm’s Clojure DSL (<http://storm.incubator.apache.org/documentation/Clojure-DSL.html>) and is extended by SCP.</span></span>

<span data-ttu-id="f23cf-236">Especificações de topologia podem ser enviadas diretamente toostorm de cluster para execução via Olá ***runspec*** comando.</span><span class="sxs-lookup"><span data-stu-id="f23cf-236">Topology specifications can be submitted directly toostorm cluster for execution via hello ***runspec*** command.</span></span>

<span data-ttu-id="f23cf-237">SCP.NET tem adicionar siga funções toodefine Olá topologia transacional:</span><span class="sxs-lookup"><span data-stu-id="f23cf-237">SCP.NET has add follow functions toodefine hello Transactional Topology:</span></span>

| <span data-ttu-id="f23cf-238">**Novas funções**</span><span class="sxs-lookup"><span data-stu-id="f23cf-238">**New Functions**</span></span> | <span data-ttu-id="f23cf-239">**Parâmetros**</span><span class="sxs-lookup"><span data-stu-id="f23cf-239">**Parameters**</span></span> | <span data-ttu-id="f23cf-240">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="f23cf-240">**Description**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="f23cf-241">**tx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="f23cf-241">**tx-topolopy**</span></span> |<span data-ttu-id="f23cf-242">topology-name</span><span class="sxs-lookup"><span data-stu-id="f23cf-242">topology-name</span></span><br /><span data-ttu-id="f23cf-243">spout-map</span><span class="sxs-lookup"><span data-stu-id="f23cf-243">spout-map</span></span><br /><span data-ttu-id="f23cf-244">bolt-map</span><span class="sxs-lookup"><span data-stu-id="f23cf-244">bolt-map</span></span> |<span data-ttu-id="f23cf-245">Definir uma topologia transacional com o nome de topologia hello, &nbsp;spouts mapa de definição e mapa de definição de parafusos Olá</span><span class="sxs-lookup"><span data-stu-id="f23cf-245">Define a transactional topology with hello topology name, &nbsp;spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="f23cf-246">**scp-tx-spout**</span><span class="sxs-lookup"><span data-stu-id="f23cf-246">**scp-tx-spout**</span></span> |<span data-ttu-id="f23cf-247">exec-name</span><span class="sxs-lookup"><span data-stu-id="f23cf-247">exec-name</span></span><br /><span data-ttu-id="f23cf-248">args</span><span class="sxs-lookup"><span data-stu-id="f23cf-248">args</span></span><br /><span data-ttu-id="f23cf-249">fields</span><span class="sxs-lookup"><span data-stu-id="f23cf-249">fields</span></span> |<span data-ttu-id="f23cf-250">Defina um spout transacional.</span><span class="sxs-lookup"><span data-stu-id="f23cf-250">Define a transactional spout.</span></span> <span data-ttu-id="f23cf-251">Ele será executado o aplicativo hello com ***nome exec*** usando ***args***.</span><span class="sxs-lookup"><span data-stu-id="f23cf-251">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="f23cf-252">Olá ***campos*** é Olá campos de saída para spout</span><span class="sxs-lookup"><span data-stu-id="f23cf-252">hello ***fields*** is hello Output Fields for spout</span></span> |
| <span data-ttu-id="f23cf-253">**scp-tx-batch-bolt**</span><span class="sxs-lookup"><span data-stu-id="f23cf-253">**scp-tx-batch-bolt**</span></span> |<span data-ttu-id="f23cf-254">exec-name</span><span class="sxs-lookup"><span data-stu-id="f23cf-254">exec-name</span></span><br /><span data-ttu-id="f23cf-255">args</span><span class="sxs-lookup"><span data-stu-id="f23cf-255">args</span></span><br /><span data-ttu-id="f23cf-256">fields</span><span class="sxs-lookup"><span data-stu-id="f23cf-256">fields</span></span> |<span data-ttu-id="f23cf-257">Defina um bolt em lote transacional.</span><span class="sxs-lookup"><span data-stu-id="f23cf-257">Define a transactional Batch Bolt.</span></span> <span data-ttu-id="f23cf-258">Ele será executado o aplicativo hello com ***nome exec*** usando ***args.***</span><span class="sxs-lookup"><span data-stu-id="f23cf-258">It will run hello application with ***exec-name*** using ***args.***</span></span><br /><br /><span data-ttu-id="f23cf-259">Olá campos é hello campos de saída para o raio.</span><span class="sxs-lookup"><span data-stu-id="f23cf-259">hello Fields is hello Output Fields for bolt.</span></span> |
| <span data-ttu-id="f23cf-260">**scp-tx-commit-bolt**</span><span class="sxs-lookup"><span data-stu-id="f23cf-260">**scp-tx-commit-bolt**</span></span> |<span data-ttu-id="f23cf-261">exec-name</span><span class="sxs-lookup"><span data-stu-id="f23cf-261">exec-name</span></span><br /><span data-ttu-id="f23cf-262">args</span><span class="sxs-lookup"><span data-stu-id="f23cf-262">args</span></span><br /><span data-ttu-id="f23cf-263">fields</span><span class="sxs-lookup"><span data-stu-id="f23cf-263">fields</span></span> |<span data-ttu-id="f23cf-264">Defina um bolt confirmador transacional.</span><span class="sxs-lookup"><span data-stu-id="f23cf-264">Define a transactional Committer Bolt.</span></span> <span data-ttu-id="f23cf-265">Ele será executado o aplicativo hello com ***nome exec*** usando ***args***.</span><span class="sxs-lookup"><span data-stu-id="f23cf-265">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="f23cf-266">Olá ***campos*** é Olá campos de saída para o raio</span><span class="sxs-lookup"><span data-stu-id="f23cf-266">hello ***fields*** is hello Output Fields for bolt</span></span> |
| <span data-ttu-id="f23cf-267">**nontx-topolopy**</span><span class="sxs-lookup"><span data-stu-id="f23cf-267">**nontx-topolopy**</span></span> |<span data-ttu-id="f23cf-268">topology-name</span><span class="sxs-lookup"><span data-stu-id="f23cf-268">topology-name</span></span><br /><span data-ttu-id="f23cf-269">spout-map</span><span class="sxs-lookup"><span data-stu-id="f23cf-269">spout-map</span></span><br /><span data-ttu-id="f23cf-270">bolt-map</span><span class="sxs-lookup"><span data-stu-id="f23cf-270">bolt-map</span></span> |<span data-ttu-id="f23cf-271">Definir uma topologia não transacional com o nome de topologia hello,&nbsp; spouts mapa de definição e mapa de definição de parafusos Olá</span><span class="sxs-lookup"><span data-stu-id="f23cf-271">Define a nontransactional topology with hello topology name,&nbsp; spouts definition map and hello bolts definition map</span></span> |
| <span data-ttu-id="f23cf-272">**scp-spout**</span><span class="sxs-lookup"><span data-stu-id="f23cf-272">**scp-spout**</span></span> |<span data-ttu-id="f23cf-273">exec-name</span><span class="sxs-lookup"><span data-stu-id="f23cf-273">exec-name</span></span><br /><span data-ttu-id="f23cf-274">args</span><span class="sxs-lookup"><span data-stu-id="f23cf-274">args</span></span><br /><span data-ttu-id="f23cf-275">fields</span><span class="sxs-lookup"><span data-stu-id="f23cf-275">fields</span></span><br /><span data-ttu-id="f23cf-276">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="f23cf-276">parameters</span></span> |<span data-ttu-id="f23cf-277">Defina um spout não transacional.</span><span class="sxs-lookup"><span data-stu-id="f23cf-277">Define a nontransactional spout.</span></span> <span data-ttu-id="f23cf-278">Ele será executado o aplicativo hello com ***nome exec*** usando ***args***.</span><span class="sxs-lookup"><span data-stu-id="f23cf-278">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="f23cf-279">Olá ***campos*** é Olá campos de saída para spout</span><span class="sxs-lookup"><span data-stu-id="f23cf-279">hello ***fields*** is hello Output Fields for spout</span></span><br /><br /><span data-ttu-id="f23cf-280">Olá ***parâmetros*** é opcional, usá-lo toospecify alguns parâmetros, como "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="f23cf-280">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |
| <span data-ttu-id="f23cf-281">**scp-bolt**</span><span class="sxs-lookup"><span data-stu-id="f23cf-281">**scp-bolt**</span></span> |<span data-ttu-id="f23cf-282">exec-name</span><span class="sxs-lookup"><span data-stu-id="f23cf-282">exec-name</span></span><br /><span data-ttu-id="f23cf-283">args</span><span class="sxs-lookup"><span data-stu-id="f23cf-283">args</span></span><br /><span data-ttu-id="f23cf-284">fields</span><span class="sxs-lookup"><span data-stu-id="f23cf-284">fields</span></span><br /><span data-ttu-id="f23cf-285">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="f23cf-285">parameters</span></span> |<span data-ttu-id="f23cf-286">Defina um bolt não transacional.</span><span class="sxs-lookup"><span data-stu-id="f23cf-286">Define a nontransactional Bolt.</span></span> <span data-ttu-id="f23cf-287">Ele será executado o aplicativo hello com ***nome exec*** usando ***args***.</span><span class="sxs-lookup"><span data-stu-id="f23cf-287">It will run hello application with ***exec-name*** using ***args***.</span></span><br /><br /><span data-ttu-id="f23cf-288">Olá ***campos*** é Olá campos de saída para o raio</span><span class="sxs-lookup"><span data-stu-id="f23cf-288">hello ***fields*** is hello Output Fields for bolt</span></span><br /><br /><span data-ttu-id="f23cf-289">Olá ***parâmetros*** é opcional, usá-lo toospecify alguns parâmetros, como "nontransactional.ack.enabled".</span><span class="sxs-lookup"><span data-stu-id="f23cf-289">hello ***parameters*** is optional, using it toospecify some parameters such as "nontransactional.ack.enabled".</span></span> |

<span data-ttu-id="f23cf-290">O SCP.NET possui as seguintes palavras-chave definidas:</span><span class="sxs-lookup"><span data-stu-id="f23cf-290">SCP.NET has follow keys words defined:</span></span>

| <span data-ttu-id="f23cf-291">**Palavras-chave**</span><span class="sxs-lookup"><span data-stu-id="f23cf-291">**Key Words**</span></span> | <span data-ttu-id="f23cf-292">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="f23cf-292">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="f23cf-293">**:name**</span><span class="sxs-lookup"><span data-stu-id="f23cf-293">**:name**</span></span> |<span data-ttu-id="f23cf-294">Definir Olá topologia nome</span><span class="sxs-lookup"><span data-stu-id="f23cf-294">Define hello Topology Name</span></span> |
| <span data-ttu-id="f23cf-295">**:topology**</span><span class="sxs-lookup"><span data-stu-id="f23cf-295">**:topology**</span></span> |<span data-ttu-id="f23cf-296">Definir Olá topologia usando Olá acima funções e que criam as.</span><span class="sxs-lookup"><span data-stu-id="f23cf-296">Define hello Topology using hello above functions and build in ones.</span></span> |
| <span data-ttu-id="f23cf-297">**:p**</span><span class="sxs-lookup"><span data-stu-id="f23cf-297">**:p**</span></span> |<span data-ttu-id="f23cf-298">Defina a dica de paralelismo Olá para cada spout ou raio.</span><span class="sxs-lookup"><span data-stu-id="f23cf-298">Define hello parallelism hint for each spout or bolt.</span></span> |
| <span data-ttu-id="f23cf-299">**:config**</span><span class="sxs-lookup"><span data-stu-id="f23cf-299">**:config**</span></span> |<span data-ttu-id="f23cf-300">Definir Configurar parâmetro ou atualização Olá existentes</span><span class="sxs-lookup"><span data-stu-id="f23cf-300">Define configure parameter or update hello existing ones</span></span> |
| <span data-ttu-id="f23cf-301">**:schema**</span><span class="sxs-lookup"><span data-stu-id="f23cf-301">**:schema**</span></span> |<span data-ttu-id="f23cf-302">Defina Olá esquema de fluxo.</span><span class="sxs-lookup"><span data-stu-id="f23cf-302">Define hello Schema of Stream.</span></span> |

<span data-ttu-id="f23cf-303">Todos os parâmetros utilizados com frequência:</span><span class="sxs-lookup"><span data-stu-id="f23cf-303">And frequently-used parameters:</span></span>

| <span data-ttu-id="f23cf-304">**Parâmetro**</span><span class="sxs-lookup"><span data-stu-id="f23cf-304">**Parameter**</span></span> | <span data-ttu-id="f23cf-305">**Descrição**</span><span class="sxs-lookup"><span data-stu-id="f23cf-305">**Description**</span></span> |
| --- | --- |
| <span data-ttu-id="f23cf-306">**"plugin.name"**</span><span class="sxs-lookup"><span data-stu-id="f23cf-306">**"plugin.name"**</span></span> |<span data-ttu-id="f23cf-307">nome do arquivo exe do plug-in de saudação c#</span><span class="sxs-lookup"><span data-stu-id="f23cf-307">exe file name of hello C# plugin</span></span> |
| <span data-ttu-id="f23cf-308">**"plugin.args"**</span><span class="sxs-lookup"><span data-stu-id="f23cf-308">**"plugin.args"**</span></span> |<span data-ttu-id="f23cf-309">args do plugin</span><span class="sxs-lookup"><span data-stu-id="f23cf-309">plugin args</span></span> |
| <span data-ttu-id="f23cf-310">**"output.schema"**</span><span class="sxs-lookup"><span data-stu-id="f23cf-310">**"output.schema"**</span></span> |<span data-ttu-id="f23cf-311">Esquema de saída</span><span class="sxs-lookup"><span data-stu-id="f23cf-311">Output schema</span></span> |
| <span data-ttu-id="f23cf-312">**"nontransactional.ack.enabled"**</span><span class="sxs-lookup"><span data-stu-id="f23cf-312">**"nontransactional.ack.enabled"**</span></span> |<span data-ttu-id="f23cf-313">Se o reconhecimento está ativado para a topologia não transacional</span><span class="sxs-lookup"><span data-stu-id="f23cf-313">Whether ack is enabled for nontransactional topology</span></span> |

<span data-ttu-id="f23cf-314">comando de runspec Hello será implantado junto com os bits de hello, uso de saudação é como:</span><span class="sxs-lookup"><span data-stu-id="f23cf-314">hello runspec command will be deployed together with hello bits, hello usage is like:</span></span>

    .\bin\runSpec.cmd
    usage: runSpec [spec-file target-dir [resource-dir] [-cp classpath]]
    ex: runSpec examples\HelloWorld\HelloWorld.spec specs examples\HelloWorld\Target

<span data-ttu-id="f23cf-315">Olá ***recurso dir*** parâmetro é opcional, você precisa toospecify, quando você deseja tooplug C\# aplicativo e esse diretório conterá aplicativo hello, dependências hello e configurações.</span><span class="sxs-lookup"><span data-stu-id="f23cf-315">hello ***resource-dir*** parameter is optional, you need toospecify it when you want tooplug a C\# application, and this directory will contain hello application, hello dependencies and configurations.</span></span>

<span data-ttu-id="f23cf-316">Olá ***classpath*** parâmetro também é opcional.</span><span class="sxs-lookup"><span data-stu-id="f23cf-316">hello ***classpath*** parameter is also optional.</span></span> <span data-ttu-id="f23cf-317">É usado toospecify Olá Java classpath arquivo especificações Olá contém Java Spout ou raio.</span><span class="sxs-lookup"><span data-stu-id="f23cf-317">It is used toospecify hello Java classpath if hello spec file contains Java Spout or Bolt.</span></span>

## <a name="miscellaneous-features"></a><span data-ttu-id="f23cf-318">Recursos diversos</span><span class="sxs-lookup"><span data-stu-id="f23cf-318">Miscellaneous Features</span></span>
### <a name="input-and-output-schema-declaration"></a><span data-ttu-id="f23cf-319">Declaração de esquema de entrada e saída</span><span class="sxs-lookup"><span data-stu-id="f23cf-319">Input and Output Schema Declaration</span></span>
<span data-ttu-id="f23cf-320">usuário Olá pode emitir tupla em C\# processar, hello plataforma precisa tooserialize Olá tupla em byte [], do lado do tooJava de transferência, e Storm transferirá os destinos de toohello essa tupla.</span><span class="sxs-lookup"><span data-stu-id="f23cf-320">hello user can emit tuple in C\# process, hello platform needs tooserialize hello tuple into byte[], transfer tooJava side, and Storm will transfer this tuple toohello targets.</span></span> <span data-ttu-id="f23cf-321">Enquanto isso, no componente downstream, Olá C\# processo receber tupla do lado do java e convertê-la tipos originais toohello pela plataforma, todas essas operações são ocultos por Olá plataforma.</span><span class="sxs-lookup"><span data-stu-id="f23cf-321">Meanwhile in downstream component, hello C\# process will receive tuple back from java side, and convert it toohello original types by platform, all these operations are hidden by hello Platform.</span></span>

<span data-ttu-id="f23cf-322">toosupport Olá serialização e desserialização de, o código do usuário precisa toodeclare esquema de saudação do hello entradas e saídas.</span><span class="sxs-lookup"><span data-stu-id="f23cf-322">toosupport hello serialization and deserialization, user code needs toodeclare hello schema of hello inputs and outputs.</span></span>

<span data-ttu-id="f23cf-323">esquema de fluxo de entrada/saída de saudação é definido como um dicionário, chave de saudação é Olá StreamId e Olá é Olá tipos de colunas de saudação.</span><span class="sxs-lookup"><span data-stu-id="f23cf-323">hello input/output stream schema is defined as a dictionary, hello key is hello StreamId and hello value is hello Types of hello columns.</span></span> <span data-ttu-id="f23cf-324">componente de saudação pode ter vários fluxos declarados.</span><span class="sxs-lookup"><span data-stu-id="f23cf-324">hello component can have multi-streams declared.</span></span>

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


<span data-ttu-id="f23cf-325">Objeto de contexto, temos Olá adicionado seguinte API:</span><span class="sxs-lookup"><span data-stu-id="f23cf-325">In Context object, we have hello following API added:</span></span>

    public void DeclareComponentSchema(ComponentStreamSchema schema)

<span data-ttu-id="f23cf-326">Código do usuário deve verificar se tuplas Olá emitidas obedecer ao esquema Olá definida para esse fluxo ou sistema Olá lançará uma exceção de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="f23cf-326">User code must make sure hello tuples emitted obey hello schema defined for that stream, or hello system will throw a runtime exception.</span></span>

### <a name="multi-stream-support"></a><span data-ttu-id="f23cf-327">Suportes a múltiplos fluxos</span><span class="sxs-lookup"><span data-stu-id="f23cf-327">Multi-Stream Support</span></span>
<span data-ttu-id="f23cf-328">SCP dá suporte ao usuário código tooemit ou recebimento de vários fluxos distintos em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="f23cf-328">SCP supports user code tooemit or receive from multiple distinct streams at hello same time.</span></span> <span data-ttu-id="f23cf-329">suporte de saudação reflete no objeto de contexto hello como Olá Emit método aceita um parâmetro de ID de fluxo opcionais.</span><span class="sxs-lookup"><span data-stu-id="f23cf-329">hello support reflects in hello Context object as hello Emit method takes an optional stream ID parameter.</span></span>

<span data-ttu-id="f23cf-330">Dois métodos em Olá objeto de contexto SCP.NET foram adicionados.</span><span class="sxs-lookup"><span data-stu-id="f23cf-330">Two methods in hello SCP.NET Context object have been added.</span></span> <span data-ttu-id="f23cf-331">Eles são usados tooemit tupla ou tuplas toospecify StreamId.</span><span class="sxs-lookup"><span data-stu-id="f23cf-331">They are used tooemit Tuple or Tuples toospecify StreamId.</span></span> <span data-ttu-id="f23cf-332">Olá StreamId é uma cadeia de caracteres e precisa toobe consistente em ambas as C\# e Olá especificação de definição de topologia.</span><span class="sxs-lookup"><span data-stu-id="f23cf-332">hello StreamId is a string and it needs toobe consistent in both C\# and hello Topology Definition Spec.</span></span>

        /* Emit tuple toohello specific stream. */
        public abstract void Emit(string streamId, List<object> values);

        /* for non-transactional Spout only */
        public abstract void Emit(string streamId, List<object> values, long seqId);

<span data-ttu-id="f23cf-333">fluxo de não existente de tooa emissão Olá fará com que as exceções de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="f23cf-333">hello emitting tooa non-existing stream will cause runtime exceptions.</span></span>

### <a name="fields-grouping"></a><span data-ttu-id="f23cf-334">Agrupamento de Campos</span><span class="sxs-lookup"><span data-stu-id="f23cf-334">Fields Grouping</span></span>
<span data-ttu-id="f23cf-335">Olá que compilação no agrupamento de campos em Strom não está funcionando corretamente em SCP.NET.</span><span class="sxs-lookup"><span data-stu-id="f23cf-335">hello build-in Fields Grouping in Strom is not working properly in SCP.NET.</span></span> <span data-ttu-id="f23cf-336">Em Olá lado Java Proxy, todos os tipos de dados de campos de saudação são, na verdade, byte [] e campos Olá agrupamento usa Olá byte [] objeto hash código tooperform Olá de agrupamento.</span><span class="sxs-lookup"><span data-stu-id="f23cf-336">On hello Java Proxy side, all hello fields data types are actually byte[], and hello fields grouping uses hello byte[] object hash code tooperform hello grouping.</span></span> <span data-ttu-id="f23cf-337">o código de hash de objeto do Hello byte [] é o endereço de saudação do objeto na memória.</span><span class="sxs-lookup"><span data-stu-id="f23cf-337">hello byte[] object hash code is hello address of this object in memory.</span></span> <span data-ttu-id="f23cf-338">Para que agrupar Olá seja incorreto de dois bytes [] objetos Olá que compartilhar o mesmo conteúdo, mas não Olá mesmo endereço.</span><span class="sxs-lookup"><span data-stu-id="f23cf-338">So hello grouping will be wrong for two byte[] objects that share hello same content but not hello same address.</span></span>

<span data-ttu-id="f23cf-339">SCP.NET adiciona um método de agrupamento personalizados, e ele usará o conteúdo de saudação do agrupamento de Olá Olá byte [] toodo.</span><span class="sxs-lookup"><span data-stu-id="f23cf-339">SCP.NET adds a customized grouping method, and it will use hello content of hello byte[] toodo hello grouping.</span></span> <span data-ttu-id="f23cf-340">Em **especificação** sintaxe de saudação do arquivo, é como:</span><span class="sxs-lookup"><span data-stu-id="f23cf-340">In **SPEC** file, hello syntax is like:</span></span>

    (bolt-spec
        {
            "spout_test" (scp-field-group :non-tx [0,1])
        }
        …
    )


<span data-ttu-id="f23cf-341">Aqui,</span><span class="sxs-lookup"><span data-stu-id="f23cf-341">Here,</span></span>

1. <span data-ttu-id="f23cf-342">“scp-field-group” significa “Agrupamento de campo personalizado implementado pelo SCP”.</span><span class="sxs-lookup"><span data-stu-id="f23cf-342">"scp-field-group" means "Customized field grouping implemented by SCP".</span></span>
2. <span data-ttu-id="f23cf-343">“:tx” ou “:non-tx” significa que se trata de uma topologia transacional.</span><span class="sxs-lookup"><span data-stu-id="f23cf-343">":tx" or ":non-tx" means if it’s transactional topology.</span></span> <span data-ttu-id="f23cf-344">Precisamos essas informações como Olá iniciando o índice é diferente em tx versus não tx topologias.</span><span class="sxs-lookup"><span data-stu-id="f23cf-344">We need this information since hello starting index is different in tx vs. non-tx topologies.</span></span>
3. <span data-ttu-id="f23cf-345">[0,1] significa o hashset dos IDs do campo, começando do 0.</span><span class="sxs-lookup"><span data-stu-id="f23cf-345">[0,1] means a hashset of field Ids, starting from 0.</span></span>

### <a name="hybrid-topology"></a><span data-ttu-id="f23cf-346">Topologia híbrida</span><span class="sxs-lookup"><span data-stu-id="f23cf-346">Hybrid topology</span></span>
<span data-ttu-id="f23cf-347">Olá que Storm nativo é escrito em Java.</span><span class="sxs-lookup"><span data-stu-id="f23cf-347">hello native Storm is written in Java.</span></span> <span data-ttu-id="f23cf-348">E SCP.Net foi aprimorada tooenable nosso toowrite personalizada C\# código toohandle sua lógica de negócios.</span><span class="sxs-lookup"><span data-stu-id="f23cf-348">And SCP.Net has enhanced it tooenable our customs toowrite C\# code toohandle their business logic.</span></span> <span data-ttu-id="f23cf-349">Mas também damos suporte a topologias híbridas, que contêm não apenas spouts/bolts do C\#, mas também do Java.</span><span class="sxs-lookup"><span data-stu-id="f23cf-349">But we also support hybrid topologies, which contains not only C\# spouts/bolts, but also Java Spout/Bolts.</span></span>

### <a name="specify-java-spoutbolt-in-spec-file"></a><span data-ttu-id="f23cf-350">Especificar o Spout/Bol do Java no arquivo de especificações</span><span class="sxs-lookup"><span data-stu-id="f23cf-350">Specify Java Spout/Bolt in spec file</span></span>
<span data-ttu-id="f23cf-351">No arquivo especial, "scp spout" e "raio scp" também podem ser usado toospecify Java Spouts e parafusos, aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="f23cf-351">In spec file, "scp-spout" and "scp-bolt" can also be used toospecify Java Spouts and Bolts, here is an example:</span></span>

    (spout-spec 
      (microsoft.scp.example.HybridTopology.Generator.)           
      :p 1)

<span data-ttu-id="f23cf-352">Aqui `microsoft.scp.example.HybridTopology.Generator` é Olá nome da classe Java Spout de saudação.</span><span class="sxs-lookup"><span data-stu-id="f23cf-352">Here `microsoft.scp.example.HybridTopology.Generator` is hello name of hello Java Spout class.</span></span>

### <a name="specify-java-classpath-in-runspec-command"></a><span data-ttu-id="f23cf-353">Especificar o caminho de classe do Java no comando runSpec</span><span class="sxs-lookup"><span data-stu-id="f23cf-353">Specify Java Classpath in runSpec Command</span></span>
<span data-ttu-id="f23cf-354">Se você quiser toosubmit topologia contendo Java Spouts ou parafusos, for necessário toofirst Olá de compilação Java Spouts ou parafusos e obter arquivos Jar de saudação.</span><span class="sxs-lookup"><span data-stu-id="f23cf-354">If you want toosubmit topology containing Java Spouts or Bolts, you need toofirst compile hello Java Spouts or Bolts and get hello Jar files.</span></span> <span data-ttu-id="f23cf-355">Em seguida, você deve especificar o classpath java Olá que contém os arquivos Jar do hello durante o envio de topologia.</span><span class="sxs-lookup"><span data-stu-id="f23cf-355">Then you should specify hello java classpath that contains hello Jar files when submitting topology.</span></span> <span data-ttu-id="f23cf-356">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="f23cf-356">Here is an example:</span></span>

    bin\runSpec.cmd examples\HybridTopology\HybridTopology.spec specs examples\HybridTopology\net\Target -cp examples\HybridTopology\java\target\*

<span data-ttu-id="f23cf-357">Aqui **exemplos\\HybridTopology\\java\\destino\\**  é o hello pasta que contém o arquivo Jar do Java Spout/raio de saudação.</span><span class="sxs-lookup"><span data-stu-id="f23cf-357">Here **examples\\HybridTopology\\java\\target\\** is hello folder containing hello Java Spout/Bolt Jar file.</span></span>

### <a name="serialization-and-deserialization-between-java-and-c"></a><span data-ttu-id="f23cf-358">Serialização e desserialização entre Java e C\\</span><span class="sxs-lookup"><span data-stu-id="f23cf-358">Serialization and Deserialization between Java and C\\</span></span>
<span data-ttu-id="f23cf-359">Nosso componente SCP inclui lado de Java e de C\#.</span><span class="sxs-lookup"><span data-stu-id="f23cf-359">Our SCP component includes Java side and C\# side.</span></span> <span data-ttu-id="f23cf-360">Em ordem toointeract com Spouts/parafusos Java nativo, serialização/desserialização deve ser feita entre C e do Java\# lado, conforme ilustrado na Olá gráfico a seguir.</span><span class="sxs-lookup"><span data-stu-id="f23cf-360">In order toointeract with native Java Spouts/Bolts, Serialization/Deserialization must be carried out between Java side and C\# side, as illustrated in hello following graph.</span></span>

![diagrama de componente de java enviando componente tooSCP enviar tooJava componente](media/hdinsight-storm-scp-programming-guide/java-compent-sending-to-scp-component-sending-to-java-component.png)

1. <span data-ttu-id="f23cf-362">**Serialização no lado do Java e desserialização no lado do C\#**</span><span class="sxs-lookup"><span data-stu-id="f23cf-362">**Serialization in Java side and Deserialization in C\# side**</span></span>
   
   <span data-ttu-id="f23cf-363">Primeiro, fornecemos a implementação padrão para serialização no lado do Java e a desserialização no lado do C\#.</span><span class="sxs-lookup"><span data-stu-id="f23cf-363">First we provide default implementation for serialization in Java side and deserialization in C\# side.</span></span> <span data-ttu-id="f23cf-364">método de serialização Hello no lado do Java pode ser especificado no arquivo especificações:</span><span class="sxs-lookup"><span data-stu-id="f23cf-364">hello serialization method in Java side can be specified in SPEC file:</span></span>
   
       (scp-bolt
           {
               "plugin.name" "HybridTopology.exe"
               "plugin.args" ["displayer"]
               "output.schema" {}
               "customized.java.serializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONSerializer"]
           })
   
   <span data-ttu-id="f23cf-365">Olá método de desserialização em C\# deve ser especificada em C\# código do usuário:</span><span class="sxs-lookup"><span data-stu-id="f23cf-365">hello deserialization method in C\# side should be specified in C\# user code:</span></span>
   
       Dictionary<string, List<Type>> inputSchema = new Dictionary<string, List<Type>>();
       inputSchema.Add("default", new List<Type>() { typeof(Person) });
       this.ctx.DeclareComponentSchema(new ComponentStreamSchema(inputSchema, null));
       this.ctx.DeclareCustomizedDeserializer(new CustomizedInteropJSONDeserializer());            
   
   <span data-ttu-id="f23cf-366">Esta implementação padrão deve lidar com a maioria dos casos, se o tipo de dados de saudação não é muito complexo.</span><span class="sxs-lookup"><span data-stu-id="f23cf-366">This default implementation should handle most cases if hello data type is not too complex.</span></span> <span data-ttu-id="f23cf-367">Em certos casos, ou porque hello tipo de dados do usuário é muito complexo ou hello desempenho de nossa implementação padrão não atende aos Olá requisito do usuário, o usuário pode plug-in sua própria implementação.</span><span class="sxs-lookup"><span data-stu-id="f23cf-367">For certain cases, either because hello user data type is too complex, or because hello performance of our default implementation does not meet hello user's requirement, user can plug-in their own implementation.</span></span>
   
   <span data-ttu-id="f23cf-368">Olá serializar interface java lado é definida como:</span><span class="sxs-lookup"><span data-stu-id="f23cf-368">hello serialize interface in java side is defined as:</span></span>
   
       public interface ICustomizedInteropJavaSerializer {
           public void prepare(String[] args);
           public List<ByteBuffer> serialize(List<Object> objectList);
       }
   
   <span data-ttu-id="f23cf-369">Olá desserializar interface em C\# lado é definida como:</span><span class="sxs-lookup"><span data-stu-id="f23cf-369">hello deserialize interface in C\# side is defined as:</span></span>
   
   <span data-ttu-id="f23cf-370">interface pública ICustomizedInteropCSharpDeserializer</span><span class="sxs-lookup"><span data-stu-id="f23cf-370">public interface ICustomizedInteropCSharpDeserializer</span></span>
   
       public interface ICustomizedInteropCSharpDeserializer
       {
           List<Object> Deserialize(List<byte[]> dataList, List<Type> targetTypes);
       }
2. <span data-ttu-id="f23cf-371">**Serialização no lado do C\# e desserialização no lado do Java**</span><span class="sxs-lookup"><span data-stu-id="f23cf-371">**Serialization in C\# side and Deserialization in Java side side**</span></span>
   
   <span data-ttu-id="f23cf-372">Olá o método de serialização em C\# deve ser especificada em C\# código do usuário:</span><span class="sxs-lookup"><span data-stu-id="f23cf-372">hello serialization method in C\# side should be specified in C\# user code:</span></span>
   
       this.ctx.DeclareCustomizedSerializer(new CustomizedInteropJSONSerializer()); 
   
   <span data-ttu-id="f23cf-373">Olá método de desserialização no lado do Java deve ser especificado no arquivo especificações:</span><span class="sxs-lookup"><span data-stu-id="f23cf-373">hello Deserialization method in Java side should be specified in SPEC file:</span></span>
   
     <span data-ttu-id="f23cf-374">(scp-spout</span><span class="sxs-lookup"><span data-stu-id="f23cf-374">(scp-spout</span></span>
   
       {
         "plugin.name" "HybridTopology.exe"
         "plugin.args" ["generator"]
         "output.schema" {"default" ["person"]}
         "customized.java.deserializer" ["microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" "microsoft.scp.example.HybridTopology.Person"]
       })
   
   <span data-ttu-id="f23cf-375">Aqui "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" é o nome de saudação do desserializador e "microsoft.scp.example.HybridTopology.Person" é dados de saudação de classe de destino de saudação são desserializados para.</span><span class="sxs-lookup"><span data-stu-id="f23cf-375">Here "microsoft.scp.storm.multilang.CustomizedInteropJSONDeserializer" is hello name of Deserializer, and "microsoft.scp.example.HybridTopology.Person" is hello target class hello data is deserialized to.</span></span>
   
   <span data-ttu-id="f23cf-376">O usuário também pode usar um plug-in para sua própria implementação de serializador de C\# e desserializador de Java.</span><span class="sxs-lookup"><span data-stu-id="f23cf-376">User can also plug-in their own implementation of C\# serializer and Java Deserializer.</span></span> <span data-ttu-id="f23cf-377">Esta é a interface Olá para C\# serializador:</span><span class="sxs-lookup"><span data-stu-id="f23cf-377">This is hello interface for C\# serializer:</span></span>
   
       public interface ICustomizedInteropCSharpSerializer
       {
           List<byte[]> Serialize(List<object> dataList);
       }
   
   <span data-ttu-id="f23cf-378">Esta é a interface de saudação para desserialização de Java:</span><span class="sxs-lookup"><span data-stu-id="f23cf-378">This is hello interface for Java Deserializer:</span></span>
   
       public interface ICustomizedInteropJavaDeserializer {
           public void prepare(String[] targetClassNames);
           public List<Object> Deserialize(List<ByteBuffer> dataList);
       }

## <a name="scp-host-mode"></a><span data-ttu-id="f23cf-379">Modo de host do SCP</span><span class="sxs-lookup"><span data-stu-id="f23cf-379">SCP Host Mode</span></span>
<span data-ttu-id="f23cf-380">Nesse modo, o usuário pode compilar tooDLL seus códigos e usar SCPHost.exe fornecido pela topologia de toosubmit SCP.</span><span class="sxs-lookup"><span data-stu-id="f23cf-380">In this mode, user can compile their codes tooDLL, and use SCPHost.exe provided by SCP toosubmit topology.</span></span> <span data-ttu-id="f23cf-381">arquivo de especificação de saudação tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="f23cf-381">hello spec file looks like this:</span></span>

    (scp-spout
      {
        "plugin.name" "SCPHost.exe"
        "plugin.args" ["HelloWorld.dll" "Scp.App.HelloWorld.Generator" "Get"]
        "output.schema" {"default" ["sentence"]}
      })

<span data-ttu-id="f23cf-382">Aqui, `plugin.name` é especificado como `SCPHost.exe` fornecido pelo SDK do SCP.</span><span class="sxs-lookup"><span data-stu-id="f23cf-382">Here, `plugin.name` is specified as `SCPHost.exe` provided by SCP SDK.</span></span> <span data-ttu-id="f23cf-383">O SCPHost.exe aceita exatamente três parâmetros:</span><span class="sxs-lookup"><span data-stu-id="f23cf-383">SCPHost.exe which accepts exactly three parameters:</span></span>

1. <span data-ttu-id="f23cf-384">Olá primeiro um é nome da DLL hello, que é `"HelloWorld.dll"` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="f23cf-384">hello first one is hello DLL name, which is `"HelloWorld.dll"` in this example.</span></span>
2. <span data-ttu-id="f23cf-385">Olá, um segundo é nome da classe hello, que é `"Scp.App.HelloWorld.Generator"` neste exemplo.</span><span class="sxs-lookup"><span data-stu-id="f23cf-385">hello second one is hello Class name, which is `"Scp.App.HelloWorld.Generator"` in this example.</span></span>
3. <span data-ttu-id="f23cf-386">Olá terceiro um é Olá nome de um método estático público, que pode ser invocado tooget uma instância de ISCPPlugin.</span><span class="sxs-lookup"><span data-stu-id="f23cf-386">hello third one is hello name of a public static method, which can be invoked tooget an instance of ISCPPlugin.</span></span>

<span data-ttu-id="f23cf-387">No modo do host, o código do usuário é compilado como DLL e é invocado pela plataforma SCP.</span><span class="sxs-lookup"><span data-stu-id="f23cf-387">In host mode, user code is compiled as DLL, and is invoked by SCP platform.</span></span> <span data-ttu-id="f23cf-388">Então plataforma SCP pode obter controle total da lógica de processamento inteiro hello.</span><span class="sxs-lookup"><span data-stu-id="f23cf-388">So SCP platform can get full control of hello whole processing logic.</span></span> <span data-ttu-id="f23cf-389">Portanto, recomendamos que nossos clientes toosubmit topologia em modo de SCP do host porque ele pode simplificar a experiência de desenvolvimento hello e nos trazem mais flexibilidade e melhor compatibilidade com versões anteriores também a versão mais recente.</span><span class="sxs-lookup"><span data-stu-id="f23cf-389">So we recommend our customers toosubmit topology in SCP host mode since it can simplify hello development experience and bring us more flexibility and better backward compatibility for later release as well.</span></span>

## <a name="scp-programming-examples"></a><span data-ttu-id="f23cf-390">Exemplos de programação do SCP</span><span class="sxs-lookup"><span data-stu-id="f23cf-390">SCP Programming Examples</span></span>
### <a name="helloworld"></a><span data-ttu-id="f23cf-391">HelloWorld</span><span class="sxs-lookup"><span data-stu-id="f23cf-391">HelloWorld</span></span>
<span data-ttu-id="f23cf-392">**HelloWorld** é um exemplo muito simples tooshow uma amostra de SCP.Net.</span><span class="sxs-lookup"><span data-stu-id="f23cf-392">**HelloWorld** is a very simple example tooshow a taste of SCP.Net.</span></span> <span data-ttu-id="f23cf-393">Ele usa uma topologia não transacional com um spout chamado **generator** e dois bolts chamados **splitter** e **counter**.</span><span class="sxs-lookup"><span data-stu-id="f23cf-393">It uses a non-transactional topology, with a spout called **generator**, and two bolts called **splitter** and **counter**.</span></span> <span data-ttu-id="f23cf-394">spout Olá **gerador** irá gerar aleatoriamente alguns sentenças e emitir essas frases muito**divisor**.</span><span class="sxs-lookup"><span data-stu-id="f23cf-394">hello spout **generator** will randomly generate some sentences, and emit these sentences too**splitter**.</span></span> <span data-ttu-id="f23cf-395">raio Olá **divisor** serão divididas Olá sentenças toowords e emitir essas palavras muito**contador** raio.</span><span class="sxs-lookup"><span data-stu-id="f23cf-395">hello bolt **splitter** will split hello sentences toowords and emit these words too**counter** bolt.</span></span> <span data-ttu-id="f23cf-396">Olá raio "counter" usa um número de ocorrência do dicionário toorecord saudação de cada palavra.</span><span class="sxs-lookup"><span data-stu-id="f23cf-396">hello bolt "counter" uses a dictionary toorecord hello occurrence number of each word.</span></span>

<span data-ttu-id="f23cf-397">Há dois arquivos de especificações, **HelloWorld.spec** e **HelloWorld\_EnableAck.spec** para este exemplo.</span><span class="sxs-lookup"><span data-stu-id="f23cf-397">There are two spec files, **HelloWorld.spec** and **HelloWorld\_EnableAck.spec** for this example.</span></span> <span data-ttu-id="f23cf-398">Em Olá C\# código, ele pode descobrir se o ack está habilitado obtendo pluginConf de saudação do lado do Java.</span><span class="sxs-lookup"><span data-stu-id="f23cf-398">In hello C\# code, it can find out whether ack is enabled by getting hello pluginConf from Java side.</span></span>

    /* demo how tooget pluginConf info */
    if (Context.Config.pluginConf.ContainsKey(Constants.NONTRANSACTIONAL_ENABLE_ACK))
    {
        enableAck = (bool)(Context.Config.pluginConf[Constants.NONTRANSACTIONAL_ENABLE_ACK]);
    }
    Context.Logger.Info("enableAck: {0}", enableAck);

<span data-ttu-id="f23cf-399">Spout Olá, se a confirmação for habilitada, um dicionário é usado toocache Olá tuplas que não foram controladas.</span><span class="sxs-lookup"><span data-stu-id="f23cf-399">In hello spout, if ack is enabled, a dictionary is used toocache hello tuples that have not been acked.</span></span> <span data-ttu-id="f23cf-400">Se for chamado Fail(), hello tupla com falha será reproduzida:</span><span class="sxs-lookup"><span data-stu-id="f23cf-400">If Fail() is called, hello failed tuple will be replayed:</span></span>

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

### <a name="helloworldtx"></a><span data-ttu-id="f23cf-401">HelloWorldTx</span><span class="sxs-lookup"><span data-stu-id="f23cf-401">HelloWorldTx</span></span>
<span data-ttu-id="f23cf-402">Olá **HelloWorldTx** exemplo demonstra como topologia transacional tooimplement.</span><span class="sxs-lookup"><span data-stu-id="f23cf-402">hello **HelloWorldTx** example demonstrates how tooimplement transactional topology.</span></span> <span data-ttu-id="f23cf-403">Ele tem um spout chamado **generator**, um bolt em lote chamado **partial-count** e um bolt de confirmação chamado **count-sum**.</span><span class="sxs-lookup"><span data-stu-id="f23cf-403">It have one spout called **generator**, a batch bolts called **partial-count**, and a commit bolt called **count-sum**.</span></span> <span data-ttu-id="f23cf-404">Também há três arquivos txt pré-criados: **DataSource0.txt**, **DataSource1.txt** e **DataSource2.txt**.</span><span class="sxs-lookup"><span data-stu-id="f23cf-404">There are also three pre-created txt files: **DataSource0.txt**, **DataSource1.txt** and **DataSource2.txt**.</span></span>

<span data-ttu-id="f23cf-405">Em cada transação, Olá spout **gerador** será aleatoriamente escolher dois arquivos de saudação criada previamente três arquivos e emitir toohello de nomes de arquivo hello dois **parcial contagem** raio.</span><span class="sxs-lookup"><span data-stu-id="f23cf-405">In each transaction, hello spout **generator** will randomly choose two files from hello pre-created three files, and emit hello two file names toohello **partial-count** bolt.</span></span> <span data-ttu-id="f23cf-406">raio Olá **parcial contagem** obterá primeiro nome de arquivo hello da tupla Olá recebida, Olá abrir arquivo e contagem Olá o número de palavras neste arquivo e, finalmente, emitir hello word número toohello **contagem total**raio.</span><span class="sxs-lookup"><span data-stu-id="f23cf-406">hello bolt **partial-count** will first get hello file name from hello received tuple, then open hello file and count hello number of words in this file, and finally emit hello word number toohello **count-sum** bolt.</span></span> <span data-ttu-id="f23cf-407">Olá **contagem soma** raio resumirá contagem total de saudação.</span><span class="sxs-lookup"><span data-stu-id="f23cf-407">hello **count-sum** bolt will summarize hello total count.</span></span>

<span data-ttu-id="f23cf-408">tooachieve **exatamente uma vez** semântica, raio de confirmação de saudação **contagem soma** necessário toojudge se trata de uma transação repetida.</span><span class="sxs-lookup"><span data-stu-id="f23cf-408">tooachieve **exactly once** semantics, hello commit bolt **count-sum** need toojudge whether it is a replayed transaction.</span></span> <span data-ttu-id="f23cf-409">Neste exemplo, ele possui uma variável do membro estático:</span><span class="sxs-lookup"><span data-stu-id="f23cf-409">In this example, it has a static member variable:</span></span>

    public static long lastCommittedTxId = -1; 

<span data-ttu-id="f23cf-410">Quando uma instância de ISCPBatchBolt é criada, ele receberá Olá `txAttempt` de parâmetros de entrada:</span><span class="sxs-lookup"><span data-stu-id="f23cf-410">When an ISCPBatchBolt instance is created, it will get hello `txAttempt` from input parameters:</span></span>

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

<span data-ttu-id="f23cf-411">Quando `FinishBatch()` é chamado, hello `lastCommittedTxId` será update se não for uma transação repetida.</span><span class="sxs-lookup"><span data-stu-id="f23cf-411">When `FinishBatch()` is called, hello `lastCommittedTxId` will be update if it is not a replayed transaction.</span></span>

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


### <a name="hybridtopology"></a><span data-ttu-id="f23cf-412">HybridTopology</span><span class="sxs-lookup"><span data-stu-id="f23cf-412">HybridTopology</span></span>
<span data-ttu-id="f23cf-413">Essa topologia contém um Spout do Java e um Bolt do C\#.</span><span class="sxs-lookup"><span data-stu-id="f23cf-413">This topology contains a Java Spout and a C\# Bolt.</span></span> <span data-ttu-id="f23cf-414">Ele usa Olá implementação padrão de serialização e desserialização fornecida pela plataforma SCP.</span><span class="sxs-lookup"><span data-stu-id="f23cf-414">It uses hello default serialization and deserialization implementation provided by SCP platform.</span></span> <span data-ttu-id="f23cf-415">Por favor Olá ref **HybridTopology.spec** na **exemplos\\HybridTopology** pasta para obter detalhes de especificação de arquivo hello, e **SubmitTopology.bat** como toospecify Java classpath.</span><span class="sxs-lookup"><span data-stu-id="f23cf-415">Please ref hello **HybridTopology.spec** in **examples\\HybridTopology** folder for hello spec file details, and **SubmitTopology.bat** for how toospecify Java classpath.</span></span>

### <a name="scphostdemo"></a><span data-ttu-id="f23cf-416">SCPHostDemo</span><span class="sxs-lookup"><span data-stu-id="f23cf-416">SCPHostDemo</span></span>
<span data-ttu-id="f23cf-417">Este exemplo é Olá essencialmente igual HelloWorld.</span><span class="sxs-lookup"><span data-stu-id="f23cf-417">This example is hello same as HelloWorld in essence.</span></span> <span data-ttu-id="f23cf-418">Hello somente diferença é que o código de usuário Olá é compilado como DLL e topologia Olá é enviada usando SCPHost.exe.</span><span class="sxs-lookup"><span data-stu-id="f23cf-418">hello only difference is that hello user code is compiled as DLL and hello topology is submitted by using SCPHost.exe.</span></span> <span data-ttu-id="f23cf-419">Faça a seção de saudação de ref "Modo de Host do SCP" para explicação mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="f23cf-419">Please ref hello section "SCP Host Mode" for more detailed explanation.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f23cf-420">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f23cf-420">Next Steps</span></span>
<span data-ttu-id="f23cf-421">Para obter exemplos de topologias Storm criados usando o SCP, consulte seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="f23cf-421">For examples of Storm topologies created using SCP, see hello following:</span></span>

* [<span data-ttu-id="f23cf-422">Desenvolver topologias C# para o Apache Storm no HDInsight usando o Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f23cf-422">Develop C# topologies for Apache Storm on HDInsight using Visual Studio</span></span>](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [<span data-ttu-id="f23cf-423">Processar eventos dos Hubs de Evento do Azure com o Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f23cf-423">Process events from Azure Event Hubs with Storm on HDInsight</span></span>](hdinsight-storm-develop-csharp-event-hub-topology.md)
* [<span data-ttu-id="f23cf-424">Criar vários fluxos de dados em uma topologia Storm em C#</span><span class="sxs-lookup"><span data-stu-id="f23cf-424">Create multiple data streams in a C# Storm topology</span></span>](hdinsight-storm-twitter-trending.md)
* [<span data-ttu-id="f23cf-425">Usar dados do Power Bi toovisualize de uma topologia Storm</span><span class="sxs-lookup"><span data-stu-id="f23cf-425">Use Power Bi toovisualize data from a Storm topology</span></span>](hdinsight-storm-power-bi-topology.md)
* [<span data-ttu-id="f23cf-426">Processar dados do sensor do veículo a partir de Hubs de Evento usando o Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f23cf-426">Process vehicle sensor data from Event Hubs using Storm on HDInsight</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/tree/master/IotExample)
* [<span data-ttu-id="f23cf-427">Extração, transformação e carregamento (ETL) de Hubs de eventos do Azure tooHBase</span><span class="sxs-lookup"><span data-stu-id="f23cf-427">Extract, Transform, and Load (ETL) from Azure Event Hubs tooHBase</span></span>](https://github.com/hdinsight/hdinsight-storm-examples/blob/master/RealTimeETLExample)
* [<span data-ttu-id="f23cf-428">Correlacionar eventos usando Storm e HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="f23cf-428">Correlate events using Storm and HBase on HDInsight</span></span>](hdinsight-storm-correlation-topology.md)

