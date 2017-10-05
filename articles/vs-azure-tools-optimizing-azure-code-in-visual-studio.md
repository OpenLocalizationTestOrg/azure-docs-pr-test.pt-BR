---
title: "Otimizando o código do Azure no Visual Studio | Microsoft Docs"
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
ms.openlocfilehash: 8f145502a856798d6e69ac11f324c72fa23f938e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="optimizing-your-azure-code"></a><span data-ttu-id="ac7e2-103">Otimizando o código do Azure</span><span class="sxs-lookup"><span data-stu-id="ac7e2-103">Optimizing Your Azure Code</span></span>
<span data-ttu-id="ac7e2-104">Quando você está programando aplicativos que usam o Microsoft Azure, existem algumas práticas de codificação que você deve seguir para ajudar a evitar problemas de escalabilidade, comportamento e desempenho do aplicativo em um ambiente de nuvem.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-104">When you’re programming apps that use Microsoft Azure, there are some coding practices you should follow to help avoid problems with app scalability, behavior and performance in a cloud environment.</span></span> <span data-ttu-id="ac7e2-105">A Microsoft fornece uma ferramenta de análise de código do Azure que reconhece e identifica vários desses problemas comumente encontrados e ajuda a resolvê-los.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-105">Microsoft provides an Azure Code Analysis tool that recognizes and identifies several of these commonly-encountered issues and helps you resolve them.</span></span> <span data-ttu-id="ac7e2-106">Você pode baixar a ferramenta no Visual Studio, via NuGet.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-106">You can download the tool in Visual Studio via NuGet.</span></span>

## <a name="azure-code-analysis-rules"></a><span data-ttu-id="ac7e2-107">Regras de análise de código do Azure</span><span class="sxs-lookup"><span data-stu-id="ac7e2-107">Azure Code Analysis rules</span></span>
<span data-ttu-id="ac7e2-108">A ferramenta de análise de código do Azure usa as seguintes regras para sinalizar automaticamente seu código do Azure quando encontra problemas conhecidos de impacto no desempenho.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-108">The Azure Code Analysis tool uses the following rules to automatically flag your Azure code when it finds known performance-impacting issues.</span></span> <span data-ttu-id="ac7e2-109">Os problemas detectados aparecem como avisos ou erros do compilador.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-109">Detected issues appear as a warnings or compiler errors.</span></span> <span data-ttu-id="ac7e2-110">Correções de código ou sugestões para resolver o erro ou aviso geralmente são fornecidos por meio de um ícone de lâmpada.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-110">Code fixes or suggestions to resolve the warning or error are often provided through a light bulb icon.</span></span>

## <a name="avoid-using-default-in-process-session-state-mode"></a><span data-ttu-id="ac7e2-111">Evitar o uso do modo de estado de sessão padrão (em processo)</span><span class="sxs-lookup"><span data-stu-id="ac7e2-111">Avoid using default (in-process) session state mode</span></span>
### <a name="id"></a><span data-ttu-id="ac7e2-112">ID</span><span class="sxs-lookup"><span data-stu-id="ac7e2-112">ID</span></span>
<span data-ttu-id="ac7e2-113">AP0000</span><span class="sxs-lookup"><span data-stu-id="ac7e2-113">AP0000</span></span>

### <a name="description"></a><span data-ttu-id="ac7e2-114">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac7e2-114">Description</span></span>
<span data-ttu-id="ac7e2-115">Se você usar o modo de estado de sessão padrão (em processo) para aplicativos em nuvem, poderá perder o estado da sessão.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-115">If you use the default (in-process) session state mode for cloud applications, you can lose session state.</span></span>

<span data-ttu-id="ac7e2-116">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-116">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="ac7e2-117">Motivo</span><span class="sxs-lookup"><span data-stu-id="ac7e2-117">Reason</span></span>
<span data-ttu-id="ac7e2-118">Por padrão, o modo de estado de sessão especificado no arquivo web.config está em processo.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-118">By default, the session state mode specified in the web.config file is in-process.</span></span> <span data-ttu-id="ac7e2-119">Além disso, se nenhuma entrada for especificada no arquivo de configuração, o modo de estado de sessão assume o padrão de em processo.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-119">Also, if no entry specified in the configuration file, the Session State mode defaults to in-process.</span></span> <span data-ttu-id="ac7e2-120">O modo em processo armazena o estado de sessão na memória, no servidor Web.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-120">The in-process mode stores session state in memory on the web server.</span></span> <span data-ttu-id="ac7e2-121">Quando uma instância é reiniciada ou uma nova instância é usada para balanceamento de carga ou suporte a failover, o estado de sessão armazenado na memória no servidor Web não é salvo.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-121">When an instance is restarted or a new instance is used for load balancing or failover support, the session state stored in memory on the web server isn’t saved.</span></span> <span data-ttu-id="ac7e2-122">Essa situação impede que o aplicativo seja escalonável na nuvem.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-122">This situation prevents the application from being scalable on the cloud.</span></span>

<span data-ttu-id="ac7e2-123">O estado da sessão ASP.NET dá suporte a várias opções diferentes de armazenamento para dados de estado de sessão: InProc, StateServer, SQLServer, Personalizado e Desativado.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-123">ASP.NET session state supports several different storage options for session state data: InProc, StateServer, SQLServer, Custom, and Off.</span></span> <span data-ttu-id="ac7e2-124">É recomendável que você use o modo Personalizado para hospedar dados em um armazenamento de estado da sessão externo, como [Provedor de estado de sessão do Azure para Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-124">It’s recommended that you use Custom mode to host data on an external Session State store, such as [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521).</span></span>

### <a name="solution"></a><span data-ttu-id="ac7e2-125">Solução</span><span class="sxs-lookup"><span data-stu-id="ac7e2-125">Solution</span></span>
<span data-ttu-id="ac7e2-126">É uma solução recomendada armazenar o estado de sessão em um serviço de cache gerenciado.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-126">One recommended solution is to store session state on a managed cache service.</span></span> <span data-ttu-id="ac7e2-127">Saiba como usar [provedor de Estado de Sessão do Azure para Redis](http://go.microsoft.com/fwlink/?LinkId=401521) para armazenar o estado de sessão.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-127">Learn how to use [Azure Session State provider for Redis](http://go.microsoft.com/fwlink/?LinkId=401521) to store your session state.</span></span> <span data-ttu-id="ac7e2-128">Você também pode armazenar o estado de sessão em outros locais para garantir que seu aplicativo seja escalonável na nuvem.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-128">You can also store session state in other places to ensure your application is scalable on the cloud.</span></span> <span data-ttu-id="ac7e2-129">Para saber mais sobre as soluções alternativas, leia [Modos de estado de sessão](https://msdn.microsoft.com/library/ms178586).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-129">To learn more about alternative solutions please read [Session State Modes](https://msdn.microsoft.com/library/ms178586).</span></span>

## <a name="run-method-should-not-be-async"></a><span data-ttu-id="ac7e2-130">O método de execução não deve ser assíncrono</span><span class="sxs-lookup"><span data-stu-id="ac7e2-130">Run method should not be async</span></span>
### <a name="id"></a><span data-ttu-id="ac7e2-131">ID</span><span class="sxs-lookup"><span data-stu-id="ac7e2-131">ID</span></span>
<span data-ttu-id="ac7e2-132">AP1000</span><span class="sxs-lookup"><span data-stu-id="ac7e2-132">AP1000</span></span>

### <a name="description"></a><span data-ttu-id="ac7e2-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac7e2-133">Description</span></span>
<span data-ttu-id="ac7e2-134">Crie métodos assíncronos (como [await](https://msdn.microsoft.com/library/hh156528.aspx)) fora do método [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) e, em seguida, chamar os métodos assíncronos de [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-134">Create asynchronous methods (such as [await](https://msdn.microsoft.com/library/hh156528.aspx)) outside of the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and then call the async methods from [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx).</span></span> <span data-ttu-id="ac7e2-135">A declaração do método [[Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) como assíncrono faz com que a função de trabalho insira um loop de reinicialização.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-135">Declaring the [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method as async causes the worker role to enter a restart loop.</span></span>

<span data-ttu-id="ac7e2-136">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-136">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="ac7e2-137">Motivo</span><span class="sxs-lookup"><span data-stu-id="ac7e2-137">Reason</span></span>
<span data-ttu-id="ac7e2-138">A chamada de métodos assíncronos dentro do método [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) método faz com que o tempo de execução do serviço de nuvem recicle a função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-138">Calling async methods inside the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes the cloud service runtime to recycle the worker role.</span></span> <span data-ttu-id="ac7e2-139">Quando uma função de trabalho é iniciada, todas as execuções do programa ocorrem dentro do método [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ac7e2-139">When a worker role starts, all program execution takes place inside the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="ac7e2-140">Sair do método [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) faz com que a função de trabalho reinicie.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-140">Exiting the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method causes the worker role to restart.</span></span> <span data-ttu-id="ac7e2-141">Quando o tempo de execução da função de trabalho atinge o método assíncrono, ele envia todas as operações posteriores ao método assíncrono e retorna.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-141">When the worker role runtime hits the async method, it dispatches all operations after the async method and then returns.</span></span> <span data-ttu-id="ac7e2-142">Isso faz com que a função de trabalho saia do método [[[[Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) e reinicialize.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-142">This causes the worker role to exit from the [[[[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method and restart.</span></span> <span data-ttu-id="ac7e2-143">Na próxima iteração da execução, a função de trabalho atinge o método assíncrono novamente e reinicia, fazendo com que a função de trabalho seja reciclada novamente.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-143">In the next iteration of execution, the worker role hits the async method again and restarts, causing the worker role to recycle again as well.</span></span>

### <a name="solution"></a><span data-ttu-id="ac7e2-144">Solução</span><span class="sxs-lookup"><span data-stu-id="ac7e2-144">Solution</span></span>
<span data-ttu-id="ac7e2-145">Coloque todas as operações assíncronas fora do método [Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) .</span><span class="sxs-lookup"><span data-stu-id="ac7e2-145">Place all async operations outside of the [Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method.</span></span> <span data-ttu-id="ac7e2-146">Chame o método async refatorado de dentro do método [[Run ()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) , como RunAsync().wait.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-146">Then, call the refactored async method from inside the [[Run()](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx)](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx) method, such as RunAsync().wait.</span></span> <span data-ttu-id="ac7e2-147">A ferramenta de análise de código do Azure pode ajudá-lo a corrigir esse problema.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-147">The Azure Code Analysis tool can help you fix this issue.</span></span>

<span data-ttu-id="ac7e2-148">O trecho de código a seguir demonstra a correção de código para esse problema:</span><span class="sxs-lookup"><span data-stu-id="ac7e2-148">The following code snippet demonstrates the code fix for this issue:</span></span>

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

## <a name="use-service-bus-shared-access-signature-authentication"></a><span data-ttu-id="ac7e2-149">Autenticação de assinatura de acesso compartilhado com barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="ac7e2-149">Use Service Bus Shared Access Signature authentication</span></span>
### <a name="id"></a><span data-ttu-id="ac7e2-150">ID</span><span class="sxs-lookup"><span data-stu-id="ac7e2-150">ID</span></span>
<span data-ttu-id="ac7e2-151">AP2000</span><span class="sxs-lookup"><span data-stu-id="ac7e2-151">AP2000</span></span>

### <a name="description"></a><span data-ttu-id="ac7e2-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac7e2-152">Description</span></span>
<span data-ttu-id="ac7e2-153">Use SAS (Assinatura de Acesso Compartilhado) para autenticação.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-153">Use Shared Access Signature (SAS) for authentication.</span></span> <span data-ttu-id="ac7e2-154">ACS (Serviço de Controle de Acesso) está sendo preterido para autenticação do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-154">Access Control Service (ACS) is being deprecated for service bus authentication.</span></span>

<span data-ttu-id="ac7e2-155">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-155">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="ac7e2-156">Motivo</span><span class="sxs-lookup"><span data-stu-id="ac7e2-156">Reason</span></span>
<span data-ttu-id="ac7e2-157">Para mais segurança, o Active Directory do Azure está substituindo a autenticação do ACS pela autenticação SAS.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-157">For enhanced security, Azure Active Directory is replacing ACS authentication with SAS authentication.</span></span> <span data-ttu-id="ac7e2-158">Consulte [Active Directory do Azure é o futuro do ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) para obter informações sobre o plano de transição.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-158">See [Azure Active Directory is the future of ACS](http://blogs.technet.com/b/ad/archive/2013/06/22/azure-active-directory-is-the-future-of-acs.aspx) for information on the transition plan.</span></span>

### <a name="solution"></a><span data-ttu-id="ac7e2-159">Solução</span><span class="sxs-lookup"><span data-stu-id="ac7e2-159">Solution</span></span>
<span data-ttu-id="ac7e2-160">Use autenticação de SAS em seus aplicativos.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-160">Use SAS authentication in your apps.</span></span> <span data-ttu-id="ac7e2-161">O exemplo a seguir mostra como usar um token SAS existente para acessar um namespace do barramento de serviço ou uma entidade.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-161">The following example shows how to use an existing SAS token to access a service bus namespace or entity.</span></span>

```
MessagingFactory listenMF = MessagingFactory.Create(endpoints, new StaticSASTokenProvider(subscriptionToken));
SubscriptionClient sc = listenMF.CreateSubscriptionClient(topicPath, subscriptionName);
BrokeredMessage receivedMessage = sc.Receive();
```

<span data-ttu-id="ac7e2-162">Para obter mais informações, consulte os tópicos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-162">See the following topics for more information.</span></span>

* <span data-ttu-id="ac7e2-163">Para uma visão geral, consulte [Autenticação de assinatura de acesso compartilhado com barramento de serviço](https://msdn.microsoft.com/library/dn170477.aspx)</span><span class="sxs-lookup"><span data-stu-id="ac7e2-163">For an overview, see [Shared Access Signature Authentication with Service Bus](https://msdn.microsoft.com/library/dn170477.aspx)</span></span>
* [<span data-ttu-id="ac7e2-164">Como usar a autenticação de assinatura de acesso compartilhado com barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="ac7e2-164">How to use Shared Access Signature Authentication with Service Bus</span></span>](https://msdn.microsoft.com/library/dn205161.aspx)
* <span data-ttu-id="ac7e2-165">Para um projeto de exemplo, consulte [Usando SAS (Assinatura de Acesso Compartilhado) com assinaturas do barramento de serviço](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span><span class="sxs-lookup"><span data-stu-id="ac7e2-165">For a sample project, see [Using Shared Access Signature (SAS) authentication with Service Bus Subscriptions](http://code.msdn.microsoft.com/windowsazure/Using-Shared-Access-e605b37c)</span></span>

## <a name="consider-using-onmessage-method-to-avoid-receive-loop"></a><span data-ttu-id="ac7e2-166">Considerar o uso do método OnMessage para evitar "loop de recebimento"</span><span class="sxs-lookup"><span data-stu-id="ac7e2-166">Consider using OnMessage method to avoid "receive loop"</span></span>
### <a name="id"></a><span data-ttu-id="ac7e2-167">ID</span><span class="sxs-lookup"><span data-stu-id="ac7e2-167">ID</span></span>
<span data-ttu-id="ac7e2-168">AP2002</span><span class="sxs-lookup"><span data-stu-id="ac7e2-168">AP2002</span></span>

### <a name="description"></a><span data-ttu-id="ac7e2-169">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac7e2-169">Description</span></span>
<span data-ttu-id="ac7e2-170">Para evitar o início de um "loop de recebimento" a chamada ao método **OnMessage** é a melhor solução para receber mensagens do que chamar o método **Receive**.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-170">To avoid going into a "receive loop," calling the **OnMessage** method is a better solution for receiving messages than calling the **Receive** method.</span></span> <span data-ttu-id="ac7e2-171">No entanto, se você deve usar o método **Receive** e especificar um tempo de espera de servidor não padrão, verifique se o tempo de espera do servidor é mais de um minuto.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-171">However, if you must use the **Receive** method, and you specify a non-default server wait time, make sure the server wait time is more than one minute.</span></span>

<span data-ttu-id="ac7e2-172">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-172">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="ac7e2-173">Motivo</span><span class="sxs-lookup"><span data-stu-id="ac7e2-173">Reason</span></span>
<span data-ttu-id="ac7e2-174">Ao chamar **OnMessage**, o cliente inicia uma bomba de mensagens internas que monitora constantemente a fila ou assinatura.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-174">When calling **OnMessage**, the client starts an internal message pump that constantly polls the queue or subscription.</span></span> <span data-ttu-id="ac7e2-175">Essa bomba de mensagens contém um loop infinito que emite uma chamada para receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-175">This message pump contains an infinite loop that issues a call to receive messages.</span></span> <span data-ttu-id="ac7e2-176">Se a chamada alcançar o tempo limite, ele emitirá uma nova chamada.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-176">If the call times out, it issues a new call.</span></span> <span data-ttu-id="ac7e2-177">O intervalo de tempo limite é determinado pelo valor da propriedade [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) do [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx) que está sendo usado.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-177">The timeout interval is determined by the value of the [OperationTimeout](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactorysettings.operationtimeout.aspx) property of the [MessagingFactory](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.messagingfactory.aspx)that’s being used.</span></span>

<span data-ttu-id="ac7e2-178">A vantagem de usar o **OnMessage** em comparação com **Receive** é que os usuários não precisarão manualmente pesquisar mensagens, manipular exceções, processar várias mensagens em paralelo e concluir mensagens.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-178">The advantage of using **OnMessage** compared to **Receive** is that users don’t have to manually poll for messages, handle exceptions, process multiple messages in parallel, and complete the messages.</span></span>

<span data-ttu-id="ac7e2-179">Se você chamar **Receive** sem usar o valor padrão, não se esqueça que o valor de *ServerWaitTime* é a mais de um minuto.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-179">If you call **Receive** without using its default value, be sure the *ServerWaitTime* value is more than one minute.</span></span> <span data-ttu-id="ac7e2-180">A definição de *ServerWaitTime* para mais de um minuto impede que o servidor alcance o tempo limite antes que a mensagem seja recebida totalmente.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-180">Setting *ServerWaitTime* to more than one minute prevents the server from timing out before the message is fully received.</span></span>

### <a name="solution"></a><span data-ttu-id="ac7e2-181">Solução</span><span class="sxs-lookup"><span data-stu-id="ac7e2-181">Solution</span></span>
<span data-ttu-id="ac7e2-182">Consulte exemplos de código a seguir para usos recomendados.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-182">Please see the following code examples for recommended usages.</span></span> <span data-ttu-id="ac7e2-183">Para obter mais detalhes, consulte o método [QueueClient.OnMessage (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx) e o método [QueueClient.Receive (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-183">For more details, see [QueueClient.OnMessage Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.onmessage.aspx)and [QueueClient.Receive Method (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.receive.aspx).</span></span>

<span data-ttu-id="ac7e2-184">Para melhorar o desempenho da infraestrutura de mensagens do Azure, consulte o padrão de design [Prévia de mensagens assíncronas](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-184">To improve the performance of the Azure messaging infrastructure, see the design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

<span data-ttu-id="ac7e2-185">A seguir, um exemplo de uso de **OnMessage** para receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-185">The following is an example of using **OnMessage** to receive messages.</span></span>

```
void ReceiveMessages()
{
    // Initialize message pump options.
    OnMessageOptions options = new OnMessageOptions();
    options.AutoComplete = true; // Indicates if the message-pump should call complete on messages after the callback has completed processing.
    options.MaxConcurrentCalls = 1; // Indicates the maximum number of concurrent calls to the callback the pump should initiate.
    options.ExceptionReceived += LogErrors; // Enables you to get notified of any errors encountered by the message pump.

    // Start receiving messages.
    QueueClient client = QueueClient.Create("myQueue");
    client.OnMessage((receivedMessage) => // Initiates the message pump and callback is invoked for each message that is recieved, calling close on the client will stop the pump.
    {
        // Process the message.
    }, options);
    Console.WriteLine("Press any key to exit.");
    Console.ReadKey();
```

<span data-ttu-id="ac7e2-186">A seguir, um exemplo de uso de **Receive** com o tempo de espera de servidor padrão.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-186">The following is an example of using **Receive** with the default server wait time.</span></span>

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

<span data-ttu-id="ac7e2-187">A seguir, um exemplo de uso de **Receive** com o tempo de espera de servidor não padrão.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-187">The following is an example of using **Receive** with a non-default server wait time.</span></span>

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
## <a name="consider-using-asynchronous-service-bus-methods"></a><span data-ttu-id="ac7e2-188">Considere o uso de métodos assíncronos de barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="ac7e2-188">Consider using asynchronous Service Bus methods</span></span>
### <a name="id"></a><span data-ttu-id="ac7e2-189">ID</span><span class="sxs-lookup"><span data-stu-id="ac7e2-189">ID</span></span>
<span data-ttu-id="ac7e2-190">AP2003</span><span class="sxs-lookup"><span data-stu-id="ac7e2-190">AP2003</span></span>

### <a name="description"></a><span data-ttu-id="ac7e2-191">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac7e2-191">Description</span></span>
<span data-ttu-id="ac7e2-192">Use os métodos assíncronos do barramento de serviço para melhorar o desempenho com sistema de mensagens agenciado.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-192">Use asynchronous Service Bus methods to improve performance with brokered messaging.</span></span>

<span data-ttu-id="ac7e2-193">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-193">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="ac7e2-194">Motivo</span><span class="sxs-lookup"><span data-stu-id="ac7e2-194">Reason</span></span>
<span data-ttu-id="ac7e2-195">O uso de métodos assíncronos permite a simultaneidade do programa aplicativo porque a execução de cada chamada não bloqueia o thread principal.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-195">Using asynchronous methods enables application program concurrency because executing each call doesn’t block the main thread.</span></span> <span data-ttu-id="ac7e2-196">Ao usar os métodos de mensagens do Barramento de Serviço, a execução de uma operação (enviar, receber, excluir, etc.) leva tempo.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-196">When using Service Bus messaging methods, performing an operation (send, receive, delete, etc.) takes time.</span></span> <span data-ttu-id="ac7e2-197">Esse tempo inclui o processamento da operação pelo serviço do barramento de serviço, além da latência da solicitação e resposta.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-197">This time includes the processing of the operation by the Service Bus service in addition to the latency of the request and the reply.</span></span> <span data-ttu-id="ac7e2-198">Para aumentar o número de operações por hora, elas devem ser executadas simultaneamente.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-198">To increase the number of operations per time, operations must execute concurrently.</span></span> <span data-ttu-id="ac7e2-199">Para obter mais informações, consulte [Práticas recomendadas para melhorias de desempenho usando o sistema de mensagens agenciado do Barramento de Serviço](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-199">For more information please refer to [Best Practices for Performance Improvements Using Service Bus Brokered Messaging](https://msdn.microsoft.com/library/azure/hh528527.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="ac7e2-200">Solução</span><span class="sxs-lookup"><span data-stu-id="ac7e2-200">Solution</span></span>
<span data-ttu-id="ac7e2-201">Consulte [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) para obter informações sobre como usar o método assíncrono recomendado.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-201">See [QueueClient Class (Microsoft.ServiceBus.Messaging)](https://msdn.microsoft.com/library/microsoft.servicebus.messaging.queueclient.aspx) for information about how to use the recommended asynchronous method.</span></span>

<span data-ttu-id="ac7e2-202">Para melhorar o desempenho da infraestrutura de mensagens do Azure, consulte o padrão de design [Prévia de mensagens assíncronas](https://msdn.microsoft.com/library/dn589781.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-202">To improve the performance of the Azure messaging infrastructure, see the design pattern [Asynchronous Messaging Primer](https://msdn.microsoft.com/library/dn589781.aspx).</span></span>

## <a name="consider-partitioning-service-bus-queues-and-topics"></a><span data-ttu-id="ac7e2-203">Considerar o particionamento de tópicos e filas do barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="ac7e2-203">Consider partitioning Service Bus queues and topics</span></span>
### <a name="id"></a><span data-ttu-id="ac7e2-204">ID</span><span class="sxs-lookup"><span data-stu-id="ac7e2-204">ID</span></span>
<span data-ttu-id="ac7e2-205">AP2004</span><span class="sxs-lookup"><span data-stu-id="ac7e2-205">AP2004</span></span>

### <a name="description"></a><span data-ttu-id="ac7e2-206">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac7e2-206">Description</span></span>
<span data-ttu-id="ac7e2-207">Particione filas e tópicos do barramento de serviço para um melhor desempenho com as mensagens do barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-207">Partition Service Bus queues and topics for better performance with Service Bus messaging.</span></span>

<span data-ttu-id="ac7e2-208">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-208">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="ac7e2-209">Motivo</span><span class="sxs-lookup"><span data-stu-id="ac7e2-209">Reason</span></span>
<span data-ttu-id="ac7e2-210">O particionamento de tópicos e filas do barramento de serviço aumenta a taxa de transferência do desempenho e a disponibilidade do serviço porque a taxa de transferência geral de uma fila ou tópico particionado não é mais limitada pelo desempenho de um único agente ou repositório de mensagens.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-210">Partitioning Service Bus queues and topics increases performance throughput and service availability because the overall throughput of a partitioned queue or topic is no longer limited by the performance of a single message broker or messaging store.</span></span> <span data-ttu-id="ac7e2-211">Além disso, uma falha temporária de um repositório de mensagens não torna uma fila ou tópico particionado indisponível.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-211">In addition, a temporary outage of a messaging store doesn’t make a partitioned queue or topic unavailable.</span></span> <span data-ttu-id="ac7e2-212">Para saber mais, confira [Particionamento de entidades de mensagens](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-212">For more information, see [Partitioning Messaging Entities](https://msdn.microsoft.com/library/azure/dn520246.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="ac7e2-213">Solução</span><span class="sxs-lookup"><span data-stu-id="ac7e2-213">Solution</span></span>
<span data-ttu-id="ac7e2-214">O trecho de código a seguir mostra como particionar entidades de mensagens.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-214">The following code snippet shows how to partition messaging entities.</span></span>

```
// Create partitioned topic.
NamespaceManager ns = NamespaceManager.CreateFromConnectionString(myConnectionString);
TopicDescription td = new TopicDescription(TopicName);
td.EnablePartitioning = true;
ns.CreateTopic(td);
```

<span data-ttu-id="ac7e2-215">Para obter mais informações, consulte [Tópicos e filas do barramento de serviço particionado | Blog do Microsoft Azure](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) e confira a amostra [Fila particionada do Barramento de Serviço do Microsoft Azure](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-215">For more information, see [Partitioned Service Bus Queues and Topics | Microsoft Azure Blog](https://azure.microsoft.com/blog/2013/10/29/partitioned-service-bus-queues-and-topics/) and check out the [Microsoft Azure Service Bus Partitioned Queue](https://code.msdn.microsoft.com/windowsazure/Service-Bus-Partitioned-7dfd3f1f) sample.</span></span>

## <a name="do-not-set-sharedaccessstarttime"></a><span data-ttu-id="ac7e2-216">Não definir SharedAccessStartTime</span><span class="sxs-lookup"><span data-stu-id="ac7e2-216">Do not set SharedAccessStartTime</span></span>
### <a name="id"></a><span data-ttu-id="ac7e2-217">ID</span><span class="sxs-lookup"><span data-stu-id="ac7e2-217">ID</span></span>
<span data-ttu-id="ac7e2-218">AP3001</span><span class="sxs-lookup"><span data-stu-id="ac7e2-218">AP3001</span></span>

### <a name="description"></a><span data-ttu-id="ac7e2-219">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac7e2-219">Description</span></span>
<span data-ttu-id="ac7e2-220">Você deve evitar usar SharedAccessStartTimeset para a hora atual para iniciar imediatamente a política de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-220">You should avoid using SharedAccessStartTimeset to the current time to immediately start the Shared Access policy.</span></span> <span data-ttu-id="ac7e2-221">Você só precisa definir essa propriedade se quiser iniciar a política de acesso compartilhado em um momento posterior.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-221">You only need to set this property if you want to start the Shared Access policy at a later time.</span></span>

<span data-ttu-id="ac7e2-222">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-222">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="ac7e2-223">Motivo</span><span class="sxs-lookup"><span data-stu-id="ac7e2-223">Reason</span></span>
<span data-ttu-id="ac7e2-224">A sincronização do relógio causa uma pequena diferença de hora entre os data centers.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-224">Clock synchronization causes a slight time difference among datacenters.</span></span> <span data-ttu-id="ac7e2-225">Por exemplo, você pensaria logicamente que definir a hora de início de uma política SAS de armazenamento como a hora atual usando o método DateTime.Now ou semelhante faria com que a política SAS entrasse em vigor imediatamente.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-225">For example, you would logically think setting the start time of a storage SAS policy as the current time by using DateTime.Now or a similar method will cause the SAS policy to take effect immediately.</span></span> <span data-ttu-id="ac7e2-226">No entanto, as pequenas diferenças de horário entre data centers podem causar problemas com isso, já que alguns horários de data center podem ser ligeiramente posteriores ou anteriores à hora de início.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-226">However, the slight time differences between datacenters can cause problems with this since some datacenter times might be slightly later than the start time, while others ahead of it.</span></span> <span data-ttu-id="ac7e2-227">Como resultado, a política de SAS pode expirar rapidamente (ou até mesmo imediatamente) se o tempo de vida da política definido for muito curto.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-227">As a result, the SAS policy can expire quickly (or even immediately) if the policy lifetime is set too short.</span></span>

<span data-ttu-id="ac7e2-228">Para orientação de como usar a assinatura de acesso compartilhado no armazenamento do Azure, consulte [Apresentando SAS (Assinatura de Acesso Compartilhado) de tabela, SAS de fila e atualização de SAS de blob - Blog da equipe de Armazenamento do Microsoft Azure - Home page do site - Blogs MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-228">For more guidance on using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="ac7e2-229">Solução</span><span class="sxs-lookup"><span data-stu-id="ac7e2-229">Solution</span></span>
<span data-ttu-id="ac7e2-230">Remova a instrução que define a hora de início da política de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-230">Remove the statement that sets the start time of the shared access policy.</span></span> <span data-ttu-id="ac7e2-231">A ferramenta de análise de código do Azure fornece uma correção para esse problema.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-231">The Azure Code Analysis tool provides a fix for this issue.</span></span> <span data-ttu-id="ac7e2-232">Para obter mais informações sobre gerenciamento de segurança, consulte o padrão de design [Padrão de chave de manobrista](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-232">For more information on security management, please see the design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="ac7e2-233">O trecho de código a seguir demonstra a correção de código para esse problema.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-233">The following code snippet demonstrates the code fix for this issue.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

## <a name="shared-access-policy-expiry-time-must-be-more-than-five-minutes"></a><span data-ttu-id="ac7e2-234">O tempo de expiração da Política de Acesso Compartilhado deve ser mais de cinco minutos</span><span class="sxs-lookup"><span data-stu-id="ac7e2-234">Shared Access Policy expiry time must be more than five minutes</span></span>
### <a name="id"></a><span data-ttu-id="ac7e2-235">ID</span><span class="sxs-lookup"><span data-stu-id="ac7e2-235">ID</span></span>
<span data-ttu-id="ac7e2-236">AP3002</span><span class="sxs-lookup"><span data-stu-id="ac7e2-236">AP3002</span></span>

### <a name="description"></a><span data-ttu-id="ac7e2-237">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac7e2-237">Description</span></span>
<span data-ttu-id="ac7e2-238">Pode haver até cinco minutos de diferença em relógios dos data centers em locais diferentes devido a uma condição conhecida como "defasagem horária".</span><span class="sxs-lookup"><span data-stu-id="ac7e2-238">There can be as much as a five minute difference in clocks among datacenters at different locations due to a condition known as "clock skew."</span></span> <span data-ttu-id="ac7e2-239">Para impedir que o token da política de SAS expire antes do planejado, defina a hora de expiração para mais de cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-239">To prevent the SAS policy token from expiring earlier than planned, set the expiry time to be more than five minutes.</span></span>

<span data-ttu-id="ac7e2-240">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-240">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="ac7e2-241">Motivo</span><span class="sxs-lookup"><span data-stu-id="ac7e2-241">Reason</span></span>
<span data-ttu-id="ac7e2-242">Data centers em locais diferentes no mundo sincronizam por um sinal de relógio.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-242">Datacenters at different locations around the world synchronize by a clock signal.</span></span> <span data-ttu-id="ac7e2-243">Como o sinal de relógio demora em viajar para locais diferentes, pode haver uma variação de tempo entre data centers em locais geográficos diferentes, embora supostamente tudo esteja sincronizado.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-243">Because it takes time for clock signal to travel to different locations, there can be a time variance between datacenters at different geographical locations although everything is supposedly synchronized.</span></span> <span data-ttu-id="ac7e2-244">Essa diferença de tempo pode afetar o intervalo de expiração e a hora de início da política de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-244">This time difference can affect the Shared Access policy start time and expiration interval.</span></span> <span data-ttu-id="ac7e2-245">Portanto, para garantir a política de acesso compartilhado entre em vigor imediatamente, não especifique a hora de início.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-245">Therefore, to ensure Shared Access policy takes effect immediately, don’t specify the start time.</span></span> <span data-ttu-id="ac7e2-246">Além disso, verifique se que a hora de expiração é de mais de 5 minutos para evitar antecipação do tempo limite.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-246">In addition, make sure the expiration time is more than 5 minutes to prevent early timeout.</span></span>

<span data-ttu-id="ac7e2-247">Para obter instruções sobre como usar assinatura de acesso compartilhado no armazenamento do Azure, consulte [Apresentando SAS (Assinatura de Acesso Compartilhado) de tabela, SAS de fila e atualização de SAS de blob - Blog da equipe de Armazenamento do Microsoft Azure - Home page do site - Blogs MSDN](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-247">For more information about using Shared Access Signature on Azure storage, see [Introducing Table SAS (Shared Access Signature), Queue SAS and update to Blob SAS - Microsoft Azure Storage Team Blog - Site Home - MSDN Blogs](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx).</span></span>

### <a name="solution"></a><span data-ttu-id="ac7e2-248">Solução</span><span class="sxs-lookup"><span data-stu-id="ac7e2-248">Solution</span></span>
<span data-ttu-id="ac7e2-249">Para obter mais informações sobre gerenciamento de segurança, consulte o padrão de design [Padrão de chave de manobrista](https://msdn.microsoft.com/library/dn568102.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-249">For more information on security management, see the design pattern [Valet Key Pattern](https://msdn.microsoft.com/library/dn568102.aspx).</span></span>

<span data-ttu-id="ac7e2-250">Este é um exemplo de não especificar uma hora de início da política de acesso compartilhado.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-250">The following is an example of not specifying a Shared Access policy start time.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
   SharedAccessExpiryTime = DateTime.UtcNow.AddHours(10),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="ac7e2-251">Este é um exemplo de especificação de uma hora de início da política de acesso compartilhado com uma duração de expiração de política superior a cinco minutos.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-251">The following is an example of specifying a Shared Access policy start time with a policy expiration duration greater than five minutes.</span></span>

```
// The shared access policy provides  
// read/write access to the container for 10 hours.
blobPermissions.SharedAccessPolicies.Add("mypolicy", new SharedAccessBlobPolicy()
{
   // To ensure SAS is valid immediately, don’t set start time.
   // This way, you can avoid failures caused by small clock differences.
  SharedAccessStartTime = new DateTime(2014,1,20),   
 SharedAccessExpiryTime = new DateTime(2014, 1, 21),
   Permissions = SharedAccessBlobPermissions.Write |
      SharedAccessBlobPermissions.Read
});
```

<span data-ttu-id="ac7e2-252">Para obter mais informações, consulte [Criar e usar uma assinatura de acesso compartilhado](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-252">For more information, see [Create and Use a Shared Access Signature](https://msdn.microsoft.com/library/azure/jj721951.aspx).</span></span>

## <a name="use-cloudconfigurationmanager"></a><span data-ttu-id="ac7e2-253">Use CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="ac7e2-253">Use CloudConfigurationManager</span></span>
### <a name="id"></a><span data-ttu-id="ac7e2-254">ID</span><span class="sxs-lookup"><span data-stu-id="ac7e2-254">ID</span></span>
<span data-ttu-id="ac7e2-255">AP4000</span><span class="sxs-lookup"><span data-stu-id="ac7e2-255">AP4000</span></span>

### <a name="description"></a><span data-ttu-id="ac7e2-256">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac7e2-256">Description</span></span>
<span data-ttu-id="ac7e2-257">O uso da classe [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) para projetos como o site do Azure e serviços móveis do Azure não introduzirá problemas de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-257">Using the [ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) class for projects such as Azure Website and Azure mobile services won't introduce runtime issues.</span></span> <span data-ttu-id="ac7e2-258">Como melhor prática, no entanto, é uma boa ideia usar Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) como uma forma unificada de gerenciamento de configurações para todos os aplicativos de nuvem do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-258">As a best practice, however, it's a good idea to use Cloud[ConfigurationManager](https://msdn.microsoft.com/library/system.configuration.configurationmanager\(v=vs.110\).aspx) as a unified way of managing configurations for all Azure Cloud applications.</span></span>

<span data-ttu-id="ac7e2-259">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-259">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="ac7e2-260">Motivo</span><span class="sxs-lookup"><span data-stu-id="ac7e2-260">Reason</span></span>
<span data-ttu-id="ac7e2-261">CloudConfigurationManager lê o arquivo de configuração apropriado para o ambiente do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-261">CloudConfigurationManager reads the configuration file appropriate to the application environment.</span></span>

[<span data-ttu-id="ac7e2-262">CloudConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="ac7e2-262">CloudConfigurationManager</span></span>](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx)

### <a name="solution"></a><span data-ttu-id="ac7e2-263">Solução</span><span class="sxs-lookup"><span data-stu-id="ac7e2-263">Solution</span></span>
<span data-ttu-id="ac7e2-264">Refatore seu código para usar a classe [CloudConfigurationManager](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-264">Refactor your code to use the [CloudConfigurationManager Class](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.cloudconfigurationmanager.aspx).</span></span> <span data-ttu-id="ac7e2-265">Uma correção de código para esse problema é fornecida pela ferramenta de análise de código do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-265">A code fix for this issue is provided by the Azure Code Analysis tool.</span></span>

<span data-ttu-id="ac7e2-266">O trecho de código a seguir demonstra a correção de código para esse problema.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-266">The following code snippet demonstrates the code fix for this issue.</span></span> <span data-ttu-id="ac7e2-267">Substitua</span><span class="sxs-lookup"><span data-stu-id="ac7e2-267">Replace</span></span>

`var settings = ConfigurationManager.AppSettings["mySettings"];`

<span data-ttu-id="ac7e2-268">por:</span><span class="sxs-lookup"><span data-stu-id="ac7e2-268">with</span></span>

`var settings = CloudConfigurationManager.GetSetting("mySettings");`

<span data-ttu-id="ac7e2-269">Eis um exemplo de como armazenar a definição de configuração em um arquivo App.config ou Web.config.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-269">Here's an example of how to store the configuration setting in a App.config or Web.config file.</span></span> <span data-ttu-id="ac7e2-270">Adicione as configurações à seção appSettings do arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-270">Add the settings to the appSettings section of the configuration file.</span></span> <span data-ttu-id="ac7e2-271">Este é o arquivo Web.config para o exemplo de código anterior.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-271">The following is the Web.config file for the previous code example.</span></span>

```
<appSettings>
    <add key="webpages:Version" value="3.0.0.0" />
    <add key="webpages:Enabled" value="false" />
    <add key="ClientValidationEnabled" value="true" />
    <add key="UnobtrusiveJavaScriptEnabled" value="true" />
    <add key="mySettings" value="[put_your_setting_here]"/>
  </appSettings>  
```

## <a name="avoid-using-hard-coded-connection-strings"></a><span data-ttu-id="ac7e2-272">Evitar o uso de cadeias de conexão embutidas em código</span><span class="sxs-lookup"><span data-stu-id="ac7e2-272">Avoid using hard-coded connection strings</span></span>
### <a name="id"></a><span data-ttu-id="ac7e2-273">ID</span><span class="sxs-lookup"><span data-stu-id="ac7e2-273">ID</span></span>
<span data-ttu-id="ac7e2-274">AP4001</span><span class="sxs-lookup"><span data-stu-id="ac7e2-274">AP4001</span></span>

### <a name="description"></a><span data-ttu-id="ac7e2-275">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac7e2-275">Description</span></span>
<span data-ttu-id="ac7e2-276">Se você usar cadeias de conexão embutidas em código e precisar atualizá-las mais tarde, terá de fazer alterações em seu código-fonte e recompilar o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-276">If you use hard-coded connection strings and you need to update them later, you’ll have to make changes to your source code and recompile the application.</span></span> <span data-ttu-id="ac7e2-277">No entanto, se você armazenar as cadeias de conexão em um arquivo de configuração, poderá alterá-las posteriormente simplesmente atualizando o arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-277">However, if you store your connection strings in a configuration file, you can change them later by simply updating the configuration file.</span></span>

<span data-ttu-id="ac7e2-278">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-278">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="ac7e2-279">Motivo</span><span class="sxs-lookup"><span data-stu-id="ac7e2-279">Reason</span></span>
<span data-ttu-id="ac7e2-280">Cadeias de conexão hard-coding é uma prática ruim, porque apresenta problemas quando as cadeias de conexão precisam ser alteradas rapidamente.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-280">Hard-coding connection strings is a bad practice because it introduces problems when connection strings need to be changed quickly.</span></span> <span data-ttu-id="ac7e2-281">Além disso, se o projeto precisar ser verificado no controle do código-fonte, as cadeias de conexão embutidas em código introduzirão vulnerabilidades de segurança, já que podem ser exibidas no código-fonte.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-281">In addition, if the project needs to be checked in to source control, hard-coded connection strings introduce security vulnerabilities since the strings can be viewed in the source code.</span></span>

### <a name="solution"></a><span data-ttu-id="ac7e2-282">Solução</span><span class="sxs-lookup"><span data-stu-id="ac7e2-282">Solution</span></span>
<span data-ttu-id="ac7e2-283">Armazene cadeias de conexão em arquivos de configuração ou ambientes do Azure.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-283">Store connection strings in the configuration files or Azure environments.</span></span>

* <span data-ttu-id="ac7e2-284">Para aplicativos autônomos, use o app.config para armazenar configurações de cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-284">For standalone applications, use app.config to store connection string settings.</span></span>
* <span data-ttu-id="ac7e2-285">Para aplicativos autônomos, use o web.config para armazenar cadeias de conexão.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-285">For IIS-hosted web applications, use web.config to store connection strings.</span></span>
* <span data-ttu-id="ac7e2-286">Para aplicativos do vNext do ASP.NET, use configuration.json para armazenar cadeias de conexão.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-286">For ASP.NET vNext applications, use configuration.json to store connection strings.</span></span>

<span data-ttu-id="ac7e2-287">Para obter informações sobre como usar arquivos de configurações, como web.config ou app.config, consulte [Diretrizes de configuração Web do ASP.NET](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-287">For information on using configurations files such as web.config or app.config, see [ASP.NET Web Configuration Guidelines](https://msdn.microsoft.com/library/vstudio/ff400235\(v=vs.100\).aspx).</span></span> <span data-ttu-id="ac7e2-288">Para obter informações sobre como variáveis de ambiente do Azure funcionam, consulte [Sites do Azure: como as cadeias de aplicativo e cadeias de conexão funcionam](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-288">For information on how Azure environment variables work, see [Azure Web Sites: How Application Strings and Connection Strings Work](https://azure.microsoft.com/blog/2013/07/17/windows-azure-web-sites-how-application-strings-and-connection-strings-work/).</span></span> <span data-ttu-id="ac7e2-289">Para obter informações sobre o armazenamento de cadeia de conexão no controle do código-fonte, consulte [Evitar colocar informações confidenciais, como cadeias de conexão em arquivos armazenados no repositório de código-fonte](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-289">For information on storing connection string in source control, see [avoid putting sensitive information such as connection strings in files that are stored in source code repository](http://www.asp.net/aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control).</span></span>

## <a name="use-diagnostics-configuration-file"></a><span data-ttu-id="ac7e2-290">Usar arquivo de configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="ac7e2-290">Use diagnostics configuration file</span></span>
### <a name="id"></a><span data-ttu-id="ac7e2-291">ID</span><span class="sxs-lookup"><span data-stu-id="ac7e2-291">ID</span></span>
<span data-ttu-id="ac7e2-292">AP5000</span><span class="sxs-lookup"><span data-stu-id="ac7e2-292">AP5000</span></span>

### <a name="description"></a><span data-ttu-id="ac7e2-293">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac7e2-293">Description</span></span>
<span data-ttu-id="ac7e2-294">Em vez de definir as configurações de diagnóstico em seu código usando a API de programação Microsoft.WindowsAzure.Diagnostics, você deve configurar as definições de diagnóstico no arquivo diagnostics.wadcfg.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-294">Instead of configuring diagnostics settings in your code such as by using the Microsoft.WindowsAzure.Diagnostics programming API, you should configure diagnostics settings in the diagnostics.wadcfg file.</span></span> <span data-ttu-id="ac7e2-295">(Ou diagnostics.wadcfgx se você usar o SDK 2.5 do Azure).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-295">(Or, diagnostics.wadcfgx if you use Azure SDK 2.5).</span></span> <span data-ttu-id="ac7e2-296">Fazendo isso, você pode alterar as configurações de diagnóstico sem recompilar o código.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-296">By doing this, you can change diagnostics settings without having to recompile your code.</span></span>

<span data-ttu-id="ac7e2-297">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-297">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="ac7e2-298">Motivo</span><span class="sxs-lookup"><span data-stu-id="ac7e2-298">Reason</span></span>
<span data-ttu-id="ac7e2-299">Antes do SDK 2.5 do Azure (que usa o diagnóstico do Azure 1.3), o diagnóstico do Azure (WAD) podia ser configurado usando vários métodos diferentes: adicionando-o ao blob de configuração no armazenamento, usando código obrigatório, configuração declarativa ou a configuração padrão.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-299">Before Azure SDK 2.5 (which uses Azure diagnostics 1.3), Azure Diagnostics (WAD) could be configured by using several different methods: adding it to the configuration blob in storage, by using imperative code, declarative configuration, or the default configuration.</span></span> <span data-ttu-id="ac7e2-300">No entanto, a melhor maneira de configurar diagnósticos é usar um arquivo de configuração XML (diagnostics.wadcfg ou diagnositcs.wadcfgx para SDK 2.5 e posterior) no projeto do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-300">However, the preferred way to configure diagnostics is to use an XML configuration file (diagnostics.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later) in the application project.</span></span> <span data-ttu-id="ac7e2-301">Nessa abordagem, o arquivo diagnostics.wadcfg define completamente a configuração e pode ser atualizado e reimplantado à vontade.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-301">In this approach, the diagnostics.wadcfg file completely defines the configuration and can be updated and redeployed at will.</span></span> <span data-ttu-id="ac7e2-302">A combinação do uso do arquivo de configuração diagnostics.wadcfg com os métodos de programação de definir configurações usando as classes [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx) ou [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx) pode gerar confusão.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-302">Mixing the use of the diagnostics.wadcfg configuration file with the programmatic methods of setting configurations by using the [DiagnosticMonitor](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.diagnosticmonitor.aspx)or [RoleInstanceDiagnosticManager](https://msdn.microsoft.com/library/microsoft.windowsazure.diagnostics.management.roleinstancediagnosticmanager.aspx)classes can lead to confusion.</span></span> <span data-ttu-id="ac7e2-303">Consulte [Inicializar ou alterar configuração de diagnóstico do Azure](https://msdn.microsoft.com/library/azure/hh411537.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-303">See [Initialize or Change Azure Diagnostics Configuration](https://msdn.microsoft.com/library/azure/hh411537.aspx) for more information.</span></span>

<span data-ttu-id="ac7e2-304">A partir do WAD 1.3 (incluído com o SDK 2.5 do Azure), não é possível usar o código para configurar diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-304">Beginning with WAD 1.3 (included with Azure SDK 2.5), it’s no longer possible to use code to configure diagnostics.</span></span> <span data-ttu-id="ac7e2-305">Como resultado, você só pode fornecer a configuração ao aplicar ou atualizar a extensão de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-305">As a result, you can only provide the configuration when applying or updating the diagnostics extension.</span></span>

### <a name="solution"></a><span data-ttu-id="ac7e2-306">Solução</span><span class="sxs-lookup"><span data-stu-id="ac7e2-306">Solution</span></span>
<span data-ttu-id="ac7e2-307">Use o designer de configuração de diagnóstico para mover as configurações de diagnóstico para o arquivo de configuração de diagnóstico (diagnositcs.wadcfg ou diagnositcs.wadcfgx para SDK 2.5 e posterior).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-307">Use the diagnostics configuration designer to move diagnostic settings to the diagnostics configuration file (diagnositcs.wadcfg or diagnositcs.wadcfgx for SDK 2.5 and later).</span></span> <span data-ttu-id="ac7e2-308">Também é recomendável que você instale [SDK 2.5 do Azure](http://go.microsoft.com/fwlink/?LinkId=513188) e usar o recurso de diagnóstico mais recente.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-308">It’s also recommended that you install [Azure SDK 2.5](http://go.microsoft.com/fwlink/?LinkId=513188) and use the latest diagnostics feature.</span></span>

1. <span data-ttu-id="ac7e2-309">No menu de atalho da função que você deseja configurar, escolha Propriedades e, em seguida, escolha a guia Configuração.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-309">On the shortcut menu for the role that you want to configure, choose Properties, and then choose the Configuration tab.</span></span>
2. <span data-ttu-id="ac7e2-310">Na seção **Diagnóstico**, verifique se a caixa de seleção **Habilitar Diagnóstico** está marcada.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-310">In the **Diagnostics** section, make sure that the **Enable Diagnostics** check box is selected.</span></span>
3. <span data-ttu-id="ac7e2-311">Escolha o botão **Configurar** .</span><span class="sxs-lookup"><span data-stu-id="ac7e2-311">Choose the **Configure** button.</span></span>

   ![Acessando a opção Habilitar Diagnóstico](./media/vs-azure-tools-optimizing-azure-code-in-visual-studio/IC796660.png)

   <span data-ttu-id="ac7e2-313">Consulte [Configurando o diagnóstico para os serviços de nuvem do Azure e máquinas virtuais](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-313">See [Configuring Diagnostics for Azure Cloud Services and Virtual Machines](vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines.md) for more information.</span></span>

## <a name="avoid-declaring-dbcontext-objects-as-static"></a><span data-ttu-id="ac7e2-314">Evitar declarar objetos DbContext como estáticos</span><span class="sxs-lookup"><span data-stu-id="ac7e2-314">Avoid declaring DbContext objects as static</span></span>
### <a name="id"></a><span data-ttu-id="ac7e2-315">ID</span><span class="sxs-lookup"><span data-stu-id="ac7e2-315">ID</span></span>
<span data-ttu-id="ac7e2-316">AP6000</span><span class="sxs-lookup"><span data-stu-id="ac7e2-316">AP6000</span></span>

### <a name="description"></a><span data-ttu-id="ac7e2-317">Descrição</span><span class="sxs-lookup"><span data-stu-id="ac7e2-317">Description</span></span>
<span data-ttu-id="ac7e2-318">Para economizar memória, evite declarar objetos DbContext como estáticos.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-318">To save memory, avoid declaring DBContext objects as static.</span></span>

<span data-ttu-id="ac7e2-319">Compartilhe suas ideias e comentários em [Comentários de análise de código do Azure](http://go.microsoft.com/fwlink/?LinkId=403771).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-319">Please share your ideas and feedback at [Azure Code Analysis feedback](http://go.microsoft.com/fwlink/?LinkId=403771).</span></span>

### <a name="reason"></a><span data-ttu-id="ac7e2-320">Motivo</span><span class="sxs-lookup"><span data-stu-id="ac7e2-320">Reason</span></span>
<span data-ttu-id="ac7e2-321">Objetos DBContext mantêm os resultados da consulta de cada chamada.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-321">DBContext objects hold the query results from each call.</span></span> <span data-ttu-id="ac7e2-322">Os objetos estáticos DBContext não são descartados até que o domínio de aplicativo seja descarregado.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-322">Static DBContext objects are not disposed until the application domain is unloaded.</span></span> <span data-ttu-id="ac7e2-323">Portanto, um objeto DBContext estático pode consumir grandes quantidades de memória.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-323">Therefore, a static DBContext object can consume large amounts of memory.</span></span>

### <a name="solution"></a><span data-ttu-id="ac7e2-324">Solução</span><span class="sxs-lookup"><span data-stu-id="ac7e2-324">Solution</span></span>
<span data-ttu-id="ac7e2-325">Declare DBContext como uma variável local ou um campo de instância não estático, use-o para uma tarefa e deixe-o ser descartado após o uso.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-325">Declare DBContext as a local variable or non-static instance field, use it for a task, and then let it be disposed of after use.</span></span>

<span data-ttu-id="ac7e2-326">O exemplo a seguir de classe de controlador MVC mostra como usar o objeto DBContext.</span><span class="sxs-lookup"><span data-stu-id="ac7e2-326">The following example MVC controller class shows how to use the DBContext object.</span></span>

```
public class BlogsController : Controller
    {
        //BloggingContext is a subclass to DbContext        
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

## <a name="next-steps"></a><span data-ttu-id="ac7e2-327">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ac7e2-327">Next steps</span></span>
<span data-ttu-id="ac7e2-328">Para saber mais sobre a otimização e solução de problemas de aplicativos do Azure, consulte [Solucionar problemas de um aplicativo Web no Serviço de Aplicativo do Azure usando o Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="ac7e2-328">To learn more about optimizing and troubleshooting Azure apps, see [Troubleshoot a web app in Azure App Service using Visual Studio](app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md).</span></span>
