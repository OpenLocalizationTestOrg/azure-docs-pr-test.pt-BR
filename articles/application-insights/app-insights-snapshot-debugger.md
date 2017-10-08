---
title: "aaaAzure depurador de instantâneo de informações do aplicativo para aplicativos .NET | Microsoft Docs"
description: "Depure instantâneos são coletados automaticamente quando exceções forem geradas na produção de aplicativos .NET"
services: application-insights
documentationcenter: 
author: qubitron
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 07/03/2017
ms.author: bwren
ms.openlocfilehash: f0173a752b5795d934fbab1bd53eb077433edc90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-snapshots-on-exceptions-in-net-apps"></a>Depurar instantâneos em exceções em aplicativos .NET

Quando ocorrer uma exceção, você pode coletar automaticamente um Instantâneo de Depuração de seu aplicativo web ativo. instantâneo Olá mostra o estado de saudação do código-fonte e variáveis na exceção de saudação do momento Olá foi lançada. Olá depurador de instantâneo (visualização) em [Azure Application Insights](app-insights-overview.md) monitora a telemetria de exceção de seu aplicativo web. Ele coleta instantâneos na sua parte superior-Lançando exceções para que você tenha informações Olá necessárias toodiagnose problemas em produção. Incluir Olá [pacote de NuGet de coletor de instantâneo](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) em seu aplicativo e, opcionalmente, configurar parâmetros de coleta em [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md). Instantâneos exibidos em [exceções](app-insights-asp-net-exceptions.md) no portal do Application Insights hello.

Você pode exibir instantâneos de depuração na pilha de chamadas de Olá Olá toosee portal e inspecionar variáveis em cada quadro de pilha de chamadas. tooget uma experiência de depuração mais eficiente com o código-fonte, abra instantâneos com Visual Studio 2017 Enterprise por [baixar a extensão de depurador instantâneo Olá para Visual Studio](https://aka.ms/snapshotdebugger).

Coleta de instantâneo está disponível para:
* Aplicativos ASP.NET e do .NET framework com o .NET Framework 4.5 ou posterior.
* Aplicativos do .NET Core 2.0 e Núcleo do ASP.NET Core 2.0 em execução no Windows.

### <a name="configure-snapshot-collection-for-aspnet-applications"></a>Configurar a coleta de instantâneo para aplicativos ASP.NET

1. [Habilite o Application Insights no seu aplicativo web](app-insights-asp-net.md), se você ainda não tiver feito isso.

2. Incluir Olá [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pacote NuGet em seu aplicativo. 

3. Examinar opções padrão Olá Olá pacote adicionado muito[Applicationinsights](app-insights-configuration-with-applicationinsights-config.md):

    ```xml
    <TelemetryProcessors>
        <Add Type="Microsoft.ApplicationInsights.SnapshotCollector.SnapshotCollectorTelemetryProcessor, Microsoft.ApplicationInsights.SnapshotCollector">
        <!-- hello default is true, but you can disable Snapshot Debugging by setting it toofalse -->
        <IsEnabled>true</IsEnabled>
        <!-- Snapshot Debugging is usually disabled in developer mode, but you can enable it by setting this tootrue. -->
        <!-- DeveloperMode is a property on hello active TelemetryChannel. -->
        <IsEnabledInDeveloperMode>false</IsEnabledInDeveloperMode>
        <!-- How many times we need toosee an exception before we ask for snapshots. -->
        <ThresholdForSnapshotting>5</ThresholdForSnapshotting>
        <!-- hello maximum number of examples we create for a single problem. -->
        <MaximumSnapshotsRequired>3</MaximumSnapshotsRequired>
        <!-- hello maximum number of problems that we can be tracking at any time. -->
        <MaximumCollectionPlanSize>50</MaximumCollectionPlanSize>
        <!-- How often tooreset problem counters. -->
        <ProblemCounterResetInterval>06:00:00</ProblemCounterResetInterval>
        <!-- hello maximum number of snapshots allowed in one minute. -->
        <SnapshotsPerMinuteLimit>2</SnapshotsPerMinuteLimit>
        <!-- hello maximum number of snapshots allowed per day. -->
        <SnapshotsPerDayLimit>50</SnapshotsPerDayLimit>
        </Add>
    </TelemetryProcessors>
    ```

4. Os instantâneos são coletados apenas em exceções que são relatados tooApplication Insights. Em alguns casos (por exemplo, versões mais antigas da plataforma de .NET Olá), talvez seja necessário muito[configurar coleta de exceção](app-insights-asp-net-exceptions.md#exceptions) toosee exceções com instantâneos no portal de saudação.


### <a name="configure-snapshot-collection-for-aspnet-core-20-applications"></a>Configurar a coleta de instantâneo para aplicativos do Núcleo do ASP.NET 2.0

1. [Habilite o Application Insights no seu aplicativo web Núcleo do ASP.NET](app-insights-asp-net-core.md), se você ainda não tiver feito isso.

2. Incluir Olá [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pacote NuGet em seu aplicativo.

3. Modificar Olá `ConfigureServices` método em seu aplicativo `Startup` classe processador de telemetria do coletor do instantâneo tooadd hello. código Hello, você deve adicionar depende da versão referenciada Olá Olá pacote Microsoft.ApplicationInsights.ASPNETCore NuGet.

   Para Microsoft.ApplicationInsights.AspNetCore 2.1.0, adicione:
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
           services.AddSingleton<Func<ITelemetryProcessor, ITelemetryProcessor>>(next => new SnapshotCollectorTelemetryProcessor(next));
           // TODO: Add any other services your application needs here.
       }
   }
   ```

   Para Microsoft.ApplicationInsights.AspNetCore 2.1.1, adicione:
   ```C#
   using Microsoft.ApplicationInsights.SnapshotCollector;
   ...
   class Startup
   {
       private class SnapshotCollectorTelemetryProcessorFactory : ITelemetryProcessorFactory
       {
           public ITelemetryProcessor Create(ITelemetryProcessor next) =>
               new SnapshotCollectorTelemetryProcessor(next);
       }

       // This method is called by hello runtime. Use it tooadd services toohello container.
       public void ConfigureServices(IServiceCollection services)
       {
            services.AddSingleton<ITelemetryProcessorFactory>(new SnapshotCollectorTelemetryProcessorFactory());
           // TODO: Add any other services your application needs here.
       }
   }
   ```

### <a name="configure-snapshot-collection-for-other-net-applications"></a>Configurar a coleta de instantâneo para outros aplicativos .NET

1. Se seu aplicativo já não está instrumentado com o Application Insights, começar por [habilitando o Application Insights e chave de instrumentação Olá configuração](app-insights-windows-desktop.md).

2. Adicionar Olá [Microsoft.ApplicationInsights.SnapshotCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.SnapshotCollector) pacote NuGet em seu aplicativo.

3. Os instantâneos são coletados apenas em exceções que são relatados tooApplication Insights. Talvez seja necessário toomodify tooreport seu código-los. código de tratamento de exceção de saudação depende da estrutura de saudação do seu aplicativo, mas é um exemplo abaixo:
    ```C#
   TelemetryClient _telemetryClient = new TelemetryClient();

   void ExampleRequest()
   {
        try
        {
            // TODO: Handle hello request.
        }
        catch (Exception ex)
        {
            // Report hello exception tooApplication Insights.
            _telemetryClient.TrackException(ex);

            // TODO: Rethrow hello exception if desired.
        }
   }
    ```
    
## <a name="grant-permissions"></a>Conceder permissões

Os proprietários de saudação assinatura do Azure podem inspecionar instantâneos. Outros usuários devem ter permissão de um proprietário.

permissão toogrant, atribuir Olá `Application Insights Snapshot Debugger` toousers de função que irá inspecionar instantâneos. Essa função pode ser atribuída tooindividual usuários ou grupos através de proprietários de assinatura de destino Olá recurso do Application Insights ou seu grupo de recursos ou a assinatura.

1. Abra a folha de controle de acesso (IAM) hello.
1. Clique em Olá + botão Adicionar.
1. Selecione depurador de instantâneo de informações do aplicativo na lista suspensa de funções da saudação.
1. Procure e insira um nome para Olá tooadd de usuário.
1. Clique em Olá Salvar botão tooadd Olá usuário toohello função.


[!IMPORTANT]
    Os instantâneos potencialmente podem conter informações pessoais e outras informações confidenciais em valores de parâmetro e variável.

## <a name="debug-snapshots-in-hello-application-insights-portal"></a>Depurar instantâneos no portal do Application Insights Olá

Se um instantâneo está disponível para uma determinada exceção ou uma ID do problema, um **abrir instantâneo depurar** botão aparece no hello [exceção](app-insights-asp-net-exceptions.md) no portal do Application Insights hello.

![Botão Abrir Instantâneo de Depuração na exceção](./media/app-insights-snapshot-debugger/snapshot-on-exception.png)

Olá exibição de instantâneo de depuração, verá uma pilha de chamadas e um painel variáveis. Quando você seleciona quadros de chamada de saudação de pilha no painel de pilha de chamada hello, você pode exibir as variáveis locais e parâmetros para essa função é chamada no painel de variáveis de saudação.

![Exibir instantâneo depurar no portal de saudação](./media/app-insights-snapshot-debugger/open-snapshot-portal.png)

Os instantâneos podem conter informações confidenciais e, por padrão, não estão visíveis. tooview instantâneos, você deve ter Olá `Application Insights Snapshot Debugger` tooyou função atribuída.

## <a name="debug-snapshots-with-visual-studio-2017-enterprise"></a>Depurar instantâneos com o Visual Studio 2017 Enterprise
1. Clique em Olá **baixar instantâneo** toodownload botão um `.diagsession` arquivo, que pode ser aberto pelo Visual Studio Enterprise de 2017. 

2. Olá tooopen `.diagsession` arquivo, você deve primeiro [baixar e instalar a extensão de depurador de instantâneo de saudação do Visual Studio](https://aka.ms/snapshotdebugger).

3. Depois de abrir o arquivo de instantâneo hello, página de depuração de minidespejo Olá no Visual Studio é exibida. Clique em **depurar código gerenciado** toostart depuração instantâneo hello. instantâneo Olá abre toohello de linha de código onde a exceção de saudação foi gerada para que você pode depurar o estado atual de saudação do processo de saudação.

    ![Exibir instantâneo de depuração no Visual Studio](./media/app-insights-snapshot-debugger/open-snapshot-visualstudio.png)

instantâneo baixados Olá contém os arquivos de símbolo que foram encontrados no servidor de aplicativos web. Esses arquivos de símbolo são dados de instantâneo tooassociate necessárias ao código-fonte. Para aplicativos de serviço de aplicativo, tornam a implantação de símbolo de tooenable-se de que quando você publicar seus aplicativos web.

## <a name="how-snapshots-work"></a>Como os instantâneos funcionam

Quando seu aplicativo é iniciado, é criado um processo separado de carregador de instantâneos que monitora seu aplicativo quanto a solicitações de instantâneos. Quando um instantâneo é solicitado, é feita uma cópia de sombra de saudação executando o processo em cerca de 10 minutos de too20. processo de sombra Olá é analisado e um instantâneo é criado durante o processo principal Olá continua toorun e servir toousers de tráfego. Olá instantâneo for carregado tooApplication Insights junto com todos os arquivos relevantes de símbolo (. PDB) que são necessárias tooview instantâneo hello.

## <a name="current-limitations"></a>Limitações atuais

### <a name="publish-symbols"></a>Publicar símbolos
Olá depurador instantâneo requer arquivos de símbolo em variáveis de toodecode de servidor de produção de hello e tooprovide uma experiência de depuração no Visual Studio. versão de Hello 15.2 do Visual Studio de 2017 publica símbolos para compilações de versão por padrão quando ele é publicado tooApp serviço. Em versões anteriores, você precisa fazer tooadd Olá seguinte perfil de publicação de linha tooyour `.pubxml` arquivos de forma que os símbolos são publicados no modo de liberação:

```xml
    <ExcludeGeneratedDebugSymbol>False</ExcludeGeneratedDebugSymbol>
```

Para outros tipos e computação do Azure, verifique se os arquivos de símbolo de saudação estão em Olá mesma pasta do. dll do aplicativo principal hello (normalmente, `wwwroot/bin`) ou estão disponíveis no caminho atual hello.

### <a name="optimized-builds"></a>Builds otimizados
Em alguns casos, variáveis locais não podem ser exibidas nas compilações de lançamento devido a otimizações que são aplicadas durante o processo de compilação hello.

## <a name="troubleshooting"></a>Solucionar problemas

Estas dicas ajudarão-lo a solucionar problemas com hello depurador de instantâneo.

### <a name="verify-hello-instrumentation-key"></a>Verifique se a chave de instrumentação Olá

Certifique-se de que você está usando a chave de instrumentação correto de saudação em seu aplicativo publicado. Geralmente, Application Insights lê chave de instrumentação de saudação do arquivo applicationinsights. config de saudação. Verifique se que o valor de saudação é Olá mesmo como chave de instrumentação de saudação do recurso do Application Insights Olá que você vê no portal de saudação.

### <a name="check-hello-uploader-logs"></a>Verifique os logs de carregador Olá

Depois que um instantâneo é criado, um arquivo de minidespejo (. dmp) é criado no disco. Um processo separado do carregador usa esse arquivo de minidespejo e carrega, juntamente com qualquer PDBs associados, tooApplication armazenamento de Insights instantâneo depurador. Após o minidespejo Olá foi carregado com êxito, ele é excluído do disco. arquivos de log de saudação de carregador de minidespejo Olá são mantidos em disco. Em um ambiente de Serviço de Aplicativo, você pode encontrar esses logs em `D:\Home\LogFiles\Uploader_*.log`. Site de gerenciamento do uso Olá Kudu para o serviço de aplicativo toofind esses arquivos de log.

1. Abra o aplicativo de serviço de aplicativo em Olá portal do Azure.

2. Selecione Olá **ferramentas avançadas de** folha ou procurar **Kudu**.
3. Clique em **Ir**.
4. Em Olá **console de depuração** caixa de listagem suspensa, selecione **CMD**.
5. Clique em **Arquivos de Log**.

Você deverá ver pelo menos um arquivo com um nome que começa com `Uploader_` e uma extensão `.log`. Clique em toodownload de ícone apropriado Olá os arquivos de log ou abri-los em um navegador.
nome de arquivo Hello inclui o nome da máquina hello. Se a instância do Serviço de Aplicativo é hospedada em mais de uma máquina, há arquivos de log separados para cada máquina. Quando o carregador de saudação detecta um novo arquivo de minidespejo, ele será registrado no arquivo de log de saudação. Aqui está um exemplo de um upload bem-sucedido:

```
MinidumpUploader.exe Information: 0 : Dump available 139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:08.0349846Z
MinidumpUploader.exe Information: 0 : Uploading D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp, 329.12 MB
    DateTime=2017-05-25T14:25:16.0145444Z
MinidumpUploader.exe Information: 0 : Upload successful.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Extracting PDB info from D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp.
    DateTime=2017-05-25T14:25:42.9164120Z
MinidumpUploader.exe Information: 0 : Matched 2 PDB(s) with local files.
    DateTime=2017-05-25T14:25:44.2310982Z
MinidumpUploader.exe Information: 0 : Stamp does not want any of our matched PDBs.
    DateTime=2017-05-25T14:25:44.5435948Z
MinidumpUploader.exe Information: 0 : Deleted D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\139e411a23934dc0b9ea08a626db16c5.dmp
    DateTime=2017-05-25T14:25:44.6095821Z
```

No exemplo anterior de saudação, chave de instrumentação Olá é `c12a605e73c44346a984e00000000000`. Esse valor deve corresponder a chave de instrumentação Olá para seu aplicativo.
minidespejo Hello está associado um instantâneo com a ID de saudação `139e411a23934dc0b9ea08a626db16c5`. Você pode usar essa ID posterior Olá de toolocate associados a telemetria de exceção no Application Insights análise.

carregador de saudação procura novos PDBs sobre uma vez a cada 15 minutos. Aqui está um exemplo:

```
MinidumpUploader.exe Information: 0 : PDB rescan requested.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\home\site\wwwroot\ for local PDBs.
    DateTime=2017-05-25T15:11:38.8003886Z
MinidumpUploader.exe Information: 0 : Scanning D:\local\Temporary ASP.NET Files\root\a6554c94\e3ad6f22\assembly\dl3\81d5008b\00b93cc8_dec5d201 for local PDBs.
    DateTime=2017-05-25T15:11:38.8160276Z
MinidumpUploader.exe Information: 0 : Local PDB scan complete. Found 2 PDB(s).
    DateTime=2017-05-25T15:11:38.8316450Z
MinidumpUploader.exe Information: 0 : Deleted PDB scan marker D:\local\Temp\Dumps\c12a605e73c44346a984e00000000000\.pdbscan.
    DateTime=2017-05-25T15:11:38.8316450Z
```

Para aplicativos que são _não_ hospedado no serviço de aplicativo, logs de carregador Olá estão em Olá mesma pasta Olá minidespejos: `%TEMP%\Dumps\<ikey>` (onde `<ikey>` é a sua chave de instrumentação).

### <a name="use-application-insights-search-toofind-exceptions-with-snapshots"></a>Use o Application Insights pesquisar exceções toofind com instantâneos

Quando um instantâneo é criado, Olá lançando a exceção é marcado com uma ID de instantâneo. Quando a telemetria de exceção Olá é relatado tooApplication Insights, essa ID de instantâneo é incluída como uma propriedade personalizada. Usando a folha de pesquisa Olá no Application Insights, você pode localizar toda a telemetria com hello `ai.snapshot.id` propriedade personalizada.

1. Procure o recurso Application Insights tooyour Olá portal do Azure.
2. Clique em **Pesquisar**.
3. Tipo `ai.snapshot.id` em Olá caixa de texto de pesquisa e pressione Enter.

![Pesquisar telemetria com uma ID de instantâneo no portal de saudação](./media/app-insights-snapshot-debugger/search-snapshot-portal.png)

Se a pesquisa não retornar resultados, nenhum instantâneo foi relatado tooApplication Insights para seu aplicativo no intervalo de tempo de saudação selecionado.

toosearch para uma ID de instantâneo específicos de logs de carregador hello, digite o ID na caixa de pesquisa de saudação. Se você não conseguir localizar telemetria para um instantâneo que você sabe que foi carregado, siga estas etapas:

1. Verifique que você está olhando de recurso do Application Insights correta Olá verificando a chave de instrumentação hello.

2. Usando Olá timestamp do log de carregador hello, ajuste o filtro de intervalo de tempo de saudação do hello pesquisa toocover esse intervalo de tempo.

Se você não vir uma exceção com essa ID de instantâneo, telemetria de exceção Olá não foi relatado tooApplication Insights. Essa situação pode ocorrer se o aplicativo falhou após levou instantâneo hello, mas antes de ela relatou a telemetria de exceção de saudação. Nesse caso, verifique Olá logs de serviço de aplicativo em `Diagnose and solve problems` toosee se houvesse inesperado reinicia ou exceções sem tratamento.

## <a name="next-steps"></a>Próximas etapas

* [Definir snappoints em seu código](https://azure.microsoft.com/blog/snapshot-debugger-for-azure/) tooget instantâneos sem esperar por uma exceção.
* [Diagnosticar exceções em seus aplicativos web](app-insights-asp-net-exceptions.md) explica como toomake tooApplication visíveis de exceções mais informações. 
* A [Detecção Inteligente](app-insights-proactive-diagnostics.md) descobre automaticamente anomalias de desempenho.
