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
# <a name="testing-hello-performance-of-a-cloud-service-locally-in-hello-azure-compute-emulator-using-hello-visual-studio-profiler"></a>Em teste o desempenho de um serviço de nuvem localmente no Olá Olá Azure emulador de computação usando o criador de perfil Visual Studio
Uma variedade de ferramentas e técnicas que estão disponíveis para teste de desempenho de saudação de serviços de nuvem.
Quando você publica um tooAzure de serviço de nuvem, você pode ter o Visual Studio coletar dados de criação e analisá-los localmente, conforme descrito em [criação de perfil de um aplicativo do Azure][1].
Você também pode usar o diagnóstico tootrack contadores de uma variedade de desempenho, conforme descrito em [usando contadores de desempenho no Azure][2].
Você também poderá tooprofile seu aplicativo localmente no emulador de computação de saudação antes de implantá-la toohello nuvem.

Este artigo aborda o método de amostragem de CPU hello de criação de perfil, que pode ser feito localmente no emulador de saudação. A Amostragem de CPU é um método de criação de perfil que não é muito invasivo. Em um intervalo de amostragem designado profiler Olá tira um instantâneo da pilha de chamadas de saudação. Olá dados são coletados por um período de tempo e mostrados em um relatório. Esse método de criação de perfil tende a tooindicate onde em um aplicativo de computação intensivo maior parte do trabalho de saudação da CPU está sendo feita.  Isso proporciona Olá toofocus de oportunidade em hello "afunilamento" onde seu aplicativo está gastando Olá maior parte do tempo.

## <a name="1-configure-visual-studio-for-profiling"></a>1: Configurar o Visual Studio para criação de perfil
Em primeiro lugar, há algumas opções de configuração do Visual Studio que podem ser úteis ao criar perfis. sentido toomake Olá relatórios de criação de perfil, você precisará de símbolos (arquivos. PDB) para seu aplicativo e também símbolos para bibliotecas do sistema. Você vai querer toomake-se de fazer referência a servidores de símbolos disponíveis de saudação. toodo isso em Olá **ferramentas** menu do Visual Studio, escolha **opções**, escolha **depuração**, em seguida, **símbolos**. Verifique se os Servidores de Símbolo da Microsoft estão listados em **Locais do arquivo de símbolos (.pdb)**.  Você também pode fazer referência a http://referencesource.microsoft.com/symbols, que pode ter arquivos de símbolos adicionais.

![Opções de símbolo][4]

Se desejar, você pode simplificar o hello relata que profiler hello gera definindo apenas meu código. Com Just My Code ativado, pilhas de chamadas de função são simplificadas para que chame toolibraries inteiramente interno e saudação do .NET Framework estão ocultos do hello relatórios. Em Olá **ferramentas** menu, escolha **opções**. Em seguida, expanda Olá **ferramentas de desempenho** nó e escolha **geral**. Selecione caixa de seleção Olá para **habilitar apenas meu código para relatórios do criador de perfil**.

![Opções Apenas Meu Código][17]

Você pode usar essas instruções com um projeto existente ou com um novo projeto.  Se você criar um novo Olá de tootry projeto técnicas descritas abaixo, escolha um c# **serviço de nuvem do Azure** do projeto e selecione um **função Web** e um **função de trabalho**.

![Funções de projeto do Serviço de Nuvem do Azure][5]

Por exemplo, fins, adicionar alguns projeto tooyour de código que leva muito tempo e demonstra a algum problema de desempenho óbvio. Por exemplo, adicione Olá projeto de função de trabalho de tooa de código a seguir:

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

Chame esse código de saudação RunAsync método na classe derivada de RoleEntryPoint da função de trabalho hello. (Ignorar aviso de saudação sobre método hello executando de forma síncrona).

        private async Task RunAsync(CancellationToken cancellationToken)
        {
            // TODO: Replace hello following with your own logic.
            while (!cancellationToken.IsCancellationRequested)
            {
                Trace.TraceInformation("Working");
                Concatenator.Concatenate(10000);
            }
        }

Compilar e executar seu serviço de nuvem localmente sem depuração (Ctrl + F5), com a configuração de solução Olá definida muito**versão**. Isso garante que todos os arquivos e pastas são criadas para executar o aplicativo hello localmente e garante que todos os emuladores de saudação são iniciados. Inicie Olá UI do emulador de computação do hello tooverify de barra de tarefas que está executando a função de trabalho.

## <a name="2-attach-tooa-process"></a>2: anexar processo tooa
Em vez de criar o perfil de aplicativo hello, iniciando-o da saudação IDE do Visual Studio 2010, você deve anexar Olá profiler tooa executando o processo. 

tooattach Olá profiler tooa processo, em Olá **analisar** menu, escolha **Profiler** e **Attach/Detach**.

![Opção Anexar perfil][6]

Para uma função de trabalho, localize o processo de WaWorkerHost.exe hello.

![Processo WaWorkerHost][7]

Se sua pasta de projeto estiver em uma unidade de rede, o criador de perfil de saudação pedirá que você tooprovide Olá de toosave outro local relatórios de criação de perfil.

 Você também pode anexar a função de web tooa anexando tooWaIISHost.exe.
Se houver vários processos de função de trabalho em seu aplicativo, você precisa toouse Olá processID toodistinguish-los. Você pode consultar Olá processID programaticamente, acessando o objeto de processo hello. Por exemplo, se você adicionar esse método de execução do código toohello da classe derivada RoleEntryPoint de saudação em uma função, você pode examinar o log Olá UI do emulador de computação tooknow tooconnect o processo para.

    var process = System.Diagnostics.Process.GetCurrentProcess();
    var message = String.Format("Process ID: {0}", process.Id);
    Trace.WriteLine(message, "Information");

log de saudação tooview, Olá iniciar IU do emulador de computação.

![Iniciar Olá UI do emulador de computação][8]

Abrir Olá trabalho função log console no hello UI do emulador de computação clicando na barra de título da janela do console de saudação. Você pode ver o ID do processo Olá no log de saudação.

![Exibir ID do processo][9]

Um anexado, execute as etapas de Olá cenário de saudação de tooreproduce do seu aplicativo da interface do usuário (se necessário).

Quando você quiser toostop de criação de perfil, escolha Olá **parar criação de perfil** link.

![Opção Parar perfil][10]

## <a name="3-view-performance-reports"></a>3: Exibir relatórios de desempenho
relatório de desempenho de saudação para seu aplicativo é exibido.

Neste ponto, profiler hello interrompe a execução, salva dados em um arquivo. vsp e exibe um relatório que mostra uma análise dos dados.

![Relatório do criador de perfil][11]

Se você vir String.wstrcpy em Olá afunilamento, clique em apenas meu código toochange Olá exibição tooshow usuário somente código.  Se você vir concat, tente pressionando o botão Mostrar todo o código de saudação.

Você deve ver o método concatenar hello e String. Concat ocupando uma grande parte do tempo de execução de saudação.

![Análise do relatório][12]

Se você adicionou o código de concatenação de cadeia de caracteres hello neste artigo, você verá um aviso na lista de tarefas de saudação para isso. Você também pode ver um aviso de que há uma quantidade excessiva de coleta de lixo, que é devido toohello número de cadeias de caracteres que são criados e descartados.

![Avisos do desempenho][14]

## <a name="4-make-changes-and-compare-performance"></a>4: Fazer alterações e comparar o desempenho
Você também pode comparar o desempenho de saudação antes e após uma alteração de código.  Parar Olá executando o processo e editar Olá código tooreplace Olá cadeia operação de concatenação com o uso de saudação de StringBuilder:

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

Fazer outra execução de desempenho e, em seguida, comparar o desempenho de saudação. Olá Gerenciador de desempenho, se hello execuções estão no hello mesma sessão, apenas selecione os dois relatórios, abra o menu de atalho hello e escolha **comparar relatórios de desempenho**. Se você quiser toocompare com uma execução em outra sessão de desempenho, abra Olá **analisar** menu e escolha **comparar relatórios de desempenho**. Especifique os dois arquivos na caixa de diálogo de saudação que é exibida.

![Opção Comparar relatórios do desempenho][15]

relatórios de saudação realce as diferenças entre duas execuções de saudação.

![Relatório da comparação][16]

Parabéns! Ter começado usar com o criador de perfil de saudação.

## <a name="troubleshooting"></a>Solucionar problemas
* Verifique se você está criando o perfil de uma compilação de versão e inicie sem depurar.
* Se Olá Attach/Detach opção não está habilitado no menu do criador de perfil hello, execute Olá Assistente de desempenho.
* Use o status de saudação de tooview Olá UI do emulador de computação do seu aplicativo. 
* Se você tiver problemas para iniciar aplicativos no emulador de saudação ou anexando Olá profiler, desligar o emulador de computação hello e reiniciá-lo. Se isso não resolver o problema de hello, tente reiniciar. Esse problema pode ocorrer se você usar o hello emulador de computação toosuspend e remove as implantações em execução.
* Se você usou qualquer um dos comandos da linha de comando de criação de perfil de hello, especialmente Olá configurações globais, certifique-se de que VSPerfClrEnv /globaloff foi chamado e VsPerfMon.exe foi desligado.
* Se durante a amostragem, você vir a mensagem de saudação "PRF0025: nenhum dado foi coletado," Verifique se Olá processo anexado atividade toohas da CPU. Os aplicativos que não estão fazendo nenhum trabalho de computação podem não produzir nenhum dado de amostragem.  Também é possível que o processo de saudação encerrado antes que qualquer amostragem foi feita. Verifique toosee não encerra um método de execução de saudação para uma função que você estiver criando um perfil.

## <a name="next-steps"></a>Próximas etapas
Não há suporte para a instrumentação de binários do Azure no emulador Olá no criador de perfil do hello Visual Studio, mas se você quiser tootest alocação de memória, você pode escolher essa opção ao criar o perfil. Também é possível criação de perfil de simultaneidade, que ajuda a determinar se threads são desperdiçar tempo competindo por bloqueios, ou camada de criação de perfil de interação, que ajuda você a localizar problemas de desempenho durante a interação entre camadas de um aplicativo, mais com frequência entre a camada de dados hello e uma função de trabalho.  Você pode exibir as consultas de banco de dados de hello gera seu aplicativo e usar Olá criação de perfil de dados tooimprove seu uso do banco de dados de saudação. Para obter informações sobre a criação de perfil de interação de camadas, consulte Olá postagem de blog [passo a passo: usando Olá criador de perfil de interação de camada no Visual Studio Team System 2010][3].

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
