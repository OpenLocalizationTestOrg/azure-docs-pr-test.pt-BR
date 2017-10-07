---
title: aplicativos da web em tempo real de aaaProfiling no Azure com o Application Insights | Microsoft Docs
description: "Identifique o afunilamento Olá no seu código do servidor da web com um criador de perfil de baixa capacidade."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/04/2017
ms.author: bwren
ms.openlocfilehash: 3c7f21076f19335e0f006327932e13623ec9526b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="profiling-live-azure-web-apps-with-application-insights"></a>Criação de perfil de aplicativos Web do Azure ativos com o Application Insights

*Este recurso do Application Insights é GA para os Serviços de Aplicativos e está na fase de versão prévia para a Computação.*

Descobrir quanto tempo é gasto em cada método em seu aplicativo web ao vivo usando Olá, ferramenta de criação de perfil [Azure Application Insights](app-insights-overview.md). Ele mostra perfis detalhados de solicitações ao vivo que foram atendidas pelo seu aplicativo e realça Olá 'afunilamento' que está usando Olá a maior parte do tempo. Ele seleciona automaticamente exemplos que têm tempos de resposta diferentes. Criador de perfil de saudação usa a sobrecarga de toominimize várias técnicas.

Olá profiler atualmente funciona para ASP.NET aplicativos web em execução nos serviços de aplicativo do Azure, pelo menos Olá Basic preço. 

<a id="installation"></a>
## <a name="enable-hello-profiler"></a>Habilitar o criador de perfil de saudação

[Instalar o Application Insights](app-insights-asp-net.md) em seu código. Se já estiver instalado, verifique se que você tem a versão mais recente do hello. (toodo isso, clique em seu projeto no Gerenciador de soluções e escolha gerenciar pacotes do NuGet. Selecione as atualizações e todos os pacotes de atualização). Implante seu aplicativo novamente.

*Usando o ASP.NET Core? [Marque aqui](#aspnetcore).*

Em [https://portal.azure.com](https://portal.azure.com), abrir o recurso do Application Insights Olá para seu aplicativo web. Abra **Desempenho** e clique em **Habilitar o Application Insights Profiler...**.

![Clique na faixa de criador de perfil de habilitar Olá][enable-profiler-banner]

Como alternativa, você pode clicar sempre **configurar** tooview status, habilitar ou desabilitar Olá criador de perfil.

![Na folha de desempenho de saudação, clique em configurar][performance-blade]

Aplicativos Web configurados com o Application Insights são listados na folha Configurar. Siga as instruções tooinstall Olá Profiler agent se necessário. Se nenhum aplicativo Web estiver configurado com o Application Insights, clique em *Adicionar Aplicativos Vinculados*.

Saudação de uso *Profiler habilitar* ou *desabilitar Profiler* botões Olá configurar folha toocontrol Olá Profiler em todos os seus aplicativos da web vinculado.



![Configurar folha][linked app services]

toostop ou reinicialização Olá criador de perfil para uma instância de serviço de aplicativo individual, você encontrará **em Olá recursos do serviço de aplicativo**, na **trabalhos Web**. toodelete-lo, veja em **extensões**.

![Desabilitar o Criador de Perfil para Trabalhos da Web][disable-profiler-webjob]

É recomendável que você tenha Olá Profiler habilitado em todos os seu toodiscover de aplicativos web qualquer desempenho problemas assim que possível.

Se você usar o aplicativo web do WebDeploy toodeploy alterações tooyour, certifique-se de que você exclua Olá **App_Data** pasta sejam excluídos durante a implantação. Caso contrário, hello arquivos da extensão do criador de perfil será excluído quando você implanta em seguida Olá web aplicativo tooAzure.

### <a name="using-profiler-with-azure-vms-and-compute-resources-preview"></a>Usando o Criador de Perfil com VMs do Azure e recursos de computação (versão prévia)

Quando você [habilita o Application Insights para os Serviços de Aplicativos do Azure em tempo de execução](app-insights-azure-web-apps.md#run-time-instrumentation-with-application-insights), o Criador de Perfil fica disponível automaticamente. (Se você tiver habilitado o Application Insights para o recurso de saudação, talvez você precise tooupdate toohello lates versão por meio de saudação **configurar** assistente.)

Há um [versão prévia do hello Profiler para recursos de computação do Azure](https://go.microsoft.com/fwlink/?linkid=848155).


## <a name="limits"></a>limites

retenção de dados saudação padrão é 5 dias. Máximo de 10 GB ingeridos por dia.

Não há nenhuma taxa para o serviço do criador de perfil de saudação. Seu aplicativo web deve ser hospedado em pelo menos Olá camada básica dos serviços de aplicativo.

## <a name="viewing-profiler-data"></a>Exibindo dados do criador de perfil

Abra a folha de desempenho hello e role para baixo a lista de operações toohello.




![Coluna de Exemplos da folha de desempenho do Application Insights][performance-blade-examples]

Olá colunas na tabela de saudação são:

* **Contagem de** -Olá número dessas solicitações no intervalo de tempo de saudação da folha de saudação.
* **Mediana** -tempo típico de saudação toorespond tooa solicitação entra em seu aplicativo. Metade de todas as respostas foram mais rápida do que isso.
* **95 Percentil** 95% de respostas foram mais rápido do que isso. Se esse valor é muito diferente da mediana hello, pode haver um problema intermitente com seu aplicativo. (Ou pode ser explicado por um recurso de design como armazenamento em cache).
* **Exemplos** -um ícone indica que profiler Olá capturou rastreamentos de pilha para esta operação.

Clique em Gerenciador de rastreamento de Olá Olá exemplos ícone tooopen. Olá explorer mostra vários exemplos que Olá profiler capturou, classificados pelo tempo de resposta.

Selecione um exemplo de tooshow uma divisão de nível de código de tempo gasto na solicitação Olá em execução.

![Gerenciador de rastreamento do Application Insights][trace-explorer]

**Mostrar o afunilamento** abre Olá maior nó de folha ou pelo menos algo fechar. Na maioria dos casos, esse nó será tooa adjacentes afunilamento de desempenho.



* **Rótulo**: nome de saudação do função hello ou evento. árvore de saudação mostra uma mistura de código e os eventos que ocorreram (como eventos SQL e http). evento superior Olá representa Olá geral duração da solicitação.
* **Decorrido**: intervalo de tempo de saudação entre o início de saudação da operação de saudação e de término da saudação.
* **Quando**: mostra quando o evento da funções hello foi executada nas funções de tooother de relação.

## <a name="how-tooread-performance-data"></a>Como os dados de desempenho de tooread

Criador de perfil de serviço Microsoft usa uma combinação de desempenho de saudação tooanalyze instrumentação e método de seu aplicativo de amostra.
Quando a coleção detalhada está em andamento, exemplos de criador de perfil de serviço Olá ponteiro de instrução de cada CPU da máquina de saudação em cada milissegundo.
Cada exemplo captura a pilha de chamadas completa de saudação do thread Olá atualmente em execução, fornecendo as informações detalhadas e úteis sobre o que se thread estava fazendo em ambas altos e baixos níveis de abstração. Criador de perfil de serviço também coleta outros eventos como eventos de alternância de contexto, a eventos TPL e a correlação de atividade do pool de threads eventos tootrack e a causalidade.

pilha de chamadas Olá mostrada na exibição de linha do tempo de saudação é resultado de saudação de saudação acima amostragem e instrumentação. Porque cada exemplo captura a pilha de chamadas completa de saudação do thread hello, ele inclui o código do .NET framework do hello, bem como outras estruturas que você faz referência.

### <a id="jitnewobj"></a>Alocação de objeto (`clr!JIT\_New or clr!JIT\_Newarr1`)
`clr!JIT\_New and clr!JIT\_Newarr1`são funções auxiliares dentro do .NET framework que aloca memória do heap gerenciado. `clr!JIT\_New`é chamado quando um objeto é alocado. `clr!JIT\_Newarr1`é invocado quando uma matriz de objeto é alocada. Essas duas funções são geralmente muito rápidas e devem levar uma quantidade relativamente pequena de tempo. Se você vir `clr!JIT\_New` ou `clr!JIT\_Newarr1` levar uma quantidade significativa de tempo na linha do tempo, é uma indicação de que o código de saudação pode ser alocando muitos objetos e consumindo uma quantidade significativa de memória.

### <a id="theprestub"></a>Carregamento de código (`clr!ThePreStub`)
`clr!ThePreStub`é uma função auxiliar dentro do .NET framework que prepara Olá código tooexecute Olá primeira vez. Isso geralmente inclui, mas não se limitando a compilação JIT (apenas no tempo). Para cada método em c#, `clr!ThePreStub` deve ser chamado no máximo uma vez durante o tempo de vida de saudação de um processo.

Se você vir `clr!ThePreStub` leva quantidade significativa de tempo para uma solicitação, indica que a solicitação é Olá a primeira alteração que executa esse método e tempo de saudação para tooload de tempo de execução do .NET framework que o método é significativo. Você pode considerar um processo de aquecimento que executa a parte do código de saudação antes dos usuários acessá-lo ou considere executar NGen em seus assemblies.

### <a id="lockcontention"></a>Contenção de bloqueio (`clr!JITutil\_MonContention` ou `clr!JITutil\_MonEnterWorker`)
`clr!JITutil\_MonContention`ou `clr!JITutil\_MonEnterWorker` indicar Olá atual está esperando um toobe bloqueio liberado. Isso normalmente aparece durante a execução de uma bloqueio instrução c#, invocando o método de monitor. Enter ou invocando um método com o atributo MethodImplOptions. Contenção de bloqueio geralmente acontece quando um do thread adquire um bloqueio e thread B tenta Olá tooacquire mesmo antes de thread A libera de bloqueio.

### <a id="ngencold"></a>Carregamento de código (`[COLD]`)
Se o nome do método hello contém `[COLD]`, como `mscorlib.ni![COLD]System.Reflection.CustomAttribute.IsDefined`, isso significa que esse tempo de execução Olá .NET framework está executando o código que não é otimizado por <a href="https://msdn.microsoft.com/library/e7k32f4k.aspx">Otimização Guiada por perfil</a> para Olá primeira vez. Para cada método, ele deve aparecer no máximo uma vez durante o tempo de vida de saudação do processo de saudação.

Se carregar código leva uma quantidade significativa de tempo para uma solicitação, indica que a solicitação é Olá primeiro tooexecute uma saudação não otimizado parte do método hello. Você pode considerar aquecimento um processo que executa a parte do código de saudação antes dos usuários acessá-lo.

### <a id="httpclientsend"></a>Enviar solicitação HTTP
Métodos como `HttpClient.Send` indicam código hello está aguardando um toocomplete de solicitação HTTP.

### <a id="sqlcommand"></a>Operação de Banco de Dados
Método como SqlCommand.Execute indica código hello está aguardando um toocomplete da operação de banco de dados.

### <a id="await"></a>Aguardando (`AWAIT\_TIME`)
`AWAIT\_TIME`indica o código de saudação está aguardando outro toocomplete de tarefa. Isso geralmente acontece com c# 'await' instrução. Quando o código de saudação não c# 'await' hello thread esvazia e retorna o pool de threads controle toohello e não existe nenhum thread que está bloqueado aguardando Olá 'await' toofinish. No entanto, Olá logicamente thread que fez Olá await é 'bloqueado' aguardando Olá operação toocomplete. O `AWAIT\_TIME` indica o tempo de saudação bloqueado aguardando Olá tarefa toocomplete.

### <a id="block"></a>Tempo bloqueado
`BLOCKED_TIME`indica o código de saudação está aguardando outro toobe de recursos disponível, como aguardando um objeto de sincronização, aguardando um toobe thread disponível ou aguardando um toofinish de solicitação.

### <a id="cpu"></a>Tempo de CPU
Olá CPU está ocupado executando instruções hello.

### <a id="disk"></a>Tempo de disco
aplicativo Hello está executando operações de disco.

### <a id="network"></a>Tempo de rede
aplicativo Hello está executando operações de rede.

### <a id="when"></a>Quando colunas
Isso é uma visualização de como exemplos INCLUSIVOS hello, coletados para um nó variam ao longo do tempo. Olá total de intervalo de solicitação de saudação é dividido em 32 segmentos de tempo e a exemplos inclusivos Olá para esse nó são acumulados nesses buckets 32. Cada bucket, em seguida, é representado como uma barra cuja altura representa um valor de escala. Para nós marcados `CPU_TIME` ou `BLOCKED_TIME`, ou onde há uma relação óbvia de consumo de um recurso (cpu, disco, thread), Olá barra representa consumindo um desses recursos para o período de saudação de bucket. Para essas métricas você pode obter maior que 100%, consumindo vários recursos. Por exemplo, se em média usar duas CPUs em um intervalo você obter 200%.


## <a id="troubleshooting"></a>Solucionar problemas

### <a name="how-can-i-know-whether-application-insights-profiler-is-running"></a>Como saber se o criador de perfil do Application Insights está em execução?

Criador de perfil de saudação é executado como um trabalho web contínuo no aplicativo Web. Você pode abrir o recurso de aplicativo Web hello em https://portal.azure.com e verificar o status de "ApplicationInsightsProfiler" na folha de trabalhos Web hello. Se ele não está em execução, abra **Logs** toofind mais.

### <a name="why-cant-i-find-any-stack-examples-even-though-hello-profiler-is-running"></a>Por que não é possível localizar exemplos pilha mesmo que o criador de perfil hello está em execução?

Aqui estão algumas coisas que você pode verificar.

1. Verifique se seu plano do serviço de aplicativo Web é a camada básica e acima.
2. Verifique se seu aplicativo Web tem o Application Insights SDK 2.2 Beta e acima habilitado.
3. Verifique se que seu aplicativo Web tem a configuração de APPINSIGHTS_INSTRUMENTATIONKEY Olá Olá mesma chave de instrumentação é usado pelo SDK do Application Insights.
4. Verifique se o seu aplicativo Web está em execução no .net Framework 4.6.
5. Se for um aplicativo do ASP.NET Core, verifique também se [Olá necessário dependências](#aspnetcore).

Depois de iniciado o criador de perfil hello, há um período de aquecimento curto quando o criador de perfil de saudação coleta ativamente vários rastreamentos de desempenho. Depois disso, o criador de perfil de saudação coleta rastreamentos de desempenho de dois minutos em cada hora.  

### <a name="i-was-using-azure-service-profiler-what-happened-tooit"></a>Estava usando o criador de perfil de serviço do Azure. Quais tooit com?  

Quando você habilita o criador de perfil do Application Insights, agente do criador de perfil de serviço do Azure está desativado.

### <a id="double-counting"></a>Dois segmentos paralelos de contagem

Em Olá alguns casos métrica de tempo total no Visualizador de pilha Olá é maior que a duração real Olá da solicitação de saudação.

Isso pode acontecer quando há dois ou mais threads associados a uma solicitação, operar em paralelo. tempo total de threads de saudação, em seguida, é maior que o tempo decorrido de saudação. Em muitos casos, um thread pode estar aguardando Olá outros toocomplete. Olá visualizador tentativas toodetect isso e omitir espera não interessam hello, mas falha no lado de saudação do mostrando muito em vez de omitindo o que pode ser informações críticas.  

Quando você vir threads paralelos em seus rastreamentos, é necessário toodetermine que threads estão esperando para que possa determinar o caminho crítico de saudação para solicitação de saudação. Na maioria dos casos, o thread de saudação rapidamente entrar em estado de espera é simplesmente aguardando Olá outros threads. Concentre Olá outros e ignorar o tempo de saudação em threads de espera de saudação.

### <a id="issue-loading-trace-in-viewer"></a>Nenhum dado de criação de perfil

1. Se dados saudação que você está tentando tooview é mais de duas semanas, tente limitar seu filtro de tempo e tente novamente.

2. Verificação de proxies ou um firewall não ter bloqueado toohttps://gateway.azureserviceprofiler.net acesso.

3. Verifique que Olá Application Insights é de chave de instrumentação que você está usando em seu aplicativo hello mesmo como Olá recurso do Application Insights que você tiver habilitado a criação de perfil com. chave de saudação geralmente está no applicationinsights. config, mas também pode ser encontrada no App. config ou Web. config.

### <a name="error-report-in-hello-profiling-viewer"></a>Relatório de erro no Visualizador de criação de perfil de saudação

Um tíquete de suporte do portal de saudação do arquivo. Inclua Olá ID de correlação da mensagem de saudação do erro.

## <a name="manual-installation"></a>Instalação manual

Quando você configura o criador de perfil hello, hello seguintes atualizações são feitas configurações do aplicativo da Web toohello. Você mesmo pode fazê-las manualmente se o ambiente exigir. Por exemplo, se o aplicativo for executado em um ASE (Ambiente do Serviço de Aplicativo do Azure):

1. Na folha de controle de aplicativo de web hello, abra as configurações.
2. Defina ".Net Framework versão" toov4.6.
3. Definir tooOn "Sempre ativos".
4. Adicionar configuração de aplicativo "__APPINSIGHTS_INSTRUMENTATIONKEY__" e o conjunto Olá valor toohello mesma chave de instrumentação é usado pelo Olá SDK.
5. Abra Ferramentas Avançadas.
6. Clique em "Ir" tooopen Olá Kudu site da Web.
7. No site do Kudu hello, selecione "Extensões de Site".
8. Instale o “__Application Insights__” por meio da Galeria.
9. Reinicie o aplicativo da web de saudação.

## <a id="aspnetcore"></a>Suporte do ASP.NET Core

Aplicativo do ASP.NET Core precisa tooinstall 2.1.0-beta6 de pacote do Microsoft.ApplicationInsights.AspNetCore Nuget ou superior toowork com hello criador de perfil. Nós não suportar versões inferiores Olá após 27/6/2017.

## <a name="next-steps"></a>Próximas etapas

* [Trabalhar com o Application Insights no Visual Studio](https://docs.microsoft.com/azure/application-insights/app-insights-visual-studio)

[performance-blade]: ./media/app-insights-profiler/performance-blade.png
[performance-blade-examples]: ./media/app-insights-profiler/performance-blade-examples.png
[trace-explorer]: ./media/app-insights-profiler/trace-explorer.png
[trace-explorer-toolbar]: ./media/app-insights-profiler/trace-explorer-toolbar.png
[trace-explorer-hint-tip]: ./media/app-insights-profiler/trace-explorer-hint-tip.png
[trace-explorer-hot-path]: ./media/app-insights-profiler/trace-explorer-hot-path.png
[enable-profiler-banner]: ./media/app-insights-profiler/enable-profiler-banner.png
[disable-profiler-webjob]: ./media/app-insights-profiler/disable-profiler-webjob.png
[linked app services]: ./media/app-insights-profiler/linked-app-services.png
