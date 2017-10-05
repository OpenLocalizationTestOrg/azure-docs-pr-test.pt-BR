---
title: "Rastrear o fluxo em um Aplicativo de Serviços de Nuvem com o Diagnóstico do Azure | Microsoft Docs"
description: "Adicione mensagens de rastreamento a um aplicativo do Azure para ajudar a depurar, medir o desempenho, monitorar, realizar a análise de tráfego e muito mais."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: 
ms.assetid: 09934772-cc07-4fd2-ba88-b224ca192f8e
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/20/2016
ms.author: robb
ms.openlocfilehash: 35b4a4270846c54a1ca760e803ef7adba60cf03b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="trace-the-flow-of-a-cloud-services-application-with-azure-diagnostics"></a><span data-ttu-id="c088e-103">Rastrear o fluxo de um aplicativo de Serviços de Nuvem com o Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="c088e-103">Trace the flow of a Cloud Services application with Azure Diagnostics</span></span>
<span data-ttu-id="c088e-104">O rastreamento é uma maneira de você monitorar a execução de seu aplicativo enquanto ele é executado.</span><span class="sxs-lookup"><span data-stu-id="c088e-104">Tracing is a way for you to monitor the execution of your application while it is running.</span></span> <span data-ttu-id="c088e-105">Você pode usar as classes [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx) e [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) para registrar informações sobre erros e execução do aplicativo em logs, arquivos de texto ou outros dispositivos para análise posterior.</span><span class="sxs-lookup"><span data-stu-id="c088e-105">You can use the [System.Diagnostics.Trace](https://msdn.microsoft.com/library/system.diagnostics.trace.aspx), [System.Diagnostics.Debug](https://msdn.microsoft.com/library/system.diagnostics.debug.aspx), and [System.Diagnostics.TraceSource](https://msdn.microsoft.com/library/system.diagnostics.tracesource.aspx) classes to record information about errors and application execution in logs, text files, or other devices for later analysis.</span></span> <span data-ttu-id="c088e-106">Para obter mais informações sobre rastreamento, consulte [Rastreamento e instrumentação de aplicativos](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span><span class="sxs-lookup"><span data-stu-id="c088e-106">For more information about tracing, see [Tracing and Instrumenting Applications](https://msdn.microsoft.com/library/zs6s4h68.aspx).</span></span>

## <a name="use-trace-statements-and-trace-switches"></a><span data-ttu-id="c088e-107">Usar instruções e opções de rastreamento</span><span class="sxs-lookup"><span data-stu-id="c088e-107">Use trace statements and trace switches</span></span>
<span data-ttu-id="c088e-108">Implemente o rastreamento em seu aplicativo de Serviços de Nuvem adicionando [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) à configuração do aplicativo e fazendo chamadas a System.Diagnostics.Trace ou System.Diagnostics.Debug no código do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c088e-108">Implement tracing in your Cloud Services application by adding the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) to the application configuration and making calls to System.Diagnostics.Trace or System.Diagnostics.Debug in your application code.</span></span> <span data-ttu-id="c088e-109">Use o arquivo de configuração *app.config* para funções de trabalho e *web.config* para funções Web.</span><span class="sxs-lookup"><span data-stu-id="c088e-109">Use the configuration file *app.config* for worker roles and the *web.config* for web roles.</span></span> <span data-ttu-id="c088e-110">Quando você cria um novo serviço hospedado usando um modelo do Visual Studio, o Diagnóstico do Azure é adicionado automaticamente ao projeto e DiagnosticMonitorTraceListener é adicionado ao arquivo de configuração apropriado para as funções que você adiciona.</span><span class="sxs-lookup"><span data-stu-id="c088e-110">When you create a new hosted service using a Visual Studio template, Azure Diagnostics is automatically added to the project and the DiagnosticMonitorTraceListener is added to the appropriate configuration file for the roles that you add.</span></span>

<span data-ttu-id="c088e-111">Para obter informações sobre como incluir instruções de rastreamento, consulte [Como: adicionar instruções de rastreamento ao código do aplicativo](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="c088e-111">For information on placing trace statements, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>

<span data-ttu-id="c088e-112">Incluindo [Opções de Rastreamento](https://msdn.microsoft.com/library/3at424ac.aspx) em seu código, você pode controlar se o rastreamento ocorre e qual a sua extensão.</span><span class="sxs-lookup"><span data-stu-id="c088e-112">By placing [Trace Switches](https://msdn.microsoft.com/library/3at424ac.aspx) in your code, you can control whether tracing occurs and how extensive it is.</span></span> <span data-ttu-id="c088e-113">Isso permite monitorar o status do aplicativo em um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="c088e-113">This lets you monitor the status of your application in a production environment.</span></span> <span data-ttu-id="c088e-114">Isso é particularmente importante em um aplicativo de negócios que usa vários componentes executados em vários computadores.</span><span class="sxs-lookup"><span data-stu-id="c088e-114">This is especially important in a business application that uses multiple components running on multiple computers.</span></span> <span data-ttu-id="c088e-115">Para obter mais informações, consulte [Como: configurar opções de rastreamento](https://msdn.microsoft.com/library/t06xyy08.aspx).</span><span class="sxs-lookup"><span data-stu-id="c088e-115">For more information, see [How to: Configure Trace Switches](https://msdn.microsoft.com/library/t06xyy08.aspx).</span></span>

## <a name="configure-the-trace-listener-in-an-azure-application"></a><span data-ttu-id="c088e-116">Configurar o ouvinte de rastreamento em um aplicativo do Azure</span><span class="sxs-lookup"><span data-stu-id="c088e-116">Configure the trace listener in an Azure application</span></span>
<span data-ttu-id="c088e-117">Rastreamento, depuração e TraceSource exigem que você configure "ouvintes" para coletar e registrar as mensagens que são enviadas.</span><span class="sxs-lookup"><span data-stu-id="c088e-117">Trace, Debug and TraceSource, require you set up "listeners" to collect and record the messages that are sent.</span></span> <span data-ttu-id="c088e-118">Os ouvintes coletam, armazenam e roteiam mensagens de rastreamento.</span><span class="sxs-lookup"><span data-stu-id="c088e-118">Listeners collect, store, and route tracing messages.</span></span> <span data-ttu-id="c088e-119">Eles direcionam a saída de rastreamento para um destino apropriado, como um log, uma janela ou um arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="c088e-119">They direct the tracing output to an appropriate target, such as a log, window, or text file.</span></span> <span data-ttu-id="c088e-120">O Diagnóstico do Azure usa a classe [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) .</span><span class="sxs-lookup"><span data-stu-id="c088e-120">Azure Diagnostics uses the [DiagnosticMonitorTraceListener](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitortracelistener.aspx) class.</span></span>

<span data-ttu-id="c088e-121">Antes de concluir o procedimento a seguir, você deve inicializar o monitor de diagnóstico do Azure.</span><span class="sxs-lookup"><span data-stu-id="c088e-121">Before you complete the following procedure, you must initialize the Azure diagnostic monitor.</span></span> <span data-ttu-id="c088e-122">Para fazer isso, consulte [Habilitando o diagnóstico no Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="c088e-122">To do this, see [Enabling Diagnostics in Microsoft Azure](cloud-services-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="c088e-123">Observe que, se você usar os modelos fornecidos pelo Visual Studio, a configuração do ouvinte será adicionada automaticamente para você.</span><span class="sxs-lookup"><span data-stu-id="c088e-123">Note that if you use the templates that are provided by Visual Studio, the configuration of the listener is added automatically for you.</span></span>

### <a name="add-a-trace-listener"></a><span data-ttu-id="c088e-124">Adicionar um ouvinte de rastreamento</span><span class="sxs-lookup"><span data-stu-id="c088e-124">Add a trace listener</span></span>
1. <span data-ttu-id="c088e-125">Abra o arquivo web.config ou app.config para sua função.</span><span class="sxs-lookup"><span data-stu-id="c088e-125">Open the web.config or app.config file for your role.</span></span>
2. <span data-ttu-id="c088e-126">Adicione o seguinte código ao arquivo.</span><span class="sxs-lookup"><span data-stu-id="c088e-126">Add the following code to the file.</span></span> <span data-ttu-id="c088e-127">Altere o atributo Version para usar o número de versão do assembly que está sendo referenciado.</span><span class="sxs-lookup"><span data-stu-id="c088e-127">Change the Version attribute to use the version number of the assembly you are referencing.</span></span> <span data-ttu-id="c088e-128">A versão do assembly não é alterada, necessariamente, com cada versão do SDK do Azure, a menos que existam atualizações a ele.</span><span class="sxs-lookup"><span data-stu-id="c088e-128">The assembly version does not necessarily change with each Azure SDK release unless there are updates to it.</span></span>
   
    ```
    <system.diagnostics>
        <trace>
            <listeners>
                <add type="Microsoft.WindowsAzure.Diagnostics.DiagnosticMonitorTraceListener,
                  Microsoft.WindowsAzure.Diagnostics,
                  Version=2.8.0.0,
                  Culture=neutral,
                  PublicKeyToken=31bf3856ad364e35"
                  name="AzureDiagnostics">
                    <filter type="" />
                </add>
            </listeners>
        </trace>
    </system.diagnostics>
    ```
   > [!IMPORTANT]
   > <span data-ttu-id="c088e-129">Verifique se você tem uma referência de projeto ao assembly Microsoft.WindowsAzure.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="c088e-129">Make sure you have a project reference to the Microsoft.WindowsAzure.Diagnostics assembly.</span></span> <span data-ttu-id="c088e-130">Atualize o número de versão no xml acima para que ele corresponda à versão do assembly referenciado Microsoft.WindowsAzure.Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="c088e-130">Update the version number in the xml above to match the version of the referenced Microsoft.WindowsAzure.Diagnostics assembly.</span></span>
   > 
   > 
3. <span data-ttu-id="c088e-131">Salve o arquivo de configuração.</span><span class="sxs-lookup"><span data-stu-id="c088e-131">Save the config file.</span></span>

<span data-ttu-id="c088e-132">Para obter mais informações sobre ouvintes, veja [Ouvintes de rastreamento](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span><span class="sxs-lookup"><span data-stu-id="c088e-132">For more information about listeners, see [Trace Listeners](https://msdn.microsoft.com/library/4y5y10s7.aspx).</span></span>

<span data-ttu-id="c088e-133">Depois de concluir as etapas para adicionar o ouvinte, você pode adicionar instruções de rastreamento ao código.</span><span class="sxs-lookup"><span data-stu-id="c088e-133">After you complete the steps to add the listener, you can add trace statements to your code.</span></span>

### <a name="to-add-trace-statement-to-your-code"></a><span data-ttu-id="c088e-134">Para adicionar a instrução de rastreamento ao código</span><span class="sxs-lookup"><span data-stu-id="c088e-134">To add trace statement to your code</span></span>
1. <span data-ttu-id="c088e-135">Abra um arquivo de origem para o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c088e-135">Open a source file for your application.</span></span> <span data-ttu-id="c088e-136">Por exemplo, o arquivo <RoleName>.cs para a função de trabalho ou função Web.</span><span class="sxs-lookup"><span data-stu-id="c088e-136">For example, the <RoleName>.cs file for the worker role or web role.</span></span>
2. <span data-ttu-id="c088e-137">Adicione a seguinte instrução using se ainda não tiver sido adicionada:</span><span class="sxs-lookup"><span data-stu-id="c088e-137">Add the following using statement if it has not already been added:</span></span>
    ```
        using System.Diagnostics;
    ```
3. <span data-ttu-id="c088e-138">Adicione instruções Trace em que você deseja capturar informações sobre o estado do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c088e-138">Add Trace statements where you want to capture information about the state of your application.</span></span> <span data-ttu-id="c088e-139">Você pode usar diversos métodos para formatar a saída da instrução Trace.</span><span class="sxs-lookup"><span data-stu-id="c088e-139">You can use a variety of methods to format the output of the Trace statement.</span></span> <span data-ttu-id="c088e-140">Para obter mais informações, veja [Como adicionar instruções de rastreamento ao código do aplicativo](https://msdn.microsoft.com/library/zd83saa2.aspx).</span><span class="sxs-lookup"><span data-stu-id="c088e-140">For more information, see [How to: Add Trace Statements to Application Code](https://msdn.microsoft.com/library/zd83saa2.aspx).</span></span>
4. <span data-ttu-id="c088e-141">Salve o arquivo de origem.</span><span class="sxs-lookup"><span data-stu-id="c088e-141">Save the source file.</span></span>

