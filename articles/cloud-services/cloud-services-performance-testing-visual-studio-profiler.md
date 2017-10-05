---
title: "Criação de um perfil de serviço de nuvem localmente no emulador de computação | Microsoft Docs"
services: cloud-services
description: "Investigar problemas de desempenho nos serviços de nuvem com o criador de perfil do Visual Studio"
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
tags: 
ms.assetid: 25e40bf3-eea0-4b0b-9f4a-91ffe797f6c3
ms.service: cloud-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 51c8192d8312dc5cf546b4c357aeecf6f19d56b8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="testing-the-performance-of-a-cloud-service-locally-in-the-azure-compute-emulator-using-the-visual-studio-profiler"></a><span data-ttu-id="6796e-103">Testando o desempenho de um serviço de nuvem localmente no emulador de computação do Azure usando o criador de perfis do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6796e-103">Testing the Performance of a Cloud Service Locally in the Azure Compute Emulator Using the Visual Studio Profiler</span></span>
<span data-ttu-id="6796e-104">Várias técnicas e ferramentas estão disponíveis para testar o desempenho de serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="6796e-104">A variety of tools and techniques are available for testing the performance of cloud services.</span></span>
<span data-ttu-id="6796e-105">Quando publica um serviço de nuvem no Azure, você pode fazer com que o Visual Studio colete dados de criação de perfil e, em seguida, os analise localmente, conforme descrito em [Criar o perfil de um aplicativo do Azure][1].</span><span class="sxs-lookup"><span data-stu-id="6796e-105">When you publish a cloud service to Azure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="6796e-106">Você também pode usar o diagnóstico para acompanhar vários contadores de desempenho, conforme descrito em [Usar contadores de desempenho no Azure][2].</span><span class="sxs-lookup"><span data-stu-id="6796e-106">You can also use diagnostics to track a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="6796e-107">Também convém criar o perfil de seu aplicativo localmente no emulador de computação antes de implantá-lo na nuvem.</span><span class="sxs-lookup"><span data-stu-id="6796e-107">You might also want to profile your application locally in the compute emulator before deploying it to the cloud.</span></span>

<span data-ttu-id="6796e-108">Este artigo aborda o método de Amostragem de CPU de criação de perfil, que pode ser executado localmente no emulador.</span><span class="sxs-lookup"><span data-stu-id="6796e-108">This article covers the CPU Sampling method of profiling, which can be done locally in the emulator.</span></span> <span data-ttu-id="6796e-109">A Amostragem de CPU é um método de criação de perfil que não é muito invasivo.</span><span class="sxs-lookup"><span data-stu-id="6796e-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="6796e-110">Em um intervalo de amostragem designado, o criador de perfis tira um instantâneo da pilha de chamadas.</span><span class="sxs-lookup"><span data-stu-id="6796e-110">At a designated sampling interval, the profiler takes a snapshot of the call stack.</span></span> <span data-ttu-id="6796e-111">Os dados são coletados durante um período de tempo e mostrados em um relatório.</span><span class="sxs-lookup"><span data-stu-id="6796e-111">The data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="6796e-112">Esse método de criação de perfis tende a indicar onde está sendo feita a maior parte do trabalho em um aplicativo que utiliza muitos recursos de computação.</span><span class="sxs-lookup"><span data-stu-id="6796e-112">This method of profiling tends to indicate where in a computationally intensive application most of the CPU work is being done.</span></span>  <span data-ttu-id="6796e-113">Isso oferece a oportunidade de focalizar o "afunilamento" onde seu aplicativo está gastando mais tempo.</span><span class="sxs-lookup"><span data-stu-id="6796e-113">This gives you the opportunity to focus on the "hot path" where your application is spending the most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="6796e-114">1: Configurar o Visual Studio para criação de perfil</span><span class="sxs-lookup"><span data-stu-id="6796e-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="6796e-115">Em primeiro lugar, há algumas opções de configuração do Visual Studio que podem ser úteis ao criar perfis.</span><span class="sxs-lookup"><span data-stu-id="6796e-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="6796e-116">Para compreender os relatórios de criação de perfis, você precisará de símbolos (arquivos .pdb) para seu aplicativo e também de símbolos para as bibliotecas do sistema.</span><span class="sxs-lookup"><span data-stu-id="6796e-116">To make sense of the profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="6796e-117">Você deve certificar-se de fazer referência aos servidores de símbolo disponíveis.</span><span class="sxs-lookup"><span data-stu-id="6796e-117">You'll want to make sure that you reference the available symbol servers.</span></span> <span data-ttu-id="6796e-118">Para fazer isso, no menu **Ferramentas** do Visual Studio, escolha **Opções**, escolha **Depuração** e, em seguida, **Símbolos**.</span><span class="sxs-lookup"><span data-stu-id="6796e-118">To do this, on the **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="6796e-119">Verifique se os Servidores de Símbolo da Microsoft estão listados em **Locais do arquivo de símbolos (.pdb)**.</span><span class="sxs-lookup"><span data-stu-id="6796e-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="6796e-120">Você também pode fazer referência a http://referencesource.microsoft.com/symbols, que pode ter arquivos de símbolos adicionais.</span><span class="sxs-lookup"><span data-stu-id="6796e-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Opções de símbolo][4]

<span data-ttu-id="6796e-122">Se desejar, você pode simplificar os relatórios que o criador de perfis gera definindo Apenas Meu Código.</span><span class="sxs-lookup"><span data-stu-id="6796e-122">If desired, you can simplify the reports that the profiler generates by setting Just My Code.</span></span> <span data-ttu-id="6796e-123">Com a opção Apenas Meu Código habilitada, as pilhas de chamadas de função são simplificadas de maneira que as chamadas inteiramente internas às bibliotecas e ao .Net Framework sejam ocultados dos relatórios.</span><span class="sxs-lookup"><span data-stu-id="6796e-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal to libraries and the .NET Framework are hidden from the reports.</span></span> <span data-ttu-id="6796e-124">No menu **Ferramentas**, escolha **Opções**.</span><span class="sxs-lookup"><span data-stu-id="6796e-124">On the **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="6796e-125">Em seguida, expanda o nó **Ferramentas de Desempenho** e escolha **Geral**.</span><span class="sxs-lookup"><span data-stu-id="6796e-125">Then expand the **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="6796e-126">Marque a caixa de seleção **Habilitar Apenas Meu Código para relatórios do criador de perfis**.</span><span class="sxs-lookup"><span data-stu-id="6796e-126">Select the checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Opções Apenas Meu Código][17]

<span data-ttu-id="6796e-128">Você pode usar essas instruções com um projeto existente ou com um novo projeto.</span><span class="sxs-lookup"><span data-stu-id="6796e-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="6796e-129">Se você criar um novo projeto para testar as técnicas descritas a seguir, escolha um projeto C# do **Serviço de Nuvem do Azure** e selecione uma **Função Web** e uma **Função de Trabalho**.</span><span class="sxs-lookup"><span data-stu-id="6796e-129">If you create a new project to try the techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Funções de projeto do Serviço de Nuvem do Azure][5]

<span data-ttu-id="6796e-131">Para fins de exemplo, adicione um código ao seu projeto que demore muito tempo e demonstre alguns problemas óbvios de desempenho.</span><span class="sxs-lookup"><span data-stu-id="6796e-131">For example purposes, add some code to your project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="6796e-132">Por exemplo, adicione o seguinte código a um projeto de função de trabalho:</span><span class="sxs-lookup"><span data-stu-id="6796e-132">For example, add the following code to a worker role project:</span></span>

    public class Concatenator
    {
        public static string Concatenate(int number)
        {
            int count;
            string s = "";
            for (count = 0; count < number; count++)
            {
                s += "\n" + count.ToString();
            }
            return s;
        }
    }

<span data-ttu-id="6796e-133">Chame esse código do método RunAsync na classe derivada de RoleEntryPoint da função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6796e-133">Call this code from the RunAsync method in the worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="6796e-134">(Ignore o alerta relacionado ao método estar em execução de modo sincronizado.)</span><span class="sxs-lookup"><span data-stu-id="6796e-134">(Ignore the warning about the method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace the following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="6796e-135">Compile e execute seu serviço de nuvem localmente sem depuração (Ctrl+F5), com a configuração da solução definida como **Versão**.</span><span class="sxs-lookup"><span data-stu-id="6796e-135">Build and run your cloud service locally without debugging (Ctrl+F5), with the solution configuration set to **Release**.</span></span> <span data-ttu-id="6796e-136">Isso garante que todos os arquivos e pastas sejam criados para executar o aplicativo localmente e garante que todos os emuladores estejam iniciados.</span><span class="sxs-lookup"><span data-stu-id="6796e-136">This ensures that all files and folders are created for running the application locally, and ensures that all the emulators are started.</span></span> <span data-ttu-id="6796e-137">Inicie a UI do Emulador de Computação na barra de tarefas para confirmar que sua função de trabalho esteja em execução.</span><span class="sxs-lookup"><span data-stu-id="6796e-137">Start the Compute Emulator UI from the taskbar to verify that your worker role is running.</span></span>

## <a name="2-attach-to-a-process"></a><span data-ttu-id="6796e-138">2: Anexar a um processo</span><span class="sxs-lookup"><span data-stu-id="6796e-138">2: Attach to a process</span></span>
<span data-ttu-id="6796e-139">Em vez de criar o perfil do aplicativo iniciando-o no IDE do Visual Studio 2010, você deve anexar o criador de perfis a um processo em execução.</span><span class="sxs-lookup"><span data-stu-id="6796e-139">Instead of profiling the application by starting it from the Visual Studio 2010 IDE, you must attach the profiler to a running process.</span></span> 

<span data-ttu-id="6796e-140">Para anexar o criador de perfis a um processo, no menu **Analisar**, escolha **Criador de Perfis** e **Anexar/Desanexar**.</span><span class="sxs-lookup"><span data-stu-id="6796e-140">To attach the profiler to a process, on the **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Opção Anexar perfil][6]

<span data-ttu-id="6796e-142">Para uma função de trabalho, localize o processo WaWorkerHost.exe.</span><span class="sxs-lookup"><span data-stu-id="6796e-142">For a worker role, find the WaWorkerHost.exe process.</span></span>

![Processo WaWorkerHost][7]

<span data-ttu-id="6796e-144">Se a pasta de seu projeto estiver em uma unidade de rede, o criador de perfis solicitará que você forneça outro local para salvar os relatórios de criação de perfis.</span><span class="sxs-lookup"><span data-stu-id="6796e-144">If your project folder is on a network drive, the profiler will ask you to provide another location to save the profiling reports.</span></span>

 <span data-ttu-id="6796e-145">Também é possível conectar-se a uma função web, conectando-se ao WaIISHost.exe.</span><span class="sxs-lookup"><span data-stu-id="6796e-145">You can also attach to a web role by attaching to WaIISHost.exe.</span></span>
<span data-ttu-id="6796e-146">Se houver vários processos de função de trabalho em seu aplicativo, você precisará usar o processID para diferenciá-los.</span><span class="sxs-lookup"><span data-stu-id="6796e-146">If there are multiple worker role processes in your application, you need to use the processID to distinguish them.</span></span> <span data-ttu-id="6796e-147">Você pode consultar o processID programaticamente acessando o objeto Process.</span><span class="sxs-lookup"><span data-stu-id="6796e-147">You can query the processID programmatically by accessing the Process object.</span></span> <span data-ttu-id="6796e-148">Por exemplo, adicionando este código ao método Run da classe derivada de RoleEntryPoint em uma função, você pode examinar o log na interface do usuário do Emulador de Computação para saber a qual processo conectar-se.</span><span class="sxs-lookup"><span data-stu-id="6796e-148">For example, if you add this code to the Run method of the RoleEntryPoint-derived class in a role, you can look at the log in the Compute Emulator UI to know what process to connect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="6796e-149">Para exibir o log, inicie a interface do usuário do Emulador de Computação.</span><span class="sxs-lookup"><span data-stu-id="6796e-149">To view the log, start the Compute Emulator UI.</span></span>

![Iniciar a IU do Emulador de Computação][8]

<span data-ttu-id="6796e-151">Abra a janela do console do log da função de trabalho na interface do usuário do Emulador de Computação clicando na barra de títulos da janela do console.</span><span class="sxs-lookup"><span data-stu-id="6796e-151">Open the worker role log console window in the Compute Emulator UI by clicking on the console window's title bar.</span></span> <span data-ttu-id="6796e-152">Você pode ver a ID do processo no log.</span><span class="sxs-lookup"><span data-stu-id="6796e-152">You can see the process ID in the log.</span></span>

![Exibir ID do processo][9]

<span data-ttu-id="6796e-154">Depois de conectar-se, execute as etapas na interface do usuário do seu aplicativo (se necessário) para reproduzir o cenário.</span><span class="sxs-lookup"><span data-stu-id="6796e-154">One you've attached, perform the steps in your application's UI (if needed) to reproduce the scenario.</span></span>

<span data-ttu-id="6796e-155">Quando desejar parar a criação de perfis, escolha o link **Parar Criação de Perfis** .</span><span class="sxs-lookup"><span data-stu-id="6796e-155">When you want to stop profiling, choose the **Stop Profiling** link.</span></span>

![Opção Parar perfil][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="6796e-157">3: Exibir relatórios de desempenho</span><span class="sxs-lookup"><span data-stu-id="6796e-157">3: View performance reports</span></span>
<span data-ttu-id="6796e-158">O relatório de desempenho de seu aplicativo é exibido.</span><span class="sxs-lookup"><span data-stu-id="6796e-158">The performance report for your application is displayed.</span></span>

<span data-ttu-id="6796e-159">Nesse ponto, o criador de perfis interromperá a execução, salvará os dados em um arquivo .vsp e exibirá um relatório que mostra uma análise dos dados.</span><span class="sxs-lookup"><span data-stu-id="6796e-159">At this point, the profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Relatório do criador de perfil][11]

<span data-ttu-id="6796e-161">Se você vir String.wstrcpy no Afunilamento, clique em Apenas Meu Código para alterar a exibição para mostrar somente o código do usuário.</span><span class="sxs-lookup"><span data-stu-id="6796e-161">If you see String.wstrcpy in the Hot Path, click on Just My Code to change the view to show user code only.</span></span>  <span data-ttu-id="6796e-162">Se você vir String.Concat, tente pressionar o botão Mostrar Todo o Código.</span><span class="sxs-lookup"><span data-stu-id="6796e-162">If you see String.Concat, try pressing the Show All Code button.</span></span>

<span data-ttu-id="6796e-163">Você verá o método Concatenate e o String.Concat tomando uma grande parte do tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="6796e-163">You should see the Concatenate method and String.Concat taking up a large portion of the execution time.</span></span>

![Análise do relatório][12]

<span data-ttu-id="6796e-165">Se você adicionou o código de concatenação de cadeia de caracteres deste artigo, verá um aviso na Lista de Tarefas por isso.</span><span class="sxs-lookup"><span data-stu-id="6796e-165">If you added the string concatenation code in this article, you should see a warning in the Task List for this.</span></span> <span data-ttu-id="6796e-166">Você também poderá ver um aviso de que há uma quantidade excessiva de coleta de lixo, devido ao número de cadeias de caracteres que são criadas e descartadas.</span><span class="sxs-lookup"><span data-stu-id="6796e-166">You may also see a warning that there is an excessive amount of garbage collection, which is due to the number of strings that are created and disposed.</span></span>

![Avisos do desempenho][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="6796e-168">4: Fazer alterações e comparar o desempenho</span><span class="sxs-lookup"><span data-stu-id="6796e-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="6796e-169">Você também pode comparar o desempenho antes e depois de uma alteração no código.</span><span class="sxs-lookup"><span data-stu-id="6796e-169">You can also compare the performance before and after a code change.</span></span>  <span data-ttu-id="6796e-170">Interrompa o processo em execução e edite o código para substituir a operação de concatenação de cadeia de caracteres pelo uso de StringBuilder:</span><span class="sxs-lookup"><span data-stu-id="6796e-170">Stop the running process, and edit the code to replace the string concatenation operation with the use of StringBuilder:</span></span>

    public static string Concatenate(int number)
    {
        int count;
        System.Text.StringBuilder builder = new System.Text.StringBuilder("");
        for (count = 0; count < number; count++)
        {
             builder.Append("\n" + count.ToString());
        }
        return builder.ToString();
    }

<span data-ttu-id="6796e-171">Realize outra execução de desempenho e, em seguida, compare o desempenho.</span><span class="sxs-lookup"><span data-stu-id="6796e-171">Do another performance run, and then compare the performance.</span></span> <span data-ttu-id="6796e-172">No Gerenciador de Desempenho, se as execuções forem na mesma sessão, você poderá selecionar os dois relatórios, abrir o menu de atalho e escolher **Comparar Relatórios de Desempenho**.</span><span class="sxs-lookup"><span data-stu-id="6796e-172">In the Performance Explorer, if the runs are in the same session, you can just select both reports, open the shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="6796e-173">Se desejar comparar com uma execução em outra sessão de desempenho, abra o menu **Analisar** e escolha **Comparar Relatórios de Desempenho**.</span><span class="sxs-lookup"><span data-stu-id="6796e-173">If you want to compare with a run in another performance session, open the **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="6796e-174">Especifique os dois arquivos na caixa de diálogo que é exibida.</span><span class="sxs-lookup"><span data-stu-id="6796e-174">Specify both files in the dialog box that appears.</span></span>

![Opção Comparar relatórios do desempenho][15]

<span data-ttu-id="6796e-176">Os relatórios destacam as diferenças entre as duas execuções.</span><span class="sxs-lookup"><span data-stu-id="6796e-176">The reports highlight differences between the two runs.</span></span>

![Relatório da comparação][16]

<span data-ttu-id="6796e-178">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="6796e-178">Congratulations!</span></span> <span data-ttu-id="6796e-179">Você começou a usar o criador de perfis.</span><span class="sxs-lookup"><span data-stu-id="6796e-179">You've gotten started with the profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="6796e-180">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="6796e-180">Troubleshooting</span></span>
* <span data-ttu-id="6796e-181">Verifique se você está criando o perfil de uma compilação de versão e inicie sem depurar.</span><span class="sxs-lookup"><span data-stu-id="6796e-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="6796e-182">Se a opção Conectar/Desconectar não estiver habilitada no menu Criador de Perfis, execute o Assistente de Desempenho.</span><span class="sxs-lookup"><span data-stu-id="6796e-182">If the Attach/Detach option is not enabled on the Profiler menu, run the Performance Wizard.</span></span>
* <span data-ttu-id="6796e-183">Use a interface do usuário do Emulador de Computação para exibir o status do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="6796e-183">Use the Compute Emulator UI to view the status of your application.</span></span> 
* <span data-ttu-id="6796e-184">Se tiver problemas para iniciar aplicativos no emulador ou para conectar o criador de perfis, desligue e reinicie o emulador de computação.</span><span class="sxs-lookup"><span data-stu-id="6796e-184">If you have problems starting applications in the emulator, or attaching the profiler, shut down the compute emulator and restart it.</span></span> <span data-ttu-id="6796e-185">Se isso não resolver o problema, tente reinicializar.</span><span class="sxs-lookup"><span data-stu-id="6796e-185">If that doesn't solve the problem, try rebooting.</span></span> <span data-ttu-id="6796e-186">Esse problema pode ocorrer se você usar o Emulador de Computação para suspender e remover implantações em execução.</span><span class="sxs-lookup"><span data-stu-id="6796e-186">This problem can occur if you use the Compute Emulator to suspend and remove running deployments.</span></span>
* <span data-ttu-id="6796e-187">Se você tiver usado qualquer um dos comandos de criação de perfil na linha de comando, especialmente as configurações globais, verifique se VSPerfClrEnv / globaloff foi chamado e se VsPerfMon.exe foi desligado.</span><span class="sxs-lookup"><span data-stu-id="6796e-187">If you have used any of the profiling commands from the command line, especially the global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="6796e-188">Se durante a amostragem você vir a mensagem "PRF0025: nenhum dado foi coletado", verifique se o processo ao qual você se conectou tem atividade de CPU.</span><span class="sxs-lookup"><span data-stu-id="6796e-188">If when sampling, you see the message "PRF0025: No data was collected," check that the process you attached to has CPU activity.</span></span> <span data-ttu-id="6796e-189">Os aplicativos que não estão fazendo nenhum trabalho de computação podem não produzir nenhum dado de amostragem.</span><span class="sxs-lookup"><span data-stu-id="6796e-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="6796e-190">Também é possível que o processo tenha sido encerrado antes de qualquer amostra ter sido feita.</span><span class="sxs-lookup"><span data-stu-id="6796e-190">It's also possible that the process exited before any sampling was done.</span></span> <span data-ttu-id="6796e-191">Verifique se o método Run para uma função para a qual você esteja criando um perfil não é encerrado.</span><span class="sxs-lookup"><span data-stu-id="6796e-191">Check to see that the Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6796e-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6796e-192">Next Steps</span></span>
<span data-ttu-id="6796e-193">A instrumentação de binários do Azure no emulador não tem suporte no criador de perfis do Visual Studio, mas para testar a alocação de memória, você poderá escolher essa opção ao criar um perfil.</span><span class="sxs-lookup"><span data-stu-id="6796e-193">Instrumenting Azure binaries in the emulator is not supported in the Visual Studio profiler, but if you want to test memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="6796e-194">Você também pode escolher a criação de perfis simultânea, que ajuda a determinar se os threads estão perdendo tempo competindo por bloqueios, ou a criação de perfis de interação de camadas, que ajuda a rastrear problemas de desempenho ao interagir entre camadas de um aplicativo, mais frequentemente entre a camada de dados e uma função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6796e-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between the data tier and a worker role.</span></span>  <span data-ttu-id="6796e-195">Você pode exibir as consultas do banco de dados que seu aplicativo gera e usar os dados da criação de perfis para melhorar o uso do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="6796e-195">You can view the database queries that your app generates and use the profiling data to improve your use of the database.</span></span> <span data-ttu-id="6796e-196">Para obter informações sobre a criação de perfis de interação de camadas, veja a postagem no blog [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3] (Passo a passo: usando o criador de perfis de interação de camadas no Visual Studio Team System 2010).</span><span class="sxs-lookup"><span data-stu-id="6796e-196">For information about tier interaction profiling, see the blog post [Walkthrough: Using the Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

[1]: http://msdn.microsoft.com/library/azure/hh369930.aspx
[2]: http://msdn.microsoft.com/library/azure/hh411542.aspx
[3]: http://blogs.msdn.com/b/habibh/archive/2009/06/30/walkthrough-using-the-tier-interaction-profiler-in-visual-studio-team-system-2010.aspx
[4]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally09.png
[5]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally10.png
[6]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally02.png
[7]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally05.png
[8]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally010.png
[9]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally07.png
[10]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally06.png
[11]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally03.png
[12]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally011.png
[14]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally04.png 
[15]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally013.png
[16]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally012.png
[17]: ./media/cloud-services-performance-testing-visual-studio-profiler/ProfilingLocally08.png
