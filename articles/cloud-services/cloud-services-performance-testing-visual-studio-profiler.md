---
title: "um serviço de nuvem localmente no emulador de computação do hello aaaProfiling | Microsoft Docs"
services: cloud-services
description: "Investigar problemas de desempenho em serviços de nuvem com o criador de perfil do hello Visual Studio"
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
ms.openlocfilehash: fc37c85dad4db4cc0310f73afad56fc0fe5f3963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a><span data-ttu-id="22603-103">Em teste o desempenho de um serviço de nuvem localmente no Olá Olá Azure emulador de computação usando o criador de perfil Visual Studio</span><span class="sxs-lookup"><span data-stu-id="22603-103">Testing hello Performance of a Cloud Service Locally in hello Azure Compute Emulator Using hello Visual Studio Profiler</span></span>
<span data-ttu-id="22603-104">Uma variedade de ferramentas e técnicas que estão disponíveis para teste de desempenho de saudação de serviços de nuvem.</span><span class="sxs-lookup"><span data-stu-id="22603-104">A variety of tools and techniques are available for testing hello performance of cloud services.</span></span>
<span data-ttu-id="22603-105">Quando você publica um tooAzure de serviço de nuvem, você pode ter o Visual Studio coletar dados de criação e analisá-los localmente, conforme descrito em [criação de perfil de um aplicativo do Azure][1].</span><span class="sxs-lookup"><span data-stu-id="22603-105">When you publish a cloud service tooAzure, you can have Visual Studio collect profiling data and then analyze it locally, as described in [Profiling an Azure Application][1].</span></span>
<span data-ttu-id="22603-106">Você também pode usar o diagnóstico tootrack contadores de uma variedade de desempenho, conforme descrito em [usando contadores de desempenho no Azure][2].</span><span class="sxs-lookup"><span data-stu-id="22603-106">You can also use diagnostics tootrack a variety of performance counters, as described in [Using performance counters in Azure][2].</span></span>
<span data-ttu-id="22603-107">Você também poderá tooprofile seu aplicativo localmente no emulador de computação de saudação antes de implantá-la toohello nuvem.</span><span class="sxs-lookup"><span data-stu-id="22603-107">You might also want tooprofile your application locally in hello compute emulator before deploying it toohello cloud.</span></span>

<span data-ttu-id="22603-108">Este artigo aborda o método de amostragem de CPU hello de criação de perfil, que pode ser feito localmente no emulador de saudação.</span><span class="sxs-lookup"><span data-stu-id="22603-108">This article covers hello CPU Sampling method of profiling, which can be done locally in hello emulator.</span></span> <span data-ttu-id="22603-109">A Amostragem de CPU é um método de criação de perfil que não é muito invasivo.</span><span class="sxs-lookup"><span data-stu-id="22603-109">CPU sampling is a method of profiling that is not very intrusive.</span></span> <span data-ttu-id="22603-110">Em um intervalo de amostragem designado profiler Olá tira um instantâneo da pilha de chamadas de saudação.</span><span class="sxs-lookup"><span data-stu-id="22603-110">At a designated sampling interval, hello profiler takes a snapshot of hello call stack.</span></span> <span data-ttu-id="22603-111">Olá dados são coletados por um período de tempo e mostrados em um relatório.</span><span class="sxs-lookup"><span data-stu-id="22603-111">hello data is collected over a period of time, and shown in a report.</span></span> <span data-ttu-id="22603-112">Esse método de criação de perfil tende a tooindicate onde em um aplicativo de computação intensivo maior parte do trabalho de saudação da CPU está sendo feita.</span><span class="sxs-lookup"><span data-stu-id="22603-112">This method of profiling tends tooindicate where in a computationally intensive application most of hello CPU work is being done.</span></span>  <span data-ttu-id="22603-113">Isso proporciona Olá toofocus de oportunidade em hello "afunilamento" onde seu aplicativo está gastando Olá maior parte do tempo.</span><span class="sxs-lookup"><span data-stu-id="22603-113">This gives you hello opportunity toofocus on hello "hot path" where your application is spending hello most time.</span></span>

## <a name="1-configure-visual-studio-for-profiling"></a><span data-ttu-id="22603-114">1: Configurar o Visual Studio para criação de perfil</span><span class="sxs-lookup"><span data-stu-id="22603-114">1: Configure Visual Studio for profiling</span></span>
<span data-ttu-id="22603-115">Em primeiro lugar, há algumas opções de configuração do Visual Studio que podem ser úteis ao criar perfis.</span><span class="sxs-lookup"><span data-stu-id="22603-115">First, there are a few Visual Studio configuration options that might be helpful when profiling.</span></span> <span data-ttu-id="22603-116">sentido toomake Olá relatórios de criação de perfil, você precisará de símbolos (arquivos. PDB) para seu aplicativo e também símbolos para bibliotecas do sistema.</span><span class="sxs-lookup"><span data-stu-id="22603-116">toomake sense of hello profiling reports, you'll need symbols (.pdb files) for your application and also symbols for system libraries.</span></span> <span data-ttu-id="22603-117">Você vai querer toomake-se de fazer referência a servidores de símbolos disponíveis de saudação.</span><span class="sxs-lookup"><span data-stu-id="22603-117">You'll want toomake sure that you reference hello available symbol servers.</span></span> <span data-ttu-id="22603-118">toodo isso em Olá **ferramentas** menu do Visual Studio, escolha **opções**, escolha **depuração**, em seguida, **símbolos**.</span><span class="sxs-lookup"><span data-stu-id="22603-118">toodo this, on hello **Tools** menu in Visual Studio, choose **Options**, then choose **Debugging**, then **Symbols**.</span></span> <span data-ttu-id="22603-119">Verifique se os Servidores de Símbolo da Microsoft estão listados em **Locais do arquivo de símbolos (.pdb)**.</span><span class="sxs-lookup"><span data-stu-id="22603-119">Make sure that Microsoft Symbol Servers is listed under **Symbol file (.pdb) locations**.</span></span>  <span data-ttu-id="22603-120">Você também pode fazer referência a http://referencesource.microsoft.com/symbols, que pode ter arquivos de símbolos adicionais.</span><span class="sxs-lookup"><span data-stu-id="22603-120">You can also reference http://referencesource.microsoft.com/symbols, which might have additional symbol files.</span></span>

![Opções de símbolo][4]

<span data-ttu-id="22603-122">Se desejar, você pode simplificar o hello relata que profiler hello gera definindo apenas meu código.</span><span class="sxs-lookup"><span data-stu-id="22603-122">If desired, you can simplify hello reports that hello profiler generates by setting Just My Code.</span></span> <span data-ttu-id="22603-123">Com Just My Code ativado, pilhas de chamadas de função são simplificadas para que chame toolibraries inteiramente interno e saudação do .NET Framework estão ocultos do hello relatórios.</span><span class="sxs-lookup"><span data-stu-id="22603-123">With Just My Code enabled, function call stacks are simplified so that calls entirely internal toolibraries and hello .NET Framework are hidden from hello reports.</span></span> <span data-ttu-id="22603-124">Em Olá **ferramentas** menu, escolha **opções**.</span><span class="sxs-lookup"><span data-stu-id="22603-124">On hello **Tools** menu, choose **Options**.</span></span> <span data-ttu-id="22603-125">Em seguida, expanda Olá **ferramentas de desempenho** nó e escolha **geral**.</span><span class="sxs-lookup"><span data-stu-id="22603-125">Then expand hello **Performance Tools** node, and choose **General**.</span></span> <span data-ttu-id="22603-126">Selecione caixa de seleção Olá para **habilitar apenas meu código para relatórios do criador de perfil**.</span><span class="sxs-lookup"><span data-stu-id="22603-126">Select hello checkbox for **Enable Just My Code for profiler reports**.</span></span>

![Opções Apenas Meu Código][17]

<span data-ttu-id="22603-128">Você pode usar essas instruções com um projeto existente ou com um novo projeto.</span><span class="sxs-lookup"><span data-stu-id="22603-128">You can use these instructions with an existing project or with a new project.</span></span>  <span data-ttu-id="22603-129">Se você criar um novo Olá de tootry projeto técnicas descritas abaixo, escolha um c# **serviço de nuvem do Azure** do projeto e selecione um **função Web** e um **função de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="22603-129">If you create a new project tootry hello techniques described below, choose a C# **Azure Cloud Service** project, and select a **Web Role** and a **Worker Role**.</span></span>

![Funções de projeto do Serviço de Nuvem do Azure][5]

<span data-ttu-id="22603-131">Por exemplo, fins, adicionar alguns projeto tooyour de código que leva muito tempo e demonstra a algum problema de desempenho óbvio.</span><span class="sxs-lookup"><span data-stu-id="22603-131">For example purposes, add some code tooyour project that takes a lot of time and demonstrates some obvious performance problem.</span></span> <span data-ttu-id="22603-132">Por exemplo, adicione Olá projeto de função de trabalho de tooa de código a seguir:</span><span class="sxs-lookup"><span data-stu-id="22603-132">For example, add hello following code tooa worker role project:</span></span>

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

<span data-ttu-id="22603-133">Chame esse código de saudação RunAsync método na classe derivada de RoleEntryPoint da função de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="22603-133">Call this code from hello RunAsync method in hello worker role's RoleEntryPoint-derived class.</span></span> <span data-ttu-id="22603-134">(Ignorar aviso de saudação sobre método hello executando de forma síncrona).</span><span class="sxs-lookup"><span data-stu-id="22603-134">(Ignore hello warning about hello method running synchronously.)</span></span>

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

<span data-ttu-id="22603-135">Compilar e executar seu serviço de nuvem localmente sem depuração (Ctrl + F5), com a configuração de solução Olá definida muito**versão**.</span><span class="sxs-lookup"><span data-stu-id="22603-135">Build and run your cloud service locally without debugging (Ctrl+F5), with hello solution configuration set too**Release**.</span></span> <span data-ttu-id="22603-136">Isso garante que todos os arquivos e pastas são criadas para executar o aplicativo hello localmente e garante que todos os emuladores de saudação são iniciados.</span><span class="sxs-lookup"><span data-stu-id="22603-136">This ensures that all files and folders are created for running hello application locally, and ensures that all hello emulators are started.</span></span> <span data-ttu-id="22603-137">Inicie Olá UI do emulador de computação do hello tooverify de barra de tarefas que está executando a função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="22603-137">Start hello Compute Emulator UI from hello taskbar tooverify that your worker role is running.</span></span>

## <a name="2-attach-tooa-process"></a><span data-ttu-id="22603-138">2: anexar processo tooa</span><span class="sxs-lookup"><span data-stu-id="22603-138">2: Attach tooa process</span></span>
<span data-ttu-id="22603-139">Em vez de criar o perfil de aplicativo hello, iniciando-o da saudação IDE do Visual Studio 2010, você deve anexar Olá profiler tooa executando o processo.</span><span class="sxs-lookup"><span data-stu-id="22603-139">Instead of profiling hello application by starting it from hello Visual Studio 2010 IDE, you must attach hello profiler tooa running process.</span></span> 

<span data-ttu-id="22603-140">tooattach Olá profiler tooa processo, em Olá **analisar** menu, escolha **Profiler** e **Attach/Detach**.</span><span class="sxs-lookup"><span data-stu-id="22603-140">tooattach hello profiler tooa process, on hello **Analyze** menu, choose **Profiler** and **Attach/Detach**.</span></span>

![Opção Anexar perfil][6]

<span data-ttu-id="22603-142">Para uma função de trabalho, localize o processo de WaWorkerHost.exe hello.</span><span class="sxs-lookup"><span data-stu-id="22603-142">For a worker role, find hello WaWorkerHost.exe process.</span></span>

![Processo WaWorkerHost][7]

<span data-ttu-id="22603-144">Se sua pasta de projeto estiver em uma unidade de rede, o criador de perfil de saudação pedirá que você tooprovide Olá de toosave outro local relatórios de criação de perfil.</span><span class="sxs-lookup"><span data-stu-id="22603-144">If your project folder is on a network drive, hello profiler will ask you tooprovide another location toosave hello profiling reports.</span></span>

 <span data-ttu-id="22603-145">Você também pode anexar a função de web tooa anexando tooWaIISHost.exe.</span><span class="sxs-lookup"><span data-stu-id="22603-145">You can also attach tooa web role by attaching tooWaIISHost.exe.</span></span>
<span data-ttu-id="22603-146">Se houver vários processos de função de trabalho em seu aplicativo, você precisa toouse Olá processID toodistinguish-los.</span><span class="sxs-lookup"><span data-stu-id="22603-146">If there are multiple worker role processes in your application, you need toouse hello processID toodistinguish them.</span></span> <span data-ttu-id="22603-147">Você pode consultar Olá processID programaticamente, acessando o objeto de processo hello.</span><span class="sxs-lookup"><span data-stu-id="22603-147">You can query hello processID programmatically by accessing hello Process object.</span></span> <span data-ttu-id="22603-148">Por exemplo, se você adicionar esse método de execução do código toohello da classe derivada RoleEntryPoint de saudação em uma função, você pode examinar o log Olá UI do emulador de computação tooknow tooconnect o processo para.</span><span class="sxs-lookup"><span data-stu-id="22603-148">For example, if you add this code toohello Run method of hello RoleEntryPoint-derived class in a role, you can look at the log in hello Compute Emulator UI tooknow what process tooconnect to.</span></span>

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

<span data-ttu-id="22603-149">log de saudação tooview, Olá iniciar IU do emulador de computação.</span><span class="sxs-lookup"><span data-stu-id="22603-149">tooview hello log, start hello Compute Emulator UI.</span></span>

![Iniciar Olá UI do emulador de computação][8]

<span data-ttu-id="22603-151">Abrir Olá trabalho função log console no hello UI do emulador de computação clicando na barra de título da janela do console de saudação.</span><span class="sxs-lookup"><span data-stu-id="22603-151">Open hello worker role log console window in hello Compute Emulator UI by clicking on hello console window's title bar.</span></span> <span data-ttu-id="22603-152">Você pode ver o ID do processo Olá no log de saudação.</span><span class="sxs-lookup"><span data-stu-id="22603-152">You can see hello process ID in hello log.</span></span>

![Exibir ID do processo][9]

<span data-ttu-id="22603-154">Um anexado, execute as etapas de Olá cenário de saudação de tooreproduce do seu aplicativo da interface do usuário (se necessário).</span><span class="sxs-lookup"><span data-stu-id="22603-154">One you've attached, perform hello steps in your application's UI (if needed) tooreproduce hello scenario.</span></span>

<span data-ttu-id="22603-155">Quando você quiser toostop de criação de perfil, escolha Olá **parar criação de perfil** link.</span><span class="sxs-lookup"><span data-stu-id="22603-155">When you want toostop profiling, choose hello **Stop Profiling** link.</span></span>

![Opção Parar perfil][10]

## <a name="3-view-performance-reports"></a><span data-ttu-id="22603-157">3: Exibir relatórios de desempenho</span><span class="sxs-lookup"><span data-stu-id="22603-157">3: View performance reports</span></span>
<span data-ttu-id="22603-158">relatório de desempenho de saudação para seu aplicativo é exibido.</span><span class="sxs-lookup"><span data-stu-id="22603-158">hello performance report for your application is displayed.</span></span>

<span data-ttu-id="22603-159">Neste ponto, profiler hello interrompe a execução, salva dados em um arquivo. vsp e exibe um relatório que mostra uma análise dos dados.</span><span class="sxs-lookup"><span data-stu-id="22603-159">At this point, hello profiler stops executing, saves data in a .vsp file, and displays a report that shows an analysis of this data.</span></span>

![Relatório do criador de perfil][11]

<span data-ttu-id="22603-161">Se você vir String.wstrcpy em Olá afunilamento, clique em apenas meu código toochange Olá exibição tooshow usuário somente código.</span><span class="sxs-lookup"><span data-stu-id="22603-161">If you see String.wstrcpy in hello Hot Path, click on Just My Code toochange hello view tooshow user code only.</span></span>  <span data-ttu-id="22603-162">Se você vir concat, tente pressionando o botão Mostrar todo o código de saudação.</span><span class="sxs-lookup"><span data-stu-id="22603-162">If you see String.Concat, try pressing hello Show All Code button.</span></span>

<span data-ttu-id="22603-163">Você deve ver o método concatenar hello e String. Concat ocupando uma grande parte do tempo de execução de saudação.</span><span class="sxs-lookup"><span data-stu-id="22603-163">You should see hello Concatenate method and String.Concat taking up a large portion of hello execution time.</span></span>

![Análise do relatório][12]

<span data-ttu-id="22603-165">Se você adicionou o código de concatenação de cadeia de caracteres hello neste artigo, você verá um aviso na lista de tarefas de saudação para isso.</span><span class="sxs-lookup"><span data-stu-id="22603-165">If you added hello string concatenation code in this article, you should see a warning in hello Task List for this.</span></span> <span data-ttu-id="22603-166">Você também pode ver um aviso de que há uma quantidade excessiva de coleta de lixo, que é devido toohello número de cadeias de caracteres que são criados e descartados.</span><span class="sxs-lookup"><span data-stu-id="22603-166">You may also see a warning that there is an excessive amount of garbage collection, which is due toohello number of strings that are created and disposed.</span></span>

![Avisos do desempenho][14]

## <a name="4-make-changes-and-compare-performance"></a><span data-ttu-id="22603-168">4: Fazer alterações e comparar o desempenho</span><span class="sxs-lookup"><span data-stu-id="22603-168">4: Make changes and compare performance</span></span>
<span data-ttu-id="22603-169">Você também pode comparar o desempenho de saudação antes e após uma alteração de código.</span><span class="sxs-lookup"><span data-stu-id="22603-169">You can also compare hello performance before and after a code change.</span></span>  <span data-ttu-id="22603-170">Parar Olá executando o processo e editar Olá código tooreplace Olá cadeia operação de concatenação com o uso de saudação de StringBuilder:</span><span class="sxs-lookup"><span data-stu-id="22603-170">Stop hello running process, and edit hello code tooreplace hello string concatenation operation with hello use of StringBuilder:</span></span>

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

<span data-ttu-id="22603-171">Fazer outra execução de desempenho e, em seguida, comparar o desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="22603-171">Do another performance run, and then compare hello performance.</span></span> <span data-ttu-id="22603-172">Olá Gerenciador de desempenho, se hello execuções estão no hello mesma sessão, apenas selecione os dois relatórios, abra o menu de atalho hello e escolha **comparar relatórios de desempenho**.</span><span class="sxs-lookup"><span data-stu-id="22603-172">In hello Performance Explorer, if hello runs are in hello same session, you can just select both reports, open hello shortcut menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="22603-173">Se você quiser toocompare com uma execução em outra sessão de desempenho, abra Olá **analisar** menu e escolha **comparar relatórios de desempenho**.</span><span class="sxs-lookup"><span data-stu-id="22603-173">If you want toocompare with a run in another performance session, open hello **Analyze** menu, and choose **Compare Performance Reports**.</span></span> <span data-ttu-id="22603-174">Especifique os dois arquivos na caixa de diálogo de saudação que é exibida.</span><span class="sxs-lookup"><span data-stu-id="22603-174">Specify both files in hello dialog box that appears.</span></span>

![Opção Comparar relatórios do desempenho][15]

<span data-ttu-id="22603-176">relatórios de saudação realce as diferenças entre duas execuções de saudação.</span><span class="sxs-lookup"><span data-stu-id="22603-176">hello reports highlight differences between hello two runs.</span></span>

![Relatório da comparação][16]

<span data-ttu-id="22603-178">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="22603-178">Congratulations!</span></span> <span data-ttu-id="22603-179">Ter começado usar com o criador de perfil de saudação.</span><span class="sxs-lookup"><span data-stu-id="22603-179">You've gotten started with hello profiler.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="22603-180">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="22603-180">Troubleshooting</span></span>
* <span data-ttu-id="22603-181">Verifique se você está criando o perfil de uma compilação de versão e inicie sem depurar.</span><span class="sxs-lookup"><span data-stu-id="22603-181">Make sure you are profiling a Release build and start without debugging.</span></span>
* <span data-ttu-id="22603-182">Se Olá Attach/Detach opção não está habilitado no menu do criador de perfil hello, execute Olá Assistente de desempenho.</span><span class="sxs-lookup"><span data-stu-id="22603-182">If hello Attach/Detach option is not enabled on hello Profiler menu, run hello Performance Wizard.</span></span>
* <span data-ttu-id="22603-183">Use o status de saudação de tooview Olá UI do emulador de computação do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="22603-183">Use hello Compute Emulator UI tooview hello status of your application.</span></span> 
* <span data-ttu-id="22603-184">Se você tiver problemas para iniciar aplicativos no emulador de saudação ou anexando Olá profiler, desligar o emulador de computação hello e reiniciá-lo.</span><span class="sxs-lookup"><span data-stu-id="22603-184">If you have problems starting applications in hello emulator, or attaching hello profiler, shut down hello compute emulator and restart it.</span></span> <span data-ttu-id="22603-185">Se isso não resolver o problema de hello, tente reiniciar.</span><span class="sxs-lookup"><span data-stu-id="22603-185">If that doesn't solve hello problem, try rebooting.</span></span> <span data-ttu-id="22603-186">Esse problema pode ocorrer se você usar o hello emulador de computação toosuspend e remove as implantações em execução.</span><span class="sxs-lookup"><span data-stu-id="22603-186">This problem can occur if you use hello Compute Emulator toosuspend and remove running deployments.</span></span>
* <span data-ttu-id="22603-187">Se você usou qualquer um dos comandos da linha de comando de criação de perfil de hello, especialmente Olá configurações globais, certifique-se de que VSPerfClrEnv /globaloff foi chamado e VsPerfMon.exe foi desligado.</span><span class="sxs-lookup"><span data-stu-id="22603-187">If you have used any of hello profiling commands from the command line, especially hello global settings, make sure that VSPerfClrEnv /globaloff has been called and that VsPerfMon.exe has been shut down.</span></span>
* <span data-ttu-id="22603-188">Se durante a amostragem, você vir a mensagem de saudação "PRF0025: nenhum dado foi coletado," Verifique se Olá processo anexado atividade toohas da CPU.</span><span class="sxs-lookup"><span data-stu-id="22603-188">If when sampling, you see hello message "PRF0025: No data was collected," check that hello process you attached toohas CPU activity.</span></span> <span data-ttu-id="22603-189">Os aplicativos que não estão fazendo nenhum trabalho de computação podem não produzir nenhum dado de amostragem.</span><span class="sxs-lookup"><span data-stu-id="22603-189">Applications that are not doing any computational work might not produce any sampling data.</span></span>  <span data-ttu-id="22603-190">Também é possível que o processo de saudação encerrado antes que qualquer amostragem foi feita.</span><span class="sxs-lookup"><span data-stu-id="22603-190">It's also possible that hello process exited before any sampling was done.</span></span> <span data-ttu-id="22603-191">Verifique toosee não encerra um método de execução de saudação para uma função que você estiver criando um perfil.</span><span class="sxs-lookup"><span data-stu-id="22603-191">Check toosee that hello Run method for a role that you are profiling does not terminate.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22603-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="22603-192">Next Steps</span></span>
<span data-ttu-id="22603-193">Não há suporte para a instrumentação de binários do Azure no emulador Olá no criador de perfil do hello Visual Studio, mas se você quiser tootest alocação de memória, você pode escolher essa opção ao criar o perfil.</span><span class="sxs-lookup"><span data-stu-id="22603-193">Instrumenting Azure binaries in hello emulator is not supported in hello Visual Studio profiler, but if you want tootest memory allocation, you can choose that option when profiling.</span></span> <span data-ttu-id="22603-194">Também é possível criação de perfil de simultaneidade, que ajuda a determinar se threads são desperdiçar tempo competindo por bloqueios, ou camada de criação de perfil de interação, que ajuda você a localizar problemas de desempenho durante a interação entre camadas de um aplicativo, mais com frequência entre a camada de dados hello e uma função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="22603-194">You can also choose concurrency profiling, which helps you determine whether threads are wasting time competing for locks, or tier interaction profiling, which helps you track down performance problems when interacting between tiers of an application, most frequently between hello data tier and a worker role.</span></span>  <span data-ttu-id="22603-195">Você pode exibir as consultas de banco de dados de hello gera seu aplicativo e usar Olá criação de perfil de dados tooimprove seu uso do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="22603-195">You can view hello database queries that your app generates and use hello profiling data tooimprove your use of hello database.</span></span> <span data-ttu-id="22603-196">Para obter informações sobre a criação de perfil de interação de camadas, consulte Olá postagem de blog [passo a passo: usando Olá criador de perfil de interação de camada no Visual Studio Team System 2010][3].</span><span class="sxs-lookup"><span data-stu-id="22603-196">For information about tier interaction profiling, see hello blog post [Walkthrough: Using hello Tier Interaction Profiler in Visual Studio Team System 2010][3].</span></span>

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
