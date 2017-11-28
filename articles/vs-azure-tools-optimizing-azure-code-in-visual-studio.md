---
title: "aaaOptimizing de código do Azure no Visual Studio | Microsoft Docs"
description: "Saiba mais sobre como as ferramentas de otimização de código do Azure no Visual Studio ajudam a tornar o código mais robusto e com melhor desempenho."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ed48ee06-e2d2-4322-af22-07200fb16987
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: 7df932def9dc16c93de29fc6a77c8fc121fda338
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="c2d03-103">Otimizando o código do Azure</span><span class="sxs-lookup"><span data-stu-id="c2d03-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="c2d03-104">Quando você estiver programando aplicativos que usam o Microsoft Azure, há algumas práticas de codificação que você deve seguir toohelp evitar problemas de escalabilidade do aplicativo, o comportamento e desempenho em um ambiente de nuvem.</span><span class="sxs-lookup"><span data-stu-id="c2d03-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow toohelp avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="c2d03-105">A Microsoft fornece uma ferramenta de análise de código do Azure que reconhece e identifica vários desses problemas comumente encontrados e ajuda a resolvê-los.</span><span class="sxs-lookup"><span data-stu-id="c2d03-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="c2d03-106">Você pode baixar a ferramenta Olá no Visual Studio por meio do NuGet.</span><span class="sxs-lookup"><span data-stu-id="c2d03-106">You can download hello tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="c2d03-107">Regras de análise de código do Azure</span><span class="sxs-lookup"><span data-stu-id="c2d03-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="c2d03-108">ferramenta de análise de código do Azure Olá usa Olá tooautomatically sinalizador seu código do Azure quando ele encontra problemas conhecidos afetam o desempenho de regras a seguir.</span><span class="sxs-lookup"><span data-stu-id="c2d03-108">hello Azure Code Analysis tool uses hello following rules tooautomatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="c2d03-109">Os problemas detectados aparecem como avisos ou erros do compilador.</span><span class="sxs-lookup"><span data-stu-id="c2d03-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="c2d03-110">Código correções ou sugestões tooresolve Olá aviso ou erro geralmente são fornecidos por meio de um ícone de lâmpada.</span><span class="sxs-lookup"><span data-stu-id="c2d03-110">Code fixes or suggestions tooresolve hello warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="c2d03-111">Evitar o uso do modo de estado de sessão padrão (em processo)</span><span class="sxs-lookup"><span data-stu-id="c2d03-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="c2d03-112">ID</span><span class="sxs-lookup"><span data-stu-id="c2d03-112">ID</span></span>
<span data-ttu-id="c2d03-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="c2d03-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="c2d03-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2d03-114">Description</span></span>
<span data-ttu-id="c2d03-115">Se você usar o modo de estado de sessão (em processo) saudação padrão para aplicativos em nuvem, você poderá perder o estado da sessão.</span><span class="sxs-lookup"><span data-stu-id="c2d03-115">If you use hello default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="c2d03-116">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="c2d03-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="c2d03-117">Motivo</span><span class="sxs-lookup"><span data-stu-id="c2d03-117">Reason</span></span>
<span data-ttu-id="c2d03-118">Por padrão, o modo de estado de sessão Olá especificado no arquivo Web. config de saudação estiver em processo.</span><span class="sxs-lookup"><span data-stu-id="c2d03-118">By default, hello session state mode specified in hello web.config file is in-process.</span></span> <span data-ttu-id="c2d03-119">Além disso, se nenhuma entrada foi especificada no arquivo de configuração hello, modo de estado da sessão de saudação padrão tooin-process.</span><span class="sxs-lookup"><span data-stu-id="c2d03-119">Also, if no entry specified in hello configuration file, hello Session State mode defaults tooin-process.</span></span> <span data-ttu-id="c2d03-120">modo do Hello em processo armazena o estado da sessão na memória no servidor de web hello.</span><span class="sxs-lookup"><span data-stu-id="c2d03-120">hello in-process mode stores session state in memory on hello web server.</span></span> <span data-ttu-id="c2d03-121">Quando uma instância é reiniciada ou uma nova instância é usada para balanceamento de carga ou o suporte a failover, o estado da sessão Olá armazenado na memória no servidor web de saudação não é salvos.</span><span class="sxs-lookup"><span data-stu-id="c2d03-121">When an instance is restarted or a new instance is used for load balancing or failover support, hello session state stored in memory on hello web server isn’t saved.</span></span> <span data-ttu-id="c2d03-122">Essa situação impede que o aplicativo hello sendo escalonável na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="c2d03-122">This situation prevents hello application from being scalable on hello cloud.</span></span>

<span data-ttu-id="c2d03-123">O estado da sessão ASP.NET dá suporte a várias opções diferentes de armazenamento para dados de estado de sessão: InProc, StateServer, SQLServer, Personalizado e Desativado.</span><span class="sxs-lookup"><span data-stu-id="c2d03-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="c2d03-124">É recomendável que você use dados de toohost de modo personalizado em um repositório externo do estado de sessão, como [provedor de estado de sessão do Azure para Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="c2d03-124">It’s recommended that you use Custom mode toohost data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="c2d03-125">Solução</span><span class="sxs-lookup"><span data-stu-id="c2d03-125">Solution</span></span>
<span data-ttu-id="c2d03-126">Uma solução recomendada é toostore estado da sessão em um serviço de cache gerenciado.</span><span class="sxs-lookup"><span data-stu-id="c2d03-126">One recommended solution is toostore session state on a managed cache service.</span></span> <span data-ttu-id="c2d03-127">Saiba como toouse [provedor de estado de sessão do Azure para Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore o estado da sessão.</span><span class="sxs-lookup"><span data-stu-id="c2d03-127">Learn how toouse [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) toostore your session state.</span></span> <span data-ttu-id="c2d03-128">Você pode também armazenamento de estado de sessão em outros lugares tooensure que seu aplicativo é escalonável na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="c2d03-128">You can also store session state in other places tooensure your application is scalable on hello cloud.</span></span> <span data-ttu-id="c2d03-129">toolearn mais sobre as soluções alternativas, consulte [modos de estado de sessão](https://msdn.microsoft.com/library/ms178586).</span><span class="sxs-lookup"><span data-stu-id="c2d03-129">toolearn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="c2d03-130">O método de execução não deve ser assíncrono</span><span class="sxs-lookup"><span data-stu-id="c2d03-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="c2d03-131">ID</span><span class="sxs-lookup"><span data-stu-id="c2d03-131">ID</span></span>
<span data-ttu-id="c2d03-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="c2d03-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="c2d03-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2d03-133">Description</span></span>
<span data-ttu-id="c2d03-134">Criar métodos assíncronos (como [await](https://msdn.microsoft.com/library/hh156528.aspx)) fora Olá [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método e, em seguida, chamar métodos de async saudação do [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2d03-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call hello async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="c2d03-135">Declarando Olá [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método como assíncronas faz com que o trabalho de saudação função tooenter um loop de reinicialização.</span><span class="sxs-lookup"><span data-stu-id="c2d03-135">Declaring hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes hello worker role tooenter a restart loop.</span></span>

<span data-ttu-id="c2d03-136">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="c2d03-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="c2d03-137">Motivo</span><span class="sxs-lookup"><span data-stu-id="c2d03-137">Reason</span></span>
<span data-ttu-id="c2d03-138">Chamando métodos assíncronos em Olá [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método faz com que a função de trabalho Olá nuvem service em tempo de execução toorecycle hello.</span><span class="sxs-lookup"><span data-stu-id="c2d03-138">Calling async methods inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello cloud service runtime toorecycle hello worker role.</span></span> <span data-ttu-id="c2d03-139">Quando uma função de trabalho é iniciado, o todos a execução do programa ocorre dentro de saudação [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="c2d03-139">When a worker role starts, all program execution takes place inside hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="c2d03-140">Olá existente [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método faz com que o trabalho de saudação toorestart de função.</span><span class="sxs-lookup"><span data-stu-id="c2d03-140">Exiting hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes hello worker role toorestart.</span></span> <span data-ttu-id="c2d03-141">Quando o tempo de execução de função de trabalho Olá atinge o método assíncrono de hello, ele envia todas as operações depois de método assíncrono de saudação e, em seguida, retorna.</span><span class="sxs-lookup"><span data-stu-id="c2d03-141">When hello worker role runtime hits hello async method, it dispatches all operations after hello async method and then returns.</span></span> <span data-ttu-id="c2d03-142">Isso faz com que trabalho Olá função tooexit de saudação [ [ [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método e reinicie.</span><span class="sxs-lookup"><span data-stu-id="c2d03-142">This causes hello worker role tooexit from hello [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="c2d03-143">Na próxima iteração de execução hello, função de trabalho Olá acertos Olá async método novamente e for reiniciado, fazendo com que o trabalho de saudação função toorecycle novamente.</span><span class="sxs-lookup"><span data-stu-id="c2d03-143">In hello next iteration of execution, hello worker role hits hello async method again and restarts, causing hello worker role toorecycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="c2d03-144">Solução</span><span class="sxs-lookup"><span data-stu-id="c2d03-144">Solution</span></span>
<span data-ttu-id="c2d03-145">Colocar todas as operações assíncronas fora Olá [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método.</span><span class="sxs-lookup"><span data-stu-id="c2d03-145">Place all async operations outside of hello [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="c2d03-146">Em seguida, chame o método assíncrono de saudação refatorado de dentro de saudação [ [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) ](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método, como RunAsync () .wait.</span><span class="sxs-lookup"><span data-stu-id="c2d03-146">Then, call hello refactored async method from inside hello [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="c2d03-147">ferramenta de análise de código do Azure Olá pode ajudá-lo a corrigir esse problema.</span><span class="sxs-lookup"><span data-stu-id="c2d03-147">hello Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="c2d03-148">saudação de trecho de código a seguir demonstra Olá código para corrigir esse problema:</span><span class="sxs-lookup"><span data-stu-id="c2d03-148">hello following code snippet demonstrates hello code fix for this issue:</span></span>

```
public override void Run()
{
    RunAsync().Wait();
}

public async Task RunAsync()
{
    //Asynchronous operations code logic
    // This is a sample worker implementation. Replace with your logic.

    Trace.TraceInformation("WorkerRole1 entry point called");

    HttpClient client = new HttpClient();

    Task<string> urlString = client.GetStringAsync("http://msdn.microsoft.com");

    while (true)
    {
        Thread.Sleep(10000);
        Trace.TraceInformation("Working");

        string stream = await urlString;
    }

}
```

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="c2d03-149">Autenticação de assinatura de acesso compartilhado com barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="c2d03-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="c2d03-150">ID</span><span class="sxs-lookup"><span data-stu-id="c2d03-150">ID</span></span>
<span data-ttu-id="c2d03-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="c2d03-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="c2d03-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2d03-152">Description</span></span>
<span data-ttu-id="c2d03-153">Use SAS (Assinatura de Acesso Compartilhado) para autenticação.</span><span class="sxs-lookup"><span data-stu-id="c2d03-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="c2d03-154">ACS (Serviço de Controle de Acesso) está sendo preterido para autenticação do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="c2d03-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="c2d03-155">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="c2d03-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="c2d03-156">Motivo</span><span class="sxs-lookup"><span data-stu-id="c2d03-156">Reason</span></span>
<span data-ttu-id="c2d03-157">Para mais segurança, o Active Directory do Azure está substituindo a autenticação do ACS pela autenticação SAS.</span><span class="sxs-lookup"><span data-stu-id="c2d03-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="c2d03-158">Consulte [Active Directory do Azure é Olá futuras do ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) para obter informações sobre o plano de transição de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2d03-158">See [Azure Active Directory is hello future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on hello transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="c2d03-159">Solução</span><span class="sxs-lookup"><span data-stu-id="c2d03-159">Solution</span></span>
<span data-ttu-id="c2d03-160">Use autenticação de SAS em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="c2d03-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="c2d03-161">saudação de exemplo a seguir mostra como toouse uma tooaccess token SAS um serviço existente do barramento do namespace ou entidade.</span><span class="sxs-lookup"><span data-stu-id="c2d03-161">hello following example shows how toouse an existing SAS token tooaccess a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="c2d03-162">Consulte Olá seguintes tópicos para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="c2d03-162">See hello following topics for more information.</span></span>

* <span data-ttu-id="c2d03-163">Para uma visão geral, consulte [Autenticação de assinatura de acesso compartilhado com barramento de serviço](https://msdn.microsoft.com/library/dn170477.aspx)</span><span class="sxs-lookup"><span data-stu-id="c2d03-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="c2d03-164">Como toouse compartilhado autenticação SAS com barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="c2d03-164">How toouse Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="c2d03-165">Para um projeto de exemplo, consulte [Usando SAS (Assinatura de Acesso Compartilhado) com assinaturas do barramento de serviço](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span><span class="sxs-lookup"><span data-stu-id="c2d03-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-tooavoid-receive-loop"></a><span data-ttu-id="c2d03-166">Considere o uso de OnMessage método tooavoid "loop de recebimento"</span><span class="sxs-lookup"><span data-stu-id="c2d03-166">Consider using OnMessage method tooavoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="c2d03-167">ID</span><span class="sxs-lookup"><span data-stu-id="c2d03-167">ID</span></span>
<span data-ttu-id="c2d03-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="c2d03-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="c2d03-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2d03-169">Description</span></span>
<span data-ttu-id="c2d03-170">tooavoid entrar em um "loop de recebimento" hello chamada **OnMessage** método é a melhor solução para receber mensagens de saudação chamada **Receive** método.</span><span class="sxs-lookup"><span data-stu-id="c2d03-170">tooavoid going into a "receive loop," calling hello **OnMessage** method is a better solution for receiving messages than calling hello **Receive** method.</span></span> <span data-ttu-id="c2d03-171">No entanto, se você precisar usar Olá **Receive** método e você especificar um tempo de espera do servidor não padrão, certifique-se de tempo de espera do servidor de saudação é de mais de um minuto.</span><span class="sxs-lookup"><span data-stu-id="c2d03-171">However, if you must use hello **Receive** method, and you specify a non-default server wait time, make sure hello server wait time is more than one minute.</span></span>

<span data-ttu-id="c2d03-172">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="c2d03-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="c2d03-173">Motivo</span><span class="sxs-lookup"><span data-stu-id="c2d03-173">Reason</span></span>
<span data-ttu-id="c2d03-174">Ao chamar **OnMessage**, cliente Olá inicia uma bomba de mensagem interno que monitora constantemente Olá fila ou assinatura.</span><span class="sxs-lookup"><span data-stu-id="c2d03-174">When calling **OnMessage**, hello client starts an internal message pump that constantly polls hello queue or subscription.</span></span> <span data-ttu-id="c2d03-175">A bomba de mensagens contém um loop infinito que emite uma chamada tooreceive mensagens.</span><span class="sxs-lookup"><span data-stu-id="c2d03-175">This message pump contains an infinite loop that issues a call tooreceive messages.</span></span> <span data-ttu-id="c2d03-176">Se a chamada de saudação expirar, ele emite uma chamada de novo.</span><span class="sxs-lookup"><span data-stu-id="c2d03-176">If hello call times out, it issues a new call.</span></span> <span data-ttu-id="c2d03-177">intervalo de tempo limite de saudação é determinado pelo valor de saudação do hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) propriedade Olá [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)que está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="c2d03-177">hello timeout interval is determined by hello value of hello [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of hello [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="c2d03-178">Olá vantagem de usar **OnMessage** comparados muito**Receive** é que os usuários não toomanually sondar mensagens, lidar com exceções, processar várias mensagens em paralelo e concluir Olá mensagens.</span><span class="sxs-lookup"><span data-stu-id="c2d03-178">hello advantage of using **OnMessage** compared too**Receive** is that users don’t have toomanually poll for messages, handle exceptions, process multiple messages in parallel, and complete hello messages.</span></span>

<span data-ttu-id="c2d03-179">Se você chamar **Receive** sem usar o valor padrão, ser Olá se *ServerWaitTime* valor é a mais de um minuto.</span><span class="sxs-lookup"><span data-stu-id="c2d03-179">If you call **Receive** without using its default value, be sure hello *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="c2d03-180">Configuração *ServerWaitTime* toomore de um minuto impede que o servidor de saudação tempo limite antes da mensagem de saudação totalmente é recebida.</span><span class="sxs-lookup"><span data-stu-id="c2d03-180">Setting *ServerWaitTime* toomore than one minute prevents hello server from timing out before hello message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="c2d03-181">Solução</span><span class="sxs-lookup"><span data-stu-id="c2d03-181">Solution</span></span>
<span data-ttu-id="c2d03-182">Consulte Olá exemplos de código para usos recomendados a seguir.</span><span class="sxs-lookup"><span data-stu-id="c2d03-182">Please see hello following code examples for recommended usages.</span></span> <span data-ttu-id="c2d03-183">Para obter mais detalhes, consulte o método [QueueClient.OnMessage (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) e o método [QueueClient.Receive (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2d03-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="c2d03-184">desempenho de saudação tooimprove de saudação infraestrutura de mensagens do Azure, consulte o padrão de design Olá [Primer de mensagens assíncronas](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2d03-184">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="c2d03-185">Olá, a seguir é um exemplo de uso **OnMessage** tooreceive mensagens.</span><span class="sxs-lookup"><span data-stu-id="c2d03-185">hello following is an example of using **OnMessage** tooreceive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if hello message-pump should call complete on messages after hello callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates hello maximum number of concurrent calls toohello callback hello pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you tooget notified of any errors encountered by hello message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates hello message pump and callback is invoked for each message that is recieved, calling close on hello client will stop hello pump.
    {
        // Process hello message.
    }, options);
    Console.WriteLine("Press any key tooexit.");
    Console.ReadKey();
```

<span data-ttu-id="c2d03-186">Olá, a seguir é um exemplo de uso **Receive** com o servidor de saudação tempo de espera.</span><span class="sxs-lookup"><span data-stu-id="c2d03-186">hello following is an example of using **Receive** with hello default server wait time.</span></span>

```
string connectionString =  
CloudConfigurationManager.GetSetting("Microsoft.ServiceBus.ConnectionString");

QueueClient Client =  
    QueueClient.CreateFromConnectionString(connectionString, "TestQueue");

while (true)  
{   
   BrokeredMessage message = Client.Receive();
   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
```

<span data-ttu-id="c2d03-187">Olá, a seguir é um exemplo de uso **Receive** tempo de espera com um servidor diferente do padrão.</span><span class="sxs-lookup"><span data-stu-id="c2d03-187">hello following is an example of using **Receive** with a non-default server wait time.</span></span>

```
while (true)  
{   
   BrokeredMessage message = Client.Receive(new TimeSpan(0,1,0));

   if (message != null)
   {
      try  
      {
         Console.WriteLine("Body: " + message.GetBody<string>());
         Console.WriteLine("MessageID: " + message.MessageId);
         Console.WriteLine("Test Property: " +  
            message.Properties["TestProperty"]);

         // Remove message from queue
         message.Complete();
      }

      catch (Exception)
      {
         // Indicate a problem, unlock message in queue
         message.Abandon();
      }
   }
}
```
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="c2d03-188">Considere o uso de métodos assíncronos de barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="c2d03-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="c2d03-189">ID</span><span class="sxs-lookup"><span data-stu-id="c2d03-189">ID</span></span>
<span data-ttu-id="c2d03-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="c2d03-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="c2d03-191">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2d03-191">Description</span></span>
<span data-ttu-id="c2d03-192">Use o desempenho de tooimprove de métodos de barramento de serviço assíncrono com mensagens orientadas.</span><span class="sxs-lookup"><span data-stu-id="c2d03-192">Use asynchronous Service Bus methods tooimprove performance with brokered messaging.</span></span>

<span data-ttu-id="c2d03-193">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="c2d03-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="c2d03-194">Motivo</span><span class="sxs-lookup"><span data-stu-id="c2d03-194">Reason</span></span>
<span data-ttu-id="c2d03-195">Usar métodos assíncronos habilita a simultaneidade de programa do aplicativo como executar cada chamada de não bloquear o thread principal de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2d03-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block hello main thread.</span></span> <span data-ttu-id="c2d03-196">Ao usar os métodos de mensagens do Barramento de Serviço, a execução de uma operação (enviar, receber, excluir, etc.) leva tempo.</span><span class="sxs-lookup"><span data-stu-id="c2d03-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="c2d03-197">Esse tempo inclui o processamento de Olá da operação de saudação pelo Olá barramento de serviço na latência de toohello de adição de solicitação de saudação e resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2d03-197">This time includes hello processing of hello operation by hello Service Bus service in addition toohello latency of hello request and hello reply.</span></span> <span data-ttu-id="c2d03-198">número de saudação tooincrease de operações por vez, as operações devem ser executadas simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="c2d03-198">tooincrease hello number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="c2d03-199">Para obter mais informações, consulte muito[práticas recomendadas para desempenho melhorias usando o serviço de barramento de mensagens orientadas](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2d03-199">For more information please refer too[Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="c2d03-200">Solução</span><span class="sxs-lookup"><span data-stu-id="c2d03-200">Solution</span></span>
<span data-ttu-id="c2d03-201">Consulte [QueueClient classe (. Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) para obter informações sobre como toouse Olá recomendado método assíncrono.</span><span class="sxs-lookup"><span data-stu-id="c2d03-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how toouse hello recommended asynchronous method.</span></span>

<span data-ttu-id="c2d03-202">desempenho de saudação tooimprove de saudação infraestrutura de mensagens do Azure, consulte o padrão de design Olá [Primer de mensagens assíncronas](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2d03-202">tooimprove hello performance of hello Azure messaging infrastructure, see hello design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="c2d03-203">Considerar o particionamento de tópicos e filas do barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="c2d03-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="c2d03-204">ID</span><span class="sxs-lookup"><span data-stu-id="c2d03-204">ID</span></span>
<span data-ttu-id="c2d03-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="c2d03-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="c2d03-206">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2d03-206">Description</span></span>
<span data-ttu-id="c2d03-207">Particione filas e tópicos do barramento de serviço para um melhor desempenho com as mensagens do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="c2d03-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="c2d03-208">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="c2d03-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="c2d03-209">Motivo</span><span class="sxs-lookup"><span data-stu-id="c2d03-209">Reason</span></span>
<span data-ttu-id="c2d03-210">Particionamento de tópicos e filas do barramento de serviço aumenta o desempenho taxa de transferência e disponibilidade do serviço porque hello taxa de transferência geral de uma fila ou tópico particionados não é mais limitada pelo desempenho de saudação de um único agente de mensagens ou repositório de mensagens.</span><span class="sxs-lookup"><span data-stu-id="c2d03-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because hello overall throughput of a partitioned queue or topic is no longer limited by hello performance of a single message broker or messaging store.</span></span> <span data-ttu-id="c2d03-211">Além disso, uma falha temporária de um repositório de mensagens não torna uma fila ou tópico particionado indisponível.</span><span class="sxs-lookup"><span data-stu-id="c2d03-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="c2d03-212">Para saber mais, confira [Particionamento de entidades de mensagens](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2d03-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="c2d03-213">Solução</span><span class="sxs-lookup"><span data-stu-id="c2d03-213">Solution</span></span>
<span data-ttu-id="c2d03-214">Olá seguindo o trecho de código mostra como toopartition entidades de mensagens.</span><span class="sxs-lookup"><span data-stu-id="c2d03-214">hello following code snippet shows how toopartition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="c2d03-215">Para obter mais informações, consulte [tópicos e filas do barramento de serviço particionado | Blog do Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) e check-out Olá [fila particionada do Microsoft Azure Service Bus](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) exemplo.</span><span class="sxs-lookup"><span data-stu-id="c2d03-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out hello [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="c2d03-216">Não definir SharedAccessStartTime</span><span class="sxs-lookup"><span data-stu-id="c2d03-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="c2d03-217">ID</span><span class="sxs-lookup"><span data-stu-id="c2d03-217">ID</span></span>
<span data-ttu-id="c2d03-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="c2d03-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="c2d03-219">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2d03-219">Description</span></span>
<span data-ttu-id="c2d03-220">Você deve evitar usar SharedAccessStartTimeset toohello tooimmediately iniciar Olá política de acesso compartilhado de tempo atual.</span><span class="sxs-lookup"><span data-stu-id="c2d03-220">You should avoid using SharedAccessStartTimeset toohello current time tooimmediately start hello Shared Access policy.</span></span> <span data-ttu-id="c2d03-221">Você só precisa tooset essa propriedade se você quiser política de acesso compartilhado toostart hello mais tarde.</span><span class="sxs-lookup"><span data-stu-id="c2d03-221">You only need tooset this property if you want toostart hello Shared Access policy at a later time.</span></span>

<span data-ttu-id="c2d03-222">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="c2d03-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="c2d03-223">Motivo</span><span class="sxs-lookup"><span data-stu-id="c2d03-223">Reason</span></span>
<span data-ttu-id="c2d03-224">A sincronização do relógio causa uma pequena diferença de hora entre os data centers.</span><span class="sxs-lookup"><span data-stu-id="c2d03-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="c2d03-225">Por exemplo, você logicamente consideraria hora de início de saudação de configuração de uma política SAS de armazenamento como hello hora atual usando Now ou um método semelhante fará com que efeito de tootake Olá SAS política imediatamente.</span><span class="sxs-lookup"><span data-stu-id="c2d03-225">For example, you would logically think setting hello start time of a storage SAS policy as hello current time by using DateTime.Now or a similar method will cause hello SAS policy tootake effect immediately.</span></span> <span data-ttu-id="c2d03-226">No entanto, diferenças de horários pequena de saudação entre data centers podem causar problemas com isso, já que algumas vezes de datacenter podem ser ligeiramente posteriores à hora de início do hello, enquanto outros antes que ele.</span><span class="sxs-lookup"><span data-stu-id="c2d03-226">However, hello slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than hello start time, while others ahead of it.</span></span> <span data-ttu-id="c2d03-227">Como resultado, Olá política da SAS pode expirar rapidamente (ou até mesmo imediatamente) se o tempo de vida de política de saudação é definido muito curto.</span><span class="sxs-lookup"><span data-stu-id="c2d03-227">As a result, hello SAS policy can expire quickly (or even immediately) if hello policy lifetime is set too short.</span></span>

<span data-ttu-id="c2d03-228">Para obter instruções sobre como usar a assinatura de acesso compartilhado no armazenamento do Azure, consulte [apresentando tabela SAS (assinatura de acesso compartilhado) SAS de fila de Site e atualização tooBlob SAS - Blog de equipe de armazenamento do Microsoft Azure - início - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2d03-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="c2d03-229">Solução</span><span class="sxs-lookup"><span data-stu-id="c2d03-229">Solution</span></span>
<span data-ttu-id="c2d03-230">Remova a instrução de saudação que define a hora de início Olá Olá compartilhado da política de acesso.</span><span class="sxs-lookup"><span data-stu-id="c2d03-230">Remove hello statement that sets hello start time of hello shared access policy.</span></span> <span data-ttu-id="c2d03-231">ferramenta de análise de código do Azure Olá fornece uma correção para esse problema.</span><span class="sxs-lookup"><span data-stu-id="c2d03-231">hello Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="c2d03-232">Para obter mais informações sobre gerenciamento de segurança, consulte o padrão de design Olá [manobrista chave padrão](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2d03-232">For more information on security management, please see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="c2d03-233">saudação de trecho de código a seguir demonstra Olá código para corrigir esse problema.</span><span class="sxs-lookup"><span data-stu-id="c2d03-233">hello following code snippet demonstrates hello code fix for this issue.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="c2d03-234">O tempo de expiração da Política de Acesso Compartilhado deve ser mais de cinco minutos</span><span class="sxs-lookup"><span data-stu-id="c2d03-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="c2d03-235">ID</span><span class="sxs-lookup"><span data-stu-id="c2d03-235">ID</span></span>
<span data-ttu-id="c2d03-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="c2d03-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="c2d03-237">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2d03-237">Description</span></span>
<span data-ttu-id="c2d03-238">Pode haver quanto um cinco minutos a diferença em relógios entre data centers em locais diferentes devido tooa condição conhecida como "pela defasagem horária".</span><span class="sxs-lookup"><span data-stu-id="c2d03-238">There can be as much as a five minute difference in clocks among datacenters at different locations due tooa condition known as "clock skew."</span></span> <span data-ttu-id="c2d03-239">token da política SAS tooprevent Olá expirem antes da data planejada, defina toobe de tempo de expiração de saudação mais de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="c2d03-239">tooprevent hello SAS policy token from expiring earlier than planned, set hello expiry time toobe more than five minutes.</span></span>

<span data-ttu-id="c2d03-240">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="c2d03-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="c2d03-241">Motivo</span><span class="sxs-lookup"><span data-stu-id="c2d03-241">Reason</span></span>
<span data-ttu-id="c2d03-242">Data centers em locais diferentes em torno de Olá, mundo sincronizem por um sinal de relógio.</span><span class="sxs-lookup"><span data-stu-id="c2d03-242">Datacenters at different locations around hello world synchronize by a clock signal.</span></span> <span data-ttu-id="c2d03-243">Como demora para locais de toodifferent de tootravel de sinal de relógio, pode ser uma variação de tempo entre data centers em locais geográficos diferentes embora supostamente tudo o que é sincronizado.</span><span class="sxs-lookup"><span data-stu-id="c2d03-243">Because it takes time for clock signal tootravel toodifferent locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="c2d03-244">Essa diferença de tempo pode afetar o acesso compartilhado política início tempo e expiração de intervalo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2d03-244">This time difference can affect hello Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="c2d03-245">Portanto, tooensure política de acesso compartilhado entra em vigor imediatamente, não especifique a hora de início de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2d03-245">Therefore, tooensure Shared Access policy takes effect immediately, don’t specify hello start time.</span></span> <span data-ttu-id="c2d03-246">Além disso, certifique-se de tempo de expiração de saudação é maior que o tempo limite inicial de tooprevent de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="c2d03-246">In addition, make sure hello expiration time is more than 5 minutes tooprevent early timeout.</span></span>

<span data-ttu-id="c2d03-247">Para obter mais informações sobre como usar a assinatura de acesso compartilhado no armazenamento do Azure, consulte [apresentando tabela SAS (assinatura de acesso compartilhado) SAS de fila de Site e atualização tooBlob SAS - Blog de equipe de armazenamento do Microsoft Azure - início - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2d03-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update tooBlob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="c2d03-248">Solução</span><span class="sxs-lookup"><span data-stu-id="c2d03-248">Solution</span></span>
<span data-ttu-id="c2d03-249">Para obter mais informações sobre gerenciamento de segurança, consulte o padrão de design Olá [manobrista chave padrão](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2d03-249">For more information on security management, see hello design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="c2d03-250">a seguir Olá é um exemplo de não especificar uma hora de início da política de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="c2d03-250">hello following is an example of not specifying a Shared Access policy start time.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="c2d03-251">a seguir Olá é um exemplo de especificar uma hora de início da política de acesso compartilhado com uma duração de expiração de política mais de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="c2d03-251">hello following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// hello shared access policy provides  
// read/write access toohello container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // tooensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="c2d03-252">Para obter mais informações, consulte [Criar e usar uma assinatura de acesso compartilhado](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2d03-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="c2d03-253">Use CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="c2d03-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="c2d03-254">ID</span><span class="sxs-lookup"><span data-stu-id="c2d03-254">ID</span></span>
<span data-ttu-id="c2d03-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="c2d03-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="c2d03-256">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2d03-256">Description</span></span>
<span data-ttu-id="c2d03-257">Usando Olá [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) classe para projetos, como o site do Azure e serviços móveis do Azure não apresentam problemas de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="c2d03-257">Using hello [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="c2d03-258">Como prática recomendada, no entanto, é uma boa ideia toouse nuvem[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) como uma forma unificada de gerenciamento de configurações para todos os aplicativos de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2d03-258">As a best practice, however, it's a good idea toouse Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="c2d03-259">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="c2d03-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="c2d03-260">Motivo</span><span class="sxs-lookup"><span data-stu-id="c2d03-260">Reason</span></span>
<span data-ttu-id="c2d03-261">CloudConfigurationManager lê o ambiente de aplicativo hello configuração arquivo toohello apropriado.</span><span class="sxs-lookup"><span data-stu-id="c2d03-261">CloudConfigurationManager reads hello configuration file appropriate toohello application environment.</span></span>

[<span data-ttu-id="c2d03-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="c2d03-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="c2d03-263">Solução</span><span class="sxs-lookup"><span data-stu-id="c2d03-263">Solution</span></span>
<span data-ttu-id="c2d03-264">Refatorar o hello toouse de código [CloudConfigurationManager classe](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="c2d03-264">Refactor your code toouse hello [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="c2d03-265">Um código para corrigir esse problema é fornecido pela ferramenta de análise de código do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="c2d03-265">A code fix for this issue is provided by hello Azure Code Analysis tool.</span></span>

<span data-ttu-id="c2d03-266">saudação de trecho de código a seguir demonstra Olá código para corrigir esse problema.</span><span class="sxs-lookup"><span data-stu-id="c2d03-266">hello following code snippet demonstrates hello code fix for this issue.</span></span> <span data-ttu-id="c2d03-267">Substitua</span><span class="sxs-lookup"><span data-stu-id="c2d03-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="c2d03-268">por:</span><span class="sxs-lookup"><span data-stu-id="c2d03-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="c2d03-269">Aqui está um exemplo de como toostore Olá configuração em um arquivo App. config ou Web. config.</span><span class="sxs-lookup"><span data-stu-id="c2d03-269">Here's an example of how toostore hello configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="c2d03-270">Adicione seção appSettings do hello configurações toohello saudação do arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="c2d03-270">Add hello settings toohello appSettings section of hello configuration file.</span></span> <span data-ttu-id="c2d03-271">seguir Olá é Olá Web. config arquivo exemplo de código anterior hello.</span><span class="sxs-lookup"><span data-stu-id="c2d03-271">hello following is hello Web.config file for hello previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="c2d03-272">Evitar o uso de cadeias de conexão embutidas em código</span><span class="sxs-lookup"><span data-stu-id="c2d03-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="c2d03-273">ID</span><span class="sxs-lookup"><span data-stu-id="c2d03-273">ID</span></span>
<span data-ttu-id="c2d03-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="c2d03-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="c2d03-275">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2d03-275">Description</span></span>
<span data-ttu-id="c2d03-276">Se você usar cadeias de caracteres de conexão embutidas e você precisa tooupdate-los mais tarde, você será toomake alterações tooyour código-fonte e recompilar o aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="c2d03-276">If you use hard-coded connection strings and you need tooupdate them later, you’ll have toomake changes tooyour source code and recompile hello application.</span></span> <span data-ttu-id="c2d03-277">No entanto, se você armazenar suas cadeias de caracteres de conexão em um arquivo de configuração, você pode alterá-las posteriormente ao simplesmente atualizar o arquivo de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2d03-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating hello configuration file.</span></span>

<span data-ttu-id="c2d03-278">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="c2d03-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="c2d03-279">Motivo</span><span class="sxs-lookup"><span data-stu-id="c2d03-279">Reason</span></span>
<span data-ttu-id="c2d03-280">Codificar cadeias de caracteres de conexão é uma prática inadequada porque ele apresenta problemas quando precisam de cadeias de caracteres de conexão toobe alterada rapidamente.</span><span class="sxs-lookup"><span data-stu-id="c2d03-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need toobe changed quickly.</span></span> <span data-ttu-id="c2d03-281">Além disso, se o projeto de saudação precisa toobe check-in de controle de toosource, cadeias de caracteres de conexão embutidas introduzem vulnerabilidades de segurança, como cadeias de caracteres de saudação podem ser exibidas no código-fonte hello.</span><span class="sxs-lookup"><span data-stu-id="c2d03-281">In addition, if hello project needs toobe checked in toosource control, hard-coded connection strings introduce security vulnerabilities since hello strings can be viewed in hello source code.</span></span>

### <a name="solution"></a><span data-ttu-id="c2d03-282">Solução</span><span class="sxs-lookup"><span data-stu-id="c2d03-282">Solution</span></span>
<span data-ttu-id="c2d03-283">Armazenar cadeias de caracteres de conexão em arquivos de configuração de saudação ou ambientes do Azure.</span><span class="sxs-lookup"><span data-stu-id="c2d03-283">Store connection strings in hello configuration files or Azure environments.</span></span>

* <span data-ttu-id="c2d03-284">Para aplicativos autônomos, use as configurações de cadeia de caracteres de conexão de toostore App. config.</span><span class="sxs-lookup"><span data-stu-id="c2d03-284">For standalone applications, use app.config toostore connection string settings.</span></span>
* <span data-ttu-id="c2d03-285">Para aplicativos web hospedados no IIS, use cadeias de caracteres de conexão de toostore Web. config.</span><span class="sxs-lookup"><span data-stu-id="c2d03-285">For IIS-hosted web applications, use web.config toostore connection strings.</span></span>
* <span data-ttu-id="c2d03-286">Para aplicativos do ASP.NET vNext, use cadeias de caracteres de conexão do configuration.json toostore.</span><span class="sxs-lookup"><span data-stu-id="c2d03-286">For ASP.NET vNext applications, use configuration.json toostore connection strings.</span></span>

<span data-ttu-id="c2d03-287">Para obter informações sobre como usar arquivos de configurações, como web.config ou app.config, consulte [Diretrizes de configuração Web do ASP.NET](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span><span class="sxs-lookup"><span data-stu-id="c2d03-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="c2d03-288">Para obter informações sobre como variáveis de ambiente do Azure funcionam, consulte [Sites do Azure: como as cadeias de aplicativo e cadeias de conexão funcionam](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="c2d03-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="c2d03-289">Para obter informações sobre o armazenamento de cadeia de conexão no controle do código-fonte, consulte [Evitar colocar informações confidenciais, como cadeias de conexão em arquivos armazenados no repositório de código-fonte](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span><span class="sxs-lookup"><span data-stu-id="c2d03-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="c2d03-290">Usar arquivo de configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="c2d03-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="c2d03-291">ID</span><span class="sxs-lookup"><span data-stu-id="c2d03-291">ID</span></span>
<span data-ttu-id="c2d03-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="c2d03-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="c2d03-293">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2d03-293">Description</span></span>
<span data-ttu-id="c2d03-294">Em vez de configurar as configurações de diagnóstico em seu código, como usando Olá Microsoft.WindowsAzure.Diagnostics API de programação, você deve configurar as configurações de diagnóstico no arquivo Diagnostics wadcfg hello.</span><span class="sxs-lookup"><span data-stu-id="c2d03-294">Instead of configuring diagnostics settings in your code such as by using hello Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in hello diagnostics.wadcfg file.</span></span> <span data-ttu-id="c2d03-295">(Ou diagnostics.wadcfgx se você usar o SDK 2.5 do Azure).</span><span class="sxs-lookup"><span data-stu-id="c2d03-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="c2d03-296">Ao fazer isso, você pode alterar as configurações de diagnóstico sem ter que toorecompile seu código.</span><span class="sxs-lookup"><span data-stu-id="c2d03-296">By doing this, you can change diagnostics settings without having toorecompile your code.</span></span>

<span data-ttu-id="c2d03-297">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="c2d03-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="c2d03-298">Motivo</span><span class="sxs-lookup"><span data-stu-id="c2d03-298">Reason</span></span>
<span data-ttu-id="c2d03-299">2.5 do SDK do Azure (que usa o diagnóstico do Azure 1.3), o diagnóstico do Azure (WAD) podem ser configurados usando vários métodos diferentes: adicionando-blob de configuração toohello no armazenamento, usando o código obrigatório, configuração declarativa ou padrão de saudação configuração.</span><span class="sxs-lookup"><span data-stu-id="c2d03-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it toohello configuration blob in storage, by using imperative code, declarative configuration, or hello default configuration.</span></span> <span data-ttu-id="c2d03-300">No entanto, Olá preferencial maneira tooconfigure diagnóstico é toouse um arquivo de configuração XML (Diagnostics. wadcfg ou diagnositcs.wadcfgx SDK 2.5 e posterior) no projeto de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="c2d03-300">However, hello preferred way tooconfigure diagnostics is toouse an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in hello application project.</span></span> <span data-ttu-id="c2d03-301">Nessa abordagem, arquivo Diagnostics wadcfg Olá completamente define a configuração de saudação e seja atualizado e reimplantado à vontade.</span><span class="sxs-lookup"><span data-stu-id="c2d03-301">In this approach, hello diagnostics.wadcfg file completely defines hello configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="c2d03-302">Combinação de uso Olá Olá wadcfg do arquivo de configuração com hello métodos programáticos de definir as configurações usando Olá [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)ou [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) classes podem gerar tooconfusion.</span><span class="sxs-lookup"><span data-stu-id="c2d03-302">Mixing hello use of hello diagnostics.wadcfg configuration file with hello programmatic methods of setting configurations by using hello [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead tooconfusion.</span></span> <span data-ttu-id="c2d03-303">Consulte [Inicializar ou alterar configuração de diagnóstico do Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="c2d03-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="c2d03-304">A partir do WAD 1.3 (incluído no Azure SDK 2.5), já não diagnóstico de tooconfigure código toouse possíveis.</span><span class="sxs-lookup"><span data-stu-id="c2d03-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible toouse code tooconfigure diagnostics.</span></span> <span data-ttu-id="c2d03-305">Como resultado, você pode fornecer configuração Olá ao aplicar ou atualizar a extensão de diagnóstico de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2d03-305">As a result, you can only provide hello configuration when applying or updating hello diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="c2d03-306">Solução</span><span class="sxs-lookup"><span data-stu-id="c2d03-306">Solution</span></span>
<span data-ttu-id="c2d03-307">Use Olá diagnóstico designer toomove configurações de diagnóstico toohello diagnóstico configuração arquivo de configuração (diagnositcs.wadcfg ou diagnositcs.wadcfgx SDK 2.5 e posterior).</span><span class="sxs-lookup"><span data-stu-id="c2d03-307">Use hello diagnostics configuration designer toomove diagnostic settings toohello diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="c2d03-308">Também é recomendável que você instale [2.5 do SDK do Azure](http://go.microsoft.com/fwlink/?LinkId=513188) e usar o recurso de diagnóstico hello mais recente.</span><span class="sxs-lookup"><span data-stu-id="c2d03-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use hello latest diagnostics feature.</span></span>

1. <span data-ttu-id="c2d03-309">No menu de atalho Olá para função hello que você deseja tooconfigure, escolha Propriedades e, em seguida, escolha a guia de configuração de saudação.</span><span class="sxs-lookup"><span data-stu-id="c2d03-309">On hello shortcut menu for hello role that you want tooconfigure, choose Properties, and then choose hello Configuration tab.</span></span>
2. <span data-ttu-id="c2d03-310">Em Olá **diagnóstico** seção, certifique-se de que Olá **habilitar o diagnóstico** caixa de seleção é marcada.</span><span class="sxs-lookup"><span data-stu-id="c2d03-310">In hello **Diagnostics** section, make sure that hello **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="c2d03-311">Escolha Olá **configurar** botão.</span><span class="sxs-lookup"><span data-stu-id="c2d03-311">Choose hello **Configure** button.</span></span>

   ![Acessando a opção de habilitar o diagnóstico Olá](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="c2d03-313">Consulte [Configurando o diagnóstico para os serviços de nuvem do Azure e máquinas virtuais](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="c2d03-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="c2d03-314">Evitar declarar objetos DbContext como estáticos</span><span class="sxs-lookup"><span data-stu-id="c2d03-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="c2d03-315">ID</span><span class="sxs-lookup"><span data-stu-id="c2d03-315">ID</span></span>
<span data-ttu-id="c2d03-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="c2d03-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="c2d03-317">Descrição</span><span class="sxs-lookup"><span data-stu-id="c2d03-317">Description</span></span>
<span data-ttu-id="c2d03-318">memória toosave, evite declarando objetos DBContext como estático.</span><span class="sxs-lookup"><span data-stu-id="c2d03-318">toosave memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="c2d03-319">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="c2d03-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="c2d03-320">Motivo</span><span class="sxs-lookup"><span data-stu-id="c2d03-320">Reason</span></span>
<span data-ttu-id="c2d03-321">Objetos de DBContext mantêm Olá resultados da consulta de cada chamada.</span><span class="sxs-lookup"><span data-stu-id="c2d03-321">DBContext objects hold hello query results from each call.</span></span> <span data-ttu-id="c2d03-322">Objetos de DBContext estáticos não são descartados até que o domínio de aplicativo hello é descarregado.</span><span class="sxs-lookup"><span data-stu-id="c2d03-322">Static DBContext objects are not disposed until hello application domain is unloaded.</span></span> <span data-ttu-id="c2d03-323">Portanto, um objeto DBContext estático pode consumir grandes quantidades de memória.</span><span class="sxs-lookup"><span data-stu-id="c2d03-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="c2d03-324">Solução</span><span class="sxs-lookup"><span data-stu-id="c2d03-324">Solution</span></span>
<span data-ttu-id="c2d03-325">Declare DBContext como uma variável local ou um campo de instância não estático, use-o para uma tarefa e deixe-o ser descartado após o uso.</span><span class="sxs-lookup"><span data-stu-id="c2d03-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="c2d03-326">saudação de classe do controlador MVC exemplo a seguir mostra como toouse Olá objeto DBContext.</span><span class="sxs-lookup"><span data-stu-id="c2d03-326">hello following example MVC controller class shows how toouse hello DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass tooDbContext        
        private BloggingContext db = new BloggingContext();
        // GET: Blogs
        public ActionResult Index()
        {
            //business logics…
            return View();
        }
        protected override void Dispose(bool disposing)
        {
            if (disposing)
            {
                db.Dispose();
            }
            base.Dispose(disposing);
        }
    }
```

## <a name="next-steps"></a><span data-ttu-id="c2d03-327">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c2d03-327">Next steps</span></span>
<span data-ttu-id="c2d03-328">toolearn mais sobre a otimização e Solucionando problemas de aplicativos do Azure, consulte [solucionar problemas de um aplicativo web no serviço de aplicativo do Azure usando o Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="c2d03-328">toolearn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
